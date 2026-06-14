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
|---|---|---|---|
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
|---|---|---|
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


## 9 Protected access — same-package vs outside-package (detailed)

### 9.1 Core definition (concise formula)

Durga Sir's handy formula captures the compiler behaviour succinctly:

protected = default + inheritance-from-outside-package

In words:
- Within the same package, `protected` behaves exactly like default (package-private): any class in the package can access the member.
- From a different package, `protected` only permits access through subclassing — and even then the compiler enforces a strict reference-type rule.

### 9.2 The strict object-reference rule (exam-critical)

When accessing a `protected` member from another package, Java requires that the reference used to access the member is of the subclass type (or a reference whose compile-time type is the subclass). The runtime object alone is not enough — the compiler looks only at the reference type.

Consequence:
- From outside the package, a parent-type reference (even if pointing to a child object) cannot be used to call the `protected` member — compile-time error.

### 9.3 Scenario A — Same package (pack1)

Both classes in the same package: unrestricted access to `protected` members.

```java
package pack1;

public class A {
	protected void m1() { System.out.println("A Class protected method"); }
}

package pack1;

public class B extends A {
	public static void main(String[] args) {
		A a = new A();   a.m1();   // OK: parent ref, parent object
		B b = new B();   b.m1();   // OK: child ref, child object
		A a1 = new B();  a1.m1();  // OK: parent ref, child object
	}
}
```

All three calls compile and run because package visibility allows any class in `pack1` to access `m1()`.

### 9.4 Scenario B — Outside package (pack2) — the trap

Now `A` stays in `pack1` and `B` moves to `pack2` and extends `A`. Access rules tighten.

```java
// File: pack1/A.java
package pack1;
public class A {
	protected void m1() { System.out.println("A Class protected method"); }
}

// File: pack2/B.java
package pack2;
import pack1.A;

public class B extends A {
	public static void main(String[] args) {
		A a = new A();      a.m1();   // ❌ Compile error: cannot access protected member via parent reference

		B b = new B();      b.m1();   // ✅ OK: child reference in subclass

		A a1 = new B();     a1.m1();  // ❌ Compile error: reference type is A (parent)
	}
}
```

Why the failures? From `pack2` the compiler allows access to `m1()` only through a reference that is a `B` (or a subclass of `B`) because the accessing code is located outside `pack1`. The reference `a` and `a1` are typed as `A`, so the compile-time check blocks the call.

### 9.5 Quick rules checklist

- Within same package: any class can access `protected` members (same as default/package-private).
- Outside package:
  - Access allowed only in subclasses (i.e., code that is inside the child class or its subclasses).
  - The reference used at the call site must be of the child type (or its subtype) — parent-type references are disallowed even if they point to child objects.

### 9.6 Why the compiler enforces reference-type checks

The compiler enforces access based on compile-time types to keep access control static and predictable. Allowing runtime type checks would complicate visibility rules and could break encapsulation assumptions across packages.

### 9.7 Summary table (concise)

| Access location | Reference variable type used | Allowed to access protected member? |
|---|---|---|
| Within same package | Parent (A) or Child (B) | ✅ Yes — any reference works |
| Outside package | Child type (B) only | ✅ Yes — but only when called through child reference |
| Outside package | Parent type (A) | ❌ No — compile-time error |

### 9.8 Exam tips and common pitfalls

- Don't confuse the runtime object with the compile-time reference type. The compiler checks the reference type only.
- Remember the formula: protected = default + inheritance-from-outside-package. Use it as a quick memory aid.
- When moving classes between packages during refactoring, re-check all calls to `protected` members — many will break if they relied on package access.
- If you need wider access across packages, consider making the member `public` or provide a `public` accessor method.

### 9.9 Example variations / edge cases

- Access from a non-subclass in another package: always disallowed for `protected` members.
- Access from a subclass that is nested or an inner class: inner-class rules still respect the same-package vs outside-package distinctions based on the containing class's package.

### 9.10 Short checklist for a quick sanity test

1. Identify the package of the class declaring the `protected` member.
2. Identify the package of the accessing code.
3. If same package — allowed. If different package — ensure the accessing code lives in a subclass and the call site uses a child-type reference.

---

If you want, I can also add runnable example files to the repository (`pack1/A.java`, `pack2/B.java`) and compile them to show the exact `javac` errors and the successful case for `b.m1()`. Which would you prefer me to create and run next?


## 10 Modifier visibility matrix — public, protected, default, private (Durga Sir visual summary)

### 10.1 The definitive visibility matrix

This table reproduces Durga Sir's structural boundary matrix and shows, for each access location, whether a member with the listed modifier is visible.

| Location / Scope Layer | public | protected | default | private |
|---|---|---|---|---|
| Within the same class | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| From child class (same package) | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No |
| From non-child class (same package) | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No |
| From child class (outside package) | ✅ Yes | ✅ Yes (child reference only!) | ❌ No | ❌ No |
| From non-child class (outside package) | ✅ Yes | ❌ No | ❌ No | ❌ No |

Notes on the table:
- A checkmark means the member is accessible from that location assuming the host class itself is visible to the caller.
- For `protected` from an outside package, the additional constraint "child reference only" refers to the compile-time reference-type rule (you must access the member through a reference whose declared type is the subclass).

### 10.2 Crucial scope extensions explained

- The Most Accessible — `public`
	- No restrictions (other than the host class being visible). Public members are accessible from any package and any class.

- The Package Extension — `default` vs `protected`
	- `default` (no modifier): visibility is strictly confined to the declaring package. No external package can access it.
	- `protected`: inside the declaring package it behaves like `default`. Outside the package it permits access only to subclasses — and still obeys the reference-type restriction (see Section 9).

- The Most Restrictive — `private`
	- Visibility is limited to the declaring class only. Not visible to any other class, not even subclasses or other classes in the same package.

### 10.3 Final scope ranking formula (memorize this)

Durga Sir's compact inequality captures the visibility ordering you should remember for exams and design decisions:

$$\text{private} < \text{default} < \text{protected} < \text{public}$$

(Read: private is the most restrictive; public is the most permissive.)

### 10.4 Core blueprint recap (practical guidelines)

- For instance (field) variables: prefer `private` to enforce data hiding and encapsulation. Expose controlled access via `public` getters/setters when necessary.
- For service/API methods: prefer `public` for the methods you intend other packages to call. Keep helpers package-private or `private` depending on the intended audience.
- Use `protected` sparingly and intentionally: it is primarily for extension points designed to be used by subclasses (remember the outside-package child-reference rule).

### 10.5 Quick engineering checklist

1. If the class is an implementation detail for a package, use package-private (default) visibility for the class and `private` for its internal fields.
2. If subclasses must override or use a method across packages, use `protected` and document the extension contract clearly.
3. If the method or field is part of your public API, mark it `public` and ensure the host class is `public` as well.

---

## 11 Interfaces (requirement specification) — Java

An interface in Java is a pure requirement specification: it declares the services a type must provide but contains no raw implementation (no method bodies for abstract methods).

- Keyword: declare an interface using the `interface` keyword (not `class`).

Example:

```java
interface Interf {
    void m1();
    void m2();
}
```

- Implicit modifiers: every method declared in an interface is implicitly `public` and `abstract` (until Java 8 default/static additions). Even if you omit `public abstract`, the compiler treats the methods as such.

### 11.1 The implementation phase (`implements`)

A concrete class provides the implementation for an interface using the `implements` keyword.

Example (incorrect):

```java
// File: ServiceProvider.java
class ServiceProvider implements Interf {
    void m1() {
        System.out.println("m1 execution");
    }
}
```

If you compile this with `javac ServiceProvider.java` the compiler will reject it and produce two compilation errors.

#### 11.1.1 Error 1 — Decreasing visibility violation

- Cause: Method overriding rules forbid reducing visibility. `m1()` inside `Interf` is implicitly `public`. In `ServiceProvider` the developer wrote `void m1()` which is package-private (default), a narrower visibility than `public`.
- Compiler message (example):

```
error: m1() in ServiceProvider cannot implement m1() in Interf; attempting to assign weaker access privileges; was public
```

- Fix: Mark the implementing method `public`:

```java
public void m1() { ... }
```

#### 11.1.2 Error 2 — Missing implementation routines

- Cause: By declaring `implements Interf`, the class promises to implement all abstract methods. Here `m2()` is not implemented.
- Compiler message (example):

```
error: ServiceProvider is not abstract and does not override abstract method m2() in Interf
```

- Fixes (two choices):
  - Choice A — Implement all interface methods:

```java
class ServiceProvider implements Interf {
    public void m1() { System.out.println("m1"); }
    public void m2() { System.out.println("m2"); }
}
```

  - Choice B — Make the class abstract and leave some methods unimplemented:

```java
abstract class ServiceProvider implements Interf {
    public void m1() { System.out.println("m1"); }
    // m2() remains abstract and will need to be implemented by a concrete subclass
}
```

Summary blueprint:

- Interface methods are implicitly `public abstract` (unless explicitly declared `default` or `static` in modern Java).
- An implementing class must declare the overridden methods `public` (cannot reduce visibility).
- The implementing class must either implement every interface method or be declared `abstract`.

---

## 11.2 Contrast: Interfaces in Java vs C++

This short comparison shows how the two languages model "interfaces" and the important differences to keep in mind.

- Syntax / language feature
  - Java: has an explicit `interface` keyword and dedicated semantics for interfaces.
  - C++: has no `interface` keyword. The equivalent is a class with only pure virtual functions (a pure abstract class).

- Declaration and visibility
  - Java: interface methods are implicitly `public` (unless `private`/`static`/`default` are used in newer Java versions). Implementations must be `public`.
  - C++: pure virtual functions can be `public`, `protected`, or `private` in the abstract class. Access control is flexible and affects how the interface is used by clients.

- Fields / state
  - Java: interfaces cannot hold instance state. They may declare constants (public static final fields). Since Java 8, interfaces can have `static` and `default` methods (with bodies), but still no instance fields.
  - C++: abstract classes can have member variables, constructors, and non-virtual helper methods. That means a C++ "interface" can carry state and implementation details if desired.

- Multiple inheritance
  - Java: a class may implement multiple interfaces (multiple inheritance of type). Prior to Java 8 there was no multiple inheritance of behavior; since Java 8 `default` methods allow behavior in interfaces, and Java defines conflict-resolution rules (class methods win, otherwise the most specific interface's default wins, or the implementing class must override).
  - C++: supports multiple inheritance of classes (including implementation). This is more powerful but can introduce complexity such as the diamond problem; C++ offers virtual inheritance to mitigate it.

- Default / provided implementations
  - Java: interfaces may provide `default` and `static` method implementations (Java 8+). This lets interfaces evolve without immediately breaking implementors.
  - C++: an abstract class can provide concrete implementations for some methods directly; derived classes inherit them normally.

- Constructors and destructors
  - Java: interfaces cannot have constructors. They cannot be instantiated on their own.
  - C++: abstract classes can have constructors and destructors. When using the abstract-class-as-interface pattern, always provide a `virtual` destructor to ensure proper cleanup through base pointers:

```cpp
struct IInterface {
    virtual ~IInterface() = default; // important
    virtual void m1() = 0;
};
```

- Overriding and visibility rules
  - Java: you cannot reduce visibility when implementing/overriding (`public` in interface must be `public` in the class).
  - C++: access specifiers may differ in derived classes; a pure virtual function can be declared `protected` in the base to hide it from public API while still forcing derived classes to implement it.

- When to use which
  - Java: use `interface` to define API contracts, especially when many unrelated classes must share a type. Prefer interfaces for purely behavioral contracts and use abstract classes when you need shared state or common implementation.
  - C++: use a pure virtual abstract class for interface-like contracts. If no shared state is required, keep it minimal (only pure virtual functions) and provide a `virtual` destructor. Use multiple inheritance cautiously and prefer composition when possible.

Key practical notes

- Java interfaces are a first-class language feature with clear rules about visibility and implementation obligations.
- In C++, interfaces are a design pattern implemented with abstract classes; they can do more (state, constructors), but that flexibility brings responsibility (manage object lifetime, consider virtual destructors, and handle multiple inheritance issues).

---

## 11.3 Difference: Abstract class vs Interface

This subsection summarizes the practical and language-level differences between an `abstract` class and an `interface` in Java.

- Purpose
  - Abstract class: used when you want to share common state or behaviour and provide partial implementation to subclasses.
  - Interface: used to define a pure contract (type) that unrelated classes can implement.

- Syntax
  - Abstract class: `abstract class A { ... }` — can contain fields, constructors, concrete and abstract methods.
  - Interface: `interface I { ... }` — primarily abstract methods (until Java 8+ where `default` and `static` are allowed), and constants.

- State and constructors
  - Abstract class: can have instance fields and constructors; useful to initialize shared state.
  - Interface: cannot have instance fields; only `public static final` constants. No constructors.

- Method implementations
  - Abstract class: can provide concrete method implementations and abstract methods.
  - Interface: prior to Java 8 interfaces had no implementations; since Java 8 they can have `default` and `static` methods with bodies, but still cannot hold instance state.

- Multiple inheritance
  - Abstract class: a class can extend only one class (single inheritance). Use abstract classes when you need shared implementation/state.
  - Interface: a class can implement multiple interfaces — interfaces support multiple inheritance of type.

- When to prefer which
  - Prefer `interface` when you need a pure contract that many unrelated classes should implement.
  - Prefer `abstract` class when you want to provide common code or fields to closely related classes and you control the class hierarchy.

- Example (abstract class):

```java
abstract class Animal {
    protected String name;
    public Animal(String name) { this.name = name; }
    public abstract void speak();
    public void log() { System.out.println(name + " exists"); }
}
```

- Example (interface):

```java
interface Flyer {
    void fly(); // implicitly public abstract
    static int MAX_ALTITUDE = 10000; // public static final
}
```

- Key practical rule: if you need both shared state/constructor logic and a contract, consider using an abstract class (or composition) since interfaces cannot hold instance state.

---

## 12 Data Hiding

Data Hiding is the practice of locking your internal data representations so that external code cannot access, read, or modify them directly. The main goal is to protect the internal state of an object and force all access through controlled APIs that enforce validation, invariants, and security checks.

### 12.1 Real-world analogies (video highlights)

- Gmail inbox
  - When you reach `gmail.com` you don’t get direct access to the raw email database. Authentication and authorization gates sit between the user and the stored data. Only after correct credentials are presented is the inbox data revealed.

- Bank balance
  - You cannot open a bank’s database file and read balances. The bank hides the balance behind authentication (user id, password, OTP). Access is provided only through validated service methods.

These analogies map directly to class design: internal fields are hidden, and public service methods provide validated access.

### 12.2 The programmatic approach (how to implement it)

The canonical Java technique for Data Hiding is simple:

- Declare instance fields `private`.
- Expose controlled access via `public` methods (getters, setters, service methods) that perform validation and enforce invariants.

#### 12.2.1 Minimal example

```java
public class Account {
    // Data hidden from external code
    private double balance;

    public Account(double initial) {
        if (initial < 0) throw new IllegalArgumentException("Negative initial balance");
        this.balance = initial;
    }

    // Controlled read access with validation/audit
    public double getBalance(String username, String password) {
        if (validate(username, password)) {
            // possibly log/audit access
            return this.balance;
        }
        throw new SecurityException("Unauthorized access denied.");
    }

    // Controlled mutation
    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("amount must be > 0");
        this.balance += amount;
    }

    public void withdraw(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("amount must be > 0");
        if (amount > this.balance) throw new IllegalStateException("Insufficient funds");
        this.balance -= amount;
    }

    private boolean validate(String user, String pass) {
        // validation logic: check credentials, roles, etc.
        return true;
    }
}
```

Why this works: If `balance` were `public`, anyone could set it directly (`a.balance = -50000.0`) and circumvent validation. Marking fields `private` forces external code to use the API methods that contain checks.

### 12.3 Security and correctness benefits

- Encapsulation and invariants: Private fields let the class enforce invariants (for example, balance >= 0) centrally.
- Auditing and logging: Accessor methods can log accesses, throttle requests, or check permissions.
- Easier evolution: Implementations can change internal representation (for example, switch to BigDecimal) without altering public APIs.
- Defense-in-depth: Validation in the class prevents accidental or malicious state corruption.

### 12.4 Implementation patterns and best practices

- Prefer private fields; provide the minimal public API required.
- Validate inputs early and fail fast (IllegalArgumentException, SecurityException).
- Use immutable objects where possible. If an object is immutable, many security concerns disappear.
- Avoid returning internal mutable objects directly: return defensive copies.

Example (defensive copy):

```java
public class Person {
    private final Date birthDate; // Date is mutable

    public Person(Date birthDate) {
        this.birthDate = new Date(birthDate.getTime()); // defensive copy
    }

    public Date getBirthDate() {
        return new Date(birthDate.getTime()); // return defensive copy
    }
}
```

- Use `final` for fields that should not be reassigned after construction.
- When exposing collections, prefer unmodifiable views or copies:

```java
public List<String> getTags() {
    return Collections.unmodifiableList(new ArrayList<>(tags));
}
```

- Use package-private helpers for test-only access instead of making fields public just for tests.
- Consider access control annotations or security frameworks for complex authorization (Spring Security, JAAS) rather than ad-hoc checks.

### 12.5 Edge cases and common pitfalls

- Over-exposing via setters: Providing public setters for every field defeats data hiding. Expose only mutations you intend callers to perform.
- Returning internal mutable references: Returning a reference to an internal List/Map/Date allows callers to mutate internal state. Use defensive copies/unmodifiable wrappers.
- Relying solely on client discipline: Data hiding requires enforcement by language features (private) and code reviews — don't rely on callers to be careful.
- Serialization risk: When using serialization frameworks, private fields may still be set during deserialization. Ensure validation runs after deserialization (readObject, @PostConstruct checks).
- Reflection: Reflection can access private fields (AccessibleObject#setAccessible) — restrict reflective access in security-sensitive environments or use SecurityManager policies (where applicable).

### 12.6 Quick checklist (practical)

- Are all internal fields declared `private` unless there's a compelling reason not to? ✅
- Do your public methods validate inputs and enforce invariants? ✅
- Do you return defensive copies for mutable internal objects? ✅
- Do you avoid unnecessary setters and expose only required mutations? ✅
- Do constructors validate initial state and set fields `final` where possible? ✅

---

Summary: Data Hiding protects internal state by declaring fields private and exposing carefully validated APIs. It improves security, correctness, and maintainability. Follow the defensive-copy, immutability, and minimal-API principles to implement it correctly.

(End of appended material.)


## 13 Abstraction

Abstraction is the process of hiding internal execution mechanics and exposing only the essential services or interfaces to the user. It focuses on what the system does rather than how it does it. Abstraction reduces complexity for users and clients by providing a simplified, stable surface for interaction.

### 13.1 Definition and conceptual model

- Definition: Concealing internal technical execution details while exposing clean service hooks and interfaces.
- Conceptual diagram:

		[ End user / client ]
							 |
		(Abstraction layer: GUI / API / Interface)
							 |
		[ Hidden internal implementation ]

### 13.2 The ATM analogy (video highlights)

- User interaction: The ATM screen shows simple options — Withdraw, Deposit, Transfer, Balance Inquiry.
- What the user does not see: database queries, backend service calls, hardware controller logic, the programming language used, or low-level error handling.
- The abstraction guarantees: a stable set of operations (the API) while the backend can be changed or optimized freely.

### 13.3 How to implement abstraction (programmatic techniques)

- Interfaces and abstract classes
	- Define a contract (API) via interfaces or abstract classes; expose only necessary methods.

- Graphical User Interfaces (GUIs)
	- Present a small, well-defined set of actions and hide the underlying control flow and implementation.

- APIs (REST, SOAP, RPC)
	- Provide service endpoints that accept defined inputs and return defined outputs; internals remain hidden behind the endpoint.

- Service layers and facades
	- Use a façade or service layer to translate client requests into internal calls; keep internal modules private to the service implementation.

### 13.4 Abstraction vs Data Hiding (structural difference)

- Data Hiding: protects internal state (fields) from direct access (private fields, defensive copies).
- Abstraction: protects internal implementation/behavior (how methods perform work) by providing a simplified interface.
- Short mnemonic: Data Hiding = "what you can't touch" (state). Abstraction = "what you don't need to know" (behavior/implementation).

### 13.5 Advantages of Abstraction

- Security: Hides internal endpoints, sensitive implementation details, and system architecture from outsiders.
- Easier enhancements / refactoring: Replace internal implementations without changing the external API or user experience.
- Maintainability & modularity: Clear separation between interface and implementation reduces coupling and improves testability.

### 13.6 Practical examples

- Java interface example (API contract):

```java
public interface PaymentProcessor {
		Receipt charge(CardInfo card, Money amount);
		boolean refund(TransactionId id);
}
```

Implementors can change how `charge` works (gateway, retries, batching) without clients knowing.

- Facade example:

```java
public class OrderServiceFacade {
		private final Inventory inventory;
		private final PaymentProcessor payments;

		public void placeOrder(Order o) {
				// internal orchestration: inventory check, reserve, payment, shipment
				// clients call one simple method and don't see the orchestration steps
		}
}
```

### 13.7 When abstraction fails / anti-patterns

- Leaky abstraction: when internal details leak through the interface (exceptions that expose implementation details, or performance characteristics tied to implementation).
- Over-abstraction: too many tiny interfaces or wrapper layers that make code hard to follow and degrade performance.

### 13.8 Quick checklist

- Does the public API present a minimal, stable surface? ✅
- Are implementation details (endpoints, credentials, internal paths) hidden from clients? ✅
- Can you replace or refactor internals without changing public signatures? ✅
- Are errors translated into API-level exceptions rather than leaking stack traces/implementation info? ✅

---

Summary: Abstraction simplifies the client's view by exposing essential operations while hiding the detailed implementation, increasing security, maintainability, and flexibility.

(End of appended material.)


## 14 Encapsulation

Encapsulation is the OOP principle that bundles data (state) and the methods that operate on that data into a single unit (a class). More precisely, encapsulation combines Data Hiding and Abstraction so a component both protects its internal state and exposes a controlled, simplified interface.

### 14.1 Compact definition and formula

- Definition: Encapsulation groups related fields and methods inside a class and enforces controlled access to the internals through well-defined APIs.
- Formula (Durga Sir's blueprint):

  Encapsulation = Data Hiding + Abstraction

  (Hide the state; expose a minimal, validated interface.)

### 14.2 Why encapsulation matters (conceptual benefits)

- Security: Prevents unauthorized or accidental state modification by external code.
- Maintainability: Changes to the internal representation don't force API consumers to change.
- Modularity: Each class owns its state and behaviour, limiting ripple effects during refactoring.
- Clear responsibility: The class is the single place to enforce invariants, validation, and auditing.

### 14.3 Canonical example — Account (structured and annotated)

```java
public class Account {
    // 1. DATA HIDING: internal state is private
    private double balance;

    // 2. CONSTRUCTION: validate initial state and set final fields where possible
    public Account(double initial) {
        if (initial < 0) throw new IllegalArgumentException("Negative initial balance");
        this.balance = initial;
    }

    // 3. ABSTRACTION: public API that hides implementation details and validates callers
    public double getBalance(String user, String pass) {
        if (!validate(user, pass)) throw new SecurityException("Access Denied");
        // Could add audit/logging here
        return this.balance;
    }

    public void deposit(double amount, String user, String pass) {
        if (!validate(user, pass)) throw new SecurityException("Access Denied");
        if (amount <= 0) throw new IllegalArgumentException("amount must be > 0");
        this.balance += amount;
    }

    public void withdraw(double amount, String user, String pass) {
        if (!validate(user, pass)) throw new SecurityException("Access Denied");
        if (amount <= 0) throw new IllegalArgumentException("amount must be > 0");
        if (amount > this.balance) throw new IllegalStateException("Insufficient funds");
        this.balance -= amount;
    }

    // 4. INTERNAL: validation is private and cannot be bypassed by external callers
    private boolean validate(String user, String pass) {
        return "admin".equals(user) && "secret".equals(pass);
    }
}
```

- Notes: The public methods form the class's external contract (abstraction); the private field and private validate() implement data hiding. Together they form an encapsulated component.

### 14.4 Key advantages (detailed)

- Maximized security: all state changes funnel through validated methods.
- Refactoring freedom: internals (data types, algorithms) can change as long as the public contract remains stable.
- Centralized invariants: checks like "balance >= 0" live in one place and cannot be forgotten across callers.
- Better testing: test the class via its public API and assert internal behaviour without exposing internals.

### 14.5 Primary disadvantage: performance overhead

- Extra method calls and validation logic add runtime cost vs direct field access.
- Increased code size and potential allocation for defensive copies or unmodifiable wrappers.

Performance trade-offs explained:
- Direct access (fastest): client reads the field directly from memory (no checks or stack frames).
- Encapsulated access (safer): client calls getter -> validation/audit -> return value (extra CPU + stack overhead).

### 14.6 Mitigation strategies (practical)

- Keep hot-path accessors lightweight: avoid expensive checks on extremely frequent reads; separate security checks from cheap reads when safe.
- Cache validated sessions / tokens: validate once and reuse a session token for subsequent accesses.
- Use immutable objects for frequently-read data: avoid defensive copies when the object is immutable.
- Inline or final small methods where JIT can optimize call overhead (let the JVM inline tiny getters).
- Profile before optimizing: only reduce encapsulation for validated, measured hotspots.

### 14.7 Antipatterns and overuse

- Over-encapsulation: wrapping every trivial field access with heavy validation even when unnecessary leads to needless complexity and latency.
- Exposing too many setters: providing public setters for all fields defeats encapsulation and moves invariants outside the class.
- Leaky encapsulation: exposing internal data structures (returning modifiable collections) or throwing implementation-specific exceptions that reveal internals.

### 14.8 Practical checklist (for design/review)

- Are fields private by default? ✅
- Do public methods validate inputs and enforce invariants? ✅
- Are mutable internals protected by defensive copies or unmodifiable views? ✅
- Have you avoided unnecessary setters? ✅
- Have you documented the public contract and kept it stable across refactors? ✅
- Have you considered performance and profiled the hot paths before changing encapsulation? ✅

---

Summary: Encapsulation unifies Data Hiding and Abstraction to produce components that are secure, maintainable, and modular. Be mindful of performance costs and apply mitigation strategies; favor correctness and API stability while profiling before making exception-based performance shortcuts.

(End of appended material.)


## 15 Tightly Encapsulated Class

A Tightly Encapsulated Class is a stricter form of encapsulation where every variable declared in the class is explicitly marked `private`. The definition is intentionally precise and binary: either 100% of the class's declared fields are private (tightly encapsulated) or they are not.

### 15.1 Compact definition and formula

- Definition: A class is tightly encapsulated iff every variable declared in that class is `private`.
- Formula:

  Tightly Encapsulated = 100% Data Hiding at the variable level

- Semicolon blueprint rule: The presence or absence of public getters/setters does not affect tight encapsulation — only the access modifier on the field matters.

### 15.2 Comparative code examples

- Scenario 1 — Tightly Encapsulated

```java
// File: Account.java
public class Account {
    private double balance; // ✅ private
    private int accountId;  // ✅ private

    public double getBalance() { return this.balance; }
}
// Status: Tightly Encapsulated
```

- Scenario 2 — NOT Tightly Encapsulated

```java
// File: Account.java
public class Account {
    private double balance; // ✅ private
    int accountId;          // ❌ package-private (not private)
}
// Status: NOT Tightly Encapsulated
```

### 15.3 Inheritance ripple effect (critical exam concept)

- Key rule: A subclass cannot be considered tightly encapsulated if any non-private field exists anywhere in its inheritance chain.

Example:

```java
class A {
    private int x = 10; // A is tightly encapsulated
}

class B extends A {
    int y = 20; // non-private -> B is NOT tightly encapsulated
}

class C extends B {
    private int z = 30; // C declares private z but inherits non-private y
}
// Result: A is tightly encapsulated; B and C are NOT tightly encapsulated
```

### 15.4 Structural rules and checklist

- Field rule: Every declared field in the class must be `private`.
- Method rule: Public getters/setters are allowed — they do not violate tight encapsulation by themselves.
- Inheritance rule: All parent classes must also be tightly encapsulated for a subclass to qualify.

Quick checklist

- Are all fields declared `private`? ✅
- Does the class inherit any non-private field from its ancestors? ❌ If yes, it's not tightly encapsulated.
- Is tight encapsulation required by design (security/contract)? Decide and document.

### 15.5 Summary reference table

| Encapsulation level | Variable requirement | Method requirement | Inheritance condition |
|---|---|---|---|
| Standard encapsulation | At least one private field | Public handlers allowed | No requirement on parents |
| Tightly encapsulated | 100% fields `private` | Methods can be any visibility | All ancestor classes must also be tightly encapsulated |

---

## 16 Inheritance

Inheritance lets a new class acquire properties (fields) and behaviors (methods) from an existing class automatically. In Java it's implemented with the `extends` keyword.

- Syntax: `class Child extends Parent { ... }`
- Terminology: the Parent class (superclass) provides members; the Child class (subclass) inherits them.

### 16.1 Primary objective: code reusability

- The main benefit of inheritance is to avoid repeating code. Shared fields and methods live in a common parent and are reused by children.
- It also models "is-a" relationships (for example, `Car` extends `Vehicle`).

### 16.2 The 4 object-reference scenarios (structural matrix)

Consider these classes:

```java
class P {
    public void m1() { System.out.println("Parent Method"); }
}

class C extends P {
    public void m2() { System.out.println("Child Method"); }
}
```

When creating objects and references, there are four important scenarios to remember.

- Scenario 1 — Parent reference, Parent object

```java
P p = new P();
p.m1(); // ✅ Valid
p.m2(); // ❌ Compile-time error: m2() not found in P
```

Rule: A parent reference only sees members declared in the Parent type.

- Scenario 2 — Child reference, Child object

```java
C c = new C();
c.m1(); // ✅ Valid (inherited)
c.m2(); // ✅ Valid (child local)
```

Rule: A child reference can call both inherited and local methods.

- Scenario 3 — Parent reference, Child object (polymorphic reference)

```java
P p1 = new C();
p1.m1(); // ✅ Valid (method exists in P)
p1.m2(); // ❌ Compile-time error: reference type P has no m2()
```

Rule: You can store a child object in a parent reference, but the compiler only permits calls to methods declared on the reference type (P).

- Scenario 4 — Child reference, Parent object (illegal)

```java
C c1 = new P(); // ❌ Compile-time error: incompatible types
```

Rule: A child reference cannot point to a plain parent object — the parent may lack child-specific members, so assignment fails.

### 16.3 Polymorphism and dynamic dispatch (short note)

- Dynamic dispatch: when a method is overridden in a subclass, a parent reference holding a child object will execute the child override at runtime. The compiler still checks the reference type for method existence, but the JVM dispatches to the overriding implementation.

Example:

```java
class P { public void hello() { System.out.println("P"); } }
class C extends P { @Override public void hello() { System.out.println("C"); } }
P p = new C();
p.hello(); // prints "C" due to dynamic dispatch
```

### 16.4 Best practices and common pitfalls

- Prefer composition over inheritance when you only need reuse of behavior without an "is-a" relationship.
- Avoid deep inheritance chains; they increase coupling and fragility.
- Mark methods `final` if subclasses must not override critical behavior.
- Use `protected` for members that are intentionally exposed to subclasses but not to other packages.
- Watch reference types: the compiler enforces visibility based on reference type, not runtime object.

### 16.5 Quick checklist

- Does the subclass actually represent an "is-a" relationship? ✅
- Are shared methods placed in a common parent to avoid duplication? ✅
- Are you using composition instead when appropriate? ✅
- Have you avoided exposing sensitive fields as non-private in parent classes (see tight encapsulation rules)? ✅

### 16.6 Summary table

| Reference type | Object type | Can call parent method? | Can call child method? | Compiles? |
|---|---|---|---|---|
| P (parent) | P (parent) | ✅ Yes | ❌ No | ✅ |
| C (child) | C (child) | ✅ Yes | ✅ Yes | ✅ |
| P (parent) | C (child) | ✅ Yes | ❌ No | ✅ |
| C (child) | P (parent) | — | — | ❌ (incompatible types) |

---

## 17 Inheritance — Comparative case study & Java API hierarchy

This section illustrates the practical power of inheritance using a real-world case study and then ties it to the native Java API hierarchy (Object and Throwable) as concrete proof of the pattern's value.

### 17.1 Comparative case study: Banking loan module

Problem: Build three loan profiles — HousingLoan, PersonalLoan, VehicleLoan — each with the same overall feature set.

- ❌ Approach A — Without inheritance
  - Developer writes each loan class independently.
  - HousingLoan: 300 methods
  - PersonalLoan: 300 methods
  - VehicleLoan: 300 methods
  - Total methods = 900
  - Consequences: massive duplication, large codebase, high maintenance and bug surface.

- ✅ Approach B — With inheritance
  - Identify commonality: 250 methods are identical across all three loans (customer tracking, logging, basic interest calculation, etc.).
  - Create a parent class `Loan` to hold the 250 common methods.
  - Each specific loan class implements only the 50 unique methods.

Math and outcome:

- Parent: 250 common methods
- Child classes: 50 unique methods × 3 = 150
- Total methods = 250 + 150 = 400

Result: Approach B reduces code from 900 → 400 methods, dramatically lowering development time and bug surface, and enabling a single-point fix for shared behavior.

### 17.2 Parent vs Child design matrix

- Parent class (superclass): place all generic, reusable methods and fields that are shared by a family of related types.
- Child class (subclass): place only specialized logic unique to that concrete variant.

Design rule: Keep the parent minimal but broad (shared core behaviors). Keep the child focused and specific (domain rules only).

### 17.3 Inheritance at scale: Java API native roots

To show inheritance's real-world value, look at the Java platform itself. The language authors use inheritance to centralize common behavior.

A. Throwable — the root for exceptions and errors

- Problem: Java has many exception/error types (ArithmeticException, NullPointerException, OutOfMemoryError, etc.). Many diagnostic and handling routines are identical.
- Solution: the `java.lang.Throwable` class defines the common behavior (stack trace capture, message handling, cause chaining, printing). All exception/error types inherit from `Throwable`, so the common code is written once.

B. Object — the universal root class

- In Java, `java.lang.Object` is the implicit superclass for every class.
- Common fundamental methods (defined once in Object):
  - `public String toString()`
  - `public boolean equals(Object o)`
  - `public int hashCode()`
  - `protected Object clone()` (where supported)
  - `public final Class<?> getClass()`
  - `public final void notify()/notifyAll()/wait()`

Why Object exists:
- Every runtime entity needs the same tiny set of universal operations (string representation, equality, hashing, identity). If inheritance didn't exist, these methods would need to be duplicated across thousands of classes in the core library.
- By centralizing these operations in `Object`, Java keeps the platform maintainable and consistent.

### 17.4 Practical takeaways

- Inheritance reduces duplication and centralizes shared behavior.
- Updating shared behavior is simple: change the parent and all children inherit the fix.
- Use inheritance when a clean "is-a" relationship exists and the shared behavior logically belongs to a parent type.
- Avoid inheritance when you only need delegation or composition; prefer composition in ambiguous or orthogonal reuse cases.

### 17.5 Summary checklist (Inheritance vs No Inheritance)

| Metric | System WITHOUT Inheritance | System WITH Inheritance |
|---|---|---|
| Code footprint | Massive duplication and bloat | Centralized shared code, smaller footprint |
| Architectural flow | Isolated, redundant modules | Shared hierarchy rooted at common templates (e.g., Loan/Throwable/Object) |
| Refactoring speed | Slow — change many files | Fast — change single parent to cascade updates |
| Bug surface area | High | Lower |

---

## 18 Types of Inheritance

This section lists the core inheritance patterns commonly discussed in OOP and explains which are supported by Java for classes. Each pattern includes a compact definition, a whiteboard-style blueprint, a short Java code sketch, and a note about Java support.

### 18.1 Single Inheritance (the baseline unit)

- Definition: A single child subclass directly inherits from a single parent superclass.

- Blueprint:

  Class A (Parent) <- Class B (Child)

- Code sketch:

```java
class A { }
class B extends A { } // B inherits directly from A
```

- Java support: Fully supported. This is the simplest and most common form of inheritance.

### 18.2 Multi-Level Inheritance (the family chain)

- Definition: A cascading chain where a class extends a child class, creating multiple downstream tiers (grandparent -> parent -> child).

- Blueprint:

  Class A (Grandparent) <- Class B (Parent) <- Class C (Child)

- Code sketch:

```java
class A { }
class B extends A { } // B inherits from A
class C extends B { } // C inherits from B (and transitively from A)
```

- Java support: Fully supported. Multi-level inheritance simply composes single-inheritance steps.

### 18.3 Hierarchical Inheritance (the fan-out hub)

- Definition: A single parent class is extended by multiple child classes (one-to-many).

- Blueprint (ASCII):

        Class A (Parent)
         /      |      \
    Class B  Class C  Class D

- Code sketch:

```java
class A { }
class B extends A { }
class C extends A { }
class D extends A { }
```

- Java support: Fully supported — it's multiple distinct single-inheritance relationships that share the same parent.

### 18.4 Multiple Inheritance (the diamond loop)

- Definition: A single child class attempts to inherit directly from more than one parent class simultaneously.

- Blueprint (ASCII):

    Class A (Parent  1)    Class B (Parent 2)
           \                /
            \              /
             Class C (Child)

- Code sketch (illegal in Java for classes):

```java
class A { }

class B { }
class C extends A, B { } // ❌ Not allowed for classes in Java
```

- Java support: STRICTLY BLOCKED for classes — Java does not allow a class to extend multiple classes at once because it would create ambiguity (the "diamond problem"). Note: similar behavior can be achieved using multiple interfaces.

### 18.5 Hybrid Inheritance (combined layouts)

- Definition: A mixed structure that combines two or more inheritance models (for example hierarchical + multiple), often producing diamond-like paths inside the overall graph.

- Blueprint (ASCII):

        Class A
        /     \
     Class B  Class C
        \     /
         Class D

- Code sketch: Hybrid forms that include direct multiple-parent links are not allowed for classes in Java.

- Java support: STRICTLY BLOCKED for classes when the hybrid contains multiple-inheritance paths. Use interfaces and composition to model such designs safely in Java.

### 18.6 Practical notes and guidance

- Java designers intentionally disallowed multiple-class inheritance to avoid ambiguity and complexity (the diamond problem). Instead Java supports multiple-type inheritance through interfaces: a class may implement many interfaces but extend only one class.
- To model complex reuse, prefer composition or interface-based design rather than attempting class-based multiple inheritance.

### 18.7 Summary table

| Inheritance Type | Number of Parents | Number of Children | Supported in Java (for Classes)? |
|---|---|---|---|
| Single | 1 | 1 | ✅ Yes |
| Multi-Level | 1 (per level) | 1 (per level) | ✅ Yes |
| Hierarchical | 1 | Multiple | ✅ Yes |
| Multiple | Multiple | 1 | ❌ No (causes ambiguity) |
| Hybrid | Mixed | Mixed | ❌ No (contains multiple inheritance paths) |

---

## 19 Why Java blocks Multiple Inheritance for Classes

This section explains the ambiguity (diamond) problem that motivated Java's decision to disallow multiple-class inheritance, why interfaces behave differently, how other languages (Python) handle it, and a common interview trap about `Object`.

### 19.1 The ambiguity (diamond) problem

- Multiple Inheritance for classes occurs when a single child class attempts to extend more than one parent class directly.

```java
// ❌ Not allowed in Java for classes
class C extends P1, P2 { }
```

- The ambiguity arises if both parents provide concrete implementations of the same method (for example `public void m1()`). If `C` inherits two concrete `m1()` implementations, the compiler and JVM cannot decide which implementation should run for `c.m1()` — this is the classic Diamond Problem.

- Java's choice: prevent the ambiguity at compile-time by disallowing comma-separated class extensions. This keeps the class inheritance model single-parented and simple.

### 19.2 Why interfaces are different (multiple inheritance of type)

- Interfaces declare method signatures (before Java 8) and therefore pass down contracts rather than concrete code. If two interfaces declare `void m1();`, there is no conflicting code to inherit—only the requirement that an implementing class provide `m1()`.

```java
interface P1 { void m1(); }
interface P2 { void m1(); }
interface C extends P1, P2 { } // legal: just combines contracts

class Impl implements C {
    public void m1() { /* single implementation */ }
}
```

- Since the concrete implementation is provided exactly once by the implementing class, there is no ambiguity at runtime.

- Java 8+: interfaces can provide `default` methods with bodies. If two interfaces provide conflicting default methods, the implementing class must resolve the conflict explicitly (by overriding the method or qualifying the interface method), so ambiguity is still controllable.

### 19.3 How other languages (Python) resolve the diamond

- Python supports multiple-class inheritance and resolves method dispatch using the Method Resolution Order (MRO).
- MRO is a deterministic ordering (C3 linearization) that the runtime uses to pick which parent's method to invoke when multiple implementations exist. The order is influenced by the order of parent classes in the class definition.

Example (Python semantics):

```python
class P1:
    def m1(self): print("P1")

class P2:
    def m1(self): print("P2")

class C(P1, P2):
    pass

c = C()
c.m1() # prints "P1" because P1 is listed first in C(P1, P2)
```

- Java intentionally avoids adding positional/algorithmic resolution rules for classes and instead keeps class inheritance single-rooted.

### 19.4 The interview trap: "every class extends Object"

- Trap claim: "If every class extends `java.lang.Object`, doesn't that mean a class extending another class has two parents (the explicit parent and `Object`)?" This is a confusion between multiple inheritance and multi-level inheritance.

- Clarification:
  - If you declare `class B { }` (no explicit `extends`), `B` implicitly extends `Object`.
  - If you declare `class A extends B {}`, `A`'s direct parent is `B` only. `A` does not directly extend `Object`; `Object` is an ancestor via the chain `Object -> B -> A`.
  - This is multi-level inheritance (single parent per level), not multiple inheritance.

### 19.5 Summary table

| Framework / Declaration | Example | Ambiguity risk | Java (classes) allowed? |
|---|---|---:|---:|
| Java class multiple-extends | `class C extends P1, P2 { }` | High (duplicate concrete methods) | ❌ No (compiler error) |
| Java interface multiple-extends | `interface C extends P1, P2 { }` | None (declarations only) | ✅ Yes (valid) |
| Python class multiple-extends | `class C(P1, P2):` | None (resolved by MRO) | ✅ Not applicable — Python allows it |

---

## 20 Cyclic Inheritance

Cyclic Inheritance is a scenario where a class attempts to inherit from itself, either directly or indirectly, creating a closed loop or "cycle" in the inheritance tree. Java strictly blocks cyclic inheritance at compile-time to prevent logically impossible and redundant inheritance relationships.

### 20.1 Core definition and problem statement

- **Definition**: Cyclic Inheritance occurs when a class inherits from itself (directly) or when a circular chain of parent-child dependencies forms (indirectly).
- **Design consequence**: Cyclic inheritance is logically impossible and redundant — the primary purpose of inheritance is to import and reuse code from an external parent class. Circular dependencies violate this principle and create infinite recursion hazards if allowed.
- **Java compiler stance**: Java strictly blocks cyclic inheritance at compile-time and throws the error:

```
error: cyclic inheritance involving [ClassName]
```

### 20.2 Direct Cyclic Inheritance (self-inheritance)

**Pattern**: A class explicitly declares that it extends itself.

**Code example** (illegal):

```java
// ❌ COMPILE-TIME ERROR!
class A extends A { }
```

**Compiler output** when attempting to compile:

```
error: cyclic inheritance involving A
```

**Why it's nonsensical**: The objective of inheritance is code reuse — bringing members from an external parent into the child class. Writing `class A extends A` means Class A is attempting to reuse its own members from itself, which are already natively available within its own body. This is completely redundant and adds no value. Self-members are always available locally; explicit inheritance from oneself provides zero additional functionality.

### 20.3 Indirect Cyclic Inheritance (circular chain)

**Pattern**: Two or more classes form a circular dependency chain, where each class extends the next in a way that eventually loops back to the starting class.

**Code example** (illegal):

```java
// ❌ COMPILE-TIME ERROR!
class A extends B { }
class B extends A { }
```

**Compiler output** when attempting to compile both classes:

```
error: cyclic inheritance involving A
error: cyclic inheritance involving B
```

**Why it's logically impossible**: Class A asserts that it needs all properties and methods from Class B. At the same time, Class B asserts that it needs all properties and methods from Class A. This creates a shared, codependent identity — two classes that depend on each other to define themselves, which is a logical dead-end. The inheritance hierarchy is supposed to form a directed acyclic graph (DAG); cycles violate this structure and make the inheritance model undefined.

### 20.4 Longer chains (generalized indirect cyclic inheritance)

**Pattern**: The cycle can involve more than two classes.

**Code example** (illegal):

```java
// ❌ COMPILE-TIME ERROR!
class A extends B { }
class B extends C { }
class C extends A { }   // completes the cycle A -> B -> C -> A
```

**Why the compiler rejects this**: The compiler performs a cycle-detection check during compilation. As it processes each class declaration, it traces the superclass hierarchy. If it ever finds that a class would eventually reach itself through the superclass chain, it halts with a cyclic-inheritance error.

### 20.5 Compiler cycle-detection mechanism

- **When checked**: Cyclic inheritance is detected at compile-time during the class declaration/loading phase.
- **Algorithm**: The compiler traces the superclass chain for each class and checks whether the chain ever loops back to the class itself.
- **Scope**: Cycles are detected at compile-time, before any code is executed. This prevents runtime reflection or classloading issues.

Example compiler session:

```bash
$ cat A.java
class A extends B { }
class B extends A { }

$ javac A.java
A.java:1: error: cyclic inheritance involving A
class A extends B { }
^
A.java:2: error: cyclic inheritance involving B
class B extends A { }
^
2 errors
```

### 20.6 Design rationale and solutions

- **Rationale for blocking cycles**: Inheritance is meant to model an "is-a" relationship and to enable code reuse. Cycles destroy both: they make the relationship circular and nonsensical, and they provide no code to inherit (both classes would be waiting for each other to define common methods).

- **Recommended solution when you encounter a cycle**:
  - **Merge into one class**: If two classes are so interdependent that they form a cycle, consider combining them into a single unified class.

Example (solution):

```java
// ❌ Before (circular and rejected by compiler)
class A extends B { int x; }
class B extends A { int y; }

// ✅ After (merged into one class)
class A {
    int x;
    int y;
}
```

- **Use composition for related behavior**: If the classes model different concerns that are closely coupled, use composition (object delegation) to link them rather than inheritance.

Example (composition approach):

```java
// ✅ Better design using composition
class A {
    private B helper; // delegate to B for certain behavior
    
    A(B helper) { this.helper = helper; }
    
    void doSomething() { helper.doWork(); }
}

class B {
    void doWork() { /* B's logic */ }
}
```

### 20.7 Relationship to the inheritance tree (DAG constraint)

- **Inheritance tree requirement**: Java's inheritance model requires that the superclass hierarchy form a directed acyclic graph (DAG) rooted ultimately at `java.lang.Object`.
- **No cycles allowed**: A DAG explicitly excludes cycles. Every class must have a unique path to `Object` through its superclass chain, with no possibility of looping.

### 20.8 Interview and exam checkpoints

- **Trap question**: "Can a class inherit from a class that inherits from it?" Answer: No, the compiler detects and blocks cyclic inheritance.
- **Trap question**: "What error does `class A extends A` produce?" Answer: `error: cyclic inheritance involving A` (compile-time error).
- **Best practice**: If you're tempted to create a cycle, reconsider your design. Either merge the classes or use composition.

### 20.9 Summary table

| Aspect | Details |
|---|---|
| **Definition** | A class inheriting from itself directly or indirectly through a circular chain of parent-child relationships |
| **Direct form** | `class A extends A { }` — a class extending itself (self-inheritance) |
| **Indirect form** | `class A extends B { } class B extends A { }` — circular dependency chain |
| **Compiler detection** | Compile-time error: `error: cyclic inheritance involving [ClassName]` |
| **Why blocked** | Cycles violate the inheritance tree structure (DAG requirement), create logically impossible relationships, and provide zero code reuse benefit |
| **Recommended fix** | Merge the interdependent classes into one, or use composition to break the cycle |

---

Summary: Cyclic Inheritance is logically impossible and redundant. Java's compiler detects and blocks all forms (direct self-inheritance and indirect circular chains) at compile-time. When you encounter a cycle in design, merge the classes or redesign using composition.

---

## 21 Method Signature

A Method Signature is the exact structural identifier that the Java compiler uses to recognize, track, and differentiate a method from other methods inside a class. Method signatures form the foundation for understanding Method Overloading and Method Overriding—the two primary mechanisms of Polymorphism in Java.

### 21.1 Core definition and composition

- **Definition**: A method signature is the unique structural fingerprint of a method consisting of exactly two components: the method name and the parameter list (argument types in order).

In Java, a method signature is formally defined as:

$$\text{Method Signature} = \text{Method Name} + \text{Parameter List (by type and order)}$$

- **Example**: For the method declaration:

```java
public int calculate(int total, float discount) { ... }
```

The method signature extracted by the compiler is:

$$\text{calculate(int, float)}$$

The signature is **not** the entire method declaration—it's only these two structural components.

### 21.2 Components of a method signature (detailed breakdown)

#### 21.2.1 Method Name

- The method name is part of the signature.
- Example: `calculate`, `m1`, `doWork`, etc.
- Methods with different names have different signatures even if their parameters are identical.

#### 21.2.2 Parameter List (Argument Types and Order)

- The parameter list consists of the data types of the parameters in the exact order they are declared.
- Only the types matter—not the variable names.
- The order is critical and affects the signature.

**Example comparing parameter lists**:

```java
// ✅ Different signatures (different order)
void m1(int i, String s) { }      // Signature: m1(int, String)
void m1(String s, int i) { }      // Signature: m1(String, int)

// ✅ Different signatures (different types)
void m1(int i) { }                // Signature: m1(int)
void m1(float f) { }              // Signature: m1(float)

// ❌ SAME signature (parameter names don't matter)
void m1(int total) { }            // Signature: m1(int)
void m1(int amount) { }           // Signature: m1(int) — DUPLICATE!
```

### 21.3 What is NOT part of a method signature (critical exam topics)

#### 21.3.1 Parameter variable names

- The variable labels (for example `total`, `discount`, `amount`) do not matter to the compiler.
- Only the underlying data types matter.
- Swapping parameter names does not change the signature.

**Example**:

```java
// ✅ SAME signature (names differ, but types are identical)
void m1(int total, float discount) { }    // Signature: m1(int, float)
void m1(int amount, float rate) { }       // Signature: m1(int, float) — DUPLICATE!
```

Why the compiler ignores names: Parameter names are purely for documentation and local variable access within the method body. The compiler's method lookup table uses only type information, not names.

#### 21.3.2 Return type

- **Critical point**: In Java, the return type is completely excluded from the method signature.
- This is a very common certification exam trap and a source of confusion because other languages (like C++) include the return type in their signatures.

**Example (Java)**:

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) { }       // Signature: m1(int)
    public int m1(int j) { return 10; }  // Signature: m1(int) — DUPLICATE!
}
```

**Compiler error**:

```
error: method m1(int) is already defined in class Test
```

Why the return type doesn't matter: The compiler distinguishes methods purely by signature. If it allowed two methods with the same name and parameter types but different return types, ambiguity would arise. Consider a call like:

```java
int x = t.m1(50);  // Which m1(int) should respond?
```

The compiler cannot decide based on return type alone.

**Example (C++ contrast—for context)**:

In C++, return type is part of the signature, so this is legal:

```cpp
// ✅ Legal in C++, illegal in Java
void m1(int i) { }
int m1(int i) { return 10; }  // Different return type makes them distinct
```

This is NOT legal in Java.

#### 21.3.3 Access modifiers

- Access modifiers (`public`, `private`, `protected`, `static`, `final`, `synchronized`, etc.) are completely excluded from the method signature.
- They do not affect method identity or lookup.

**Example**:

```java
// ✅ SAME signature (access modifiers differ, but name and params are identical)
public void m1(int i) { }       // Signature: m1(int)
private void m1(int i) { }      // Signature: m1(int) — DUPLICATE!
```

Why: Access modifiers control visibility and behavior semantics, not method identity. The compiler stores methods in its lookup table by signature string alone, independent of visibility rules.

### 21.4 The compiler's method table (internal mechanism)

When you compile a Java file, the compiler builds an internal lookup ledger for each class called a **Method Table**. This table stores every method mapped exclusively by its signature string.

**Example**:

```java
class Test {
    public void m1(int i) { System.out.println("m1 with int"); }
    public void m2(String s) { System.out.println("m2 with String"); }
    public double calculate(int x, float y) { return x + y; }
}
```

The compiler's internal Method Table for class `Test` looks like:

```
Method Table for class Test
├─ m1(int)
├─ m2(String)
└─ calculate(int, float)
```

**Lookup process during compilation**:

1. When you write `t.m1(10)` in code, the compiler:
   - Extracts the reference type: `Test` (from variable `t`)
   - Analyzes the argument: `10` is of type `int`
   - Constructs the lookup key: `m1(int)`
   - Searches the Method Table of class `Test` for entry `m1(int)`
   - If found ✅, compilation proceeds
   - If not found ❌, compilation fails with error: `cannot find symbol - method m1(int)`

2. When you write `t.m3(10.5)`, the compiler:
   - Constructs lookup key: `m3(double)`
   - Searches Method Table for `m3(double)`
   - Fails to find it
   - Reports error: `error: cannot find symbol - method m3(double)`

### 21.5 The duplicate signature rule (the core constraint)

**Rule**: Within the exact same class, no two methods are allowed to possess the identical method signature.

This rule is fundamental and non-negotiable. If you violate it, the compiler immediately rejects the class definition.

**Rationale**: If two methods had the same signature, the Method Table lookup would be ambiguous. When a method call is made, the compiler wouldn't know which method to invoke.

**Examples of violations**:

#### Violation 1: Same name, same parameter types (different names)

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    void m1(int i) { }           // Signature: m1(int)
    void m1(int j) { }           // Signature: m1(int) — DUPLICATE!
}
```

**Compiler error**:

```
error: method m1(int) is already defined in class Test
```

#### Violation 2: Same name, same parameter types (different return types)

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) { }       // Signature: m1(int)
    public int m1(int i) { return 10; }  // Signature: m1(int) — DUPLICATE!
}
```

**Compiler error**:

```
error: method m1(int) is already defined in class Test
```

#### Violation 3: Same name, same parameter types (different access modifiers)

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) { }       // Signature: m1(int)
    private void m1(int i) { }      // Signature: m1(int) — DUPLICATE!
}
```

**Compiler error**:

```
error: method m1(int) is already defined in class Test
```

### 21.6 Legal method variations (what CAN coexist in the same class)

The following methods can coexist in the same class because they have different signatures:

```java
class Test {
    // ✅ Different signatures (different parameter types)
    void m1(int i) { }                    // Signature: m1(int)
    void m1(float f) { }                  // Signature: m1(float)
    void m1(String s) { }                 // Signature: m1(String)

    // ✅ Different signatures (different parameter counts)
    void m1() { }                         // Signature: m1()
    void m1(int i, int j) { }             // Signature: m1(int, int)

    // ✅ Different signatures (different parameter order)
    void m2(int i, String s) { }          // Signature: m2(int, String)
    void m2(String s, int i) { }          // Signature: m2(String, int)

    // ✅ Different method names
    void m3(int i) { }                    // Signature: m3(int)
    void m4(int i) { }                    // Signature: m4(int)

    // ✅ Same signature allowed in DIFFERENT classes (inheritance)
    // This is the basis for method overriding (covered in detail later)
}
```

All of these compile successfully because each has a unique signature.

### 21.7 Why this matters: connection to Polymorphism

Method signatures are the foundation for two critical polymorphic mechanisms:

#### 21.7.1 Method Overloading

- Multiple methods with the same name but different signatures in the same class.
- Example:

```java
class Calculator {
    // ✅ Overloading: all named "add" but different signatures
    public int add(int a, int b) { return a + b; }                // Signature: add(int, int)
    public double add(double a, double b) { return a + b; }       // Signature: add(double, double)
    public int add(int a, int b, int c) { return a + b + c; }     // Signature: add(int, int, int)
}

Calculator calc = new Calculator();
calc.add(5, 10);              // Calls add(int, int)
calc.add(5.5, 10.5);          // Calls add(double, double)
calc.add(5, 10, 15);          // Calls add(int, int, int)
```

Each call is matched to the correct method by its signature.

#### 21.7.2 Method Overriding

- A subclass defines a method with the same signature as its parent class.
- Example:

```java
class Parent {
    public void display() { System.out.println("Parent display"); }  // Signature: display()
}

class Child extends Parent {
    @Override
    public void display() { System.out.println("Child display"); }   // Signature: display()
}
```

The same signature in parent and child enables polymorphic behavior (covered in detail later).

### 21.8 Compiler error scenarios (exam-critical)

| Scenario | Code | Error | Reason |
|---|---|---|---|
| Duplicate signature (same params) | `void m1(int i) { } void m1(int j) { }` | method m1(int) is already defined in class Test | Parameter names don't affect signature |
| Return type ignored | `void m1(int i) { } int m1(int i) { }` | method m1(int) is already defined in class Test | Return type is not part of signature |
| Access modifier ignored | `public void m1(int i) { } private void m1(int i) { }` | method m1(int) is already defined in class Test | Access modifiers are not part of signature |
| Method not found | `t.m1(10.5);` where only `m1(int)` exists | cannot find symbol - method m1(double) | No method with signature m1(double) |
| Wrong argument count | `t.m1(5, 10);` where only `m1(int)` exists | method m1(int) cannot be applied to given types | No method with signature m1(int, int) |

### 21.9 Interview and exam checkpoints

- **Trap question**: "Is the return type part of the method signature in Java?" Answer: No. Return type is excluded. (Note: different in C++.)
- **Trap question**: "Can I have two methods with the same name and parameters but different access modifiers?" Answer: No. Access modifiers don't create different signatures.
- **Trap question**: "Does changing a parameter name from `(int i)` to `(int j)` change the signature?" Answer: No. Only the type matters, not the name.
- **Best practice**: Always remember the formula: Signature = Method Name + Parameter Types (in order). Everything else is ignored.

### 21.10 Summary table

| Component | Part of signature? | Impact on method identity | Example |
|---|---|---|---|
| **Method name** | ✅ Yes | Different names = different signatures | `m1(int)` vs `m2(int)` |
| **Parameter types** | ✅ Yes | Different types = different signatures | `m1(int)` vs `m1(float)` |
| **Parameter order** | ✅ Yes (if types differ) | Order matters | `m1(int, String)` vs `m1(String, int)` |
| **Parameter names** | ❌ No | Names irrelevant to signature | `m1(int i)` vs `m1(int j)` — same signature |
| **Return type** | ❌ No | Cannot disambiguate methods | `void m1(int)` vs `int m1(int)` — duplicate! |
| **Access modifiers** | ❌ No | Visibility doesn't affect identity | `public void m1(int)` vs `private void m1(int)` — duplicate! |
| **Static/final/synchronized** | ❌ No | Behavioral modifiers excluded | `static void m1(int)` vs `void m1(int)` — duplicate! |

---

Summary: A Method Signature in Java consists of the method name and parameter types in order. Parameter names, return type, and access modifiers are completely excluded from the signature and do not create method identity. The compiler enforces a strict no-duplicate-signatures rule within the same class. This foundational concept is essential for understanding Method Overloading and Method Overriding, the two pillars of Polymorphism.

---

## 22 Method Overloading

Method Overloading is a core mechanism of Compile-Time Polymorphism where two or more methods inside the exact same class share the identical method name but possess different argument lists. Overloading simplifies API design by allowing developers to use a single method name for semantically equivalent operations on different data types, drastically reducing cognitive overhead compared to procedural languages like C.

### 22.1 Core definition and requirements

- **Definition**: Method Overloading occurs when two or more methods within the same class satisfy both of the following conditions:
  1. They share the identical method name.
  2. They possess different argument lists (different parameter types, counts, or sequential order).

**Formal requirement**:

$$\text{Overloaded Methods} = \text{Same Method Name} + \text{Different Signatures}$$

- **Example**:

```java
public class Calculator {
    // All named "add" but with different signatures
    public void add(int a, int b) { ... }              // Signature: add(int, int)
    public void add(double a, double b) { ... }        // Signature: add(double, double)
    public void add(int a, int b, int c) { ... }       // Signature: add(int, int, int)
}
```

All three methods are overloaded variants of `add` because they share the name but have different signatures.

### 22.2 What does NOT affect overloading (critical constraints)

The following characteristics are completely ignored when determining whether methods are overloaded:

#### 22.2.1 Return type

- Return type has no influence on overloading.
- Two methods with the same name and parameters but different return types do NOT constitute overloading—they create a compile-time error.

**Example (illegal)**:

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) { }       // Signature: m1(int)
    public int m1(int i) { }        // Signature: m1(int) — DUPLICATE, not overloading
}
```

**Error**:

```
error: method m1(int) is already defined in class Test
```

#### 22.2.2 Access modifiers

- Access modifiers (`public`, `private`, `protected`, `static`, etc.) are completely ignored.
- Changing access modifier alone does not create overloading.

**Example (illegal)**:

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) { }       // Signature: m1(int)
    private void m1(int i) { }      // Signature: m1(int) — DUPLICATE, not overloading
}
```

#### 22.2.3 Thrown exceptions

- Exceptions declared in the `throws` clause do not affect overloading.

**Example (illegal)**:

```java
// ❌ COMPILE-TIME ERROR!
class Test {
    public void m1(int i) throws IOException { }       // Signature: m1(int)
    public void m1(int i) throws SQLException { }      // Signature: m1(int) — DUPLICATE
}
```

#### 22.2.4 Other modifiers (final, synchronized, strictfp)

- Behavioral modifiers like `final`, `synchronized`, and `strictfp` are excluded from overloading consideration.

### 22.3 The Java vs. C contrast (why overloading matters)

One of the most powerful arguments for method overloading is its contrast with procedural, non-OOP languages like C, which strictly disallow overloading. This section highlights why overloading is a game-changer for API design and developer productivity.

#### 22.3.1 The C approach (no overloading)

In C, no two functions can ever share the same name. For each variation of behavior, you must create a completely different function name.

**Example: Absolute value utility functions in C**

```c
int abs(int x) { return x < 0 ? -x : x; }        // For int
long labs(long x) { return x < 0 ? -x : x; }     // For long
float fabs(float x) { return x < 0 ? -x : x; }   // For float
double dabs(double x) { return x < 0 ? -x : x; } // For double
```

**The cognitive overhead**:
- Developers must memorize four distinct function names for the exact same conceptual operation: absolute value.
- The library documentation explodes in size with thousands of similar but differently-named functions.
- Code readability suffers: readers must context-switch between `abs()`, `labs()`, `fabs()`, `dabs()`.
- This cognitive load increases with library size and complexity.

#### 22.3.2 The Java approach (with overloading)

In Java, you define a single unified method name and let overloading handle the dispatch automatically based on argument types.

**Example: Absolute value with overloading in Java**

```java
public class MathUtils {
    public static int abs(int x) { return x < 0 ? -x : x; }           // Signature: abs(int)
    public static long abs(long x) { return x < 0 ? -x : x; }         // Signature: abs(long)
    public static float abs(float x) { return x < 0 ? -x : x; }       // Signature: abs(float)
    public static double abs(double x) { return x < 0 ? -x : x; }     // Signature: abs(double)
}

// Usage
int a = MathUtils.abs(-5);           // Calls abs(int)
long b = MathUtils.abs(-50L);        // Calls abs(long)
float c = MathUtils.abs(-5.5f);      // Calls abs(float)
double d = MathUtils.abs(-5.5);      // Calls abs(double)
```

**The benefits**:
- Single, unified method name: `abs()` is easier to remember and discover.
- Compiler automatically routes to the correct variant based on argument type.
- API is simpler and more intuitive.
- Cognitive load dramatically reduced.
- Code is more readable: readers always see `abs()`, not a mix of `abs`, `labs`, `fabs`, `dabs`.

**Comparison**:

| Aspect | C (No Overloading) | Java (With Overloading) |
|---|---|---|
| Function names | `abs`, `labs`, `fabs`, `dabs` | Single: `abs` |
| Developer memory load | High (must memorize 4+ names) | Low (single name) |
| Code readability | Poor (scattered similar names) | Excellent (consistent naming) |
| API complexity | Explodes with library size | Scales elegantly |
| Error risk | Higher (typo in function name) | Lower (single canonical name) |

### 22.4 Implementation walkthrough: The PolyTest model

Durga Sir presents a clean, practical class demonstrating three overloaded variants of a single method `m1()`.

```java
public class PolyTest {
    // Overloaded Variant 1: No arguments
    public void m1() {
        System.out.println("no-arg method");
    }

    // Overloaded Variant 2: Single int argument
    public void m1(int i) {
        System.out.println("int-arg method: " + i);
    }

    // Overloaded Variant 3: Single double argument
    public void m1(double d) {
        System.out.println("double-arg method: " + d);
    }

    public static void main(String[] args) {
        PolyTest t = new PolyTest();

        t.m1();       // Call 1: No arguments
        t.m1(10);     // Call 2: Pass int
        t.m1(10.5);   // Call 3: Pass double
    }
}
```

**Execution output**:

```
no-arg method
int-arg method: 10
double-arg method: 10.5
```

**Analysis**:

1. `t.m1()` → Matches signature `m1()` → Calls Variant 1
2. `t.m1(10)` → Argument is `int` → Matches signature `m1(int)` → Calls Variant 2
3. `t.m1(10.5)` → Argument is `double` → Matches signature `m1(double)` → Calls Variant 3

Each call targets the correct overloaded method automatically through compiler resolution.

### 22.5 Method resolution mechanism (compiler-driven dispatch)

The architectural centerpiece of method overloading is **Method Resolution**—the algorithmic process where the compiler determines exactly which overloaded method should execute for a given method call.

#### 22.5.1 The overloading commandment

**Rule**: In method overloading, method resolution is handled **exclusively by the compiler at compile-time**, driven strictly by the **Reference Type** of the variable, not by runtime object state.

**Key insight**: Because resolution happens before the program runs, the runtime state of the object is completely bypassed during lookup and matching. This is what makes overloading deterministic and predictable.

#### 22.5.2 Compile-time resolution process

When the compiler encounters a method call like `t.m1(10)`, it performs these steps:

1. **Extract reference type**: Examine the declared type of variable `t` (e.g., `PolyTest`).
2. **Analyze arguments**: Determine the types of arguments passed (e.g., `10` is `int`).
3. **Construct method signature**: Build the lookup key from method name + argument types (e.g., `m1(int)`).
4. **Search method table**: Look up the signature in the class's internal method table.
5. **Match and bind**: If found, bind the call to that specific method at compile-time.
6. **Generate bytecode**: Emit bytecode that hardcodes the method binding (no runtime lookup needed).

**Example trace**:

```java
PolyTest t = new PolyTest();
t.m1(10);  // Compiler processes this call
```

Compiler reasoning:
- Reference type: `PolyTest`
- Argument type: `int` (literal `10`)
- Lookup key: `m1(int)`
- Found in method table: ✅ Yes
- Binding: `t.m1(10)` → call `PolyTest.m1(int)` (hardcoded in bytecode)
- Result: No runtime overhead; the correct method is already determined

#### 22.5.3 Why reference type matters (not runtime object type)

**Critical principle**: The compiler uses the **reference type** (declared type of the variable), not the **runtime object type**, to resolve overloaded method calls.

**Example demonstrating the distinction**:

```java
class Animal { void speak() { System.out.println("Animal sound"); } }
class Dog extends Animal { void speak() { System.out.println("Woof"); } }

public class Test {
    // Overloaded method: accepts Animal reference
    public void process(Animal a) { System.out.println("Processing Animal"); }
    
    // Overloaded method: accepts Dog reference
    public void process(Dog d) { System.out.println("Processing Dog"); }

    public static void main(String[] args) {
        Test t = new Test();
        
        Animal a = new Dog();        // Reference type: Animal, Object type: Dog
        t.process(a);                // Compiler sees: process(Animal) — calls first variant
        
        Dog d = new Dog();           // Reference type: Dog, Object type: Dog
        t.process(d);                // Compiler sees: process(Dog) — calls second variant
    }
}
```

**Output**:

```
Processing Animal
Processing Dog
```

**Explanation**:
- First call: `a` is declared as `Animal` (reference type) even though it holds a `Dog` object. Compiler resolves to `process(Animal)`.
- Second call: `d` is declared as `Dog` (reference type) and holds a `Dog` object. Compiler resolves to `process(Dog)`.

The runtime object type (`Dog`) is irrelevant to overloading resolution; only the reference type matters.

### 22.6 Aliases for method overloading (three names, one concept)

Method overloading is known by three equivalent technical names in computer science, all describing the same underlying mechanism:

#### 22.6.1 Compile-Time Polymorphism

- **Meaning**: The compiler determines which method to call at compile-time, before the program runs.
- **Characteristic**: The method binding is fixed and deterministic at build time.

#### 22.6.2 Static Polymorphism

- **Meaning**: The method resolution is static (fixed) rather than dynamic (determined at runtime).
- **Characteristic**: No runtime lookup or decision-making is required.

#### 22.6.3 Early Binding

- **Meaning**: Method binding occurs early (at compile-time) rather than late (at runtime).
- **Characteristic**: The bytecode already contains the exact method reference; no indirect method table lookup happens at runtime.

**All three names describe the same mechanism**:

$$\text{Compile-Time Polymorphism} = \text{Static Polymorphism} = \text{Early Binding}$$

### 22.7 Overloading vs. Overriding (quick distinction)

This is a common source of confusion. Here's the key difference:

| Aspect | Method Overloading | Method Overriding |
|---|---|---|
| **Definition** | Multiple methods with same name, different signatures in the **same class** | Child class method with same name and signature as parent class method |
| **Resolution** | Compile-time (Static Polymorphism) | Runtime (Dynamic Polymorphism) |
| **Requirements** | Different signatures (parameter types/count/order) | **Identical** signature (name + parameters) |
| **Return type** | Can differ (doesn't affect overloading) | Must be compatible (covariant return types allowed in Java 5+) |
| **Access modifier** | Can differ | Cannot be more restrictive |
| **Scope** | Same class | Parent and child classes |
| **Example** | `add(int)` and `add(double)` in same class | `toString()` in child overrides `toString()` in parent |

### 22.8 Legal overloading scenarios (what IS allowed)

These method combinations all constitute valid overloading within the same class:

```java
public class ValidOverloading {
    // ✅ Different number of parameters
    public void m1() { }
    public void m1(int i) { }
    public void m1(int i, int j) { }

    // ✅ Different parameter types
    public void m2(int i) { }
    public void m2(double d) { }
    public void m2(String s) { }

    // ✅ Different parameter order
    public void m3(int i, String s) { }
    public void m3(String s, int i) { }

    // ✅ Different return types (allowed!)
    public int m4(int i) { return i; }
    public double m4(double d) { return d; }

    // ✅ Different access modifiers (allowed!)
    public void m5(int i) { }
    private void m5(String s) { }

    // ✅ Different thrown exceptions (allowed!)
    public void m6(int i) throws IOException { }
    public void m6(String s) throws SQLException { }
}
```

All combinations above are valid overloading.

### 22.9 Illegal overloading scenarios (what is NOT allowed)

These combinations do NOT constitute valid overloading and result in compile-time errors:

```java
// ❌ ILLEGAL: Identical signatures
class Test {
    public void m1(int i) { }
    public void m1(int i) { }  // ERROR: duplicate method
}

// ❌ ILLEGAL: Only return type differs
class Test {
    public void m1(int i) { }
    public int m1(int i) { }   // ERROR: duplicate method
}

// ❌ ILLEGAL: Only access modifier differs
class Test {
    public void m1(int i) { }
    private void m1(int i) { } // ERROR: duplicate method
}

// ❌ ILLEGAL: Only thrown exception differs
class Test {
    public void m1(int i) throws IOException { }
    public void m1(int i) throws SQLException { }  // ERROR: duplicate method
}
```

### 22.10 Compiler error scenarios (method overloading traps)

| Scenario | Code | Error | Reason |
|---|---|---|---|
| Identical signatures | `void m1(int) { } void m1(int) { }` | method m1(int) is already defined | Signatures identical; not overloading |
| Return type only differs | `void m1(int) { } int m1(int) { }` | method m1(int) is already defined | Return type ignored; creates duplicate |
| Access modifier only differs | `public void m1(int) { } private void m1(int) { }` | method m1(int) is already defined | Modifier ignored; creates duplicate |
| No matching overload | `t.m1(10.5);` where only `m1(int)` exists | cannot find symbol - method m1(double) | No signature `m1(double)` in method table |
| Ambiguous overloading | `void m1(int) { } void m1(long) { } ... t.m1(5);` | reference to m1 is ambiguous | Both int and long could match |

### 22.11 Real-world overloading examples (Java standard library)

The Java standard library uses method overloading extensively:

#### 22.11.1 System.out.println()

```java
// All named "println" but different signatures
System.out.println();              // println()
System.out.println(true);          // println(boolean)
System.out.println(int);           // println(int)
System.out.println(long);          // println(long)
System.out.println(float);         // println(float)
System.out.println(double);        // println(double)
System.out.println(char);          // println(char)
System.out.println(String);        // println(String)
System.out.println(Object);        // println(Object)
```

All overloads provide the same semantic behavior (print a value) but handle different types.

#### 22.11.2 String.valueOf()

```java
String.valueOf(true);              // valueOf(boolean)
String.valueOf(5);                 // valueOf(int)
String.valueOf(5L);                // valueOf(long)
String.valueOf(5.5f);              // valueOf(float)
String.valueOf(5.5);               // valueOf(double)
String.valueOf(new Object());      // valueOf(Object)
```

#### 22.11.3 Math.min() / Math.max()

```java
Math.min(5, 10);                   // min(int, int)
Math.min(5L, 10L);                 // min(long, long)
Math.min(5.5f, 10.5f);             // min(float, float)
Math.min(5.5, 10.5);               // min(double, double)
```

### 22.12 Interview and exam checkpoints

- **Trap question**: "Are methods with the same name and parameters but different return types overloaded?" Answer: No. Return type is ignored. This creates a duplicate method error.
- **Trap question**: "Does access modifier affect overloading?" Answer: No. Overloading is determined solely by method name and parameter types.
- **Trap question**: "Is method overloading resolved at compile-time or runtime?" Answer: Compile-time (Static Polymorphism / Early Binding).
- **Trap question**: "In overloading, does the reference type or runtime object type determine which method is called?" Answer: Reference type. The compiler uses the declared type.
- **Best practice**: Use overloading to provide a unified, intuitive API for semantically equivalent operations on different data types.

### 22.13 Summary table

| Aspect | Details |
|---|---|
| **Definition** | Multiple methods with same name but different signatures in the same class |
| **Requirements** | Same method name + Different parameter types/count/order |
| **Resolution** | Compile-time (Static Polymorphism, Early Binding) |
| **Reference vs Runtime** | Compiler uses reference type, not runtime object type |
| **What matters** | Method name + Parameter types (in order) |
| **What doesn't matter** | Return type, access modifiers, thrown exceptions |
| **C contrast** | C requires unique names (abs, labs, fabs); Java uses single name with overloading |
| **Real-world example** | `System.out.println()` has 9+ overloads for different types |
| **Benefit** | Reduced cognitive load, cleaner API, more intuitive code |
| **Common trap** | Thinking return type or access modifier affects overloading |

---

Summary: Method Overloading is Compile-Time Polymorphism where multiple methods share the same name but have different signatures. Resolution is handled entirely by the compiler based on the reference type and argument types at compile-time. Return types, access modifiers, and thrown exceptions do not affect overloading. Java's overloading dramatically simplifies API design compared to procedural languages like C, where functions must have unique names for each variant.

---

## 22.1 Method Overloading Case Study-1: Automatic Type Promotion

This case study explores how the Java compiler uses automatic promotion of primitive data types during compile-time method resolution. When an exact type match is not found for an overloaded method call, the compiler attempts to widen the argument type and search again, following a strict promotion hierarchy.

### 22.1.1 Conceptual foundation: Automatic promotion

When you pass an argument into an overloaded method, the compiler immediately scans the class's method table for a method with an exact matching parameter data type.

**The Promotion Rule**:

If an exact type match is not available, the compiler does **not** throw an error immediately. Instead, it attempts to automatically promote (widen) the argument data type to its next highest compatible primitive type and searches the method table again. The compiler repeats this widening process step-by-step until it finds a match or runs out of compatible wider types, at which point it throws a compilation error.

**Key principle**: Widening is safe (no data loss) and is allowed. Narrowing (downcasting) is not allowed because it can cause data loss.

### 22.1.2 The primitive promotion hierarchy

Java defines a strict promotion pathway for primitive types. The compiler follows this hierarchy when attempting to find a matching overloaded method:

$$\text{byte} \to \text{short} \to \text{int} \to \text{long} \to \text{float} \to \text{double}$$

$$\text{char} \to \text{int}$$

**Key observation**: 
- Both `byte` and `short` promote up to `int` (they skip directly to `int`, not to each other).
- `char` bypasses `short` and goes directly to `int`.
- `long` can promote to `float` and then to `double`.
- `double` is the highest and cannot be promoted further.

**The promotion hierarchy visualized**:

```
┌─────────────────────────────────────────────────┐
│        Java Primitive Type Promotion            │
├─────────────────────────────────────────────────┤
│                                                 │
│  byte  ─┐                                       │
│         ├─→ int ─→ long ─→ float ─→ double     │
│  short ─┘                                       │
│                                                 │
│  char  ──────────┘                              │
│                                                 │
└─────────────────────────────────────────────────┘
```

### 22.1.3 Case study implementation: CaseStudyOne class

Durga Sir maps out a practical class structure containing two overloaded methods: one taking an `int` and one taking a `float`.

```java
public class CaseStudyOne {
    // Overloaded Variant 1: int argument
    public void m1(int i) {
        System.out.println("int-arg method");
    }

    // Overloaded Variant 2: float argument
    public void m1(float f) {
        System.out.println("float-arg method");
    }

    public static void main(String[] args) {
        CaseStudyOne t = new CaseStudyOne();

        // Call 1: Exact Match (int)
        t.m1(10);       // Outputs: "int-arg method"

        // Call 2: Exact Match (float)
        t.m1(10.5f);    // Outputs: "float-arg method"

        // Call 3: Promotion (char)
        t.m1('a');      // Outputs: "int-arg method"

        // Call 4: Promotion (long)
        t.m1(10L);      // Outputs: "float-arg method"

        // Call 5: Compilation Collapse (double)
        // t.m1(10.5);  // ❌ COMPILE-TIME ERROR!
    }
}
```

**Expected output**:

```
int-arg method
float-arg method
int-arg method
float-arg method
```

### 22.1.4 Step-by-step resolution trace

#### 22.1.4.1 Call 1: t.m1(10);

**Argument passed**: `int` (literal `10` is an `int`)

**Compiler resolution**:
1. Scans class method table for exact match
2. Finds signature `m1(int)` ✅ Exact match found
3. Executes Variant 1 natively (no promotion needed)

**Output**: `"int-arg method"`

**Analysis**: This is the simplest case—exact type match requires no promotion.

#### 22.1.4.2 Call 2: t.m1(10.5f);

**Argument passed**: `float` (suffix `f` explicitly declares it as `float`)

**Compiler resolution**:
1. Scans class method table for exact match
2. Finds signature `m1(float)` ✅ Exact match found
3. Executes Variant 2 natively (no promotion needed)

**Output**: `"float-arg method"`

**Analysis**: Explicit float literal matches the second overload directly.

#### 22.1.4.3 Call 3: t.m1('a'); (The Char Promotion)

**Argument passed**: `char` (character `'a'`)

**Compiler resolution process**:

1. **Step 1**: Scans for exact match `m1(char)` → Not found ❌
2. **Step 2**: Applies promotion rule: char → int
3. **Step 3**: Scans for `m1(int)` → Found ✅
4. **Step 4**: Binds call to Variant 1

**Promotion flow**:

```
char 'a' ──→ (promoted to int) ──→ Matches m1(int)
```

**Output**: `"int-arg method"`

**Analysis**: The compiler automatically promotes the char argument to int (the next tier in the hierarchy), finds a match, and executes Variant 1. This is a **Promotion Level 1** case.

#### 22.1.4.4 Call 4: t.m1(10L); (The Long Promotion)

**Argument passed**: `long` (suffix `L` explicitly declares it as `long`)

**Compiler resolution process**:

1. **Step 1**: Scans for exact match `m1(long)` → Not found ❌
2. **Step 2**: Looks at promotion hierarchy from `long`:
   - `long` cannot demote to `int` (data loss risk, blocked)
   - `long` can promote to `float` ✅
3. **Step 3**: Scans for `m1(float)` → Found ✅
4. **Step 4**: Binds call to Variant 2

**Promotion flow**:

```
long 10L ──→ (promoted to float) ──→ Matches m1(float)
```

**Output**: `"float-arg method"`

**Analysis**: The compiler cannot demote `long` to `int` (that would risk data loss), but it can widen `long` to `float`. This is a **Promotion Level 2** case, requiring a two-step promotion up the hierarchy.

#### 22.1.4.5 Call 5: t.m1(10.5); (The Failure Case)

**Argument passed**: `double` (un-suffixed decimal floating-point literals default to `double`)

**Compiler resolution process**:

1. **Step 1**: Scans for exact match `m1(double)` → Not found ❌
2. **Step 2**: Looks at promotion hierarchy from `double`:
   - `double` is the **highest** primitive type
   - No type can promote `double` further ❌
   - Demoting to `float` or `int` is blocked (data loss risk) ❌
3. **Step 3**: No match found; compilation fails

**Error message**:

```
error: no suitable method found for m1(double)
  required: int or float
  found: double
  reason: actual argument double cannot be converted to int by method invocation conversion
```

**Output**: ❌ **COMPILE-TIME ERROR**

**Analysis**: `double` is at the top of the promotion hierarchy and cannot be promoted further. Downcasting (narrowing) is strictly forbidden because it risks precision loss. The compiler has no valid promotion path, so compilation fails immediately.

### 22.1.5 Promotion rules summary table

| Parameter Type | Search 1 | Search 2 | Search 3 | Search 4 | Result |
|---|---|---|---|---|---|
| `int` | `m1(int)` ✅ | — | — | — | **Matched** |
| `float` | `m1(float)` ✅ | — | — | — | **Matched** |
| `char` | `m1(char)` ❌ | `m1(int)` ✅ | — | — | **Matched** (promoted) |
| `long` | `m1(long)` ❌ | `m1(float)` ✅ | — | — | **Matched** (promoted) |
| `double` | `m1(double)` ❌ | `m1(float)` ❌ | Cannot promote higher | — | **ERROR** |

**Key observations**:
- Exact matches require zero promotions.
- `char` requires one promotion step (`char` → `int`).
- `long` requires widening to the next compatible type (`long` → `float`).
- `double` cannot find a promotion path; no suitable method exists.

### 22.1.6 Execution trace summary checklist

| Call | Parameter Type | Target Search | Promotional Action | Resolved Method | Output |
|---|---|---|---|---|---|
| `t.m1(10)` | `int` | `m1(int)` | Exact match (no promotion) | `m1(int)` | `"int-arg method"` |
| `t.m1(10.5f)` | `float` | `m1(float)` | Exact match (no promotion) | `m1(float)` | `"float-arg method"` |
| `t.m1('a')` | `char` | `m1(char)` | Promoted to `int` | `m1(int)` | `"int-arg method"` |
| `t.m1(10L)` | `long` | `m1(long)` | Promoted to `float` | `m1(float)` | `"float-arg method"` |
| `t.m1(10.5)` | `double` | `m1(double)` | Cannot promote; max type reached | — | **❌ COMPILE ERROR** |

### 22.1.7 Critical compilation rules for promotion

**Rule 1: Exact match preferred**
- If an exact type match exists, it is always chosen first. No promotion occurs.

**Rule 2: Widening is allowed**
- Automatic widening (promotion to a larger type) is permitted because no data loss occurs.
- Example: `int` → `long`, `float` → `double`, `char` → `int`.

**Rule 3: Narrowing is blocked**
- Automatic narrowing (demotion to a smaller type) is not allowed because it risks data loss.
- Example: `long` → `int` (would lose the upper 32 bits) is forbidden.
- Exception: `double` → `float` (would lose precision) is also forbidden automatically.

**Rule 4: Maximum type reached = error**
- If a type reaches the top of the hierarchy (`double` for numeric types) and no exact match exists, promotion cannot proceed, and compilation fails.

**Rule 5: Promotion follows strict hierarchy**
- The compiler follows the official promotion chain. Shortcuts or alternative paths are not allowed.

### 22.1.8 Why the double case fails

The failure case (`t.m1(10.5)`) deserves special attention because it reveals an important principle:

**The double problem**:
- `double` is the largest, most general numeric primitive type in Java.
- It can hold any value that `int`, `long`, `float` can hold (and more).
- However, no method signature exists for `double`.
- The compiler **cannot** automatically downcast `double` to `float` or `int` because:
  - **Data loss risk**: Converting `double` → `float` loses precision.
  - **No implicit narrowing**: Java's type system forbids automatic narrowing conversions.
  - **Safety principle**: The compiler must ensure no accidental data corruption.

**Solution alternatives**:
If you actually need to call a method with a `double` argument when only `int` or `float` overloads exist:

```java
CaseStudyOne t = new CaseStudyOne();

// Option 1: Explicit cast to float (data loss)
t.m1((float) 10.5);        // ✅ Legal; casts double to float explicitly

// Option 2: Use a float literal
t.m1(10.5f);               // ✅ Legal; creates float directly

// Option 3: Add an overload for double
public void m1(double d) { System.out.println("double-arg method"); }
```

### 22.1.9 Promotion hierarchy reference (for all primitive types)

Complete promotion rules for all primitive types:

```
byte   ──→ short ──→ int ──→ long ──→ float ──→ double
                      ↑
char   ─────────────┘

boolean: No promotion; not part of numeric hierarchy
```

**Detailed rules**:

| Source Type | Can promote to | Cannot promote to |
|---|---|---|
| `byte` | short, int, long, float, double | — |
| `short` | int, long, float, double | byte, char |
| `char` | int, long, float, double | byte, short |
| `int` | long, float, double | byte, short, char |
| `long` | float, double | byte, short, char, int |
| `float` | double | byte, short, char, int, long |
| `double` | — (max type) | All narrowing blocked |
| `boolean` | — (not numeric) | All promotions blocked |

### 22.1.10 Real-world implications for API design

Understanding type promotion has practical implications when designing overloaded methods:

**Implication 1: Avoid ambiguous overloads**

```java
// ⚠️ Potentially problematic design
public void process(int i) { }
public void process(long l) { }

// Calling with byte:
process((byte) 5);  // Promotes to int; calls first method
```

**Implication 2: Document promotion behavior**

```java
/**
 * Processes an integer value.
 * Note: byte and short arguments are automatically promoted to int.
 * Char arguments are also promoted to int.
 */
public void process(int i) { }
```

**Implication 3: Use explicit types for clarity**

```java
// Less clear
double result = calculate(10);  // Is this 10.0 or 10?

// More clear
double result = calculate(10.0);  // Explicitly double
int result = calculate(10);       // Explicitly int
```

### 22.1.11 Interview and exam checkpoints

- **Trap question**: "If I pass a `char` to a method expecting `int`, what happens?" Answer: The compiler automatically promotes `char` to `int` and calls the method.
- **Trap question**: "Can a `double` be automatically converted to `float`?" Answer: No. Automatic narrowing is forbidden. You must explicitly cast.
- **Trap question**: "What does the compiler do if no promotion path exists?" Answer: It throws a compile-time error `no suitable method found`.
- **Trap question**: "Is `boolean` part of the promotion hierarchy?" Answer: No. `boolean` is not a numeric type and cannot be promoted.
- **Best practice**: Add overloads for the types you expect, but be aware of the automatic promotion hierarchy.

### 22.1.12 Summary: Automatic type promotion in method overloading

**Key takeaways**:

1. **Exact match first**: If an exact type match exists in the method table, it is always chosen.
2. **Automatic widening**: If no exact match, the compiler attempts to widen (promote) the argument type following the strict promotion hierarchy.
3. **No automatic narrowing**: Narrowing conversions (e.g., `double` → `float`) are forbidden to prevent data loss.
4. **Hierarchy is fixed**: The promotion path is: `byte` → `short` → `int` → `long` → `float` → `double`, with `char` → `int`.
5. **Maximum type error**: If the argument type reaches the top of the hierarchy (`double`) with no match, compilation fails.
6. **Deterministic resolution**: Because promotion is automatic and follows a fixed hierarchy, method resolution is completely deterministic and can be verified at compile-time.

---

Summary: Method Overloading Case Study-1 demonstrates how the Java compiler uses automatic type promotion to resolve overloaded method calls. When an exact type match is not found, the compiler widens the argument type through a strict promotion hierarchy (byte/short/char → int → long → float → double). Narrowing (downcasting) is forbidden to prevent data loss. If promotion reaches the top of the hierarchy without finding a match, compilation fails. Understanding this mechanism is critical for designing clear APIs and avoiding unexpected method invocations.
