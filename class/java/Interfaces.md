# Interfaces  
Interfaces and abstract classes provide more structured way to separate interface from implementation.  


## Abstract classes and methods  
Here is the syntax for an abstract method declaration.
>abstract void f( );

A class containing abstract methods is called an abstract class. If a class contains one or more abstract methods, the class itself must be qualified as abstract. (Otherwise, the compiler gives you an error message.)

It’s possible to make a class abstract without including any abstract methods. This is useful when you’ve got a class in which it doesn’t make sense to have any abstract methods, and yet you want to prevent any instances of that class.

## Interfaces  
As with a class, you can add the public keyword before the interface keyword.If you leave off the public keyword, you get package access, so the interface is only usable within the same package. An interface can also contain fields, but these are implicitly static and final.You can choose to explicitly declare the methods in an interface as public, but they are public even if you don’t say it.

## “Multiple inheritance” in Java  
+ Keep in mind that one of the core reasons for interfaces is shown in the preceding example: to upcast to more than one base type.
+ a second reason for using interfaces is the same as using an abstract base class: to prevent the client programmer from making an object of this class and to establish that it is only an interface.

This brings up a question: Should you use an interface or an abstract class? If it’s possible to create your base class without any method definitions or member variables, you should always prefer interfaces to abstract classes. In fact, if you know something is going to be a base class, you can consider making it an interface.

## Extending an interface with inheritance  
Normally, you can use extends with only a single class, but extends can refer to multiple base interfaces when building a new interface. As you can see, the interface names are simply separated with commas.
```
interface Vampire extends DangerousMonster, Lethal {
    void drinkBlood();
}
```


