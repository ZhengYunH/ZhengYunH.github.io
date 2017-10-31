# Reusing Classes  
two ways to accomplish using the classes without soiling the existing code.

+ composition
+ inheritance

## Composition syntax  
Simply place object refernces inside new classes.  
It makes sense that the compiler doesn’t just create a default object for every reference, because that would incur unnecessary overhead in many cases. If you want the references initialized, you can do it:
1. At the point the objects are defined. This means that they’ll always be initialized before the constructor is called.
2. In the constructor for that class.
3. Right before you actually need to use the object. This is often called lazy initialization. It can reduce overhead in situations where object creation is expensive and the object doesn’t need to be created every time.
4. Using instance initialization.

## Inheritance syntax  
`main()` when you say java Detergent, Detergent.main( ) will be called. But you can also say java Cleanser to invoke Cleanser.main( ), even though Cleanser is not a public class. Even if a class has package access, a public main() is accessible.  

### Initializing the base class
the base class is initialized before the derived-class constructors can access it. Even if you don’t create a constructor for derived-class, the compiler will synthesize a default constructor for you that calls the base class constructor.

### Constructors with arguments  
If your class doesn’t have default arguments, or if you want to call a base-class constructor that has an argument, you must explicitly write the calls to the base-class constructor using the super keyword and the appropriate argument list.

## Delegation  
This is midway between inheritance and composition, because you place a member object in the class you’re building (like composition), but at the same time you expose all the methods from the member object in your new class (like inheritance).  

## Combining composition and inheritance  
It is very common to use composition and inheritance together.  
Although the compiler forces you to initialize the base classes, and requires that you do it right at the beginning of the constructor, it doesn’t watch over you to make sure that you initialize the member objects, so you must remember to pay attention to that.

### Guatanteeing proper cleanup  
In general, you should follow the same form that is imposed by a C++ compiler on its destructors: First perform all of the cleanup work specific to your class, in the reverse order of creation. (In general, this requires that base-class elements still be viable.) Then call the base-class cleanup method, as demonstrated here.  
If you want cleanup to take place, make your own cleanup methods and don’t use on finalize( ).

### Name hiding
If a Java base class has a method name that’s overloaded several times, redefining that method name in the derived class will not hide any of the base-class versions.  
Java SE5 has added the __@Override__ annotation, which is not a keyword but can be used as if it were. When you mean to override a method, you can choose to add this annotation and the compiler will produce an error message if you accidentally overload instead of overriding.

## Choosing composition vs. inheritance  
+ Composition is generally used when you want the features of an existing class inside your new class, but not its interface.For this effect, you embed private objects of existing classes inside your new class.  
+ When you inherit, you take an existing class and make a special version of it. In general, this means that you’re taking a general-purpose class and specializing it for a particular need.

## protected  
Although it’s possible to create protected fields, the best approach is to leave the fields private; you should always preserve your right to change the underlying implementation.  
In Java, protected also provides package access.

## Upcasting  
Inheritance means that all of the methods in the base class are also available in the derived class, any message you can send to the base class can also be sent to the derived class.

### Why 'upcasting'
Upcasting is always safe because you’re going from a more specific type to a more general type.  
You can also perform the reverse of upcasting, called downcasting, but this involves a dilemma.

### Composition vs. inheritance revisited
You’ll also use existing classes to build new classes with composition. Less frequently, you’ll use inheritance.   
One of the clearest ways to determine whether you should use composition or inheritance is to ask whether you’ll ever need to upcast from your new class to the base class.  

## The final keyword  
Java’s final keyword has slightly different meanings depending on the context, but in general it says “This cannot be changed.”

### final data  
A field that is both static and final has only one piece of storage that cannot be changed.  
With a primitive, final makes the value a constant, but with an object reference, final makes the reference a constant. Once the reference is initialized to an object, it can never be changed to point to another object.However, the object itself can be modified.  

### Blank finals  
Java allows the creation of blank finals, which are fields that are declared as final but are not given an initialization value.  

### final arguments  
Java allows you to make arguments final by declaring them as such in the argument list. This means that inside the method you cannot change what the argument reference points to.

### final methods  
With Java SE5/6, you should let the compiler and JVM handle efficiency issues and make a method final only if you want to explicitly prevent overriding.

### final and private  
Any private methods in a class are implicitly final.  

### final classes  
When you say that an entire class is final (by preceding its definition with the final keyword), you state that you don’t want to inherit from this class or allow anyone else to do so.  

### final caution  
In general, it’s difficult to anticipate how a class can be reused, especially a general-purpose class. If you define a method as final, you might prevent the possibility of reusing your class through inheritance in some other programmer’s project simply because you couldn’t imagine it being used that way.  

## Initialization and class loading  
In general, you can say that “class code is loaded at the point of first use.” This is usually when the first object of that class is constructed, but loading also occurs when a static field or static method is accessed.  
The point of first use is also where the static initialization takes place. All the static objects and the static code block will be initialized in textual order.  

### Initialization with inheritance  
First, all the primitives in this object are set to their default values and the object references are set to null—this happens in one fell swoop by setting the memory in the object to binary zero. Then the base-class constructor will be called. In this case the call is automatic, but you can also specify the base-class constructor call by using super.After the base-class constructor completes, the instance variables are initialized in textual order. Finally, the rest of the body of the constructor is executed.
