# Modern Java Architecture (Java 21 / Java 25)

## Overview

Java follows the principle:

> **Write Once, Run Anywhere (WORA)**

A Java application is compiled into **Bytecode**, which can run on any platform that has a compatible **Java Virtual Machine (JVM)**.

---

# Modern Java Architecture Diagram

```text
+-------------------------------------+
|        Java Application             |
|           (.java file)              |
+-------------------------------------+
                 |
                 v
+-------------------------------------+
|         Java Compiler               |
|             (javac)                 |
+-------------------------------------+
                 |
                 v
+-------------------------------------+
|        Bytecode (.class)            |
+-------------------------------------+
                 |
                 v
+--------------------------------------------------+
|                     JVM                          |
|                                                  |
|  +--------------------------------------------+  |
|  | Class Loader Subsystem                     |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | Bytecode Verifier                          |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | Runtime Data Areas                         |  |
|  |  - Heap                                    |  |
|  |  - Stack                                   |  |
|  |  - Metaspace                               |  |
|  |  - PC Register                             |  |
|  |  - Native Method Stack                     |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | Execution Engine                           |  |
|  |  - Interpreter                             |  |
|  |  - JIT Compiler (C1/C2)                    |  |
|  |  - Garbage Collector                       |  |
|  +--------------------------------------------+  |
|                                                  |
|  Modern Features                                |
|  - Virtual Threads (Project Loom)               |
|  - Scoped Values                                |
|  - Structured Concurrency                       |
|  - Foreign Function & Memory API                |
|  - Vector API                                   |
+--------------------------------------------------+
                 |
                 v
+-------------------------------------+
|        Operating System             |
+-------------------------------------+
                 |
                 v
+-------------------------------------+
|            Hardware                 |
+-------------------------------------+
```

---

# Java Platform Components

## JVM (Java Virtual Machine)

The JVM is responsible for:

- Loading classes
- Verifying bytecode
- Executing bytecode
- Managing memory
- Performing garbage collection
- Enabling platform independence

```text
Bytecode
    ↓
   JVM
    ↓
Machine Code
```

---

## JRE (Java Runtime Environment)

Provides the runtime environment required to run Java applications.

```text
JRE = JVM + Java Libraries
```

### Contents

- JVM
- Core Java Libraries
- Runtime Components

### Purpose

Run Java applications.

---

## JDK (Java Development Kit)

Provides tools for developing Java applications.

```text
JDK = JRE + Development Tools
```

### Common Tools

- javac
- java
- jar
- javadoc
- jdb
- jconsole

### Purpose

Develop, compile, and run Java programs.

---

# JVM Internal Architecture

## 1. Class Loader Subsystem

Loads class files into memory.

### Types of Class Loaders

#### Bootstrap Class Loader

Loads core Java classes:

```java
java.lang.*
java.util.*
java.io.*
```

#### Platform Class Loader

Loads standard Java platform libraries.

#### Application Class Loader

Loads application-specific classes.

---

## 2. Bytecode Verifier

Checks:

- Security rules
- Bytecode correctness
- Access permissions

Ensures safe execution before running code.

---

## 3. Runtime Data Areas

### Method Area / Metaspace

Stores:

- Class metadata
- Runtime constants
- Method information
- Static variables

---

### Heap Memory

Stores:

- Objects
- Instance variables

Example:

```java
Employee emp = new Employee();
```

The object is allocated in the Heap.

---

### Stack Memory

Stores:

- Local variables
- Method calls
- Object references

Example:

```java
int count = 10;
```

Stored inside the Stack.

Each thread has its own stack.

---

### Program Counter (PC) Register

Stores the address of the current instruction being executed.

Each thread has a dedicated PC Register.

---

### Native Method Stack

Used when JVM calls native code through:

```java
JNI (Java Native Interface)
```

---

# 4. Execution Engine

Executes bytecode.

## Interpreter

Reads and executes bytecode line by line.

### Advantages

- Fast startup
- Simple execution

### Disadvantages

- Slower for repetitive code

---

## JIT Compiler (Just-In-Time Compiler)

Converts frequently used bytecode into native machine code.

```text
Bytecode
    ↓
JIT Compiler
    ↓
Machine Code
```

### Benefits

- Faster execution
- Improved performance
- Optimized code generation

---

## Garbage Collector (GC)

Automatically removes unused objects from memory.

### Popular Garbage Collectors

- G1 GC (Default)
- ZGC
- Shenandoah GC
- Parallel GC

### Benefits

- Automatic memory management
- Reduced memory leaks
- Better application performance

---

# Modern Java Features (Java 21 / Java 25)

## Virtual Threads

Lightweight JVM-managed threads.

```java
Thread.startVirtualThread(() ->
    System.out.println("Hello"));
```

### Benefits

- Millions of concurrent threads
- High scalability
- Lower memory usage

---

## Scoped Values

Modern replacement for many ThreadLocal use cases.

```java
ScopedValue.where(USER, "Admin")
           .run(task);
```

### Benefits

- Immutable context sharing
- Better performance

---

## Structured Concurrency

Treats related concurrent tasks as a single unit.

### Benefits

- Simplified error handling
- Easier cancellation management
- Cleaner asynchronous code

---

## Foreign Function & Memory API

Allows Java to interact with native libraries without traditional JNI code.

### Benefits

- Simpler native integration
- Better performance
- Improved safety

---

## Vector API

Provides SIMD operations for high-performance computing.

### Use Cases

- Machine Learning
- Finance
- Scientific Computing
- Image Processing

---

# Java Program Execution Flow

```text
1. Write Source Code (.java)
              |
              v
2. Compile using javac
              |
              v
3. Generate Bytecode (.class)
              |
              v
4. JVM Loads Classes
              |
              v
5. Bytecode Verification
              |
              v
6. Memory Allocation
              |
              v
7. Execution Engine Runs Code
              |
              v
8. Garbage Collection
              |
              v
9. Output Generated
```

---

# Why Java is Platform Independent?

Java source code is compiled into platform-independent bytecode.

```text
Java Source Code
        ↓
       javac
        ↓
  Bytecode (.class)
        ↓
 ┌──────────────┐
 │ Windows JVM  │
 │ Linux JVM    │
 │ macOS JVM    │
 └──────────────┘
        ↓
   Machine Code
```

The same bytecode can run on any operating system with a compatible JVM.

---

# JDK vs JRE vs JVM

```text
JDK
 └── JRE
      └── JVM
```

| Component | Responsibility |
|------------|---------------|
| JVM | Executes Bytecode |
| JRE | Runtime Environment |
| JDK | Development + Runtime Tools |

---

# Interview Summary

### Formula

```text
JDK = JRE + Development Tools
JRE = JVM + Libraries
```

### Key Components

1. Java Source Code
2. Compiler (javac)
3. Bytecode
4. JVM
5. Class Loader
6. Runtime Memory Areas
7. Execution Engine
8. JIT Compiler
9. Garbage Collector
10. Virtual Threads
11. Scoped Values
12. Structured Concurrency
13. Foreign Function & Memory API

### Modern Java Architecture Highlights

- Virtual Threads (Project Loom)
- Scoped Values
- Structured Concurrency
- ZGC and Shenandoah GC
- Foreign Function & Memory API
- Vector API
- Metaspace instead of PermGen

This is the recommended Java Architecture explanation for **Java 21, Java 25, interviews, certifications, and modern enterprise development**.