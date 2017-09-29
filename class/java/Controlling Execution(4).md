# Controlling Execution
## true and false  
Java doesn't allow you to use a number as a boolean.
## if-else
## Iteration
+ while
+ do-while
+ for

## The comma operator  
## Foreach sysntax
```
import java.util.*;
public class ForEachFloat {
    public static void main(String[] args) {
        Random rand = new Random(47);
        float f[] = new float[10];
        for(int i = 0; i < 10; i++)
        f[i] = rand.nextFloat();
        for(float x : f)
        System.out.println(x);
    }
} 

Output:
0.72711575
...
0.73734957

//like `for x in range(f)` in Python
```

Any method that returns an array is a candidate for use with foreach. For example, the String class has a method toCharArray( ) that returns an array of char, so you can easily iterate through the characters in a string:
```
public class ForEachString {
    public static void main(String[] args) {
        for(char c : "An African Swallow".toCharArray() )
            System.out.print(c + " ");
    }
} 

Output:
A n   A f r i c a n   S w a l l o w
```

As you’ll see in the [Holding Your Objects chapter](),foreach will also work with any object that is Iterable.

## return  
## break and continue
## goto(label)  
Java has no goto.However, it does have something that looks a bit like a jump tied in with the break and continue keywords.It’s not a jump but rather a way to break out of an iteration statement.  
A label is an identifier followed by a colon, like this:  
```
label1:
```

The only place a label is useful in Java is right before an iteration statement.
```
label1:
outer-iteration {
    inner-iteration {
        //...
        break; // (1)
        //...
        continue; // (2)
        //...
        continue label1; // (3)
        //...
        break label1; // (4)
    }
}
```

+ In (3), the continue label1 breaks out of the inner iteration and the outer iteration, all the way back to `label1`.
+ In (4),the `break label1` also breaks all the way out to `label1`, but it does not reenter the iteration. It actually does break out of both iterations.

```
public class LabeledWhile {
    public static void main(String[] args) {
        int i = 0;
        outer:
        while(true) {
            print("Outer while loop");
            while(true) {
                i++;
                print("i = " + i);
                if(i == 1) {
                    print("continue");
                    continue;
                }
                if(i == 3) {
                    print("continue outer");
                    continue outer;
                }
                if(i == 5) {
                    print("break");
                    break;
                }
                if(i == 7) {
                    print("break outer");
                    break outer;
                }
            }
        }
    }
} 

Output:
Outer while loop
i = 1
continue
i = 2
i = 3
continue outer
Outer while loop
i = 4
i = 5
break
Outer while loop
i = 6
i = 7
break outer
```

### Rule  
1. A plain continue goes to the top of the innermost loop and continues.
2. A labeled continue goes to the label and reenters the loop right after that label.
3. A break “drops out of the bottom” of the loop.
4. A labeled break drops out of the bottom of the end of the loop denoted by the label.

## switch  
It requires a selector that evaluates to an integral value, such as int or char. If you want to use, for example, a string or a floating point number as a selector, it won’t work in a switch statement.  
For non-integral types, you must use a series of if statements. At the end of the next chapter, you’ll see that Java SE5’s new enum feature helps ease this restriction, as enums are designed to work nicely with switch.
