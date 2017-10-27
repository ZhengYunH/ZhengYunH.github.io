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
