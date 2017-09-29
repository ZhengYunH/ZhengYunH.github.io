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