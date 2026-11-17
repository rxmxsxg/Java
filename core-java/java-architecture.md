# Java Architecture

## Overview

Java follows the principle:

> **"Write Once, Run Anywhere (WORA)"**

Java architecture enables Java programs to run on any platform without recompilation by using the **Java Virtual Machine (JVM)**.

---

# Java Architecture Diagram

```text
+--------------------------------+
|       Java Application         |
|       (.java Source File)      |
+--------------------------------+
               |
               v
+--------------------------------+
|        Java Compiler           |
|            (javac)             |
+--------------------------------+
               |
               v
+--------------------------------+
|         Bytecode (.class)      |
+--------------------------------+
               |
               v
+--------------------------------+
|               JVM              |
|   (Java Virtual Machine)       |
+--------------------------------+
     |          |         |
     v          v         v
   Class      Memory     JIT
  Loader      Area     Compiler
     |
     v
+--------------------------------+
|            JRE                 |
|  JVM + Java Libraries          |
+--------------------------------+
               |
               v
+--------------------------------+
|        Operating System        |
+--------------------------------+
               |
               v
+--------------------------------+
|            Hardware            |
+--------------------------------+
```

---

# Components of Java Architecture

## 1. Java Source Code

Java programs are written in:

```java
HelloWorld.java
```

Example:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello Java");
    }
}
```

---

## 2. Java Compiler (javac)

The Java Compiler converts:

```text
.java
```

into

```text
.class
```

(Bytecode)

```bash
javac HelloWorld.java
```

Output:

```text
HelloWorld.class
```

---

## 3. Bytecode

Bytecode is platform-independent instruction code.

```text
Java Source Code
        ↓
     javac
        ↓
    Bytecode
```

Advantages:

- Platform Independent
- Secure
- Portable

---

# JVM (Java Virtual Machine)

JVM is the heart of Java Architecture.

Responsibilities:

- Loads classes
- Verifies bytecode
- Executes bytecode
- Manages memory
- Performs Garbage Collection

```text
Bytecode
    ↓
   JVM
    ↓
Machine Code
```

---

# JVM Architecture

```text
+-----------------------------------+
|              JVM                  |
+-----------------------------------+
| Class Loader Subsystem            |
+-----------------------------------+
| Runtime Data Areas                |
+-----------------------------------+
| Execution Engine                  |
+-----------------------------------+
| Native Method Interface (JNI)     |
+-----------------------------------+
| Native Method Libraries           |
+-----------------------------------+
```

---

# 4. Class Loader Subsystem

Loads `.class` files into memory.

### Types of Class Loaders

#### Bootstrap Class Loader

Loads core Java classes:

```text
java.lang.*
java.util.*
```

#### Extension Class Loader

Loads extension libraries.

#### Application Class Loader

Loads application classes.

---

# 5. Bytecode Verifier

Checks bytecode for:

- Security
- Format correctness
- Illegal access

Ensures safe execution before running.

---

# 6. Runtime Data Areas

Memory areas used by JVM.

## Method Area

Stores:

- Class metadata
- Static variables
- Runtime constants

```text
Class Information
Methods
Static Variables
```

---

## Heap Area

Stores:

- Objects
- Instance variables

Example:

```java
Employee emp = new Employee();
```

The object is stored in Heap Memory.

### Shared Memory

Used by all threads.

---

## Stack Area

Stores:

- Method calls
- Local variables
- References

Example:

```java
int x = 10;
```

Stored in Stack Memory.

### One Stack per Thread

```text
Thread 1 → Stack 1
Thread 2 → Stack 2
```

---

## Program Counter (PC) Register

Stores:

```text
Current instruction address
```

Each thread has its own PC Register.

---

## Native Method Stack

Used when calling:

```java
C
C++
Native Code
```

through JNI.

---

# 7. Execution Engine

Executes bytecode.

Components:

## Interpreter

Reads bytecode line by line.

```text
Bytecode → Interpretation → Execution
```

### Advantage

- Fast startup

### Disadvantage

- Slower execution

---

## JIT Compiler (Just-In-Time Compiler)

Converts frequently used bytecode into machine code.

```text
Bytecode
    ↓
JIT Compiler
    ↓
Machine Code
```

Benefits:

- Faster execution
- Better performance

---

## Garbage Collector (GC)

Automatically removes unused objects.

Example:

```java
Employee emp = null;
```

Object becomes eligible for garbage collection.

Responsibilities:

- Memory cleanup
- Memory optimization

Popular GCs:

- G1 GC
- ZGC
- Shenandoah GC
- Parallel GC

---

# 8. JNI (Java Native Interface)

Allows Java to interact with native applications.

Example:

```java
Native Method
C Program
C++ Library
```

```java
public native void display();
```

Uses:

- Device Drivers
- Native Libraries
- OS-specific Functions

---

# 9. Native Method Libraries

Libraries written in:

- C
- C++
- Assembly

Examples:

```text
.dll (Windows)
.so  (Linux)
.dylib (macOS)
```

---

# JRE (Java Runtime Environment)

JRE provides everything needed to run Java applications.

```text
JRE = JVM + Libraries
```

Contains:

- JVM
- Core Libraries
- Runtime Components

### Purpose

Run Java Applications

---

# JDK (Java Development Kit)

JDK is used to develop Java applications.

```text
JDK = JRE + Development Tools
```

Tools included:

```text
javac
java
javadoc
jar
jdb
jconsole
```

### Purpose

Develop + Compile + Run Java Programs

---

# JDK vs JRE vs JVM

```text
JDK
 └── JRE
      └── JVM
```

| Component | Purpose |
|------------|---------|
| JVM | Executes Java Bytecode |
| JRE | Provides Runtime Environment |
| JDK | Provides Development Tools |

---

# Java Program Execution Flow

```text
1. Write Program (.java)
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
6. Execution Engine Executes Code
            |
            v
7. Output Generated
```

---

# Interview Question: Why Java is Platform Independent?

Because Java source code is compiled into:

```text
Bytecode (.class)
```

Bytecode runs on any operating system that has a compatible JVM.

```text
Java Program
      ↓
   Bytecode
      ↓
 Windows JVM
 Linux JVM
 macOS JVM
```

Same bytecode runs everywhere.

---

# Java Architecture Summary

```text
Source Code (.java)
        ↓
      javac
        ↓
 Bytecode (.class)
        ↓
      JVM
 ┌──────────────┐
 │ Class Loader │
 │ Memory Area  │
 │ JIT Compiler │
 │ GC           │
 └──────────────┘
        ↓
 Operating System
        ↓
    Hardware
```

## Key Components

1. JDK (Development Kit)
2. JRE (Runtime Environment)
3. JVM (Java Virtual Machine)
4. Class Loader
5. Runtime Memory Areas
6. Execution Engine
7. JIT Compiler
8. Garbage Collector
9. JNI
10. Native Libraries

**Formula to Remember:**

```text
JDK = JRE + Development Tools
JRE = JVM + Libraries
```