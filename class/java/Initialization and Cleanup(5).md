# Initialization
## Guaranteed initialization with the constructor
```
class Rock {
    Rock() { // This is the constructor
        System.out.print("Rock ");
        }
    }
    public class SimpleConstructor {
        public static void main(String[] args) {
        for(int i = 0; i < 10; i++)
            new Rock();
    }
} 

Output:
Rock Rock Rock Rock Rock Rock Rock Rock Rock Rock
```

## Method overloading  
```
class Tree {
    int height;
    Tree() {
        print("Planting a seedling");
        height = 0;
    }
    Tree(int initialHeight) {
        height = initialHeight;
        print("Creating new Tree that is " +
        height + " feet tall");
    }
    void info() {
        print("Tree is " + height + " feet tall");
    }
    void info(String s) {
        print(s + ": Tree is " + height + " feet tall");
    }
}

public class Overloading {
    public static void main(String[] args) {
        for(int i = 0; i < 5; i++) {
            Tree t = new Tree(i);
            t.info();
            t.info("overloaded method");
        }
        // Overloaded constructor:
        new Tree();
    }
}

Output:
Creating new Tree that is 0 feet tall
Tree is 0 feet tall
overloaded method: Tree is 0 feet tall
Creating new Tree that is 1 feet tall
Tree is 1 feet tall
overloaded method: Tree is 1 feet tall
Creating new Tree that is 2 feet tall
Tree is 2 feet tall
overloaded method: Tree is 2 feet tall
Creating new Tree that is 3 feet tall
Tree is 3 feet tall
overloaded method: Tree is 3 feet tall
Creating new Tree that is 4 feet tall
Tree is 4 feet tall
overloaded method: Tree is 4 feet tall
Planting a seedling
```

### Distinguishing overloaded methods  
```
public class OverloadingOrder {
    static void f(String s, int i) {
        print("String: " + s + ", int: " + i);
    }
    static void f(int i, String s) {
        print("int: " + i + ", String: " + s);
    }
    public static void main(String[] args) {
        f("String first", 11);
        f(99, "Int first");
    }
} 

Output:
String: String first, int: 11
int: 99, String: Int first
```

### Overloading with primitives  
```
public class Demotion {
    void f1(char x) { print("f1(char)"); }
    void f1(byte x) { print("f1(byte)"); }
    void f1(short x) { print("f1(short)"); }
    void f1(int x) { print("f1(int)"); }
    void f1(long x) { print("f1(long)"); }
    void f1(float x) { print("f1(float)"); }
    void f1(double x) { print("f1(double)"); }

    void f2(char x) { print("f2(char)"); }
    void f2(byte x) { print("f2(byte)"); }
    void f2(short x) { print("f2(short)"); }
    void f2(int x) { print("f2(int)"); }
    void f2(long x) { print("f2(long)"); }
    void f2(float x) { print("f2(float)"); }

    void f3(char x) { print("f3(char)"); }
    void f3(byte x) { print("f3(byte)"); }
    void f3(short x) { print("f3(short)"); }
    void f3(int x) { print("f3(int)"); }
    void f3(long x) { print("f3(long)"); }

    void f4(char x) { print("f4(char)"); }
    void f4(byte x) { print("f4(byte)"); }
    void f4(short x) { print("f4(short)"); }
    void f4(int x) { print("f4(int)"); }

    void f5(char x) { print("f5(char)"); }
    void f5(byte x) { print("f5(byte)"); }
    void f5(short x) { print("f5(short)"); }

    void f6(char x) { print("f6(char)"); }
    void f6(byte x) { print("f6(byte)"); }

    void f7(char x) { print("f7(char)"); }

    void testDouble() {
        double x = 0;
        print("double argument:");
        f1(x);f2((float)x);f3((long)x);f4((int)x);
        f5((short)x);f6((byte)x);f7((char)x);
    }

    public static void main(String[] args) {
        Demotion p = new Demotion();
        p.testDouble();
    }

Output:
double argument:
f1(double)
f2(float)
f3(long)
f4(int)
f5(short)
f6(byte)
f7(char)
```

+ if you have a data type that is smaller than the argument in the method, that data type is promoted.
+ char produces a slightly different effect, since if it doesn’t find an exact char match, it is promoted to int.
+ If your argument is wider, then you must perform a narrowing conversion with a cast. If you don’t do this, the compiler will issue an error message.

### Overloading on return values  
you cannot use return value types to distinguish overloaded methods.

## Default constructors  
```
class Bird2 {
    Bird2(int i) {}
    Bird2(double d) {}
    }
public class NoSynthesis {
    public static void main(String[] args) {
        //! Bird2 b = new Bird2(); // No default
        Bird2 b2 = new Bird2(1);
        Bird2 b3 = new Bird2(1.0);
    }
}
```

## The `this` keyword
```
class Person {
    public void eat(Apple apple) {
        Apple peeled = apple.getPeeled();
        System.out.println("Yummy");
    }
}
class Peeler {
    static Apple peel(Apple apple) {
        // ... remove peel
        return apple; // Peeled
    }
}
class Apple {
    Apple getPeeled() { return Peeler.peel(this); }
}
public class PassingThis {
    public static void main(String[] args) {
        new Person().eat(new Apple());
    }
}

Output:
Yummy
```

### Calling constructors from constructors  
```
public class Flower{
    int petalCount=0;
    String s="initial value";
    Flower(int petals){
        petalCount=petals;
        print("Constructor w/ int arg only , petalCount= " + petalCount);
    }
    Flower(String ss) {
        print("Constructor w/ String arg only, s = " + ss);
        s = ss;
    }
    Flower(String s, int petals) {
        this(petals);
        //! this(s); // Can’t call two!
        this.s = s; // Another use of "this"
        print("String & int args");
    }
    Flower() {
        this("hi", 47);
        print("default constructor (no args)");
    }
    void printPetalCount() {
        //! this(11); // Not inside non-constructor!
        print("petalCount = " + petalCount + " s = "+ s);
    }
    public static void main(String[] args) {
        Flower x = new Flower();
        x.printPetalCount();
    }
}

Output:
Constructor w/ int arg only, petalCount= 47
String & int args
default constructor (no args)
petalCount = 47 s = hi
```

+ The constructor `Flower(String s, int petals)` shows that, while you can call one constructor using this, you cannot call two. In addition, the constructor call must be the first thing you do, or you’ll get a compiler error message.
+ The compiler won’t let you call a constructor from inside any method other than a constructor.

### The meaning of static  
With the this keyword in mind, you can more fully understand what it means to make a method static. It means that there is no this for that particular method.  

You cannot call non-static methods from inside static methods (although the reverse is possible), and you can call a static method for the class itself, without any object. In fact, that’s primarily what a static method is for.

## Cleanup:finalization and garbage collection  

1. _Your objects might not get garbage collected_  
2. _Grabage collection is not destruction_
What it means is that if there is some activity that must be performed before you no longer need an object, you must perform that activity yourself.  
3. _Grabage collection is only about memory_  

### You must perform cleanup  
+ In Java,there is no "delete" for releasing the object.
+ You should never call `finalize()` directly.
+ If you want some kind of cleanup performed other than storage release, you must still explicitly call an appropriate method in Java.

### The termination condition
```
class Book {
    boolean checkedOut = false;
    Book(boolean checkOut) {
        checkedOut = checkOut;
    }
    void checkIn() {
        checkedOut = false;
    }
    protected void finalize() {
        if(checkedOut)
            System.out.println("Error: checked out");
        // Normally, you’ll also do this:
        // super.finalize(); // Call the base-class version
    }
}

public class TerminationCondition {
    public static void main(String[] args) {
        Book novel = new Book(true);
        // Proper cleanup:
        novel.checkIn();
        // Drop the reference, forget to clean up:
        new Book(true);
        // Force garbage collection & finalization:
        System.gc();
    }
} 

Output:
Error: checked out
```

### How a garbage collector works  
+ Reference Counting Collector 
+ mark-and-sweep 
    + Tracing Collector
    + Compacting Collector  
+ stop-and-copy
    + Coping Collector ()
    + Generational Collector  
+ Adaptive Collector

## Member initialization  
In the case of a method’s local variables, this guarantee comes in the form of a compile-time error. So if you say:
```
void f() {
    int i;
    i++; // Error -- i not initialized
}
```
You’ll get an error message that says that i might not have been initialized. 

If a primitive is a field in a class,each primitive field of a class is guaranteed to get an initial value.  
## Specifying initialization  
What happens if you want to give a variable an initial value? One direct way to do this is simply to assign the value at the point you define the variable in the class.
```
public class InitialValues2 {
    boolean bool = true;
    char ch = ‘x’;
    byte b = 47;
    short s = 0xff;
    int i = 999;
    long lng = 1;
    float f = 3.14f;
    double d = 3.14159;
}
```
You can also initialize non-primitive objects in this same way. If Depth is a class, you can create a variable and initialize it like so:
```
//If you haven’t given d an initial value and you try to use it anyway, you’ll get a runtime error called an exception.  
public class Measurement {
    Depth d = new Depth();
}
```
You can even call a method to provide an initialization value:
```
public class MethodInit {
    int i = f();
    int f() { return 11; }
}
```
But you cannot do this:
```
public class MethodInit3 {
    //! int j = g(i); // Illegal forward reference
    int i = f();
    int f() { return 11; }
    int g(int n) { return n * 10; }
}
```

## Constructor initialization  
```
public class Counter {
    int i;
    Counter() { i = 7; 
}
```

## Order of initialization  
The variable definitions may be scattered throughout and in between method definitions, but the variables are initialized before any methods can be called—even the constructor.  

## static data initialization  
There’s only a single piece of storage for a static, regardless of how many objects are created. You can’t apply the static keyword to local variables, so it only applies to fields. If a field is a static primitive and you don’t initialize it, it gets the standard initial value for its type.  
If you want to place initialization at the point of definition, it looks the same as for non-statics. 

### Explicit static initialization  
```
static int i;
static double k;
static{
    i=40;
    k=1.0;
}
```

## Non-static instance initialization  
Java provides a similar syntax, called instance initialization, for initializing non-static variables for each object.
```
class Mug{
    Mug(int marker){
        print("Mug("+marker+")");
    }
}
public class Mugs{
    Mug mug1;
    Mug mug2;
    {
        mug1=new Mug(1);
        mug2=new Mug(2);
        print("mug1 and mug2 initialized");
    }
}
```

## Array initializaton  
`int[] a1` == `int a1[]`  
This special initialization is a set of values surrounded by curly braces. The storage allocation (the equivalent of using new) is taken care of by the compiler in this case. 
```
int[] a1={1,2,3,4,5};
int[] a2=a1;    //just copy a reference
for(int i = 0; i < a2.length; i++)
    a2[i] = a2[i] + 1;
for(int i = 0; i < a1.length; i++)
    print("a1[" + i + "] = " + a1[i]);

output:
a1[0] = 2
a1[1] = 3
a1[2] = 4
a1[3] = 5
a1[4] = 6
```
The `Arrays.toString()` method, which is part of the standard java.util library, produces a printable version of a one-dimensional array.  
```
int[] a=new int[rand.nextInt(20)];
for(int i = 0; i < a.length; i++) 
    a[i] = rand.nextInt(500); // Autoboxing
print(Arrays.toString(a));
```
you could create an array of String objects to pass to the main( ) of another method, to provide alternate command-line arguments to that main( ):
```
public class DynamicArray {
    public static void main(String[] args) {
        Other.main(new String[]{ "fiddle", "de", "dum" });
    }
}
class Other {
    public static void main(String[] args) {
        for(String s : args)
            System.out.print(s + " ");
    }
} 

Output:
fiddle de dum
```

## Variable argument lists
```
public class NewVarArgs {
    static void printArray(Object... args) {
        for(Object obj : args)
            System.out.print(obj + " ");
        System.out.println();
}
public static void main(String[] args) {
    // Can take individual elements:
    printArray(new Integer(47), new Float(3.14),new Double(11.11));
    printArray(47, 3.14F, 11.11);
    printArray("one", "two", "three");
    printArray(new A(), new A(), new A());
    // Or an array:
    printArray((Object[])new Integer[]{ 1, 2, 3, 4 });
    printArray(); // Empty list is OK
    }
}

Output:
47 3.14 11.11
47 3.14 11.11
one two three
A@1bab50a A@c3c749 A@150bd4d
1 2 3 4
```

## Enumerated types
### Create  
```
public enum Spiciness{
    NOT,MILD,MEDIUM,HOT,FLAMING
}
```
### Use
```
Spiciness howHot=Spiciness.MEDIUM;
```
### Ordinal  
```
for(Spiciness s : Spiciness.values())
    System.out.println(s + ", ordinal " + s.ordinal());

Output:
NOT, ordinal 0
MILD, ordinal 1
MEDIUM, ordinal 2
HOT, ordinal 3
FLAMING, ordinal 4
```