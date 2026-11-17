# **OOPS Concepts in Java – Detailed Explanation**

OOPS stands for **Object-Oriented Programming System**. It is a programming approach in which we organize code using **classes and objects**.

Java is primarily an object-oriented programming language. OOPS helps us write code that is:

- Reusable
- Maintainable
- Secure
- Flexible
- Easy to extend

There are **four major pillars of OOPS** in Java:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

Let's understand each concept with real-time examples and Java 17 code.

# **1. Class and Object**

Before learning the four pillars, you should understand classes and objects.

## **What is a class?**

A class is a blueprint or template used to create objects.

For example, consider an Employee class. It defines employee properties and behaviours.

```
public class Employee {

    int employeeId;
    String employeeName;
    double salary;

    public void displayDetails() {
        System.out.println(employeeId);
        System.out.println(employeeName);
        System.out.println(salary);
    }
}
```

Here:

- `employeeId`, `employeeName`, `salary` are variables.
- `displayDetails()` is a method.
- `Employee` is a class.

## **What is an object?**

An object is an instance of a class.

```
public class Main {

    public static void main(String[] args) {

        Employee emp = new Employee();

        emp.employeeId = 101;
        emp.employeeName = "Ramesh";
        emp.salary = 50000;

        emp.displayDetails();
    }
}
```

Output:

```
101
Ramesh
50000.0
```

[Telusko Docs](https://images.openai.com/static-rsc-4/ArSNVGr1B1El3pv13gkMwGU4B6VYFzVsq2BqhizA0VyqONz5UHDbY7k8O8DJUTf80M7NI_2ffs6yLo5jXtQZMmd6ijNIYht7Se8-e1JQat6Y2SRK2FCYja_nKqpStn99hFTWNnCtdxugXxk04p3x5Er8MWDAySPQgcKAIkJH45Y?purpose=inline)

[docs.telusko.com](https://docs.telusko.com/docs/java/classes-and-objects/class-and-object?utm_source=chatgpt.com)

Think of it this way:

- Class = Blueprint of a house.
- Object = Actual house constructed using that blueprint.

You can create multiple objects from one class.

# **2. Encapsulation**

Pillar 1

## **What is encapsulation?**

Encapsulation means **wrapping data (variables) and methods into a single unit (class) and restricting direct access to the data.**

We generally achieve encapsulation using:

- Private variables
- Public getter and setter methods

### **Real-time example**

Consider a bank account.

You cannot directly change your bank balance. You must use authorized operations such as deposit and withdrawal.

[AlgoDaily - Software interview prep made easy. Coding Interview Questions.](https://images.openai.com/static-rsc-4/H06Y1CQ33OrMq8e_Cr_sVWaggDbLRhONCbOglhctWUiCMCxMF8BMEqLYcdmcFZNrkpkGNrmfrMwFpw-f3uC3VUQVogCj8bCOTSgX0n2CwPAcnTmwn_-dzZ4XtOTa4GX6avlI_bSw4qERmIXJUiVuf0UZBD2OW0UPS7zDihcfvlE?purpose=inline)

[algodaily.com](https://algodaily.com/lessons/understanding-encapsulation-in-programming?utm_source=chatgpt.com)

### **Java example**

```
public class BankAccount {

    private double balance;

    public void deposit(double amount) {

        if (amount > 0) {
            balance = balance + amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Main class:

```
public class Main {

    public static void main(String[] args) {

        BankAccount account = new BankAccount();

        account.deposit(10000);

        System.out.println(account.getBalance());
    }
}
```

Output:

```
10000.0
```

### **Why use encapsulation?**

1. Protects data from unauthorized access.
2. Provides controlled access through methods.
3. Makes code easier to maintain.
4. Allows validation before changing data.

**Interview question:** Why do we declare variables as private in Java?

Answer: To prevent direct access from outside the class and provide controlled access through public methods.

# **3. Inheritance**

Pillar 2

## **What is inheritance?**

Inheritance means one class can acquire the properties and methods of another class.

It helps us achieve **code reusability**.

Java uses the `extends` keyword for class inheritance.

### **Real-time example**

Consider an organization:

- Parent class: Employee
- Child class: Developer
- Child class: Manager

Both Developer and Manager share common employee properties.

[Asosiasi - Hubungan Antar Kelas - Kata Pengantar - IS521 Praktikum Pemrograman Berorientasi Obj](https://images.openai.com/static-rsc-4/UWUdabbvyNmw1A1aYWMhhYPYa2TlMKJg26mGljlYRN9EFol_dboNp2FqBJmdAxZPkjsUZjsIKSW83kiaQQwL8dLVQ-BC4S8FhBjt-lTdja-be8Q2ylkGmAxEefQM1b11uX5w13hLkDNUYK-vzWzpd7V0eiiuGawq0InqtenHU_w?purpose=inline)

[123dok.com](https://123dok.com/article/asosiasi-hubungan-kelas-kata-pengantar-praktikum-pemrograman-berorientasi.z3ex2e8q?utm_source=chatgpt.com)

### **Java example**

Parent class:

```
public class Employee {

    int employeeId;
    String employeeName;

    public void login() {
        System.out.println("Employee logged in");
    }
}
```

Child class:

```
public class Developer extends Employee {

    public void writeCode() {
        System.out.println("Developer is writing code");
    }
}
```

Main class:

```
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

```
Employee logged in
Developer is writing code
```

Notice that the Developer class can access the inherited `login()` method without implementing it again.

### **Types of inheritance**

Java supports these class inheritance structures:

[Inheritance in Java | Java Tutorial | PrepInsta](https://images.openai.com/static-rsc-4/pO8ozk0At_2xbp-uSRUbc0RhoKuj0aNF7Y9qQrqKo5OtGmAd5voEbfhL8KWMu84hdx91U1wnVBCUnqdh8pus57_7ZvNe0CMm2Sn3iDJ2b599LCN30kibBIlRg4jLaJR9vBvLN1KCF4le6_SIOHQxrUNZlp3ZnPaaTzTcI0nG_jE?purpose=inline)

[prepinsta.com](https://prepinsta.com/java/inheritance/?utm_source=chatgpt.com)

| Type         | Explanation                                                       |
| ------------ | ----------------------------------------------------------------- |
| Single       | One child inherits one parent                                     |
| Multilevel   | A class inherits from a class that already inherits another class |
| Hierarchical | Multiple child classes inherit one parent                         |
| Multiple     | One class inherits multiple parents                               |
| Hybrid       | Combination of inheritance types                                  |

**Important Java interview point:**

Java does not support multiple inheritance through classes.

For example:

```
class A {
}

class B {
}

// Not allowed in Java
class C extends A, B {
}
```

However, Java supports multiple inheritance of type through interfaces.

# **4. Polymorphism**

Pillar 3

## **What is polymorphism?**

Polymorphism means **one thing having multiple forms**.

In Java, polymorphism allows the same method name or reference to behave differently depending on the situation.

There are two major types:

1. Compile-time polymorphism (Method Overloading)
2. Runtime polymorphism (Method Overriding)

## **4.1 Method Overloading**

Method overloading means having multiple methods with the same name but different parameter lists within a class.

Example:

```
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

Main class:

```
public class Main {

    public static void main(String[] args) {

        Calculator calculator = new Calculator();

        System.out.println(calculator.add(10, 20));

        System.out.println(calculator.add(10, 20, 30));

        System.out.println(calculator.add(10.5, 20.5));
    }
}
```

Output:

```
30
60
31.0
```

The method name is the same, but the parameters are different.

The compiler determines which method to execute.

**Important:** Changing only the return type does not constitute method overloading.

## **4.2 Method Overriding**

Method overriding means a child class provides its own implementation of a method already defined in its parent class.

Example:

Parent class:

```
public class Animal {

    public void sound() {
        System.out.println("Animal makes sound");
    }
}
```

Child class:

```
public class Dog extends Animal {

    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

Main class:

```
public class Main {

    public static void main(String[] args) {

        Animal animal = new Dog();

        animal.sound();
    }
}
```

Output:

```
Dog barks
```

### **Understand this important statement**

```
Animal animal = new Dog();
```

What is happening here?

- `Animal` is the reference type.
- `Dog` is the actual object type.
- The overridden method of `Dog` executes at runtime.

This is called **runtime polymorphism** or dynamic method dispatch.

[Mastering Java Polymorphism: The Ultimate Guide with Code, Benchmarks, and Diagrams | by inside Nikita's Mind | Medium](https://images.openai.com/static-rsc-4/vTiNJj8yCBZY66BYLUuPrUAUguCK4Y7y8-suM9P1TCrhGhWseMym6mcXxL1isEHuVNCVjvq67qr7JsOLWpH5dNY8-JpCPadNu7S2Ho5f6fTYxv0aMBp8xMCUb4U2-ViVFR6dBnyzVhO_uODQRfp3EqkjjYRIP4J-P4-EJd4i_Qg?purpose=inline)

[medium.com](https://medium.com/%40ntiinsd/mastering-java-polymorphism-the-ultimate-guide-with-code-benchmarks-and-diagrams-5300c1516349?utm_source=chatgpt.com)

### **Overloading vs Overriding**

| Method Overloading            | Method Overriding                                   |
| ----------------------------- | --------------------------------------------------- |
| Same method name              | Same method signature (with compatible return type) |
| Different parameter lists     | Same parameters                                     |
| Usually within the same class | Requires inheritance or interface implementation    |
| Compile-time polymorphism     | Runtime polymorphism                                |
| Inheritance not required      | Inheritance or interface implementation required    |

# **5. Abstraction**

Pillar 4

## **What is abstraction?**

Abstraction means **hiding implementation details and showing only essential functionality to the user.**

For example, when you use an ATM:

- You enter your PIN.
- You select withdrawal.
- You receive money.

You don't need to know the internal banking implementation.

[Understanding Abstraction in Java: Key Concept for OOP and Software Design | by Eshin Menusha Fernando | Medium](https://images.openai.com/static-rsc-4/kAc-XndJTzRsK0FCcZVJB40VnpgCNRlxXMbH92MvRrXQ4sVit8pCdIlF_chKMrH9NQ0zEN-Bb1lDYRsXjcFAPzUW2sXGXu_LylXlmymJiOg9ZkFwxfxIgOCdxWyXOnRYs0AiQdYakof6CjwcXlU2_ZZXz7JTCMD0zIecQKt74Yo?purpose=inline)

[medium.com](https://medium.com/%40emenusha14/understanding-abstraction-in-java-key-concept-for-oop-and-software-design-9ed14f041650?utm_source=chatgpt.com)

Java supports abstraction mainly through:

1. Abstract classes
2. Interfaces

## **5.1 Abstract class**

An abstract class is a class declared with the `abstract` keyword.

It can contain:

- Abstract methods (without implementation).
- Normal methods (with implementation).
- Variables.
- Constructors.

Example:

```
abstract class Vehicle {

    abstract void start();

    public void stop() {
        System.out.println("Vehicle stopped");
    }
}
```

Child class:

```
class Car extends Vehicle {

    @Override
    void start() {
        System.out.println("Car starts with a key");
    }
}
```

Main class:

```
public class Main {

    public static void main(String[] args) {

        Vehicle vehicle = new Car();

        vehicle.start();
        vehicle.stop();
    }
}
```

Output:

```
Car starts with a key
Vehicle stopped
```

You cannot directly create an object of an abstract class.

```
// Vehicle vehicle = new Vehicle(); // Not allowed
```

## **5.2 Interface**

An interface defines a contract that implementing classes agree to follow.

Example:

```
interface Payment {

    void pay(double amount);
}
```

Implementation:

```
class CreditCardPayment implements Payment {

    @Override
    public void pay(double amount) {
        System.out.println("Paid using Credit Card: " + amount);
    }
}
```

Another implementation:

```
class UpiPayment implements Payment {

    @Override
    public void pay(double amount) {
        System.out.println("Paid using UPI: " + amount);
    }
}
```

Main class:

```
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

```
Paid using Credit Card: 1000.0
Paid using UPI: 2000.0
```

The caller uses the same `Payment` interface, but different implementations perform the payment differently.

### **Abstract class vs Interface**

| Abstract class                         | Interface                                              |
| -------------------------------------- | ------------------------------------------------------ |
| Uses `abstract class`                  | Uses `interface`                                       |
| Class extends it                       | Class implements it                                    |
| Can have instance variables            | Fields are implicitly `public static final`            |
| Can have constructors                  | Cannot have constructors                               |
| Can have abstract and concrete methods | Can have abstract, default, static and private methods |
| A class can extend only one class      | A class can implement multiple interfaces              |

# **6. Other important OOPS concepts**

Apart from the four pillars, understand these concepts too.

## **6.1 Association**

Association represents a relationship between two independent classes.

Example: Employee and Department.

An employee belongs to a department, but both can exist independently.

## **6.2 Aggregation**

Aggregation is a weak HAS-A relationship.

Example: Department and Employees.

A department contains employees, but employees can exist even if the department is removed.

## **6.3 Composition**

Composition is a strong HAS-A relationship.

Example: House and Rooms.

A room is considered part of a particular house in the modeled relationship.

[Association, Composition and Aggregation | Board Infinity](https://images.openai.com/static-rsc-4/g4noNQK45azxF0rJNZT-MKKJVlVY8LWLSNgdjvHuOAXaFm5GRCs3vtDYsjgd5kXUU3CPtyNpThc3M7Bl6Y7SdHXnm-JaOgtZPSQFXt5f-eKLwJ4Jt5KxhjAb6bBExmVKKombM1gRFK8RpsiY_ZeQi3Tdla_ao2C7kg6YgXYXHTk?purpose=inline)

[boardinfinity.com](https://www.boardinfinity.com/blog/a-guide-to-association-aggregation-and-composition-in-java/?utm_source=chatgpt.com)

## **6.4 IS-A vs HAS-A**

| IS-A                           | HAS-A                                        |
| ------------------------------ | -------------------------------------------- |
| Represents inheritance         | Represents object composition or association |
| Uses `extends` or `implements` | Uses object references as fields             |
| Developer IS-A Employee        | Employee HAS-A Address                       |

Example:

```
class Employee {
    Address address;
}
```

Here, Employee HAS-A Address.

# **7. Real-time example combining all four pillars**

Let's build a simple payment application using all four OOPS concepts.

Practical example

```
abstract class Payment {

    private double amount;

    public void setAmount(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Invalid amount");
        }
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }

    abstract void makePayment();
}

class UpiPayment extends Payment {

    @Override
    void makePayment() {
        System.out.println("UPI payment: " + getAmount());
    }
}

class CardPayment extends Payment {

    @Override
    void makePayment() {
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

### **Where are the OOPS concepts?**

| Concept       | Implementation                                  |
| ------------- | ----------------------------------------------- |
| Encapsulation | Private `amount` with getter and setter         |
| Inheritance   | UpiPayment and CardPayment extend Payment       |
| Polymorphism  | Same `makePayment()` method behaves differently |
| Abstraction   | Payment is an abstract class                    |

This is similar to how real-world Spring Boot applications use interfaces, service implementations, inheritance, and encapsulated entities.

# **8. Important OOPS interview questions**

Here are questions you should prepare for Java interviews, especially for 4–6 years of experience.

| No. | Interview question                                                 |
| --- | ------------------------------------------------------------------ |
| 1   | What are the four pillars of OOPS?                                 |
| 2   | What is the difference between abstraction and encapsulation?      |
| 3   | What is the difference between method overloading and overriding?  |
| 4   | Why doesn't Java support multiple inheritance using classes?       |
| 5   | Can we override static methods?                                    |
| 6   | Can we overload the main method?                                   |
| 7   | Can a constructor be overridden?                                   |
| 8   | What is runtime polymorphism?                                      |
| 9   | What is the difference between an abstract class and an interface? |
| 10  | What is the difference between IS-A and HAS-A relationships?       |
| 11  | What is the difference between aggregation and composition?        |
| 12  | Can an abstract class have a constructor?                          |
| 13  | Can an interface have default and static methods?                  |
| 14  | What is dynamic method dispatch?                                   |
| 15  | What is the difference between inheritance and composition?        |

# **9. Test your understanding**

Try these questions. Select your answers and check your understanding.

**Java OOPS Quiz**

0/5 answered

**1. Which OOPS concept provides data hiding?**

Inheritance

Encapsulation

Polymorphism

Abstraction

**2. Which keyword is used for class inheritance?**

implements

extends

inherits

super

**3. Which type of polymorphism is achieved through method overriding?**

Compile-time

Runtime

Static

None

**4. Can Java classes implement multiple interfaces?**

Yes

No

Only two

Only abstract classes

**5. Which keyword is used to declare an abstract class?**

interface

final

abstract

static

Submit answers

## **10. Recommended learning order**

For your Java full-stack interview preparation, I recommend this sequence:

1. Class, Object and Constructors
2. Encapsulation
3. Inheritance
4. Polymorphism
5. Abstraction
6. Interfaces vs Abstract Classes
7. Association, Aggregation and Composition
8. Tricky OOPS interview coding programs

The next useful step is to practise  20 tricky OOPS interview programs with solutions.