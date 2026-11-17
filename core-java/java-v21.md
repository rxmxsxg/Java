# Java 21 Features

## Overview

Java 21, released in **September 2023**, is a **Long-Term Support (LTS)** release that introduces major improvements in concurrency, pattern matching, performance, and developer productivity.

---

# 1. Virtual Threads (Final)

One of the most significant features of Java 21.

Virtual Threads are lightweight threads managed by the JVM instead of the operating system.

### Traditional Thread

```java
Thread thread = new Thread(() -> {
    System.out.println("Task");
});
thread.start();
```

### Virtual Thread

```java
Thread.startVirtualThread(() -> {
    System.out.println("Task");
});
```

### Benefits

- Millions of concurrent threads
- Reduced memory consumption
- Simplified concurrent programming
- Better scalability

### Example

```java
try (var executor =
         Executors.newVirtualThreadPerTaskExecutor()) {

    executor.submit(() -> {
        System.out.println("Hello Virtual Thread");
        return null;
    });
}
```

---

# 2. Structured Concurrency (Preview)

Treats multiple tasks as a single unit of work.

### Example

```java
try (var scope =
    new StructuredTaskScope.ShutdownOnFailure()) {

    Future<String> user =
        scope.fork(() -> getUser());

    Future<String> order =
        scope.fork(() -> getOrder());

    scope.join();
    scope.throwIfFailed();

    System.out.println(
        user.resultNow() + order.resultNow());
}
```

### Benefits

- Better error handling
- Easier cancellation
- Improved readability

---

# 3. Record Patterns (Final)

Allows destructuring records directly.

### Record

```java
record Person(String name, int age) {}
```

### Example

```java
if (obj instanceof Person(String name, int age)) {
    System.out.println(name);
}
```

### Benefits

- Cleaner code
- Easier object decomposition

---

# 4. Pattern Matching for Switch (Final)

Enhanced switch statements with patterns.

### Example

```java
static String format(Object obj) {
    return switch (obj) {
        case Integer i -> "Integer: " + i;
        case String s -> "String: " + s;
        case null -> "Null";
        default -> "Unknown";
    };
}
```

### Benefits

- Reduced casting
- Better type safety
- Cleaner code

---

# 5. Sequenced Collections

Provides consistent ordering operations for collections.

### New Interfaces

```java
SequencedCollection
SequencedSet
SequencedMap
```

### Example

```java
SequencedSet<String> set =
    new LinkedHashSet<>();

set.add("Java");
set.add("Spring");

System.out.println(set.getFirst());
System.out.println(set.getLast());
```

### New Methods

```java
getFirst()
getLast()
addFirst()
addLast()
reversed()
```

---

# 6. String Templates (Preview)

Simplifies string interpolation.

### Example

```java
String name = "John";

String message =
    STR."Hello \{name}";
```

### Benefits

- Cleaner string formatting
- Safer SQL and JSON generation

---

# 7. Scoped Values (Preview)

An alternative to ThreadLocal.

### Example

```java
static final ScopedValue<String> USER =
    ScopedValue.newInstance();

ScopedValue.where(USER, "Admin")
    .run(() -> {
        System.out.println(USER.get());
    });
```

### Benefits

- Better performance
- Immutable context sharing
- Works well with Virtual Threads

---

# 8. Foreign Function & Memory API (Preview)

Interacts with native libraries without JNI.

### Example

```java
MemorySegment segment =
    Arena.ofConfined()
         .allocate(100);
```

### Benefits

- Native memory access
- Better safety
- Higher performance

---

# 9. Unnamed Patterns and Variables (Preview)

Ignore unused variables.

### Before

```java
if (obj instanceof Person p) {
}
```

### Java 21

```java
if (obj instanceof Person _) {
}
```

### Benefits

- Cleaner code
- Better readability

---

# 10. Key Encapsulation Mechanism API (KEM)

Adds support for post-quantum cryptography preparations.

### Benefits

- Modern security support
- Future-proof cryptographic operations

---

# 11. Z Garbage Collector (ZGC) Enhancements

### Improvements

- Lower latency
- Better memory management
- Higher scalability

### Suitable For

- Large enterprise applications
- Low-latency systems

---

# 12. Generational ZGC

Introduces generations in ZGC.

### Benefits

- Better throughput
- Lower garbage collection overhead
- Improved memory efficiency

---

# 13. Vector API (Incubator)

Provides vector computations using modern CPU instructions.

### Use Cases

- Machine Learning
- Scientific Computing
- Financial Analytics
- Image Processing

---

# 14. Deprecation and Removals

### Removed

- Legacy APIs and outdated features
- Some obsolete JVM options

### Benefits

- Cleaner platform
- Easier maintenance

---

# Java 21 Language Improvements

### Records

```java
record Employee(
    Long id,
    String name
) {}
```

### Sealed Classes

```java
sealed class Shape
permits Circle, Square {
}
```

### Text Blocks

```java
String json = """
{
  "name":"Java"
}
""";
```

### Switch Expressions

```java
String result = switch(day) {
    case "SAT" -> "Weekend";
    default -> "Weekday";
};
```

---

# Java 17 vs Java 21

| Feature | Java 17 | Java 21 |
|----------|----------|----------|
| Records | ✅ | ✅ |
| Sealed Classes | ✅ | ✅ |
| Text Blocks | ✅ | ✅ |
| Pattern Matching for instanceof | ✅ | ✅ |
| Virtual Threads | ❌ | ✅ |
| Record Patterns | ❌ | ✅ |
| Pattern Matching for Switch | Preview | ✅ |
| Sequenced Collections | ❌ | ✅ |
| Scoped Values | ❌ | Preview |
| String Templates | ❌ | Preview |
| Structured Concurrency | ❌ | Preview |

---

# Top Java 21 Interview Features

1. Virtual Threads
2. Structured Concurrency
3. Record Patterns
4. Pattern Matching for Switch
5. Sequenced Collections
6. Scoped Values
7. String Templates
8. Foreign Function & Memory API
9. Generational ZGC
10. Vector API

---

# Why Upgrade to Java 21?

- Long-Term Support (LTS)
- Massive improvement in concurrency using Virtual Threads
- Better pattern matching
- Modern collection APIs
- Improved performance and garbage collection
- Enhanced cloud-native application support
- Reduced complexity for asynchronous programming

---

# Summary

Java 21 is the most significant Java release since Java 8 because of **Virtual Threads (Project Loom)**.

The most important Java 21 features are:

- **Virtual Threads**
- **Structured Concurrency**
- **Record Patterns**
- **Pattern Matching for Switch**
- **Sequenced Collections**
- **Scoped Values**
- **Generational ZGC**

These features make Java applications more scalable, readable, and efficient while simplifying concurrent programming.