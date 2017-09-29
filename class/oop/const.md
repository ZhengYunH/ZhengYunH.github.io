# 常元 const
## const 修饰成员变量
1. 定义常量
`TYPE const ValueName=value;`
`const TYPE ValueName=valuel;`
等价，const修饰的类型为TYPE的变量value是不可变的。

2. 指针使用const
+ 指针本身不可变 `char* const p`
+ 指针所指向的内容不可变 `const char *p`
+ 两者都不可变 `const char* const p`
+ 区别方法，沿着`*`划一条线
    * const 在 `*` 左侧，修饰的是指针对应的常量
    * const 在 `*` 右侧，修饰的是指针本身

## const 修饰函数参数  
传递过来的参数在函数内不可以改变，与上面修饰变量时的性质一样。
```
void function(const int Var);
void function(const char* Var);
void function(char* const Var);
```

## const 修饰函数返回值
const修饰函数返回值其实用的并不是很多，它的含义和const修饰普通变量以及指针的含义基本相同。
```
const int fun1() //这个其实无意义，因为参数返回本身就是赋值。
const int * fun2() //调用时 const int *pValue = fun2(); 我们可以把fun2()看作成一个变量，即指针内容不可变。
int* const fun3()   //调用时 int * const pValue = fun2(); 我们可以把fun2()看作成一个变量，即指针本身不可变。
void function(const Class& Var); //引用参数在函数内不可以改变
void function(const TYPE& Var); //引用参数在函数内为常量不可变
```

对值传递来说，加const没有任何意义

## const 修饰成员函数  
1. const修饰的成员函数不能修改任何的成员变量(`mutable`修饰的变量除外)
2. const成员函数不能调用非const成员函数，因为非const成员函数可以修改成员变量
```
void function()const; //它不改变对象的成员变量,也不能调用常成员函数, 类中任何非const成员函数。
```

## const 修饰类对象/对象指针/对象引用
+ const修饰类对象表示该对象为常量对象，其中的任何成员都不能被修改。对于对象指针和对象引用也是一样。
+   const修饰的对象，该对象的任何非const成员函数都不能被调用，因为任何非const成员函数会有修改成员变量的企图。
```
class AAA
{ 
    void func1(); 
    void func2() const; 
} 

const AAA aObj; 
aObj.func1(); ×
aObj.func2(); 正确

const AAA* aObj = new AAA(); 
aObj-> func1(); ×
aObj-> func2(); 正确
```

## 将 const 类型转化为 非const 类型的方法  
采用`const_cast`进行转换
### 用法
`const_cast <type_id> (expression)`
+ 常量指针被转化成非常量指针，并且仍然指向原来的对象
+ 常量引用被转换成非常量引用，并且仍然指向原来的对象
+ 常量对象被转换成非常量对象
```
const int constant = 21;
const int* const_p = &constant;
int* modifier = const_cast<int*>(const_p);
*modifier = 7;
```

## 示例 
利用const修饰函数和变量
```
class A
{
    int x;
    char *p;
public:
    int get_day() const;
    int set(int year,int month,int day);
    void f() const{
        x=10;    //error
        p=new char[20];    //error
        strcpy(p,"ABCD");   //feasible,doesn't change the value of p
    }
}

void f(const Date &d){
    d.get_day();    //OK
    d.set(11,1,1);  //error
}

```
