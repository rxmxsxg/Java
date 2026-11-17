# Java Data Types --- Detailed Guide

## 1. What is a data type?

A **data type** tells Java what kind of value a variable can store, how
much memory is generally needed for that value, and which operations are
valid for it.

For example:

``` java
int age = 25;
double price = 199.99;
char grade = 'A';
boolean isActive = true;
```

Here, `int`, `double`, `char`, and `boolean` are data types.

Java is a **statically typed** language. You normally declare a
variable's type before using it, and the compiler checks that
assignments and operations are type-compatible.

## 2. Main categories of Java data types

Java data types are commonly divided into two categories:

1.  **Primitive data types** --- store simple values directly.
2.  **Reference data types** --- variables hold references to objects
    (or `null`).

``` text
Java data types
|
+-- Primitive
|   +-- Integer: byte, short, int, long
|   +-- Floating-point: float, double
|   +-- Character: char
|   +-- Boolean: boolean
|
+-- Reference
    +-- Classes (for example, String, Scanner, Employee)
    +-- Arrays
    +-- Interfaces (references to implementing objects)
    +-- Enums
    +-- Records and other class types
```

## 3. Primitive data types

Java has exactly **eight primitive data types**.

  -------------------------------------------------------------------------
  Type                              Size Range / values   Typical use
  ---------------- --------------------- ---------------- -----------------
  `byte`                 8 bits (1 byte) -128 to 127      Small integer
                                                          values,
                                                          byte-oriented
                                                          data

  `short`              16 bits (2 bytes) -32,768 to       Small integer
                                         32,767           values

  `int`                32 bits (4 bytes) -2\^31 to        General-purpose
                                         2\^31 - 1        whole numbers

  `long`               64 bits (8 bytes) -2\^63 to        Large whole
                                         2\^63 - 1        numbers

  `float`              32 bits (4 bytes) Approx. 6--7     Lower-precision
                                         decimal digits   decimal
                                         of precision     calculations

  `double`             64 bits (8 bytes) Approx. 15--16   General-purpose
                                         decimal digits   decimal
                                         of precision     calculations

  `char`               16 bits (2 bytes) `'\u0000'` to    One UTF-16 code
                                         `'\uFFFF'` (0 to unit
                                         65,535)          

  `boolean`          JVM storage size is `true` or        Conditions and
                      not specified as a `false`          flags
                       simple fixed size                  
  -------------------------------------------------------------------------

The sizes above describe the primitive value widths in the Java
language. Actual object and array memory usage also includes
JVM-specific layout and overhead.

### 3.1 `byte`

-   Size: 8 bits.
-   Range: -128 to 127.
-   Useful when working with raw byte data or compact numeric data
    structures.

``` java
public class ByteExample {
    public static void main(String[] args) {
        byte age = 25;
        byte minimum = -128;
        byte maximum = 127;

        System.out.println(age);
        System.out.println(minimum);
        System.out.println(maximum);
    }
}
```

This causes a compile-time error because 128 is outside the `byte`
range:

``` java
byte number = 128; // Compile-time error
```

### 3.2 `short`

-   Size: 16 bits.
-   Range: -32,768 to 32,767.
-   Less commonly used than `int` in everyday application code.

``` java
short temperature = 280;
short year = 2026;

System.out.println(temperature);
System.out.println(year);
```

### 3.3 `int`

-   Size: 32 bits.
-   Range: -2,147,483,648 to 2,147,483,647.
-   The usual default choice for whole-number calculations.

``` java
int employeeId = 101;
int salary = 75000;
int total = 100 + 200;

System.out.println(total); // 300
```

An `int` can overflow if the result exceeds its range. Java integer
arithmetic does not automatically throw an exception for ordinary
overflow:

``` java
int value = Integer.MAX_VALUE;
System.out.println(value + 1); // -2147483648
```

Use a wider type or checked arithmetic when overflow matters.

### 3.4 `long`

-   Size: 64 bits.
-   Range: -2\^63 to 2\^63 - 1.
-   Use it for whole numbers that may exceed the `int` range.

Add `L` (recommended uppercase) to a long literal when needed:

``` java
long population = 8_000_000_000L;
long distanceInMeters = 12345678901L;

System.out.println(population);
```

Without the `L`, an integer literal is normally treated as an `int`, so
a value too large for `int` may fail to compile.

### 3.5 `float`

-   Size: 32 bits.
-   Approximate precision: 6--7 significant decimal digits.
-   A decimal literal is a `double` by default, so add `f` or `F` for a
    `float`.

``` java
float percentage = 85.5f;
float height = 5.8F;

System.out.println(percentage);
```

Floating-point values are approximate. For example:

``` java
float result = 0.1f + 0.2f;
System.out.println(result); // May print 0.3 with a small representation difference
```

### 3.6 `double`

-   Size: 64 bits.
-   Approximate precision: 15--16 significant decimal digits.
-   The default type for decimal floating-point literals.
-   Usually preferred over `float` for general scientific or measurement
    calculations.

``` java
double productPrice = 1999.99;
double average = 10.0 / 3.0;

System.out.println(productPrice);
System.out.println(average);
```

**Important:** Neither `float` nor `double` represents every decimal
fraction exactly. For money and exact decimal arithmetic, consider
`BigDecimal`.

``` java
import java.math.BigDecimal;

BigDecimal price = new BigDecimal("19.99");
BigDecimal tax = new BigDecimal("1.50");
BigDecimal total = price.add(tax);

System.out.println(total); // 21.49
```

Prefer constructing `BigDecimal` from a string (or using
`BigDecimal.valueOf`) rather than `new BigDecimal(0.1)`.

### 3.7 `char`

-   Size: 16 bits.
-   Stores one UTF-16 code unit, represented with single quotes.
-   Can hold a basic character or a Unicode escape.

``` java
char grade = 'A';
char digit = '7';
char symbol = '#';
char letter = '\u0041'; // A

System.out.println(grade);
System.out.println(letter);
```

A Java `char` is not always a complete Unicode character. Some Unicode
characters, such as many emoji, require two `char` values (a surrogate
pair). For full Unicode code points, use `String` and code-point APIs.

### 3.8 `boolean`

-   Values: `true` or `false`.
-   Used for conditions, decisions, and flags.
-   Java does not allow `0` and `1` to be used as booleans.

``` java
boolean isLoggedIn = true;
boolean hasPermission = false;

if (isLoggedIn) {
    System.out.println("User is logged in");
}
```

This is invalid Java:

``` java
boolean status = 1; // Compile-time error
```

## 4. Default values of fields

Instance variables and static variables receive default values if you do
not initialize them explicitly.

  Type             Default value
  ---------------- ---------------
  `byte`           `0`
  `short`          `0`
  `int`            `0`
  `long`           `0L`
  `float`          `0.0f`
  `double`         `0.0d`
  `char`           `'\u0000'`
  `boolean`        `false`
  Reference type   `null`

Example:

``` java
public class Defaults {
    int count;
    double amount;
    boolean active;
    char initial;
    String name;

    public static void main(String[] args) {
        Defaults obj = new Defaults();

        System.out.println(obj.count);   // 0
        System.out.println(obj.amount);  // 0.0
        System.out.println(obj.active);  // false
        System.out.println((int) obj.initial); // 0
        System.out.println(obj.name);    // null
    }
}
```

**Important:** Local variables inside methods do not receive automatic
default values. You must initialize them before reading them.

``` java
public void example() {
    int count;
    // System.out.println(count); // Compile-time error
    count = 10;
    System.out.println(count);
}
```

## 5. Reference data types

A reference variable refers to an object. The object is created
separately, commonly with `new`, or obtained from another expression. A
reference can also be `null`, meaning it refers to no object.

### 5.1 `String`

`String` is a class, not a primitive type. Strings are immutable:
operations that appear to modify a string produce another string.

``` java
String firstName = "Ramesh";
String message = firstName.concat(" Kumar");

System.out.println(firstName); // Ramesh
System.out.println(message);   // Ramesh Kumar
```

### 5.2 Arrays

An array stores a fixed number of values of one component type. Arrays
are objects, so an array variable is a reference.

``` java
int[] numbers = {10, 20, 30, 40};

System.out.println(numbers[0]); // 10
System.out.println(numbers.length); // 4
```

An array can store primitives:

``` java
double[] prices = {10.5, 20.0, 30.75};
```

Or references:

``` java
String[] names = {"Asha", "Ravi", "Maya"};
```

### 5.3 Classes and objects

A class defines a type. An object is an instance of a class.

``` java
class Employee {
    int id;
    String name;
}

public class Main {
    public static void main(String[] args) {
        Employee employee = new Employee();
        employee.id = 101;
        employee.name = "Ramesh";

        System.out.println(employee.id);
        System.out.println(employee.name);
    }
}
```

### 5.4 Interfaces

An interface reference can refer to an object whose class implements
that interface.

``` java
List<String> names = new ArrayList<>();
names.add("Ramesh");
```

Here, `List` is an interface and `ArrayList` is a class that implements
it.

### 5.5 Enums

An enum defines a fixed set of named constants.

``` java
enum Status {
    NEW, IN_PROGRESS, COMPLETED
}

public class Main {
    public static void main(String[] args) {
        Status currentStatus = Status.IN_PROGRESS;
        System.out.println(currentStatus);
    }
}
```

### 5.6 Records

Records are a concise way to declare classes that primarily carry data
(available from Java 16 as a standard feature).

``` java
record User(int id, String name) {}

public class Main {
    public static void main(String[] args) {
        User user = new User(101, "Ramesh");
        System.out.println(user.id());
        System.out.println(user.name());
    }
}
```

## 6. Primitive types vs reference types

  ---------------------------------------------------------------------------
  Feature                 Primitive type          Reference type
  ----------------------- ----------------------- ---------------------------
  Examples                `int`, `double`, `char` `String`, arrays,
                                                  `Employee`

  What a variable holds   A primitive value       A reference to an object,
                                                  or `null`

  Can be `null`?          No                      Yes

  Has methods directly?   No                      Objects expose methods

  Equality with `==`      Compares primitive      Compares whether references
                          values                  identify the same object

  Examples of             `int age = 25;`         `String name = "Ramesh";`
  declarations                                    
  ---------------------------------------------------------------------------

For strings, use `.equals()` when you want to compare text content:

``` java
String a = new String("Java");
String b = new String("Java");

System.out.println(a == b);      // false: different objects
System.out.println(a.equals(b)); // true: same text content
```

## 7. Wrapper classes

Each primitive type has a corresponding wrapper class:

  Primitive   Wrapper class
  ----------- ---------------
  `byte`      `Byte`
  `short`     `Short`
  `int`       `Integer`
  `long`      `Long`
  `float`     `Float`
  `double`    `Double`
  `char`      `Character`
  `boolean`   `Boolean`

Wrapper classes are useful when an object is required, such as in
generic collections. Java collections cannot use primitive type
arguments:

``` java
List<Integer> numbers = new ArrayList<>();
numbers.add(10);
numbers.add(20);
```

### Autoboxing and unboxing

-   **Autoboxing:** Java automatically converts a primitive to its
    wrapper object.
-   **Unboxing:** Java automatically converts a wrapper object to its
    primitive value.

``` java
int number = 100;

Integer objectNumber = number; // Autoboxing
int anotherNumber = objectNumber; // Unboxing

System.out.println(objectNumber);
System.out.println(anotherNumber);
```

Be careful when unboxing `null`:

``` java
Integer value = null;
// int number = value; // Throws NullPointerException at runtime
```

## 8. Type conversion and casting

Type conversion means changing a value from one type to another.

### 8.1 Widening conversion (usually automatic)

A value is converted to a type that can represent a broader range of
values.

A common numeric widening path is:

``` text
byte -> short -> int -> long -> float -> double
                    |
                    +-------------------->
char -----------------> int -> long -> float -> double
```

`char` can widen to numeric types, but it does not widen to `short`.

``` java
int number = 100;
long largeNumber = number;
double decimalNumber = largeNumber;

System.out.println(largeNumber);
System.out.println(decimalNumber);
```

Widening avoids an out-of-range integer narrowing, but conversion to
`float` or `double` can lose precision for some large integer values.

### 8.2 Narrowing conversion (explicit cast required)

A conversion to a type with a smaller range or precision requires an
explicit cast. It may lose information.

``` java
double price = 99.99;
int wholePrice = (int) price;

System.out.println(wholePrice); // 99
```

For integer narrowing, high-order bits can be discarded:

``` java
int number = 130;
byte smallNumber = (byte) number;

System.out.println(smallNumber); // -126
```

### 8.3 String conversions

Convert a number to a string:

``` java
int age = 25;
String text = String.valueOf(age);
// Or:
String text2 = Integer.toString(age);
```

Parse a string into a number:

``` java
String value = "250";
int number = Integer.parseInt(value);

String decimalValue = "19.95";
double amount = Double.parseDouble(decimalValue);
```

Invalid numeric text causes `NumberFormatException`:

``` java
// int number = Integer.parseInt("abc"); // NumberFormatException
```

## 9. Type promotion in arithmetic

In arithmetic expressions, `byte`, `short`, and `char` operands are
generally promoted to `int` (or to a wider type if another operand
requires it).

``` java
byte a = 10;
byte b = 20;

// byte result = a + b; // Compile-time error: expression is int
int result = a + b;

System.out.println(result); // 30
```

To assign the result to a `byte`, cast explicitly, and ensure the result
is within range:

``` java
byte result = (byte) (a + b);
```

## 10. The `var` keyword is not a data type

Local-variable type inference (`var`) was introduced in Java 10. It lets
the compiler infer a local variable's static type from its initializer.

``` java
var name = "Ramesh"; // inferred as String
var age = 25;        // inferred as int
var salary = 50000.50; // inferred as double
```

It does **not** make Java dynamically typed. The inferred type is fixed:

``` java
var count = 10;
// count = "ten"; // Compile-time error
```

`var` is restricted to eligible local variable declarations (and certain
loop/resource contexts); it cannot be used as a field type or as a
method parameter or return type. It needs an initializer.

## 11. Choosing the right data type

  -----------------------------------------------------------------------
  Requirement             Suggested type          Reason
  ----------------------- ----------------------- -----------------------
  Age, count, quantity    `int`                   Normal whole-number
                                                  range

  Very large whole-number `long`                  Larger integer range
  ID or count                                     

  Percentage or           `double`                General-purpose
  scientific measurement                          floating point

  Small raw byte values   `byte`                  Byte-sized data

  Single UTF-16 code unit `char`                  Character/code-unit
                                                  representation

  True/false condition    `boolean`               Logical state

  Money requiring decimal `BigDecimal`            Decimal arithmetic with
  accuracy                                        explicit
                                                  precision/rounding

  Optional integer value  `Integer`               Object form can be
  or collection element                           `null` and works with
                                                  generics

  Text                    `String`                Text is represented by
                                                  a class
  -----------------------------------------------------------------------

Do not choose a type only because it uses fewer bytes. Choose one that
safely represents the domain values and makes the code clear.

## 12. Common interview questions

### Q1. How many primitive data types are available in Java?

There are eight: `byte`, `short`, `int`, `long`, `float`, `double`,
`char`, and `boolean`.

### Q2. Is `String` a primitive data type?

No. `String` is a class and therefore a reference type.

### Q3. What is the difference between `int` and `Integer`?

`int` is a primitive type. `Integer` is its wrapper class. An `Integer`
can be `null` and can be used in collections such as `List<Integer>`.

### Q4. What is the default value of a local variable?

There is no automatic default value for a local variable. It must be
definitely assigned before it is read. Fields do receive default values.

### Q5. What is the default type of an integer literal?

An integer literal is normally `int`, unless it has an `L`/`l` suffix or
is otherwise contextually handled by the language's literal rules.

### Q6. What is the default type of a decimal literal?

A decimal floating-point literal such as `10.5` is `double` by default.
Use `10.5f` for a `float` literal.

### Q7. Can boolean be converted to int?

No. Java does not allow a conversion between `boolean` and numeric
types.

### Q8. Why does `byte + byte` produce an `int`?

Because `byte` operands are promoted to `int` for most arithmetic
operations.

### Q9. What happens when an integer overflows?

For ordinary integer arithmetic, the result wraps according to the
fixed-width two's-complement representation. Java does not automatically
throw an overflow exception.

### Q10. Why should `BigDecimal` be used for financial calculations?

Binary floating-point types such as `double` cannot represent many
decimal fractions exactly. `BigDecimal` supports decimal arithmetic with
explicit precision and rounding choices.

## 13. Practice exercises

Try these before checking the answers.

1.  Declare variables for an employee ID, employee name, salary, and
    active status using suitable types.

2.  What is the output of the following code?

    ``` java
    int a = 10;
    double b = 3;
    System.out.println(a / b);
    ```

3.  Why does the following code fail to compile?

    ``` java
    byte a = 10;
    byte b = 20;
    byte c = a + b;
    ```

4.  What is the difference between `==` and `.equals()` when comparing
    two `String` objects?

5.  What happens when you assign `null` to an `Integer` and then unbox
    it into an `int`?

### Answers

1.  One possible declaration:

    ``` java
    int employeeId = 101;
    String employeeName = "Ramesh";
    double salary = 75000.00;
    boolean isActive = true;
    ```

2.  Output: `3.3333333333333335` (the `int` value is promoted to
    `double` for division).

3.  `a + b` is promoted to `int`, and assigning that `int` to `byte`
    requires an explicit cast.

4.  `==` compares object identity for references; `.equals()` on
    `String` compares text content.

5.  Unboxing a null wrapper throws `NullPointerException`.

## 14. Quick revision

-   Java has **8 primitive types**.
-   Reference types include classes, arrays, interfaces, enums, and
    records.
-   `String` is a reference type, not a primitive.
-   `int` is the usual choice for whole numbers; `double` is the usual
    choice for decimal floating-point values.
-   Use `long` for larger integer ranges and `BigDecimal` for exact
    decimal calculations such as money.
-   Fields receive default values; local variables must be initialized
    before use.
-   Widening conversions are generally automatic; narrowing conversions
    usually need a cast and may lose information.
-   Wrapper classes allow primitive values to be used as objects.
-   `var` infers a local variable's type; it does not remove Java's
    static typing.

## 15. Recommended way to learn

1.  Practise declaring all eight primitive types.
2.  Print each type's minimum and maximum values using wrapper constants
    such as `Integer.MIN_VALUE` and `Integer.MAX_VALUE`.
3.  Experiment with widening, narrowing, overflow, and type promotion.
4.  Compare `String` references using `==` and `.equals()`.
5.  Practise wrapper classes, autoboxing, and unboxing.
6.  Build a small employee program using `int`, `String`, `double`,
    `boolean`, arrays, and an `enum`.
