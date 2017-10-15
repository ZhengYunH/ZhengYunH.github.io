# Access Control  
Java provides _access specifiers_ to allow the library creator to say what is available to the client programmer and what is not.  
+ public
+ protected
+ package access(no keyword)
+ private
## package: the library unit  
`import java.util.*`

### Code organization  
If you use a package statement, it must appear as the first non-comment in the file. When you say:  
`package acess`  
you’re stating that this compilation unit is part of a library named access.

### Creating unique package names  
By convention, the first part of the package name is the reversed Internet domain name of the creator of the class.The second part of this trick is resolving the package name into a directory on your machine.  

#### Collisions
```
import net.mindview.simple.*;
import java.util.*;
Vector v = new Vector();
```
Which Vector class does this refer to? The compiler can’t know, and the reader can’t know either. So the compiler complains and forces you to be explicit. If I want the standard Java Vector, for example, I must say:
`java.util.Vector v = new java.util.Vector();`

### A custom tool library  
Whenever you come up with a useful new utility, you can add it to your own library.

### Using imports to change behavior  
there are other valuable uses for conditional compilation. A very common use is for debugging code. The debugging features are enabled during development and disabled in the shipping product. You can accomplish this by changing the —__package__ that’s imported in order to change the code used in your program from the debug version to the production version. This technique can be used for any kind of conditional code.

## Java access specifiers  

### Package access  
It means that all the other classes in the current package have access to that member, but to all the classes outside of this package, the member appears to be private.  

### public: interface access
When you use the public keyword, it means that the member declaration that immediately follows public is available to everyone, in particular to the client programmer who uses the library.  

#### The default package  

##### access/Cake.java
```
class Cake {
    public static void main(String[] args) {
        Pie x = new Pie();
        x.f();
    }
}

Output:
Pie.f()
```
##### access/Pie.java
```
class Pie {
    void f() { System.out.println("Pie.f()"); }
}
```
The reason that they are available in Cake.java is because they are in the same directory and have no explicit package name. Java treats files like this as implicitly part of the “default package” for that directory, and thus they provide package access to all the other files in that directory.

### private: you can't touch that!  

##### access/IceCream.java
```
class Sundae {
    private Sundae() {}
    static Sundae makeASundae() {
        return new Sundae();
    }
}

public class IceCream {
    public static void main(String[] args) {
        //! Sundae x = new Sundae();
        Sundae x = Sundae.makeASundae();
    }
}
```
This shows an example in which private comes in handy: You might want to control how an object is created and prevent someone from directly accessing a particular constructor.  

### procected: inheritance access  
The protected keyword deals with a concept called inheritance.  
__protected__ also gives package access—that is, other classes in the same package may access protected elements.

## Interface and implementation  
Access control puts boundaries within a data type for two important reasons.  
1.To establish what the client programmers can and can’t use.
2.To separate the interface from the implementation.

For clarity, you might prefer a style of creating classes that puts the public members at the beginning, followed by the protected, package-access, and private members.  

## Class access 
there’s an extra set of constraints:
1. There can be only one public class per compilation unit (file).
2. The name of the public class must exactly match the name of the file containing the compilation unit, including capitalization.
3. It is possible, though not typical, to have a compilation unit with no public class at all.  

you have only two choices for class access: package access or public.