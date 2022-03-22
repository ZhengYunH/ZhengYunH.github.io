# 多线程

+ FRunnable
+ AsyncTask
+ TaskGraph

## FRunnable

> https://unrealcommunity.wiki/multithreading-with-frunnable-2a4xuf68

Runnable是最直接的线程执行方式，不提供任何的管理。

#### 定义

```c++
class CORE_API FRunnable
{
public:
    virtual bool Init() { ... }
    virtual uint32 Run() = 0;
    virtual void Stop() { }
    virtual void Exit() { }
}
```

Runnable只是线程执行的逻辑单元，而不是真正的线程。换句话说，Runnable给线程中提供具体的执行内容，而真正的线程是RunnableThread。

#### 使用

自定义Runnable

```c++
class GAME_API FMyWorker : public FRunnable
{
public:
    FMyWork() { Thread = FRunnableThread::Create(this, TEXT("MyWork Name")); }
    virtual ~FMyWorker() override { Thread->Kill(); delete Thread; }
    bool Init() override { return true; }
    uint32 Run() override 
    { 
        while (bRunThread)
        {
            FPlatformProcess::Sleep(1.0f);
        }  
        return 0;
    }
    void Stop() override { bRunThread = false; }
private:
    FRunnableThread* Thread;
    bool bRunThread{ true };
}
```

使用Runnable：在需要使用Runnable的地方直接new

```c++
FMyWorker* Worker = new FMyWorker();
...
delete Worker;
```

## AsyncTask

> https://zhuanlan.zhihu.com/p/38881269

```c++
/* AsyncWork.h */
template<typename TTask>
class FAsyncTask: private IQueuedWork {...}

/* ThreadingBase.cpp */
class FQueuedThread : public FRunnable { ... }

class FQueuedThreadPoolBase : public FQueuedThreadPool
{
protected:
   TArray<IQueuedWork*> QueuedWork;
   TArray<FQueuedThread*> QueuedThreads;
   ...
}
```

首先需要理清QueuedThreadPoolBase \ QueuedThread \ AsyncTask三者的关系：

UE中自己实现了一个线程池QueuedThreadPoolBase （经典的Queue实现），池中保存着任务队列QueuedWork和线程队列QueuedThreads。

根据以上继承和组合关系可以这样描述他们的关系：QueuedThreadPool管理着两个队列，任务队列QueueThread和线程队列IQueueWork，而AsynTask是IQueueWork的子类，也就是其中的一种实现。

类比上面的Runnable，AsyncTask像是被单独抽离出来的Runnable，但不依托于某个Thread（Runnable中需要自己Create Thread）。具体使用哪个Thread，由类似于Manager的QueuedThreadPool进行分发管理。

QueuedThread是由信号驱动的，当来了任务的时候才进行处理，平时都是处于Wait的状态（见FQueuedThread::Run）。

对于Pool，在游戏一开始会创建几个主要的Pool：其中包含服务器、编辑器、IO等（见FEngineLoop.PreInit）

#### 定义

```c++
template<typename TTask>
class FAsyncTask : private IQueuedWork
{
    TTask Task;
    FThreadSafeCounter	WorkNotFinishedCounter;
    FEvent*				DoneEvent;
    FQueuedThreadPool*	QueuedPool;
    ...
    void DoWork()
	{	
		...
		Task.DoWork();		
		...
	}
    ...
}
```

主要关注其中的成员变量。AsyncTask是个模板类，真正执行逻辑的位置是传入的Task。具体在AsyncTask::DoWork方法中执行传入的Task执行DoWork方法（因此只需要传入的TTask包含DoTask方法即可）。

#### 使用

```c++
class MyTask : public FNonAbandonableTask
{
    friend class FAsyncTask<MyTask>;
    
    int32 InExampleData;
    ExampleAsyncTask(int32 InExampleData)
		 : ExampleData(InExampleData)
	{
	}
    
    void DoWork()
	{
    }
    
    FORCEINLINE TStatId GetStatId() const
	{
		RETURN_QUICK_DECLARE_CYCLE_STAT(ExampleAsyncTask, STATGROUP_ThreadPoolAsyncTasks);
	}
}

FAsyncTask<ExampleAsyncTask>* MyTask = new FAsyncTask<ExampleAsyncTask>( 5 );
MyTask->StartBackgroundTask(); // 如果想在同一线程执行可使用MyTask->StartSynchronousTask();
MyTask->EnsureCompletion(); //  Wait until the job is complete
delete Task;
```

其中GetStatId是通用写法，只需要将并行逻辑写在DoWork中即可。另外如果想指定Pool，而可以在StartBackgroundTask中传入。

## TaskGraph

> https://www.cnblogs.com/shiroe/p/14723592.html

TaskGraph是一套更加抽象的异步处理系统，可以处理任务间的顺序和依赖，适合简单的任务（不然可能会阻塞主线程的执行），复杂的任务应使用Runnable和AsyncTask

#### 定义

```c++
/* TaskGraphInterfaces.h */
template<typename TTask>
class TGraphTask final : public FBaseGraphTask {}
```

类似AsyncTask，TaskGraph也是在Task中执行具体逻辑。

#### 使用

```c++
class FGenericTask
{
	TSomeType	SomeArgument;
public:
	FGenericTask(TSomeType InSomeArgument) 
		: SomeArgument(InSomeArgument)
	{
	}
	~FGenericTask()
	{
	}
	FORCEINLINE TStatId GetStatId() const
	{
		RETURN_QUICK_DECLARE_CYCLE_STAT(FGenericTask, STATGROUP_TaskGraphTasks);
	}

	[static] ENamedThreads::Type GetDesiredThread()
	{
		return ENamedThreads::[named thread or AnyThread];
	}
	void DoTask(ENamedThreads::Type CurrentThread, const FGraphEventRef& MyCompletionGraphEvent)
	{
		MyCompletionGraphEvent->DontCompleteUntil(TGraphTask<FSomeChildTask>::CreateTask(NULL,CurrentThread).ConstructAndDispatchWhenReady());
	}
};

FGraphEventRef GraphEventRef = TGraphTask<FTaskGraph_SimpleTask>::CreateTask().ConstructAndDispatchWhenReady(ThreadName);
```

创建一个TaskGraph执行的线程需要包括两步（见DoTask）：`CreateTask`以及返回对象中的方法（以上为`ConstructAndDispatchWhenReady`）

对于`CreateTask`中包含两个参数：

+ Prerequisites：用来指定该任务依赖的事件数组，当依赖事件都被触发之后，该任务才会被放到任务队列里执行
+ ENamedThreads::Type：传入当前所在得线程，默认为空即可，在Enqueue中会自动处理空的情况

TGraphTask::CreateTask()返回的对象中包含两种不同的方法： 

+ `ConstructAndDispatchWhenReady`：创建任务后立即执行
+ `ConstructAndHold`：创建任务后挂起，等待Unlock唤醒。

利用Prerequisite和`ConstructAndHold`两个方法，就可以建立起任务之间的依赖了。



最后介绍一个依赖于TaskGraph的并行函数ParallelFor，在引擎很多地方用到，一个Helper函数用于遍历数组。

## 小结

对于最直接使用多线程的方法，可以直接用FRunnable处理。如果需要用到线程池，可以利用AsyncTask。对于需要处理依赖的任务，使用TaskGraph是最好的选择。
