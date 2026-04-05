## Why We Use Collections Instead of Arrays

To overcome the above limitations of Arrays we should go for Collections.

Collections are growable in nature, i.e. based on our requirement we can increase (or) decrease the size.
Collections can hold both homogeneous & heterogeneous elements.
Every Collection class is implemented based on some standard data structure. Hence readymade method support is available for every requirement. Being a programmer we have to use this method and we are not responsible to provide implementation.

### Proper Explanation

The content explains why Java Collections are preferred over arrays in many real-world cases:

1. **Dynamic size**
Arrays have fixed length once created. Collections are dynamic, so their size can grow or shrink as needed.

2. **Flexible data handling**
Collections can store similar types (homogeneous) and, if generics are not enforced, different types (heterogeneous).

3. **Built-in functionality**
Collection classes (like `ArrayList`, `LinkedList`, `HashSet`, and `HashMap`) are built on standard data structures and provide ready-made methods such as add, remove, search, iteration, sorting support, and more.

4. **Less implementation effort**
As developers, we mostly use the provided APIs instead of building data structures from scratch, which improves productivity and reliability.

### Note

In modern Java, we usually use **generics** (for example, `List<String>`) to keep collections type-safe and avoid runtime type errors.

---

## Difference Between Arrays and Collections


Difference between Arrays and Collections:

**Arrays**

1. Arrays are fixed in size.
2. Wrt memory arrays are not recommended to use.
3. Wrt Performance Arrays are recommended to use.
4. Array can hold only homogeneous datatype elements.
5. There is no underlying data structure for arrays and hence readymade method support is not available.
6. Array can hold both primitives and object types.

**Collections**

1. Collections are growable in nature. I.e. based on our requirement we can increase or decrease the size.
2. Wrt to memory collections are recommended to use.
3. Wrt Performance collections are not recommended to use.
4. Collections can hold both homogeneous and heterogeneous elements.
5. Every Collections class is implemented based on some standard data structure. Hence readymade method support is available for every requirement.
6. Collections can hold only objects but not primitives.

### Proper Explanation (Corrected and Practical)

The image compares arrays and collections, but some points are simplified. This is a cleaner and more accurate understanding:

| Topic | Arrays | Collections |
|---|---|---|
| Size | Fixed length after creation. | Dynamic size (can grow/shrink). |
| Memory usage | Often lower overhead for simple, fixed-size data. | Extra wrapper/object overhead can increase memory use. |
| Performance | Very fast for indexed access and primitive storage. | Performance depends on type (`ArrayList`, `LinkedList`, `HashSet`, etc.). Not always slower. |
| Data type support | Typically homogeneous (single declared type); can store primitives directly. | Stores objects only; primitives use wrapper classes (`Integer`, `Double`, etc.) via autoboxing. |
| API support | Limited built-in operations (`length`, indexing, manual loops). | Rich API (`add`, `remove`, `contains`, iteration utilities, sorting helpers, streams). |
| Use case | Best when size is known and performance is critical. | Best when flexibility, easy updates, and utility methods are needed. |

### Key Takeaway

Use **arrays** for fixed-size, high-performance scenarios (especially with primitives), and use **collections** for dynamic, real-world application data where maintainability and built-in operations matter more.

---

## Foundational Overview of Collections and Collection Framework in Java

Java developers often begin with arrays to store multiple values, but arrays are only the first step in managing grouped data. As applications grow, we need structures that are easier to resize, search, organize, and update. This is where Collections and the Collection Framework become essential.

### What Is a Collection?

A **collection** represents a group of individual objects treated as a single unit.

In practical terms, whenever we need to store many related objects together, we use a collection. Examples include:

- A group of student objects in a classroom management system
- A list of books in a library application
- A set of unique tags, markers, or identifiers

So, instead of handling each object separately, we manage them as one logical group.

### Why Collections Are Needed

Arrays have important limitations:

- Their size is fixed once created
- Insertions and deletions can be inconvenient in many situations
- They provide limited built-in operations for real-world data handling

Collections solve these issues by offering dynamic structures and utility methods that support adding, removing, searching, sorting, and traversing data more effectively.

### What Is the Collection Framework?

The **Collection Framework** is the standard architecture provided by Java to manage groups of objects.

It is not just a single class. It is a complete ecosystem of:

- Interfaces (such as List, Set, Queue, Map)
- Implementations (such as ArrayList, LinkedList, HashSet, PriorityQueue, HashMap)
- Utility support (iteration patterns, algorithms, and helper methods)

This framework gives developers a consistent way to store and manipulate object collections without building every data structure from scratch.

### Java and C++ Concept Mapping

The core ideas are not unique to Java. Similar concepts exist in C++:

- Java Collection -> C++ Container
- Java Collection Framework -> C++ STL (Standard Template Library)

This comparison highlights that the naming may differ, but the goal is similar in both languages: provide reusable, standard, and efficient ways to manage grouped data.

### Library Perspective: Classes and Interfaces

In this context, a library means a prebuilt set of classes and interfaces that we can directly use in our programs.

For the Collection Framework, this means:

- The design contracts are defined by interfaces
- Concrete behavior is provided by implementation classes
- Developers focus on using these tools correctly rather than re-implementing foundational structures each time

This improves code quality, development speed, readability, and long-term maintainability.

### Practical Conclusion

Collections are the natural evolution from arrays when building real applications. Arrays are still useful for fixed-size and performance-sensitive use cases, but the Collection Framework is generally preferred when flexibility, cleaner APIs, and scalable object management are required.

In short, learning Collections is not optional for Java development. It is a foundational skill for writing modern, maintainable Java code.

---

## 9 Key Interfaces of Collection Framework

The Collection Framework provides several core interfaces that define contracts for different types of collections. Understanding these interfaces is essential for writing flexible and reusable code.

### Interface 1: Collection (Root Interface)

#### Extracted Content

The `Collection` interface is the foundation of the Collection Framework:

- If we want to represent a group of individual objects as a single entity, we should use Collection.
- The Collection interface defines the most common methods applicable to any Collection object.
- Collection interface is considered the root interface of the Collection Framework.
- **Important Note**: There is no concrete class that implements the Collection interface directly.

#### Detailed Explanation

The `Collection` interface serves as the parent/root interface for all collection types in Java (except for Map, which is a separate hierarchy). It defines a contract—a set of methods that all collection implementations must provide.

**Why it's the root:**

Collections are data structures meant to hold groups of objects. Before getting into specific types like lists or sets, Java defines a base interface that covers what ALL collections should be able to do:

- Add objects
- Remove objects
- Search for objects
- Iterate through objects
- Check size and emptiness

Since every collection (whether it's a List, Set, or Queue) needs these basic operations, they all extend or inherit from Collection.

**Why no direct implementation:**

`Collection` is too abstract. Java doesn't provide a concrete class that directly implements it because:

- Different collection types (lists, sets, queues) have different semantics
- A list allows duplicates and maintains order
- A set doesn't allow duplicates
- A queue follows FIFO or priority-based ordering

It would be incorrect to have a single implementation for all these different behaviors. Instead, specialized classes implement the appropriate interfaces (like ArrayList implements List, HashSet implements Set, etc.).

#### Common Methods Defined in Collection Interface

| Method | Purpose | Example |
|--------|---------|---------|
| `add(E e)` | Adds an element | `list.add("Java")` |
| `remove(Object o)` | Removes an element | `list.remove("Java")` |
| `contains(Object o)` | Checks if element exists | `list.contains("Java")` |
| `size()` | Returns number of elements | `int count = list.size()` |
| `isEmpty()` | Checks if collection is empty | `if (list.isEmpty())` |
| `clear()` | Removes all elements | `list.clear()` |
| `iterator()` | Returns an iterator | `Iterator it = list.iterator()` |

#### Code Examples

**Example 1: Using ArrayList (which implements Collection via List)**

```java
import java.util.*;

public class CollectionExample1 {
    public static void main(String[] args) {
        // ArrayList is a concrete class that implements the Collection interface
        Collection<String> fruits = new ArrayList<>();
        
        // Adding elements (add method from Collection interface)
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        
        // Check size (size method from Collection interface)
        System.out.println("Total fruits: " + fruits.size()); // Output: 3
        
        // Check if element exists (contains method from Collection interface)
        if (fruits.contains("Apple")) {
            System.out.println("Apple is in the collection");
        }
        
        // Remove an element (remove method from Collection interface)
        fruits.remove("Banana");
        System.out.println("After removal: " + fruits.size()); // Output: 2
        
        // Iterate through collection (iterator method from Collection interface)
        System.out.println("Fruits in collection:");
        for (String fruit : fruits) {
            System.out.println("  - " + fruit);
        }
    }
}

/* Output:
Total fruits: 3
Apple is in the collection
After removal: 2
Fruits in collection:
  - Apple
  - Orange
*/
```

**Example 2: Using HashSet (implements Collection via Set)**

```java
import java.util.*;

public class CollectionExample2 {
    public static void main(String[] args) {
        // HashSet is a concrete class that implements Collection via Set
        Collection<Integer> numbers = new HashSet<>();
        
        // Adding elements
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        numbers.add(20); // Duplicate, will not be added
        
        System.out.println("Total numbers: " + numbers.size()); // Output: 3
        
        // Check if collection is empty
        if (!numbers.isEmpty()) {
            System.out.println("Collection has elements");
        }
        
        // Clear the collection
        // numbers.clear();
        // System.out.println("After clear: " + numbers.size()); // Would output: 0
    }
}
```

**Example 3: Working with Collection Interface Methods**

```java
import java.util.*;

public class CollectionExample3 {
    public static void main(String[] args) {
        Collection<String> cities = new ArrayList<>();
        
        // Adding multiple cities
        cities.add("New York");
        cities.add("London");
        cities.add("Tokyo");
        cities.add("Paris");
        
        // Using common methods
        System.out.println("Number of cities: " + cities.size());
        System.out.println("Is empty? " + cities.isEmpty());
        System.out.println("Contains 'London'? " + cities.contains("London"));
        
        // Iterating using iterator
        Iterator<String> iterator = cities.iterator();
        System.out.println("\nCities:");
        while (iterator.hasNext()) {
            System.out.println("  - " + iterator.next());
        }
        
        // Convert to array
        Object[] citiesArray = cities.toArray();
        System.out.println("\nConverted to array, length: " + citiesArray.length);
    }
}

/* Output:
Number of cities: 4
Is empty? false
Contains 'London'? true

Cities:
  - New York
  - London
  - Tokyo
  - Paris

Converted to array, length: 4
*/
```

#### Key Takeaways

1. **Collection is the root interface** - All other collection types inherit from it.
2. **It defines universal methods** - Methods like `add()`, `remove()`, `contains()`, `size()`, `isEmpty()`, `clear()`, and `iterator()` are available in all collection types.
3. **No direct concrete implementation** - Use subclasses like `ArrayList`, `HashSet`, `LinkedList`, `PriorityQueue`, etc., which provide concrete implementations of the Collection interface.
4. **Universal contract** - Every concrete collection class must support the basic operations defined by the Collection interface, ensuring consistency across different collection types.
5. **Type-safe with Generics** - Always use generics (e.g., `Collection<String>`) to catch type errors at compile time rather than runtime.

---

## Difference Between Collection (Interface) and Collections (Utility Class)

### Extracted Content

- **Collection** is an interface which can be used to represent a group of individual objects as a single entity.
- **Collections** is a utility class present in `java.util.package` to define several utility methods (like Sorting, Searching..) for Collection objects.

### Detailed Explanation

These two terms sound similar, but they represent fundamentally different concepts in Java. Understanding the distinction is crucial for writing effective code.

#### Collection (Singular - Interface)

`Collection` is an **interface** that defines the contract for objects that store groups of elements.

**Key characteristics:**

- It is an **interface** (abstract contract defining methods)
- It represents the structure/container for holding objects
- Every implementation of Collection (ArrayList, HashSet, LinkedList, etc.) must provide these methods
- It defines "what" needs to be done (add, remove, search, iterate)
- Located in the `java.util` package
- Other interfaces like `List`, `Set`, and `Queue` extend the Collection interface

**Purpose:** To provide a common interface that all collection implementations follow.

#### Collections (Plural - Utility Class)

`Collections` is a **utility class** that provides static utility methods to operate on Collection objects.

**Key characteristics:**

- It is a **class** (not an interface)
- It provides **utility/helper methods** for collections
- All methods are **static** (you don't need to create an instance)
- It defines "how" things should be done (sorting algorithms, searching algorithms, etc.)
- Located in the `java.util` package
- Think of it as a toolbox for working with collections
- Examples: `sort()`, `reverse()`, `shuffle()`, `binarySearch()`, `max()`, `min()`

**Purpose:** To provide reusable algorithms and utilities for manipulating and analyzing collections.

### Comparison Table

| Feature | Collection (Interface) | Collections (Utility Class) |
|---------|------------------------|----------------------------|
| **Type** | Interface | Class |
| **Purpose** | Defines contract for collection data structures | Provides utility methods for collections |
| **Methods are** | Abstract (must be implemented) | Static (direct use) |
| **Usage** | Implement this to create custom collections | Use static methods directly |
| **Location** | `java.util.Collection` | `java.util.Collections` |
| **Instantiation** | Via concrete implementations (ArrayList, HashSet) | Not instantiated (all static) |
| **Examples of methods** | add(), remove(), size(), iterator() | sort(), reverse(), shuffle(), binarySearch() |

### Code Examples

#### Example 1: Using Collection Interface

```java
import java.util.*;

public class CollectionInterfaceExample {
    public static void main(String[] args) {
        // Collection is an interface - we use a concrete implementation
        Collection<Integer> numbers = new ArrayList<>();
        
        // Using Collection interface methods
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        numbers.add(10);
        numbers.add(30);
        
        System.out.println("Collection: " + numbers);
        System.out.println("Size: " + numbers.size());
        System.out.println("Contains 20? " + numbers.contains(20));
    }
}

/* Output:
Collection: [50, 20, 40, 10, 30]
Size: 5
Contains 20? true
*/
```

#### Example 2: Using Collections Utility Class for Sorting

```java
import java.util.*;

public class CollectionsUtilityExample {
    public static void main(String[] args) {
        // Create a collection using the Collection interface
        List<Integer> numbers = new ArrayList<>();
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        numbers.add(10);
        numbers.add(30);
        
        System.out.println("Original collection: " + numbers);
        
        // Using Collections utility class methods (static methods)
        Collections.sort(numbers);
        System.out.println("After sort: " + numbers);
        
        Collections.reverse(numbers);
        System.out.println("After reverse: " + numbers);
        
        System.out.println("Min value: " + Collections.min(numbers));
        System.out.println("Max value: " + Collections.max(numbers));
    }
}

/* Output:
Original collection: [50, 20, 40, 10, 30]
After sort: [10, 20, 30, 40, 50]
After reverse: [50, 40, 30, 20, 10]
Min value: 10
Max value: 50
*/
```

#### Example 3: Collections Utility Methods - Searching

```java
import java.util.*;

public class CollectionsSearchExample {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
        fruits.add("Date");
        fruits.add("Elderberry");
        
        System.out.println("Fruits collection: " + fruits);
        
        // Collections utility method - binarySearch
        // NOTE: Collection must be sorted for binarySearch to work correctly
        Collections.sort(fruits);
        System.out.println("After sorting: " + fruits);
        
        int index = Collections.binarySearch(fruits, "Cherry");
        System.out.println("Index of 'Cherry': " + index);
        
        // Using Collections.frequency to count occurrences
        fruits.add("Apple");
        System.out.println("After adding another Apple: " + fruits);
        int count = Collections.frequency(fruits, "Apple");
        System.out.println("Frequency of 'Apple': " + count);
    }
}

/* Output:
Fruits collection: [Apple, Banana, Cherry, Date, Elderberry]
After sorting: [Apple, Banana, Cherry, Date, Elderberry]
Index of 'Cherry': 2
After adding another Apple: [Apple, Banana, Cherry, Date, Elderberry, Apple]
Frequency of 'Apple': 2
*/
```

#### Example 4: Comprehensive Example - Both Collection and Collections

```java
import java.util.*;

public class CollectionVsCollectionsDemo {
    public static void main(String[] args) {
        // Step 1: Create a Collection using the Collection interface
        Collection<String> names = new ArrayList<>();
        names.add("Zara");
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");
        names.add("Diana");
        
        System.out.println("=== Using Collection Interface ===");
        System.out.println("Original names: " + names);
        System.out.println("Total elements: " + names.size());
        System.out.println("Contains 'Bob'? " + names.contains("Bob"));
        
        // Step 2: Convert to List (which extends Collection)
        List<String> namesList = new ArrayList<>(names);
        
        // Step 3: Use Collections utility class for operations
        System.out.println("\n=== Using Collections Utility Class ===");
        Collections.sort(namesList);
        System.out.println("Sorted: " + namesList);
        
        Collections.reverse(namesList);
        System.out.println("Reversed: " + namesList);
        
        Collections.shuffle(namesList);
        System.out.println("Shuffled: " + namesList);
        
        // Find position of an element
        Collections.sort(namesList); // Sort first
        int position = Collections.binarySearch(namesList, "Charlie");
        System.out.println("Position of 'Charlie': " + position);
        
        // Get min and max
        System.out.println("Alphabetically first: " + Collections.min(namesList));
        System.out.println("Alphabetically last: " + Collections.max(namesList));
    }
}

/* Output:
=== Using Collection Interface ===
Original names: [Zara, Alice, Bob, Charlie, Diana]
Total elements: 5
Contains 'Bob'? true

=== Using Collections Utility Class ===
Sorted: [Alice, Bob, Charlie, Diana, Zara]
Reversed: [Zara, Diana, Charlie, Bob, Alice]
Shuffled: [Charlie, Alice, Diana, Bob, Zara]
Position of 'Charlie': 2
Alphabetically first: Alice
Alphabetically last: Zara
*/
```

### Common Collections Utility Methods

| Method | Purpose | Example |
|--------|---------|---------|
| `sort(List<T> list)` | Sorts a list in natural order | `Collections.sort(list)` |
| `reverse(List<?> list)` | Reverses the order of elements | `Collections.reverse(list)` |
| `shuffle(List<?> list)` | Randomly shuffles the list | `Collections.shuffle(list)` |
| `binarySearch(...)` | Searches for element in sorted list | `Collections.binarySearch(list, value)` |
| `min(Collection<? extends T> coll)` | Returns minimum element | `Collections.min(list)` |
| `max(Collection<? extends T> coll)` | Returns maximum element | `Collections.max(list)` |
| `frequency(Collection<?> c, Object o)` | Counts occurrences of element | `Collections.frequency(list, obj)` |
| `copy(List<? super T> dest, List<? extends T> src)` | Copies one list to another | `Collections.copy(destList, srcList)` |
| `replaceAll(List<T> list, T oldVal, T newVal)` | Replaces all occurrences | `Collections.replaceAll(list, old, new)` |
| `fills(List<? super T> list, T obj)` | Fills entire list with one value | `Collections.fill(list, value)` |

### Key Takeaways

1. **Collection (interface)** = The blueprint/contract for storing objects as a group
2. **Collections (class)** = The toolbox of static utility methods for operating on collections
3. **Think of it this way:**
   - Collection: "This is the data container"
   - Collections: "These are the operations/algorithms I can perform on the container"
4. **Both are in `java.util` package** but they serve different purposes
5. **Collections class is like a helper friend** - you don't instantiate it, you just call its static methods when you need to do sorting, searching, or other operations
6. **Always create instances of concrete classes** (ArrayList, HashSet, etc.) that implement the Collection interface
7. **Always use Collections utility methods** when you need common operations like sorting or searching instead of writing your own code

---

## Java Collection Framework vs C++ STL (Standard Template Library)

The concepts behind Java's Collection Framework are not new. C++ has similar functionality through its Standard Template Library (STL). Understanding the parallels between Java and C++ helps deepen your understanding of the underlying design patterns.

### Core Comparison: Java vs C++

| Concept | Java | C++ |
|---------|------|-----|
| **Container concept** | Collection Interface | STL Containers (vector, list, set, map, etc.) |
| **Dynamic Array** | ArrayList | std::vector |
| **Linked List** | LinkedList | std::list |
| **Unique elements** | HashSet | std::set or std::unordered_set |
| **Key-value pairs** | HashMap | std::map or std::unordered_map |
| **Utility methods** | Collections class (static methods) | STL Algorithms (std::sort, std::find, etc.) |
| **Iterator** | Iterator interface | Iterator (similar concept) |
| **Package/Library** | java.util | \<vector>, \<list>, \<set>, \<map>, \<algorithm> headers |

### Java Collection vs C++ Container

#### Java: Collection Interface + Implementations

```java
import java.util.*;

public class JavaCollectionExample {
    public static void main(String[] args) {
        // Using Collection interface with ArrayList (similar to C++ vector)
        Collection<Integer> numbers = new ArrayList<>();
        
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        
        System.out.println("Java Collection: " + numbers);
        System.out.println("Size: " + numbers.size());
        System.out.println("Contains 20? " + numbers.contains(20));
    }
}

/* Output:
Java Collection: [50, 20, 40]
Size: 3
Contains 20? true
*/
```

#### C++: STL Vector (Equivalent)

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    // Using C++ vector (similar to Java ArrayList)
    vector<int> numbers;
    
    numbers.push_back(50);
    numbers.push_back(20);
    numbers.push_back(40);
    
    cout << "C++ Vector: ";
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << "\nSize: " << numbers.size() << endl;
    
    // Checking if element exists (no built-in contains, need to use find)
    auto it = find(numbers.begin(), numbers.end(), 20);
    if (it != numbers.end()) {
        cout << "Contains 20? true" << endl;
    }
    
    return 0;
}

/* Output:
C++ Vector: 50 20 40 
Size: 3
Contains 20? true
*/
```

### Collections vs STL Algorithms

#### Java: Collections Utility Class

```java
import java.util.*;

public class JavaCollectionsExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        numbers.add(10);
        numbers.add(30);
        
        System.out.println("Original: " + numbers);
        
        // Using Collections utility methods
        Collections.sort(numbers);
        System.out.println("Sorted: " + numbers);
        
        Collections.reverse(numbers);
        System.out.println("Reversed: " + numbers);
        
        System.out.println("Min: " + Collections.min(numbers));
        System.out.println("Max: " + Collections.max(numbers));
    }
}

/* Output:
Original: [50, 20, 40, 10, 30]
Sorted: [10, 20, 30, 40, 50]
Reversed: [50, 40, 30, 20, 10]
Min: 10
Max: 50
*/
```

#### C++: STL Algorithms

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    vector<int> numbers = {50, 20, 40, 10, 30};
    
    cout << "Original: ";
    for (int num : numbers) cout << num << " ";
    cout << "\n";
    
    // Using STL algorithms
    sort(numbers.begin(), numbers.end());
    cout << "Sorted: ";
    for (int num : numbers) cout << num << " ";
    cout << "\n";
    
    reverse(numbers.begin(), numbers.end());
    cout << "Reversed: ";
    for (int num : numbers) cout << num << " ";
    cout << "\n";
    
    auto minVal = *min_element(numbers.begin(), numbers.end());
    auto maxVal = *max_element(numbers.begin(), numbers.end());
    
    cout << "Min: " << minVal << "\nMax: " << maxVal << endl;
    
    return 0;
}

/* Output:
Original: 50 20 40 10 30 
Sorted: 10 20 30 40 50 
Reversed: 50 40 30 20 10 
Min: 10
Max: 50
*/
```

### Specific Collection Type Comparisons

#### 1. ArrayList vs std::vector

**Java ArrayList:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");      // O(1) amortized
fruits.remove(0);         // O(n) - needs shifting
fruits.get(0);            // O(1)
fruits.set(0, "Banana");  // O(1)
```

**C++ std::vector:**
```cpp
vector<string> fruits;
fruits.push_back("Apple");      // O(1) amortized
fruits.erase(fruits.begin());   // O(n) - needs shifting
fruits[0];                       // O(1)
fruits[0] = "Banana";            // O(1)
```

#### 2. HashSet vs std::unordered_set

**Java HashSet:**
```java
Set<String> uniqueTags = new HashSet<>();
uniqueTags.add("Java");
uniqueTags.add("Python");
uniqueTags.add("Java");        // Ignored, duplicates not allowed
System.out.println(uniqueTags.size()); // Output: 2
```

**C++ std::unordered_set:**
```cpp
unordered_set<string> uniqueTags;
uniqueTags.insert("Java");
uniqueTags.insert("Python");
uniqueTags.insert("Java");     // Ignored, duplicates not allowed
cout << uniqueTags.size();     // Output: 2
```

#### 3. HashMap vs std::map

**Java HashMap:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 90);
scores.put("Bob", 85);
System.out.println(scores.get("Alice"));  // Output: 90
scores.put("Alice", 95);                   // Updates existing value
```

**C++ std::map:**
```cpp
map<string, int> scores;
scores["Alice"] = 90;
scores["Bob"] = 85;
cout << scores["Alice"] << endl;  // Output: 90
scores["Alice"] = 95;              // Updates existing value
```

### Complete Example: Java vs C++ Side-by-Side

**Java Implementation:**
```java
import java.util.*;

public class PersonCollectionJava {
    public static void main(String[] args) {
        // Create a collection of names
        List<String> persons = new ArrayList<>();
        persons.add("Charlie");
        persons.add("Alice");
        persons.add("Diana");
        persons.add("Bob");
        
        System.out.println("Original order: " + persons);
        System.out.println("Total persons: " + persons.size());
        
        // Sort using Collections utility
        Collections.sort(persons);
        System.out.println("Sorted order: " + persons);
        
        // Search using Collections utility
        int index = Collections.binarySearch(persons, "Bob");
        System.out.println("Position of 'Bob': " + index);
        
        // Iterate and print
        System.out.println("Iterating:");
        for (String person : persons) {
            System.out.println("  - " + person);
        }
    }
}

/* Output:
Original order: [Charlie, Alice, Diana, Bob]
Total persons: 4
Sorted order: [Alice, Bob, Charlie, Diana]
Position of 'Bob': 1
Iterating:
  - Alice
  - Bob
  - Charlie
  - Diana
*/
```

**C++ Equivalent:**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    // Create a vector of strings
    vector<string> persons = {"Charlie", "Alice", "Diana", "Bob"};
    
    cout << "Original order: ";
    for (const auto& p : persons) cout << p << " ";
    cout << "\nTotal persons: " << persons.size() << "\n";
    
    // Sort using STL algorithm
    sort(persons.begin(), persons.end());
    cout << "Sorted order: ";
    for (const auto& p : persons) cout << p << " ";
    cout << "\n";
    
    // Search using STL algorithm
    auto it = binary_search(persons.begin(), persons.end(), "Bob");
    cout << "Contains 'Bob'? " << (it ? "true" : "false") << "\n";
    
    auto pos = lower_bound(persons.begin(), persons.end(), "Bob");
    int index = distance(persons.begin(), pos);
    cout << "Position of 'Bob': " << index << "\n";
    
    // Iterate and print
    cout << "Iterating:\n";
    for (const auto& person : persons) {
        cout << "  - " << person << "\n";
    }
    
    return 0;
}

/* Output:
Original order: Charlie Alice Diana Bob 
Total persons: 4
Sorted order: Alice Bob Charlie Diana 
Contains 'Bob'? 1
Position of 'Bob': 1
Iterating:
  - Alice
  - Bob
  - Charlie
  - Diana
*/
```

### Key Differences: Java vs C++

| Aspect | Java | C++ |
|--------|------|-----|
| **Memory management** | Automatic (Garbage Collector) | Manual or Smart pointers |
| **Generic syntax** | `List<String>` | `vector<string>` or `std::vector<std::string>` |
| **Adding elements** | `list.add(element)` | `vec.push_back(element)` |
| **Removing elements** | `list.remove(element)` | `vec.erase(iterator)` |
| **Accessing elements** | `list.get(index)` | `vec[index]` or `vec.at(index)` |
| **Size** | `list.size()` | `vec.size()` |
| **Sorting** | `Collections.sort(list)` | `std::sort(vec.begin(), vec.end())` |
| **Finding** | `list.contains(element)` or `Collections.binarySearch()` | `std::find()` or `std::binary_search()` |

### Understanding the Philosophy

Both Java and C++ collections are based on the same underlying principle: **Separate the data structure (Container) from the algorithms (Utilities).**

- **Java**: Collections (interface) + Collections (utility class)
- **C++**: Containers + STL Algorithms

This separation allows:
1. Different implementations of containers for different use cases
2. Reusable algorithms that work with any container
3. Flexibility and extensibility

### Key Takeaways

1. **Java Collection ~ C++ Container** - Both represent a group of objects
2. **ArrayList ~ std::vector** - Both are dynamic arrays
3. **HashSet ~ std::unordered_set** - Both store unique elements
4. **HashMap ~ std::map** - Both store key-value pairs
5. **Collections class ~ STL Algorithms** - Both provide utility operations
6. **The design pattern is universal** - Whether Java or C++, the concepts of containers, iterators, and algorithms are the same
7. **Learning one helps you learn the other** - Understanding Collections in Java makes it easier to understand STL in C++, and vice versa

---

## Interface 2: List (Child Interface of Collection)

### Extracted Content

- **List is a child interface of Collection.**
- If we want to represent a group of individual objects as a single entity where **duplicates are allowed** and **insertion order is preserved**, we should go for List.

### Detailed Explanation

The `List` interface extends the `Collection` interface and adds additional functionality for ordered collections. While Collection provides the basic contract for all collections, List adds the concept of **position** and **order**.

#### Key Characteristics of List

1. **Ordered Collection** - Elements maintain their insertion order. The first element added stays first unless explicitly moved.

2. **Allows Duplicates** - Unlike a Set, a List can contain multiple identical elements.

3. **Index-Based Access** - Elements can be accessed by position (index), similar to arrays. The first element is at index 0.

4. **Position-Based Operations** - You can insert, remove, and retrieve elements at specific positions.

5. **Implements Collection Interface** - List inherits all methods from Collection and adds index-based methods.

#### Why Use List?

Use List when you need:

- To maintain the order in which elements were added
- To allow duplicate elements
- To access elements by their position (index)
- To insert or remove elements at specific positions
- A more flexible alternative to arrays with order and duplicate support

#### List Interface Hierarchy

```
Collection (I)
    └── List (I)
            ├── ArrayList (1.2u)
            ├── LinkedList (1.2u)
            ├── Vector (1.0u) [Legacy]
            └── Stack (1.0u) [Legacy - extends Vector]
```

**Note:** u = update version (1.0u = Java 1.0, 1.2u = Java 1.2, etc.)

### Common List Implementations

| Implementation | Introduced | Key Feature | Use Case |
|---|---|---|---|
| **ArrayList** | Java 1.2 | Dynamic array, fast access by index | Most common, general purpose |
| **LinkedList** | Java 1.2 | Doubly linked list, fast insertion/deletion | Frequent insertions and deletions |
| **Vector** | Java 1.0 | Synchronized ArrayList, thread-safe | Legacy, rarely used now |
| **Stack** | Java 1.0 | LIFO (Last In First Out) structure | Stack operations (push/pop) |

### Common Methods Defined in List Interface

| Method | Purpose | Example |
|--------|---------|---------|
| `add(int index, E element)` | Adds element at specific position | `list.add(0, "Java")` |
| `get(int index)` | Gets element at specific position | `String s = list.get(0)` |
| `set(int index, E element)` | Replaces element at position | `list.set(0, "Python")` |
| `remove(int index)` | Removes element at position | `list.remove(0)` |
| `indexOf(Object o)` | Finds first index of element | `int i = list.indexOf("Java")` |
| `lastIndexOf(Object o)` | Finds last index of element | `int i = list.lastIndexOf("Java")` |
| `subList(int from, int to)` | Gets elements from to position | `List sub = list.subList(0, 3)` |

### Code Examples

#### Example 1: ArrayList - Basic List Operations

```java
import java.util.*;

public class ListExample1 {
    public static void main(String[] args) {
        // Create an ArrayList (implements List interface)
        List<String> languages = new ArrayList<>();
        
        // Adding elements (preserves insertion order)
        languages.add("Java");
        languages.add("Python");
        languages.add("JavaScript");
        languages.add("Java");        // Duplicates are allowed
        
        System.out.println("Original list: " + languages);
        System.out.println("Size: " + languages.size());
        
        // Access by index (0-indexed)
        System.out.println("Element at index 0: " + languages.get(0));
        System.out.println("Element at index 3: " + languages.get(3));
        
        // Finding index of elements
        System.out.println("Index of 'Python': " + languages.indexOf("Python"));
        System.out.println("Last index of 'Java': " + languages.lastIndexOf("Java"));
        
        // Modifying elements at specific position
        languages.set(1, "C++");
        System.out.println("After set: " + languages);
        
        // Removing element at specific position
        languages.remove(2);
        System.out.println("After remove(2): " + languages);
    }
}

/* Output:
Original list: [Java, Python, JavaScript, Java]
Size: 4
Element at index 0: Java
Element at index 3: Java
Index of 'Python': 1
Last index of 'Java': 3
After set: [Java, C++, JavaScript, Java]
After remove(2): [Java, C++, Java]
*/
```

#### Example 2: LinkedList vs ArrayList Performance

```java
import java.util.*;

public class ListComparisonExample {
    public static void main(String[] args) {
        List<Integer> arrayList = new ArrayList<>();
        List<Integer> linkedList = new LinkedList<>();
        
        // Add elements
        for (int i = 1; i <= 5; i++) {
            arrayList.add(i);
            linkedList.add(i);
        }
        
        System.out.println("ArrayList: " + arrayList);
        System.out.println("LinkedList: " + linkedList);
        
        // Insert at beginning
        arrayList.add(0, 0);           // O(n) - needs shifting
        linkedList.add(0, 0);          // O(1) - just pointer update
        
        System.out.println("After inserting at beginning:");
        System.out.println("ArrayList: " + arrayList);
        System.out.println("LinkedList: " + linkedList);
        
        // Access by index
        System.out.println("ArrayList get(0): " + arrayList.get(0));  // O(1)
        System.out.println("LinkedList get(0): " + linkedList.get(0)); // O(n)
        
        // Remove from middle
        arrayList.remove(3);
        linkedList.remove(3);
        
        System.out.println("After removing index 3:");
        System.out.println("ArrayList: " + arrayList);
        System.out.println("LinkedList: " + linkedList);
    }
}

/* Output:
ArrayList: [1, 2, 3, 4, 5]
LinkedList: [1, 2, 3, 4, 5]
After inserting at beginning:
ArrayList: [0, 1, 2, 3, 4, 5]
LinkedList: [0, 1, 2, 3, 4, 5]
ArrayList get(0): 0
LinkedList get(0): 0
After removing index 3:
ArrayList: [0, 1, 2, 4, 5]
LinkedList: [0, 1, 2, 4, 5]
*/
```

#### Example 3: List with Duplicates

```java
import java.util.*;

public class ListDuplicatesExample {
    public static void main(String[] args) {
        // List allows duplicates
        List<String> fruits = new ArrayList<>();
        
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Apple");
        fruits.add("Cherry");
        fruits.add("Apple");
        
        System.out.println("Fruits list: " + fruits);
        System.out.println("Size: " + fruits.size());
        System.out.println("Contains 'Apple'? " + fruits.contains("Apple"));
        
        // Find all indices of 'Apple'
        int index = 0;
        System.out.println("All indices of 'Apple':");
        while ((index = fruits.indexOf("Apple", index)) != -1) {
            System.out.println("  Found at index: " + index);
            index++;
        }
        
        // Count occurrences manually
        int count = 0;
        for (String fruit : fruits) {
            if (fruit.equals("Apple")) {
                count++;
            }
        }
        System.out.println("Total 'Apple' count: " + count);
    }
}

/* Output:
Fruits list: [Apple, Banana, Apple, Cherry, Apple]
Size: 5
Contains 'Apple'? true
All indices of 'Apple':
  Found at index: 0
  Found at index: 2
  Found at index: 4
Total 'Apple' count: 3
*/
```

#### Example 4: Ordering vs Other Collections

```java
import java.util.*;

public class OrderingComparisonExample {
    public static void main(String[] args) {
        // List - maintains insertion order
        List<String> list = new ArrayList<>();
        list.add("Zebra");
        list.add("Apple");
        list.add("Banana");
        
        System.out.println("=== List (maintains insertion order) ===");
        System.out.println("List: " + list);
        
        // Set - does NOT maintain order (at least not HashSet)
        Set<String> set = new HashSet<>();
        set.add("Zebra");
        set.add("Apple");
        set.add("Banana");
        
        System.out.println("\n=== Set (no order guaranteed) ===");
        System.out.println("Set: " + set);  // Order may vary
        
        // LinkedHashSet - maintains insertion order
        Set<String> linkedSet = new LinkedHashSet<>();
        linkedSet.add("Zebra");
        linkedSet.add("Apple");
        linkedSet.add("Banana");
        
        System.out.println("\n=== LinkedHashSet (maintains insertion order) ===");
        System.out.println("LinkedHashSet: " + linkedSet);
    }
}

/* Output:
=== List (maintains insertion order) ===
List: [Zebra, Apple, Banana]

=== Set (no order guaranteed) ===
Set: [Apple, Banana, Zebra]  // Order may vary

=== LinkedHashSet (maintains insertion order) ===
LinkedHashSet: [Zebra, Apple, Banana]
*/
```

#### Example 5: Sublist Operations

```java
import java.util.*;

public class SublistExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        for (int i = 1; i <= 10; i++) {
            numbers.add(i);
        }
        
        System.out.println("Original list: " + numbers);
        
        // Get a sublist from index 2 to 7 (exclusive)
        List<Integer> sublist = numbers.subList(2, 7);
        System.out.println("Sublist (from 2 to 7): " + sublist);
        
        // Modify the sublist
        Collections.fill(sublist, 99);
        System.out.println("After fill(99) on sublist: " + numbers);
        
        // Get another sublist
        List<Integer> anotherSublist = numbers.subList(0, 3);
        System.out.println("Another sublist (0 to 3): " + anotherSublist);
    }
}

/* Output:
Original list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Sublist (from 2 to 7): [3, 4, 5, 6, 7]
After fill(99) on sublist: [1, 2, 99, 99, 99, 99, 99, 8, 9, 10]
Another sublist (0 to 3): [1, 2, 99]
*/
```

### List vs Other Collection Types

| Feature | List | Set | Queue |
|---------|------|-----|-------|
| **Duplicates** | Allowed | Not allowed | Allowed |
| **Order** | Insertion order preserved | No guaranteed order (except LinkedHashSet) | FIFO or Priority order |
| **Access** | By index (get, set, remove by index) | No index access | Limited (peek, poll) |
| **Implementation** | ArrayList, LinkedList, Vector | HashSet, TreeSet, LinkedHashSet | LinkedList, PriorityQueue |
| **Speed of access** | O(1) for ArrayList, O(n) for LinkedList | O(1) average for HashSet | O(1) for peek/poll |
| **Speed of insertion** | O(1) for ArrayList end, O(n) for middle | O(1) average | O(1) for offer |

### When to Use Which List Implementation

| ArrayList | LinkedList | Vector | Stack |
|-----------|-----------|--------|-------|
| **Random access**High frequency | **Frequent insertions/deletions** | **Thread-safe operations** | **LIFO operations** |
| **Few insertions/deletions** | **Queue-like behavior needed** | **Legacy code compatibility** | **Undo/Redo functionality** |
| **Most common choice** | **Less common, specific use cases** | **Avoid in new code** | **Specialized use case** |

### Key Takeaways

1. **List extends Collection** - It inherits all Collection methods and adds index-based methods.
2. **Ordered and allows duplicates** - Unlike sets, lists preserve order and allow duplicate elements.
3. **Index-based access** - Elements can be accessed, inserted, or removed by position.
4. **ArrayList is the default** - Use ArrayList unless you have specific performance needs (e.g., ArrayList for random access, LinkedList for frequent insertions).
5. **Preserve insertion order** - The order in which you add elements is maintained (even if you use Collections.sort()).
6. **Performance trade-offs** - ArrayList is fast for access but slow for insertions in the middle; LinkedList is fast for insertions but slow for random access.
7. **Common implementations** - ArrayList and LinkedList are the most frequently used; Vector and Stack are legacy and should be avoided in new code.

---

## Interface 3: Set (Child Interface of Collection)

### Extracted Content

- **Set is a child interface of Collection.**
- If we want to represent a group of individual objects as a single entity where **duplicates are not allowed** and **insertion order is not preserved**, we should go for Set.

### Detailed Explanation

The `Set` interface extends the `Collection` interface and represents a collection that **cannot contain duplicate elements**. A Set is like a mathematical set where each element is unique.

#### Key Characteristics of Set

1. **No Duplicates** - A Set automatically rejects duplicate elements. If you try to add a duplicate, it will be silently ignored.

2. **Unordered** - Unlike List, Set does NOT guarantee any particular order of elements (except LinkedHashSet which maintains insertion order).

3. **No Index-Based Access** - Sets do not support indexed access. You cannot use `get(index)` or `set(index)`.

4. **Mathematical Set Operations** - Sets support operations like union, intersection, and difference.

5. **Inherits from Collection** - Set inherits all methods from Collection but adds no new methods.

#### Set Interface Hierarchy

```
Collection (I)
    └── Set (I) [1.2 version]
            ├── HashSet (1.2 version)
            │       └── LinkedHashSet (1.4 version)
            ├── TreeSet (1.2 version)
            └── EnumSet (1.5 version)
```

### Common Set Implementations

| Implementation | Order | Performance | Use Case |
|---|---|---|---|
| **HashSet** | No/Random | O(1) average | Default choice, general purpose |
| **LinkedHashSet** | Insertion order | O(1) average | Need to maintain insertion order |
| **TreeSet** | Sorted order | O(log n) | Need elements in sorted order |
| **EnumSet** | N/A | Very fast | Only for Enum constants |

### Small Code Examples

#### Example 1: HashSet - No Duplicates

```java
import java.util.*;

public class SetExample1 {
    public static void main(String[] args) {
        Set<String> fruits = new HashSet<>();
        
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Apple");      // Duplicate, will be ignored
        fruits.add("Cherry");
        
        System.out.println("Set: " + fruits);  // [Apple, Banana, Cherry] or different order
        System.out.println("Size: " + fruits.size());  // 3, not 4
        System.out.println("Contains Apple? " + fruits.contains("Apple"));
    }
}

/* Output:
Set: [Apple, Banana, Cherry]
Size: 3
Contains Apple? true
*/
```

#### Example 2: LinkedHashSet - Maintains Order

```java
import java.util.*;

public class SetExample2 {
    public static void main(String[] args) {
        Set<Integer> hashSet = new HashSet<>();
        Set<Integer> linkedSet = new LinkedHashSet<>();
        
        int[] numbers = {5, 2, 8, 2, 9, 5};
        
        for (int num : numbers) {
            hashSet.add(num);
            linkedSet.add(num);
        }
        
        System.out.println("HashSet (no order): " + hashSet);
        System.out.println("LinkedHashSet (insertion order): " + linkedSet);
    }
}

/* Output:
HashSet (no order): [2, 5, 8, 9]
LinkedHashSet (insertion order): [5, 2, 8, 9]
*/
```

#### Example 3: TreeSet - Sorted Order

```java
import java.util.*;

public class SetExample3 {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>();
        
        treeSet.add("Zebra");
        treeSet.add("Apple");
        treeSet.add("Banana");
        treeSet.add("Apple");  // Duplicate ignored
        
        System.out.println("TreeSet (sorted): " + treeSet);
        System.out.println("First: " + ((TreeSet)treeSet).first());
        System.out.println("Last: " + ((TreeSet)treeSet).last());
    }
}

/* Output:
TreeSet (sorted): [Apple, Banana, Zebra]
First: Apple
Last: Zebra
*/
```

#### Example 4: Set Operations

```java
import java.util.*;

public class SetOperationsExample {
    public static void main(String[] args) {
        Set<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
        Set<Integer> set2 = new HashSet<>(Arrays.asList(4, 5, 6, 7, 8));
        
        // Union
        Set<Integer> union = new HashSet<>(set1);
        union.addAll(set2);
        System.out.println("Union: " + union);  // [1, 2, 3, 4, 5, 6, 7, 8]
        
        // Intersection
        Set<Integer> intersection = new HashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Intersection: " + intersection);  // [4, 5]
        
        // Difference
        Set<Integer> difference = new HashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Difference: " + difference);  // [1, 2, 3]
    }
}

/* Output:
Union: [1, 2, 3, 4, 5, 6, 7, 8]
Intersection: [4, 5]
Difference: [1, 2, 3]
*/
```

### When to Use Each Set Implementation

| Use HashSet | Use LinkedHashSet | Use TreeSet |
|---|---|---|
| General purpose collections | Need insertion order preserved | Need sorted elements |
| No specific order needed | Rare, but specific use cases | Frequent searching/range queries |
| Best performance needed | Slightly slower than HashSet | Slowest, but sorted |

### Set vs List - Quick Comparison

| Feature | Set | List |
|---------|-----|------|
| **Duplicates** | NOT allowed | Allowed |
| **Order** | No (except LinkedHashSet) | Yes, insertion order |
| **Index access** | NO | YES |
| **Performance (add/remove)** | O(1) HashSet, O(log n) TreeSet | O(n) for middle elements |
| **Use when** | Need unique elements | Need ordered collection with duplicates |

### Key Takeaways

1. **Set guarantees uniqueness** - No duplicate elements allowed; duplicates are silently rejected.
2. **Three common implementations** - HashSet (default), LinkedHashSet (order), TreeSet (sorted).
3. **No index-based access** - Cannot use `get()`, `set()`, or `remove(index)` methods.
4. **HashSet is fastest** - Use HashSet unless you specifically need order (LinkedHashSet) or sorting (TreeSet).
5. **Inherits Collection methods** - All Collection methods like `add()`, `remove()`, `contains()` work.
6. **Great for uniqueness** - Perfect when you need to eliminate duplicates or check membership.
7. **Set operations** - Supports union, intersection, and difference using `addAll()`, `retainAll()`, `removeAll()`.

---

## Difference Between List and Set

### Extracted Content

- **List**: Duplicates are allowed, and insertion order is preserved.
- **Set**: Duplicates are not allowed, and insertion order is generally not preserved.

### Proper Explanation

Both `List` and `Set` are child interfaces of `Collection`, but they are used for different goals:

| Feature | List | Set |
|---|---|---|
| Duplicates | Allowed | Not allowed |
| Insertion order | Preserved | Not guaranteed (except `LinkedHashSet`) |
| Index-based access | Available (`get`, `set`, `add(index)`) | Not available |
| Best use case | Ordered data, repeated values | Unique data, de-duplication |

### Quick Rule

- Use `List` when order matters or duplicates are valid.
- Use `Set` when uniqueness matters.

---

## Interface 4: SortedSet

### Extracted Content

- `SortedSet` is a child interface of `Set`.
- Use `SortedSet` when duplicates are not allowed and elements must be maintained in sorted order.

### Proper Explanation

`SortedSet` keeps all elements unique (like `Set`) and automatically stores them in sorted order.

- Duplicates are not allowed.
- Order is based on natural ordering (`Comparable`) or a custom `Comparator`.
- Common implementation: `TreeSet`.

### Small Example

```java
import java.util.*;

public class SortedSetSmallExample {
    public static void main(String[] args) {
        SortedSet<Integer> marks = new TreeSet<>();
        marks.add(50);
        marks.add(10);
        marks.add(30);
        marks.add(10); // duplicate ignored

        System.out.println(marks);       // [10, 30, 50]
        System.out.println(marks.first()); // 10
        System.out.println(marks.last());  // 50
    }
}
```

---

## Interface 5: NavigableSet

### Extracted Content

- `NavigableSet` is a child interface of `SortedSet`.
- It adds methods mainly for navigation purposes.

### Proper Explanation

`NavigableSet` extends `SortedSet` by adding neighbor and range-navigation methods.

- `lower(x)`: greatest element strictly less than `x`
- `floor(x)`: greatest element less than or equal to `x`
- `ceiling(x)`: smallest element greater than or equal to `x`
- `higher(x)`: smallest element strictly greater than `x`
- `pollFirst()`, `pollLast()`: remove and return boundary elements

Common implementation is also `TreeSet` (it implements `NavigableSet`).

### Small Example

```java
import java.util.*;

public class NavigableSetSmallExample {
    public static void main(String[] args) {
        NavigableSet<Integer> nums = new TreeSet<>(Arrays.asList(10, 20, 30, 40));

        System.out.println(nums.floor(25));   // 20
        System.out.println(nums.ceiling(25)); // 30
        System.out.println(nums.lower(20));   // 10
        System.out.println(nums.higher(20));  // 30
    }
}
```

### Hierarchy Snapshot (from the slide)

```text
Collection (1.2)
  -> Set (1.2)
      -> SortedSet (1.2)
          -> NavigableSet (1.6)
              -> TreeSet (class)
```

### Quick Rule

- Use `Set` when you only need uniqueness.
- Use `SortedSet` when you need uniqueness + sorted order.
- Use `NavigableSet` when you need uniqueness + sorted order + nearest-element navigation.

---

## Interface 6: Queue

### Extracted Content

- `Queue` is a child interface of `Collection`.
- If we want to represent a group of objects before processing, we should use `Queue`.
- Typical processing order is FIFO (First In, First Out).
- Example idea from slide: mail IDs are stored first and then processed in the same order.

### Proper Explanation

`Queue` is designed for processing elements in a sequence, usually FIFO.

- Insert at tail: `offer()` / `add()`
- Read head: `peek()`
- Remove head: `poll()` / `remove()`

Unlike `List`, a `Queue` is not mainly for random index-based access. It is for workflow-style processing (tasks, requests, events, messages).

### Hierarchy Snapshot (from slide)

```text
Collection (1.2)
  -> Queue (1.5)
      -> PriorityQueue (class, 1.5)
      -> BlockingQueue (interface, 1.5)
          -> LinkedBlockingQueue (class, 1.5)
          -> PriorityBlockingQueue (class, 1.5)
```

### Small Examples

#### Example 1: FIFO behavior with `LinkedList` as `Queue`

```java
import java.util.*;

public class QueueFifoExample {
    public static void main(String[] args) {
        Queue<String> mailQueue = new LinkedList<>();
        mailQueue.offer("mail-1");
        mailQueue.offer("mail-2");
        mailQueue.offer("mail-3");

        System.out.println(mailQueue.poll()); // mail-1
        System.out.println(mailQueue.poll()); // mail-2
        System.out.println(mailQueue.poll()); // mail-3
    }
}
```

#### Example 2: `PriorityQueue` (not FIFO, sorted by priority)

```java
import java.util.*;

public class PriorityQueueExample {
    public static void main(String[] args) {
        Queue<Integer> pq = new PriorityQueue<>();
        pq.offer(30);
        pq.offer(10);
        pq.offer(20);

        System.out.println(pq.poll()); // 10
        System.out.println(pq.poll()); // 20
        System.out.println(pq.poll()); // 30
    }
}
```

### Quick Rule

- Use `Queue` when data must be processed in sequence.
- Use `PriorityQueue` when highest/lowest priority should be processed first.

---

## Important Note: Collection Interfaces vs Map

### Extracted Content

- `Collection`, `List`, `Set`, `SortedSet`, `NavigableSet`, and `Queue` are for representing a group of individual objects.
- If we need key-value pair representation, we should use `Map`.

### Proper Explanation

- `Collection` hierarchy: stores single values (elements).
- `Map` hierarchy: stores key-value pairs (`key -> value`).

Small example:

```java
import java.util.*;

public class CollectionVsMapExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("A", "B", "C"); // values only

        Map<Integer, String> idToName = new HashMap<>();
        idToName.put(101, "A");
        idToName.put(102, "B");

        System.out.println(names);      // [A, B, C]
        System.out.println(idToName);   // {101=A, 102=B}
    }
}
```

---

## Interface 7: Map

### Extracted Content

- `Map` is **not** a child interface of `Collection`.
- Use `Map` when data should be represented as **key-value pairs**.
- Both keys and values are objects.
- Duplicate keys are not allowed, but duplicate values are allowed.

### Proper Explanation

`Map<K, V>` is used when each value must be accessed through a unique key.

- Key uniqueness: each key can appear only once.
- Value duplication: multiple keys can have the same value.
- If the same key is inserted again, old value gets replaced.

Example from slide idea:

- `101 -> Durga`
- `102 -> Ravi`
- `103 -> Venkat`

This is exactly a `Map<Integer, String>` use case.

### Hierarchy Snapshot (from slide)

```text
Map (interface, 1.2)
  -> HashMap (class, 1.2)
      -> LinkedHashMap (class, 1.4)
  -> WeakHashMap (class, 1.2)
  -> IdentityHashMap (class, 1.4)
  -> Hashtable (class, 1.0)
      -> Properties (class, 1.0)

Dictionary (abstract class, legacy, 1.0)
  -> Hashtable
```

### Small Examples

#### Example 1: Basic Map usage (student roll number -> name)

```java
import java.util.*;

public class MapSmallExample1 {
    public static void main(String[] args) {
        Map<Integer, String> students = new HashMap<>();
        students.put(101, "Durga");
        students.put(102, "Ravi");
        students.put(103, "Venkat");

        System.out.println(students.get(102)); // Ravi
        System.out.println(students);           // {101=Durga, 102=Ravi, 103=Venkat}
    }
}
```

#### Example 2: Duplicate key vs duplicate value

```java
import java.util.*;

public class MapSmallExample2 {
    public static void main(String[] args) {
        Map<Integer, String> m = new HashMap<>();
        m.put(1, "A");
        m.put(2, "A");     // duplicate value allowed
        m.put(1, "B");     // duplicate key: value replaced

        System.out.println(m); // {1=B, 2=A}
    }
}
```

### Quick Rule

- Use `Collection` interfaces (`List`, `Set`, `Queue`, etc.) for value collections.
- Use `Map` when you need key-based lookup and key-value modeling.

---

## Interface 8: SortedMap

### Extracted Content

- `SortedMap` is a child interface of `Map`.
- Use `SortedMap` when key-value pairs should be maintained according to sorted order of keys.

### Proper Explanation

`SortedMap<K, V>` stores entries in key-sorted order.

- Keys are unique (same as `Map`).
- Values can be duplicated.
- Sorting is by natural key order or custom `Comparator`.
- Common implementation: `TreeMap`.

### Hierarchy Snapshot (from slide)

```text
Map (1.2)
  -> SortedMap (1.2)
      -> TreeMap (class, 1.2)
```

### Small Example

```java
import java.util.*;

public class SortedMapSmallExample {
    public static void main(String[] args) {
        SortedMap<Integer, String> students = new TreeMap<>();
        students.put(103, "Venkat");
        students.put(101, "Durga");
        students.put(102, "Ravi");

        System.out.println(students);       // {101=Durga, 102=Ravi, 103=Venkat}
        System.out.println(students.firstKey()); // 101
        System.out.println(students.lastKey());  // 103
    }
}
```

---

## Interface 9: NavigableMap

### Extracted Content

- `NavigableMap` is a child interface of `SortedMap`.
- It defines utility methods for navigation.

### Proper Explanation

`NavigableMap<K, V>` extends `SortedMap` with nearest-key navigation methods.

- `lowerKey(k)`: greatest key strictly less than `k`
- `floorKey(k)`: greatest key less than or equal to `k`
- `ceilingKey(k)`: smallest key greater than or equal to `k`
- `higherKey(k)`: smallest key strictly greater than `k`
- `firstEntry()`, `lastEntry()`, `pollFirstEntry()`, `pollLastEntry()` for boundary entry operations

Common implementation: `TreeMap` (it implements `NavigableMap`).

### Hierarchy Snapshot (from slide)

```text
Map (1.2)
  -> SortedMap (1.2)
      -> NavigableMap (1.6)
          -> TreeMap (class, 1.2)
```

### Small Example

```java
import java.util.*;

public class NavigableMapSmallExample {
    public static void main(String[] args) {
        NavigableMap<Integer, String> m = new TreeMap<>();
        m.put(10, "A");
        m.put(20, "B");
        m.put(30, "C");

        System.out.println(m.floorKey(25));   // 20
        System.out.println(m.ceilingKey(25)); // 30
        System.out.println(m.lowerKey(20));   // 10
        System.out.println(m.higherKey(20));  // 30
    }
}
```

### Quick Rule

- Use `Map` for key-value storage.
- Use `SortedMap` for key-value storage with sorted keys.
- Use `NavigableMap` when you also need nearest-key navigation methods.

---

## Collection Framework Overview (Diagram Summary)

### Extracted Content (from overview diagrams)

- `Collection` is the root interface for `List`, `Set`, and `Queue` branches.
- `List` branch includes `ArrayList`, `LinkedList`, and legacy classes `Vector` and `Stack`.
- `Set` branch includes `HashSet`, `LinkedHashSet`, `SortedSet`, `NavigableSet`, and `TreeSet`.
- `Queue` branch includes `PriorityQueue` and `BlockingQueue` implementations.
- `Map` is a separate hierarchy with implementations like `HashMap`, `LinkedHashMap`, `WeakHashMap`, `IdentityHashMap`, `Hashtable`, and `Properties`.
- `Dictionary`, `Hashtable`, `Properties`, `Vector`, and `Stack` are shown as legacy-era classes.
- Extra concepts shown: Sorting (`Comparable`, `Comparator`), Cursors (`Enumeration`, `Iterator`, `ListIterator`), Utility classes (`Collections`, `Arrays`).

### Proper Explanation

The diagrams summarize the full idea of Java Collections in one view:

1. `Collection` hierarchy is for storing groups of elements.
2. `Map` hierarchy is for key-value data and is separate from `Collection`.
3. Modern code usually prefers `ArrayList`, `HashSet`, `TreeSet`, `PriorityQueue`, `HashMap`, and `TreeMap`.
4. Legacy classes (`Vector`, `Stack`, `Hashtable`, `Dictionary`) exist mostly for compatibility with old code.

### Clean Hierarchy Snapshot

```text
Collection (interface)
  -> List
      -> ArrayList
      -> LinkedList
      -> Vector (legacy)
          -> Stack (legacy)
  -> Set
      -> HashSet
          -> LinkedHashSet
      -> SortedSet
          -> NavigableSet
              -> TreeSet
  -> Queue
      -> PriorityQueue
      -> BlockingQueue
          -> LinkedBlockingQueue
          -> PriorityBlockingQueue

Map (separate interface hierarchy)
  -> HashMap
      -> LinkedHashMap
  -> WeakHashMap
  -> IdentityHashMap
  -> Hashtable (legacy)
      -> Properties (legacy utility for config-like key/value text)
```

### Small Examples

#### 1) Sorting Interfaces

```java
import java.util.*;

class Student implements Comparable<Student> {
    int id;
    Student(int id) { this.id = id; }
    public int compareTo(Student o) { return Integer.compare(this.id, o.id); }
}

// Comparator example (custom order)
Comparator<Student> descById = (a, b) -> Integer.compare(b.id, a.id);
```

#### 2) Cursor Types

```java
// Iterator: works for most collections
Iterator<String> it = Arrays.asList("A", "B").iterator();

// ListIterator: only for List, supports bidirectional traversal
ListIterator<String> li = new ArrayList<>(Arrays.asList("A", "B")).listIterator();
```

#### 3) Utility Classes

```java
List<Integer> nums = new ArrayList<>(Arrays.asList(3, 1, 2));
Collections.sort(nums); // [1, 2, 3]

int[] a = {3, 1, 2};
Arrays.sort(a); // [1, 2, 3]
```

### Quick Study Rules

- Need ordered duplicates -> `List`
- Need uniqueness -> `Set`
- Need sorted uniqueness -> `SortedSet`/`NavigableSet`
- Need processing pipeline (FIFO/priority) -> `Queue`
- Need key-value lookup -> `Map`
---

## Collection Interface Methods and Operations

The `Collection` interface defines a set of fundamental methods that are applicable to all collection types. These methods cover basic operations like adding, removing, searching, and iterating through elements.

### Common Collection Interface Methods

| Method | Return Type | Purpose | Example |
|--------|-------------|---------|---------|
| `add(E e)` | boolean | Adds an element to the collection | `collection.add("Java")` |
| `addAll(Collection<? extends E> c)` | boolean | Adds all elements from another collection | `collection.addAll(otherCollection)` |
| `remove(Object o)` | boolean | Removes a specific element | `collection.remove("Java")` |
| `removeAll(Collection<?> c)` | boolean | Removes all elements present in another collection | `collection.removeAll(otherCollection)` |
| `retainAll(Collection<?> c)` | boolean | Keeps only elements present in another collection (intersection) | `collection.retainAll(otherCollection)` |
| `clear()` | void | Removes all elements from the collection | `collection.clear()` |
| `contains(Object o)` | boolean | Checks if an element exists | `collection.contains("Java")` |
| `containsAll(Collection<?> c)` | boolean | Checks if all elements from another collection exist | `collection.containsAll(otherCollection)` |
| `size()` | int | Returns the number of elements | `int count = collection.size()` |
| `isEmpty()` | boolean | Checks if collection is empty | `if (collection.isEmpty())` |
| `iterator()` | Iterator | Returns an iterator for traversal | `Iterator it = collection.iterator()` |
| `toArray()` | Object[] | Converts collection to an array | `Object[] arr = collection.toArray()` |

### Detailed Explanation of Collection Operations

All these methods are fundamental to working with collections. Understanding each operation is essential for effective collection manipulation.

#### 1. Adding Elements: `add()` and `addAll()`

**`add(E e)` method:**
- Adds a single element to the collection
- Returns `true` if the element was added successfully
- Returns `false` if the element could not be added (e.g., duplicate in a Set)

**`addAll(Collection<? extends E> c)` method:**
- Adds all elements from another collection
- Returns `true` if at least one element was added
- Returns `false` if no elements were added

#### 2. Removing Elements: `remove()`, `removeAll()`, `clear()`

**`remove(Object o)` method:**
- Removes the specified element from the collection
- Returns `true` if the element was found and removed
- Returns `false` if the element was not found

**`removeAll(Collection<?> c)` method:**
- Removes all elements that are present in the specified collection
- Returns `true` if any element was removed
- Returns `false` if no elements were removed

**`clear()` method:**
- Removes all elements from the collection
- Always succeeds; no return value
- The collection becomes empty after this call

#### 3. Searching Elements: `contains()`, `containsAll()`

**`contains(Object o)` method:**
- Checks if a specific element exists in the collection
- Returns `true` if found, `false` otherwise
- Uses `equals()` method for comparison

**`containsAll(Collection<?> c)` method:**
- Checks if all elements of another collection exist in this collection
- Returns `true` only if ALL elements are found
- Returns `false` if even one element is missing

#### 4. Set Operations: `retainAll()`

**`retainAll(Collection<?> c)` method:**
- Performs intersection operation
- Keeps only elements that are present in both collections
- Removes all elements NOT in the specified collection
- Returns `true` if any element was removed
- Returns `false` if no changes were made

#### 5. Information Methods: `size()`, `isEmpty()`

**`size()` method:**
- Returns the number of elements in the collection
- Returns 0 if the collection is empty

**`isEmpty()` method:**
- Returns `true` if the collection contains no elements
- Returns `false` if the collection contains at least one element
- Equivalent to `size() == 0` but more efficient

#### 6. Conversion: `toArray()`

**`toArray()` method:**
- Converts the collection to an array
- Returns an `Object[]` array containing all elements
- Provides interoperability with code expecting arrays

#### 7. Traversal: `iterator()`

**`iterator()` method:**
- Returns an `Iterator` object for traversing elements
- Allows safe removal of elements during iteration using `iterator.remove()`

### Code Examples: All Collection Operations

#### Example 1: Add and Contains Operations

```java
import java.util.*;

public class CollectionAddAndContainsExample {
    public static void main(String[] args) {
        Collection<String> languages = new ArrayList<>();
        
        // add() - Adding single elements
        boolean added1 = languages.add("Java");
        boolean added2 = languages.add("Python");
        boolean added3 = languages.add("JavaScript");
        
        System.out.println("After adding elements: " + languages);
        System.out.println("Java added? " + added1);  // true
        
        // addAll() - Adding multiple elements
        Collection<String> moreLanguages = new ArrayList<>();
        moreLanguages.add("C++");
        moreLanguages.add("Go");
        
        languages.addAll(moreLanguages);
        System.out.println("After addAll(): " + languages);
        
        // contains() - Check for single element
        System.out.println("Contains 'Java'? " + languages.contains("Java"));      // true
        System.out.println("Contains 'Rust'? " + languages.contains("Rust"));      // false
        
        // containsAll() - Check for all elements
        System.out.println("Contains all in moreLanguages? " + languages.containsAll(moreLanguages)); // true
    }
}

/* Output:
After adding elements: [Java, Python, JavaScript]
Java added? true
After addAll(): [Java, Python, JavaScript, C++, Go]
Contains 'Java'? true
Contains 'Rust'? false
Contains all in moreLanguages? true
*/
```

#### Example 2: Remove Operations

```java
import java.util.*;

public class CollectionRemoveExample {
    public static void main(String[] args) {
        Collection<Integer> numbers = new ArrayList<>();
        numbers.addAll(Arrays.asList(10, 20, 30, 40, 50, 60));
        
        System.out.println("Original: " + numbers);
        
        // remove() - Remove single element
        boolean removed = numbers.remove(30);
        System.out.println("After remove(30): " + numbers);
        System.out.println("Was 30 removed? " + removed);  // true
        
        // removeAll() - Remove multiple elements
        Collection<Integer> toRemove = Arrays.asList(20, 40);
        numbers.removeAll(toRemove);
        System.out.println("After removeAll(20, 40): " + numbers);
        
        // clear() - Remove all elements
        Collection<Integer> temp = new ArrayList<>(numbers);
        temp.clear();
        System.out.println("After clear(): " + temp);
        System.out.println("Is empty? " + temp.isEmpty());  // true
    }
}

/* Output:
Original: [10, 20, 30, 40, 50, 60]
After remove(30): [10, 20, 40, 50, 60]
Was 30 removed? true
After removeAll(20, 40): [10, 50, 60]
After clear(): []
Is empty? true
*/
```

#### Example 3: Set Operations with retainAll()

```java
import java.util.*;

public class CollectionRetainAllExample {
    public static void main(String[] args) {
        Collection<Integer> set1 = new ArrayList<>(Arrays.asList(10, 20, 30, 40, 50));
        Collection<Integer> set2 = new ArrayList<>(Arrays.asList(30, 40, 50, 60, 70));
        
        System.out.println("Set 1: " + set1);
        System.out.println("Set 2: " + set2);
        
        // retainAll() - Intersection
        set1.retainAll(set2);
        System.out.println("After retainAll(set2): " + set1);  // [30, 40, 50]
        
        // Union example
        Collection<Integer> union = new ArrayList<>(Arrays.asList(10, 20, 30, 40, 50));
        Collection<Integer> toAdd = Arrays.asList(30, 40, 50, 60, 70);
        union.addAll(toAdd);
        System.out.println("Union: " + union);  // [10, 20, 30, 40, 50, 30, 40, 50, 60, 70]
        
        // Difference (removeAll)
        Collection<Integer> difference = new ArrayList<>(Arrays.asList(10, 20, 30, 40, 50));
        Collection<Integer> toRemove = Arrays.asList(30, 40, 50, 60, 70);
        difference.removeAll(toRemove);
        System.out.println("Difference: " + difference);  // [10, 20]
    }
}

/* Output:
Set 1: [10, 20, 30, 40, 50]
Set 2: [30, 40, 50, 60, 70]
After retainAll(set2): [30, 40, 50]
Union: [10, 20, 30, 40, 50, 30, 40, 50, 60, 70]
Difference: [10, 20]
*/
```

#### Example 4: Size and isEmpty() Operations

```java
import java.util.*;

public class CollectionSizeExample {
    public static void main(String[] args) {
        Collection<String> fruits = new ArrayList<>();
        
        // isEmpty() - Check if empty
        System.out.println("Is empty initially? " + fruits.isEmpty());  // true
        
        // Add some elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        fruits.add("Mango");
        fruits.add("Grapes");
        
        // size() - Get count
        System.out.println("Size: " + fruits.size());  // 5
        System.out.println("Is empty now? " + fruits.isEmpty());  // false
        
        // Remove and check size again
        fruits.remove("Banana");
        System.out.println("Size after remove: " + fruits.size());  // 4
        
        // Clear and check
        fruits.clear();
        System.out.println("Size after clear: " + fruits.size());  // 0
        System.out.println("Is empty after clear? " + fruits.isEmpty());  // true
    }
}

/* Output:
Is empty initially? true
Size: 5
Is empty now? false
Size after remove: 4
Size after clear: 0
Is empty after clear? true
*/
```

#### Example 5: toArray() - Conversion Operation

```java
import java.util.*;

public class CollectionToArrayExample {
    public static void main(String[] args) {
        Collection<String> cities = new ArrayList<>();
        cities.add("New York");
        cities.add("London");
        cities.add("Tokyo");
        cities.add("Paris");
        
        System.out.println("Collection: " + cities);
        
        // Convert to Object array
        Object[] objectArray = cities.toArray();
        System.out.println("Array length: " + objectArray.length);
        System.out.println("Array contents:");
        for (Object obj : objectArray) {
            System.out.println("  - " + obj);
        }
        
        // Convert to typed String array
        String[] stringArray = cities.toArray(new String[0]);
        System.out.println("\nString array:");
        for (String city : stringArray) {
            System.out.println("  - " + city);
        }
        
        // Modify array doesn't affect original collection
        stringArray[0] = "Paris";
        System.out.println("\nAfter modifying array, collection: " + cities);
    }
}

/* Output:
Collection: [New York, London, Tokyo, Paris]
Array length: 4
Array contents:
  - New York
  - London
  - Tokyo
  - Paris

String array:
  - New York
  - London
  - Tokyo
  - Paris

After modifying array, collection: [New York, London, Tokyo, Paris]
*/
```

#### Example 6: Iterator() - Traversal and Safe Removal

```java
import java.util.*;

public class CollectionIteratorExample {
    public static void main(String[] args) {
        Collection<Integer> numbers = new ArrayList<>(Arrays.asList(10, 20, 30, 40, 50, 60));
        
        System.out.println("Original collection: " + numbers);
        
        // Using iterator for traversal
        Iterator<Integer> iterator = numbers.iterator();
        System.out.println("\nTraversing with iterator:");
        while (iterator.hasNext()) {
            System.out.println("  - " + iterator.next());
        }
        
        // Safe removal using iterator
        iterator = numbers.iterator();
        System.out.println("\nRemoving even numbers:");
        while (iterator.hasNext()) {
            Integer num = iterator.next();
            if (num % 2 == 0) {
                iterator.remove();
            }
        }
        System.out.println("After removing even numbers: " + numbers);
        
        // Dangerous: modifying collection directly during iteration
        Collection<String> fruits = new ArrayList<>(Arrays.asList("Apple", "Banana", "Orange"));
        System.out.println("\nOriginal fruits: " + fruits);
        
        // This is the RIGHT way using iterator
        Iterator<String> fruitIterator = fruits.iterator();
        while (fruitIterator.hasNext()) {
            String fruit = fruitIterator.next();
            if (fruit.startsWith("B")) {
                fruitIterator.remove();  // Safe removal
            }
        }
        System.out.println("After safe removal: " + fruits);
    }
}

/* Output:
Original collection: [10, 20, 30, 40, 50, 60]

Traversing with iterator:
  - 10
  - 20
  - 30
  - 40
  - 50
  - 60

Removing even numbers:
After removing even numbers: [10, 30, 50]

Original fruits: [Apple, Banana, Orange]
After safe removal: [Apple, Orange]
*/
```

#### Example 7: Comprehensive Example - All Operations Combined

```java
import java.util.*;

public class CollectionComprehensiveExample {
    public static void main(String[] args) {
        System.out.println("=== COMPREHENSIVE COLLECTION OPERATIONS DEMO ===\n");
        
        // Create primary collection
        Collection<String> colors = new ArrayList<>();
        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");
        
        System.out.println("Step 1 - Initial colors: " + colors);
        System.out.println("Size: " + colors.size());
        System.out.println("Is empty? " + colors.isEmpty());
        
        // Add multiple colors
        Collection<String> moreColors = Arrays.asList("Yellow", "Purple", "Orange");
        colors.addAll(moreColors);
        System.out.println("\nStep 2 - After addAll(): " + colors);
        
        // Check containment
        System.out.println("\nStep 3 - Containment checks:");
        System.out.println("Contains 'Red'? " + colors.contains("Red"));
        System.out.println("Contains 'Pink'? " + colors.contains("Pink"));
        System.out.println("Contains all from moreColors? " + colors.containsAll(moreColors));
        
        // Convert to array
        String[] colorArray = colors.toArray(new String[0]);
        System.out.println("\nStep 4 - Converted to array (length: " + colorArray.length + ")");
        
        // Remove specific element
        colors.remove("Purple");
        System.out.println("\nStep 5 - After remove('Purple'): " + colors);
        
        // Remove all elements matching a criteria using iterator
        Collection<String> primaries = Arrays.asList("Red", "Green", "Blue");
        System.out.println("\nStep 6 - Before retainAll (keep only primary colors): " + colors);
        colors.retainAll(primaries);
        System.out.println("After retainAll(primary colors): " + colors);
        
        // Add back some colors
        colors.addAll(Arrays.asList("Cyan", "Magenta"));
        System.out.println("\nStep 7 - After adding Cyan and Magenta: " + colors);
        
        // Clear all
        Collection<String> temp = new ArrayList<>(colors);
        temp.clear();
        System.out.println("\nStep 8 - After clear(): " + temp);
        System.out.println("Is temp empty? " + temp.isEmpty());
        System.out.println("Original colors (unchanged): " + colors);
    }
}

/* Output:
=== COMPREHENSIVE COLLECTION OPERATIONS DEMO ===

Step 1 - Initial colors: [Red, Green, Blue]
Size: 3
Is empty? false

Step 2 - After addAll(): [Red, Green, Blue, Yellow, Purple, Orange]

Step 3 - Containment checks:
Contains 'Red'? true
Contains 'Pink'? false
Contains all from moreColors? true

Step 4 - Converted to array (length: 6)

Step 5 - After remove('Purple'): [Red, Green, Blue, Yellow, Orange]

Step 6 - Before retainAll (keep only primary colors): [Red, Green, Blue, Yellow, Orange]
After retainAll(primary colors): [Red, Green, Blue]

Step 7 - After adding Cyan and Magenta: [Red, Green, Blue, Cyan, Magenta]

Step 8 - After clear(): []
Is temp empty? true
Original colors (unchanged): [Red, Green, Blue, Cyan, Magenta]
*/
```

### Key Takeaways

1. **`add()` and `addAll()`** - Use these to add single or multiple elements to a collection.
2. **`remove()`, `removeAll()`, and `clear()`** - Use these to remove elements; be careful with concurrent modification.
3. **`contains()` and `containsAll()`** - Use these to check for element existence before processing.
4. **`retainAll()`** - Performs intersection; keeps only common elements between two collections.
5. **`size()` and `isEmpty()`** - Always prefer `isEmpty()` to `size() == 0` for better readability.
6. **`toArray()`** - Use this when you need to work with array-based APIs or need fixed-size structures.
7. **`iterator()`** - Always use iterator for---

## List Interface Specific Methods and Operations

The `List` interface extends `Collection` and adds index-based operations. These methods allow you to work with elements by their position in the list, making List more powerful than the basic Collection interface.

### List Interface Specific Methods

| Method | Return Type | Purpose | Example |
|--------|-------------|---------|---------|
| `add(int index, E element)` | void | Inserts element at specific index | `list.add(0, "Java")` |
| `addAll(int index, Collection<? extends E> c)` | boolean | Inserts all elements from collection at index | `list.addAll(1, otherList)` |
| `get(int index)` | E | Retrieves element at specific index | `String s = list.get(0)` |
| `set(int index, E element)` | E | Replaces element at index, returns old element | `list.set(0, "Python")` |
| `remove(int index)` | E | Removes and returns element at index | `list.remove(0)` |
| `indexOf(Object o)` | int | Returns first index of element (-1 if not found) | `int i = list.indexOf("Java")` |
| `lastIndexOf(Object o)` | int | Returns last index of element (-1 if not found) | `int i = list.lastIndexOf("Java")` |
| `subList(int from, int to)` | List | Returns view of list from index to index (to exclusive) | `List sub = list.subList(0, 3)` |
| `listIterator()` | ListIterator | Returns bidirectional iterator | `ListIterator it = list.listIterator()` |
| `listIterator(int index)` | ListIterator | Returns iterator starting at specific index | `ListIterator it = list.listIterator(2)` |

### Comprehensive Example: All List Operations in One Demo

```java
import java.util.*;

public class ListInterfaceComprehensiveExample {
    public static void main(String[] args) {
        System.out.println("========== LIST INTERFACE OPERATIONS DEMO ==========\n");
        
        // Step 1: Create and populate a List
        List<String> languages = new ArrayList<>();
        languages.add("Java");
        languages.add("Python");
        languages.add("JavaScript");
        languages.add("C++");
        languages.add("Go");
        
        System.out.println("Step 1 - Initial List: " + languages);
        System.out.println("Size: " + languages.size());
        System.out.println("Is empty? " + languages.isEmpty());
        
        // Step 2: Access elements using get(int index)
        System.out.println("\nStep 2 - Access elements by index (get operation):");
        System.out.println("Element at index 0: " + languages.get(0));  // Java
        System.out.println("Element at index 2: " + languages.get(2));  // JavaScript
        System.out.println("Element at index 4: " + languages.get(4));  // Go
        System.out.println("Last element: " + languages.get(languages.size() - 1));  // Go
        
        // Step 3: Find indices using indexOf() and lastIndexOf()
        System.out.println("\nStep 3 - Find indices of elements:");
        languages.add("Java");  // Add duplicate
        System.out.println("List after adding 'Java' again: " + languages);
        System.out.println("First index of 'Java': " + languages.indexOf("Java"));  // 0
        System.out.println("Last index of 'Java': " + languages.lastIndexOf("Java"));  // 5
        System.out.println("Index of 'Python': " + languages.indexOf("Python"));  // 1
        System.out.println("Index of 'Rust' (not exists): " + languages.indexOf("Rust"));  // -1
        
        // Step 4: Replace elements using set(int index, E element)
        System.out.println("\nStep 4 - Replace element at specific index (set operation):");
        String oldValue = languages.set(1, "TypeScript");
        System.out.println("Replaced element at index 1: " + oldValue + " -> TypeScript");
        System.out.println("List after set: " + languages);
        
        // Step 5: Insert at specific position using add(int index, E element)
        System.out.println("\nStep 5 - Insert element at specific index (add at index):");
        languages.add(0, "Kotlin");  // Insert at beginning
        System.out.println("After add('Kotlin', 0): " + languages);
        
        languages.add(3, "Rust");  // Insert in middle
        System.out.println("After add('Rust', 3): " + languages);
        
        languages.add(languages.size(), "Scala");  // Insert at end
        System.out.println("After add('Scala', end): " + languages);
        
        // Step 6: Add all elements from another collection at specific index
        System.out.println("\nStep 6 - Add all from another collection at index (addAll at index):");
        List<String> newLanguages = Arrays.asList("Ruby", "PHP");
        languages.addAll(2, newLanguages);
        System.out.println("After addAll(2, [Ruby, PHP]): " + languages);
        
        // Step 7: Remove element by index using remove(int index)
        System.out.println("\nStep 7 - Remove element at specific index (remove by index):");
        String removed = languages.remove(2);
        System.out.println("Removed element at index 2: " + removed);
        System.out.println("List after remove(2): " + languages);
        
        // Step 8: Get substring of list using subList()
        System.out.println("\nStep 8 - Get sublist (subList operation):");
        List<String> sublist = languages.subList(1, 4);  // from index 1 to 4 (exclusive)
        System.out.println("Sublist from index 1 to 4: " + sublist);
        
        // Modify sublist to see effect on original list
        System.out.println("Original list before modifying sublist: " + languages);
        Collections.fill(sublist, "Modified");
        System.out.println("After Collections.fill(sublist, 'Modified'): " + languages);
        System.out.println("(Note: Sublist changes affect original list!)");
        
        // Step 9: Restore list and use ListIterator for bidirectional traversal
        System.out.println("\nStep 9 - ListIterator for bidirectional traversal:");
        languages = new ArrayList<>(Arrays.asList("Java", "Python", "JavaScript", "C++", "Go"));
        System.out.println("Fresh list: " + languages);
        
        ListIterator<String> listIterator = languages.listIterator();
        System.out.println("\nForward traversal using ListIterator:");
        while (listIterator.hasNext()) {
            System.out.println("  - " + listIterator.next());
        }
        
        System.out.println("\nBackward traversal using ListIterator:");
        while (listIterator.hasPrevious()) {
            System.out.println("  - " + listIterator.previous());
        }
        
        // Step 10: ListIterator starting at specific index
        System.out.println("\nStep 10 - ListIterator starting at index 2:");
        listIterator = languages.listIterator(2);
        System.out.println("Iterator at index 2, next elements:");
        while (listIterator.hasNext()) {
            System.out.println("  - " + listIterator.next());
        }
        
        // Step 11: Demonstrate index preservation and duplicates
        System.out.println("\nStep 11 - Index preservation and duplicate handling:");
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Apple");
        fruits.add("Cherry");
        fruits.add("Apple");
        
        System.out.println("List with duplicates: " + fruits);
        System.out.println("Duplicates by index:");
        for (int i = 0; i < fruits.size(); i++) {
            if (fruits.get(i).equals("Apple")) {
                System.out.println("  - 'Apple' found at index: " + i);
            }
        }
        
        // Step 12: Demonstrate order preservation
        System.out.println("\nStep 12 - Order preservation in List:");
        List<Integer> numbers = new ArrayList<>();
        numbers.add(50);
        numbers.add(20);
        numbers.add(40);
        numbers.add(10);
        numbers.add(30);
        
        System.out.println("Original insertion order: " + numbers);
        System.out.println("(List preserves order even after adding in random sequence)");
        
        // Step 13: ArrayList vs LinkedList performance implications
        System.out.println("\nStep 13 - ArrayList vs LinkedList - Index-based access:");
        List<Integer> arrayList = new ArrayList<>();
        List<Integer> linkedList = new LinkedList<>();
        
        for (int i = 0; i < 100000; i++) {
            arrayList.add(i);
            linkedList.add(i);
        }
        
        // ArrayList: O(1) access
        long startAL = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            arrayList.get(i);
        }
        long endAL = System.nanoTime();
        
        // LinkedList: O(n) access
        long startLL = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            linkedList.get(i);
        }
        long endLL = System.nanoTime();
        
        System.out.println("ArrayList get() 1000 times: " + (endAL - startAL) + " ns");
        System.out.println("LinkedList get() 1000 times: " + (endLL - startLL) + " ns");
        System.out.println("(ArrayList is much faster for random access)");
        
        // Step 14: Summary of all operations
        System.out.println("\n========== SUMMARY OF LIST OPERATIONS ==========");
        System.out.println("✓ get(index) - Access by position");
        System.out.println("✓ add(index, element) - Insert at position");
        System.out.println("✓ addAll(index, collection) - Insert collection at position");
        System.out.println("✓ set(index, element) - Replace at position");
        System.out.println("✓ remove(index) - Remove by position");
        System.out.println("✓ indexOf(element) - Find first occurrence");
        System.out.println("✓ lastIndexOf(element) - Find last occurrence");
        System.out.println("✓ subList(from, to) - Get range (from-to exclusive)");
        System.out.println("✓ listIterator() - Bidirectional iteration");
        System.out.println("✓ listIterator(index) - Bidirectional from index");
        System.out.println("✓ Duplicates allowed - Same element at different indices");
        System.out.println("✓ Order preserved - Insertion order maintained");
    }
}

/* Output:
========== LIST INTERFACE OPERATIONS DEMO ==========

Step 1 - Initial List: [Java, Python, JavaScript, C++, Go]
Size: 5
Is empty? false

Step 2 - Access elements by index (get operation):
Element at index 0: Java
Element at index 2: JavaScript
Element at index 4: Go
Last element: Go

Step 3 - Find indices of elements:
List after adding 'Java' again: [Java, Python, JavaScript, C++, Go, Java]
First index of 'Java': 0
Last index of 'Java': 5
Index of 'Python': 1
Index of 'Rust' (not exists): -1

Step 4 - Replace element at specific index (set operation):
Replaced element at index 1: Python -> TypeScript
List after set: [Java, TypeScript, JavaScript, C++, Go, Java]

Step 5 - Insert element at specific index (add at index):
After add('Kotlin', 0): [Kotlin, Java, TypeScript, JavaScript, C++, Go, Java]
After add('Rust', 3): [Kotlin, Java, TypeScript, Rust, JavaScript, C++, Go, Java]
After add('Scala', end): [Kotlin, Java, TypeScript, Rust, JavaScript, C++, Go, Java, Scala]

Step 6 - Add all from another collection at index (addAll at index):
After addAll(2, [Ruby, PHP]): [Kotlin, Java, Ruby, PHP, TypeScript, Rust, JavaScript, C++, Go, Java, Scala]

Step 7 - Remove element at specific index (remove by index):
Removed element at index 2: Ruby
List after remove(2): [Kotlin, Java, PHP, TypeScript, Rust, JavaScript, C++, Go, Java, Scala]

Step 8 - Get sublist (subList operation):
Sublist from index 1 to 4: [Java, PHP, TypeScript]
Original list before modifying sublist: [Kotlin, Java, PHP, TypeScript, Rust, JavaScript, C++, Go, Java, Scala]
After Collections.fill(sublist, 'Modified'): [Kotlin, Modified, Modified, Modified, Rust, JavaScript, C++, Go, Java, Scala]
(Note: Sublist changes affect original list!)

Step 9 - ListIterator for bidirectional traversal:
Fresh list: [Java, Python, JavaScript, C++, Go]

Forward traversal using ListIterator:
  - Java
  - Python
  - JavaScript
  - C++
  - Go

Backward traversal using ListIterator:
  - Go
  - C++
  - JavaScript
  - Python
  - Java

Step 10 - ListIterator starting at index 2:
Iterator at index 2, next elements:
  - JavaScript
  - C++
  - Go

Step 11 - Demonstrate index preservation and duplicates:
List with duplicates: [Apple, Banana, Apple, Cherry, Apple]
Duplicates by index:
  - 'Apple' found at index: 0
  - 'Apple' found at index: 2
  - 'Apple' found at index: 4

Step 12 - Demonstrate order preservation:
Original insertion order: [50, 20, 40, 10, 30]
(List preserves order even after adding in random sequence)

Step 13 - ArrayList vs LinkedList - Index-based access:
ArrayList get() 1000 times: 1234567 ns
LinkedList get() 1000 times: 45678901 ns
(ArrayList is much faster for random access)

Step 14 - Summary of all operations
✓ get(index) - Access by position
✓ add(index, element) - Insert at position
✓ addAll(index, collection) - Insert collection at position
✓ set(index, element) - Replace at position
✓ remove(index) - Remove by position
✓ indexOf(element) - Find first occurrence
✓ lastIndexOf(element) - Find last occurrence
✓ subList(from, to) - Get range (from-to exclusive)
✓ listIterator() - Bidirectional iteration
✓ listIterator(index) - Bidirectional from index
✓ Duplicates allowed - Same element at different indices
✓ Order preserved - Insertion order maintained
*/
```

### Key Characteristics of List Interface

#### 1. Index-Based Access
Elements can be accessed, inserted, or removed by their position (0-indexed).

#### 2. Duplicates Allowed
A List can contain multiple identical elements. Duplicates can be differentiated by their index.

#### 3. Insertion Order Preserved
The order in which elements are added is maintained even when not sorted.

#### 4. Bidirectional Iteration
`ListIterator` allows traversal both forward and backward.

#### 5. Index Play Important Role
Index is central to List operations, making it different from Set which has no index concept.

### List Implementations Comparison

| Feature | ArrayList | LinkedList |
|---------|-----------|-----------|
| **Internal structure** | Dynamic array | Doubly linked list |
| **get(index)** | O(1) - Very fast | O(n) - Must traverse |
| **add(element)** | O(1) amortized | O(1) |
| **add(index, element)** | O(n) - Shift elements | O(1) - Just update pointers |
| **remove(index)** | O(n) - Shift elements | O(n) - Must traverse |
| **Memory usage** | Lower overhead | Higher overhead (pointers) |
| **Thread-safety** | Not synchronized | Not synchronized |
| **Best use case** | Random access, iteration | Frequent insertion/deletion |
| **Most common** | Yes | Rarely, special cases |

### When to Use Which List Implementation

| Use ArrayList | Use LinkedList | Use Vector/Stack |
|---|---|---|
| Default choice for most cases | Frequent middle insertions | Thread-safe operations |
| Frequent random access | Frequent middle deletions | Legacy code |
| Few insertions/deletions | Rare random access needed | LIFO structure needed |
| Performance critical | Queue-like operations | Old code compatibility |

### ListIterator vs Iterator

| Feature | Iterator | ListIterator |
|---------|----------|-------------|
| **Direction** | Forward only | Bidirectional |
| **Available for** | All Collections | Only List |
| **Methods** | hasNext(), next(), remove() | hasPrevious(), previous(), hasNext(), next(), set(), add(), remove() |
| **Use case** | General iteration | Advanced list manipulation |

### Key Takeaways

1. **List extends Collection** - Inherits all Collection methods and adds index-based methods.
2. **Index is central** - All unique List methods revolve around index positioning.
3. **Duplicates and order** - List allows duplicates and preserves insertion order.
4. **ArrayList is default** - Use ArrayList unless you have specific performance needs.
5. **Performance trade-off** - ArrayList: fast access, slow insertion in middle; LinkedList: slow access, fast insertion.
6. **Bidirectional iteration** - ListIterator provides forward and backward traversal.
7. **Sublist is a view** - Changes to sublist reflect in original list (backed collection).
8. **indexOf() returns -1 for not found** - Always check return value or use contains() first.
9. **Set (index-based)** - Replaces and returns old value; different from add() which inserts.
10. **ListIterator starting at index** - Use `listIterator(index)` to start traversal from specific position.
 safe element removal during traversal.
8. **Return values matter** - Most methods return boolean indicating success/change; use these to validate operations.
9. **Set operations** - `addAll()` (union), `retainAll()` (intersection), `removeAll()` (difference) can implement basic set theory.
10. **Efficiency** - Choose the right collection type based on your operations; different implementations have different performance characteristics.
<!-- ...existing code... -->

### Key Takeaways

1. **`add()` and `addAll()`** - Use these to add single or multiple elements to a collection.
2. **`remove()`, `removeAll()`, and `clear()`** - Use these to remove elements; be careful with concurrent modification.
3. **`contains()` and `containsAll()`** - Use these to check for element existence before processing.
4. **`retainAll()`** - Performs intersection; keeps only common elements between two collections.
5. **`size()` and `isEmpty()`** - Always prefer `isEmpty()` to `size() == 0` for better readability.
6. **`toArray()`** - Use this when you need to work with array-based APIs or need fixed-size structures.
7. **`iterator()`** - Always use iterator for safe element removal during traversal.
8. **Return values matter** - Most methods return boolean indicating success/change; use these to validate operations.
9. **Set operations** - `addAll()` (union), `retainAll()` (intersection), `removeAll()` (difference) can implement basic set theory.
10. **Efficiency** - Choose the right collection type based on your operations; different implementations have different performance characteristics.

---

## ArrayList (Detailed)

### Core Points

- `ArrayList` uses a **resizable array** internally.
- Duplicates are allowed.
- Insertion order is preserved.
- `null` values are allowed.
- Random/index-based retrieval is fast (`get(index)` is O(1) average).
- Middle insertion/deletion is slower (shifting required, O(n)).
- `ArrayList` implements:
  - `Serializable`
  - `Cloneable`
  - `RandomAccess` (marker interface in `java.util`, no methods)

### Why RandomAccess Matters

- `RandomAccess` is a marker interface (no methods).
- It indicates efficient index-based access.
- `ArrayList` and `Vector` implement it; `LinkedList` does not.

### Constructors

```java
ArrayList<E> list1 = new ArrayList<>();
ArrayList<E> list2 = new ArrayList<>(int initialCapacity);
ArrayList<E> list3 = new ArrayList<>(Collection<? extends E> c);
```

---

### One Comprehensive Example (Important ArrayList + List methods together)

```java
import java.util.*;

public class ArrayListAllMethodsOneExample {
    public static void main(String[] args) {
        // 1) Constructors
        ArrayList<String> a = new ArrayList<>();                         // default
        ArrayList<String> b = new ArrayList<>(20);                       // with capacity
        ArrayList<String> c = new ArrayList<>(Arrays.asList("X", "Y"));  // from collection

        // 2) Marker/interface checks
        System.out.println(a instanceof Serializable);   // true
        System.out.println(a instanceof Cloneable);      // true
        System.out.println(a instanceof RandomAccess);   // true
        System.out.println(new LinkedList<>() instanceof RandomAccess); // false

        // 3) add, add(index), addAll, addAll(index)
        a.add("Java");
        a.add("Python");
        a.add("Java");              // duplicate
        a.add(null);                // null allowed
        a.add(1, "C++");
        a.addAll(Arrays.asList("Go", "Rust"));
        a.addAll(2, Arrays.asList("Kotlin", "Scala"));
        System.out.println("After adds: " + a);

        // 4) get, set
        System.out.println("get(0): " + a.get(0));
        String old = a.set(0, "JAVA");
        System.out.println("set(0): old=" + old + ", new list=" + a);

        // 5) contains, containsAll, indexOf, lastIndexOf
        System.out.println("contains(Java): " + a.contains("Java"));
        System.out.println("containsAll([Go, Rust]): " + a.containsAll(Arrays.asList("Go", "Rust")));
        System.out.println("indexOf(Java): " + a.indexOf("Java"));
        System.out.println("lastIndexOf(Java): " + a.lastIndexOf("Java"));

        // 6) remove(index), remove(object), removeAll, retainAll
        String removedByIndex = a.remove(1);
        boolean removedObj = a.remove("Rust");
        System.out.println("removed index value: " + removedByIndex + ", removed Rust? " + removedObj);
        a.removeAll(Arrays.asList("Scala", "Kotlin"));
        System.out.println("After removeAll: " + a);

        ArrayList<String> keep = new ArrayList<>(Arrays.asList("JAVA", "Go", null));
        a.retainAll(keep);
        System.out.println("After retainAll: " + a);

        // 7) size, isEmpty, toArray
        System.out.println("size: " + a.size());
        System.out.println("isEmpty: " + a.isEmpty());
        Object[] arr1 = a.toArray();
        String[] arr2 = a.toArray(new String[0]);
        System.out.println("toArray length: " + arr1.length + ", typed length: " + arr2.length);

        // 8) iterator, listIterator
        System.out.print("Iterator: ");
        Iterator<String> it = a.iterator();
        while (it.hasNext()) System.out.print(it.next() + " ");
        System.out.println();

        System.out.print("ListIterator forward/backward: ");
        ListIterator<String> li = a.listIterator();
        while (li.hasNext()) System.out.print(li.next() + " ");
        while (li.hasPrevious()) System.out.print(li.previous() + " ");
        System.out.println();

        // 9) subList
        ArrayList<Integer> nums = new ArrayList<>(Arrays.asList(10, 20, 30, 40, 50));
        List<Integer> sub = nums.subList(1, 4); // [20, 30, 40]
        System.out.println("subList: " + sub);

        // 10) sort, replaceAll, removeIf
        nums.sort(Integer::compareTo); // sort
        nums.replaceAll(n -> n + 1);   // [11, 21, 31, 41, 51]
        nums.removeIf(n -> n > 40);    // [11, 21, 31]
        System.out.println("After sort/replaceAll/removeIf: " + nums);

        // 11) ensureCapacity, trimToSize
        ArrayList<Integer> cap = new ArrayList<>();
        cap.ensureCapacity(100);
        cap.addAll(Arrays.asList(1, 2, 3));
        cap.trimToSize();

        // 12) clone
        @SuppressWarnings("unchecked")
        ArrayList<String> cloned = (ArrayList<String>) c.clone();
        System.out.println("Cloned list: " + cloned);

        // 13) clear
        a.clear();
        System.out.println("After clear, isEmpty: " + a.isEmpty());
    }
}
```
<!-- ...existing code... -->

---

## Difference Between ArrayList and Vector

### Extracted Points (from slide) with Correct Explanation

| Point | ArrayList | Vector |
|---|---|---|
| Synchronization | Methods are **not synchronized** by default | Most methods are **synchronized** |
| Thread safety | Not thread-safe for concurrent modification (without external sync) | Thread-safe for many basic operations due to internal synchronization |
| Performance | Usually faster in single-threaded use (no lock overhead) | Usually slower because locking adds overhead |
| Waiting/locking behavior | Threads do not block each other by default | Threads may wait due to lock contention |
| Introduced in | Java **1.2** | Java **1.0** |
| Legacy status | Modern Collections Framework class | Legacy class (still available, but less preferred in new code) |

### Point-by-Point Explanation

1. **“ArrayList methods are non-synchronized”**  
   Correct. `ArrayList` does not lock methods internally.  
   Result: better speed in normal single-threaded programs.

2. **“Vector methods are synchronized”**  
   Correct. `Vector` uses intrinsic synchronization on most methods.  
   Result: safer in concurrent access scenarios, but slower.

3. **“Multiple threads can operate on ArrayList, so not thread-safe”**  
   Correct idea. Multiple threads can access it, but concurrent structural changes can cause race conditions or `ConcurrentModificationException`.

4. **“Only one thread at a time on Vector object”**  
   Mostly correct for synchronized method calls. A lock allows one thread per monitor for those synchronized operations.

5. **“ArrayList performance is relatively high”**  
   Generally true (especially in single-threaded contexts) because there is no method-level locking.

6. **“Vector performance is relatively low”**  
   Generally true versus `ArrayList`, because synchronization adds overhead.

7. **“ArrayList introduced in 1.2, non-legacy”**  
   Correct. Part of Java Collections Framework (JCF).

8. **“Vector introduced in 1.0, legacy”**  
   Correct. Still valid but mostly replaced by `ArrayList` + explicit synchronization when needed.

### Practical Rule

- Use **ArrayList** by default.
- Use **Vector** only for legacy compatibility.
- For modern thread-safe lists, prefer:
  - `Collections.synchronizedList(new ArrayList<>())`, or
  - `CopyOnWriteArrayList` (read-heavy scenarios).

### One Small Demo

```java
import java.util.*;
import java.util.concurrent.CopyOnWriteArrayList;

public class ArrayListVsVectorDemo {
    public static void main(String[] args) {
        List<Integer> arrayList = new ArrayList<>();
        List<Integer> vector = new Vector<>();

        // Basic add
        for (int i = 0; i < 5; i++) {
            arrayList.add(i);
            vector.add(i);
        }

        System.out.println("ArrayList: " + arrayList);
        System.out.println("Vector   : " + vector);

        // Type checks
        System.out.println("arrayList instanceof RandomAccess: " + (arrayList instanceof RandomAccess));
        System.out.println("vector    instanceof RandomAccess: " + (vector instanceof RandomAccess));

        // Modern synchronized alternatives
        List<Integer> syncList = Collections.synchronizedList(new ArrayList<>());
        List<Integer> cowList = new CopyOnWriteArrayList<>();

        syncList.addAll(Arrays.asList(1, 2, 3));
        cowList.addAll(Arrays.asList(1, 2, 3));

        System.out.println("SynchronizedList: " + syncList);
        System.out.println("CopyOnWriteList : " + cowList);
    }
}
```

### Quick Takeaway

- **ArrayList**: faster, non-synchronized, modern default.
- **Vector**: synchronized, legacy, slower under lock overhead.
- Prefer **modern concurrency wrappers/classes** instead of `Vector` in new code.

<!-- ...existing code... -->
### Quick Rule

- Frequent **retrieval** by index -> prefer `ArrayList`
- Frequent **middle insert/delete** -> prefer `LinkedList`

<!-- ...existing code... --><!-- ...existing code... -->

---

## How to Get a Synchronized Version of ArrayList, Set, and Map

By default, `ArrayList`, `HashSet`, and `HashMap` are **not synchronized**.  
If multiple threads modify them concurrently, results are unsafe.

Java provides synchronized wrappers via the `Collections` utility class.

### Correct Method Signatures

```java
public static <T> List<T> synchronizedList(List<T> list);
public static <T> Set<T> synchronizedSet(Set<T> s);
public static <K,V> Map<K,V> synchronizedMap(Map<K,V> m);
```

> Note: It is `Collections` (plural), not `Collection`.  
> Also `synchronizedMap` returns `Map`, not `Set`.

---

### 1) Synchronized `ArrayList`

```java
import java.util.*;

public class SynchronizedListExample {
    public static void main(String[] args) {
        List<String> normal = new ArrayList<>();
        normal.add("A");
        normal.add("B");

        List<String> syncList = Collections.synchronizedList(normal);

        syncList.add("C");
        syncList.remove("A");
        System.out.println(syncList); // [B, C] (order depends on operations)
    }
}
```

---

### 2) Synchronized `Set`

```java
import java.util.*;

public class SynchronizedSetExample {
    public static void main(String[] args) {
        Set<Integer> normalSet = new HashSet<>();
        Set<Integer> syncSet = Collections.synchronizedSet(normalSet);

        syncSet.add(10);
        syncSet.add(20);
        syncSet.add(10); // duplicate ignored
        System.out.println(syncSet);
    }
}
```

---

### 3) Synchronized `Map`

```java
import java.util.*;

public class SynchronizedMapExample {
    public static void main(String[] args) {
        Map<Integer, String> normalMap = new HashMap<>();
        Map<Integer, String> syncMap = Collections.synchronizedMap(normalMap);

        syncMap.put(101, "Durga");
        syncMap.put(102, "Ravi");
        syncMap.put(101, "DURGA"); // key replaced

        System.out.println(syncMap); // {101=DURGA, 102=Ravi}
    }
}
```

---

### Important Rule While Iterating

Even with synchronized wrappers, iteration must be manually synchronized on the same object.

```java
import java.util.*;

public class SynchronizedIterationRule {
    public static void main(String[] args) {
        List<String> list = Collections.synchronizedList(new ArrayList<>());
        list.add("Java");
        list.add("Python");
        list.add("Go");

        synchronized (list) {
            Iterator<String> it = list.iterator();
            while (it.hasNext()) {
                System.out.println(it.next());
            }
        }
    }
}
```

If you do not synchronize during iteration, `ConcurrentModificationException` can still happen.

---

### One Combined Example (List + Set + Map)

```java
import java.util.*;

public class SynchronizedCollectionsCombined {
    public static void main(String[] args) {
        List<String> syncList = Collections.synchronizedList(new ArrayList<>());
        Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
        Map<Integer, String> syncMap = Collections.synchronizedMap(new HashMap<>());

        syncList.addAll(Arrays.asList("A", "B", "C"));
        syncSet.addAll(Arrays.asList("X", "Y", "X"));
        syncMap.put(1, "One");
        syncMap.put(2, "Two");

        synchronized (syncList) {
            for (String s : syncList) System.out.print(s + " ");
        }
        System.out.println();

        synchronized (syncSet) {
            for (String s : syncSet) System.out.print(s + " ");
        }
        System.out.println();

        synchronized (syncMap) {
            for (Map.Entry<Integer, String> e : syncMap.entrySet()) {
                System.out.println(e.getKey() + " -> " + e.getValue());
            }
        }
    }
}
```

---

### Modern Alternatives (Preferred in many concurrent applications)

- `CopyOnWriteArrayList` (read-heavy list workloads)
- `ConcurrentHashMap` (highly concurrent map access)
- `ConcurrentSkipListSet` / `ConcurrentSkipListMap` (sorted concurrent structures)

---

### Quick Takeaways

1. Default `ArrayList/HashSet/HashMap` are not thread-safe.
2. Use `Collections.synchronizedList/Set/Map` for synchronized wrappers.
3. Synchronize manually during iteration.
4. For high concurrency, prefer concurrent collections from `java.util.concurrent`.

<!-- ...existing code... --><!-- ...existing code... -->

---

## LinkedList (Detailed)

### Core Points

- `LinkedList` uses a **doubly linked list** data structure.
- Insertion order is preserved.
- Duplicates are allowed.
- `null` insertion is allowed.
- Good for frequent **insertion/deletion in middle**.
- Not good for frequent **random/index-based retrieval**.
- `LinkedList` implements `Serializable` and `Cloneable`, but **not** `RandomAccess`.

### Constructors

```java
LinkedList<E> l1 = new LinkedList<>();
LinkedList<E> l2 = new LinkedList<>(Collection<? extends E> c);
```

### LinkedList Specific Methods

| Method | Return Type | Purpose |
|---|---|---|
| `addFirst(E e)` | `void` | Insert at beginning |
| `addLast(E e)` | `void` | Insert at end |
| `getFirst()` | `E` | Read first element |
| `getLast()` | `E` | Read last element |
| `removeFirst()` | `E` | Remove and return first |
| `removeLast()` | `E` | Remove and return last |

### One Demo (all major operations)

```java
import java.io.Serializable;
import java.util.*;

public class LinkedListAllInOneDemo {
    public static void main(String[] args) {
        LinkedList<Object> l1 = new LinkedList<>();
        LinkedList<String> l2 = new LinkedList<>(Arrays.asList("X", "Y", "Z"));

        // Interface checks
        System.out.println(l1 instanceof Serializable); // true
        System.out.println(l1 instanceof Cloneable);    // true
        System.out.println(l1 instanceof RandomAccess); // false

        // Basic behavior
        l1.add("durga");
        l1.add(30);
        l1.add(null);
        l1.add("durga");           // duplicate allowed
        l1.set(0, "software");
        l1.add(0, "venkey");
        l1.addFirst("ccc");
        l1.addLast("zzz");

        System.out.println("After add/set: " + l1);

        System.out.println("getFirst(): " + l1.getFirst());
        System.out.println("getLast(): " + l1.getLast());

        System.out.println("removeFirst(): " + l1.removeFirst());
        System.out.println("removeLast(): " + l1.removeLast());

        System.out.println("After removeFirst/removeLast: " + l1);
        System.out.println("From collection constructor: " + l2);
    }
}
```

### Quick Rule

- Frequent retrieval by index -> prefer `ArrayList`
- Frequent insertion/deletion in middle -> prefer `LinkedList`


---

## Difference Between ArrayList and LinkedList

### Extracted Points (Corrected)

| Point | ArrayList | LinkedList |
|---|---|---|
| Best choice when | Frequent retrieval/access by index | Frequent insertion/deletion (especially near ends or via iterator) |
| Worst choice when | Frequent insertion/deletion in middle | Frequent random retrieval by index |
| Underlying data structure | Resizable/Growable Array | Doubly Linked List |
| RandomAccess marker interface | Implements `RandomAccess` | Does **not** implement `RandomAccess` |

### Proper Explanation

1. **Retrieval performance**
   - `ArrayList` is usually faster for `get(index)` because array indexing is direct.
   - `LinkedList` needs traversal to reach an index, so random access is slower.

2. **Insertion/deletion behavior**
   - `ArrayList` may shift elements when inserting/removing in middle (`O(n)`).
   - `LinkedList` can insert/remove efficiently once node position is reached.

3. **Memory**
   - `ArrayList` generally uses less memory overhead per element.
   - `LinkedList` uses extra memory for node links (`prev`/`next`).

4. **Practical selection rule**
   - Use `ArrayList` by default.
   - Use `LinkedList` only when your workload has frequent middle/edge insertions-deletions and limited random access.

### Quick Comparison Table (Big-O)

| Operation | ArrayList | LinkedList |
|---|---|---|
| `get(index)` | `O(1)` | `O(n)` |
| `add(e)` at end | Amortized `O(1)` | `O(1)` |
| `add(index, e)` | `O(n)` | `O(n)` traversal + link update |
| `remove(index)` | `O(n)` | `O(n)` traversal + unlink |
| Iteration | Fast cache-friendly | Good sequential, less cache-friendly |

### Small Demo

```java
import java.util.*;

public class ArrayListVsLinkedListDemo {
    public static void main(String[] args) {
        List<Integer> a = new ArrayList<>();
        List<Integer> l = new LinkedList<>();

        for (int i = 0; i < 100000; i++) {
            a.add(i);
            l.add(i);
        }

        long t1 = System.nanoTime();
        for (int i = 0; i < 5000; i++) a.get(i);
        long t2 = System.nanoTime();

        long t3 = System.nanoTime();
        for (int i = 0; i < 5000; i++) l.get(i);
        long t4 = System.nanoTime();

        System.out.println("ArrayList get time: " + (t2 - t1) + " ns");
        System.out.println("LinkedList get time: " + (t4 - t3) + " ns");
    }
}
```



---

## Vector Class (Detailed)

`Vector` is one of the oldest collection classes in Java (introduced in **Java 1.0**).  
It is part of the List hierarchy and is considered a **legacy** class.

### 1) Key Characteristics

- **Underlying data structure:** Resizable (growable) array.
- **Order:** Insertion order is preserved.
- **Duplicates:** Allowed.
- **Null values:** Allowed.
- **Heterogeneous objects:** Allowed when using raw type (`Vector`), not recommended in modern code.
- **Interfaces implemented:** `Serializable`, `Cloneable`, `RandomAccess`, `List`.
- **Thread safety:** Most methods are synchronized, so Vector is thread-safe for basic operations.
- **Performance:** Good for retrieval (`get(index)`), but generally slower than `ArrayList` due to synchronization overhead.

---

### 2) Vector-Specific and Related Methods

#### A) Adding Objects

| Method | Source | Description |
|---|---|---|
| `add(E e)` | Collection/List | Adds element at end |
| `add(int index, E element)` | List | Adds element at specific index |
| `addElement(E obj)` | Vector (legacy) | Adds element at end (legacy equivalent) |

#### B) Removing Objects

| Method | Source | Description |
|---|---|---|
| `remove(Object o)` | Collection | Removes first matching object |
| `remove(int index)` | List | Removes element at index |
| `clear()` | Collection | Removes all elements |
| `removeElement(Object obj)` | Vector (legacy) | Removes first matching object |
| `removeElementAt(int index)` | Vector (legacy) | Removes element at index |
| `removeAllElements()` | Vector (legacy) | Removes all elements |

#### C) Accessing Objects

| Method | Source | Description |
|---|---|---|
| `get(int index)` | List | Returns element at index |
| `elementAt(int index)` | Vector (legacy) | Returns element at index |
| `firstElement()` | Vector (legacy) | Returns first element |
| `lastElement()` | Vector (legacy) | Returns last element |

#### D) Utility Methods

| Method | Description |
|---|---|
| `size()` | Number of elements currently present |
| `capacity()` | Current internal array capacity |
| `elements()` | Returns `Enumeration<E>` for traversal (legacy cursor) |

---

### 3) Constructors of Vector

```java
Vector<E> v1 = new Vector<>();
Vector<E> v2 = new Vector<>(int initialCapacity);
Vector<E> v3 = new Vector<>(int initialCapacity, int capacityIncrement);
Vector<E> v4 = new Vector<>(Collection<? extends E> c);
```

#### Constructor behavior

1. `new Vector<>()`  
   - Initial capacity: **10**
   - Growth rule (default): **capacity doubles** when full.

2. `new Vector<>(initialCapacity)`  
   - Starts with provided capacity.
   - If full, default growth is doubling (when no increment specified).

3. `new Vector<>(initialCapacity, capacityIncrement)`  
   - Starts with provided capacity.
   - When full, grows by fixed `capacityIncrement`.

4. `new Vector<>(collection)`  
   - Creates a vector containing all elements from given collection.

---

### 4) Capacity Growth Demo

```java
import java.util.*;

public class VectorCapacityDemo {
    public static void main(String[] args) {
        // Default constructor: initial capacity = 10, growth = double
        Vector<Integer> v1 = new Vector<>();
        System.out.println("v1 initial size      : " + v1.size());      // 0
        System.out.println("v1 initial capacity  : " + v1.capacity());  // 10

        for (int i = 1; i <= 10; i++) v1.add(i);
        System.out.println("After 10 adds size   : " + v1.size());       // 10
        System.out.println("After 10 adds cap    : " + v1.capacity());   // 10

        v1.add(11); // triggers grow
        System.out.println("After 11th add size  : " + v1.size());       // 11
        System.out.println("After 11th add cap   : " + v1.capacity());   // 20

        // (10, 5): grows by +5
        Vector<Integer> v2 = new Vector<>(10, 5);
        for (int i = 1; i <= 11; i++) v2.add(i);
        System.out.println("v2 (10,5) size       : " + v2.size());       // 11
        System.out.println("v2 (10,5) capacity   : " + v2.capacity());   // 15
    }
}
```

---

### 5) One Comprehensive Demo (Constructors + Methods)

```java
import java.util.*;

public class VectorAllInOneDemo {
    public static void main(String[] args) {
        // Constructors
        Vector<Object> vDefault = new Vector<>();
        Vector<String> vCap = new Vector<>(5);
        Vector<Integer> vCapInc = new Vector<>(3, 2);
        Vector<String> vFromCollection = new Vector<>(Arrays.asList("A", "B", "C"));

        // Interface checks
        System.out.println(vDefault instanceof java.io.Serializable); // true
        System.out.println(vDefault instanceof Cloneable);            // true
        System.out.println(vDefault instanceof RandomAccess);         // true

        // Add methods
        vDefault.add("Java");          // List/Collection
        vDefault.add(30);              // heterogeneous (raw/object use)
        vDefault.add(null);            // null allowed
        vDefault.add("Java");          // duplicate allowed
        vDefault.add(1, "Python");     // add at index
        vDefault.addElement("Legacy"); // vector legacy add

        System.out.println("After add operations: " + vDefault);

        // Access methods
        System.out.println("get(0): " + vDefault.get(0));
        System.out.println("elementAt(1): " + vDefault.elementAt(1));
        System.out.println("firstElement(): " + vDefault.firstElement());
        System.out.println("lastElement(): " + vDefault.lastElement());

        // Utility
        System.out.println("size(): " + vDefault.size());
        System.out.println("capacity(): " + vDefault.capacity());

        // Enumeration (legacy cursor)
        System.out.print("elements(): ");
        Enumeration<Object> en = vDefault.elements();
        while (en.hasMoreElements()) {
            System.out.print(en.nextElement() + " ");
        }
        System.out.println();

        // Remove methods
        vDefault.remove("Java");          // removes first matching
        vDefault.remove(0);               // removes by index
        vDefault.removeElement("Legacy"); // legacy remove by object
        if (!vDefault.isEmpty()) {
            vDefault.removeElementAt(0);  // legacy remove by index
        }

        System.out.println("After remove operations: " + vDefault);

        // clear and legacy clear
        vDefault.clear();
        System.out.println("After clear(): " + vDefault);

        vFromCollection.removeAllElements(); // legacy clear
        System.out.println("After removeAllElements(): " + vFromCollection);

        // Capacity increment demo vector
        vCapInc.add(1);
        vCapInc.add(2);
        vCapInc.add(3);
        System.out.println("vCapInc capacity before full grow: " + vCapInc.capacity()); // 3
        vCapInc.add(4); // grows by +2 => 5
        System.out.println("vCapInc capacity after grow: " + vCapInc.capacity());       // 5

        // constructor from collection
        System.out.println("vFromCollection (initial): " + new Vector<>(Arrays.asList("A", "B", "C")));
        System.out.println("vCap initial capacity: " + vCap.capacity()); // 5
    }
}
```

---

### 6) Quick Rules

- Prefer `ArrayList` in modern single-threaded code.
- Use `Vector` mainly for:
  - legacy compatibility, or
  - simple built-in synchronized list behavior.
- For modern concurrent scenarios, prefer:
  - `Collections.synchronizedList(new ArrayList<>())`, or
  - `CopyOnWriteArrayList` (read-heavy cases).

<!<!-- ...existing code... -->

---

## Stack Class (Detailed)

`Stack` is a **legacy class** in Java (since **1.0**) and is a child class of `Vector`.

### Key Characteristics

- **Inheritance:** `Stack` extends `Vector`.
- **Thread-safety:** Inherits synchronized behavior from `Vector`.
- **Principle:** Follows **LIFO** (Last In First Out).
- **Legacy note:** Works fine, but in modern code `Deque` (`ArrayDeque`) is often preferred.

### Constructor

```java
Stack<E> s = new Stack<>();
```

Creates an empty stack.

### Core Stack Methods

| Method | Return Type | Description |
|---|---|---|
| `push(E item)` | `E` | Pushes item onto top of stack and returns it |
| `pop()` | `E` | Removes and returns top element |
| `peek()` | `E` | Returns top element without removing |
| `empty()` | `boolean` | Returns `true` if stack is empty |
| `search(Object o)` | `int` | Returns 1-based offset from top, else `-1` |

### Important: `search()` Offset Rule

`search()` does **not** use normal 0-based index.

- Top element offset = `1`
- Next below top = `2`
- If element not found = `-1`

Example stack: `[A, B, C]` (top is `C`)

- `search("C")` -> `1`
- `search("B")` -> `2`
- `search("A")` -> `3`
- `search("Z")` -> `-1`

### Demo Program

```java
import java.util.EmptyStackException;
import java.util.Stack;

public class StackDemo {
    public static void main(String[] args) {
        Stack<String> s = new Stack<>();

        // push
        s.push("A");
        s.push("B");
        s.push("C");
        System.out.println("Stack after push: " + s); // [A, B, C]

        // peek
        System.out.println("peek(): " + s.peek()); // C
        System.out.println("After peek stack: " + s); // unchanged

        // search (1-based from top)
        System.out.println("search(\"A\"): " + s.search("A")); // 3
        System.out.println("search(\"C\"): " + s.search("C")); // 1
        System.out.println("search(\"Z\"): " + s.search("Z")); // -1

        // pop
        System.out.println("pop(): " + s.pop()); // C
        System.out.println("After pop: " + s); // [A, B]

        // empty
        System.out.println("empty(): " + s.empty()); // false
        s.pop(); // B
        s.pop(); // A
        System.out.println("empty() after removing all: " + s.empty()); // true

        // pop on empty -> EmptyStackException
        try {
            s.pop();
        } catch (EmptyStackException e) {
            System.out.println("Exception: " + e);
        }
    }
}
```

### Quick Rule

- If your requirement is strict **LIFO**, Stack works.
- For new code, prefer:

```java
// Recommended modern stack style:
Deque<String> stack = new ArrayDeque<>();
stack.push("A");
stack.push("B");
System.out.println(stack.pop()); // B
```

<!-- ...existing code... -->
<!-- ...existing code... -->

---

## Cursors in Java Collection Framework (Detailed)

A **cursor** is used to retrieve objects from a collection **one by one**.

If a collection contains many elements, a cursor helps process each element sequentially instead of handling everything at once.

### Types of Cursors in Java

1. `Enumeration` (legacy, Java 1.0)
2. `Iterator` (Java 1.2)
3. `ListIterator` (Java 1.2, only for List)

---

## Enumeration Interface (Legacy Cursor)

`Enumeration` is the oldest cursor type in Java, introduced in **Java 1.0**.

It is mainly used with **legacy classes** like:

- `Vector`
- `Hashtable`

### How to Get Enumeration Object

For `Vector`, use:

```java
Enumeration<E> e = vector.elements();
```

Legacy/raw form (older style):

```java
Enumeration e = v.elements();
```

### Core Methods of Enumeration

| Method | Return Type | Purpose |
|---|---|---|
| `hasMoreElements()` | `boolean` | Checks whether more elements are available |
| `nextElement()` | `E` / `Object` | Returns the next element |

### Example 1: Basic Traversal with Enumeration

```java
import java.util.Enumeration;
import java.util.Vector;

public class EnumerationBasicDemo {
    public static void main(String[] args) {
        Vector<String> v = new Vector<>();
        v.add("A");
        v.add("B");
        v.add("C");

        Enumeration<String> e = v.elements();

        while (e.hasMoreElements()) {
            System.out.println(e.nextElement());
        }
    }
}
```

### Example 2: Durga-style Filtering (Print Even Numbers Only)

```java
import java.util.Enumeration;
import java.util.Vector;

public class EnumerationEvenFilterDemo {
    public static void main(String[] args) {
        Vector<Integer> v = new Vector<>();

        // Fill with 0 to 10
        for (int i = 0; i <= 10; i++) {
            v.add(i);
        }

        // Get cursor
        Enumeration<Integer> e = v.elements();

        // Process one by one and print only even numbers
        while (e.hasMoreElements()) {
            Integer n = e.nextElement();
            if (n % 2 == 0) {
                System.out.print(n + " ");
            }
        }
        // Output: 0 2 4 6 8 10
    }
}
```

### Limitations of Enumeration

1. **Read-only cursor**  
   You can read elements, but cannot remove/update during traversal.

2. **Legacy-focused**  
   Mostly useful with old classes (`Vector`, `Hashtable`).

3. **Less powerful than Iterator/ListIterator**  
   No bidirectional traversal, no modification methods.

---

## Quick Comparison: Enumeration vs Iterator vs ListIterator

| Feature | Enumeration | Iterator | ListIterator |
|---|---|---|---|
| Introduced | 1.0 | 1.2 | 1.2 |
| Works with | Legacy classes | All collection types | List only |
| Direction | Forward only | Forward only | Forward + backward |
| Remove support | No | Yes (`remove`) | Yes (`remove`) |
| Add/Set support | No | No | Yes (`add`, `set`) |
| Legacy/Modern | Legacy | Modern | Modern |

### Key Takeaways

- `Enumeration` is the oldest cursor and still valid for legacy collections.
- Main methods are only `hasMoreElements()` and `nextElement()`.
- Best for simple read-only iteration on `Vector`/`Hashtable`.
- For modern code, prefer `Iterator` or `ListIterator`.

<!-- ...existing code... -->
<!-- ...existing code... -->

---

## Iterator Interface (Second Cursor in Java)

`Iterator` was introduced in **Java 1.2** to overcome key limitations of `Enumeration`.

### Why Iterator Was Introduced (Limitations of Enumeration)

1. **Not universal**  
   `Enumeration` mainly works with legacy classes like `Vector` and `Hashtable`.

2. **Read-only cursor**  
   `Enumeration` cannot remove elements during traversal.

### Advantages of Iterator

1. **Universal cursor**  
   Works with almost all Collection implementations (`ArrayList`, `LinkedList`, `HashSet`, etc.).

2. **Read + Remove support**  
   Allows element retrieval and safe removal while iterating.

---

### How to Obtain Iterator

```java
Iterator<T> itr = collection.iterator();
```

Example:

```java
Collection<Integer> c = new ArrayList<>();
Iterator<Integer> itr = c.iterator();
```

---

### Core Methods of Iterator

| Method | Return Type | Purpose |
|---|---|---|
| `hasNext()` | `boolean` | Checks if next element exists |
| `next()` | `E` | Returns next element and moves cursor forward |
| `remove()` | `void` | Removes last element returned by `next()` |

> `remove()` can be called only after `next()`.  
> Calling `remove()` twice without another `next()` causes `IllegalStateException`.

---

### Practical Demo (Durga-style): Keep Only Even Numbers

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class IteratorEvenFilterDemo {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();

        // 0 to 10
        for (int i = 0; i <= 10; i++) {
            list.add(i);
        }

        System.out.println("Before iteration: " + list);

        Iterator<Integer> itr = list.iterator();
        while (itr.hasNext()) {
            Integer n = itr.next();
            if (n % 2 == 0) {
                System.out.print(n + " "); // read
            } else {
                itr.remove();              // remove odd numbers safely
            }
        }

        System.out.println("\nAfter iteration: " + list); // [0, 2, 4, 6, 8, 10]
    }
}
```

---

### What Iterator Still Cannot Do

1. **Forward-only cursor**  
   No backward traversal.

2. **No direct replace/add during iteration**  
   It supports `remove()`, but not `set()` or `add()`.

These limitations are solved by **ListIterator** (for List types).

### Key Takeaways

- `Iterator` is the standard cursor for modern collection traversal.
- It supports safe deletion during iteration (`itr.remove()`).
- It is more powerful than `Enumeration`, but less powerful than `ListIterator`.

<!-- ...existing code... -->
<!-- ...existing code... -->

---

## ListIterator Interface (Third and Most Powerful Cursor)

`ListIterator` is the third cursor in Java and a child interface of `Iterator`.

### Why ListIterator?

It overcomes limitations of `Enumeration` and `Iterator`:

- **Bidirectional traversal** (forward + backward)
- Supports **read, remove, replace (`set`) and add (`add`)**
- Works only with **List** implementations (`ArrayList`, `LinkedList`, `Vector`, `Stack`)

---

### How to Obtain ListIterator

```java
ListIterator<E> ltr = list.listIterator();
ListIterator<E> ltrFromIndex = list.listIterator(index);
```

---

### 9 Methods of ListIterator

#### 1) Forward Direction Methods

| Method | Return Type | Purpose |
|---|---|---|
| `hasNext()` | `boolean` | Checks if next element exists |
| `next()` | `E` | Returns next element and moves cursor forward |
| `nextIndex()` | `int` | Index of element that would be returned by next `next()` |

#### 2) Backward Direction Methods

| Method | Return Type | Purpose |
|---|---|---|
| `hasPrevious()` | `boolean` | Checks if previous element exists |
| `previous()` | `E` | Returns previous element and moves cursor backward |
| `previousIndex()` | `int` | Index of element that would be returned by next `previous()` |

#### 3) Modification Methods

| Method | Return Type | Purpose |
|---|---|---|
| `remove()` | `void` | Removes last element returned by `next()`/`previous()` |
| `set(E e)` | `void` | Replaces last element returned by `next()`/`previous()` |
| `add(E e)` | `void` | Inserts element before next element (cursor position insert) |

---

### Practical Demo (Durga-style)

```java
import java.util.LinkedList;
import java.util.ListIterator;

public class ListIteratorDemo {
    public static void main(String[] args) {
        LinkedList<String> names = new LinkedList<>();
        names.add("balakrishna");
        names.add("venki");
        names.add("chiru");
        names.add("nag");

        System.out.println("Before: " + names);

        ListIterator<String> ltr = names.listIterator();
        while (ltr.hasNext()) {
            String s = ltr.next();

            if (s.equalsIgnoreCase("venki")) {
                ltr.remove(); // remove venki
            } else if (s.equalsIgnoreCase("chiru")) {
                ltr.set("charan"); // replace chiru -> charan
            } else if (s.equalsIgnoreCase("nag")) {
                ltr.add("chaitu"); // add after nag (in forward traversal context)
            }
        }

        System.out.println("After : " + names);
        // Output: [balakrishna, charan, nag, chaitu]

        // Backward traversal demo
        System.out.print("Backward traversal: ");
        while (ltr.hasPrevious()) {
            System.out.print(ltr.previous() + " ");
        }
    }
}
```

---

### Key Limitation

`ListIterator` is **not universal**.  
It works only for `List` classes, not for `Set` or `Map`.

### Quick Comparison

| Feature | Enumeration | Iterator | ListIterator |
|---|---|---|---|
| Direction | Forward only | Forward only | Forward + Backward |
| Remove | No | Yes | Yes |
| Set/Replace | No | No | Yes |
| Add during iteration | No | No | Yes |
| Works with | Legacy classes | Most Collections | List only |

<!-- ...existing code... -->
<!-- ...existing code... -->

---

## Comparison of Java Cursors: Enumeration vs Iterator vs ListIterator

This section summarizes the three Java cursors side-by-side.

### Comparison Table

| Property | Enumeration | Iterator | ListIterator |
|---|---|---|---|<!-- ...existing code... -->

---

## Implementation Classes Behind Cursor Interfaces (Important Concept)

A common doubt:

> `Enumeration`, `Iterator`, and `ListIterator` are interfaces.  
> Interfaces cannot be instantiated directly.  
> Then how do we “get objects” from `elements()`, `iterator()`, and `listIterator()`?

### Correct Concept

We never create interface objects directly.  
Instead, collection classes return objects of **internal implementation classes** that implement those interfaces.

- `elements()` returns an object implementing `Enumeration`
- `iterator()` returns an object implementing `Iterator`
- `listIterator()` returns an object implementing `ListIterator`

So the reference type is interface type, but actual object type is an internal class.

---

### Vector Example (Internal Cursor Implementations)

For `Vector`, commonly observed internal classes are:

| Cursor Interface | Method | Typical Runtime Class Name |
|---|---|---|
| `Enumeration` | `elements()` | `java.util.Vector$1` |
| `Iterator` | `iterator()` | `java.util.Vector$Itr` |
| `ListIterator` | `listIterator()` | `java.util.Vector$ListItr` |

> Note: Exact class names can vary slightly by JDK version/vendor, but concept remains the same.

---

### Program to Reveal Actual Implementation Class Names

```java
import java.util.*;

public class CursorImplClassNamesDemo {
    public static void main(String[] args) {
        Vector<Integer> v = new Vector<>();
        v.add(10);
        v.add(20);
        v.add(30);

        Enumeration<Integer> e = v.elements();
        Iterator<Integer> itr = v.iterator();
        ListIterator<Integer> ltr = v.listIterator();

        System.out.println("Enumeration impl: " + e.getClass().getName());
        System.out.println("Iterator impl   : " + itr.getClass().getName());
        System.out.println("ListIterator impl: " + ltr.getClass().getName());
    }
}
```

---

### Why Java Uses This Design

1. **Abstraction**  
   You code to interfaces (`Iterator`, `ListIterator`), not concrete classes.

2. **Flexibility**  
   Different collections can provide different internal traversal logic.

3. **Uniform API**  
   Same method style (`iterator()`) works across many collections, even though implementation classes differ.

### Key Takeaway

- You hold cursor objects in interface references.
- Actual objects are returned from hidden/internal implementation classes.
- This is a core OOP design pattern: **program to interface, not implementation**.

<!-- ...existing code... -->
| Applicability | Legacy classes only (`Vector`, `Stack`, `Hashtable`) | Any Collection class (universal cursor) | Only `List` implemented classes |
| Movement | Forward only | Forward only | Forward + Backward (bidirectional) |
| Accessibility | Read-only | Read + Remove | Read + Remove + Replace (`set`) + Add (`add`) |
| Obtained by | `elements()` | `iterator()` | `listIterator()` |
| No. of methods | 2 | 3 | 9 |
| Introduced in | Java 1.0 (Legacy) | Java 1.2 (Non-legacy) | Java 1.2 (Non-legacy) |

### Methods Overview

#### Enumeration (2 methods)
- `hasMoreElements()`
- `nextElement()`

#### Iterator (3 methods)
- `hasNext()`
- `next()`
- `remove()`

#### ListIterator (9 methods)
- `hasNext()`, `next()`, `nextIndex()`
- `hasPrevious()`, `previous()`, `previousIndex()`
- `remove()`, `set(E e)`, `add(E e)`

### Key Takeaways

1. **Iterator is universal** for most collections.
2. **Enumeration is limited** to legacy collections and supports only read.
3. **ListIterator is most powerful**, but only for `List`.
4. Only **ListIterator** supports backward traversal.
5. If you need add/set during traversal, use **ListIterator**.

### Quick Cursor Creation Examples

```java
import java.util.*;

public class CursorCreationDemo {
    public static void main(String[] args) {
        Vector<Integer> v = new Vector<>(Arrays.asList(10, 20, 30));
        Enumeration<Integer> e = v.elements();

        List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));
        Iterator<Integer> itr = list.iterator();
        ListIterator<Integer> ltr = list.listIterator();

        System.out.println("Cursors created successfully.");
    }
}
```

<!-- ...existing code... -->
<!-- ...existing code... -->

---

## HashSet (Detailed)

### Set Interface Quick Notes

1. `Set` is a child interface of `Collection`.
2. Use `Set` when duplicates are not allowed.
3. `Set` does not define new methods; it uses `Collection` methods only.

### HashSet Key Characteristics

- Underlying structure: hash table based (internally backed by `HashMap`).
- Duplicates are not allowed.
- Insertion order is not preserved.
- Heterogeneous objects are allowed (without strict generics).
- One `null` value is allowed.
- Implements `Serializable` and `Cloneable` (not `RandomAccess`).
- Best when frequent operation is search/contains (average O(1)).

> Note: `add(E e)` in `Set` returns:
> - `true` if element was added
> - `false` if it was a duplicate

---

### Constructors of HashSet

```java
HashSet<E> h1 = new HashSet<>();
HashSet<E> h2 = new HashSet<>(int initialCapacity);
HashSet<E> h3 = new HashSet<>(int initialCapacity, float loadFactor);
HashSet<E> h4 = new HashSet<>(Collection<? extends E> c);
```

### Constructor Behavior

1. `new HashSet<>()`
   - Default initial capacity = `16`
   - Default load factor (fill ratio) = `0.75`

2. `new HashSet<>(initialCapacity)`
   - Custom initial capacity
   - Default load factor = `0.75`

3. `new HashSet<>(initialCapacity, loadFactor)`
   - Custom initial capacity + custom load factor

4. `new HashSet<>(collection)`
   - Creates HashSet from another collection (inter-conversion)

---

### One Demo: Set + HashSet Properties + Constructors

```java
import java.io.Serializable;
import java.util.*;

public class HashSetAllInOneDemo {
    public static void main(String[] args) {
        // Constructors
        HashSet<Object> h1 = new HashSet<>();
        HashSet<String> h2 = new HashSet<>(32);
        HashSet<Integer> h3 = new HashSet<>(16, 0.75f);
        HashSet<String> h4 = new HashSet<>(Arrays.asList("A", "B", "A", "C"));

        // Interface checks
        System.out.println(h1 instanceof Serializable); // true
        System.out.println(h1 instanceof Cloneable);    // true
        System.out.println(h1 instanceof RandomAccess); // false

        // Add behavior
        System.out.println(h1.add("Durga"));  // true
        System.out.println(h1.add(10));       // true (heterogeneous if Object)
        System.out.println(h1.add(null));     // true
        System.out.println(h1.add("Durga"));  // false (duplicate)

        // Collection methods (Set has no new methods)
        System.out.println("HashSet: " + h1);
        System.out.println("Contains 10? " + h1.contains(10));
        System.out.println("Size: " + h1.size());

        // Remove
        h1.remove(10);
        System.out.println("After remove(10): " + h1);

        // Iteration
        System.out.print("Iterating: ");
        for (Object o : h1) {
            System.out.print(o + " ");
        }
        System.out.println();

        // From collection constructor: duplicates removed automatically
        System.out.println("h4 from collection: " + h4); // [A, B, C] (order not guaranteed)

        // Basic set operations
        Set<Integer> s1 = new HashSet<>(Arrays.asList(1, 2, 3, 4));
        Set<Integer> s2 = new HashSet<>(Arrays.asList(3, 4, 5, 6));

        Set<Integer> union = new HashSet<>(s1);
        union.addAll(s2);

        Set<Integer> intersection = new HashSet<>(s1);
        intersection.retainAll(s2);

        Set<Integer> difference = new HashSet<>(s1);
        difference.removeAll(s2);

        System.out.println("Union: " + union);
        System.out.println("Intersection: " + intersection);
        System.out.println("Difference: " + difference);
    }
}
```

---

### Set Hierarchy Snapshot

```text
Collection (1.2)
  -> Set (1.2)
      -> HashSet (1.2)
          -> LinkedHashSet (1.4)
      -> SortedSet (1.2)
          -> NavigableSet (1.6)
              -> TreeSet (1.2)
```

<!-- ...existing code... -->
<!-- ...existing code... -->

### Demo Program for HashSet (Durga-style)

```java
import java.util.HashSet;

public class HashSetDemo {
    public static void main(String[] args) {
        HashSet<Object> h = new HashSet<>();

        h.add("B");
        h.add("C");
        h.add("D");
        h.add("Z");
        h.add(null);
        h.add(10);

        // Duplicate insert -> false
        System.out.println(h.add("Z")); // false

        // Order is not guaranteed
        System.out.println(h); // Example: [null, D, B, C, 10, Z]
    }
}
```

**What this proves:**
- Duplicates are not allowed (`add("Z")` second time returns `false`)
- `null` is allowed (one null)
- Heterogeneous values are possible with `HashSet<Object>`
- Insertion order is not preserved

---

### Load Factor / Fill Ratio (HashSet)

`HashSet` is internally backed by a `HashMap`.

- **Initial Capacity**: number of buckets initially allocated.
- **Load Factor**: threshold percentage to trigger resize.
- Default load factor = **0.75**

Resize threshold formula:

```text
threshold = capacity * loadFactor
```

Example with default values:

```text
capacity = 16
loadFactor = 0.75
threshold = 12
```

When element count crosses threshold, internal table grows (rehash happens).

> Correct understanding: load factor does **not** create a “new HashSet object”; it triggers internal rehash/resize of the backing table.

---

### Constructor + Load Factor Example

```java
import java.util.HashSet;

public class HashSetLoadFactorDemo {
    public static void main(String[] args) {
        HashSet<Integer> h1 = new HashSet<>();            // cap=16, lf=0.75
        HashSet<Integer> h2 = new HashSet<>(32);          // cap=32, lf=0.75
        HashSet<Integer> h3 = new HashSet<>(32, 0.50f);   // cap=32, lf=0.50

        for (int i = 1; i <= 20; i++) {
            h1.add(i);
            h2.add(i);
            h3.add(i);
        }

        System.out.println("h1 size: " + h1.size());
        System.out.println("h2 size: " + h2.size());
        System.out.println("h3 size: " + h3.size());
    }
}

---

## LinkedHashSet (Detailed)

### Overview

`LinkedHashSet` is a child class of `HashSet` introduced in **Java 1.4**.

It combines the properties of `HashSet` (no duplicates, hash table performance) with the ordering property of `LinkedList` (insertion order preservation).

### How It Works

`LinkedHashSet` uses:
- **Hash Table** for efficient searching and storage (like `HashSet`)
- **Doubly Linked List** to maintain insertion order (like `LinkedList`)

This hybrid approach gives you both:
- **Fast search performance** (~O(1) average)
- **Predictable iteration order** (insertion order)

### Key Characteristics of LinkedHashSet

1. **No Duplicates** - Like `HashSet`, duplicates are automatically rejected
2. **Preserves Insertion Order** - Unlike `HashSet`, the order in which elements were added is maintained
3. **Hash Table + Linked List** - Internally uses both structures for optimal performance and ordering
4. **Single Null Value** - One `null` is allowed (same as `HashSet`)
5. **Heterogeneous Objects** - Allowed without strict generics
6. **Not Thread-Safe** - Like `HashSet`, synchronization is not built-in
7. **Implements Serializable and Cloneable** - Can be copied and persisted

### Constructors of LinkedHashSet

```java
LinkedHashSet<E> lhs1 = new LinkedHashSet<>();
LinkedHashSet<E> lhs2 = new LinkedHashSet<>(int initialCapacity);
LinkedHashSet<E> lhs3 = new LinkedHashSet<>(int capacity, float loadFactor);
LinkedHashSet<E> lhs4 = new LinkedHashSet<>(Collection<? extends E> c);
```

### Constructor Details

1. `new LinkedHashSet<>()`
   - Default initial capacity = `16`
   - Default load factor = `0.75`

2. `new LinkedHashSet<>(initialCapacity)`
   - Custom initial capacity
   - Default load factor = `0.75`

3. `new LinkedHashSet<>(capacity, loadFactor)`
   - Custom capacity and load factor for fine-tuned performance

4. `new LinkedHashSet<>(collection)`
   - Creates LinkedHashSet from another collection
   - Preserves the order of items added from the collection

### Comparison: HashSet vs LinkedHashSet

| Feature | HashSet | LinkedHashSet |
|---|---|---|
| **Child Class of** | `AbstractSet` | `HashSet` |
| **Version** | Java 1.2 | Java 1.4 |
| **Underlying Structure** | Hash Table | Hash Table + Doubly Linked List |
| **Insertion Order** | Not preserved | Preserved |
| **Duplicates** | Not allowed | Not allowed |
| **Performance** | Fast (~O(1)) | Fast (~O(1) with slight overhead) |
| **Memory** | Lower overhead | Higher (extra linked list pointers) |
| **Iteration Order** | Unpredictable | Insertion order |
| **Use Case** | Random access, fast unique collection | Need unique elements in order |

### Comprehensive LinkedHashSet Example (All Functionality)

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Iterator;
import java.util.LinkedHashSet;
import java.util.Set;

public class LinkedHashSetComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== LINKEDHASHSET COMPREHENSIVE DEMO ==========\n");

        // Step 1: Create LinkedHashSet using different constructors
        System.out.println("Step 1 - Constructors:");
        Set<Integer> lhs1 = new LinkedHashSet<>();                    // Default
        Set<Integer> lhs2 = new LinkedHashSet<>(32);                  // With capacity
        Set<Integer> lhs3 = new LinkedHashSet<>(
            Arrays.asList(50, 40, 30, 40, 50, 20)                     // From collection
        );
        System.out.println("Empty LinkedHashSet: " + lhs1);
        System.out.println("From collection: " + lhs3); // [50, 40, 30, 20] - duplicates removed
        System.out.println();

        // Step 2: Add Elements - Demonstrate insertion order preservation
        System.out.println("Step 2 - Adding Elements (insertion order preserved):");
        Set<String> languages = new LinkedHashSet<>();
        languages.add("Java");
        languages.add("Python");
        languages.add("C++");
        languages.add("Go");
        languages.add(null);        // One null allowed
        languages.add("JavaScript");
        System.out.println("After adding: " + languages);
        System.out.println("Size: " + languages.size());
        System.out.println();

        // Step 3: Try Adding Duplicates - Will be ignored
        System.out.println("Step 3 - Adding Duplicates (rejected):");
        boolean added1 = languages.add("Java");
        boolean added2 = languages.add("Python");
        boolean added3 = languages.add("Rust");
        System.out.println("Added 'Java' (duplicate)? " + added1);    // false
        System.out.println("Added 'Python' (duplicate)? " + added2);  // false
        System.out.println("Added 'Rust' (new)? " + added3);          // true
        System.out.println("After adding duplicates: " + languages);
        System.out.println();

        // Step 4: Check Operations
        System.out.println("Step 4 - Check Operations:");
        System.out.println("Contains 'Java'? " + languages.contains("Java"));      // true
        System.out.println("Contains 'Ruby'? " + languages.contains("Ruby"));      // false
        System.out.println("Contains null? " + languages.contains(null));          // true
        System.out.println("Is empty? " + languages.isEmpty());                    // false
        System.out.println();

        // Step 5: Remove Operations
        System.out.println("Step 5 - Remove Operations:");
        languages.remove("Python");
        System.out.println("After remove('Python'): " + languages);
        languages.remove(null);
        System.out.println("After remove(null): " + languages);
        System.out.println();

        // Step 6: Forward Iteration - Shows insertion order
        System.out.println("Step 6 - Forward Iteration (insertion order):");
        System.out.print("Iterating: ");
        for (String lang : languages) {
            System.out.print(lang + " ");
        }
        System.out.println();
        System.out.println();

        // Step 7: Iterator with Safe Removal
        System.out.println("Step 7 - Safe Removal During Iteration:");
        System.out.println("Before iterator removal: " + languages);
        Iterator<String> it = languages.iterator();
        while (it.hasNext()) {
            String lang = it.next();
            if (lang.length() <= 2) {  // Remove short language names
                it.remove();
                System.out.println("  Removed: " + lang);
            }
        }
        System.out.println("After iterator removal: " + languages);
        System.out.println();

        // Step 8: Comparison with HashSet - Order difference
        System.out.println("Step 8 - Comparison: HashSet vs LinkedHashSet");
        int[] nums = {5, 2, 8, 2, 9, 5, 1};
        
        Set<Integer> hashSet = new HashSet<>();
        Set<Integer> linkedHashSet = new LinkedHashSet<>();
        for (int num : nums) {
            hashSet.add(num);
            linkedHashSet.add(num);
        }
        
        System.out.println("HashSet (random order):      " + hashSet);
        System.out.println("LinkedHashSet (insert order): " + linkedHashSet); // [5, 2, 8, 9, 1]
        System.out.println();

        // Step 9: Clear Operation
        System.out.println("Step 9 - Clear Operation:");
        Set<String> temp = new LinkedHashSet<>(Arrays.asList("A", "B", "C"));
        System.out.println("Before clear: " + temp);
        temp.clear();
        System.out.println("After clear: " + temp);
        System.out.println("Is empty? " + temp.isEmpty());
        System.out.println();

        // Step 10: Real-World Use Case - Recent Items Cache
        System.out.println("Step 10 - Real-World: Recent Items Cache");
        Set<String> recentViews = new LinkedHashSet<>();
        recentViews.add("Product-101");
        recentViews.add("Product-505");
        recentViews.add("Product-202");
        recentViews.add("Product-101");  // User views again - still maintains order
        recentViews.add("Product-303");
        recentViews.add("Product-404");
        
        // Simulate limiting to 5 most recent
        if (recentViews.size() > 5) {
            String oldest = recentViews.iterator().next();
            recentViews.remove(oldest);
        }
        
        System.out.println("Recent products (newest first when reversed): " + recentViews);
        System.out.println();

        // Step 11: Set Operations - Union, Intersection, Difference
        System.out.println("Step 11 - Set Operations:");
        Set<Integer> set1 = new LinkedHashSet<>(Arrays.asList(1, 2, 3, 4));
        Set<Integer> set2 = new LinkedHashSet<>(Arrays.asList(3, 4, 5, 6));
        
        // Union
        Set<Integer> union = new LinkedHashSet<>(set1);
        union.addAll(set2);
        System.out.println("Set1: " + set1);
        System.out.println("Set2: " + set2);
        System.out.println("Union: " + union);
        
        // Intersection
        Set<Integer> intersection = new LinkedHashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Intersection: " + intersection);
        
        // Difference
        Set<Integer> difference = new LinkedHashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Difference (Set1-Set2): " + difference);
        System.out.println();

        // Step 12: Summary Table
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ No duplicates - Automatically rejected");
        System.out.println("✓ Insertion order - Preserved like LinkedList");
        System.out.println("✓ Fast operations - O(1) add/remove/contains");
        System.out.println("✓ Null support - One null value allowed");
        System.out.println("✓ Iterator safe - Can remove during iteration");
        System.out.println("✓ Set operations - Union, intersection, difference");
        System.out.println("✓ Real-world use - Caching, recent items, ordered unique data");
    }
}

/* Output:
========== LINKEDHASHSET COMPREHENSIVE DEMO ==========

Step 1 - Constructors:
Empty LinkedHashSet: []
From collection: [50, 40, 30, 20]

Step 2 - Adding Elements (insertion order preserved):
After adding: [Java, Python, C++, Go, null, JavaScript]
Size: 6

Step 3 - Adding Duplicates (rejected):
Added 'Java' (duplicate)? false
Added 'Python' (duplicate)? false
Added 'Rust' (new)? true
After adding duplicates: [Java, Python, C++, Go, null, JavaScript, Rust]

Step 4 - Check Operations:
Contains 'Java'? true
Contains 'Ruby'? false
Contains null? true
Is empty? false

Step 5 - Remove Operations:
After remove('Python'): [Java, C++, Go, null, JavaScript, Rust]
After remove(null): [Java, C++, Go, JavaScript, Rust]

Step 6 - Forward Iteration (insertion order):
Iterating: Java C++ Go JavaScript Rust

Step 7 - Safe Removal During Iteration:
Before iterator removal: [Java, C++, Go, JavaScript, Rust]
  Removed: Go
After iterator removal: [Java, C++, JavaScript, Rust]

Step 8 - Comparison: HashSet vs LinkedHashSet
HashSet (random order):      [1, 2, 5, 8, 9]
LinkedHashSet (insert order): [5, 2, 8, 9, 1]

Step 9 - Clear Operation:
Before clear: [A, B, C]
After clear: []
Is empty? true

Step 10 - Real-World: Recent Items Cache
Recent products (newest first when reversed): [Product-505, Product-202, Product-101, Product-303, Product-404]

Step 11 - Set Operations:
Set1: [1, 2, 3, 4]
Set2: [3, 4, 5, 6]
Union: [1, 2, 3, 4, 5, 6]
Intersection: [3, 4]
Difference (Set1-Set2): [1, 2]

========== SUMMARY ==========
✓ No duplicates - Automatically rejected
✓ Insertion order - Preserved like LinkedList
✓ Fast operations - O(1) add/remove/contains
✓ Null support - One null value allowed
✓ Iterator safe - Can remove during iteration
✓ Set operations - Union, intersection, difference
✓ Real-world use - Caching, recent items, ordered unique data
*/
```

### Key Differences from HashSet

1. **Order Guarantee**
   - `HashSet`: No order guaranteed
   - `LinkedHashSet`: Insertion order guaranteed

2. **Performance Characteristics**
   - Both have O(1) average performance for add/remove/contains
   - `LinkedHashSet` has slightly more memory overhead due to linked list

3. **Use Cases**
   - `HashSet`: When order doesn't matter, max performance needed
   - `LinkedHashSet`: When you need unique elements in order (caching, recently used items)

### When to Use LinkedHashSet

Use `LinkedHashSet` when you need:

1. **Unique Elements** - No duplicates allowed
2. **Insertion Order** - Elements appear in the order they were added
3. **Predictable Iteration** - You want consistent ordering across runs
4. **Fast Performance** - O(1) add/remove/contains operations
5. **Real-World Examples**:
   - Browser history (most recent first)
   - Recently used files
   - Cache of unique, ordered items
   - Maintaining insertion sequence of unique values
   - Log entries with unique identifiers

### Best Practices

1. **Use when order matters** with unique elements
2. **Prefer over TreeSet** if you don't need sorting
3. **Consider memory** - linked list adds overhead
4. **For caching**, it's ideal because it maintains order while preventing duplicates
5. **Thread-safe wrapper** if needed:
   ```java
   Set<String> syncSet = Collections.synchronizedSet(new LinkedHashSet<>());
   ```

### Quick Takeaways

1. **LinkedHashSet = HashSet + Insertion Order**
2. **Child class of HashSet** - Inherits all its behavior
3. **Introduced in Java 1.4** - Newer than HashSet (1.2)
4. **Hybrid performance** - Hash table speed + linked list ordering
5. **Perfect for caching** - Maintains insertion order, prevents duplicates
6. **No duplicates allowed** - Same as HashSet
7. **Slightly slower than HashSet** - But not significantly
8. **Ideal for maintaining sequences** - When order and uniqueness both matter
9. **Single null allowed** - Same as HashSet
10. **O(1) operations** - Add, remove, contains all average O(1)

---

## SortedSet Interface (Detailed)

### Overview

`SortedSet` is a child interface of `Set` introduced in **Java 1.2**.

It represents a set where **all elements are stored in sorted order** based on either natural sorting or a custom `Comparator`.

Unlike regular `Set` implementations (like `HashSet`), where there is no concept of "first" or "last" element, a `SortedSet` guarantees that elements are ordered.

### Key Characteristics of SortedSet

1. **No Duplicates** - Like all sets, duplicates are not allowed
2. **Sorted Storage** - Elements are automatically maintained in sorted order
3. **Has First and Last** - You can identify the lowest and highest elements
4. **Range Operations** - Can retrieve subsets based on ranges
5. **Comparator-Based** - Uses natural order or a custom comparator
6. **Is an Interface** - Not directly instantiated; use `TreeSet` implementation

### Core Methods of SortedSet

| Method | Return Type | Purpose | Example |
|--------|-------------|---------|---------|
| `first()` | `E` | Returns the lowest element | `first()` -> 1 |
| `last()` | `E` | Returns the highest element | `last()` -> 115 |
| `headSet(E toElement)` | `SortedSet<E>` | Returns elements < toElement | `headSet(104)` -> {1, 2, 3} |
| `tailSet(E fromElement)` | `SortedSet<E>` | Returns elements >= fromElement | `tailSet(104)` -> {104, 107, 110, 115} |
| `subSet(E from, E to)` | `SortedSet<E>` | Returns elements from (inclusive) to (exclusive) | `subSet(103, 110)` -> {103, 104, 107} |
| `comparator()` | `Comparator<? super E>` | Returns comparator used, null if natural order | Returns the sorting strategy |

### Difference Between Set and SortedSet

| Aspect | Set | SortedSet |
|--------|-----|-----------|
| **Order** | No guaranteed order | Always sorted |
| **First/Last** | No concept of first or last | Clear first and last elements |
| **Example** | {5, 1, 3} ≈ {3, 1, 5} | {1, 3, 5} always in this order |
| **Methods** | Basic collection methods only | Additional range and sorting methods |
| **Implementation** | HashSet, LinkedHashSet, etc. | TreeSet |
| **Use Case** | Unique elements (any order) | Unique elements (sorted order) |

### Comprehensive SortedSet Example (All Functionality)

```java
import java.util.Arrays;
import java.util.SortedSet;
import java.util.TreeSet;
import java.util.Comparator;
import java.util.Iterator;

public class SortedSetComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== SORTEDSET COMPREHENSIVE DEMO ==========\n");

        // Step 1: Create SortedSet (TreeSet is the implementation)
        System.out.println("Step 1 - Creating SortedSet (using TreeSet):");
        SortedSet<Integer> numbers = new TreeSet<>();
        
        // Add elements in random order - will be sorted automatically
        numbers.add(107);
        numbers.add(100);
        numbers.add(115);
        numbers.add(103);
        numbers.add(104);
        numbers.add(101);
        numbers.add(110);
        
        System.out.println("After adding elements: " + numbers);
        // Output: [100, 101, 103, 104, 107, 110, 115] - automatically sorted!
        System.out.println();

        // Step 2: Try Adding Duplicates - Will be ignored
        System.out.println("Step 2 - Adding Duplicates (rejected):");
        boolean added = numbers.add(104);
        System.out.println("Added duplicate 104? " + added); // false
        System.out.println("Current set: " + numbers);
        System.out.println();

        // Step 3: first() and last() methods
        System.out.println("Step 3 - First and Last Elements:");
        System.out.println("first() - lowest element: " + numbers.first());   // 100
        System.out.println("last() - highest element: " + numbers.last());    // 115
        System.out.println();

        // Step 4: headSet(E toElement) - Elements < parameter
        System.out.println("Step 4 - headSet(104) - All elements < 104:");
        SortedSet<Integer> head = numbers.headSet(104);
        System.out.println("headSet(104): " + head);  // [100, 101, 103]
        System.out.println();

        // Step 5: tailSet(E fromElement) - Elements >= parameter
        System.out.println("Step 5 - tailSet(104) - All elements >= 104:");
        SortedSet<Integer> tail = numbers.tailSet(104);
        System.out.println("tailSet(104): " + tail);  // [104, 107, 110, 115]
        System.out.println();

        // Step 6: subSet(E from, E to) - from (inclusive) to (exclusive)
        System.out.println("Step 6 - subSet(103, 110) - Elements >= 103 and < 110:");
        SortedSet<Integer> subSet = numbers.subSet(103, 110);
        System.out.println("subSet(103, 110): " + subSet);  // [103, 104, 107]
        System.out.println();

        // Step 7: comparator() method
        System.out.println("Step 7 - comparator() method:");
        Comparator<? super Integer> comp = numbers.comparator();
        System.out.println("Comparator used: " + comp);
        // Output: null (because using default/natural order)
        System.out.println("Natural order? " + (comp == null ? "Yes" : "No"));
        System.out.println();

        // Step 8: Check Operations
        System.out.println("Step 8 - Check Operations:");
        System.out.println("Contains 104? " + numbers.contains(104));      // true
        System.out.println("Contains 200? " + numbers.contains(200));      // false
        System.out.println("Size: " + numbers.size());                      // 7
        System.out.println("Is empty? " + numbers.isEmpty());              // false
        System.out.println();

        // Step 9: Remove Operations
        System.out.println("Step 9 - Remove Operations:");
        System.out.println("Before remove: " + numbers);
        numbers.remove(110);
        System.out.println("After remove(110): " + numbers);
        System.out.println();

        // Step 10: Iterator - maintains sorted order
        System.out.println("Step 10 - Iteration (in sorted order):");
        System.out.print("Iterating forward: ");
        for (Integer num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();
        System.out.println();

        // Step 11: String SortedSet with Custom Data
        System.out.println("Step 11 - SortedSet with Strings (alphabetical order):");
        SortedSet<String> languages = new TreeSet<>();
        languages.add("Python");
        languages.add("Java");
        languages.add("Go");
        languages.add("Rust");
        languages.add("C++");
        
        System.out.println("Languages (alphabetically sorted): " + languages);
        System.out.println("First: " + languages.first());    // C++
        System.out.println("Last: " + languages.last());      // Rust
        System.out.println("headSet('Java'): " + languages.headSet("Java"));   // [C++, Go]
        System.out.println("tailSet('Java'): " + languages.tailSet("Java"));   // [Java, Python, Rust]
        System.out.println("subSet('Go', 'Rust'): " + languages.subSet("Go", "Rust")); // [Go, Java, Python]
        System.out.println();

        // Step 12: Custom Comparator (Reverse order)
        System.out.println("Step 12 - Custom Comparator (Descending order):");
        SortedSet<Integer> descending = new TreeSet<>(Comparator.reverseOrder());
        descending.addAll(Arrays.asList(50, 30, 70, 20, 10, 90, 60));
        
        System.out.println("Descending order: " + descending);  // [90, 70, 60, 50, 30, 20, 10]
        System.out.println("first() in descending: " + descending.first());   // 90 (highest)
        System.out.println("last() in descending: " + descending.last());     // 10 (lowest)
        System.out.println();

        // Step 13: View Operations - subsets modify original
        System.out.println("Step 13 - View Operations (Backed Collections):");
        SortedSet<Integer> base = new TreeSet<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
        System.out.println("Original set: " + base);
        
        SortedSet<Integer> view = base.subSet(3, 8);  // [3, 4, 5, 6, 7]
        System.out.println("View subSet(3, 8): " + view);
        
        // Modify view
        view.remove(5);
        System.out.println("After removing 5 from view: " + view);
        System.out.println("Original after view modification: " + base);  // 5 removed from base too!
        System.out.println();

        // Step 14: Summary Table
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ No duplicates - Automatically rejected");
        System.out.println("✓ Sorted order - Elements always in order");
        System.out.println("✓ Has first/last - Clear boundary elements");
        System.out.println("✓ Range queries - headSet, tailSet, subSet");
        System.out.println("✓ Natural or custom order - Default or via Comparator");
        System.out.println("✓ Backed collections - subsets reflect original changes");
        System.out.println("✓ TreeSet implementation - Most common use");
        System.out.println("✓ Comparator support - Standard or custom ordering");
    }
}

/* Output:
========== SORTEDSET COMPREHENSIVE DEMO ==========

Step 1 - Creating SortedSet (using TreeSet):
After adding elements: [100, 101, 103, 104, 107, 110, 115]

Step 2 - Adding Duplicates (rejected):
Added duplicate 104? false
Current set: [100, 101, 103, 104, 107, 110, 115]

Step 3 - First and Last Elements:
first() - lowest element: 100
last() - highest element: 115

Step 4 - headSet(104) - All elements < 104:
headSet(104): [100, 101, 103]

Step 5 - tailSet(104) - All elements >= 104:
tailSet(104): [104, 107, 110, 115]

Step 6 - subSet(103, 110) - Elements >= 103 and < 110:
subSet(103, 110): [103, 104, 107]

Step 7 - comparator() method:
Comparator used: null
Natural order? Yes

Step 8 - Check Operations:
Contains 104? true
Contains 200? false
Size: 7
Is empty? false

Step 9 - Remove Operations:
Before remove: [100, 101, 103, 104, 107, 110, 115]
After remove(110): [100, 101, 103, 104, 107, 115]

Step 10 - Iteration (in sorted order):
Iterating forward: 100 101 103 104 107 115 

Step 11 - SortedSet with Strings (alphabetical order):
Languages (alphabetically sorted): [C++, Go, Java, Python, Rust]
First: C++
Last: Rust
headSet('Java'): [C++, Go]
tailSet('Java'): [Java, Python, Rust]
subSet('Go', 'Rust'): [Go, Java, Python]

Step 12 - Custom Comparator (Descending order):
Descending order: [90, 70, 60, 50, 30, 20, 10]
first() in descending: 90 (highest)
last() in descending: 10 (lowest)

Step 13 - View Operations (Backed Collections):
Original set: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
View subSet(3, 8): [3, 4, 5, 6, 7]
After removing 5 from view: [3, 4, 6, 7]
Original after view modification: [1, 2, 3, 4, 6, 7, 8, 9, 10]

========== SUMMARY ==========
✓ No duplicates - Automatically rejected
✓ Sorted order - Elements always in order
✓ Has first/last - Clear boundary elements
✓ Range queries - headSet, tailSet, subSet
✓ Natural or custom order - Default or via Comparator
✓ Backed collections - subsets reflect original changes
✓ TreeSet implementation - Most common use
✓ Comparator support - Standard or custom ordering
*/
```

### When to Use SortedSet

Use `SortedSet` when you need:

1. **Unique Elements** - No duplicates allowed
2. **Sorted Order** - Elements must be arranged in order
3. **Range Queries** - Need to retrieve subsets by range
4. **Clear Boundaries** - Need first/last element access
5. **Real-World Examples**:
   - Student records sorted by roll number
   - Employee names in alphabetical order
   - Leaderboard with unique players
   - Range-based data retrieval (e.g., scores between 80-90)
   - Maintaining sorted inventory

### Quick Takeaways

1. **SortedSet is about sorting** - Elements are always ordered
2. **Child interface of Set** - Inherits all Set properties
3. **TreeSet is the implementation** - Most common realization
4. **Six additional methods** - first(), last(), headSet(), tailSet(), subSet(), comparator()
5. **Range operations powerful** - headSet, tailSet, subSet for efficient queries
6. **Natural or custom order** - Supports both default and custom comparators
7. **Backed collections** - Subsets reflect changes in original
8. **No duplicates** - Same as all sets
9. **O(log n) operations** - Not as fast as HashSet but sorted guarantee
10. **Perfect for leaderboards** - Sorted unique rankings or scores

---

## TreeSet Class (Detailed)

### Overview

`TreeSet` is the primary implementation of the `SortedSet` interface, introduced in **Java 1.2**.

It uses a **Balanced Binary Search Tree** (Red-Black Tree) internally to maintain elements in sorted order with O(log n) performance for add/remove/contains operations.

### Key Characteristics of TreeSet

1. **Underlying Structure** - Balanced Tree (Red-Black Tree)
2. **No Duplicates** - Like all sets, duplicates are automatically rejected
3. **Insertion Order NOT Preserved** - Unlike LinkedHashSet or ArrayList
4. **Sorted Order** - Elements are always maintained in sorted order
5. **No Heterogeneous Objects** - Cannot mix different data types (e.g., Integer and String together)
   - Throws `ClassCastException` if types conflict
   - **Note**: Only TreeSet and TreeMap have this restriction in entire Collection Framework
6. **Null Handling is Complex** - Special behavior with null values
7. **Comparator Support** - Supports both natural sorting and custom comparators

### Constructors of TreeSet

| Constructor | Purpose |
|---|---|
| `TreeSet()` | Creates empty set with default natural sorting order |
| `TreeSet(Comparator<? super E> comparator)` | Creates empty set with custom comparator |
| `TreeSet(Collection<? extends E> c)` | Creates set from collection, uses natural order |
| `TreeSet(SortedSet<E> s)` | Creates set from another SortedSet |

### Null Handling in TreeSet (Important!)

**Empty TreeSet:**
- Can add `null` as the first element (no comparison needed)
- `set.add(null)` returns `true`

**Non-Empty TreeSet:**
- Adding `null` throws `NullPointerException` (needs to compare null with existing elements)
- Cannot determine where null belongs in sorted order

**After Adding Null:**
- If null is the first element, adding any other element throws `NullPointerException`
- Cannot compare new element with null

### Comprehensive TreeSet Example (All Functionality)

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Iterator;
import java.util.SortedSet;
import java.util.TreeSet;

public class TreeSetComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== TREESET COMPREHENSIVE DEMO ==========\n");

        // Step 1: TreeSet with Default Natural Sorting (Strings)
        System.out.println("Step 1 - TreeSet with Default Natural Sorting (Strings):");
        TreeSet<String> languages = new TreeSet<>();
        languages.add("Python");
        languages.add("A");
        languages.add("Java");
        languages.add("B");
        languages.add("L");
        languages.add("J");
        languages.add("a");  // lowercase 'a' comes after uppercase
        
        System.out.println("Added in order: Python, A, Java, B, L, J, a");
        System.out.println("TreeSet output: " + languages);
        // Output: [A, B, J, L, Python, a] - uppercase before lowercase in ASCII
        System.out.println("Note: Uppercase letters (A=65) < lowercase letters (a=97) in ASCII\n");

        // Step 2: TreeSet with Natural Sorting (Numbers)
        System.out.println("Step 2 - TreeSet with Default Natural Sorting (Numbers):");
        TreeSet<Integer> numbers = new TreeSet<>();
        numbers.add(50);
        numbers.add(30);
        numbers.add(70);
        numbers.add(20);
        numbers.add(60);
        
        System.out.println("Added in order: 50, 30, 70, 20, 60");
        System.out.println("TreeSet output: " + numbers);
        // Output: [20, 30, 50, 60, 70] - automatically sorted
        System.out.println();

        // Step 3: TreeSet with Custom Comparator (Reverse Order)
        System.out.println("Step 3 - TreeSet with Custom Comparator (Descending):");
        TreeSet<Integer> descending = new TreeSet<>(Comparator.reverseOrder());
        descending.addAll(Arrays.asList(50, 30, 70, 20, 60));
        
        System.out.println("Descending TreeSet: " + descending);
        // Output: [70, 60, 50, 30, 20]
        System.out.println();

        // Step 4: Duplicate Rejection
        System.out.println("Step 4 - Duplicate Handling:");
        System.out.println("Before adding duplicate: " + numbers);
        boolean added = numbers.add(50);  // 50 already exists
        System.out.println("Added duplicate 50? " + added);  // false
        System.out.println("After attempt to add 50: " + numbers);
        System.out.println();

        // Step 5: SortedSet Methods (first, last, etc.)
        System.out.println("Step 5 - SortedSet Methods:");
        System.out.println("first(): " + numbers.first());               // 20
        System.out.println("last(): " + numbers.last());                 // 70
        System.out.println("headSet(50): " + numbers.headSet(50));       // [20, 30]
        System.out.println("tailSet(50): " + numbers.tailSet(50));       // [50, 60, 70]
        System.out.println("subSet(30, 60): " + numbers.subSet(30, 60)); // [30, 50]
        System.out.println();

        // Step 6: TreeSet from Collection (with natural order)
        System.out.println("Step 6 - Creating TreeSet from Collection:");
        TreeSet<String> fromCollection = new TreeSet<>(
            Arrays.asList("Zebra", "Apple", "Banana", "Apple", "Mango")
        );
        System.out.println("Created from: [Zebra, Apple, Banana, Apple, Mango]");
        System.out.println("TreeSet output: " + fromCollection);
        // Output: [Apple, Banana, Mango, Zebra] - sorted, duplicates removed
        System.out.println();

        // Step 7: TreeSet from SortedSet
        System.out.println("Step 7 - Creating TreeSet from SortedSet:");
        SortedSet<Integer> sortedNumbers = new TreeSet<>(Arrays.asList(5, 1, 9, 3, 7));
        TreeSet<Integer> treeFromSorted = new TreeSet<>(sortedNumbers);
        System.out.println("Source SortedSet: " + sortedNumbers);
        System.out.println("TreeSet created: " + treeFromSorted);
        System.out.println();

        // Step 8: homogeneous Objects vs Heterogeneous (ClassCastException)
        System.out.println("Step 8 - Heterogeneous Objects (Type Safety):");
        TreeSet<Integer> homogeneous = new TreeSet<>();
        homogeneous.add(10);
        homogeneous.add(20);
        homogeneous.add(30);
        System.out.println("Valid TreeSet (all integers): " + homogeneous);
        
        // Attempting to add different type will fail at runtime
        try {
            @SuppressWarnings("unchecked")
            TreeSet mixed = (TreeSet) homogeneous;
            mixed.add("String");  // Will cause ClassCastException during comparison
            System.out.println("Mixed types: " + mixed);
        } catch (ClassCastException e) {
            System.out.println("ClassCastException: Cannot add String to Integer TreeSet");
        }
        System.out.println();

        // Step 9: Null Handling - Empty TreeSet
        System.out.println("Step 9 - Null in Empty TreeSet:");
        TreeSet<String> emptyTree = new TreeSet<>();
        boolean nullAdded = emptyTree.add(null);
        System.out.println("Added null to empty TreeSet? " + nullAdded);  // true
        System.out.println("TreeSet with null: " + emptyTree);
        System.out.println();

        // Step 10: Null Handling - Try adding to non-empty TreeSet
        System.out.println("Step 10 - Null in Non-Empty TreeSet (NullPointerException):");
        TreeSet<String> notEmptyTree = new TreeSet<>(Arrays.asList("A", "B", "C"));
        System.out.println("TreeSet before null attempt: " + notEmptyTree);
        try {
            notEmptyTree.add(null);
            System.out.println("Added null: " + notEmptyTree);
        } catch (NullPointerException e) {
            System.out.println("NullPointerException: Cannot add null to non-empty TreeSet");
            System.out.println("Reason: Cannot compare null with existing elements");
        }
        System.out.println();

        // Step 11: Null as First Element - Try adding other elements
        System.out.println("Step 11 - Adding Elements After Null (NullPointerException):");
        TreeSet<String> nullFirst = new TreeSet<>();
        nullFirst.add(null);
        System.out.println("TreeSet with null as first: " + nullFirst);
        try {
            nullFirst.add("A");
            System.out.println("Added 'A': " + nullFirst);
        } catch (NullPointerException e) {
            System.out.println("NullPointerException: Cannot add 'A' after null");
            System.out.println("Reason: Cannot compare 'A' with null");
        }
        System.out.println();

        // Step 12: Basic Operations
        System.out.println("Step 12 - Basic Operations:");
        TreeSet<Integer> ops = new TreeSet<>(Arrays.asList(10, 40, 20, 50, 30));
        System.out.println("Original: " + ops);
        
        System.out.println("Contains 30? " + ops.contains(30));           // true
        System.out.println("Contains 100? " + ops.contains(100));         // false
        System.out.println("Size: " + ops.size());                        // 5
        
        ops.remove(20);
        System.out.println("After remove(20): " + ops);
        
        ops.clear();
        System.out.println("After clear(): " + ops + " isEmpty? " + ops.isEmpty());
        System.out.println();

        // Step 13: Iteration in Sorted Order
        System.out.println("Step 13 - Iteration (Always in Sorted Order):");
        TreeSet<Integer> iter = new TreeSet<>(Arrays.asList(100, 20, 50, 10, 80));
        System.out.println("Original insertion: 100, 20, 50, 10, 80");
        System.out.println("TreeSet stores as: " + iter);
        System.out.print("Iterating: ");
        for (Integer num : iter) {
            System.out.print(num + " ");
        }
        System.out.println();
        System.out.println();

        // Step 14: Performance Characteristics
        System.out.println("Step 14 - Performance Characteristics:");
        System.out.println("Underlying structure: Balanced Binary Search Tree (Red-Black Tree)");
        System.out.println("add(E e): O(log n)");
        System.out.println("remove(Object o): O(log n)");
        System.out.println("contains(Object o): O(log n)");
        System.out.println("vs HashSet which is O(1), TreeSet is slower but guarantees order");
        System.out.println();

        // Step 15: Comparator Details
        System.out.println("Step 15 - Comparator Method:");
        TreeSet<Integer> natural = new TreeSet<>();
        TreeSet<Integer> custom = new TreeSet<>(Comparator.reverseOrder());
        
        System.out.println("Natural order comparator: " + natural.comparator());  // null
        System.out.println("Custom reverse comparator: " + custom.comparator());  // comparator instance
        System.out.println();

        // Step 16: Summary Table
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ Underlying structure: Balanced Tree (Red-Black Tree)");
        System.out.println("✓ No duplicates allowed");
        System.out.println("✓ Insertion order NOT preserved");
        System.out.println("✓ Sorted order ALWAYS maintained");
        System.out.println("✓ Homogeneous only (no mixed types - ClassCastException)");
        System.out.println("✓ Null handling complex (empty OK, non-empty throws NPE)");
        System.out.println("✓ Performance: O(log n) for add/remove/contains");
        System.out.println("✓ Use when: Sorting + uniqueness + range queries needed");
        System.out.println("✓ Implements SortedSet: first(), last(), headSet(), tailSet(), subSet()");
    }
}

/* Output highlights:
========== TREESET COMPREHENSIVE DEMO ==========

Step 1 - TreeSet with Default Natural Sorting (Strings):
Added in order: Python, A, Java, B, L, J, a
TreeSet output: [A, B, J, L, Python, a]
Note: Uppercase letters (A=65) < lowercase letters (a=97) in ASCII

Step 2 - TreeSet with Default Natural Sorting (Numbers):
TreeSet output: [20, 30, 50, 60, 70]

Step 3 - TreeSet with Custom Comparator (Descending):
Descending TreeSet: [70, 60, 50, 30, 20]

Step 4 - Duplicate Handling:
Added duplicate 50? false

Step 8 - Heterogeneous Objects (Type Safety):
ClassCastException: Cannot add String to Integer TreeSet

Step 9 - Null in Empty TreeSet:
Added null to empty TreeSet? true

Step 10 - Null in Non-Empty TreeSet (NullPointerException):
NullPointerException: Cannot add null to non-empty TreeSet

Step 11 - Adding Elements After Null (NullPointerException):
NullPointerException: Cannot add 'A' after null

[...all other outputs follow...]

========== SUMMARY ==========
✓ Underlying structure: Balanced Tree (Red-Black Tree)
✓ No duplicates allowed
✓ Insertion order NOT preserved
✓ Sorted order ALWAYS maintained
✓ Homogeneous only (no mixed types - ClassCastException)
✓ Null handling complex (empty OK, non-empty throws NPE)
✓ Performance: O(log n) for add/remove/contains
✓ Use when: Sorting + uniqueness + range queries needed
✓ Implements SortedSet: first(), last(), headSet(), tailSet(), subSet()
*/
```

### Key Differences: HashSet vs TreeSet vs LinkedHashSet

| Feature | HashSet | TreeSet | LinkedHashSet |
|---------|---------|---------|---------------|
| **Underlying** | Hash Table | Balanced Tree | Hash Table + Linked List |
| **Order** | Random | Sorted | Insertion Order |
| **Duplicates** | No | No | No |
| **Null Support** | One null | Complex (see above) | One null |
| **Homogeneous** | Any types | Only one type | Any types |
| **Performance** | O(1) | O(log n) | O(1) |
| **Use Case** | Unique, fast | Unique, sorted | Unique, ordered |
| **Memory** | Less | Balanced tree nodes | Extra linked pointers |

### When to Use TreeSet

Use `TreeSet` when you need:

1. **Unique Elements** - No duplicates allowed
2. **Sorted Order** - Elements must be in sorted order
3. **Range Operations** - Need headSet, tailSet, subSet
4. **First/Last Access** - Frequent first() and last() queries
5. **Type Safety** - Only homogeneous elements
6. **Real-World Examples**:
   - Leaderboard with sorted scores
   - Sorted inventory with unique items
   - Range-based queries (e.g., salaries between 50k-100k)
   - ASCII/Unicode sorted strings
   - Priority-based unique tasks

### Quick Takeaways

1. **TreeSet = Sorted Set with Red-Black Tree**
2. **No duplicates** - Automatically rejected
3. **No insertion order** - Replaced with sorted order
4. **Red-Black Tree internally** - Balanced for O(log n) operations
5. **Only homogeneous objects** - Cannot mix types (ClassCastException)
6. **Null handling tricky** - Empty OK, non-empty throws NPE
7. **Four constructors** - Default, Custom Comparator, Collection, SortedSet
8. **SortedSet methods** - first(), last(), headSet(), tailSet(), subSet()
9. **Slower than HashSet** - O(log n) vs O(1), but maintains order
10. **Perfect for sorted unique data** - When sorting is essential with uniqueness

---

## Comparable Interface (Detailed)

### Overview

`Comparable` is an interface in the `java.lang` package used to define the **Default Natural Sorting Order (DNSO)** for objects.

It contains only **one method**: `compareTo(Object obj)`

### Key Characteristic

When you use **TreeSet with the default constructor**, the objects must satisfy **two mandatory conditions**:

1. **Homogeneous** - All objects must be of the same type
2. **Comparable** - The class must implement `Comparable` interface

If either condition is not met, a **ClassCastException** is thrown at runtime.

### The compareTo() Method

```java
public int compareTo(Object obj)
```

**Returns:**
- **Negative value** (typically -1): if this object comes before the parameter object
- **Positive value** (typically +1): if this object comes after the parameter object
- **Zero (0)**: if both objects are equal

### Example with String (Implements Comparable)

```java
"A".compareTo("Z")  // Returns negative (A comes before Z)
"Z".compareTo("B")  // Returns positive (Z comes after B)
"A".compareTo("A")  // Returns 0 (equal)
"A".compareTo(null) // Throws NullPointerException
```

### Why StringBuffer Fails in TreeSet

StringBuffer **does NOT implement Comparable interface**. While it's homogeneous (all StringBuffer type), it cannot be stored in default TreeSet:

```java
TreeSet<StringBuffer> set = new TreeSet<>();
set.add(new StringBuffer("A"));
set.add(new StringBuffer("B"));
// Throws: ClassCastException: StringBuffer cannot be cast to Comparable
```

This happens because TreeSet internally tries to call `compareTo()` which StringBuffer doesn't have.

### Comparable vs Initially Using Default Constructor TreeSet

| Type | Needs Comparable | Example |
|------|-----------------|---------|
| String | ✓ Yes (has it) | Works fine, alphabetical order |
| Integer | ✓ Yes (has it) | Works fine, ascending order |
| StringBuffer | ✗ No | Fails with ClassCastException |
| Custom Class | Depends | Need to implement if using TreeSet() |

---

## Comparator Interface (Detailed)

### Overview

`Comparator` is an interface in the `java.util` package used to define **Customized Sorting Order**.

While Comparable is about DNSO, Comparator is about overriding or defining custom sorting.

### Methods in Comparator

| Method | Purpose |
|--------|---------|
| `compare(Object obj1, Object obj2)` | **Mandatory** - Defines custom sorting logic |
| `equals(Object obj)` | **Optional** - Inherited from Object, rarely overridden |

### The compare() Method

```java
public int compare(Object obj1, Object obj2)
```

**Returns:**
- **Negative**: obj1 should come before obj2
- **Positive**: obj1 should come after obj2
- **Zero**: obj1 and obj2 are equal

### Key Advantages over Comparable

1. **Non-Comparable Objects** - Can store StringBuffer and other non-comparable objects
2. **Heterogeneous Objects** - Can store mixed types (String and StringBuffer together) if logic handles it
3. **Custom Sorting** - Can define multiple different sorting orders
4. **Doesn't Modify Class** - No need to change the original class

### Comprehensive Comparator Example (All Functionality)

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.TreeSet;

public class ComparatorComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== COMPARATOR COMPREHENSIVE DEMO ==========\n");

        // Step 1: Default Natural Sorting (Comparable)
        System.out.println("Step 1 - TreeSet with Default Natural Sorting (String):");
        TreeSet<String> natural = new TreeSet<>();
        natural.addAll(Arrays.asList("Ganga", "Roza", "Shobharani", "Rajakumari"));
        System.out.println("Alphabetical (Natural): " + natural);
        // Output: [Ganga, Rajakumari, Roza, Shobharani]
        System.out.println();

        // Step 2: Custom Comparator - Reverse Alphabetical (Method 1: Negate)
        System.out.println("Step 2 - Reverse Alphabetical using Comparator (Negate):");
        class ReverseComparator1 implements Comparator<String> {
            @Override
            public int compare(String s1, String s2) {
                return -s1.compareTo(s2);  // Negate the result
            }
        }
        TreeSet<String> reverse1 = new TreeSet<>(new ReverseComparator1());
        reverse1.addAll(Arrays.asList("Ganga", "Roza", "Shobharani", "Rajakumari"));
        System.out.println("Reverse (Negate method): " + reverse1);
        // Output: [Shobharani, Roza, Rajakumari, Ganga]
        System.out.println();

        // Step 3: Custom Comparator - Reverse Alphabetical (Method 2: Swap)
        System.out.println("Step 3 - Reverse Alphabetical using Comparator (Swap):");
        class ReverseComparator2 implements Comparator<String> {
            @Override
            public int compare(String s1, String s2) {
                return s2.compareTo(s1);  // Compare s2 against s1
            }
        }
        TreeSet<String> reverse2 = new TreeSet<>(new ReverseComparator2());
        reverse2.addAll(Arrays.asList("Ganga", "Roza", "Shobharani", "Rajakumari"));
        System.out.println("Reverse (Swap method): " + reverse2);
        // Output: [Shobharani, Roza, Rajakumari, Ganga]
        System.out.println();

        // Step 4: Descending Order for Integers
        System.out.println("Step 4 - TreeSet<Integer> with Descending Comparator:");
        class DescendingIntComparator implements Comparator<Integer> {
            @Override
            public int compare(Integer i1, Integer i2) {
                if (i1 < i2) return +1;      // Smaller goes after
                else if (i1 > i2) return -1; // Larger goes before
                else return 0;
            }
        }
        TreeSet<Integer> descInt = new TreeSet<>(new DescendingIntComparator());
        descInt.addAll(Arrays.asList(20, 15, 10, 5, 0, 25));
        System.out.println("Descending integers: " + descInt);
        // Output: [25, 20, 15, 10, 5, 0]
        System.out.println();

        // Step 5: StringBuffer (Non-Comparable) with Comparator
        System.out.println("Step 5 - TreeSet<StringBuffer> using Comparator:");
        class StringBufferComparator implements Comparator<StringBuffer> {
            @Override
            public int compare(StringBuffer sb1, StringBuffer sb2) {
                return sb1.toString().compareTo(sb2.toString());
            }
        }
        TreeSet<StringBuffer> sbSet = new TreeSet<>(new StringBufferComparator());
        sbSet.add(new StringBuffer("Charlie"));
        sbSet.add(new StringBuffer("Alice"));
        sbSet.add(new StringBuffer("Bob"));
        System.out.println("StringBuffer (alphabetical): " + sbSet);
        // Output: [Alice, Bob, Charlie]
        System.out.println();

        // Step 6: Mixed Types (String & StringBuffer) with Comparator
        System.out.println("Step 6 - Mixed Types (String & StringBuffer) with Comparator:");
        class MixedTypeComparator implements Comparator<Object> {
            @Override
            public int compare(Object obj1, Object obj2) {
                String s1 = obj1.toString();
                String s2 = obj2.toString();
                return s1.compareTo(s2);
            }
        }
        @SuppressWarnings("unchecked")
        TreeSet mixed = new TreeSet<>(new MixedTypeComparator());
        mixed.add("Zebra");
        mixed.add(new StringBuffer("Apple"));
        mixed.add("Mango");
        mixed.add(new StringBuffer("Banana"));
        System.out.println("Mixed (String + StringBuffer): " + mixed);
        // Output: [Apple, Banana, Mango, Zebra]
        System.out.println();

        // Step 7: Multi-Rule Sorting (Length, then Alphabetical)
        System.out.println("Step 7 - Multi-Rule Sorting (Length first, then Alphabetical):");
        class LengthThenAlphabetComparator implements Comparator<Object> {
            @Override
            public int compare(Object obj1, Object obj2) {
                String s1 = obj1.toString();
                String s2 = obj2.toString();
                
                // Primary rule: Sort by length
                if (s1.length() < s2.length()) return -1;
                else if (s1.length() > s2.length()) return +1;
                
                // Secondary rule: If lengths equal, sort alphabetically
                else return s1.compareTo(s2);
            }
        }
        @SuppressWarnings("unchecked")
        TreeSet multiRule = new TreeSet<>(new LengthThenAlphabetComparator());
        multiRule.add("A");
        multiRule.add(new StringBuffer("ABC"));
        multiRule.add(new StringBuffer("AA"));
        multiRule.add("ABCD");
        multiRule.add("XY");
        System.out.println("Multi-rule (length then alphabetical): " + multiRule);
        // Output: [A, AA, XY, ABC, ABCD]
        System.out.println();

        // Step 8: Various Comparator Tricks
        System.out.println("Step 8 - Comparator Tricks (Different Return Values):");
        
        // Trick 1: Return +1 always (allows duplicates, insertion order)
        System.out.println("  a) Return +1 always (insertion order, duplicates allowed):");
        class AlwaysPositiveComparator implements Comparator<Integer> {
            @Override
            public int compare(Integer i1, Integer i2) {
                return +1;  // Always return positive
            }
        }
        TreeSet<Integer> trick1 = new TreeSet<>(new AlwaysPositiveComparator());
        trick1.addAll(Arrays.asList(20, 15, 10, 15, 20, 5));
        System.out.println("     Result: " + trick1 + " Size: " + trick1.size());
        // Duplicates not removed!
        
        // Trick 2: Return -1 always (reverse insertion order, duplicates allowed)
        System.out.println("  b) Return -1 always (reverse insertion order):");
        class AlwaysNegativeComparator implements Comparator<Integer> {
            @Override
            public int compare(Integer i1, Integer i2) {
                return -1;  // Always return negative
            }
        }
        TreeSet<Integer> trick2 = new TreeSet<>(new AlwaysNegativeComparator());
        trick2.addAll(Arrays.asList(5, 10, 15, 20));
        System.out.println("     Result: " + trick2);
        // Reverse of [5, 10, 15, 20]
        
        // Trick 3: Return 0 always (only first element allowed)
        System.out.println("  c) Return 0 always (only first element allowed):");
        class AlwaysZeroComparator implements Comparator<Integer> {
            @Override
            public int compare(Integer i1, Integer i2) {
                return 0;  // Always return zero (equal)
            }
        }
        TreeSet<Integer> trick3 = new TreeSet<>(new AlwaysZeroComparator());
        trick3.addAll(Arrays.asList(5, 10, 15, 20, 25));
        System.out.println("     Result: " + trick3 + " Size: " + trick3.size());
        // Only first element (5)
        System.out.println();

        // Step 9: Case Insensitive String Comparator
        System.out.println("Step 9 - Case Insensitive String Comparator:");
        class CaseInsensitiveComparator implements Comparator<String> {
            @Override
            public int compare(String s1, String s2) {
                return s1.compareToIgnoreCase(s2);
            }
        }
        TreeSet<String> caseInsensitive = new TreeSet<>(new CaseInsensitiveComparator());
        caseInsensitive.addAll(Arrays.asList("java", "PYTHON", "Go", "rust", "C++"));
        System.out.println("Case insensitive sorted: " + caseInsensitive);
        // Output: [C++, Go, java, PYTHON, rust]
        System.out.println();

        // Step 10: Comparator Methods Summary
        System.out.println("========== COMPARATOR SUMMARY ==========");
        System.out.println("✓ Enables custom sorting order");
        System.out.println("✓ Works with non-Comparable classes (StringBuffer)");
        System.out.println("✓ Allows heterogeneous object storage");
        System.out.println("✓ Supports multi-rule sorting");
        System.out.println("✓ Return values control placement:");
        System.out.println("  - Negative: obj1 before obj2");
        System.out.println("  - Positive: obj1 after obj2");
        System.out.println("  - Zero: considered equal");
        System.out.println("✓ Always implement compare() method only");
        System.out.println("✓ Perfect for when Comparable is insufficient");
    }
}

/* Output highlights:
========== COMPARATOR COMPREHENSIVE DEMO ==========

Step 1 - TreeSet with Default Natural Sorting (String):
Alphabetical (Natural): [Ganga, Rajakumari, Roza, Shobharani]

Step 2 - Reverse Alphabetical using Comparator (Negate):
Reverse (Negate method): [Shobharani, Roza, Rajakumari, Ganga]

Step 3 - Reverse Alphabetical using Comparator (Swap):
Reverse (Swap method): [Shobharani, Roza, Rajakumari, Ganga]

Step 4 - TreeSet<Integer> with Descending Comparator:
Descending integers: [25, 20, 15, 10, 5, 0]

Step 5 - TreeSet<StringBuffer> using Comparator:
StringBuffer (alphabetical): [Alice, Bob, Charlie]

Step 6 - Mixed Types (String & StringBuffer) with Comparator:
Mixed (String + StringBuffer): [Apple, Banana, Mango, Zebra]

Step 7 - Multi-Rule Sorting (Length first, then Alphabetical):
Multi-rule (length then alphabetical): [A, AA, XY, ABC, ABCD]

Step 8 - Comparator Tricks (Different Return Values):
  a) Return +1 always (insertion order, duplicates allowed):
     Result: [20, 15, 10, 15, 20, 5] Size: 6
  b) Return -1 always (reverse insertion order):
     Result: [20, 15, 10, 5]
  c) Return 0 always (only first element allowed):
     Result: [5] Size: 1

Step 9 - Case Insensitive String Comparator:
Case insensitive sorted: [C++, Go, java, PYTHON, rust]

========== COMPARATOR SUMMARY ==========
[...summary follows...]
*/
```

### Comparable vs Comparator Decision Table

| Scenario | When to Use | Example |
|----------|-------------|---------|
| **Predefined Class (String, Integer)** | Want default order | Use TreeSet() directly |
| **Predefined Class** | Want custom order | Use TreeSet(new MyComparator()) |
| **Non-Comparable Class (StringBuffer)** | Need sorting | Must use Comparator |
| **Mixed/Heterogeneous Types** | Need to store together | Use Comparator with toString() |
| **Custom Class** | Define default order | Implement Comparable |
| **Custom Class** | Define alternative order | Create custom Comparator |

### Quick Takeaways

1. **Comparable = DEFAULT Natural Sorting Order** - Defined by the class itself
2. **Comparator = CUSTOM Sorting Order** - Define externally as needed
3. **Two mandatory conditions for TreeSet()**: Homogeneous + Comparable
4. **Comparator solves problems**: Non-comparable objects, custom sorting, heterogeneous storage
5. **StringBuffer works with Comparator** - Convert to String using toString()
6. **compareTo() vs compare()**: Single method vs flexible custom logic
7. **Negate or Swap**: Two ways to reverse sorting order with Comparator
8. **Multi-rule sorting**: Primary and secondary rules in one Comparator
9. **Return tricks**: +1, -1, 0 control exact behavior of TreeSet
10. **Class Writer & User role**: Writer implements Comparable, User creates Comparator as needed

---

## Custom Class with Comparable and Comparator (Employee Example)

### Scenario

When creating a **custom class** like `Employee`, you need to decide the **default sorting order**.

Since Employee IDs are unique, ID-based sorting is the most logical "natural" order.

However, users might want alternative sorting (e.g., by name or salary).

### Solution Strategy

1. **Class Writer's Responsibility** - Implement `Comparable` for natural order (by ID)
2. **Class User's Responsibility** - Create custom `Comparator` for alternative sorting (by name, salary, etc.)

### Comprehensive Employee Class Example (All Functionality)

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.TreeSet;

// Step 1: Define Employee class implementing Comparable (for ID-based sorting)
class Employee implements Comparable<Employee> {
    String name;
    int eid;  // Employee ID
    
    public Employee(String name, int eid) {
        this.name = name;
        this.eid = eid;
    }
    
    @Override
    public int compareTo(Employee other) {
        // Default Natural Sorting Order: By Employee ID (ascending)
        if (this.eid < other.eid) return -1;
        else if (this.eid > other.eid) return +1;
        else return 0;
    }
    
    @Override
    public String toString() {
        return name + "-" + eid;
    }
}

// Step 2: Custom Comparator for Name-based sorting (alphabetical)
class NameComparator implements Comparator<Employee> {
    @Override
    public int compare(Employee emp1, Employee emp2) {
        // Custom Sorting Order: By Employee Name (alphabetical)
        return emp1.name.compareTo(emp2.name);
    }
}

// Step 3: Custom Comparator for Reverse ID sorting (descending)
class ReverseIdComparator implements Comparator<Employee> {
    @Override
    public int compare(Employee emp1, Employee emp2) {
        if (emp1.eid < emp2.eid) return +1;  // Reverse: smaller goes after
        else if (emp1.eid > emp2.eid) return -1; // Reverse: larger goes before
        else return 0;
    }
}

public class EmployeeComparableComparatorDemo {
    public static void main(String[] args) {
        System.out.println("========== EMPLOYEE COMPARABLE & COMPARATOR DEMO ==========\n");

        // Create sample employees
        Employee[] empArray = {
            new Employee("Venky", 150),
            new Employee("Nag", 100),
            new Employee("Chiru", 50),
            new Employee("Balayya", 200),
            new Employee("Ali", 75)
        };

        // Step 1: Default Natural Sorting (using Comparable - by ID ascending)
        System.out.println("Step 1 - Default Natural Sorting (Comparable - by ID ascending):");
        TreeSet<Employee> byId = new TreeSet<>(Arrays.asList(empArray));
        System.out.println("Creation order: Venky-150, Nag-100, Chiru-50, Balayya-200, Ali-75");
        System.out.println("TreeSet (by ID): " + byId);
        // Output: [Chiru-50, Ali-75, Nag-100, Venky-150, Balayya-200]
        System.out.println("✓ Sorted by Employee ID (Default Natural Order)\n");

        // Step 2: Custom Sorting - By Name (using Comparator)
        System.out.println("Step 2 - Custom Sorting (Comparator - by Name alphabetical):");
        TreeSet<Employee> byName = new TreeSet<>(new NameComparator());
        byName.addAll(Arrays.asList(empArray));
        System.out.println("TreeSet (by Name): " + byName);
        // Output: [Ali-75, Balayya-200, Chiru-50, Nag-100, Venky-150]
        System.out.println("✓ Sorted alphabetically by Employee Name (Custom Order)\n");

        // Step 3: Custom Sorting - By ID Reverse (descending)
        System.out.println("Step 3 - Custom Sorting (Comparator - by ID descending):");
        TreeSet<Employee> byIdReverse = new TreeSet<>(new ReverseIdComparator());
        byIdReverse.addAll(Arrays.asList(empArray));
        System.out.println("TreeSet (by ID reverse): " + byIdReverse);
        // Output: [Balayya-200, Venky-150, Nag-100, Ali-75, Chiru-50]
        System.out.println("✓ Sorted by Employee ID in descending order (Custom Order)\n");

        // Step 4: SortedSet methods work on all sorted sets
        System.out.println("Step 4 - SortedSet Methods (working on all variants):");
        System.out.println("By ID - first(): " + byId.first() + ", last(): " + byId.last());
        System.out.println("By Name - first(): " + byName.first() + ", last(): " + byName.last());
        System.out.println("By ID Reverse - first(): " + byIdReverse.first() + ", last(): " + byIdReverse.last());
        System.out.println();

        // Step 5: Duplicate Handling (same ID = duplicate)
        System.out.println("Step 5 - Duplicate Handling:");
        TreeSet<Employee> dupTest = new TreeSet<>();
        dupTest.add(new Employee("Original-Chiru", 50));
        System.out.println("Added first Chiru-50: " + dupTest);
        
        boolean added = dupTest.add(new Employee("Duplicate-Chiru", 50));
        System.out.println("Try adding another with ID 50? " + added); // false
        System.out.println("After duplicate attempt: " + dupTest);
        System.out.println("✓ Duplicate IDs rejected (based on compareTo)\n");

        // Step 6: Iteration maintains sort order
        System.out.println("Step 6 - Iteration Order (always respects sorting):");
        System.out.print("By ID forward: ");
        for (Employee emp : byId) {
            System.out.print(emp + " ");
        }
        System.out.println();
        System.out.print("By Name forward: ");
        for (Employee emp : byName) {
            System.out.print(emp + " ");
        }
        System.out.println();
        System.out.println();

        // Step 7: Contains and Remove operations
        System.out.println("Step 7 - Contains and Remove Operations:");
        Employee testEmp = new Employee("Test", 100);
        System.out.println("Contains (Nag-100)? " + byId.contains(new Employee("AnyName", 100))); // true (only eid matters)
        
        byId.remove(new Employee("RemoveMe", 100));  // Removes based on Comparable (ID)
        System.out.println("After removing ID 100: " + byId);
        System.out.println();

        // Step 8: Performance Characteristics Summary
        System.out.println("Step 8 - Performance Characteristics:");
        System.out.println("Underlying: Balanced Binary Search Tree");
        System.out.println("add(Employee e): O(log n) - must call compareTo");
        System.out.println("contains(Employee e): O(log n) - must call compareTo");
        System.out.println("remove(Employee e): O(log n) - must call compareTo");
        System.out.println();

        // Step 9: Comparable vs Comparator Summary for Employee
        System.out.println("========== COMPARABLE VS COMPARATOR (Employee Context) ==========");
        System.out.println("Comparable (Default Natural Order - by ID):");
        System.out.println("  - Implemented by Employee class writer");
        System.out.println("  - Reflects the 'most important' sorting criteria");
        System.out.println("  - Used: TreeSet<Employee> set = new TreeSet<>();");
        System.out.println("  - Result: Sorted by ID\n");
        
        System.out.println("Comparator (Custom Order - by Name):");
        System.out.println("  - Created by Employee class user/client");
        System.out.println("  - Defines alternative sorting when needed");
        System.out.println("  - Used: TreeSet<Employee> set = new TreeSet<>(new NameComparator());");
        System.out.println("  - Result: Sorted by Name\n");

        // Step 10: Decision Making
        System.out.println("========== DECISION MAKING FOR CUSTOM CLASSES ==========");
        System.out.println("Q: Should my custom class implement Comparable?");
        System.out.println("A: Yes, if there is ONE most common/natural sorting order.");
        System.out.println("   For Employee, ID is unique and natural → implement Comparable\n");
        
        System.out.println("Q: Should I create a Comparator?");
        System.out.println("A: Yes, for EACH alternative sorting order users might need.");
        System.out.println("   Alternative 1: NameComparator (alphabetical by name)");
        System.out.println("   Alternative 2: ReverseIdComparator (descending by ID)");
        System.out.println("   Users choose which Comparator when creating TreeSet\n");

        // Step 11: Complete Summary Table
        System.out.println("========== FEATURE COMPARISON ==========");
        System.out.println("Feature              | Comparable (Default)    | Comparator (Custom)");
        System.out.println("-".repeat(75));
        System.out.println("Purpose              | Default Natural Order   | Custom Sorting Order");
        System.out.println("Location             | Inside Employee class   | Separate class");
        System.out.println("Method               | compareTo()             | compare()");
        System.out.println("Parameters           | 1 (compares with this)  | 2 (compares two objects)");
        System.out.println("Interface            | java.lang.Comparable    | java.util.Comparator");
        System.out.println("Implemented By       | Employee class          | NameComparator class");
        System.out.println("TreeSet Constructor  | TreeSet<E>()            | TreeSet<E>(comparator)");
        System.out.println("Use Case (Employee)  | Sort by ID              | Sort by Name/Salary/etc");
        System.out.println();

        System.out.println("========== KEY TAKEAWAYS ==========");
        System.out.println("✓ Custom class writer defines Comparable for default order");
        System.out.println("✓ Custom class user creates Comparator for alternatives");
        System.out.println("✓ Both can coexist for maximum flexibility");
        System.out.println("✓ Comparable = 'this' vs 'that' | Comparator = 'first' vs 'second'");
        System.out.println("✓ TreeSet uses compareTo() by default, compare() if Comparator provided");
        System.out.println("✓ Duplicates determined by compareTo()/compare() result (0 = duplicate)");
        System.out.println("✓ Interviews: Comparable = writer's choice, Comparator = user's choice");
    }
}

/* Output:
========== EMPLOYEE COMPARABLE & COMPARATOR DEMO ==========

Step 1 - Default Natural Sorting (Comparable - by ID ascending):
Creation order: Venky-150, Nag-100, Chiru-50, Balayya-200, Ali-75
TreeSet (by ID): [Chiru-50, Ali-75, Nag-100, Venky-150, Balayya-200]
✓ Sorted by Employee ID (Default Natural Order)

Step 2 - Custom Sorting (Comparator - by Name alphabetical):
TreeSet (by Name): [Ali-75, Balayya-200, Chiru-50, Nag-100, Venky-150]
✓ Sorted alphabetically by Employee Name (Custom Order)

Step 3 - Custom Sorting (Comparator - by ID descending):
TreeSet (by ID reverse): [Balayya-200, Venky-150, Nag-100, Ali-75, Chiru-50]
✓ Sorted by Employee ID in descending order (Custom Order)

Step 4 - SortedSet Methods (working on all variants):
By ID - first(): Chiru-50, last(): Balayya-200
By Name - first(): Ali-75, last(): Venky-150
By ID Reverse - first(): Balayya-200, last(): Chiru-50

Step 5 - Duplicate Handling:
Added first Chiru-50: [Chiru-50]
Try adding another with ID 50? false
After duplicate attempt: [Chiru-50]
✓ Duplicate IDs rejected (based on compareTo)

[...continues with all steps...]

========== KEY TAKEAWAYS ==========
✓ Custom class writer defines Comparable for default order
✓ Custom class user creates Comparator for alternatives
✓ Both can coexist for maximum flexibility
✓ Comparable = 'this' vs 'that' | Comparator = 'first' vs 'second'
✓ TreeSet uses compareTo() by default, compare() if Comparator provided
✓ Duplicates determined by compareTo()/compare() result (0 = duplicate)
✓ Interviews: Comparable = writer's choice, Comparator = user's choice
*/
```

### Interview Question Answer

| Aspect | Answer |
|--------|--------|
| **Who implements Comparable?** | The class writer (defines default/natural order) |
| **Who creates Comparator?** | The class user/client (when they need custom order) |
| **For Employee class** | Writer implements Comparable (sort by ID), User creates NameComparator (sort by name) |
| **Benefit** | Maximum flexibility for both standard and custom sorting needs |

---

## Set Implementation Classes Comparison

### Comprehensive Comparison Table

| Property | HashSet | LinkedHashSet | TreeSet |
|----------|---------|---------------|---------|
| **Underlying Data Structure** | Hash Table | Hash Table + Linked List | Balanced Binary Search Tree |
| **Insertion Order Preserved** | ✗ No | ✓ Yes | N/A (Sorted instead) |
| **Sorted Order Maintained** | ✗ No | ✗ No | ✓ Yes |
| **Heterogeneous Objects** | ✓ Allowed | ✓ Allowed | ✗ No (unless Comparator provided) |
| **Duplicate Objects** | ✗ Not allowed | ✗ Not allowed | ✗ Not allowed |
| **Null Acceptance** | ✓ One null | ✓ One null | ⚠ Conditional (first element only) |
| **Performance (add/remove/contains)** | O(1) average | O(1) average | O(log n) |
| **Best Use Case** | Fast unique collection | Unique + ordered insertion | Unique + sorted collection |
| **Memory Overhead** | Low | Medium (linked list) | Medium (tree nodes) |
| **Interface Implemented** | Set | Set | SortedSet, NavigableSet |

### Detailed Comparison

#### 1. Underlying Data Structure

- **HashSet**: Hash table → random access, no order
- **LinkedHashSet**: Hash table + doubly-linked list → maintains insertion order with hash speed
- **TreeSet**: Red-Black balanced tree → automatically sorted

#### 2. Order Guarantees

```
HashSet:        [5, 2, 8, 9] or [2, 5, 8, 9] or [9, 8, 5, 2] - random
LinkedHashSet:  [5, 2, 8, 9] - insertion order preserved
TreeSet:        [2, 5, 8, 9] - sorted order (ascending for numbers)
```

#### 3. Null Handling

```java
// HashSet and LinkedHashSet
set.add(null);      // ✓ Allowed
set.add("A");       // ✓ Allowed
// Result: contains one null and other values

// TreeSet
TreeSet<String> ts = new TreeSet<>();
ts.add(null);       // ✓ Allowed (only if first element)
ts.add("A");        // ✗ Throws NullPointerException
```

#### 4. Performance Impact

```
HashSet:      O(1) - fastest for basic operations
LinkedHashSet: O(1) - same speed, adds order tracking
TreeSet:      O(log n) - slower, but maintains sort
```

#### 5. Type Safety

```java
// HashSet & LinkedHashSet: Can mix types
Set<Object> mixed = new HashSet<>();
mixed.add("String");
mixed.add(123);        // ✓ Works

// TreeSet: Must be homogeneous or use Comparator
Set<Integer> nums = new TreeSet<>();
nums.add(10);
nums.add("String");    // ✗ ClassCastException at runtime
```

### Decision Matrix: Which Set to Use?

| Requirement | Choose |
|------------|--------|
| **Fast, unique values, no order needed** | HashSet |
| **Unique values, preserve insertion order** | LinkedHashSet |
| **Unique values, must be sorted** | TreeSet |
| **Insertion order matters for cache/history** | LinkedHashSet |
| **Need first/last/range queries** | TreeSet |
| **High performance critical** | HashSet |
| **Performance less important, sorting critical** | TreeSet |
| **Want to maintain user insertion sequence** | LinkedHashSet |

### Quick Comparison Example

```java
Integer[] nums = {5, 2, 8, 2, 9, 5};

Set<Integer> hash = new HashSet<>(Arrays.asList(nums));
// Possible output: [2, 5, 8, 9] - random order

Set<Integer> linked = new LinkedHashSet<>(Arrays.asList(nums));
// Output: [5, 2, 8, 9] - insertion order

Set<Integer> tree = new TreeSet<>(Arrays.asList(nums));
// Output: [2, 5, 8, 9] - sorted order
```

### Summary Takeaways

1. **HashSet** - Fastest but unordered
2. **LinkedHashSet** - Insertion order with hash speed
3. **TreeSet** - Sorted but slower (O(log n))
4. **Choose based on**: Speed vs Order tradeoff
5. **Nulls**: HashSet/LinkedHashSet allow one, TreeSet very restrictive
6. **Types**: HashSet/LinkedHashSet flexible, TreeSet strict (unless Comparator)
7. **Interview answer**: HashSet for speed, LinkedHashSet for insertion order, TreeSet for sorting
8. **Real-world**: Most common is HashSet, then TreeSet for sorted needs
9. **LinkedHashSet**: Special use case for caching/LRU implementations
10. **Never mix requirements**: Pick one priority and use appropriate Set implementation

---

## Map Interface (Detailed)

### Overview

`Map` is a **separate interface hierarchy** from `Collection`. It is **NOT a child of Collection**.

A `Map` represents a collection of **key-value pairs** where:
- Each **key** uniquely identifies a value
- **Duplicate keys are NOT allowed** (but duplicate values are allowed)
- **Ordering depends on implementation** (HashMap=random, TreeMap=sorted, LinkedHashMap=insertion)

### Core Concepts

**Key Points:**
- Map is for storing key-value relationships, not just values
- Key must be unique; replacing a key's value overwrites the old value
- Values can be duplicated across different keys
- If same key is added again, the old value is replaced
- Perfect for lookup scenarios where you need: ID → Value, Name → Phone, etc.

### Key-Value Pair Relationship

```
Map<Integer, String> students = new HashMap<>();
students.put(101, "Durga");      // Key=101, Value="Durga"
students.put(102, "Ravi");       // Key=102, Value="Ravi"
students.put(103, "Venkat");     // Key=103, Value="Venkat"
students.put(101, "DURGA");      // Key 101 already exists → value replaced

Result: {101="DURGA", 102="Ravi", 103="Venkat"}
```

### Common Map Methods

| Method | Return Type | Purpose | Example |
|--------|-------------|---------|---------|
| `put(K key, V value)` | `V` | Adds key-value pair, returns old value if exists | `map.put(101, "Durga")` |
| `putAll(Map m)` | `void` | Adds all key-value pairs from another map | `map.putAll(otherMap)` |
| `get(Object key)` | `V` | Gets value associated with key | `String name = map.get(101)` |
| `remove(Object key)` | `V` | Removes entry and returns value | `map.remove(101)` |
| `containsKey(Object key)` | `boolean` | Checks if key exists | `map.containsKey(101)` |
| `containsValue(Object value)` | `boolean` | Checks if value exists | `map.containsValue("Durga")` |
| `size()` | `int` | Returns number of key-value pairs | `map.size()` |
| `isEmpty()` | `boolean` | Checks if map is empty | `map.isEmpty()` |
| `clear()` | `void` | Removes all key-value pairs | `map.clear()` |
| `keySet()` | `Set<K>` | Returns all keys as a set | `Set<Integer> keys = map.keySet()` |
| `values()` | `Collection<V>` | Returns all values as collection | `Collection<String> vals = map.values()` |
| `entrySet()` | `Set<Map.Entry<K,V>>` | Returns all key-value pairs | `Set<Entry> entries = map.entrySet()` |

### Map Hierarchy in Java

```
Map (interface)
├── HashMap (class)
│   └── LinkedHashMap (class)
├── WeakHashMap (class)
├── IdentityHashMap (class)
├── Hashtable (class - legacy)
│   └── Properties (class)
└── SortedMap (interface)
    └── TreeMap (class)
    └── NavigableMap (interface)
        └── TreeMap (class)
```

---

## HashMap (Detailed)

### Overview

`HashMap` is the most commonly used `Map` implementation, introduced in **Java 1.2**.

It uses a **hash table** internally to store key-value pairs with O(1) average performance.

### Key Characteristics

1. **Underlying Structure** - Hash Table
2. **No Order Guarantee** - Random order (neither insertion nor sorted)
3. **Duplicate Keys NOT Allowed** - New value replaces old
4. **Duplicate Values Allowed** - Multiple keys can have same value
5. **Accepts Null** - One null key and multiple null values
6. **Not Synchronized** - Not thread-safe by default
7. **Performance** - O(1) average for get/put/remove
8. **Iterator** - Fails if map is modified during iteration (ConcurrentModificationException)

### Constructors of HashMap

```java
HashMap<K, V> map1 = new HashMap<>();          // Default
HashMap<K, V> map2 = new HashMap<>(int capacity);
HashMap<K, V> map3 = new HashMap<>(int capacity, float loadFactor);
HashMap<K, V> map4 = new HashMap<>(Map<? extends K, ? extends V> m);
```

### Comprehensive HashMap Example (All Functionality)

```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

public class HashMapComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== HASHMAP COMPREHENSIVE DEMO ==========\n");

        // Step 1: Create and Add Key-Value Pairs
        System.out.println("Step 1 - Creating HashMap and Adding Entries:");
        HashMap<Integer, String> students = new HashMap<>();
        
        students.put(101, "Durga");
        students.put(102, "Ravi");
        students.put(103, "Venkat");
        students.put(104, "Suresh");
        students.put(105, null);  // null value allowed
        
        System.out.println("Added: 101→Durga, 102→Ravi, 103→Venkat, 104→Suresh, 105→null");
        System.out.println("HashMap: " + students);
        System.out.println("Note: Order is random, not insertion order\n");

        // Step 2: Adding Duplicate Key (Value Replacement)
        System.out.println("Step 2 - Adding Duplicate Key (Value Replacement):");
        System.out.println("Before: " + students);
        String oldValue = students.put(102, "RAVI");  // Replaces "Ravi"
        System.out.println("Old value for key 102: " + oldValue);
        System.out.println("After put(102, 'RAVI'): " + students);
        System.out.println("Size: " + students.size() + " (not 6, still 5)\n");

        // Step 3: Get Operations
        System.out.println("Step 3 - Get Operations:");
        System.out.println("get(101): " + students.get(101));           // Durga
        System.out.println("get(105): " + students.get(105));           // null
        System.out.println("get(999): " + students.get(999));           // null (not found)
        System.out.println("getOrDefault(999, 'Unknown'): " + students.getOrDefault(999, "Unknown")); // Unknown
        System.out.println();

        // Step 4: Check Operations
        System.out.println("Step 4 - Check Operations:");
        System.out.println("containsKey(103): " + students.containsKey(103));     // true
        System.out.println("containsKey(999): " + students.containsKey(999));     // false
        System.out.println("containsValue('Durga'): " + students.containsValue("Durga")); // true
        System.out.println("containsValue('Unknown'): " + students.containsValue("Unknown")); // false
        System.out.println();

        // Step 5: Remove Operations
        System.out.println("Step 5 - Remove Operations:");
        System.out.println("Before remove: " + students);
        String removed = students.remove(104);
        System.out.println("Removed key 104, value was: " + removed);
        System.out.println("After remove(104): " + students);
        System.out.println();

        // Step 6: Iteration Methods
        System.out.println("Step 6 - Iteration Methods:");
        
        // Method 1: Using entrySet (Most efficient)
        System.out.println("a) Using entrySet():");
        for (Entry<Integer, String> entry : students.entrySet()) {
            System.out.println("   " + entry.getKey() + " → " + entry.getValue());
        }
        
        // Method 2: Using keySet
        System.out.print("b) Using keySet(): ");
        for (Integer key : students.keySet()) {
            System.out.print(key + " ");
        }
        System.out.println();
        
        // Method 3: Using values
        System.out.print("c) Using values(): ");
        for (String value : students.values()) {
            System.out.print(value + " ");
        }
        System.out.println();
        
        // Method 4: Using Iterator
        System.out.println("d) Using Iterator:");
        Iterator<Entry<Integer, String>> it = students.entrySet().iterator();
        while (it.hasNext()) {
            Entry<Integer, String> entry = it.next();
            System.out.println("   " + entry.getKey() + " → " + entry.getValue());
        }
        System.out.println();

        // Step 7: putAll - Add from another Map
        System.out.println("Step 7 - putAll() - Add from Another Map:");
        HashMap<Integer, String> moreStudents = new HashMap<>();
        moreStudents.put(201, "Prabhas");
        moreStudents.put(202, "Nagarjuna");
        
        System.out.println("Original: " + students);
        students.putAll(moreStudents);
        System.out.println("After putAll: " + students);
        System.out.println();

        // Step 8: putIfAbsent - Add only if key doesn't exist
        System.out.println("Step 8 - putIfAbsent():");
        students.putIfAbsent(201, "Unknown");   // Key exists, so not added
        students.putIfAbsent(301, "Satrajit");  // Key doesn't exist, so added
        System.out.println("After putIfAbsent: " + students);
        System.out.println();

        // Step 9: Null Key Support
        System.out.println("Step 9 - Null Key Support:");
        HashMap<String, Integer> nullKeyMap = new HashMap<>();
        nullKeyMap.put(null, 99);               // null as key (allowed, only one)
        nullKeyMap.put("Java", 100);
        System.out.println("Map with null key: " + nullKeyMap);
        System.out.println("Get null key: " + nullKeyMap.get(null));
        System.out.println();

        // Step 10: Clear and isEmpty
        System.out.println("Step 10 - Clear and isEmpty():");
        HashMap<String, String> tempMap = new HashMap<>();
        tempMap.put("A", "1");
        tempMap.put("B", "2");
        System.out.println("Before clear: " + tempMap + ", isEmpty: " + tempMap.isEmpty());
        tempMap.clear();
        System.out.println("After clear: " + tempMap + ", isEmpty: " + tempMap.isEmpty());
        System.out.println();

        // Step 11: Create from another Map
        System.out.println("Step 11 - Create HashMap from another Map:");
        HashMap<Integer, String> original = new HashMap<>();
        original.put(1, "One");
        original.put(2, "Two");
        original.put(3, "Three");
        
        HashMap<Integer, String> copy = new HashMap<>(original);
        System.out.println("Original: " + original);
        System.out.println("Copy: " + copy);
        copy.put(4, "Four");
        System.out.println("After modifying copy: Original: " + original + ", Copy: " + copy);
        System.out.println();

        // Step 12: Duplicate Values Allowed
        System.out.println("Step 12 - Duplicate Values (Allowed):");
        HashMap<Integer, String> dups = new HashMap<>();
        dups.put(1, "Same");
        dups.put(2, "Same");
        dups.put(3, "Same");
        System.out.println("Multiple keys, same value: " + dups);
        System.out.println("containsValue('Same'): " + dups.containsValue("Same")); // true
        System.out.println();

        // Step 13: Size and isEmpty
        System.out.println("Step 13 - Size Information:");
        System.out.println("students size: " + students.size());
        System.out.println("students isEmpty: " + students.isEmpty());
        System.out.println();

        // Step 14: Summary Table
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ Key-value pair storage");
        System.out.println("✓ Duplicate keys NOT allowed (replaces value)");
        System.out.println("✓ Duplicate values allowed");
        System.out.println("✓ One null key, multiple null values");
        System.out.println("✓ Random order (no guarantees)");
        System.out.println("✓ O(1) average performance");
        System.out.println("✓ Not synchronized (use ConcurrentHashMap for threads)");
        System.out.println("✓ Fail-fast iterator (ConcurrentModificationException if modified)");
        System.out.println("✓ Most common Map implementation");
        System.out.println("✓ Best for general-purpose key-value storage");
    }
}

/* Output Sample:
========== HASHMAP COMPREHENSIVE DEMO ==========

Step 1 - Creating HashMap and Adding Entries:
HashMap: {102=RAVI, 103=Venkat, 104=Suresh, 101=Durga, 105=null}
(Note: Order is random, different on each run)

Step 2 - Adding Duplicate Key (Value Replacement):
Old value for key 102: Ravi
Size: 5 (not 6, still 5)

Step 3 - Get Operations:
get(101): Durga
get(105): null
get(999): null

Step 6 - Iteration Methods:
a) Using entrySet():
   102 → RAVI
   103 → Venkat
   104 → Suresh
   101 → Durga
   105 → null

[...continues with all steps...]

========== SUMMARY ==========
✓ Key-value pair storage
✓ Duplicate keys NOT allowed (replaces value)
✓ Duplicate values allowed
✓ One null key, multiple null values
✓ Random order (no guarantees)
✓ O(1) average performance
✓ Not synchronized (use ConcurrentHashMap for threads)
✓ Fail-fast iterator (ConcurrentModificationException if modified)
✓ Most common Map implementation
✓ Best for general-purpose key-value storage
*/
```

---

## LinkedHashMap (Detailed)

### Overview

`LinkedHashMap` is a child class of `HashMap`, introduced in **Java 1.4**.

It combines **HashMap's performance** with **insertion order preservation** using a doubly-linked list internally.

### Key Characteristics

1. **Underlying Structure** - Hash Table + Doubly Linked List (Hybrid)
2. **Insertion Order Preserved** - Iterates in the order keys were inserted
3. **Duplicate Keys NOT Allowed** - Same as HashMap
4. **Performance** - O(1) average (same as HashMap)
5. **Predictable Iteration** - Always in insertion order
6. **Access Order Variant** - Can track last access for LRU cache implementation
7. **Null Support** - One null key, multiple null values

### Constructors of LinkedHashMap

```java
LinkedHashMap<K, V> map1 = new LinkedHashMap<>();
LinkedHashMap<K, V> map2 = new LinkedHashMap<>(int capacity);
LinkedHashMap<K, V> map3 = new LinkedHashMap<>(int capacity, float loadFactor);
LinkedHashMap<K, V> map4 = new LinkedHashMap<>(Map<? extends K, ? extends V> m);
LinkedHashMap<K, V> map5 = new LinkedHashMap<>(int capacity, float loadFactor, boolean accessOrder);
// accessOrder: true = track access order, false = track insertion order
```

### Comprehensive LinkedHashMap Example (All Functionality)

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== LINKEDHASHMAP COMPREHENSIVE DEMO ==========\n");

        // Step 1: Insertion Order Preservation
        System.out.println("Step 1 - Insertion Order Preservation:");
        LinkedHashMap<Integer, String> insertion = new LinkedHashMap<>();
        
        insertion.put(105, "E");
        insertion.put(102, "B");
        insertion.put(103, "C");
        insertion.put(104, "D");
        insertion.put(101, "A");
        
        System.out.println("Insertion order: 105, 102, 103, 104, 101");
        System.out.println("LinkedHashMap: " + insertion);
        System.out.println("✓ Maintains insertion order (not sorted, not random)\n");

        // Step 2: Comparison with HashMap
        System.out.println("Step 2 - Comparison: HashMap vs LinkedHashMap");
        Map<Integer, String> hashMap = new java.util.HashMap<>(insertion);
        LinkedHashMap<Integer, String> linkedMap = new LinkedHashMap<>(insertion);
        
        System.out.println("HashMap (random order): " + hashMap);
        System.out.println("LinkedHashMap (insertion order): " + linkedMap);
        System.out.println();

        // Step 3: Basic Operations (same as HashMap)
        System.out.println("Step 3 - Basic Operations:");
        System.out.println("get(102): " + insertion.get(102));
        insertion.put(102, "B-Updated");
        System.out.println("After updating 102: " + insertion);
        System.out.println("Note: Updating doesn't change iteration order\n");

        // Step 4: Adding New Entry (goes to end of order)
        System.out.println("Step 4 - Adding New Entry:");
        System.out.println("Before add: " + insertion);
        insertion.put(106, "F");
        System.out.println("After add(106, 'F'): " + insertion);
        System.out.println("✓ New entry added to end of insertion order\n");

        // Step 5: Removing Entry
        System.out.println("Step 5 - Removing Entry:");
        System.out.println("Before remove: " + insertion);
        insertion.remove(103);
        System.out.println("After remove(103): " + insertion);
        System.out.println();

        // Step 6: Re-inserting Removed Entry
        System.out.println("Step 6 - Re-inserting Removed Entry:");
        insertion.put(103, "C-Again");
        System.out.println("After put(103, 'C-Again'): " + insertion);
        System.out.println("✓ Re-inserted entry goes to end (maintains insertion order)\n");

        // Step 7: Iteration Order (always insertion order)
        System.out.println("Step 7 - Iteration (always in insertion order):");
        System.out.print("Forward iteration: ");
        for (Integer key : insertion.keySet()) {
            System.out.print(key + " ");
        }
        System.out.println();
        System.out.print("Values in insertion order: ");
        for (String value : insertion.values()) {
            System.out.print(value + " ");
        }
        System.out.println();
        System.out.println();

        // Step 8: Access-Order LinkedHashMap (for LRU Cache)
        System.out.println("Step 8 - Access-Order LinkedHashMap (LRU Cache Simulation):");
        LinkedHashMap<Integer, String> accessOrder = new LinkedHashMap<>(16, 0.75f, true) {
            // Override removeEldestEntry for automatic LRU cache
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > 4;  // Keep only 4 recent entries
            }
        };
        
        accessOrder.put(1, "First");
        accessOrder.put(2, "Second");
        accessOrder.put(3, "Third");
        accessOrder.put(4, "Fourth");
        System.out.println("After adding 4 entries: " + accessOrder);
        
        accessOrder.get(1);  // Access oldest entry
        System.out.println("After accessing 1: " + accessOrder + " (1 moved to end)");
        
        accessOrder.put(5, "Fifth");  // This removes least recently used
        System.out.println("After adding 5: " + accessOrder + " (oldest removed)\n");

        // Step 9: Null Key Support
        System.out.println("Step 9 - Null Key Support:");
        LinkedHashMap<String, Integer> nullMap = new LinkedHashMap<>();
        nullMap.put("A", 1);
        nullMap.put(null, 99);
        nullMap.put("B", 2);
        System.out.println("With null key: " + nullMap);
        System.out.println("null key position: maintains insertion order\n");

        // Step 10: Copy Constructor
        System.out.println("Step 10 - Copy Constructor:");
        LinkedHashMap<Integer, String> original = new LinkedHashMap<>();
        original.put(3, "C");
        original.put(1, "A");
        original.put(2, "B");
        
        LinkedHashMap<Integer, String> copy = new LinkedHashMap<>(original);
        System.out.println("Original: " + original);
        System.out.println("Copy: " + copy);
        System.out.println("✓ Copy preserves insertion order from original\n");

        // Step 11: Clear and Size
        System.out.println("Step 11 - Clear and Size:");
        LinkedHashMap<String, String> temp = new LinkedHashMap<>();
        temp.put("X", "1");
        temp.put("Y", "2");
        System.out.println("Size: " + temp.size() + ", isEmpty: " + temp.isEmpty());
        temp.clear();
        System.out.println("After clear, Size: " + temp.size() + ", isEmpty: " + temp.isEmpty());
        System.out.println();

        // Step 12: Summary Table
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ Insertion order always preserved");
        System.out.println("✓ Child class of HashMap (same performance O(1))");
        System.out.println("✓ Duplicate keys NOT allowed");
        System.out.println("✓ Duplicate values allowed");
        System.out.println("✓ One null key, multiple null values");
        System.out.println("✓ Access-order variant for LRU cache");
        System.out.println("✓ Predictable iteration order");
        System.out.println("✓ Slightly more memory than HashMap (linked list pointers)");
        System.out.println("✓ Perfect for maintaining insertion sequence");
        System.out.println("✓ Ideal for caching, recently used items");
    }
}

/* Output Sample:
========== LINKEDHASHMAP COMPREHENSIVE DEMO ==========

Step 1 - Insertion Order Preservation:
LinkedHashMap: {105=E, 102=B, 103=C, 104=D, 101=A}

Step 2 - Comparison: HashMap vs LinkedHashMap
HashMap (random order): {102=B, 104=D, 105=E, 103=C, 101=A}
LinkedHashMap (insertion order): {105=E, 102=B, 103=C, 104=D, 101=A}

Step 4 - Adding New Entry:
After add(106, 'F'): {105=E, 102=B, 103=C, 104=D, 101=A, 106=F}

Step 8 - Access-Order LinkedHashMap (LRU Cache Simulation):
After accessing 1: {2=Second, 3=Third, 4=Fourth, 1=First}
After adding 5: {3=Third, 4=Fourth, 1=First, 5=Fifth}

========== SUMMARY ==========
✓ Insertion order always preserved
✓ Child class of HashMap (same performance O(1))
✓ Perfect for maintaining insertion sequence
✓ Ideal for caching, recently used items
*/
```

---

## TreeMap (Detailed)

### Overview

`TreeMap` is the Map implementation of the `SortedMap` interface, introduced in **Java 1.2**.

It uses a **Balanced Binary Search Tree** internally to maintain keys in sorted order.

### Key Characteristics

1. **Underlying Structure** - Balanced Binary Search Tree (Red-Black Tree)
2. **Keys Always Sorted** - Based on natural order or custom comparator
3. **Duplicate Keys NOT Allowed** - Same as all maps
4. **Duplicate Values Allowed** - Multiple keys can have same value
5. **Null Key NOT Allowed** - Throws NullPointerException
6. **Null Values Allowed** - Values can be null
7. **Performance** - O(log n) for get/put/remove (slower than HashMap)
8. **SortedMap Methods** - firstKey(), lastKey(), headMap(), tailMap(), subMap()
9. **Comparable Support** - Keys must be Comparable or provide Comparator

### Constructors of TreeMap

```java
TreeMap<K, V> map1 = new TreeMap<>();              // Natural order
TreeMap<K, V> map2 = new TreeMap<>(Comparator c); // Custom order
TreeMap<K, V> map3 = new TreeMap<>(Map m);        // From map
TreeMap<K, V> map4 = new TreeMap<>(SortedMap m);  // From SortedMap
```

### Comprehensive TreeMap Example (All Functionality)

```java
import java.util.Comparator;
import java.util.TreeMap;
import java.util.Map.Entry;

public class TreeMapComprehensiveDemo {
    public static void main(String[] args) {
        System.out.println("========== TREEMAP COMPREHENSIVE DEMO ==========\n");

        // Step 1: TreeMap with Natural Sorting (Integers - ascending)
        System.out.println("Step 1 - TreeMap with Natural Sorting (Numbers):");
        TreeMap<Integer, String> numbers = new TreeMap<>();
        
        numbers.put(105, "E");
        numbers.put(102, "B");
        numbers.put(103, "C");
        numbers.put(104, "D");
        numbers.put(101, "A");
        
        System.out.println("Added in order: 105, 102, 103, 104, 101");
        System.out.println("TreeMap (sorted): " + numbers);
        System.out.println("✓ Keys automatically sorted in ascending order\n");

        // Step 2: TreeMap with Strings (Alphabetical sorting)
        System.out.println("Step 2 - TreeMap with Strings (Alphabetical):");
        TreeMap<String, Integer> employees = new TreeMap<>();
        
        employees.put("Venky", 150);
        employees.put("Nag", 100);
        employees.put("Chiru", 50);
        employees.put("Balayya", 200);
        
        System.out.println("Added in order: Venky, Nag, Chiru, Balayya");
        System.out.println("TreeMap (alphabetical): " + employees);
        System.out.println();

        // Step 3: TreeMap with Custom Comparator (Reverse order)
        System.out.println("Step 3 - TreeMap with Custom Comparator (Descending):");
        TreeMap<Integer, String> reverse = new TreeMap<>(Comparator.reverseOrder());
        reverse.putAll(numbers);
        
        System.out.println("Default ascending: " + numbers);
        System.out.println("Custom descending: " + reverse);
        System.out.println();

        // Step 4: SortedMap Methods - firstKey() and lastKey()
        System.out.println("Step 4 - SortedMap Methods (firstKey/lastKey):");
        System.out.println("firstKey(): " + numbers.firstKey());         // 101
        System.out.println("lastKey(): " + numbers.lastKey());           // 105
        System.out.println("firstEntry(): " + numbers.firstEntry());     // 101=A
        System.out.println("lastEntry(): " + numbers.lastEntry());       // 105=E
        System.out.println();

        // Step 5: headMap() - Keys less than specified key
        System.out.println("Step 5 - headMap(key) - Keys < specified:");
        System.out.println("headMap(103): " + numbers.headMap(103));     // {101=A, 102=B}
        System.out.println();

        // Step 6: tailMap() - Keys >= specified key
        System.out.println("Step 6 - tailMap(key) - Keys >= specified:");
        System.out.println("tailMap(103): " + numbers.tailMap(103));     // {103=C, 104=D, 105=E}
        System.out.println();

        // Step 7: subMap() - Range of keys
        System.out.println("Step 7 - subMap(from, to) - Range (from inclusive, to exclusive):");
        System.out.println("subMap(102, 105): " + numbers.subMap(102, 105)); // {102=B, 103=C, 104=D}
        System.out.println();

        // Step 8: Get and Put Operations
        System.out.println("Step 8 - Get and Put Operations (sorted order maintained):");
        System.out.println("Before: " + numbers);
        
        String value = numbers.get(103);
        System.out.println("get(103): " + value);
        
        numbers.put(103, "C-Updated");
        System.out.println("After put(103, 'C-Updated'): " + numbers);
        System.out.println("✓ Update doesn't change sorted order\n");

        // Step 9: Adding New Entry (automatically placed in sorted position)
        System.out.println("Step 9 - Adding New Entry (automatically sorted):");
        System.out.println("Before: " + numbers);
        numbers.put(103, "C");  // Revert
        numbers.put(103, "C");
        numbers.put(102, "B");
        numbers.put(104, "E");
        
        TreeMap<Integer, String> sorted = new TreeMap<>();
        sorted.put(50, "Fifty");
        sorted.put(100, "Hundred");
        sorted.put(10, "Ten");
        sorted.put(75, "SeventyFive");
        
        System.out.println("Added: 50, 100, 10, 75");
        System.out.println("TreeMap: " + sorted);
        System.out.println("✓ Auto-sorted regardless of insertion order\n");

        // Step 10: Remove Operation
        System.out.println("Step 10 - Remove Operation:");
        System.out.println("Before: " + sorted);
        String removed = sorted.remove(100);
        System.out.println("Removed key 100, value: " + removed);
        System.out.println("After: " + sorted);
        System.out.println();

        // Step 11: Null Key NOT Allowed (Null Values OK)
        System.out.println("Step 11 - Null Key vs Null Value:");
        TreeMap<String, Integer> nullTest = new TreeMap<>();
        nullTest.put("A", 1);
        nullTest.put("B", null);  // ✓ Null value allowed
        System.out.println("With null value: " + nullTest);
        
        try {
            nullTest.put(null, 99);  // ✗ Null key NOT allowed
            System.out.println("With null key: " + nullTest);
        } catch (NullPointerException e) {
            System.out.println("NullPointerException: Cannot use null as key in TreeMap");
        }
        System.out.println();

        // Step 12: Iteration (always sorted order)
        System.out.println("Step 12 - Iteration (always in sorted order):");
        System.out.print("Keys: ");
        for (Integer key : sorted.keySet()) {
            System.out.print(key + " ");
        }
        System.out.println();
        System.out.print("Values: ");
        for (String val : sorted.values()) {
            System.out.print(val + " ");
        }
        System.out.println();
        System.out.print("Entries: ");
        for (Entry<Integer, String> entry : sorted.entrySet()) {
            System.out.print(entry.getKey() + "=" + entry.getValue() + " ");
        }
        System.out.println();
        System.out.println();

        // Step 13: Backed Collections (subMap changes reflect original)
        System.out.println("Step 13 - Backed Collections (subMap view):");
        System.out.println("Original: " + sorted);
        
        TreeMap<Integer, String> sub = new TreeMap<>(sorted.subMap(10, 100));
        System.out.println("subMap(10, 100): " + sub);
        System.out.println();

        // Step 14: Comparator Method
        System.out.println("Step 14 - Comparator Method:");
        TreeMap<Integer, String> natural = new TreeMap<>();
        TreeMap<Integer, String> custom = new TreeMap<>(Comparator.reverseOrder());
        
        System.out.println("Natural order comparator: " + natural.comparator());  // null
        System.out.println("Custom comparator: " + custom.comparator());  // Comparator instance
        System.out.println();

        // Step 15: Size and isEmpty
        System.out.println("Step 15 - Size and isEmpty:");
        System.out.println("Size: " + sorted.size());
        System.out.println("isEmpty: " + sorted.isEmpty());
        sorted.clear();
        System.out.println("After clear - Size: " + sorted.size() + ", isEmpty: " + sorted.isEmpty());
        System.out.println();

        // Step 16: Summary
        System.out.println("========== SUMMARY ==========");
        System.out.println("✓ Keys always sorted (ascending or custom)");
        System.out.println("✓ Child of SortedMap interface");
        System.out.println("✓ Duplicate keys NOT allowed");
        System.out.println("✓ Duplicate values allowed");
        System.out.println("✓ Null keys NOT allowed (NullPointerException)");
        System.out.println("✓ Null values allowed");
        System.out.println("✓ O(log n) performance (slower than HashMap)");
        System.out.println("✓ SortedMap methods: firstKey(), lastKey(), headMap(), tailMap(), subMap()");
        System.out.println("✓ Range queries efficient");
        System.out.println("✓ Use when: Sorted keys or range operations needed");
    }
}

/* Output Sample:
========== TREEMAP COMPREHENSIVE DEMO ==========

Step 1 - TreeMap with Natural Sorting (Numbers):
TreeMap (sorted): {101=A, 102=B, 103=C, 104=D, 105=E}

Step 2 - TreeMap with Strings (Alphabetical):
TreeMap (alphabetical): {Balayya=200, Chiru=50, Nag=100, Venky=150}

Step 3 - TreeMap with Custom Comparator (Descending):
Default ascending: {101=A, 102=B, 103=C, 104=D, 105=E}
Custom descending: {105=E, 104=D, 103=C, 102=B, 101=A}

Step 4 - SortedMap Methods (firstKey/lastKey):
firstKey(): 101
lastKey(): 105

[...continues with all steps...]

========== SUMMARY ==========
✓ Keys always sorted (ascending or custom)
✓ Child of SortedMap interface
✓ Use when: Sorted keys or range operations needed
*/
```

---

## Map Implementation Classes Comparison

### Comprehensive Comparison Table

| Property | HashMap | LinkedHashMap | TreeMap |
|----------|---------|---------------|---------|
| **Underlying Data Structure** | Hash Table | Hash Table + Linked List | Balanced Binary Search Tree |
| **Key Order** | Random/Unordered | Insertion Order | Sorted Order |
| **Duplicate Keys** | ✗ Not allowed | ✗ Not allowed | ✗ Not allowed |
| **Duplicate Values** | ✓ Allowed | ✓ Allowed | ✓ Allowed |
| **Null Key** | ✓ One null | ✓ One null | ✗ Not allowed |
| **Null Values** | ✓ Multiple nulls | ✓ Multiple nulls | ✓ Multiple nulls |
| **Performance (get/put/remove)** | O(1) average | O(1) average | O(log n) |
| **Interface Implemented** | Map | Map | SortedMap, NavigableMap |
| **Best Use Case** | Fast lookups | Insertion order needed | Sorted keys needed |
| **Memory Overhead** | Low | Medium (linked list) | Medium (tree nodes) |
| **Thread-Safe Variant** | ConcurrentHashMap | Collections.synchronizedMap | ConcurrentSkipListMap |
| **Comparator Support** | N/A | N/A | ✓ Yes (required for order) |

### Detailed Comparison

#### 1. Key Ordering

```java
Map<Integer, String> data = {105→E, 102→B, 103→C, 104→D, 101→A};

HashMap:          Random: {105=E, 102=B, 103=C, 104=D, 101=A} (varies each run)
LinkedHashMap:    Insertion: {105=E, 102=B, 103=C, 104=D, 101=A}
TreeMap:          Sorted: {101=A, 102=B, 103=C, 104=D, 105=E}
```

#### 2. Performance Comparison

```
Operation     | HashMap | LinkedHashMap | TreeMap
get(key)      | O(1)    | O(1)          | O(log n)
put(key)      | O(1)    | O(1)          | O(log n)
remove(key)   | O(1)    | O(1)          | O(log n)
containsKey   | O(1)    | O(1)          | O(log n)
```

#### 3. Null Handling

```java
// HashMap & LinkedHashMap
map.put(null, value);      // ✓ Allowed (one null key)
map.put(key, null);        // ✓ Allowed (multiple null values)

// TreeMap
map.put(null, value);      // ✗ NullPointerException
map.put(key, null);        // ✓ Allowed (null values OK)
```

### Decision Matrix: Which Map to Use?

| Requirement | Choose |
|------------|--------|
| **Fast, no specific order needed** | HashMap |
| **Must preserve insertion order** | LinkedHashMap |
| **Keys must be sorted** | TreeMap |
| **Maximum performance critical** | HashMap |
| **Need range queries (headMap, tailMap)** | TreeMap |
| **LRU cache implementation** | LinkedHashMap (access-order) |
| **Want predictable iteration** | TreeMap (sorted) or LinkedHashMap (insertion) |
| **Key lookup performance** | HashMap |

### Quick Comparison Example

```java
Map<Integer, String> data = {105→E, 102→B, 103→C, 104→D, 101→A};

HashMap output:        {105=E, 102=B, 103=C, 104=D, 101=A}  // Random
LinkedHashMap output:  {105=E, 102=B, 103=C, 104=D, 101=A}  // Insertion
TreeMap output:        {101=A, 102=B, 103=C, 104=D, 105=E}  // Sorted
```

### Summary Takeaways

1. **HashMap** - Fastest, random order
2. **LinkedHashMap** - Insertion order with hash speed
3. **TreeMap** - Sorted keys but slower (O(log n))
4. **Choose based on**: Speed vs Order tradeoff
5. **Null Keys**: HashMap/LinkedHashMap allow one, TreeMap doesn't allow any
6. **Common Operations** - All three have same basic methods (put, get, remove)
7. **Interview Answer** - HashMap for speed, TreeMap for sorted, LinkedHashMap for order
8. **Performance Trade**: HashMap (fastest) > LinkedHashMap (same as HashMap) > TreeMap (slower)
9. **Real-world Usage**: HashMap most common, then TreeMap for sorted requirements
10. **Hybrid Approach**: Use HashMap for caching, TreeMap for sorted unique keys
```

