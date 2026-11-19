# Java Core Concept

## Table of Contents

1. [Java Basics](#1-java-basics)
   - [JDK, JRE, JVM](#11-jdk-jre-jvm)
   - [Variables and Data Types](#12-variables-and-data-types)
   - [Operators](#13-operators)
   - [Conditional Statements](#14-conditional-statements)
   - [Loops](#15-loops)
   - [Type Casting](#16-type-casting)
2. [Object-Oriented Programming](#2-object-oriented-programming)
   - [Classes and Objects](#21-classes-and-objects)
   - [Constructors](#22-constructors)
   - [Inheritance](#23-inheritance)
   - [Polymorphism](#24-polymorphism)
   - [Encapsulation](#25-encapsulation)
   - [Abstraction](#26-abstraction)
   - [Interfaces](#27-interfaces)
   - [Method Overloading and Overriding](#28-method-overloading-and-overriding)
   - [Static and Final Keywords](#29-static-and-final-keywords)
3. [Core Concepts](#3-core-concepts)
   - [Strings](#31-strings-and-string-manipulation)
   - [Arrays](#32-arrays)
   - [Collections Framework](#33-collections-list-set-map)
   - [ArrayList, LinkedList, HashSet, HashMap](#34-arraylist-linkedlist-hashset-hashmap)
   - [Exception Handling](#35-exception-handling)
   - [Wrapper Classes](#36-wrapper-classes)
   - [Generics](#37-generics)
   - [File Handling](#38-file-handling)
4. [Java 8 Features](#4-java-8-features)
   - [Lambda Expressions](#41-lambda-expressions)
   - [Functional Interfaces](#42-functional-interfaces)
   - [Stream API](#43-stream-api)
   - [Optional](#44-optional)
   - [Method References](#45-method-references)

---

# 1. Java Basics

## 1.1 JDK, JRE, JVM

Java is a **platform-independent** language: *"Write Once, Run Anywhere" (WORA)*. Source code is compiled into **bytecode** (`.class` files), which runs on any machine that has a JVM.

### Relationship

```
JDK  =  JRE  +  Development Tools (javac, jar, javadoc, debugger)
JRE  =  JVM  +  Core Libraries (java.lang, java.util, ...)
JVM  =  Executes bytecode
```

| Component | Full Form | Purpose |
|-----------|-----------|---------|
| **JVM** | Java Virtual Machine | Runs bytecode; provides memory management and garbage collection. Platform-specific. |
| **JRE** | Java Runtime Environment | JVM + libraries needed to *run* Java programs. |
| **JDK** | Java Development Kit | JRE + compiler and tools needed to *develop* Java programs. |

### How a Java program runs

```
Hello.java  --javac-->  Hello.class (bytecode)  --JVM-->  Machine code  --> Output
```

1. **Write** the source code (`.java`).
2. **Compile** with `javac` into bytecode (`.class`).
3. **Run** with `java`. The JVM loads the class, verifies the bytecode, and executes it (using the interpreter and JIT compiler).

### JVM Architecture (simplified)

- **Class Loader**: loads `.class` files.
- **Runtime Data Areas**: Heap (objects), Stack (method calls, local variables), Method Area (class metadata), PC Register, Native Method Stack.
- **Execution Engine**: Interpreter, JIT (Just-In-Time) compiler, Garbage Collector.

### First program

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

```bash
javac Hello.java
java Hello
```

---

## 1.2 Variables and Data Types

A **variable** is a named memory location that stores a value.

```java
dataType variableName = value;
int age = 25;
```

### Types of variables

| Type | Where declared | Scope |
|------|----------------|-------|
| **Local** | Inside a method/block | Only inside that method/block. Must be initialized before use. |
| **Instance** | Inside a class, outside methods | Each object has its own copy. |
| **Static (class)** | Inside a class with `static` | One copy shared by all objects. |

### Primitive data types (8)

| Type | Size | Range / Values | Default |
|------|------|----------------|---------|
| `byte` | 1 byte | -128 to 127 | 0 |
| `short` | 2 bytes | -32,768 to 32,767 | 0 |
| `int` | 4 bytes | about -2.1 billion to 2.1 billion | 0 |
| `long` | 8 bytes | about -9.2 x 10^18 to 9.2 x 10^18 | 0L |
| `float` | 4 bytes | ~6-7 decimal digits precision | 0.0f |
| `double` | 8 bytes | ~15 decimal digits precision | 0.0d |
| `char` | 2 bytes | Single Unicode character (0 to 65,535) | '\u0000' |
| `boolean` | JVM-dependent | `true` or `false` | false |

```java
byte  b = 100;
short s = 20000;
int   i = 100000;
long  l = 10000000000L;   // note the L suffix
float f = 3.14f;          // note the f suffix
double d = 3.14159;
char  c = 'A';
boolean flag = true;
```

### Non-primitive (reference) types

Strings, arrays, classes, interfaces, enums. They store a **reference (address)** to an object on the heap. Default value is `null`.

### Other useful points

```java
// var (Java 10+): type inference for local variables
var name = "Java";          // inferred as String

// Constants
final double PI = 3.14159;  // cannot be reassigned

// Literals and underscores
int million = 1_000_000;
int binary  = 0b1010;       // 10
int hex     = 0xFF;         // 255
int octal   = 017;          // 15
```

### Naming rules

- Can contain letters, digits, `_`, `$`. Cannot start with a digit.
- Cannot be a keyword (`class`, `int`, ...).
- Case-sensitive. Convention: `camelCase` for variables/methods, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants.

---

## 1.3 Operators

### Arithmetic

| Operator | Meaning | Example |
|----------|---------|---------|
| `+` | Addition (also string concat) | `5 + 3` -> 8 |
| `-` | Subtraction | `5 - 3` -> 2 |
| `*` | Multiplication | `5 * 3` -> 15 |
| `/` | Division (integer division truncates) | `7 / 2` -> 3 |
| `%` | Modulus (remainder) | `7 % 2` -> 1 |

### Unary

```java
int a = 5;
a++;   // post-increment: use then increase
++a;   // pre-increment: increase then use
a--;   // post-decrement
--a;   // pre-decrement
int neg = -a;
boolean notFlag = !true;
```

```java
int x = 5;
int y = x++ + ++x;   // 5 + 7 = 12   (x++ gives 5, x becomes 6, ++x makes 7)
```

### Relational (comparison)

`==`, `!=`, `>`, `<`, `>=`, `<=` (all return `boolean`)

> For objects, `==` compares **references**. Use `.equals()` to compare content.

### Logical

| Operator | Meaning |
|----------|---------|
| `&&` | AND (short-circuit: if left is false, right is not evaluated) |
| `\|\|` | OR (short-circuit: if left is true, right is not evaluated) |
| `!` | NOT |

### Assignment

`=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=`

```java
int n = 10;
n += 5;   // n = n + 5 -> 15
```

### Bitwise

| Operator | Meaning | Example |
|----------|---------|---------|
| `&` | AND | `5 & 3` -> 1 |
| `\|` | OR | `5 \| 3` -> 7 |
| `^` | XOR | `5 ^ 3` -> 6 |
| `~` | Complement | `~5` -> -6 |
| `<<` | Left shift | `5 << 1` -> 10 |
| `>>` | Signed right shift | `-8 >> 1` -> -4 |
| `>>>` | Unsigned right shift | fills with 0 |

### Ternary

```java
int max = (a > b) ? a : b;
```

### instanceof

```java
String s = "hi";
boolean r = s instanceof String;   // true

// Pattern matching (Java 16+)
Object o = "hello";
if (o instanceof String str) {
    System.out.println(str.length());
}
```

### Precedence (high to low, simplified)

`() []  .` > `++ -- ! ~ (unary)` > `* / %` > `+ -` > `<< >> >>>` > `< <= > >= instanceof` > `== !=` > `&` > `^` > `|` > `&&` > `||` > `?:` > `= += -= ...`

---

## 1.4 Conditional Statements

### if / else if / else

```java
int marks = 82;

if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 75) {
    System.out.println("Grade B");
} else if (marks >= 50) {
    System.out.println("Grade C");
} else {
    System.out.println("Fail");
}
```

### switch (classic)

Works with `byte, short, int, char, String, enum` (and wrapper types). Without `break`, execution **falls through** to the next case.

```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Other day");
}
```

### Enhanced switch (Java 14+)

```java
String type = switch (day) {
    case 1, 7       -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default         -> "Invalid";
};
```

- No fall-through with `->`.
- Can be used as an expression that returns a value. Use `yield` inside block bodies.

---

## 1.5 Loops

### for loop

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

Structure: `for (initialization; condition; update)`

### while loop (condition checked first)

```java
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

### do-while loop (runs at least once)

```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

### Enhanced for loop (for-each)

```java
int[] nums = {10, 20, 30};
for (int n : nums) {
    System.out.println(n);
}
```

### break, continue, labels

```java
for (int i = 1; i <= 10; i++) {
    if (i == 3) continue;   // skip this iteration
    if (i == 6) break;      // exit the loop
    System.out.println(i);  // 1 2 4 5
}

// Labeled break: exits the outer loop
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) break outer;
        System.out.println(i + "," + j);
    }
}
```

### Infinite loops

```java
while (true) { /* ... break when needed */ }
for (;;)     { /* ... */ }
```

---

## 1.6 Type Casting

Converting one data type into another.

### Widening (implicit / automatic)

Smaller type to larger type. Safe, no data loss.

```
byte -> short -> int -> long -> float -> double
              char -> int
```

```java
int i = 100;
long l = i;       // automatic
double d = l;     // automatic
```

### Narrowing (explicit / manual)

Larger type to smaller type. May lose data. Needs a cast.

```java
double d = 9.78;
int i = (int) d;        // 9 (decimal part truncated)

int big = 130;
byte b = (byte) big;    // -126 (overflow wraps around)
```

### Reference type casting (Upcasting / Downcasting)

```java
Animal a = new Dog();     // upcasting (implicit, safe)
Dog d = (Dog) a;          // downcasting (explicit, may throw ClassCastException)

if (a instanceof Dog) {   // check before downcasting
    Dog safe = (Dog) a;
}
```

### Other conversions

```java
int n = Integer.parseInt("123");     // String -> int
String s = String.valueOf(123);      // int -> String
String s2 = Integer.toString(123);
char c = (char) 65;                  // 'A'
int code = 'A';                      // 65
```

> Note: in expressions, `byte`, `short`, `char` are promoted to `int` automatically. `byte a = 10; byte b = 20; byte c = a + b;` is a compile error; use `(byte)(a + b)`.

---

# 2. Object-Oriented Programming

**OOP** organizes code around **objects** (data + behavior). The four pillars are **Encapsulation, Inheritance, Polymorphism, Abstraction**.

## 2.1 Classes and Objects

- **Class**: a blueprint/template that defines fields (state) and methods (behavior).
- **Object**: an instance of a class, created at runtime with `new`.

```java
public class Car {
    // fields (state)
    String brand;
    int speed;

    // method (behavior)
    void accelerate(int amount) {
        speed += amount;
        System.out.println(brand + " speed: " + speed);
    }
}

public class Main {
    public static void main(String[] args) {
        Car c1 = new Car();     // object creation
        c1.brand = "Toyota";
        c1.accelerate(20);

        Car c2 = new Car();
        c2.brand = "Honda";
        c2.accelerate(50);
    }
}
```

### Key points

- `new` allocates memory on the **heap** and returns a reference.
- The reference variable (`c1`) lives on the stack and points to the heap object.
- The `this` keyword refers to the current object.
- Class members: fields, methods, constructors, initializer blocks, nested classes.

### Access modifiers

| Modifier | Same class | Same package | Subclass (other pkg) | Everywhere |
|----------|:---------:|:------------:|:--------------------:|:----------:|
| `private` | Yes | No | No | No |
| *(default)* | Yes | Yes | No | No |
| `protected` | Yes | Yes | Yes | No |
| `public` | Yes | Yes | Yes | Yes |

---

## 2.2 Constructors

A **constructor** initializes a new object. It has the **same name as the class** and **no return type**. It is called automatically by `new`.

### Types

```java
public class Student {
    String name;
    int age;

    // 1. Default (no-arg) constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // 2. Parameterized constructor
    Student(String name, int age) {
        this.name = name;     // 'this' distinguishes field from parameter
        this.age = age;
    }

    // 3. Copy constructor (user-defined)
    Student(Student other) {
        this.name = other.name;
        this.age = other.age;
    }
}
```

### Constructor chaining

```java
class Student {
    String name; int age;

    Student() {
        this("Unknown", 0);         // calls another constructor of same class
    }
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

```java
class Child extends Parent {
    Child() {
        super();                    // calls parent constructor (must be first statement)
    }
}
```

### Important rules

- If you write **no** constructor, the compiler provides a default no-arg constructor.
- If you write **any** constructor, the compiler does **not** add a default one.
- Constructors are **not inherited** and cannot be `abstract`, `static`, `final`, or `synchronized`.
- `this(...)` or `super(...)` must be the **first statement**; only one of them per constructor.
- A constructor can be `private` (used in Singleton pattern).

---

## 2.3 Inheritance

A class (**subclass / child**) acquires the properties and methods of another class (**superclass / parent**) using `extends`. It represents an **IS-A** relationship and promotes **code reuse**.

```java
class Animal {
    String name;
    void eat() {
        System.out.println(name + " is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.name = "Bruno";
        d.eat();     // inherited
        d.bark();
    }
}
```

### Types of inheritance in Java

| Type | Supported? |
|------|-----------|
| Single (A -> B) | Yes |
| Multilevel (A -> B -> C) | Yes |
| Hierarchical (A -> B, A -> C) | Yes |
| Multiple (class extends 2 classes) | **No** (diamond problem), achieved via interfaces |
| Hybrid | Only via interfaces |

### The `super` keyword

```java
class Parent {
    String msg = "Parent";
    void show() { System.out.println("Parent show"); }
}

class Child extends Parent {
    String msg = "Child";
    void show() {
        super.show();                       // call parent method
        System.out.println(super.msg);      // access parent field
        System.out.println(this.msg);
    }
}
```

### Key points

- Every class implicitly extends `java.lang.Object`.
- `private` members are not accessible in the subclass directly.
- A `final` class cannot be extended. A `final` method cannot be overridden.
- Constructors run **parent first, then child**.

### Composition (HAS-A)

Prefer composition when the relationship is not truly IS-A.

```java
class Engine { }
class Car {
    private Engine engine = new Engine();   // Car HAS-A Engine
}
```

---

## 2.4 Polymorphism

"Many forms": the same method call behaves differently based on context.

| Type | Also called | Resolved at | Achieved by |
|------|-------------|-------------|-------------|
| **Compile-time** | Static binding | Compile time | Method **overloading** |
| **Runtime** | Dynamic binding | Run time | Method **overriding** |

### Runtime polymorphism (dynamic method dispatch)

```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Woof"); }
}
class Cat extends Animal {
    @Override
    void sound() { System.out.println("Meow"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog();   // parent reference, child object
        Animal a2 = new Cat();
        a1.sound();   // Woof
        a2.sound();   // Meow
    }
}
```

The **object's actual type** (not the reference type) decides which overridden method runs.

### Use case: treating different objects uniformly

```java
Animal[] zoo = { new Dog(), new Cat(), new Dog() };
for (Animal a : zoo) {
    a.sound();
}
```

> Fields and static methods are **not** polymorphic. They are resolved by reference type.

---

## 2.5 Encapsulation

**Binding data and the methods that operate on it into a single unit (class)**, and **restricting direct access** to the data. This is called **data hiding**.

### How to achieve it

1. Declare fields `private`.
2. Provide `public` getters and setters.
3. Put validation logic in setters.

```java
public class BankAccount {
    private double balance;           // hidden

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            throw new IllegalArgumentException("Amount must be positive");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            throw new IllegalArgumentException("Invalid withdrawal");
        }
    }
}
```

### Benefits

- **Security**: internal state cannot be corrupted from outside.
- **Flexibility**: internals can change without breaking callers.
- **Validation** and control over how data is set.
- Can create **read-only** (getter only) or **write-only** classes.

### Immutable class (advanced encapsulation)

```java
public final class Point {
    private final int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
    public int getX() { return x; }
    public int getY() { return y; }
}
```

(Or use a `record` in Java 16+: `record Point(int x, int y) {}`.)

---

## 2.6 Abstraction

**Hiding implementation details and showing only essential features.** Focus on *what* an object does, not *how*.

Achieved using **abstract classes** (0-100% abstraction) and **interfaces** (100% abstraction up to Java 7; more flexible since Java 8).

### Abstract class

```java
abstract class Shape {
    String color;

    Shape(String color) { this.color = color; }   // can have constructors

    abstract double area();                       // abstract method (no body)

    void display() {                              // concrete method
        System.out.println("Color: " + color + ", Area: " + area());
    }
}

class Circle extends Shape {
    double radius;
    Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    @Override
    double area() { return Math.PI * radius * radius; }
}

class Rectangle extends Shape {
    double w, h;
    Rectangle(String color, double w, double h) {
        super(color);
        this.w = w; this.h = h;
    }
    @Override
    double area() { return w * h; }
}
```

### Rules for abstract classes

- Declared with the `abstract` keyword; **cannot be instantiated**.
- May contain abstract and non-abstract methods, fields, constructors, static methods.
- A subclass must implement **all** abstract methods, or itself be declared `abstract`.
- Abstract methods cannot be `private`, `final`, or `static`.

---

## 2.7 Interfaces

An **interface** is a contract that defines *what* a class must do. A class **implements** it.

```java
interface Drawable {
    void draw();                       // implicitly public abstract
}

interface Resizable {
    void resize(int percent);
}

class Circle implements Drawable, Resizable {   // multiple interfaces allowed
    @Override
    public void draw() { System.out.println("Drawing circle"); }

    @Override
    public void resize(int percent) { System.out.println("Resized by " + percent + "%"); }
}
```

### Features by Java version

```java
interface Vehicle {
    int MAX_SPEED = 200;                // implicitly public static final

    void start();                       // abstract

    default void honk() {               // Java 8: default method (has body)
        System.out.println("Beep!");
    }

    static void info() {                // Java 8: static method
        System.out.println("Vehicle interface");
    }

    private void helper() {             // Java 9: private method
        System.out.println("helper");
    }
}
```

### Interface vs Abstract class

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| Keyword | `interface` / `implements` | `abstract class` / `extends` |
| Multiple inheritance | Yes (a class can implement many) | No (extend only one) |
| Fields | `public static final` only | Any kind |
| Constructors | No | Yes |
| Methods | abstract, default, static, private | abstract and concrete |
| Use when | Defining a capability/contract | Sharing common state/code among related classes |

### Other points

- An interface can **extend** one or more interfaces: `interface A extends B, C`.
- **Marker interface**: empty interface (e.g., `Serializable`, `Cloneable`).
- **Functional interface**: exactly one abstract method (see Java 8 section).
- If two interfaces have the same default method, the implementing class **must override** it to resolve the conflict (`InterfaceName.super.method()`).

---

## 2.8 Method Overloading and Overriding

### Overloading (compile-time polymorphism)

Same method name, **different parameter list** (number, type, or order) in the **same class**. Return type alone cannot differentiate.

```java
class Calculator {
    int add(int a, int b)           { return a + b; }
    int add(int a, int b, int c)    { return a + b + c; }
    double add(double a, double b)  { return a + b; }
}
```

### Overriding (runtime polymorphism)

A subclass provides its **own implementation** of a method already defined in the parent, with the **same signature**.

```java
class Animal {
    void sound() { System.out.println("..."); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Woof"); }
}
```

### Rules for overriding

- Same name, same parameters.
- Return type: same, or a **covariant** (subtype) return type.
- Access level: cannot be **more restrictive** (can be wider).
- Cannot override `static`, `final`, or `private` methods (static/private are *hidden*, not overridden).
- Overriding method cannot throw **broader checked exceptions**.
- Use `@Override` so the compiler catches mistakes.

### Comparison

| Aspect | Overloading | Overriding |
|--------|-------------|------------|
| Location | Same class | Parent and child class |
| Parameters | Must differ | Must be the same |
| Return type | Can differ | Same or covariant |
| Binding | Compile-time | Runtime |
| Inheritance needed | No | Yes |

---

## 2.9 Static and Final Keywords

### `static`

Belongs to the **class**, not to any particular object.

```java
public class Counter {
    static int count = 0;            // shared by all objects
    int id;

    Counter() {
        count++;
        id = count;
    }

    static void showCount() {        // call with Counter.showCount()
        System.out.println("Total: " + count);
    }

    static {                         // static block: runs once when class loads
        System.out.println("Class loaded");
    }
}
```

| Use | Meaning |
|-----|---------|
| **static variable** | One copy shared across all instances |
| **static method** | Called without an object; can access only static members directly; no `this`/`super` |
| **static block** | Runs once at class loading, used for static initialization |
| **static nested class** | Nested class that doesn't need an outer instance |
| **static import** | `import static java.lang.Math.*;` |

### `final`

Means "cannot be changed".

| Applied to | Effect |
|------------|--------|
| **Variable** | Value can be assigned only once (constant) |
| **Method** | Cannot be overridden |
| **Class** | Cannot be extended (e.g., `String`, `Integer`) |
| **Parameter** | Cannot be reassigned inside the method |

```java
final int MAX = 100;
// MAX = 200;                // compile error

final List<String> list = new ArrayList<>();
list.add("ok");              // allowed: the object's content can change
// list = new ArrayList<>(); // error: reference cannot change

class Parent {
    final void show() { }    // cannot be overridden
}
final class Util { }         // cannot be subclassed
```

### `static final` constants

```java
public static final double PI = 3.14159;
```

> A `final` blank variable (declared without a value) must be initialized in the constructor (or initializer block). A `final static` blank variable must be initialized in a static block.

---

# 3. Core Concepts

## 3.1 Strings and String Manipulation

`String` is an **immutable** sequence of characters (class in `java.lang`). Once created, its content cannot change; operations return a **new** String.

### Creating strings

```java
String s1 = "Hello";               // String literal (stored in String Pool)
String s2 = "Hello";               // reuses the same pool object
String s3 = new String("Hello");   // new object on heap (outside pool)

System.out.println(s1 == s2);        // true  (same reference)
System.out.println(s1 == s3);        // false (different objects)
System.out.println(s1.equals(s3));   // true  (same content)
System.out.println(s3.intern() == s1); // true
```

### Common methods

```java
String s = "  Java Programming  ";

s.length();                  // 20
s.trim();                    // "Java Programming"   (strip() in Java 11+)
s.toUpperCase();             // "  JAVA PROGRAMMING  "
s.toLowerCase();
s.charAt(2);                 // 'J'
s.indexOf("a");              // 3
s.lastIndexOf("a");
s.contains("Java");          // true
s.startsWith("  J");         // true
s.endsWith("  ");            // true
s.isEmpty();                 // false
s.isBlank();                 // false (Java 11)

String t = "Hello World";
t.substring(6);              // "World"
t.substring(0, 5);           // "Hello"   (end index exclusive)
t.replace('l', 'L');         // "HeLLo WorLd"
t.replace("World", "Java");  // "Hello Java"
t.replaceAll("[aeiou]", "*");// regex replace
t.split(" ");                // ["Hello", "World"]
t.concat("!");               // "Hello World!"
t.equals("hello world");     // false
t.equalsIgnoreCase("hello world"); // true
t.compareTo("Hello");        // positive (lexicographic comparison)
"ab".repeat(3);              // "ababab" (Java 11)
String.join("-", "a", "b", "c");   // "a-b-c"
String.valueOf(42);          // "42"
t.toCharArray();             // char[]
String.format("Name: %s, Age: %d, GPA: %.2f", "Ann", 20, 3.456);
```

### StringBuilder and StringBuffer (mutable)

Use them when you modify strings frequently (loops, concatenations).

| Class | Mutable | Thread-safe | Speed |
|-------|:------:|:-----------:|-------|
| `String` | No | Yes (immutable) | Slow for repeated changes |
| `StringBuilder` | Yes | No | Fastest |
| `StringBuffer` | Yes | Yes (synchronized) | Slower than StringBuilder |

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");       // Hello World
sb.insert(0, ">> ");       // >> Hello World
sb.reverse();              // dlroW olleH >>
sb.deleteCharAt(0);
sb.setCharAt(0, 'D');
String result = sb.toString();
```

### Examples

```java
// Palindrome check
static boolean isPalindrome(String s) {
    return new StringBuilder(s).reverse().toString().equalsIgnoreCase(s);
}

// Count vowels
static int countVowels(String s) {
    int count = 0;
    for (char c : s.toLowerCase().toCharArray()) {
        if ("aeiou".indexOf(c) != -1) count++;
    }
    return count;
}

// Text blocks (Java 15+)
String json = """
    {
      "name": "Java",
      "version": 21
    }
    """;
```

---

## 3.2 Arrays

An **array** is a fixed-size, ordered collection of elements of the **same type**, stored in contiguous memory. Index starts at **0**.

### Declaration and initialization

```java
int[] a = new int[5];                 // [0, 0, 0, 0, 0]
int[] b = {10, 20, 30, 40};           // literal initialization
String[] names = new String[]{"A", "B", "C"};

a[0] = 99;
System.out.println(b.length);         // 4  (length is a field, not a method)
```

Accessing an invalid index throws `ArrayIndexOutOfBoundsException`.

### Traversing

```java
for (int i = 0; i < b.length; i++) System.out.println(b[i]);
for (int x : b) System.out.println(x);
```

### Multi-dimensional arrays

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
System.out.println(matrix[1][2]);     // 6

for (int[] row : matrix) {
    for (int val : row) System.out.print(val + " ");
    System.out.println();
}

// Jagged array (rows of different lengths)
int[][] jagged = new int[3][];
jagged[0] = new int[]{1};
jagged[1] = new int[]{1, 2};
jagged[2] = new int[]{1, 2, 3};
```

### `java.util.Arrays` utility class

```java
import java.util.Arrays;

int[] arr = {5, 2, 9, 1};

Arrays.sort(arr);                         // [1, 2, 5, 9]
int idx = Arrays.binarySearch(arr, 5);    // 2 (array must be sorted)
System.out.println(Arrays.toString(arr)); // [1, 2, 5, 9]
int[] copy  = Arrays.copyOf(arr, 6);      // [1,2,5,9,0,0]
int[] range = Arrays.copyOfRange(arr, 1, 3); // [2, 5]
Arrays.fill(arr, 7);                      // [7, 7, 7, 7]
Arrays.equals(arr, copy);
Arrays.deepToString(new int[][]{{1,2},{3,4}}); // [[1, 2], [3, 4]]
List<Integer> list = Arrays.asList(1, 2, 3);   // fixed-size list
```

### Limitations

- Fixed size (use `ArrayList` for dynamic size).
- Only one element type (primitive or object).

---

## 3.3 Collections (List, Set, Map)

The **Java Collections Framework (JCF)** provides ready-made data structures and algorithms in `java.util`.

### Hierarchy

```
Iterable
   |
Collection
   |-- List     (ordered, allows duplicates)  -> ArrayList, LinkedList, Vector, Stack
   |-- Set      (no duplicates)               -> HashSet, LinkedHashSet, TreeSet
   |-- Queue    (FIFO)                        -> PriorityQueue, ArrayDeque, LinkedList

Map  (key -> value pairs; NOT a child of Collection)
   -> HashMap, LinkedHashMap, TreeMap, Hashtable
```

### Overview

| Interface | Ordered | Duplicates | Key characteristic |
|-----------|---------|-----------|--------------------|
| **List** | Insertion order, index-based | Allowed | Access by index |
| **Set** | Depends on implementation | Not allowed | Uniqueness |
| **Map** | Depends on implementation | Keys unique, values can repeat | Key-value pairs |
| **Queue** | FIFO / priority | Allowed | Processing order |

### Common Collection methods

`add()`, `addAll()`, `remove()`, `contains()`, `size()`, `isEmpty()`, `clear()`, `iterator()`, `stream()`

### Iterating

```java
List<String> list = List.of("A", "B", "C");

for (String s : list) System.out.println(s);        // for-each
list.forEach(System.out::println);                   // Java 8

Iterator<String> it = new ArrayList<>(list).iterator();
while (it.hasNext()) {
    String s = it.next();
    // it.remove() is the safe way to remove while iterating
}
```

### Collections utility class

```java
List<Integer> nums = new ArrayList<>(List.of(5, 3, 8, 1));
Collections.sort(nums);                 // [1, 3, 5, 8]
Collections.reverse(nums);
Collections.shuffle(nums);
Collections.max(nums);
Collections.min(nums);
Collections.unmodifiableList(nums);
```

### Comparable vs Comparator (sorting objects)

```java
class Student implements Comparable<Student> {
    String name; int marks;
    Student(String n, int m) { name = n; marks = m; }

    @Override
    public int compareTo(Student o) {       // natural ordering
        return Integer.compare(this.marks, o.marks);
    }
}

// Comparator: custom/external ordering
list.sort(Comparator.comparing(Student::getName));
list.sort(Comparator.comparingInt((Student s) -> s.marks).reversed());
```

### Immutable factories (Java 9+)

```java
List<String> l = List.of("a", "b");
Set<Integer> s = Set.of(1, 2, 3);
Map<String,Integer> m = Map.of("a", 1, "b", 2);
```

---

## 3.4 ArrayList, LinkedList, HashSet, HashMap

### ArrayList

Resizable array implementation of `List`. Fast random access, slower inserts/removals in the middle.

```java
import java.util.*;

List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add(1, "Mango");          // insert at index
fruits.get(0);                   // "Apple"
fruits.set(0, "Grapes");         // replace
fruits.remove("Banana");         // remove by object
fruits.remove(0);                // remove by index
fruits.contains("Mango");
fruits.indexOf("Mango");
fruits.size();
```

- Internally an array; grows by ~50% when full.
- `get(i)`: O(1). `add(end)`: amortized O(1). `add/remove(middle)`: O(n).
- Not synchronized.

### LinkedList

Doubly-linked list. Implements both `List` and `Deque`.

```java
LinkedList<Integer> ll = new LinkedList<>();
ll.add(10);
ll.addFirst(5);
ll.addLast(20);
ll.removeFirst();
ll.peekFirst();
ll.getLast();
```

- `get(i)`: O(n). `addFirst/addLast/removeFirst`: O(1).
- Uses more memory (node objects with prev/next pointers).

| | ArrayList | LinkedList |
|---|-----------|------------|
| Structure | Dynamic array | Doubly linked list |
| Random access | Fast, O(1) | Slow, O(n) |
| Insert/delete in middle | Slow, O(n) | Fast once positioned, O(1) |
| Memory | Less | More |
| Best for | Reading/searching | Frequent insert/delete at ends |

### HashSet

Stores **unique** elements using a hash table. **No guaranteed order.**

```java
Set<String> set = new HashSet<>();
set.add("Java");
set.add("Python");
set.add("Java");             // ignored (duplicate)
System.out.println(set.size());   // 2
set.contains("Python");      // true (O(1) average)
set.remove("Java");
```

- Backed by a `HashMap` internally.
- Uses `hashCode()` and `equals()` to detect duplicates. **Override both** for custom classes.
- Allows one `null`.
- Variants: `LinkedHashSet` (insertion order), `TreeSet` (sorted order).

### HashMap

Stores **key-value pairs**. Keys are unique; values can repeat. **No guaranteed order.**

```java
Map<String, Integer> map = new HashMap<>();
map.put("Alice", 90);
map.put("Bob", 85);
map.put("Alice", 95);                 // overwrites value for existing key

map.get("Alice");                     // 95
map.getOrDefault("Zed", 0);           // 0
map.containsKey("Bob");               // true
map.containsValue(85);                // true
map.remove("Bob");
map.putIfAbsent("Carl", 70);
map.size();

// Iterating
for (Map.Entry<String, Integer> e : map.entrySet()) {
    System.out.println(e.getKey() + " = " + e.getValue());
}
for (String k : map.keySet())      { }
for (Integer v : map.values())     { }
map.forEach((k, v) -> System.out.println(k + " -> " + v));

// Useful Java 8 methods
map.merge("Alice", 5, Integer::sum);                  // add 5 to existing
map.computeIfAbsent("Dan", k -> 60);
```

#### How HashMap works (interview favorite)

1. `key.hashCode()` is computed and mapped to a **bucket index**.
2. If the bucket is empty, the entry is stored there.
3. On collision, entries form a **linked list** in that bucket (converted to a **balanced tree** when a bucket exceeds 8 entries, Java 8+).
4. `equals()` finds the exact key within the bucket.
5. Default capacity is 16, load factor 0.75; it **resizes (doubles)** when 75% full.

| Map | Order | Null keys | Thread-safe | Complexity |
|-----|-------|-----------|-------------|-----------|
| `HashMap` | None | 1 null key | No | O(1) avg |
| `LinkedHashMap` | Insertion | 1 null key | No | O(1) |
| `TreeMap` | Sorted by key | No null key | No | O(log n) |
| `Hashtable` | None | No nulls | Yes (legacy) | O(1) |
| `ConcurrentHashMap` | None | No nulls | Yes | O(1) |

---

## 3.5 Exception Handling

An **exception** is an event that disrupts normal program flow. Exception handling lets you manage errors gracefully.

### Hierarchy

```
Throwable
 |-- Error                     (serious, don't catch: OutOfMemoryError, StackOverflowError)
 |-- Exception
      |-- Checked exceptions   (compile-time: IOException, SQLException, FileNotFoundException)
      |-- RuntimeException     (unchecked: NullPointerException, ArithmeticException,
                                ArrayIndexOutOfBoundsException, IllegalArgumentException,
                                ClassCastException, NumberFormatException)
```

| Type | Checked at | Must handle? |
|------|-----------|-------------|
| **Checked** | Compile time | Yes (`try-catch` or `throws`) |
| **Unchecked** (RuntimeException) | Run time | No (optional) |
| **Error** | Run time | Normally no |

### try-catch-finally

```java
try {
    int result = 10 / 0;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} catch (Exception e) {            // more general catch must come AFTER specific ones
    System.out.println("General error");
} finally {
    System.out.println("Always runs (cleanup)");
}
```

### Multi-catch

```java
try {
    // ...
} catch (NumberFormatException | NullPointerException e) {
    System.out.println(e);
}
```

### throw vs throws

```java
// throw: actually throws an exception object
static void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Under 18");
    }
}

// throws: declares that a method may throw a checked exception
static void readFile() throws IOException {
    throw new IOException("File problem");
}
```

### try-with-resources (auto-closing, Java 7+)

Resource must implement `AutoCloseable`.

```java
try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
}   // br.close() called automatically
```

### Custom exceptions

```java
// Checked custom exception
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// Unchecked custom exception
class InvalidInputException extends RuntimeException {
    public InvalidInputException(String message) {
        super(message);
    }
}

// Usage
static void withdraw(double bal, double amt) throws InsufficientFundsException {
    if (amt > bal) throw new InsufficientFundsException("Not enough balance");
}
```

### Key points

- `finally` runs whether or not an exception occurs (except `System.exit()` or JVM crash).
- A `try` needs at least one `catch` or a `finally`.
- Catch **specific** exceptions first, general ones last.
- Don't swallow exceptions silently; log or handle them.
- Useful methods: `getMessage()`, `printStackTrace()`, `getCause()`.

---

## 3.6 Wrapper Classes

Each primitive has a corresponding **object** type in `java.lang`. Needed because collections and generics work only with objects.

| Primitive | Wrapper |
|-----------|---------|
| `byte` | `Byte` |
| `short` | `Short` |
| `int` | `Integer` |
| `long` | `Long` |
| `float` | `Float` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

### Autoboxing and unboxing

```java
int a = 10;
Integer boxed = a;            // autoboxing: int -> Integer
int b = boxed;                // unboxing: Integer -> int

List<Integer> list = new ArrayList<>();
list.add(5);                  // autoboxing happens automatically
int x = list.get(0);          // unboxing
```

### Useful methods

```java
Integer.parseInt("123");              // String -> int
Integer.valueOf("123");               // String -> Integer
Integer.toString(123);                // int -> String
Integer.MAX_VALUE;                    // 2147483647
Integer.MIN_VALUE;
Integer.compare(3, 5);                // -1
Integer.toBinaryString(10);           // "1010"
Integer.toHexString(255);             // "ff"
Double.parseDouble("3.14");
Boolean.parseBoolean("true");
Character.isDigit('5');
Character.isLetter('a');
Character.toUpperCase('a');
```

### Gotchas

```java
Integer i1 = 127, i2 = 127;
System.out.println(i1 == i2);         // true  (cached range -128 to 127)

Integer i3 = 128, i4 = 128;
System.out.println(i3 == i4);         // false (different objects)
System.out.println(i3.equals(i4));    // true  (always use equals)

Integer n = null;
// int m = n;                         // NullPointerException on unboxing
```

- Wrapper objects are **immutable**.
- Prefer primitives for performance when objects are not needed.

---

## 3.7 Generics

Generics let you write **type-safe, reusable** code by using **type parameters**. They provide compile-time type checking and eliminate casts.

### Without vs with generics

```java
// Without generics (unsafe)
List list = new ArrayList();
list.add("text");
list.add(10);
String s = (String) list.get(1);     // ClassCastException at runtime

// With generics (safe)
List<String> names = new ArrayList<>();
names.add("text");
// names.add(10);                    // compile-time error
String s2 = names.get(0);            // no cast needed
```

### Generic class

```java
class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}

Box<Integer> intBox = new Box<>();
intBox.set(100);
Box<String> strBox = new Box<>();
strBox.set("Hello");
```

Common type parameter names: `T` (Type), `E` (Element), `K` (Key), `V` (Value), `N` (Number).

### Multiple type parameters

```java
class Pair<K, V> {
    private K key; private V value;
    Pair(K key, V value) { this.key = key; this.value = value; }
    K getKey() { return key; }
    V getValue() { return value; }
}
Pair<String, Integer> p = new Pair<>("Age", 25);
```

### Generic method

```java
public static <T> void printArray(T[] arr) {
    for (T item : arr) System.out.println(item);
}

public static <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}
```

### Bounded types

```java
class Calculator<T extends Number> {      // T must be Number or a subclass
    T value;
    double doubled() { return value.doubleValue() * 2; }
}
```

### Wildcards

| Wildcard | Meaning | Use |
|----------|---------|-----|
| `<?>` | Unknown type | Read-only generic handling |
| `<? extends Number>` | Number or subclass (upper bound) | **Reading** (producer) |
| `<? super Integer>` | Integer or superclass (lower bound) | **Writing** (consumer) |

```java
static double sum(List<? extends Number> list) {
    double total = 0;
    for (Number n : list) total += n.doubleValue();
    return total;
}
```

> Mnemonic: **PECS**: *Producer Extends, Consumer Super*.

### Important notes

- Generics work only with **reference types** (`List<Integer>`, not `List<int>`).
- **Type erasure**: generic type info is removed at runtime; the compiler enforces types at compile time.
- You cannot do `new T()`, `new T[10]`, or `static T field`.
- `List<Object>` is **not** a supertype of `List<String>` (generics are invariant).

---

## 3.8 File Handling

Java provides file I/O in `java.io` (classic) and `java.nio.file` (modern, recommended).

### The `File` class (metadata and paths)

```java
import java.io.File;

File file = new File("data.txt");
file.exists();
file.getName();
file.getAbsolutePath();
file.length();                 // size in bytes
file.isFile();
file.isDirectory();
file.createNewFile();          // throws IOException
file.delete();
new File("myDir").mkdir();
String[] names = new File(".").list();   // list directory
```

### Writing to a file

```java
import java.io.*;

// FileWriter (text)
try (FileWriter fw = new FileWriter("out.txt")) {            // overwrites
    fw.write("Hello\n");
    fw.write("Java File Handling");
} catch (IOException e) {
    e.printStackTrace();
}

// Append mode
try (FileWriter fw = new FileWriter("out.txt", true);
     BufferedWriter bw = new BufferedWriter(fw)) {
    bw.write("New line");
    bw.newLine();
} catch (IOException e) {
    e.printStackTrace();
}
```

### Reading from a file

```java
// BufferedReader (efficient line-by-line)
try (BufferedReader br = new BufferedReader(new FileReader("out.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}

// Scanner
try (Scanner sc = new Scanner(new File("out.txt"))) {
    while (sc.hasNextLine()) {
        System.out.println(sc.nextLine());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
}
```

### Modern NIO.2 (`Files` and `Path`)

```java
import java.nio.file.*;
import java.util.List;

Path path = Paths.get("notes.txt");

Files.writeString(path, "Hello NIO\n");                         // Java 11
Files.write(path, List.of("line1", "line2"));                   // write lines
String content = Files.readString(path);                        // Java 11
List<String> lines = Files.readAllLines(path);
Files.exists(path);
Files.copy(path, Paths.get("copy.txt"), StandardCopyOption.REPLACE_EXISTING);
Files.move(path, Paths.get("moved.txt"));
Files.delete(Paths.get("moved.txt"));

// Stream large files lazily
try (Stream<String> stream = Files.lines(path)) {
    stream.filter(l -> l.contains("Java")).forEach(System.out::println);
}
```

### Byte streams (binary files)

```java
try (FileInputStream in = new FileInputStream("a.jpg");
     FileOutputStream out = new FileOutputStream("b.jpg")) {
    byte[] buffer = new byte[1024];
    int n;
    while ((n = in.read(buffer)) != -1) {
        out.write(buffer, 0, n);
    }
}
```

### Serialization (saving objects)

```java
class User implements Serializable {
    private static final long serialVersionUID = 1L;
    String name;
    transient String password;       // transient: not serialized
}

// Write object
try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("user.ser"))) {
    oos.writeObject(new User());
}
// Read object
try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("user.ser"))) {
    User u = (User) ois.readObject();
}
```

### Stream types

| Kind | Classes | Data |
|------|---------|------|
| Byte streams | `InputStream`, `OutputStream`, `FileInputStream`, `FileOutputStream` | Binary (images, PDFs) |
| Character streams | `Reader`, `Writer`, `FileReader`, `FileWriter`, `BufferedReader` | Text |

> Always close resources, ideally with **try-with-resources**.

---

# 4. Java 8 Features

Java 8 (2014) introduced **functional programming** support: lambdas, streams, `Optional`, method references, default methods, and the new Date/Time API (`java.time`).

## 4.1 Lambda Expressions

A **lambda** is a concise way to represent an **anonymous function** (an implementation of a functional interface).

### Syntax

```
(parameters) -> expression
(parameters) -> { statements; }
```

### Before vs after

```java
// Anonymous class (old)
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running");
    }
};

// Lambda (Java 8)
Runnable r2 = () -> System.out.println("Running");
```

### Syntax variations

```java
() -> System.out.println("No params");            // no parameter
x -> x * x                                        // one param (parentheses optional)
(a, b) -> a + b                                   // multiple params
(int a, int b) -> a + b                           // explicit types
(a, b) -> {                                       // block body, needs return
    int sum = a + b;
    return sum;
}
```

### Examples

```java
// Sorting with a lambda
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
Collections.sort(names, (a, b) -> a.compareTo(b));
names.sort((a, b) -> b.compareTo(a));          // descending

// Iterating
names.forEach(n -> System.out.println(n));

// Threads
new Thread(() -> System.out.println("In thread")).start();

// Removing elements
names.removeIf(n -> n.startsWith("A"));
```

### Rules

- Lambdas work only with **functional interfaces**.
- Variables from the enclosing scope used inside a lambda must be **final or effectively final**.
- `this` inside a lambda refers to the **enclosing class**, unlike an anonymous class.

---

## 4.2 Functional Interfaces

An interface with **exactly one abstract method (SAM: Single Abstract Method)**. It may have any number of `default` and `static` methods. Annotate with `@FunctionalInterface` (optional, but compiler-checked).

```java
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);                 // single abstract method

    default void log() { System.out.println("Calculating"); }
}

Calculator add = (a, b) -> a + b;
Calculator mul = (a, b) -> a * b;
System.out.println(add.operate(3, 4));         // 7
System.out.println(mul.operate(3, 4));         // 12
```

Existing functional interfaces include `Runnable`, `Callable`, `Comparator`, `Comparable`.

### Built-in interfaces in `java.util.function`

| Interface | Method | Description | Example |
|-----------|--------|-------------|---------|
| `Predicate<T>` | `boolean test(T t)` | Test a condition | `s -> s.isEmpty()` |
| `Function<T,R>` | `R apply(T t)` | Transform T to R | `s -> s.length()` |
| `Consumer<T>` | `void accept(T t)` | Consume, no return | `s -> System.out.println(s)` |
| `Supplier<T>` | `T get()` | Supply a value, no input | `() -> "Hello"` |
| `UnaryOperator<T>` | `T apply(T t)` | `Function<T,T>` | `s -> s.toUpperCase()` |
| `BinaryOperator<T>` | `T apply(T a, T b)` | `BiFunction<T,T,T>` | `(a, b) -> a + b` |
| `BiFunction<T,U,R>` | `R apply(T t, U u)` | Two inputs | `(a, b) -> a + b` |
| `BiPredicate<T,U>` | `boolean test(T,U)` | Two-input test | |
| `BiConsumer<T,U>` | `void accept(T,U)` | Two-input consume | |

Primitive specializations avoid boxing: `IntPredicate`, `IntFunction`, `IntSupplier`, `ToIntFunction`, etc.

```java
Predicate<Integer> isEven = n -> n % 2 == 0;
Function<String, Integer> len = String::length;
Consumer<String> printer = System.out::println;
Supplier<Double> random = Math::random;
UnaryOperator<String> upper = String::toUpperCase;
BinaryOperator<Integer> sum = Integer::sum;

System.out.println(isEven.test(4));        // true
System.out.println(len.apply("Hello"));    // 5
printer.accept("Hi");
System.out.println(random.get());
```

### Composition

```java
Predicate<Integer> positive = n -> n > 0;
Predicate<Integer> even = n -> n % 2 == 0;

positive.and(even).test(4);       // true
positive.or(even).test(-2);       // true
positive.negate().test(5);        // false

Function<Integer, Integer> doubleIt = x -> x * 2;
Function<Integer, Integer> addTen   = x -> x + 10;

doubleIt.andThen(addTen).apply(5);   // (5*2)+10 = 20
doubleIt.compose(addTen).apply(5);   // (5+10)*2 = 30
```

---

## 4.3 Stream API

A **Stream** is a sequence of elements supporting **functional-style operations** on collections/arrays. A stream **does not store data** and **does not modify the source**.

### Pipeline structure

```
Source  ->  Intermediate operations (lazy)  ->  Terminal operation (triggers execution)
```

```java
List<Integer> result = numbers.stream()      // source
        .filter(n -> n % 2 == 0)             // intermediate
        .map(n -> n * n)                     // intermediate
        .collect(Collectors.toList());       // terminal
```

### Creating streams

```java
list.stream();
Arrays.stream(array);
Stream.of(1, 2, 3);
IntStream.range(1, 5);               // 1,2,3,4
IntStream.rangeClosed(1, 5);         // 1..5
Stream.iterate(1, x -> x * 2).limit(5);   // 1,2,4,8,16
Stream.generate(Math::random).limit(3);
list.parallelStream();               // parallel processing
```

### Intermediate operations (return a Stream, lazy)

| Operation | Purpose |
|-----------|---------|
| `filter(Predicate)` | Keep matching elements |
| `map(Function)` | Transform each element |
| `flatMap(Function)` | Flatten nested streams |
| `distinct()` | Remove duplicates |
| `sorted()` / `sorted(Comparator)` | Sort |
| `limit(n)` / `skip(n)` | Truncate / skip |
| `peek(Consumer)` | Debugging / side effects |
| `mapToInt()`, `mapToDouble()` | Convert to primitive streams |

### Terminal operations (trigger the pipeline)

| Operation | Purpose |
|-----------|---------|
| `forEach(Consumer)` | Perform action on each |
| `collect(Collector)` | Gather into a collection/map/string |
| `toList()` | Immutable list (Java 16+) |
| `count()` | Number of elements |
| `reduce(identity, BinaryOperator)` | Combine into one value |
| `min()` / `max(Comparator)` | Smallest / largest |
| `findFirst()` / `findAny()` | Returns `Optional` |
| `anyMatch()` / `allMatch()` / `noneMatch()` | Boolean checks |
| `toArray()` | Convert to array |

### Examples

```java
List<Integer> nums = Arrays.asList(5, 2, 8, 1, 9, 2, 4);

// Filter + map + collect
List<Integer> squaresOfEvens = nums.stream()
        .filter(n -> n % 2 == 0)
        .map(n -> n * n)
        .collect(Collectors.toList());              // [4, 64, 4, 16]

// Distinct and sorted
nums.stream().distinct().sorted().toList();          // [1, 2, 4, 5, 8, 9]
nums.stream().sorted(Comparator.reverseOrder()).toList();

// Reduce
int sum = nums.stream().reduce(0, Integer::sum);     // 31
Optional<Integer> max = nums.stream().max(Integer::compare);

// Primitive streams
int total = nums.stream().mapToInt(Integer::intValue).sum();
double avg = nums.stream().mapToInt(i -> i).average().orElse(0);
IntSummaryStatistics stats = nums.stream().mapToInt(i -> i).summaryStatistics();

// Matching
boolean anyBig  = nums.stream().anyMatch(n -> n > 8);   // true
boolean allPos  = nums.stream().allMatch(n -> n > 0);   // true

// Strings
List<String> names = List.of("alice", "bob", "charlie");
names.stream()
     .map(String::toUpperCase)
     .collect(Collectors.joining(", "));                // "ALICE, BOB, CHARLIE"

// flatMap
List<List<Integer>> nested = List.of(List.of(1, 2), List.of(3, 4));
nested.stream().flatMap(List::stream).toList();         // [1, 2, 3, 4]
```

### Collectors (grouping, partitioning, mapping)

```java
class Employee {
    String name; String dept; double salary;
    // constructor, getters...
}

// Group by department
Map<String, List<Employee>> byDept =
    employees.stream().collect(Collectors.groupingBy(Employee::getDept));

// Count per department
Map<String, Long> countByDept =
    employees.stream().collect(Collectors.groupingBy(Employee::getDept, Collectors.counting()));

// Average salary per department
Map<String, Double> avgSalary =
    employees.stream().collect(Collectors.groupingBy(Employee::getDept,
                                Collectors.averagingDouble(Employee::getSalary)));

// Partition by condition (true/false)
Map<Boolean, List<Employee>> highLow =
    employees.stream().collect(Collectors.partitioningBy(e -> e.getSalary() > 50000));

// To Map
Map<String, Double> nameToSalary =
    employees.stream().collect(Collectors.toMap(Employee::getName, Employee::getSalary));

// Highest salary
Optional<Employee> top = employees.stream()
        .max(Comparator.comparingDouble(Employee::getSalary));
```

### Key characteristics

- **Lazy**: intermediate operations run only when a terminal operation is called.
- **Single-use**: a stream cannot be reused after a terminal operation (`IllegalStateException`).
- **Non-mutating**: the source collection is unchanged.
- **Parallel**: `parallelStream()` can use multiple cores (use carefully; best for large, CPU-bound, stateless operations).

---

## 4.4 Optional

`Optional<T>` is a **container** that may or may not hold a non-null value. It helps avoid `NullPointerException` and makes "no value" explicit in the API.

### Creating

```java
Optional<String> a = Optional.of("Java");          // value must be non-null
Optional<String> b = Optional.ofNullable(null);    // empty if null
Optional<String> c = Optional.empty();
```

### Checking and retrieving

```java
Optional<String> opt = Optional.ofNullable(getName());

opt.isPresent();          // true if value exists
opt.isEmpty();            // Java 11+
opt.get();                // returns value or throws NoSuchElementException (avoid)

opt.orElse("Default");                        // value or default (always evaluated)
opt.orElseGet(() -> "Computed Default");      // lazy default via Supplier
opt.orElseThrow(() -> new IllegalStateException("No value"));
opt.orElseThrow();                            // Java 10+
```

### Functional style

```java
opt.ifPresent(v -> System.out.println("Value: " + v));
opt.ifPresentOrElse(v -> System.out.println(v), () -> System.out.println("none"));  // Java 9

Optional<Integer> length = opt.map(String::length);
Optional<String> filtered = opt.filter(s -> s.startsWith("J"));
Optional<String> chained  = opt.flatMap(s -> Optional.of(s.toUpperCase()));
Optional<String> fallback = opt.or(() -> Optional.of("Other"));   // Java 9
```

### Practical example

```java
// Without Optional (nested null checks)
String city = null;
if (user != null && user.getAddress() != null) {
    city = user.getAddress().getCity();
}

// With Optional
String city2 = Optional.ofNullable(user)
        .map(User::getAddress)
        .map(Address::getCity)
        .orElse("Unknown");
```

### Best practices

- Use `Optional` mainly as a **method return type**.
- Do **not** use it for fields, method parameters, or in collections.
- Never return `null` from a method that returns `Optional`.
- Avoid `get()` without checking; prefer `orElse`, `orElseGet`, `orElseThrow`, `map`.
- Primitive versions: `OptionalInt`, `OptionalDouble`, `OptionalLong`.

---

## 4.5 Method References

A **shorthand for a lambda** that only calls an existing method. Syntax: `Class::method` (no parentheses).

### Four types

| Type | Syntax | Lambda equivalent |
|------|--------|-------------------|
| **Static method** | `ClassName::staticMethod` | `x -> ClassName.staticMethod(x)` |
| **Instance method of a particular object** | `object::method` | `x -> object.method(x)` |
| **Instance method of an arbitrary object of a type** | `ClassName::instanceMethod` | `x -> x.instanceMethod()` |
| **Constructor** | `ClassName::new` | `() -> new ClassName()` |

### Examples

```java
// 1. Static method reference
Function<String, Integer> parse1 = s -> Integer.parseInt(s);
Function<String, Integer> parse2 = Integer::parseInt;

// 2. Instance method of a particular object
Consumer<String> p1 = s -> System.out.println(s);
Consumer<String> p2 = System.out::println;

// 3. Instance method of an arbitrary object of a given type
Function<String, String> up1 = s -> s.toUpperCase();
Function<String, String> up2 = String::toUpperCase;

BiFunction<String, String, Boolean> eq = String::equalsIgnoreCase;
// (a, b) -> a.equalsIgnoreCase(b)

// 4. Constructor reference
Supplier<List<String>> s1 = () -> new ArrayList<>();
Supplier<List<String>> s2 = ArrayList::new;

Function<String, Person> create = Person::new;       // new Person(name)

// Array constructor reference
IntFunction<int[]> arrMaker = int[]::new;
```

### In streams

```java
List<String> names = List.of("alice", "bob", "carol");

names.stream()
     .map(String::toUpperCase)             // arbitrary object
     .forEach(System.out::println);        // particular object

List<Person> people = names.stream()
     .map(Person::new)                     // constructor ref
     .collect(Collectors.toList());

people.sort(Comparator.comparing(Person::getName));    // sorting via reference
```

> Use a method reference when it makes the code **more readable** than the equivalent lambda.

---

# Quick Revision Cheat Sheet

| Topic | Remember |
|-------|----------|
| JDK/JRE/JVM | JDK = JRE + tools; JRE = JVM + libs; JVM runs bytecode |
| Primitives | byte, short, int, long, float, double, char, boolean |
| `==` vs `equals()` | `==` compares references; `equals()` compares content |
| Casting | Widening is automatic; narrowing needs `(type)` |
| Constructor | Same name as class, no return type, not inherited |
| Inheritance | `extends`; single class inheritance only; multiple via interfaces |
| Overload vs Override | Same class, different params / Parent-child, same signature |
| Encapsulation | `private` fields + public getters/setters |
| Abstraction | `abstract` class or `interface` |
| `static` | Belongs to class | `final` | Cannot change/override/extend |
| String | Immutable; use `StringBuilder` for frequent changes |
| ArrayList vs LinkedList | Array (fast get) vs doubly linked list (fast insert/delete) |
| HashSet / HashMap | Hash-based, unordered; need `hashCode()` + `equals()` |
| Checked vs Unchecked | Compile-time enforced vs runtime (`RuntimeException`) |
| `throw` vs `throws` | Throw an exception / declare it |
| Generics | Type safety at compile time; type erasure at runtime |
| Lambda | `(params) -> body`; needs a functional interface |
| Stream | source -> intermediate (lazy) -> terminal |
| Optional | Container to avoid nulls; prefer `orElse`/`map` over `get` |
| Method reference | `Class::method` shorthand for lambda |

---

*End of notes. Happy coding!*
