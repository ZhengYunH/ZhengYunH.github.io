# 基础概念解释

### Outer（外部对象）

**Outer**语义上的含义即拥有当前Object的Object，可以称之为**外部对象**。有些资料可能会将其翻译为父对象，但父对象的说法容易与继承冲突，这里为了区分组合和继承，排除父对象的说法，仅使用外部对象的说法。

一个Object可能会有很多地方引用，但是Outer有且仅有一个。Outer作为Object的持有者，它控制着Object的生命周期，并且在序列化时，Object的数据会被保存在Outer中，其它引用Object的对象仅保存路径。

Outer本身也是Object，那Outer的Outer...一直到最外层的Outer，我们称之为**OuterMost**（类似继承链中最基础的那个类型）。OuterMost一定是UPackage类型。

**例子：**

我们新建了一个Level，在Level中拖入了一些Actor。那这些Actor的Outer就是这个Level，另外Actor中的Component将Actor作为Outer。但这些Actor和Level存在于某个Package中（ .BP / .umap），这些Package就是OuterMost。

### Package（包）

Package对应磁盘上的一个.uasset资源文件，或全局临时包（TransientPackage）。如果ObjectA属于某个Package，Package实际指示了在物理上这个对象的存储位置。想象一下，Package占用了一大块内存，而其中一段连续的内存划出来交给ObjectA，也就是说ObjectA被包含在Package中，Object和Package之间存在真正的内外关系，而Outer则是一个逻辑概念，在内存中没有真正的包含关系。

**例子：**

对于名为 /Game/SomeDirectory/SomePackage.SomeObject:SubObject 的对象路径。

+ SomePackage：为Package的对象名称
+ SomeObject：该Package中顶层对象
+ SubObject：SomeObject的一个子对象

### Archetype（原型）& CDO（类默认对象）

#### Archetype

说到原型，就能想到设计模式中的[原型模式](https://refactoringguru.cn/design-patterns/prototype)。简而言之就是提供一个模板对象、抄作业的答案，在实例化对象的时候直接拷贝Archetype中的数据，速度比重新调用构造函数快。类似于拷贝构造函数的概念，但相对于前者，Archetype可以处理“新对象是派生类”的情况，也就是说可以利用父类的数据作为子类（新产生的）的Archetype，初始化其类成员。

通常而言，当描述Template时，与Archetype大部分情况下是等价的。

#### CDO

对于任何的继承于UObject的类，都存在一个默认的对象，它由引擎自动创建（注册类的过程中会创建），这个对象就称为CDO。CDO的意义在于为类提供默认值，当我们编辑蓝图的属性时，实际修改的是蓝图类的CDO；当创建一个新对象时，直接利用CDO拷贝数值生成实例。可以想到，当保存实例（比如在Level中）或者进行网络传输时，只需要处理修改过的内容。

总结起来是一个很直观的逻辑：存在这样一个前提——大部分类属性是不会被修改的，因此我们对实例化对象的成员进行赋值时只需要Base + Diff。这个Base就是CDO，Diff就是具体存储的内容。

#### 对比

关于Archetype和CDO二者容易产生混淆，在此做一个区分的阐述。

Archetype是实例化对象时的模板，而CDO是属于类本身的特定属性。换句话说，Archetype定义在对象的范畴，而CDO则是定义在类的范畴。通常情况下，对象的Archetype就是类的CDO，但有一些特殊情况下Archetype和CDO是不同的：

1. 当创建类CDO时，与普通创建Object走的逻辑是一致的，因此CDO的创建也会提供一个Archetype。此时CDO的Archetype就是其父类的CDO，也就是Class利用父类的CDO来创建其CDO
2. 当我们在New Object的过程中传入Template参数，用于实例化对象，则此对象的Archetype为传入的Template

### Reference（引用）

#### Object Reference（对象引用） & Class Reference（类引用）

当在蓝图中新增Object类型变量时（例如Actor），会出现Object Reference \ Class Reference \ Soft Object Reference \ Soft Class Reference可供选择。

+ Object Reference：直接引用一个具体的实例，例如场景中的某个具体的对象。
+ Class Reference：用于指定特定的Class类型，例如我们需要在BP中Spawn特定的类型Actor，就可以暴露这种类型的变量。

类比于C++代码，Object Reference为Actor*，而Class Reference则类比于TSubclassOf。

对于另外两个Soft开头的类型，其实是前面二者的软引用方式。Object Reference \ Class Reference 是硬引用，当加载BP的时候就会加载所有需要使用到的资源，包含变量中的引用，而使用Soft类型可以利用异步资源加载的方式减少BP加载时的卡顿。

#### 实例化引用 和 普通引用

对于使用 UPROPERTY(Instanced) 修饰的UObject* 引用称为**实例化引用**，否则就是**普通引用**。

在实例化对象时，会利用类的CDO作为模板创建对象（如上CDO所述），**普通引用**直接通过CDO中同名属性拷贝引用，而**实例化引用**则会由CDO中同名引用的对象作为Template创建子对象。

另外，如果类自身标记为UCLASS(**DefaultToInstanced**)，无论指向它的是什么引用都会进行实例化。

### SubObject（子对象）

#### 原型子对象 和 实例子对象

这两个子对象的概念都是对于实例化引用而言。

对于存在一个**实例化引用**的对象，可以在编辑器中创建具体实例化的子对象。也就是说，蓝图CDO会包含一个特殊的子对象，作为实例化引用的Archetype，并序列化到蓝图文件中，这个对象称为**原型子对象**。

在创建蓝图类对象时，蓝图类对象中的实例化引用，会以蓝图类 CDO 中实例化引用指向的**原型子对象**作为模板，来为自己创建新的**实例子对象**。换句话说，**原型子对象**是针对于蓝图CDO的，而**实例子对象**则是针对于具体的对象的。

#### 默认子对象

也就是常用的子对象初始化接口`CreateDefaultSubObject`所产生的对象。仅能在UObject的Native构造函数中，调用该函数创建默认子对象。默认子对象有以下特性：

1. 位于CDO中，且创建默认子对象时要显示指定对象名
2. 蓝图类的CDO中所有默认子对象和原型子对象，回和蓝图类的CDO序列化在一起

因此，默认子对象是位于CDO中，一个路径稳定，并且和蓝图CDO序列化在一起的子对象。

