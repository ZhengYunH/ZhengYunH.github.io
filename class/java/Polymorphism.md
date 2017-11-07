# Polymorphism  
Polymorphism is the third essential feature of an object-oriented programming language, after data abstraction and inheritance. 

## Method-call binding  
Connecting a method call to a method body is called binding.  

+ early binding : Binding is performed before the program is run 
+ late binding : Binding occurs at running time ,also called _dynamic binding_ or _runtime binding_  

All method binding in Java uses late binding unless the method is static or final (private methods are implicitly final).  

## Extensibility
In a well-designed OOP program, most or all of your methods will communicate only with the base-class interface.

A program is extensible because you can add new functionality by inheriting new data types from the common base class.

## Pitfall: private,fields and static methods 
Only ordinary method calls can be polymorphic.

## Constructors and polymorphism  
The order of constructor calls for a complex object is as follows:  

1.The storage allocated for the object is initialized to binary zero before anything else happens
2. The base-class constructor is called.
3. Member initializers are called in the order of declaration.
4. The body of the derived-class constructor is called.

## Inheritance and cleanup  
And with inheritance, you must override dispose() in the derived class if you have any special cleanup that must happen as part of garbage collection. When you override dispose() in an inherited class, it’s important to remember to call the base-class version of dispose(), since otherwise the base-class cleanup will not happen.  
The order of disposal should be the reverse of the order of initialization, in case one subobject is dependent on another.  

## Behavior of polymorphic methods inside constructors
The only safe methods to call inside a constructor are those that are final in the base class. 

## Covariant return types  
Java SE5 adds covariant return types, which means that an overridden method in a derived class can return a type derived from the type returned by the base-class method.

## Designing with inheritance
To choose composition first, especially when it’s not obvious which one you should use. Composition does not force a design into an inheritance hierarchy. But composition is also more flexible since it’s possible to dynamically choose a type (and thus behavior) when using composition, whereas inheritance requires an exact type to be known at compile time.  
A general guideline is “Use inheritance to express differences in behavior, and fields to express variations in state.”

## Downcasting and runtime type information  
In some languages (like C++) you must perform a special operation in order to get a type-safe downcast, but in Java, every cast is checked! So even though it looks like you’re just performing an ordinary parenthesized cast, at run time this cast is checked to ensure that it is in fact the type you think it is. If it isn’t, you get a ClassCastException. This act of checking types at run time is called runtime type identification (RTTI).

