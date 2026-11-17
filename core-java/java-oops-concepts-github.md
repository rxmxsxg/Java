# Object-Oriented Programming (OOP) Concepts in Java

A detailed guide to the core object-oriented programming concepts in
Java, with examples, practical scenarios, and interview questions.

## Table of contents

1.  [Introduction to OOP](#1-introduction-to-oop)
2.  [Classes and objects](#2-classes-and-objects)
3.  [Encapsulation](#3-encapsulation)
4.  [Inheritance](#4-inheritance)
5.  [Polymorphism](#5-polymorphism)
6.  [Abstraction](#6-abstraction)
7.  [Relationships between objects](#7-relationships-between-objects)
8.  [IS-A and HAS-A relationships](#8-is-a-and-has-a-relationships)
9.  [A practical example combining the four
    pillars](#9-a-practical-example-combining-the-four-pillars)
10. [Common interview questions](#10-common-interview-questions)
11. [Practice exercises](#11-practice-exercises)
12. [Summary](#12-summary)

------------------------------------------------------------------------

## 1. Introduction to OOP

OOP stands for **Object-Oriented Programming**. It is a programming
paradigm in which software is designed around objects that contain data
and behaviour.

Java is primarily an object-oriented language, although it also supports
primitive types and functional programming features.

### Benefits of OOP

-   **Reusability:** Reuse existing code through inheritance and
    composition.
-   **Maintainability:** Keep related data and behaviour organized.
-   **Extensibility:** Add new implementations with fewer changes to
    existing code.
-   **Encapsulation:** Protect an object's internal state.
-   **Flexibility:** Use common interfaces with different
    implementations.

### Four pillars of OOP

1.  Encapsulation
2.  Inheritance
3.  Polymorphism
4.  Abstraction

## 2. Classes and objects

### What is a class?

A class is a blueprint that describes the data (fields) and behaviour
(methods) its objects can have.

``` java
public class Employee {
    int employeeId;
    String employeeName;
    double salary;

    public void displayDetails() {
        System.out.println("ID: " + employeeId);
        System.out.println("Name: " + employeeName);
        System.out.println("Salary: " + salary);
    }
}
```

In this example:

-   `Employee` is the class.
-   `employeeId`, `employeeName`, and `salary` are fields.
-   `displayDetails()` is a method.

### What is an object?

An object is an instance of a class. A class describes what an object
can contain and do; an object is a particular instance created from that
description.

``` java
public class Main {
    public static void main(String[] args) {
        Employee employee = new Employee();

        employee.employeeId = 101;
        employee.employeeName = "Ramesh";
        employee.salary = 50000.00;

        employee.displayDetails();
    }
}
```

Output:

``` text
ID: 101
Name: Ramesh
Salary: 50000.0
```

You can create multiple objects from the same class:

``` java
Employee firstEmployee = new Employee();
Employee secondEmployee = new Employee();
```

A useful analogy is that a class is a house blueprint and an object is a
house built using that blueprint.

## 3. Encapsulation

**Encapsulation** means bundling data and the methods that operate on
that data inside a class, while controlling access to the object's
internal state.

It is commonly implemented by:

-   Declaring fields `private`.
-   Providing public methods to read or change the state.
-   Validating input before changing the state.

### Real-world example: Bank account

A bank customer should not be able to assign an arbitrary value directly
to the account balance. The account should control how its balance
changes.

``` java
public class BankAccount {
    private double balance;

    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Deposit must be positive");
        }

        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        account.deposit(10000);

        System.out.println(account.getBalance()); // 10000.0

        // account.balance = -5000; // Compile-time error: balance is private
    }
}
```

### Why use encapsulation?

1.  Prevents uncontrolled direct modification of fields.
2.  Allows validation when state changes.
3.  Hides internal implementation details.
4.  Makes future changes easier because callers use methods rather than
    depending on internal fields.

**Interview question: Why do we declare variables as private?**

To prevent direct access from outside the class and to control how the
object's state is read or modified.

## 4. Inheritance

**Inheritance** allows a class to derive fields and methods from another
class. It supports code reuse and models an IS-A relationship.

Java uses the `extends` keyword for class inheritance.

-   Parent class: superclass or base class.
-   Child class: subclass or derived class.

### Example: Employee and Developer

Parent class:

``` java
public class Employee {
    protected int employeeId;
    protected String employeeName;

    public void login() {
        System.out.println("Employee logged in");
    }
}
```

Child class:

``` java
public class Developer extends Employee {
    public void writeCode() {
        System.out.println(employeeName + " is writing code");
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        Developer developer = new Developer();

        developer.employeeId = 101;
        developer.employeeName = "Ramesh";

        developer.login();
        developer.writeCode();
    }
}
```

Output:

``` text
Employee logged in
Ramesh is writing code
```

The `Developer` class inherits accessible members from `Employee`. The
`protected` fields in this example are accessible to the subclass.

### Types of inheritance

Common class-inheritance structures include:

1.  **Single inheritance:** One child class extends one parent class.
2.  **Multilevel inheritance:** A class extends a class that itself
    extends another class.
3.  **Hierarchical inheritance:** Multiple child classes extend the same
    parent class.

Java does not support multiple inheritance of classes. A class cannot
extend two classes:

``` java
class A {}
class B {}

// Invalid Java:
// class C extends A, B {}
```

Java does support implementing multiple interfaces:

``` java
interface Printable {
    void print();
}

interface Scannable {
    void scan();
}

class MultiFunctionPrinter implements Printable, Scannable {
    @Override
    public void print() {
        System.out.println("Printing");
    }

    @Override
    public void scan() {
        System.out.println("Scanning");
    }
}
```

## 5. Polymorphism

**Polymorphism** means "many forms". It allows a common method name or
reference type to work with different behaviours.

The two commonly discussed forms are:

1.  Compile-time polymorphism (method overloading).
2.  Runtime polymorphism (method overriding).

### 5.1 Method overloading

Method overloading means defining methods with the same name but
different parameter lists.

The parameter lists must differ by number, types, or order of
parameters. Changing only the return type is not enough.

``` java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        System.out.println(calculator.add(10, 20));       // 30
        System.out.println(calculator.add(10, 20, 30));   // 60
        System.out.println(calculator.add(10.5, 20.5));   // 31.0
    }
}
```

The compiler selects the applicable overload based on the arguments and
Java's method-resolution rules.

### 5.2 Method overriding

Method overriding occurs when a subclass provides an implementation of
an inherited instance method with a compatible signature and return
type.

Parent class:

``` java
public class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}
```

Child class:

``` java
public class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.sound();
    }
}
```

Output:

``` text
Dog barks
```

Consider this statement:

``` java
Animal animal = new Dog();
```

-   `Animal` is the reference's declared type.
-   `Dog` is the actual runtime object type.
-   The overridden `Dog.sound()` implementation is selected at runtime.

This is called **dynamic method dispatch** or runtime polymorphism.

### Overloading vs overriding

  -----------------------------------------------------------------------
  Method overloading                  Method overriding
  ----------------------------------- -----------------------------------
  Same method name with different     Subclass provides a compatible
  parameter lists                     implementation of an inherited
                                      instance method

  Can occur in one class              Requires inheritance or interface
                                      implementation

  Resolved at compile time            Instance-method implementation is
                                      selected at runtime

  Return type alone cannot            Return type must be the same or
  distinguish overloads               covariant

  Commonly called compile-time        Commonly called runtime
  polymorphism                        polymorphism
  -----------------------------------------------------------------------

**Important:** Static methods are hidden, not overridden. Private
methods are not overridden. Constructors cannot be overridden.

## 6. Abstraction

**Abstraction** means exposing essential operations while hiding
implementation details that callers do not need to know.

For example, an ATM user selects a withdrawal operation without needing
to understand the internal bank transaction processing.

Java supports abstraction through abstract classes and interfaces.

### 6.1 Abstract classes

An abstract class is declared with the `abstract` keyword. It cannot be
instantiated directly.

An abstract class can contain:

-   Abstract methods (without a method body).
-   Concrete methods (with a method body).
-   Instance fields.
-   Constructors.
-   Static methods and other class members.

Example:

``` java
abstract class Vehicle {
    abstract void start();

    public void stop() {
        System.out.println("Vehicle stopped");
    }
}
```

Subclass:

``` java
class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car starts with a key");
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        Vehicle vehicle = new Car();

        vehicle.start();
        vehicle.stop();
    }
}
```

Output:

``` text
Car starts with a key
Vehicle stopped
```

You cannot instantiate the abstract class directly:

``` java
// Vehicle vehicle = new Vehicle(); // Compile-time error
```

### 6.2 Interfaces

An interface defines a contract that implementing classes agree to
follow.

``` java
interface Payment {
    void pay(double amount);
}
```

First implementation:

``` java
class CreditCardPayment implements Payment {
    @Override
    public void pay(double amount) {
        System.out.println("Paid using credit card: " + amount);
    }
}
```

Second implementation:

``` java
class UpiPayment implements Payment {
    @Override
    public void pay(double amount) {
        System.out.println("Paid using UPI: " + amount);
    }
}
```

Usage:

``` java
public class Main {
    public static void main(String[] args) {
        Payment payment = new CreditCardPayment();
        payment.pay(1000);

        payment = new UpiPayment();
        payment.pay(2000);
    }
}
```

Output:

``` text
Paid using credit card: 1000.0
Paid using UPI: 2000.0
```

The caller works with the `Payment` contract, while the concrete
implementation determines how payment is performed.

### Abstract class vs interface

  -----------------------------------------------------------------------
  Abstract class                      Interface
  ----------------------------------- -----------------------------------
  Declared using `abstract class`     Declared using `interface`

  A class extends it                  A class implements it

  Can have instance fields            Fields are implicitly
                                      `public static final`

  Can have constructors               Cannot have constructors

  Can have abstract and concrete      Can have abstract, default, static,
  methods                             and private methods

  A class can extend only one class   A class can implement multiple
                                      interfaces
  -----------------------------------------------------------------------

Use an abstract class when related classes need shared state or common
implementation. Use an interface to define a capability or contract that
potentially unrelated classes can implement.

## 7. Relationships between objects

### 7.1 Association

Association represents a relationship between two independent classes.

Example: An employee works with a department. Both employee and
department can exist independently.

``` java
class Department {
    String departmentName;
}

class Employee {
    String employeeName;
    Department department;
}
```

### 7.2 Aggregation

Aggregation is a weak HAS-A relationship. The contained object can exist
independently of the container.

Example: A department has employees, but an employee can continue to
exist even if the department object is removed.

``` java
import java.util.List;

class Employee {
    private final String name;

    Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

class Department {
    private final List<Employee> employees;

    Department(List<Employee> employees) {
        this.employees = employees;
    }
}
```

The employees are created and managed independently, then supplied to
the department.

### 7.3 Composition

Composition is a strong ownership relationship in which a containing
object controls the lifecycle of its parts in the domain model.

Example: A house creates and owns its rooms in this simplified model.

``` java
import java.util.ArrayList;
import java.util.List;

class Room {
    private final String name;

    Room(String name) {
        this.name = name;
    }
}

class House {
    private final List<Room> rooms = new ArrayList<>();

    House() {
        rooms.add(new Room("Living room"));
        rooms.add(new Room("Bedroom"));
    }
}
```

Composition and aggregation are modeling concepts. Java does not enforce
a special language-level keyword for either relationship.

## 8. IS-A and HAS-A relationships

  -----------------------------------------------------------------------
  IS-A                                HAS-A
  ----------------------------------- -----------------------------------
  Represents inheritance or           Represents a relationship through
  implementation                      object references

  Uses `extends` or `implements`      Uses fields that refer to other
                                      objects

  Developer IS-A Employee             Employee HAS-A Address
  -----------------------------------------------------------------------

Example:

``` java
class Address {
    String city;
}

class Employee {
    private Address address;
}
```

Here, an Employee HAS-A Address.

### Inheritance vs composition

Inheritance reuses or specializes a parent type. Composition builds a
class by combining other objects.

Prefer composition when a class needs to use another object's
functionality without necessarily being a subtype of that object.

## 9. A practical example combining the four pillars

This example combines encapsulation, inheritance, polymorphism, and
abstraction in a small payment application.

``` java
abstract class Payment {
    private double amount;

    public void setAmount(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Amount must be positive");
        }
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }

    public abstract void makePayment();
}

class UpiPayment extends Payment {
    @Override
    public void makePayment() {
        System.out.println("UPI payment: " + getAmount());
    }
}

class CardPayment extends Payment {
    @Override
    public void makePayment() {
        System.out.println("Card payment: " + getAmount());
    }
}

public class Main {
    public static void main(String[] args) {
        Payment payment = new UpiPayment();
        payment.setAmount(1000);
        payment.makePayment();

        payment = new CardPayment();
        payment.setAmount(2000);
        payment.makePayment();
    }
}
```

Output:

``` text
UPI payment: 1000.0
Card payment: 2000.0
```

Where are the four pillars?

  -----------------------------------------------------------------------
  OOP concept                         Implementation
  ----------------------------------- -----------------------------------
  Encapsulation                       `amount` is private and accessed
                                      through validated methods

  Inheritance                         `UpiPayment` and `CardPayment`
                                      extend `Payment`

  Polymorphism                        The same `makePayment()` call
                                      invokes different implementations

  Abstraction                         `Payment` declares the abstract
                                      `makePayment()` operation
  -----------------------------------------------------------------------

## 10. Common interview questions

These questions are useful preparation for Java developer interviews,
including mid-level roles.

1.  What are the four pillars of OOP?
2.  What is the difference between abstraction and encapsulation?
3.  What is the difference between method overloading and overriding?
4.  Why does Java not support multiple inheritance through classes?
5.  Can static methods be overridden?
6.  Can the `main` method be overloaded?
7.  Can a constructor be overridden?
8.  What is runtime polymorphism?
9.  What is the difference between an abstract class and an interface?
10. What is the difference between IS-A and HAS-A?
11. What is the difference between aggregation and composition?
12. Can an abstract class have a constructor?
13. Can an interface have default and static methods?
14. What is dynamic method dispatch?
15. What is the difference between inheritance and composition?
16. Can we override a private method?
17. What is a covariant return type?
18. What is the purpose of the `super` keyword?
19. What is the difference between `this` and `super`?
20. Why should we prefer programming to interfaces?

## 11. Practice exercises

Try to solve these exercises before looking at the suggested approach.

### Exercise 1: Encapsulation

Create an `Employee` class with:

-   Private fields: `id`, `name`, and `salary`.
-   Getters and setters.
-   A validation rule that salary cannot be negative.

### Exercise 2: Inheritance

Create a parent class `Vehicle` with a `start()` method.

Create two child classes:

-   `Car`
-   `Bike`

Override `start()` in each child class.

### Exercise 3: Method overloading

Create a `Calculator` class with overloaded `multiply()` methods:

-   Multiply two integers.
-   Multiply three integers.
-   Multiply two double values.

### Exercise 4: Runtime polymorphism

Create an interface `Notification` with a `send()` method.

Implement it in:

-   `EmailNotification`
-   `SmsNotification`
-   `PushNotification`

Use an interface reference to call each implementation.

### Exercise 5: Abstraction

Create an abstract class `Shape` with an abstract `calculateArea()`
method.

Implement it in:

-   `Circle`
-   `Rectangle`

Calculate and print the area of each shape.

### Exercise 6: Composition

Create an `Order` class that contains an `OrderItem` object. Give the
order responsibility for creating and managing its items.

## 12. Summary

  -----------------------------------------------------------------------
  Concept                 Meaning                 Main Java feature
  ----------------------- ----------------------- -----------------------
  Class                   Blueprint for objects   `class`

  Object                  Instance of a class     Object creation

  Encapsulation           Control access to       `private`, getters,
                          internal state          setters

  Inheritance             Derive a class from     `extends`
                          another class           

  Polymorphism            Same contract or method Overloading and
                          call, different         overriding
                          behaviour               

  Abstraction             Expose essential        `abstract`, `interface`
                          operations, hide        
                          implementation details  

  Association             Relationship between    Object references
                          independent objects     

  Aggregation             Weak HAS-A relationship Object references

  Composition             Strong ownership        Object references and
                          relationship            lifecycle design
  -----------------------------------------------------------------------

### Recommended learning sequence

1.  Understand classes, objects, constructors, and access modifiers.
2.  Practise encapsulation.
3.  Learn inheritance, `this`, and `super`.
4.  Understand overloading and overriding.
5.  Practise abstract classes and interfaces.
6.  Learn association, aggregation, and composition.
7.  Build a small application combining all four pillars.

**Key takeaway:** OOP is not just about knowing definitions. Practise
designing classes and choosing the right relationships between them.
That is what helps you apply OOP effectively in real Java and Spring
Boot applications.
