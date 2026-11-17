# Java 8 Features

Java 8, released in **March 2014**, was one of the most significant Java releases. It introduced functional programming capabilities and several enhancements to improve code readability, maintainability, and performance.

## 1. Lambda Expressions

Lambda expressions enable writing anonymous functions more concisely.

### Before Java 8

```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};
```

### Java 8

```java
Runnable r = () -> System.out.println("Hello");
```

### Benefits

- Less boilerplate code
- Improved readability
- Supports functional programming

---

## 2. Functional Interfaces

A functional interface contains only one abstract method.

### Example

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}
```

### Common Functional Interfaces

- Predicate<T>
- Function<T,R>
- Consumer<T>
- Supplier<T>

---

## 3. Stream API

Allows processing collections in a functional style.

### Example

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");

names.stream()
     .filter(name -> name.startsWith("J"))
     .forEach(System.out::println);
```

### Features

- Filtering
- Mapping
- Sorting
- Reducing
- Parallel processing

---

## 4. Method References

Shorter version of lambda expressions for calling existing methods.

### Example

```java
List<String> names = Arrays.asList("Java", "Python", "C++");

names.forEach(System.out::println);
```

### Types

- Static Method Reference
- Instance Method Reference
- Constructor Reference

---

## 5. Default Methods in Interfaces

Interfaces can now have method implementations.

### Example

```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle Started");
    }
}
```

### Benefits

- Backward compatibility
- Easier interface evolution

---

## 6. Static Methods in Interfaces

Interfaces can contain static methods.

### Example

```java
interface MathUtil {
    static int square(int x) {
        return x * x;
    }
}
```

Usage:

```java
MathUtil.square(5);
```

---

## 7. Optional Class

Helps avoid NullPointerException.

### Example

```java
Optional<String> name = Optional.of("Java");

name.ifPresent(System.out::println);
```

### Common Methods

```java
isPresent()
get()
orElse()
orElseGet()
orElseThrow()
```

---

## 8. New Date and Time API

Introduced in package:

```java
java.time
```

### Example

```java
LocalDate today = LocalDate.now();
LocalTime time = LocalTime.now();

System.out.println(today);
System.out.println(time);
```

### Important Classes

- LocalDate
- LocalTime
- LocalDateTime
- ZonedDateTime
- Period
- Duration

### Benefits

- Immutable
- Thread-safe
- Better than Date and Calendar

---

## 9. Collectors API

Used with Streams for aggregation.

### Example

```java
List<String> names = Arrays.asList("A", "B", "C");

List<String> result = names.stream()
                           .collect(Collectors.toList());
```

Common Collectors:

```java
toList()
toSet()
joining()
groupingBy()
counting()
```

---

## 10. forEach Method

Simplified iteration over collections.

### Example

```java
List<String> names = Arrays.asList("Java", "Spring", "Hibernate");

names.forEach(System.out::println);
```

---

## 11. Parallel Streams

Process data in parallel using multiple CPU cores.

### Example

```java
numbers.parallelStream()
       .forEach(System.out::println);
```

### Benefits

- Improved performance for large datasets
- Automatic thread management

---

## 12. Nashorn JavaScript Engine

Execute JavaScript within Java applications.

### Example

```java
ScriptEngine engine =
    new ScriptEngineManager()
        .getEngineByName("nashorn");

engine.eval("print('Hello from JavaScript');");
```

---

## 13. CompletableFuture

Supports asynchronous programming.

### Example

```java
CompletableFuture.runAsync(() ->
    System.out.println("Async Task"));
```

### Benefits

- Non-blocking programming
- Better async code management

---

## 14. Type and Repeatable Annotations

### Type Annotations

```java
List<@NonNull String> names;
```

### Repeatable Annotations

```java
@Role("Admin")
@Role("Manager")
class User {
}
```

---

## Most Important Interview Features

1. Lambda Expressions
2. Functional Interfaces
3. Stream API
4. Method References
5. Optional Class
6. Date and Time API
7. Default Methods
8. Parallel Streams
9. CompletableFuture

## Summary

Java 8 revolutionized Java development by introducing:

- Functional Programming
- Lambda Expressions
- Stream API
- Optional Class
- New Date & Time API
- Interface Default Methods
- Parallel Processing
- CompletableFuture

These features made Java code more concise, expressive, and efficient.