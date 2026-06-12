# How Java Works

Last Updated: 12 Jun, 2026

This document explains, in a structured way, how Java programs are built and executed. It covers the compile/run lifecycle, the Java Virtual Machine (JVM) internals, memory layout, class loading, bytecode and the JIT compiler, garbage collection, and includes a small example with commands and a short `javap` (bytecode) inspection.

## 1. High-level contract

- Inputs: `.java` source files containing Java code.
- Outputs: `.class` files (bytecode) and the program's observable behavior when run on a JVM.
- Error modes: compile-time syntax/type errors, runtime exceptions/errors, JVM crashes (rare), and resource limits (memory/threads).
- Success criteria: compiled without errors, runs on any JVM-compliant platform with expected output.

## 2. Development → Execution flow (summary)

1. Write Java source code in `.java` files.
2. Compile source with `javac` → produces `.class` files containing Java bytecode.
3. The JVM loads classes, verifies bytecode, and executes it using an interpreter and/or JIT-compiled native code.
4. The program runs with services from the JVM (thread scheduling, GC, security manager, classloading).

## Java program lifecycle (picture-aligned, step-by-step)

Below is a detailed, step-by-step explanation that follows the picture you provided (HelloWorld.java → javac → HelloWorld.class → JVM → Program). Each numbered step shows the command you run, what the tool does, and the relevant JVM internals.

1) Create the source file (HelloWorld.java)

  - Action: write Java source in a file named after the public class.
  - Example file `HelloWorld.java`:

```java
public class HelloWorld {
   public static void main(String[] args) {
      System.out.println("Hello World!");
   }
}
```

  - Why filename matters: a top-level `public` class must be in a file with the same name (here `HelloWorld.java`).

2) Compile source to bytecode with `javac` (HelloWorld.class)

  - Command:

```bash
javac HelloWorld.java
```

  - What `javac` does (pipeline): lexing → parsing → AST → symbol table/semantic analysis → annotation processing → bytecode generation → write `.class` file(s).
  - Output: `HelloWorld.class` containing JVM bytecode and attributes (constant pool, method code, LineNumberTable, StackMapTable, etc.).

3) Inspect the `.class` file (optional)

  - Command:

```bash
javap -c -v HelloWorld
```

  - This prints method bytecode, stack/local variable info and the constant pool so you can see the translation from Java source to bytecode instructions.

4) Launch the JVM and load classes (`java HelloWorld`)

  - Command:

```bash
java HelloWorld
```

  - What happens when `java` starts:
    - The JVM process is launched. The launcher locates the bootstrap classes (core Java) and the application classpath.
    - The Application (system) class loader locates `HelloWorld.class` (from current directory, classpath or module path).

5) Class loading, linking, and initialization (per-class lifecycle)

  - Loading: the binary class data is read into memory by a class loader.
  - Linking: three sub-steps
    - Verification: bytecode verifier checks structural correctness and type-safety (prevents illegal memory access or stack misuse). Failures produce `VerifyError`.
    - Preparation: static fields are allocated and set to default values.
    - (Optional) Resolution: symbolic references (names in constant pool) are resolved to direct references (can be lazy).
  - Initialization: JVM runs `<clinit>` (static initializers and `static { }` blocks) in the proper dependency order. Only after initialization is the class ready for use.

6) Execution: interpreter + JIT

  - The Execution Engine interprets bytecode instructions using an internal bytecode interpreter.
  - The JVM profiles method execution; hot methods are compiled by the JIT to native machine code for faster execution.
  - Modern HotSpot uses tiered compilation (C1 for quick optimizations, C2 for deeper optimizations).

7) Runtime memory areas (what the JVM uses while executing)

  - Heap: objects and arrays live here. It's garbage-collected.
  - Stack (per thread): each method call gets a stack frame with local variables and operand stack.
  - Metaspace: class metadata and static structures (replaces PermGen in modern JVMs).
  - Code cache: JIT-produced native code and runtime stubs.
  - PC registers and native memory for OS-level resources.

8) Output and program termination

  - The program prints `Hello World!` to stdout because `System.out.println` writes to the standard output stream handled by the JVM.
  - On normal termination the JVM runs shutdown hooks (if any), releases OS resources and exits with a status code.

Quick ASCII flow (maps to your picture)

```
HelloWorld.java  --(javac)-->  HelloWorld.class  --(java launcher)-->  JVM (classloader -> verify -> link -> init -> exec)  --> Program output
```

Notes and common variants

- Single-file run (Java 11+): you can skip `javac` for simple programs:

```bash
java HelloWorld.java
```

- Packaging into a JAR changes the location where the launcher finds classes but the lifecycle is otherwise identical:

```bash
jar cfe hello.jar HelloWorld HelloWorld.class
java -jar hello.jar
```

- If the remote or local classpaths differ you'll see `NoClassDefFoundError` or `ClassNotFoundException`.

Troubleshooting tips (quick):

- `UnsupportedClassVersionError`: compiled with newer Java than the runtime. Recompile or use a newer JVM.
- `VerifyError` or `ClassFormatError`: likely corrupted class, incompatible bytecode or a bug in an agent/bytecode manipulator.
- `NoClassDefFoundError`: class was present at compile time but not found at runtime (check classpath/JARs).

The sections later in this file go deeper into the JVM internals (GC, JIT, memory layout and tooling). The step-by-step sequence above follows the image you provided while adding the underlying details for each stage.

## 3. Compilation step

- `javac HelloWorld.java` parses the source, checks types, and emits `.class` bytecode files.
- Bytecode is platform-independent; the same `.class` can run on any OS that has a JVM implementation.

Example compile and run:

```bash
javac HelloWorld.java
java HelloWorld
```

## 4. Java Virtual Machine (JVM) — core components

- Class Loader Subsystem: Finds and loads binary class data (from .class files, JARs, or network).
  - Bootstrap, Extension (Platform), and Application (System) class loaders are the typical hierarchy.
- Bytecode Verifier: Ensures loaded bytecode obeys JVM safety rules; prevents certain illegal operations.
- Runtime Data Areas: Memory regions the JVM uses during execution (detailed below).
- Execution Engine: Interprets bytecode and invokes the JIT compiler for hot code paths.
- Native Interface: JNI for calling native (C/C++) libraries when needed.

## 5. JVM memory structure (common HotSpot layout)

- Heap: Stores objects and arrays. Collected by the Garbage Collector.
- Stack (per thread): Holds frames for method calls (local variables, operand stack, return addresses).
- Native/Code Cache: JIT-compiled native code and JVM internal code.
- Metaspace (or PermGen in older JVMs): Class metadata, method data, constants.
- PC Register (per thread): Keeps address of the currently executing JVM instruction.

Why this matters: memory areas affect GC tuning, performance, and out-of-memory errors.

## 6. Class loading and linking phases

1. Loading: Binary data for a class is located and read.
2. Linking:
   - Verification: Checks structural correctness.
   - Preparation: Allocates static fields and sets default values.
   - (Optional) Resolution: Resolves symbolic references to direct references.
3. Initialization: Executes static initializers and `static {}` blocks.

Class loaders create separate namespaces; two classes with the same fully-qualified name loaded by different class loaders are treated as distinct.

## 7. Bytecode and the JIT

- Bytecode: A compact, stack-based instruction set (e.g., iload_1, invokevirtual, getfield).
- Interpreter: Executes bytecode directly — quick startup, slower steady-state.
- JIT (Just-In-Time) compiler: Observes hot methods and compiles them into optimized native code (improves throughput for long-running apps).
- Tiered compilation: Modern JVMs (HotSpot) use multiple compilation levels (C1, C2) balancing startup and peak performance.

Quick bytecode inspection (after compile):

```bash
javap -c HelloWorld
```

This prints a human-readable form of bytecode for each method.

## 8. Garbage collection (GC)

- The GC reclaims memory for objects no longer reachable.
- Common collectors in HotSpot:
  - Serial: single-threaded, simple (good for small apps/dev).
  - Parallel (Throughput): multi-threaded GC for high throughput.
  - G1 (Garbage-First): Balanced pauses and throughput, now default in many JDKs.
  - ZGC and Shenandoah: Low-pause collectors for extremely large heaps.
- Generational hypothesis: Most objects die young. Heaps usually split into Young and Old generations to optimize GC.

Tuning GC involves choosing an algorithm and configuring heap sizes:

```bash
java -Xms512m -Xmx2g -XX:+UseG1GC HelloWorld
```

## 9. Example: HelloWorld and a method that demonstrates stack/heap behavior

Save this as `HowJavaWorksExample.java`:

```java
public class HowJavaWorksExample {
    public static void main(String[] args) {
        System.out.println("Start");
        int result = factorial(5);
        System.out.println("5! = " + result);
        System.out.println("End");
    }

    static int factorial(int n) {
        if (n <= 1) return 1;
        return n * factorial(n - 1);
    }
}
```

Explanation:
- Each call to `factorial` pushes a new frame onto the thread stack (locals and return address).
- The allocated ints are primitives stored on the stack; if we used `new Integer(...)` instead, the Integer objects would be allocated on the heap and later collected.

Compile and run:

```bash
javac HowJavaWorksExample.java
java HowJavaWorksExample
```

Inspect bytecode for `factorial`:

```bash
javap -c HowJavaWorksExample
```

You will see instructions for loading arguments, calling methods, and returning values (e.g., iload_0, ifle, iconst_1, imul, ireturn).

## 10. Common pitfalls and tips

- Forgetting to compile before running: `java` needs `.class` files unless running JShell or single-file source mode (Java 11+ supports `java File.java`).
- ClassNotFoundException / NoClassDefFoundError: Check classpath and packaging.
- OutOfMemoryError: inspect heap usage, increase `-Xmx` or check for memory leaks.
- Threading issues: race conditions, deadlocks — use proper synchronization or high-level concurrency utilities (`java.util.concurrent`).
- Don’t prematurely tune the JVM — measure with profiling tools (`jcmd`, `jvisualvm`, `async-profiler`).

## 11. Useful commands and tools

- Compile: `javac MyClass.java`
- Run: `java MyClass`
- Show bytecode: `javap -c MyClass`
- Show memory and GC info: `java -Xlog:gc* -jar app.jar` (JDK 9+ unified logging)
- Tools: `jcmd`, `jstack`, `jmap`, `jstat`, `jvisualvm`


---

