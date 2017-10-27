# λ表达式  
具体可以参考[MSDN官网](https://msdn.microsoft.com/zh-cn/library/dd293608.aspx)
## 问题的提出
对于求定积分函数：
```
double integrate(double (*f)(double),double a,double b);
double square(double x) { return x*x; }
integrate(square,0,1);
```
其中的f函数是个简单并且很少使用的函数，λ表达式就是用来处理这种函数的

## 定义格式

![lambda表达式](https://i-msdn.sec.s-msft.com/dynimg/IC251606.jpeg)
1. Capture 子句（在 C++ 规范中也称为 lambda 引导。）
2. 参数列表（可选）。 （也称为 lambda 声明符)
3. 可变规范（可选）。
4. 异常规范（可选）。
5. 尾随返回类型（可选）。
6. “lambda 体”

`[<环境变量使用说明>]<形式参数><返回值类型指定><函数体>`  

+ `[<环境变量使用说明>]`（Capture子句）:指出函数体中对外层作用域中的自动变量的使用限制
    * 空：不能使用外层作用域中的自动变量。
    * &：按引用方式使用外层作用域中的自动变量（可以改变这些变量的值）
    * =：按值方式使用使用外层作用域中的自动变量（不能改变这些变量的值）
    * &和=可以用来统一指定对外层作用域中自动变量的使用方式，也可以用来单独指定可使用的外层自动变量（变量名前可以加&，默认为=）
+ `<形式参数>`:指出函数的参数及类型，其格式为
    * (<形式参数表>)
    * 如果函数没有参数，则这项可以省略
+ `<返回值类型指定>`:指出函数的返回值类型，其格式为
    * -> <返回值类型>
    * 它可以省略，这时根据函数体中return返回的值隐式确定返回值类型
+ 因此，以上的函数可以写为 `integrate([](double x)->double { return x*x; },0,1);
`

## 例子
```
{ int k,m,n;
   ...[](int x)->int { return x; } //不能使用k、m、n
   ...[&](int x)->int { k++; m++; n++; return x+k+m+n; } //k、m、n可以被修改
   ...[=](int x)->int { return x+k+m+n; } //k、m、n不能被修改
   ...[&,n](int x)->int { k++; m++; return x+k+m+n; } //n不能被修改
   ...[=,&n](int x)->int { n++; return x+k+m+n; } //n可以被修改
   ...[&k,m](int x)->int { k++; return x+k+m; } //只能使用k和m，k可以被修改
   ...[] { return k+m+n; } //没有参数，返回值类型为int,不能使用k、m、n
}
```

## Remark
+ λ表达式通常用于把一个匿名函数作为参数传给另一个函数的场合
+ 不使用环境变量的λ表达式可隐式转换成函数指针
+ 在C++中，λ表达式是通过函数对象来实现的