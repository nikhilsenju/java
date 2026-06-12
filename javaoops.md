# 1 Java Classes, File Naming, Compilation and Execution (OOPs rules)

Last Updated: 12 Jun, 2026

This document explains common rules and behaviors about classes, file naming, compilation and execution in Java. The explanations follow the numbered points you provided and include concrete examples and common errors you will see if the rules are broken.

---

## 1.1 Class declarations and file-naming rules

Java source files can contain multiple class declarations, but there are strict rules about public classes and the filename.

- Number of classes per file
	- You can declare any number of classes in a single `.java` source file (for example `class A`, `class B`, `class C`, `class D`). There is no language limit on how many classes a single file may contain.

- Public class limit
	- At most one top-level class in a single source file may be declared `public`.
	- That means each `.java` file may contain exactly one `public` top-level class or none at all.

- File naming scenarios
	- Scenario A — No public class:
		- If none of the top-level classes are declared `public`, the source file may be named arbitrarily (for example `durga.java`). The filename does not have to match any class name.

	- Scenario B — One public class:
		- If one top-level class is declared `public` (for example `public class B`), the source file name must match the public class name: `B.java`.
		- If the filename does not match the public class, the compiler will produce an error like:

```
error: class B is public, should be declared in a file named B.java
```

Example (valid):

```java
// File: B.java
public class B {
		// class body
}

class A { }
class C { }
```

Example (valid without public class):

```java
// File: durga.java (filename can be any name)
class A { }
class B { }
class C { }
```

Example (invalid):

```java
// File: wrongname.java
public class B { }

// javac wrongname.java
// -> error: class B is public, should be declared in a file named B.java
```

---

## 1.2 compilation process and generated `.class` files

When you compile a Java source file, the compiler (`javac`) produces output on a per-class basis.

- Separate `.class` files for each class
	- For every top-level or nested class defined in the source, the compiler generates one `.class` file containing the bytecode for that class.
	- If `durga.java` contains `class A`, `class B`, `class C`, and `class D`, then running:

```bash
javac durga.java
```

	will produce `A.class`, `B.class`, `C.class`, and `D.class` (assuming those classes exist in the source). There will be no `durga.class` unless a class named `durga` is declared inside the file.

- Where `.class` files go
	- By default, the `.class` files are written to the current directory alongside the source file. You can change the output directory using `javac -d <outdir> ...`.

- Example source `durga.java` and compilation result

```java
// File: durga.java
class A { }
class B { }
class C { }
class D { }
```

Run:

```bash
javac durga.java
ls *.class
# -> A.class B.class C.class D.class
```

---

## 1.3 execution (`main` method) rules and behavior

The file name and public class rules are unrelated to which class contains the `main` method. You execute a specific class (its `.class`) and the JVM looks for its `main` method.

- How execution works
	- You compile one or more `.java` files into `.class` files with `javac`.
	- To run a program you call the launcher with a fully-qualified class name: `java A` will attempt to run the `main` method in class `A`.

- Multiple `main` methods
	- If several classes have their own `public static void main(String[] args)` method, each can be executed separately by calling `java` with the desired class name.

Examples:

```java
// File: MultiMain.java
class A {
		public static void main(String[] args) {
				System.out.println("A.main");
		}
}

class B {
		public static void main(String[] args) {
				System.out.println("B.main");
		}
}
```

Compile and run:

```bash
javac MultiMain.java
java A   # prints: A.main
java B   # prints: B.main
```

- Common runtime errors
	- Main method not found:
		- If you run `java D` but `D.class` exists and has no `main` method, the JVM will report an error similar to:

```
Error: Main method not found in class D, please define the main method as:
	 public static void main(String[] args)
```

	- Class not found / Could not find or load main class:
		- If you run `java durga` but there is no `durga.class` in the classpath (because source had no class `durga`), you'll get:

```
Error: Could not find or load main class durga
```

	- UnsupportedClassVersionError:
		- If a `.class` was compiled with a newer JDK than the runtime, the JVM complains with `UnsupportedClassVersionError`.

---

## 1.4 Quick summary checklist

- Classes per file: unlimited top-level classes allowed in a single `.java` file.
- Public classes: at most one `public` top-level class per source file.
- File naming: if a `public` top-level class exists, the filename must match it (`PublicClassName.java`). If there is no public class, the filename can be arbitrary.
- Compilation: `javac` generates one `.class` file per class defined in the source.
- Execution: you run a specific class using `java <ClassName>`; whichever class you specify, the JVM executes its `main` (if present).

---

## 2 Import statements and fully-qualified names

This section explains why you sometimes see the compiler error "cannot find symbol" when referring to library classes (for example `ArrayList`) and shows how to fix it using fully-qualified names or import statements. It also explains the difference between explicit and implicit imports and gives best-practice advice.

### 2.1 Core problem: "cannot find symbol"

- When you use a class like `ArrayList` in your code, the compiler must know which package the class belongs to.
- Writing:

```java
ArrayList l = new ArrayList();
```

without guidance will produce a compile-time error such as:

```
error: cannot find symbol
  symbol:   class ArrayList
```

This happens because the compiler recognizes the identifier `ArrayList` but has no mapping (import or fully-qualified reference) to where that class is defined.

### 2.2 Solution A — Fully qualified class names

- You can avoid imports by using the fully-qualified name every time you reference the type. For `ArrayList` (in `java.util`) that looks like:

```java
java.util.ArrayList<String> l = new java.util.ArrayList<>();
```

- This always works but quickly becomes verbose and hard to read when the class name is used repeatedly.

Example (compiles):

```java
public class Test {
	public static void main(String[] args) {
		java.util.ArrayList<String> list = new java.util.ArrayList<>();
		list.add("hello");
		System.out.println(list);
	}
}
```

### 2.3 Solution B — The `import` statement

- The idiomatic way is to add an `import` statement at the top of the source file. This tells the compiler which class name maps to which package so you can use the short class name in code.

```java
import java.util.ArrayList;

public class Test {
	public static void main(String[] args) {
		ArrayList<String> l = new ArrayList<>(); // short form, works because of import
	}
}
```

### 2.4 Explicit imports vs. implicit (wildcard) imports

- Explicit import
  - Syntax: `import java.util.ArrayList;`
  - Advantage: Readers immediately know the exact class dependency. IDEs and tooling prefer explicit imports for clarity.

- Implicit (wildcard) import
  - Syntax: `import java.util.*;`
  - Effect: makes all public classes in `java.util` available by simple name.
  - Drawback: reduces clarity and can cause ambiguous references if two packages contain classes with the same simple name (for example `com.hdfc.Account` and `com.icicibank.Account`). If both packages are wildcard-imported, the compiler will complain about ambiguity when `Account` is referenced.

Example ambiguity problem:

```java
import com.hdfc.*;
import com.icicibank.*;

public class UseAccount {
	public static void main(String[] args) {
		Account a; // which Account? compiler error if ambiguous
	}
}
```

### 2.5 Static imports (brief)

- Java also supports `static import` to import static members (fields or methods) so they can be referenced without a class qualifier.

```java
import static java.lang.Math.*;

public class UseMath {
	public static void main(String[] args) {
		double r = sqrt(2); // sqrt is available without Math.
	}
}
```

- Use static imports sparingly: overuse can reduce readability.

### 2.6 Best practices and IDE behavior

- Prefer explicit imports (`import java.util.ArrayList;`) over wildcard imports for readability and to avoid accidental name clashes.
- Modern IDEs (IntelliJ IDEA, Eclipse, VS Code with Java extensions) automatically manage and insert imports and will usually convert repeated wildcard imports to explicit imports per project style settings.
- When working on libraries or public APIs, explicit imports make dependencies clearer to readers and tools (static analysis, build systems).

### 2.7 Common errors and fixes

- `cannot find symbol` for a class: add the correct `import` or use the fully-qualified name, and ensure the library is on the classpath.
- `Cannot find symbol: variable Arrays` when using `Arrays` methods: add `import java.util.Arrays;` or use `java.util.Arrays.sort(...)`.
- Ambiguity after wildcard imports: replace wildcard imports with explicit ones for the specific classes you need.

---

If you want, I can now:
- Add example source files (`Test.java`, `MultiImport.java`) to the repository and compile them to show the errors and fixes live.
- Add a short table comparing fully-qualified names, explicit imports, wildcard imports, and static imports.

Tell me which next action you prefer and I will run it.

## 3 Import nuances: default packages and the sub-package trap

This topic explains two important edge cases covered in the video: (1) which packages are implicitly available (no import required) and (2) why wildcard imports do not include sub-packages (the "sub-package trap"). The examples are exact and exam-friendly.

### 3.1 The two default packages (no import required)

Java gives you automatic access to classes in two situations — you don't need to add an `import` statement for these.

#### 3.1.1 `java.lang`

- The entire `java.lang` package is implicitly imported into every Java source file.
- Common classes in `java.lang` include: `String`, `Thread`, `Exception`, `StringBuffer`, `System`, `Math`, etc.
- Example: you can write

```java
String s = new String("durga");
System.out.println(s);
```

without any import and it will compile and run because `String` and `System` are part of `java.lang`.

#### 3.1.2 The default (unnamed) package — same directory classes

- If two classes live in the same directory (the default package when no `package` declaration is used), you can reference one from the other without an import.
- Example: if `Test.java` and `Student.java` are both in the same folder and neither declares a `package`, then `Test` can use `Student` directly:

```java
// File: Student.java
class Student { }

// File: Test.java
class Test {
	public static void main(String[] args) {
		Student s = new Student();
	}
}
```

No import is necessary because the compiler looks in the current directory for classes in the unnamed package.

> Note: Relying on the unnamed package is not recommended for larger projects or libraries; it's fine for small demos or learning exercises.

### 3.2 The sub-package trap (packages are not recursive)

This is a very common exam/interview trap: importing a package with a wildcard does NOT import classes from its sub-packages.

- Consider the `Pattern` class which lives at `java.util.regex.Pattern` (package path: `java` -> `util` -> `regex`).

- Evaluate these import attempts when you want to use `Pattern`:

❌ `import java.*;` or `import java.r*;` — Fails. Wildcards only match the classes directly inside the named package, not deeper levels.

❌ `import java.util.*;` — Fails for `Pattern` because `Pattern` is in the `java.util.regex` sub-package, not directly in `java.util`.

✅ `import java.util.regex.*;` or `import java.util.regex.Pattern;` — Succeeds because you explicitly import the sub-package or the exact class.

Example showing the correct import:

```java
import java.util.regex.Pattern;

public class UsePattern {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("AB");
		System.out.println(p);
	}
}
```

If you instead wrote `import java.util.*;` and tried to use `Pattern`, the compiler will say `cannot find symbol: class Pattern`.

### 3.3 Takeaway summary (exam/interview-ready)

- You do NOT need to import `java.lang.*` — those classes are always available.
- You do NOT need to import classes that live in the same (unnamed) package / directory.
- Wildcard imports are not recursive: `import pack.*;` only exposes classes directly inside `pack`, not inside `pack.subpack`.
- To use classes inside a sub-package you must either import that sub-package explicitly (e.g., `import pack.subpack.*;`) or import the exact class (e.g., `import pack.subpack.ClassName;`).

These are common Java certification (OCAJP) and interview questions — memorize the rule "packages are not recursive" and you'll avoid the most frequent traps.

## 4 Class-Level Access Modifiers — public vs default (package-level)

This topic explains class-level access modifiers in Java, focusing on the difference between `public` and default (package-private) for top-level classes, which modifiers are permitted on top-level vs inner classes, and how visibility changes across package boundaries.

### 4.1 Overview of class-level modifiers

- Modifiers inform the compiler/JVM about a class's visibility and special behavior (inheritance rules, floating-point semantics, etc.).
- For top-level classes (those declared directly in a `.java` file) the commonly allowed modifiers are:
  - `public`
  - default (no modifier — package-private)
  - `abstract`
  - `final`
  - `strictfp` (strict floating-point semantics)
- For inner (nested) classes declared inside another class, three additional modifiers are permitted:
  - `private`
  - `protected`
  - `static`

> Note: newer Java versions introduce additional modifiers (for example `sealed`/`non-sealed`), but the list above covers the classic interview/certification surface.

### 4.2 The `public` modifier

- Meaning: a `public` top-level class has no visibility restrictions — it is accessible from any other class in any package.
- Usage requirement: when you use a `public` class from a different package you must import it (or use its fully-qualified name).

Example (public class in package `pack1`, used from `pack2`):

```java
// File: pack1/A.java
package pack1;

public class A {
	public void hello() { System.out.println("A.hello"); }
}

// File: pack2/B.java
package pack2;

import pack1.A;

public class B {
	public static void main(String[] args) {
		A a = new A();
		a.hello();
	}
}
```

Compiling and running `B` works because `A` is `public` and imported into `pack2`.

### 4.3 The default modifier (package-private)

- Meaning: a top-level class declared without an access modifier (for example `class A { ... }`) has default (package-private) access.
- Accessibility: package-private classes are visible only to other classes in the same package. They cannot be accessed from classes in other packages.

Example (default class in `pack1` and attempted access from `pack2`):

```java
// File: pack1/A.java
package pack1;

class A { // default (package-private)
	void hello() { System.out.println("A.hello"); }
}

// File: pack2/B.java
package pack2;

import pack1.A; // attempt to import a package-private class

public class B {
	public static void main(String[] args) {
		A a = new A(); // compile-time error: A is not public in pack1; cannot be accessed from outside package
	}
}
```

Compiling `B.java` will produce an error similar to:

```
error: A is not public in pack1; cannot be accessed from outside package
```

However, another class located inside `pack1` (for example `pack1.Test`) can access `A` without any import because they share the same package.

### 4.4 Quick access summary

| Modifier | Accessible within same package? | Accessible from external packages? | Key trait |
|---|:---:|:---:|---|
| public | Yes | Yes (requires import or fully-qualified name) | Global visibility |
| default (no modifier) | Yes | No | Package-private; restricted to same package |

Practical tips:
- Use `public` for API classes that other packages must use.
- Use default/package-private to hide implementation helpers that should remain internal to a package.
- For nested classes choose `private`/`protected`/`public`/`static` depending on intended visibility and lifecycle.

## 5 Abstract methods — meaning, use-cases, syntax rules and class relationship

This topic explains what `abstract` means in Java, why abstract methods are useful in software design, the exact syntax rules the compiler enforces, and the relationship between abstract methods and their enclosing classes.

### 5.1 What does "Abstract" mean?

- In plain English "abstract" means incomplete or not fully specified. In Java, an `abstract` method declares a method signature without providing an implementation (no method body).
- Targets: the `abstract` keyword can be applied to classes and methods. There is no such thing as an abstract variable.

Example (method declaration only):

```java
public abstract void m1(); // declaration, no body
```

### 5.2 Why we need abstract methods (real-world use-cases)

- Use when you know "what" should be done but not "how" — the concrete implementation depends on subclasses.
- Common examples:
  - Vehicle base class: `getNumberOfWheels()` — Bike, Car, Auto provide different answers.
  - Fruit base class: `getTaste()` — Mango (sweet), Lemon (sour).
  - Loan base class: `getInterestRate()` — HomeLoan, CarLoan, PersonalLoan implement different computations.

Example (Vehicle):

```java
abstract class Vehicle {
	public abstract int getNumberOfWheels();
}

class Bike extends Vehicle {
	public int getNumberOfWheels() { return 2; }
}

class Car extends Vehicle {
	public int getNumberOfWheels() { return 4; }
}
```

### 5.3 Abstract method syntax rules (exam-critical)

- Valid abstract method declaration:

```java
public abstract void m1(); // OK — ends with semicolon, no body
```

- Valid concrete method:

```java
public void m1() { }
```

- Invalid: abstract method with a body (compiler error)

```java
public abstract void m1() { } // ❌ invalid: "abstract methods cannot have a body"
```

- Invalid: concrete method without body (compiler error)

```java
public void m1(); // ❌ invalid: "missing method body, or declare abstract"
```

Compiler messages to expect:
- If you provide a body for an abstract method: "abstract methods cannot have a body"
- If you end a non-abstract method signature with `;`: "missing method body, or declare abstract"

### 5.4 Class relationship rule

- Rule: If a class contains at least one abstract method, the class itself must be declared `abstract`.

Incorrect example (will not compile):

```java
class Test {
	public abstract void m1(); // ERROR: class must be abstract
}
```

Correct example:

```java
abstract class Test {
	public abstract void m1();
}
```

If you forget to declare the class `abstract`, the compiler will complain and fail the build.

### 5.5 Summary cheat sheet

- Abstract methods: declaration only, no body — must end with a semicolon.
- Use abstract methods when implementation depends on concrete subclasses.
- Any class that declares an abstract method must itself be declared abstract.

---

If you'd like, I can now add a small example Java project inside the repository that demonstrates abstract classes and methods, compile it, and show the `javac` output and `java` runtime demonstration.

## 6 Abstract classes — definition, rules, and instantiation limits

This topic continues from abstract methods and explains abstract classes: what they are, why Java restricts direct instantiation, the relationship between abstract methods and abstract classes, and the special case where a class is abstract with no abstract methods.

### 6.1 What is an abstract class?

- An abstract class is a class declared with the `abstract` keyword that represents an incomplete or partial implementation — a blueprint for related subclasses.
- Syntax example:

```java
abstract class Vehicle { /* partial implementation or declarations */ }
```

- Instantiation rule: you cannot create an object of an abstract class. Attempting `new Vehicle()` will cause a compile-time error.

### 6.2 Core relationship: methods vs classes

- Rule: If a class declares one or more abstract methods, the class itself must be declared `abstract`.

Illegal example (won't compile):

```java
class Car {
	public abstract void breakSystem(); // compile error: class must be abstract
}
```

Correct form:

```java
abstract class Car {
	public abstract void breakSystem();
}
```

Reason: an abstract method is a method without an implementation; therefore the containing class is incomplete and must be marked abstract so Java prevents direct instantiation.

### 6.3 Reverse scenario: abstract class with no abstract methods

- Rule: A class may be declared `abstract` even if it contains zero abstract methods — this is legal and common in frameworks.

Example:

```java
abstract class DatabaseConfig {
	public void connect() { System.out.println("Connecting..."); }
	public void disconnect() { System.out.println("Disconnected."); }
}
```

- Why do this? Declaring a class abstract (even with only concrete methods) is a design decision to prevent direct instantiation and force subclassing. A real-world example is `HttpServlet` in Java web APIs.

### 6.4 Who provides the code? (subclass responsibilities)

- Because abstract classes cannot be instantiated, subclasses are responsible for providing implementations for any inherited abstract methods.
- If a subclass fails to implement an inherited abstract method, the subclass must also be declared `abstract`.

Example:

```java
abstract class Parent {
	public abstract void doWork();
}

class Child extends Parent {
	public void doWork() { System.out.println("Working..."); }
}

// If Child didn't implement doWork(), then Child must be declared abstract as well.
```

### 6.5 Summary table

| Code scenario | Class type required | Instantiation allowed? |
|---|---:|:---:|
| Contains ≥ 1 abstract method | Must be `abstract` | No |
| Contains 0 abstract methods | Can be concrete or `abstract` | Only concrete classes can be instantiated |

---

If you want, I can create small example files that demonstrate each rule (illegal case, legal case, abstract-but-no-abstract-methods) and compile them here to show the exact compiler messages and runtime behavior. Tell me which examples to generate and I will run them.

## 7 Abstract Class vs Abstract Method — responsibilities and enforcement

This topic directly compares abstract methods and abstract classes and explains the strict parent/child responsibilities enforced by the Java compiler. The section emphasizes the "2-choice fix" a child class has when inheriting abstract behavior and the architectural purpose of declaring methods abstract in a parent class.

### 7.1 Core conceptual difference

- Abstract Method: declares *what* should be done but provides no implementation. Syntax: a declaration that ends with a semicolon and no body.

```java
public abstract void m1(); // abstract method: no body
```

- Abstract Class: a class declared with `abstract` that represents a partial implementation or blueprint. You cannot instantiate it directly (`new AbstractClass()` is illegal).

### 7.2 Child class inheritance rules — the 2-choice fix

Consider a parent with two abstract methods:

```java
abstract class Test {
	public abstract void m1();
	public abstract void m2();
}
```

If a child `SubTest` extends `Test` but implements only `m1()`, the compilation will fail with a message like:

```
SubTest is not abstract and does not override abstract method m2()
```

To resolve this, the child has two choices (the "2-choice fix"):

- Choice A — Implement every abstract method:

```java
class SubTest extends Test {
	public void m1() { /* ... */ }
	public void m2() { /* ... */ }
}
```

This makes `SubTest` a concrete class and compilation succeeds.

- Choice B — Declare the child class abstract (pass the responsibility down):

```java
abstract class SubTest extends Test {
	public void m1() { /* ... */ }
	// m2() remains unimplemented, so SubTest must be abstract
}
```

Now the obligation to implement `m2()` moves to whatever concrete subclass eventually extends `SubTest`.

### 7.3 The architectural advantage (why force methods abstract?)

- If the parent does not declare a method abstract, child classes are free to override it but are not required to. Declaring a method abstract enforces a contract: every concrete subclass must provide an implementation.

- Example (Vehicle enforcement):

```java
abstract class Vehicle {
	public abstract int getNoOfWheels(); // mandatory contract
}

class Bus extends Vehicle {
	public int getNoOfWheels() { return 6; }
}

class Auto extends Vehicle {
	public int getNoOfWheels() { return 3; }
}
```

By marking `getNoOfWheels()` abstract in `Vehicle`, the compiler guarantees structural consistency: every concrete vehicle type must supply its wheel count. This prevents accidental omission and enforces a design rule at compile time rather than relying on documentation or code review.

---

If you want, I can now create example files for the illegal case (child missing an implementation), the two-choice fixes, and compile them to show the exact compiler messages. Which examples should I generate and compile? 

## 8 Member-level access modifiers — precedence rule, public, default, private

This topic covers member-level access modifiers (fields and methods), explains the precedence rule (class visibility vs member visibility), lists the three core member modifiers in detail, and provides industry-standard best practices and a cheat-sheet. Numbering follows your requested convention: 8, 8.1, 8.2, 8.3.

### 8.1 The Precedence Rule (Class vs. Member Visibility)

- Power rule: a member's modifier only matters if its enclosing class is visible to the caller. If the class itself is not accessible (for example it's package-private), then no member inside it can be accessed from outside that package — even if the member is declared `public`.
- Consequence: marking a method `public` inside a package-private class does not expose it to other packages.

Fix: mark the top-level class `public` as well as the member, or use a different packaging approach.

Example (conceptual):

```java
// File: pack1/Hidden.java
package pack1;

class Hidden { // package-private
	public void exposed() { System.out.println("exposed"); }
}

// File: pack2/Test.java
package pack2;
import pack1.Hidden;

public class Test {
	public static void main(String[] args) {
		// new Hidden(); // compile error: Hidden is not public in pack1; cannot be accessed from outside package
	}
}
```

### 8.2 The three core member modifiers

A. `public`
- Visibility: global (accessible from any package, subject to module rules).
- Typical use: public API methods and constants.

B. default (package-private)
- Visibility: only classes within the same package can access the member.
- Typical use: package-level helpers and implementation collaboration inside a package.

C. `private`
- Visibility: only inside the declaring class. Not visible to other classes, not even subclasses.
- Typical use: data members and internal helper methods to enforce encapsulation.

Examples:

```java
// pack1/Employee.java
package pack1;
public class Employee {
	// data hidden
	private double salary;

	// public API
	public double getSalary() { return salary; }

	// package-private helper
	void audit() { /* package-only */ }
}
```

```java
// pack2/Client.java
package pack2;
import pack1.Employee;

public class Client {
	public static void main(String[] args) {
		Employee e = new Employee();
		System.out.println(e.getSalary()); // OK
		// e.audit(); // compile error: audit() is not public in Employee; cannot be accessed from outside package
	}
}
```

### 8.3 Industry-standard best practices and cheat-sheet

- Fields should generally be `private` to protect internal state. Expose controlled access via `public` getters/setters when necessary.
- Methods that form the public service/API should be `public` so external components have a clear entry point.
- Use package-private (no modifier) for classes and members that should be shared only within the package.

Cheat-sheet:

| Modifier | Visibility boundary | Recommended for |
|---|---|---|
| public | Global (any package) | Methods (public API), constants |
| default (no keyword) | Same package only | Package-level utilities/internal cooperation |
| private | Same class only | Fields (data hiding), internal helper methods |

---

If you want, I can now create and compile the example files above (the precedence rule and public/default/private examples) and paste the exact `javac` output and any runtime output. Which examples should I run? 

