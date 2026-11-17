# Java 17 Features

## Overview

Java 17, released in **September 2021**, is a **Long-Term Support (LTS)** release. It includes several language enhancements, JVM improvements, security updates, and performance optimizations.

---

# 1. Sealed Classes

Sealed classes restrict which classes can extend or implement them.

### Example

```java
public sealed class Shape
    permits Circle, Rectangle {
}

final class Circle extends Shape {
}

final class Rectangle extends Shape {
}
```

### Benefits

- Better control over inheritance
- Improved maintainability
- Supports exhaustive pattern matching

---

# 2. Enhanced Switch Expressions

Switch became more concise and expressive.

### Example

```java
String dayType = switch(day) {
    case "SATURDAY", "SUNDAY" -> "Weekend";
    default -> "Weekday";
};
```

### Benefits

- Cleaner syntax
- Eliminates many break statements
- Can return values directly

---

# 3. Pattern Matching for `instanceof`

Removes the need for explicit type casting.

### Before Java 17

```java
if (obj instanceof String) {
    String str = (String) obj;
    System.out.println(str.length());
}
```

### Java 17

```java
if (obj instanceof String str) {
    System.out.println(str.length());
}
```

### Benefits

- Less boilerplate code
- Improved readability

---

# 4. Records

Records provide a compact way to create immutable data classes.

### Traditional POJO

```java
public class Employee {
    private final String name;
    private final int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
}
```

### Java 17 Record

```java
public record Employee(
    String name,
    int age
) {}
```

### Automatically Generates

- Constructor
- Getters
- equals()
- hashCode()
- toString()

---

# 5. Text Blocks

Multi-line string literals.

### Example

```java
String html = """
    <html>
        <body>
            <h1>Hello Java 17</h1>
        </body>
    </html>
    """;
```

### Benefits

- Cleaner SQL queries
- Better HTML/XML formatting
- Easier JSON construction

---

# 6. Strong Encapsulation of JDK Internals

Internal JDK APIs are strongly encapsulated.

### Benefits

- Better security
- Improved maintainability
- Encourages supported APIs

---

# 7. New macOS Rendering Pipeline

Uses Apple's Metal API instead of OpenGL.

### Benefits

- Better graphics performance
- Improved macOS compatibility

---

# 8. Foreign Function & Memory API (Incubator)

Provides safer access to native code.

### Example Use Cases

- Calling C libraries
- Native memory management
- High-performance applications

### Benefits

- Alternative to JNI
- Better safety
- Simpler programming model

---

# 9. Context-Specific Deserialization Filters

Provides more control when deserializing objects.

### Benefits

- Enhanced security
- Protection against malicious serialized data

---

# 10. Enhanced Random Number Generators

Introduces new interfaces and algorithms.

### Example

```java
RandomGenerator generator =
    RandomGenerator.getDefault();

int num = generator.nextInt();
```

### Benefits

- Better performance
- More random algorithms
- Improved flexibility

---

# 11. Deprecation of Security Manager

Security Manager is deprecated for future removal.

### Reason

- Modern security practices have evolved
- Low usage in newer applications

---

# 12. JVM Performance Improvements

Java 17 includes improvements in:

- Garbage Collection
- JIT Compilation
- Memory Management
- Startup Performance

### Supported Garbage Collectors

- G1 GC
- ZGC
- Shenandoah GC

---

# 13. Helpful NullPointerException Messages

Java provides detailed NPE error messages.

### Example

```java
user.getAddress().getCity();
```

Error:

```text
Cannot invoke "Address.getCity()"
because "user.getAddress()" is null
```

### Benefits

- Faster debugging
- Improved developer productivity

---

# 14. Vector API (Incubator)

Provides vector computations that can leverage modern CPU instructions.

### Use Cases

- Machine Learning
- Scientific Computing
- Financial Calculations

---

# 15. Modern Language Features Available in Java 17

Java 17 includes features introduced in previous releases, such as:

### Java 8
- Lambda Expressions
- Stream API
- Optional
- Date & Time API

### Java 11
- HTTP Client API
- String Methods
- Local Variable Syntax (`var`)

### Java 16
- Records
- Pattern Matching Enhancements

---

# Key Interview Features of Java 17

1. Sealed Classes
2. Records
3. Pattern Matching for `instanceof`
4. Text Blocks
5. Enhanced Switch Expressions
6. Foreign Function & Memory API
7. Enhanced Random Number Generators
8. Strong Encapsulation
9. ZGC and Shenandoah Improvements
10. Helpful NullPointerExceptions

---

# Java 8 vs Java 17

| Feature | Java 8 | Java 17 |
|----------|---------|---------|
| Lambda Expressions | ✅ | ✅ |
| Stream API | ✅ | ✅ |
| Optional | ✅ | ✅ |
| Date-Time API | ✅ | ✅ |
| Records | ❌ | ✅ |
| Sealed Classes | ❌ | ✅ |
| Text Blocks | ❌ | ✅ |
| Pattern Matching | ❌ | ✅ |
| Enhanced Switch | ❌ | ✅ |
| Strong Encapsulation | ❌ | ✅ |

---

# Summary

Java 17 is a modern LTS release focused on:

- Improved Developer Productivity
- Better Performance
- Enhanced Security
- Reduced Boilerplate Code
- Stronger Type Safety

The most important features are:

- **Records**
- **Sealed Classes**
- **Pattern Matching for instanceof**
- **Text Blocks**
- **Enhanced Switch Expressions**

These features make Java applications cleaner, safer, and easier to maintain.