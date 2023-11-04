# Java Minimalist Survival Guide

<!-- TOC -->
* [Java Minimalist Survival Guide](#java-minimalist-survival-guide)
  * [Tooling](#tooling)
  * [Comments](#comments)
  * [Variables](#variables)
  * [Constants](#constants)
  * [Control flow](#control-flow)
  * [Operators](#operators)
  * [Primitive Value Types](#primitive-value-types)
  * [Complex Value Types (Object)](#complex-value-types-object)
    * [Top-level Class](#top-level-class)
    * [Abstract Class](#abstract-class)
    * [Final Class](#final-class)
    * [Interface](#interface)
    * [Enum](#enum)
    * [Nested Class - Static Nested Class](#nested-class---static-nested-class)
    * [Nested Class - Inner class](#nested-class---inner-class)
    * [Nested Class - Local Class](#nested-class---local-class)
    * [Nested Class - Anonymous Class](#nested-class---anonymous-class)
    * [Record](#record)
    * [Class Accessors](#class-accessors)
    * [Class Packages](#class-packages)
    * [This keyword](#this-keyword)
    * [Equality](#equality)
    * [Inheritance](#inheritance)
    * [Polymorphism](#polymorphism)
  * [Methods](#methods)
    * [Variable Arguments](#variable-arguments)
    * [Methods Accessors](#methods-accessors)
  * [Generics](#generics)
  * [Exceptions](#exceptions)
  * [Annotations](#annotations)
  * [Optional](#optional)
  * [Lambda](#lambda)
  * [Stream](#stream)
<!-- TOC -->

## Tooling

```java
javac Main.java                             // compile the file into bytecode
java Main                                   // run the bytecode
```

## Comments
Comment your code

```java
  */ Multi-line 
     comment */
  String city = "tokyo"                     // single line comment
```

## Variables
Points to a primitive or object value

```java
int c$nt = 0;                               // can only contain letters, digits, or $ and _, not start with a digit
int cnt,CNT;                                // is case sensitive cnt != CNT
int cnt = 0;                                // initialize and declare
```

## Constants
Forbid variable to point to another value (compilation check)

```java
final int CNT = 3;                          // convention is to use uppercase
CNT = 2;                                    // won't compile
```

## Control flow
Influence the order of execution of the statements.

```java
if () { }                                   // if
if () { } else {}                           // if..else
if () { } else if {}                        // if..else..if

switch (test) {                             // switch
  case "string":
    break;
  default:
    break;
}

while() {}                                  // while
do {} while()                               // do..while
for (i = 0; i < 10; i++) {}                 // for
for (i = 0; i < 10; i++) { break }          // terminate current loop
lab: for (i = 0; i < 10; i++) { break }     // terminate labeled loop
for (i = 0; i < 10; i++) { continue}        // skip current iteration of the loop
for (String s : list){}                     // foreach 
```

## Operators
Perfom mathematical or logical function based on the values provided to the operator.

```java
// arithmetic
-a                                          // unary -
+a                                          // unary +
a + b                                       // addition
a - b                                       // substraction
a * b                                       // multiplication
a / b                                       // division
a % b                                       // modulo
a++, ++a                                    // post and pre increment
a--, --a                                    // post and and pre decrement

// Comparaison
(a == b)                                    // compare memory address value
(a != b)                                    // different memory address
(a >= b)                                    // greater or equal than
(a > b)                                     // strictly greater
(a <= b)                                    // small or equal than
(a > b)                                     // strictly smaller

// bitwise
a & b                                       // bitwise and
a | b                                       // bitwise or
a ^ b                                       // bitwise xor
~a                                          // bitwise not
a << 5                                      // shifts 5 bits to the left
a >> 5                                      // shifts 5 bits to the right
a >>> 5                                     // sifts 5 bits to the right and shifting zeros from left

// logic
a && b                                      // logical and: true if a and b
a || b                                      // logical or : true if a or b
a ˆ b                                       // logical xor : true if a xor b
!a                                          // logical not: true if not a

//assignement
a = a                                       // assigne
a += 5                                      // a = a+5
a -= 5                                      // a = a-5
a *= 5                                      // a = a*5
a /= 5                                      // a = a/5
a %= 5                                      // a = a%5
a <<= 5                                     // a = a<<5
a >>= 5                                     // a = a>>5
a >>>= 5                                    // a = a>>>5
a &= 5                                      // a = a&5
a |= 5                                      // a = a|5
a ^= 5                                      // a = a^5

// ternary
(b >= 5) ? 100 : 0                          // if  b >=5 return 100 otherwise return 0
```

## Primitive Value Types
There are 8 java primitive value. Primitive have always a default value.

```java
  boolean                                   // 1 bit, true or false, default false
  char                                      // 16 bit, default \u0000 (null character)
  byte                                      // 8 bits, default 0
  short                                     // 16 bits, default 0
  int                                       // 32 bits, default 0
  long                                      // 64 bits, default 0L
  float                                     // 32 bits, default 0.0f
  double                                    // 64 bits, default 0.0d
```
When you assign a primitive value to a variable, the variable directly holds that value in memory.

## Complex Value Types (Object)
In java, to create object you must go through a Class. A Class defines an object data type.

### Top-level Class
A class that is not nested within any other class.

```java
public class Person {}                      // accessible for everyone
Person person = new Person()                // create an object of type Person
```

### Abstract Class
A class that cannot be instantiated directly and is used as a base class for deriving concrete subclasses.

```java
public abstract class Shape {
    public void print(){}                   // inherited by all subclass
    public abstract double getArea();       // needed to be implemented by subclass
}

public class Square extends Shape {         // cannot extends multiple abstract classes
    @Override
    public double getArea() { }             // implement abstract method
}
```

### Final Class
A class which can't be subclassed.

```java
public final class Shape { }                // no subclass of Shape are permitted.
```

### Interface
A contract that a class can implement.

```java
public interface Drawable {
   public void draw();                      // needed to be implemented by interface implementors
   default void isDrawable() { }            // available to all interface implementors
}

public class Shape implements Bounceable { } 
```

### Enum
A class with a fixed set of state.

```java
public enum Week {
    MONDAY,                                 // set of values
    TUESDAY;
}

Week today = Week.MONDAY;
```

### Nested Class - Static Nested Class
A top-level class encapsulated in another class and is instantiated through static access of its enclosing class.

```java
public class ShoppingCart {
    public static class Item { }            // has access to only private static members of enclosing class
}

new ShoppingCart.Item();                    // instantiate using static access of enclosing class
```

### Nested Class - Inner class
A class which only live and is instantiated through an instance of its enclosing class.

```java
public class Collection {
    public class Iterator  { }              // has access to all private members of enclosing class
}

new Collection().new Iterator();            // instantiate through an instance of enclosing class
```

### Nested Class - Local Class
A class that is defined inside a method, constructor, or a block of code.

```java
public int calculateSalary() {
    class SalaryCalculator { }              // access private enclosing class members and final local variables
    new SalaryCalculator();                 // only viewable in this block of code
}
```

### Nested Class - Anonymous Class
A class that is declared and instantiated at the same time, typically used for one-time use or overriding a single method.

```java
public class ThreadManager{
    public runAThread() {
        Thread th = new Thread() {          // creating an instance of an anonymous class that extends the Thread class 
            public void run() { }
        };
        thread.start();
    }
}
```

### Record
The equals, hashCode, and toString methods, as well as the private, final fields and public constructor, are generated by the Java compiler.

```java
public record Person (String name, String address) {}
```

### Class Accessors
Define the visibility of a class
```java
  class Shape {}                            // accessible only in same package 
  public class Shape {}                     // accessible from everywhere 
```

### Class Packages
How to organize your classes and avoid naming collisions
```java
  package com.microsoft.translator          // define the package to which the class belong

  import com.google.common.escape.Escaper   // import a class
  import static java.lang.System.out        // import static method or field
```

### This keyword
Pointer to the current instance object
```java
  public String getName() {
    return this.name;                       // this points to current instance 
  }
```

### Equality
Check equality of two object
```java
shape1 == shape2                            // reference equality 
shape1.equals(shape2)                       // object content equality 

@Override
public boolean equals(Object o) {}          // override equals to specifiy object content equality 
```


### Inheritance
Create a new class that is a modified version of an existing class ("is-a relationship").

```java
class Shape {
  int size;
  public void draw() { }
}

class Circle extends Shape {                // inherit non-private fields and methods from Shape
  public Circle(){
    super();                                // call parent constructor
    super.size;                             // super points to parent
  }
}

new Circle().draw();                  
```

### Polymorphism
Allows objects of different classes to be treated as objects of a common superclass. Two type of polymorphism,
compile-time binding (overloading) and runtime binding (overriding).

```java
class Shape {
  void draw() { }
}

class Circle extends Shape {                
  @Override
  void draw() { }                           // overriding: binding is made at runtime
  
  void display(){}                          // overloading: binding is made at compile time based on signature
  void display(String text){}
}

new Circle().display();                     // calling the display method without parameters
Shape shape = new Circle();
shape.draw();                               // calling the draw method of circle although my reference is of type Shape
```
## Methods
Methods are functions attached to object. They are not first class citizen in Java and they can only return one value.

```java
int count(){}                               // instance method returning int value
static int count(){}                        // method attached to the class not the instance
final int count(){}                         // cannot be subclassed
```

### Variable Arguments
Received multiple arguments
```java
 public int count(String...nbr){}           // receive an array
 count("a","b");
```

### Methods Accessors
Define the visibility of an class
```java
 public int count(){}                       // accessible from everywhere
 protected int count(){}                    // only within same package and any subclass
 int count(){}                              // accessible only the same package 
 private int count(){}                      // accessible only within the same class
```


## Generics
Create classes, interfaces, and methods that operate on types as parameters. Specialing used for ensuring collection homogeneity.

```java
public class Box<T> {                       // a Type parametrized Box
  private T content;

  public Box(T content) {
    this.content = content;
  }
}
Box<Integer> integerBox = new Box<>(0);     // create a box which can only contain an Integer
List<Box> boxList = new ArrayList<>();      // used to ensure only box in boxList
```

## Exceptions
Handle unexpected or erroneous conditions, such as runtime errors. Disrupt normal flow.

```java
try {
    int result = 10 / 0;                    // runtime error / 0
    int a = 3;                              // will never be executed 
    } catch (RuntimeException e) {
      System.err.println("error");          // will jump here
    } finally {
      System.err.println("final");          // and thene here
    }
}

public void getShape() throws Exception     // responsibility to handle the exception on caller
```

## Annotations
Metadata that can be added to classes, methods, fields, and other program elements to provide additional information, instructions, or configuration, which can be used by the Java compiler or runtime.

```java
@Override
public void getShape(){}
```

## Optional
Force you to think about possible optional value (encapsulate possible null)

```java
  Optional.of("test");                      // throw NullPointerException if value is null
  Optional.ofNullable(null);                // throw NullPointerException if value is null
  Optional.empty();                         // same as Optional.ofNullable(null)

  optional.get();                           // return value or throw noSuchElementException if value is null
  optional.orElse("barbara");               // return value or "else value" if value is null
  optional.orElseGet(()-> "barbara");       // return value or "method execution return value" if value is null
```


## Lambda
Java does not have anonymous function. A lambda expression is essentially an anonymous function that can be treated as an object and passed around as an argument to methods or stored in variables. Lambdas are used heavily in the Stream API, allowing you to perform operations on collections of data in a concise and readable way.

```java
import examples.LambdaMain;

@FunctionalInterface
public interface MathOperation {
    public Integer operate(Integer a, Integer b);
}

MathOperation add = (a, b) -> a + b;        // create a function object
MathOperation sub = LambdaMain::sub;        // create a function object based on a static method

add.operate(3,4);    // call the function 
```

## Stream
A stream is a sequence of elements that you can process in a functional and declarative style.
A stream is composed of a stream source, intermediate operations and a terminal operaation.

```java
    List<String> names = List.of("Nicolas", "Nolwen", "Batiste");

    Stream<String> nameStream = names.stream();
    nameStream.filter(name -> name.startsWith("C")) 
              .toList(); 
```
