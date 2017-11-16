# Inner Classes  

## Creating inner classes  
Typically, an outer class will have a method that returns a reference to an inner class.
```
class OuterClass
{
    class InnerClass{ }
    public InnerClass f(){
        return new InnerClass();
    }
}
OuterClass oc=new OuterClass();
OuterClass.InnerClass ic=oc.f();
```

## The link to the outer class  
When you create an inner class,an object of that inner class has a link to the enclosing object that made it, and so it can access the members of that enclosing object—without any special qualifications.  
Inner classes have access rights to all the elements in the enclosing class.  

## Using .this and .new  
If you need to produce the reference to the outer-class object, you name the outer class followed by a dot and this.  
Sometimes you want to tell some other object to create an object of one of its inner classes. To do this you must provide a reference to the other outer-class object in the new expression, using the .new syntax.
```
public InnerClass{}
OuterClass oc=new OuterClass();
OuterClass.InnerClass=oc.new Inner();
```

## Why inner classes?  
Each inner class can independently inherit from an implementation. Thus, the inner class is not limited by whether the outer class is already inheriting from an implementation.  

+ The inner class can have multiple instances, each with its own state information that is independent of the information in the outer-class object.
+ In a single outer class you can have several inner classes, each of which implements the same interface or inherits from the same class in a different way. An example of this will be shown shortly.
+ The point of creation of the inner-class object is not tied to the creation of the outer-class object.
+ There is no potentially confusing "is-a" relationship with the inner class; it’s a separate entity.