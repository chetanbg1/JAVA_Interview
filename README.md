# JAVA_Interview

1. What are the four main principles of OOP in Java?

The four fundamental principles of Object-Oriented Programming in Java are:
Encapsulation: Wrapping data (variables) and methods that operate on the data into a single unit called a class. It helps in protecting the internal state of the object from outside modification.

public class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }
}

Abstraction: Hiding the implementation details and exposing only the functionality to the user. Achieved using abstract classes and interfaces.
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}

Inheritance: A mechanism where one class acquires the properties and behavior of another class. Promotes code reuse.

class Animal {
    void eat() {
        System.out.println("This animal eats food");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

Polymorphism: The ability to present the same interface for different data types or forms. Achieved via method overloading and overriding.

class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

// Runtime Polymorphism
Animal a = new Dog();
a.sound(); // Output: Dog barks

2. What is the difference between an interface and an abstract class?

 1. Purpose
Abstract Class: Used when classes share common behavior (methods and fields) and you want to provide a partial implementation.
Interface: Used to define a contract that multiple unrelated classes can implement.

🔹 2. Keyword
Abstract Class: Declared using the abstract keyword.
Interface: Declared using the interface keyword.

🔹 3. Method Implementation
Abstract Class: Can have both abstract methods (no body) and fully implemented (concrete) methods.
abstract class Animal {
    abstract void sound(); // abstract method
    void eat() {
        System.out.println("Eating...");
    }
}
Interface: Before Java 8, could only have abstract methods. From Java 8 onwards, can have:
default methods with implementation
static methods with implementation
Abstract methods (by default)

interface Animal {
    void sound(); // abstract by default

    default void eat() {
        System.out.println("Eating...");
    }
}
🔹 4. Fields / Variables
Abstract Class: Can have instance variables (state), with any access modifier (private, protected, etc.).
Interface: Can only have public static final constants (i.e., variables are implicitly static and final).

🔹 5. Constructors
Abstract Class: Can have constructors.
Interface: Cannot have constructors.

🔹 6. Multiple Inheritance
Abstract Class: Java does not support multiple inheritance with classes (to avoid the diamond problem).
Interface: Supports multiple inheritance. A class can implement multiple interfaces.

interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

class Duck implements Flyable, Swimmable {
    public void fly() { System.out.println("Flying"); }
    public void swim() { System.out.println("Swimming"); }
}
🔹 7. Accessibility Modifiers for Members
Abstract Class: Members can have any access modifier (private, protected, public).
Interface: All methods are public by default.

🔹 8. When to Use What?
Use an Abstract Class:
When you want to share code among several closely related classes.
When you expect classes to have common state or fields.

Use an Interface:
When you want to define a role that other classes can play, regardless of where they sit in the class hierarchy.
When you need multiple inheritance of type.

🔹 9. Java 8, 9 and Onward Enhancements
Interface: Since Java 8 — default and static methods.
Since Java 9 — private methods in interfaces are also allowed.
Abstract class has remained mostly the same.
Feature	                              Abstract Class	                        Interface
Keyword	                              abstract                              	interface
Method types	                        Abstract + Concrete                     Abstract, Default, Static
Fields	                              Any type	                              public static final only
Constructors                        	Yes                                    	No
Multiple inheritance                	Not                                     supported	Supported
Access modifiers	                    Flexible                              	Only public
Use case	                            Common behavior	                        Capability or contract

3. What is method overloading and method overriding?
Method Overloading: Same method name with different parameter lists within the same class. It is resolved at compile-time.

class MathUtil {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

Method Overriding: A subclass provides a specific implementation of a method already defined in its superclass. Resolved at runtime (polymorphism).

class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow");
    }
}

4. What is the difference between this and super keywords?
this: Refers to the current class instance. It is used to access fields and methods of the current object.
super: Refers to the immediate parent class. It is used to call the parent class’s methods and constructors.

class Animal {
    String color = "white";
}

class Dog extends Animal {
    String color = "black";

    void printColor() {
        System.out.println(super.color); // white
        System.out.println(this.color);  // black
    }
}

5. Can we achieve multiple inheritance in Java?
Java does not support multiple inheritance using classes to avoid ambiguity. However, it is supported through interfaces.
interface Printable {
    void print();
}

interface Showable {
    void show();
}

class Test implements Printable, Showable {
    public void print() {
        System.out.println("Print");
    }
    public void show() {
        System.out.println("Show");
    }
}

6. What is the difference between composition and inheritance?
Inheritance: Represents an "is-a" relationship.
Composition: Represents a "has-a" relationship (i.e., using instances of one class inside another).
Inheritance is tightly coupled and less flexible. Composition promotes flexibility and reusability.

7. What is constructor overloading?
Constructor overloading means having more than one constructor in a class with different parameter lists.

class Employee {
    Employee() {
        System.out.println("Default constructor");
    }

    Employee(String name) {
        System.out.println("Constructor with name: " + name);
    }
}

8. What is object cloning?
Object cloning is the process of creating an exact copy of an object. This is done using the clone() method from the Object class.

class Employee implements Cloneable {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
You must implement Cloneable interface and override clone() method.

9. What is the difference between shallow and deep copy?
Shallow Copy: Copies object references. Changes to referenced objects reflect in both original and copy.
Deep Copy: Creates a copy of object along with the objects it refers to (nested objects).
Deep copy requires manual copying or serialization-based cloning.

10. What is the role of access modifiers in OOP?
Access modifiers define the visibility of classes, methods, and fields:
private: Accessible only within the class.
default (no modifier): Accessible within the package.
protected: Accessible in the same package and subclasses.
public: Accessible from everywhere.
Using proper modifiers ensures encapsulation and security.

1. What is the Stream API in Java?
Answer:
The Stream API, introduced in Java 8, provides a functional-style way to process collections of objects. A stream is not a data structure; instead, it is a sequence of elements from a source (like a collection or array) that supports aggregate operations (like filter, map, reduce, etc.).

Key characteristics:
Doesn't modify the original data structure.
Lazy: operations are only performed when a terminal operation is invoked.
Can be parallel or sequential.

2. What is the difference between a stream and a collection?

Answer:

Feature

Collection

Stream

Storage

Stores data

Does not store data

Iteration

External iteration (for-each)

Internal iteration (managed by JVM)

Reusability

Can be iterated multiple times

Can only be consumed once

Operations

CRUD operations

Aggregate functional operations

3. What are intermediate and terminal operations in streams?
Intermediate operations: Return another stream. They are lazy, meaning the computation is deferred until a terminal operation is called.
Examples: filter, map, sorted, limit
Terminal operations: Produce a result or side-effect. They trigger the actual processing of the stream pipeline.
Examples: collect, forEach, count, reduce

Example:
List<String> names = List.of("John", "Jane", "Jack");
names.stream()
     .filter(name -> name.startsWith("J")) // intermediate
     .forEach(System.out::println);         // terminal

4. What is the difference between map() and flatMap()?
map() is used to transform each element into another form (one-to-one mapping).
flatMap() is used when each element is transformed into a stream, and those multiple streams are then flattened into a single stream (one-to-many).

Example:
List<String> words = List.of("hello", "world");
List<String> chars = words.stream()
     .map(word -> word.split("")) // Stream<String[]>
     .flatMap(Arrays::stream)      // Stream<String>
     .collect(Collectors.toList());

5. What is the use of collect() in streams?
collect() is a terminal operation used to transform the stream elements into a collection, map, or a single result.
Example:
List<String> filteredNames = names.stream()
     .filter(name -> name.length() > 3)
     .collect(Collectors.toList());
You can also use Collectors.joining(), Collectors.groupingBy(), Collectors.partitioningBy(), etc.

6. What is reduce() in streams?
Answer:
reduce() is a terminal operation that aggregates elements of a stream into a single result by repeatedly applying a combining function.
Example:
int sum = List.of(1, 2, 3, 4)
     .stream()
     .reduce(0, Integer::sum); // returns 10

7. What is lazy evaluation in streams?
Answer:
Streams use lazy evaluation, meaning intermediate operations are not executed until a terminal operation is encountered. This improves performance and allows short-circuiting (e.g., in findFirst(), limit()).

8. What is a parallel stream?
Answer:
A parallel stream splits the stream into multiple substreams and processes them in parallel using multiple threads (Fork/Join framework). It can improve performance for large data sets but may not always be faster due to thread overhead.
Example:
list.parallelStream()
    .filter(x -> x > 10)
    .forEach(System.out::println);

9. Can you reuse a stream in Java?
Answer:
No. A stream can only be consumed once. Attempting to reuse a stream after a terminal operation results in IllegalStateException.

10. What is the difference between findFirst() and findAny()?
Answer:
findFirst() returns the first element in the stream (useful when order matters).
findAny() may return any element (useful in parallel streams for better performance).

11. What are custom collectors and how do you create one?
Answer:
Custom collectors are user-defined implementations of the Collector interface used with the collect() terminal operation. You create one when built-in collectors don't fit your requirements.
A custom collector requires:
A supplier (creates a container),
An accumulator (adds elements),
A combiner (merges two containers in parallel streams),
A finisher (optional transformation),
acteristics (e.g., CONCURRENT, UNORDERED, IDENTITY_FINISH).

Example:

Collector<String, StringBuilder, String> customCollector = Collector.of(
    StringBuilder::new,
    StringBuilder::append,
    StringBuilder::append,
    StringBuilder::toString
);

String result = Stream.of("Java", "Stream", "API")
                      .collect(customCollector);
System.out.println(result); // JavaStreamAPI

12. How does short-circuiting work in streams?
Answer:
Short-circuiting refers to stopping the stream pipeline early when the desired result is found. It helps improve performance.
Examples:
limit(n) – stops after processing n elements.
anyMatch() / findFirst() – terminates as soon as condition is satisfied.

Stream.of(1, 2, 3, 4, 5)
      .filter(n -> n > 2)
      .findFirst(); // Stops after finding 3
      
13. How do you handle checked exceptions in a stream pipeline?
Answer:
Streams don’t allow checked exceptions in lambdas. You must handle them explicitly, often by wrapping with a try-catch or rethrowing as unchecked.
Example:
Stream.of("file1.txt", "file2.txt")
      .map(path -> {
          try {
              return new String(Files.readAllBytes(Paths.get(path)));
          } catch (IOException e) {
              throw new UncheckedIOException(e);
          }
      })
      .forEach(System.out::println);
14. What are infinite streams? How do you generate them?
Answer:
Infinite streams are streams that don't have a predefined size. You can generate them using Stream.generate() or Stream.iterate().
Stream.generate(Math::random)
      .limit(5)
      .forEach(System.out::println);

Stream.iterate(0, n -> n + 2)
      .limit(5)
      .forEach(System.out::println); // 0, 2, 4, 6, 8
15. What is the difference between groupingBy() and partitioningBy() in streams?
Answer:
groupingBy() groups elements by a classifier function and returns a Map<K, List<T>>.
partitioningBy() splits the stream into two groups based on a predicate (true/false) and returns Map<Boolean, List<T>>.

// groupingBy
Map<Integer, List<String>> map = Stream.of("apple", "banana", "pear")
    .collect(Collectors.groupingBy(String::length));

// partitioningBy
Map<Boolean, List<String>> partition = Stream.of("apple", "banana", "pear")
    .collect(Collectors.partitioningBy(s -> s.length() > 4));
    
16. When should you prefer sequential vs. parallel streams?
Answer:
Use sequential streams when:
Order matters
The dataset is small
You have I/O-bound operations

Use parallel streams when:
The dataset is large
CPU-intensive operations are involved
No side effects (stateless, associative operations)
You don't care about order

Be cautious with:
Shared mutable state (may cause race conditions)
Performance — parallelism may not always be faster due to thread overhead



1. What is the static keyword in Java?
Answer:
The static keyword in Java is used for memory management. It can be applied to:
Variables
Methods
Blocks
Nested classes
Static members belong to the class rather than instances, meaning they are shared across all objects of that class.

2. What is a static variable?
Answer:
A static variable is shared among all instances of a class. It is initialized only once, at class loading time.
Example:

class Counter {
    static int count = 0;
    Counter() {
        count++;
        System.out.println(count);
    }
}
Each new object increments the same shared variable count.

3. What is a static method?
Answer:
A static method belongs to the class and can be called without creating an object. It can only access other static members.

class MathUtil {
    public static int square(int x) {
        return x * x;
    }
}
Call: MathUtil.square(5);

4. What is a static block?
Answer:
A static block is used to initialize static variables. It is executed only once when the class is first loaded.

class Test {
    static int num;
    static {
        num = 100;
        System.out.println("Static block executed");
    }
}

5. Can we override static methods?
Answer:
No. Static methods are not polymorphic and cannot be overridden in the classical sense. If you declare a static method with the same signature in a subclass, it hides the superclass method.

6. Can a static class exist in Java?
Answer:
Only nested (inner) classes can be static. A static nested class can access static members of the outer class.

class Outer {
    static class Inner {
        void msg() { System.out.println("Static inner class"); }
    }
}

Java Multithreading Qna

[Multithreading, Memory Management, Exception Handling, OOPs, Stream API, Static, Inner Classes Interview Questions and Answers]

(...existing content...)

Java Inner Classes Interview Questions (with Detailed Answers)

1. What are inner classes in Java?
Answer:
Inner classes are classes defined within another class. They are used to logically group classes that are only used in one place and can access all members (even private) of the outer class. Java supports the following types:
Non-static (regular) inner class
Static nested class
Local inner class (defined inside a method)
Anonymous inner class (without a name, used for one-time use)

2. What is the difference between a static nested class and a non-static inner class?

 1. Definition:
Static Nested Class:
Declared static inside another class.
Does not require an instance of the outer class to be instantiated.

Non-static Inner Class (Member Inner Class):
Declared without the static keyword.
Is associated with an instance of the outer class.

🔹 2. Access to Outer Class Members:
Static Nested Class:
Can only access static members (fields or methods) of the outer class directly.
Cannot access instance members of the outer class unless an object is created explicitly.

Non-static Inner Class:
Can access all members (static and instance) of the outer class.
Has an implicit reference to the outer class instance.

🔹 3. Instantiation:
Static Nested Class:

Outer.StaticNested obj = new Outer.StaticNested();

Non-static Inner Class:
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();

🔹 4. Memory Implication:
Static Nested Class:
Doesn't keep a reference to the outer class object.
Consumes less memory in some cases.
Non-static Inner Class:
Holds an implicit reference to its enclosing outer class instance.
May cause memory leaks if not managed properly.

🔹 5. Use Case:
Static Nested Class:
Use when the nested class is logically associated with the outer class but does not need access to instance members.
Example: Map.Entry inside Map
Non-static Inner Class:
Use when the nested class needs to work closely with the outer class's instance members.
class Outer {
    private int outerData = 10;
    static int staticOuterData = 20;

    static class StaticNested {
        void display() {
            // System.out.println(outerData); // Error: can't access non-static
            System.out.println(staticOuterData); // OK
        }
    }

    class Inner {
        void display() {
            System.out.println(outerData); // OK
            System.out.println(staticOuterData); // OK
        }
    }
}
🧠 Summary:
Feature                                  	Static Nested Class                      	Non-static Inner Class
Requires outer class instance?	          ❌ No                                    	✅ Yes
Access to outer instance members	        ❌ No (only static members)	              ✅ Yes
Can be static?                          	✅ Yes	                                   ❌ No
Use case	                                Utility/helper class	                    Instance-bound logic


3. What is an anonymous inner class? Give an example.
Answer:
An anonymous inner class is a class without a name and is used to provide a class implementation on the fly, typically for interfaces or abstract classes.
Example:
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Running in thread");
    }
};
new Thread(r).start();

4. What is a local inner class?
Answer:
A local inner class is defined within a method and is accessible only within that method. It cannot be declared with static and can access final or effectively final variables of the enclosing method.
Example:
void display() {
    final int num = 100;
    class Local {
        void print() {
            System.out.println(num);
        }
    }
    new Local().print();
}

5. Why and when should you use inner classes?
Answer:
Use inner classes to logically group code that is only used in one place, enhance encapsulation, and simplify code readability. For instance, when a class helps only its outer class, it makes sense to keep it as an inner class.

6. Can an inner class extend another class or implement an interface?
Answer:
Yes. Inner classes can extend other classes or implement interfaces just like regular classes.
Example:
class Outer {
    class Inner implements Runnable {
        public void run() {
            System.out.println("Running");
        }
    }
}

7. Can we declare a static method inside a non-static inner class?
Answer:
No. A non-static inner class cannot have static members, including static methods. Only static nested classes can have static members.


1. What is a thread in Java?
A thread in Java is a lightweight process and the smallest unit of CPU execution.
Java enables concurrent execution of two or more parts of a program using threads.
Each thread has its own call stack and program counter but shares memory and resources with other threads in the same process.
Threads are especially useful in applications that require background processing, parallel tasks, or responsiveness (like GUIs or servers).

2. What is the difference between a process and a thread?
A process is an independent program in execution with its own memory space and resources.
A thread is a sub-unit of a process and shares the same memory and resources of its parent process.
Processes are isolated from each other, whereas threads within the same process can communicate directly by reading and writing to shared variables.

3. How do you create a thread in Java?There are two main ways:
Extending the Thread class and overriding its run() method. Then you create an object of your class and call start().
Implementing the Runnable interface, passing it to a Thread object, and then calling start(). This is preferred since Java supports single inheritance.
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}

// OR

class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running");
    }
}

4. What are the thread lifecycle states in Java?Java threads can be in one of the following states:
New: Thread is created but not started.
Runnable: Thread is ready to run but waiting for CPU.
Running: Thread is currently executing.
Blocked: Thread is waiting to acquire a monitor lock.
Waiting: Thread is waiting indefinitely for another thread to perform a particular action.
Timed Waiting: Thread is waiting for a specific time (e.g., sleep() or join(timeout)).
Terminated: Thread has finished execution.

5. What is the difference between start() and run() method?
start() is used to start a new thread, which then calls the run() method in a new call stack.
Calling run() directly doesn't start a new thread—it just runs the code in the current thread like a normal method call.

6. What is the purpose of the sleep() method in threads?
The sleep() method pauses the current thread for a given time (in milliseconds). This gives other threads a chance to execute.
Thread.sleep(1000); // pauses for 1 second
It's often used for timing control, simulating delay, or throttling operations.

7. What is the use of join() method?
The join() method causes the current thread to wait until the thread on which it is called has finished executing. It's useful when one thread needs to finish before another continues.

Thread t1 = new Thread(() -> { /* task */ });
t1.start();
t1.join(); // current thread waits for t1 to finish

8. What is thread priority and how is it set?
Each thread has a priority (from 1 to 10), influencing thread scheduling. Higher priority threads are more likely to be selected for execution, though it's not guaranteed due to OS-level scheduling.

Thread.currentThread().setPriority(Thread.MAX_PRIORITY); // value 10

9. What is the default priority of a thread?
The default thread priority is Thread.NORM_PRIORITY, which is 5. Threads inherit the priority of their parent thread unless changed explicitly.

10. What happens if an exception is thrown inside a thread?
If an exception is thrown and not caught within a thread's run() method, the thread will terminate abnormally. It does not affect other threads, but uncaught exceptions should be logged or handled using Thread.setUncaughtExceptionHandler() for graceful degradation.

11. What is synchronization in Java? Why is it needed?
    Synchronization in Java is a mechanism that ensures only one thread can access a critical section (shared resource) at a time. It's necessary when multiple threads share data to prevent data inconsistency and race conditions. Without synchronization, two threads could simultaneously change the same data, leading to unpredictable results.

synchronized void increment() {
    count++;
}

12. What is a race condition?
A race condition occurs when two or more threads try to modify shared data concurrently and the final outcome depends on the thread scheduling. This leads to unexpected results and bugs. Synchronization helps avoid race conditions.

14. How do you synchronize a method or block of code?
You can use the synchronized keyword:
Synchronized method:

public synchronized void method() {
    // critical section
}

Synchronized block:

public void method() {
    synchronized(this) {
        // critical section
    }
}

14. What is the difference between synchronized method and synchronized block?

A synchronized method locks the whole object (or class for static methods).
A synchronized block allows you to lock only a specific section of code or a particular object, improving performance by reducing the scope of locking.

15. What is the difference between wait(), notify(), and notifyAll()?
wait(): Causes the current thread to wait until it is notified. It releases the lock.
notify(): Wakes up one waiting thread.
notifyAll(): Wakes up all threads waiting on the object's monitor.
All must be used inside synchronized blocks or methods.

16. Why should wait(), notify(), and notifyAll() be called inside a synchronized block?
    Because these methods are dependent on an object monitor, and only a thread holding the monitor (lock) can call them. Calling them outside a synchronized context causes IllegalMonitorStateException.

18. What is a deadlock? Can you give an example?
    A deadlock is a situation where two or more threads are waiting for each other to release resources, and none can proceed. It happens when four conditions hold: mutual exclusion, hold and wait, no preemption, and circular wait.

Example:

Thread-1 locks A, waits for B
Thread-2 locks B, waits for A

Both threads wait indefinitely, causing a deadlock.

18. How can you avoid deadlock?
Avoid nested locks (locking multiple resources)
Use a consistent lock ordering
Use tryLock() with timeout from ReentrantLock
Avoid holding locks during lengthy operations

19. What is a daemon thread?
A daemon thread is a background thread that runs continuously and supports other threads (e.g., garbage collector). It doesn't block the JVM from exiting.

Thread t = new Thread();
t.setDaemon(true);

20. What happens when the main thread exits but daemon threads are still running?
All daemon threads are terminated when all user (non-daemon) threads have finished. JVM exits automatically.

21. What is the difference between Callable and Runnable?
Runnable is an interface meant for tasks that do not return a result or throw checked exceptions. Callable is a more flexible interface that allows returning a result and throwing checked exceptions. It is part of java.util.concurrent package and is often used with ExecutorService.

Callable<Integer> task = () -> {
    return 123;
};

22. What is Future and how do you get the result from a thread?
A Future represents the result of an asynchronous computation. You get a Future when you submit a Callable to an ExecutorService. You can retrieve the result using get(), which blocks until the result is available.

ExecutorService executor = Executors.newSingleThreadExecutor();
Future<Integer> future = executor.submit(() -> 42);
Integer result = future.get(); // waits if necessary

23. What is the ExecutorService? How does it help manage threads?
ExecutorService is an interface that provides a framework for managing a pool of threads.
It abstracts away thread creation and lifecycle management.
It helps in reusing threads (thread pooling), scheduling tasks, and controlling execution policies.

Common implementations:

newFixedThreadPool(int n)

newSingleThreadExecutor()

newCachedThreadPool()

24. What is a thread pool? Why should we use it?
    A thread pool is a group of worker threads that are reused to execute tasks.
    Instead of creating a new thread for each task, threads are borrowed from the pool and returned after completion.
    This saves memory and improves performance by reducing thread creation overhead.

26. What is ThreadLocal in Java? When would you use it?
ThreadLocal provides thread-local variables.
Each thread accessing a ThreadLocal variable has its own, independently initialized copy.
It is useful in multi-threaded applications where you want to avoid synchronization.

Example use case: User sessions, database connections, formatting objects (like SimpleDateFormat).

ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);

26. What is the difference between ReentrantLock and synchronized?
synchronized is easier to use but less flexible.
ReentrantLock provides advanced features:

Try locking with timeout (tryLock())

Interruptible lock acquisition
Fair ordering policies
Explicit unlock required

ReentrantLock lock = new ReentrantLock();
lock.lock();
try {
    // critical section
} finally {
    lock.unlock();
}

27. Explain the volatile keyword. How is it different from synchronized?
volatile ensures that changes to a variable are always visible to all threads.
It prevents caching of the variable locally by threads. However, it does not ensure atomicity of compound actions (e.g., incrementing).

synchronized provides both visibility and atomicity but comes with performance overhead due to locking.

28. What is the Java Memory Model (JMM)?
JMM defines how threads interact through memory and what behaviors are allowed. It specifies rules for reads/writes of shared variables, visibility, and ordering. Without proper synchronization, the JVM is allowed to reorder instructions for performance, which may lead to unexpected results in multithreaded programs.

29. What are atomic operations? What is AtomicInteger?
Atomic operations are performed in a single step without interference from other threads.
Java provides classes in java.util.concurrent.atomic package for atomic operations.

AtomicInteger supports thread-safe, lock-free operations like increment, decrement, compare-and-set, etc.

AtomicInteger counter = new AtomicInteger();
counter.incrementAndGet();

30. Explain the concept of ForkJoinPool
ForkJoinPool is a special kind of thread pool designed for parallelism where tasks can be recursively split into smaller subtasks (fork) and their results combined (join). It uses the work-stealing algorithm where idle threads can "steal" tasks from busy threads to improve throughput.

Used primarily for divide-and-conquer algorithms (like merge sort, recursive calculations).

ForkJoinPool pool = new ForkJoinPool();
int result = pool.invoke(new MyRecursiveTask());

 1. What is the Java Collection Framework?
Answer:
The Java Collection Framework is a unified architecture for representing and manipulating collections (groups of objects). It includes:
Interfaces: List, Set, Queue, Map
Implementations: ArrayList, HashSet, LinkedList, HashMap, etc.
Algorithms: Sorting, searching, shuffling
Utility classes: Collections, Arrays

🔹 2. Difference between List, Set, and Map?
Feature	                                  List                          	Set                                       Map
Duplicates	                              Allowed	Not                     allowed	                                  Keys: No duplicates, Values: Allowed
Order	                                    Maintains order                	Unordered (except LinkedHashSet)        	Key-value pairs, unordered (HashMap)
Indexing                                	Supported	                      Not supported                            	Not applicable

🔹 3. What is the difference between ArrayList and LinkedList?
Feature                                  	ArrayList	                                        LinkedList
Storage type                            	Dynamic array	                                    Doubly linked list
Access time	                              Fast (O(1)) for get()	                            Slow (O(n)) for get()
Insertion/deletion	                      Slow (shifting required)                        	Fast (no shifting needed)
Memory usage                             	Less                                            	More (extra pointers)

🔹 4. What is the difference between HashSet and TreeSet?
Feature	                                      HashSet	                                          TreeSet
Order	                                        No ordering	                                      Sorted in natural/custom order
Performance	                                  Faster (O(1) for add, remove)                     Slower (O(log n))
Null element	                                Allows one null	                                  Does not allow null (in some cases)

🔹 5. How does HashMap work internally?
Answer:
HashMap stores key-value pairs using an array of buckets.
Each key is hashed (hashCode()), then modulus is applied to find the bucket.
If collisions occur (same hash), keys are stored in a linked list or balanced tree (Java 8+).
Retrieval checks equality using equals() after hash match.

🔹 6. What are the differences between HashMap and Hashtable?
Feature                                        	HashMap                                         	Hashtable
Thread-safe                                    	❌ No                                            	✅ Yes
Null key/value	                                1 null key, many null values	                    ❌ No null key or values
Performance	                                    Faster	                                           Slower (due to synchronization)
Introduced in	                                  Java 1.2 (part of Collections)	                   Java 1.0 (legacy)

🔹 7. What is the difference between Comparable and Comparator?
Feature	                                          Comparable	                                    Comparator
Package	                                          java.lang                                      	java.util
Method	                                          compareTo(Object o)	                            compare(Object o1, o2)
Modification	                                    Affects original class	                        Separate logic for sorting
Used for	                                        Natural sorting	                                Custom sorting

🔹 8. What is the difference between fail-fast and fail-safe iterators?
Feature	                      Fail-Fast                                                                        Fail-Safe
Behavior	                    Throws ConcurrentModificationException on structural modification                Works on a copy, no exception
Examples	                    ArrayList, HashMap                                                	             CopyOnWriteArrayList, ConcurrentHashMap

🔹 9. When to use LinkedHashMap vs TreeMap?
LinkedHashMap: Maintains insertion order.
TreeMap: Maintains sorted order (natural/custom).
Use LinkedHashMap for predictable iteration.
Use TreeMap when sorting keys is important.

🔹 10. What is the difference between Collection and Collections?
Term	                                        Collection                                            	Collections
Type	                                         Interface	                                            Utility class
Purpose	                                        Base interface for List, Set, etc.	                  Contains static utility methods
Example	                                        List extends Collection	                              Collections.sort(list)

🔹 11. Advanced: How does ConcurrentHashMap handle concurrency?
Answer:
In Java 8, ConcurrentHashMap uses bucket-level locking via synchronized blocks and CAS operations.
Buckets are segmented, and only one thread can update a segment at a time.
Read operations are mostly lock-free.

1. What is a Lambda Expression in Java?
Answer:
Lambda expressions, introduced in Java 8, provide a concise way to represent an anonymous function (a method without a name) that can be passed around. They enable functional programming features in Java and are used primarily to implement functional interfaces.
Syntax:
(parameters) -> expression
// or
(parameters) -> { statements }
Example:
Runnable r = () -> System.out.println("Running a thread");
2. What is the syntax of a Lambda Expression?
Answer:
Lambda expressions consist of three parts:
Argument list: (a, b) — similar to method parameters.
Arrow token: -> — separates the parameter list from the body.
Body: An expression or a block of code.
Examples:
(a, b) -> a + b                    // single expression
(String name) -> { return name.length(); }  // block
() -> System.out.println("Hello");         // no arguments
3. What are the advantages of using Lambda Expressions?
Answer:
Reduces boilerplate code.
Improves readability.
Enables functional-style operations on collections (e.g., map, filter).
Enables concise event handling and thread creation.
Useful with streams and functional interfaces.

4. Can lambda expressions access variables from the outer scope?
Answer:
Yes, they can access final or effectively final variables (i.e., variables not changed after initialization).
int factor = 2;
Function<Integer, Integer> multiply = x -> x * factor; // 'factor' must be effectively final
5. What is a functional interface, and how is it related to lambda expressions?
Answer:
A functional interface is an interface with only one abstract method. Lambda expressions are used to provide the implementation for the single abstract method.

@FunctionalInterface
interface Greeting {
    void sayHello();
}
Greeting g = () -> System.out.println("Hi!");

6. Can a lambda expression throw an exception?
Answer:
Yes, but it must be declared in the functional interface's method signature.

@FunctionalInterface
interface ThrowingFunction {
    void run() throws IOException;
}
ThrowingFunction tf = () -> { throw new IOException("IO Error"); };

7. What is the difference between an anonymous class and a lambda expression?
Feature                              	Anonymous Class	                                                           Lambda Expression
Syntax	                              Verbose	                                                                   Concise
this reference	                      Refers to anonymous class	                                                  Refers to enclosing class
Multiple methods	                    Can have multiple methods                                                	Only one abstract method (functional)
Use case	                            For complex implementations	                                              For simple functional interfaces

8. Can lambda expressions be serialized?
Answer:
Not directly. Lambda expressions do not implement Serializable by default. If needed, the target functional interface must extend Serializable.

9. What is the scope of this inside a lambda?
Answer:
In a lambda expression, this refers to the instance of the enclosing class — not the lambda itself. This differs from anonymous inner classes where this refers to the anonymous class instance.

10. Can a lambda expression implement multiple methods?
Answer:
No. A lambda expression can only implement a functional interface, which has exactly one abstract method.

 1. What are design patterns in Java?
Answer:
Design patterns are standard, reusable solutions to common software design problems. They represent best practices used by experienced developers to solve problems in a flexible and efficient way.
Java design patterns are classified into:
Creational (e.g., Singleton, Factory)
Structural (e.g., Adapter, Decorator)
Behavioral (e.g., Observer, Strategy)

🔷 2. What is the Singleton Pattern?
Answer:
The Singleton pattern ensures that a class has only one instance and provides a global access point to it.
Usage: Database connections, configuration settings, logging.
public class Singleton {
    private static final Singleton instance = new Singleton();
    private Singleton() {}
    public static Singleton getInstance() {
        return instance;
    }
}
Thread-safe Lazy Version:

public class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
🔷 3. What is the Factory Pattern?
Answer:
The Factory Pattern provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created.
Usage: GUI toolkits, frameworks, driver loaders.

interface Shape { void draw(); }

class Circle implements Shape {
    public void draw() { System.out.println("Circle"); }
}

class ShapeFactory {
    public Shape getShape(String type) {
        if ("circle".equals(type)) return new Circle();
        return null;
    }
}
🔷 4. What is the Builder Pattern?
Answer:
The Builder pattern separates the construction of a complex object from its representation so the same construction process can create different representations.
Usage: When object creation requires many parameters (e.g., StringBuilder, HttpClient).

class User {
    private String name, email;
    public static class Builder {
        private String name, email;
        public Builder setName(String name) { this.name = name; return this; }
        public Builder setEmail(String email) { this.email = email; return this; }
        public User build() { return new User(this); }
    }
    private User(Builder b) {
        this.name = b.name;
        this.email = b.email;
    }
}
🔷 5. What is the Prototype Pattern?
Answer:
It involves cloning existing objects instead of creating new ones, typically by using a prototype interface.
Usage: When object creation is costly (e.g., loading resources or database objects).

class Document implements Cloneable {
    String content;
    public Document clone() throws CloneNotSupportedException {
        return (Document) super.clone();
    }
}
🔷 6. What is the Adapter Pattern?
Answer:
The Adapter pattern allows incompatible classes to work together by converting the interface of one class into another.
Usage: Wrapping legacy classes or APIs.

class OldPrinter {
    void printOld(String msg) {
        System.out.println("Old: " + msg);
    }
}

interface NewPrinter {
    void print(String msg);
}

class Adapter implements NewPrinter {
    OldPrinter oldPrinter = new OldPrinter();
    public void print(String msg) {
        oldPrinter.printOld(msg);
    }
}
🔷 7. What is the Decorator Pattern?
Answer:
Decorator lets you dynamically add behaviors to objects by wrapping them.
Usage: Java I/O streams (BufferedInputStream wrapping FileInputStream).

interface Coffee {
    String getDescription();
}

class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple Coffee"; }
}

class MilkDecorator implements Coffee {
    private Coffee coffee;
    public MilkDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }
}
🔷 8. What is the Strategy Pattern?
Answer:
Strategy pattern allows selecting an algorithm at runtime by defining a family of algorithms, encapsulating each one, and making them interchangeable.
Usage: Sorting strategies, payment gateways.

interface PaymentStrategy {
    void pay(int amount);
}
class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) { System.out.println("Paid by card"); }
}
class PaymentService {
    private PaymentStrategy strategy;
    public PaymentService(PaymentStrategy strategy) {
        this.strategy = strategy;
    }
    public void pay(int amount) {
        strategy.pay(amount);
    }
}
🔷 9. What is the Observer Pattern?
Answer:
The Observer pattern defines a one-to-many dependency so when one object changes state, all its dependents are notified.
Usage: Event listeners, UI frameworks, pub-sub systems.

interface Observer {
    void update(String message);
}

class Subject {
    List<Observer> observers = new ArrayList<>();
    void subscribe(Observer o) { observers.add(o); }
    void notifyAll(String msg) {
        for (Observer o : observers) o.update(msg);
    }
}
🔷 10. What is the Template Method Pattern?
Answer:
Template Method defines the skeleton of an algorithm in a method, deferring some steps to subclasses.
Usage: HttpServlet's doGet() and doPost() in Java EE.

abstract class Game {
    final void play() {
        initialize();
        start();
        end();
    }
    abstract void initialize();
    abstract void start();
    abstract void end();
}

🔷 1. What is Serialization in Java?
Answer:
Serialization is the process of converting a Java object into a byte stream so that it can be saved to a file, transmitted over a network, or stored in memory.
It enables persistence and communication between Java programs.

Java provides this via:
ObjectOutputStream
Serializable interface (a marker interface, i.e., no methods)

🔷 2. What is Deserialization in Java?
Answer:
Deserialization is the reverse process of serialization—converting the byte stream back into a copy of the original object.

🔷 3. How do you make a Java class Serializable?
Answer:
Implement the java.io.Serializable interface:
import java.io.Serializable;

public class Student implements Serializable {
    private static final long serialVersionUID = 1L;  // version control
    private String name;
    private int age;

    // getters and setters
}
🔷 4. How do you serialize and deserialize an object in Java?
Serialization Example:
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("student.ser"));
Student student = new Student("John", 20);
oos.writeObject(student);
oos.close();

Deserialization Example:
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("student.ser"));
Student deserialized = (Student) ois.readObject();
ois.close();
🔷 5. What is serialVersionUID and why is it important?
Answer:
serialVersionUID is a unique identifier for Serializable classes. It ensures the sender and receiver of a serialized object have loaded classes that are compatible with respect to serialization.
If you don't declare it manually, JVM generates it dynamically based on class details, which can cause InvalidClassException during deserialization if the class structure changes.

🔷 6. What happens if a class does not implement Serializable but you try to serialize it?
Answer:
Java will throw a NotSerializableException.

🔷 7. What is a transient keyword?
Answer:
transient is used to exclude a field from serialization.
private transient String password; // will not be serialized
🔷 8. Can a static variable be serialized?
Answer:
No, static fields belong to the class, not to any instance. Since serialization is instance-based, static fields are not serialized.

🔷 9. Can you customize the serialization process?
Answer:
Yes, by providing custom methods in your class:
private void writeObject(ObjectOutputStream oos) throws IOException {
    oos.defaultWriteObject();
    oos.writeObject("Encrypted_" + password);
}

private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
    ois.defaultReadObject();
    this.password = ((String) ois.readObject()).replace("Encrypted_", "");
}
🔷 10. What is Externalizable interface?
Answer:
Externalizable is an alternative to Serializable that allows complete control over serialization by implementing two methods:
writeExternal(ObjectOutput out)
readExternal(ObjectInput in)
You must implement both methods and explicitly handle each field.
public class User implements Externalizable {
    private String name;
    private int age;

    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(name);
        out.writeInt(age);
    }

    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = (String) in.readObject();
        age = in.readInt();
    }
}
🔷 11. Can you serialize an object that has a reference to a non-serializable class?
Answer:
No. If any field in a serializable object refers to a non-serializable object, serialization will fail with NotSerializableException.

To handle it:
Mark the field as transient, or
Make the referenced class serializable too

🔷 12. What are some real-world use cases of serialization?
Answer:
Saving session state in web applications
Caching objects
Sending objects over a network (e.g., RMI, socket programming)
Deep cloning (as an alternative to copy constructors)

1. What is the JVM memory structure? Describe its components.
The JVM divides memory into several runtime areas:
Heap: Stores objects and class instances.
Stack: Stores method calls and local variables.
Method Area (MetaSpace in Java 8+): Stores class metadata.
Program Counter (PC) Register: Indicates current instruction of each thread.
Native Method Stack: Used for native (non-Java) methods.

2. What is the heap and how is it divided?
Heap is the runtime area from which memory is allocated for class instances and arrays. It is divided into:
Young Generation: Where new objects are created. Subdivided into Eden and Survivor spaces.
Old (Tenured) Generation: Stores long-living objects.
MetaSpace: Stores class metadata (replaced PermGen in Java 8).

3. Explain how Garbage Collection works in Java.
Garbage Collection (GC) is the process of automatically identifying and removing objects that are no longer used to free up memory. Java uses various GC algorithms:
Serial GC: Single-threaded.
Parallel GC: Multi-threaded, good for throughput.
CMS (Concurrent Mark Sweep): Minimizes pauses.
G1 GC: Divides heap into regions, balances throughput and latency.
ZGC/Shenandoah: Low-latency collectors (Java 11+).

4. What is the difference between finalize() and garbage collection?
finalize() is a method that gets called before an object is collected, allowing cleanup.
GC is automatic and manages memory cleanup, but relying on finalize() is discouraged due to unpredictability and performance issues.

5. What is a memory leak in Java? How can you detect it?
A memory leak happens when objects are no longer used but still referenced, preventing GC. This can lead to OutOfMemoryError.
Detection tools:
VisualVM
JProfiler
Eclipse MAT (Memory Analyzer Tool)

6. What is the OutOfMemoryError? How do you handle it?
This error occurs when the JVM cannot allocate more memory. Causes:
Memory leak
Large object creation
Insufficient heap size
To handle:
Analyze memory usage
Use heap dumps
Tune JVM memory settings

7. How do you tune JVM memory parameters?
Use JVM options:
-Xms<size>: Initial heap size
-Xmx<size>: Maximum heap size
-XX:NewSize and -XX:MaxNewSize: Young generation
-XX:+UseG1GC: Use G1 GC

8. What is SoftReference, WeakReference, and PhantomReference?
These classes in java.lang.ref provide levels of reference strength:
SoftReference: Collected only when memory is low (caching).
WeakReference: Collected more aggressively (used in maps).
PhantomReference: Used for post-mortem cleanup; collected after finalization.

9. Can you force garbage collection? Should you?
You can suggest it using System.gc(), but it’s not guaranteed to run immediately. Forcing GC is generally discouraged because it can affect performance.

10. What are some best practices to avoid memory issues?
Avoid unnecessary object references (nullify them if needed).
Use collections wisely (beware of large maps/lists).
Use profiling tools to monitor heap.
Prefer try-with-resources for managing I/O and DB connections.

1. What is the difference between checked and unchecked exceptions?

Checked Exceptions are exceptions that are checked at compile-time. If a method can throw a checked exception, it must either handle it using a try-catch block or declare it using the throws keyword in the method signature. Examples include IOException, SQLException, etc.

Unchecked Exceptions, on the other hand, are not checked at compile-time. These are subclasses of RuntimeException, and handling them is optional. Common unchecked exceptions include NullPointerException, ArithmeticException, and ArrayIndexOutOfBoundsException.

2. What is the base class for all exceptions in Java?

The base class for all exceptions is Throwable. It has two main subclasses:
Error: Represents serious problems that applications should not try to catch, such as OutOfMemoryError.
Exception: Represents conditions that a program might want to catch.

3. What is the purpose of the finally block?
The finally block provides a mechanism to clean up resources, such as file streams, database connections, etc., regardless of whether an exception occurs or not. Code inside finally will always execute after the try and catch blocks, even if an exception is thrown or a return statement is encountered.

try {
    // risky code
} catch (Exception e) {
    // handle exception
} finally {
    // cleanup code
}

4. What happens if an exception is thrown in the finally block?
If an exception occurs in the finally block, it can override or suppress exceptions thrown in the try or catch blocks. This can lead to confusion if not handled carefully. It's a good practice to avoid writing code in finally that can throw new exceptions unless properly managed.

5. What is try-with-resources? How is it useful?
Introduced in Java 7, try-with-resources is used to automatically close resources that implement the AutoCloseable interface (like streams, readers, database connections). It ensures that resources are closed properly even if an exception occurs.

try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // read file
}

No need to explicitly close the BufferedReader; it’s done automatically.

6. What is the difference between throw and throws?
throw is used to explicitly throw an exception.
throws is used in a method declaration to indicate that the method may throw one or more exceptions.

void readFile() throws IOException {
    throw new IOException("File not found");
}

7. Can we have multiple catch blocks for a single try?
Yes, Java allows multiple catch blocks to handle different types of exceptions separately. Each block handles a specific type, and only one catch block is executed — the first one matching the exception type.

try {
    // code
} catch (IOException e) {
    // handle IO issues
} catch (Exception e) {
    // handle other issues
}

8. Can we catch multiple exceptions in a single catch block?
Yes, Java 7 introduced multi-catch, allowing multiple exception types to be handled in a single catch block using the | (pipe) symbol.

try {
    // code
} catch (IOException | SQLException e) {
    // handle both exceptions
}

This simplifies code when different exceptions are handled in the same way.

9. What is exception chaining?
Exception chaining is wrapping one exception inside another. This helps to preserve the original cause when catching and rethrowing an exception. It’s useful for debugging the root cause of a problem.

try {
    throw new IOException("Low-level IO issue");
} catch (IOException e) {
    throw new RuntimeException("High-level app failure", e);
}

10. Can we override a method and throw a different exception?
Yes, but with restrictions:
The overriding method can throw the same exceptions or their subclasses (for checked exceptions).

It can throw unchecked exceptions freely.

class Parent {
    void readFile() throws IOException {}
}

class Child extends Parent {
    void readFile() throws FileNotFoundException {} // Valid
}

11. What is the use of custom exceptions?
Custom exceptions allow you to create application-specific error types that make your code more readable and organized.

class UserNotFoundException extends Exception {
    public UserNotFoundException(String msg) {
        super(msg);
    }
}

// Usage
throw new UserNotFoundException("User with ID 123 not found");
This makes it easier to identify specific errors in logs or handle them differently.

12. What is the difference between Error and Exception?
Error represents serious problems, typically related to the JVM (like OutOfMemoryError), and should not be caught in application code.
Exception represents issues that application code can potentially handle (like FileNotFoundException).
Catching Error is considered bad practice.

13. What is the StackTrace? How is it useful?
A stack trace shows the method call hierarchy leading up to an exception. It helps pinpoint where the error occurred in the code.

try {
    int a = 5 / 0;
} catch (ArithmeticException e) {
    e.printStackTrace();
}
The output tells you the exact line number and method where the error occurred.

14. What are some best practices for exception handling?
Catch specific exceptions: Avoid using a generic Exception unless necessary.
Don't suppress exceptions: Don’t use empty catch blocks.
Clean up resources: Always use finally or try-with-resources.
Avoid using exceptions for flow control: Use conditionals instead.
Log exceptions: Ensure stack traces and messages are logged
Create custom exceptions: For domain-specific scenarios.

 1. What is JDBC?
Answer:
JDBC (Java Database Connectivity) is an API that enables Java applications to interact with relational databases using SQL queries. It provides a set of interfaces and classes to connect, query, and update a database.

🔹 2. What are the main components of JDBC?
Answer:
DriverManager – Manages JDBC drivers.
Connection – Establishes a session with the database.
Statement / PreparedStatement / CallableStatement – Executes SQL queries.
ResultSet – Represents the result of a query.
SQLException – Handles database-related exceptions.

🔹 3. How do you connect to a database using JDBC?
Answer:
Class.forName("com.mysql.cj.jdbc.Driver"); // Load driver (optional for JDBC 4+)
Connection conn = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/mydb", "username", "password");
    
🔹 4. What is the difference between Statement and PreparedStatement?
Feature                        	Statement                                                	PreparedStatement
SQL                            	Sent as a plain string                                  	Precompiled SQL with placeholders (?)
Performance	                    Recompiled every time	                                    Better for repeated execution
Security	                      Prone to SQL injection	                                  Helps prevent SQL injection
Example	                        "SELECT * FROM users WHERE id=" + userId	                "SELECT * FROM users WHERE id=?"

🔹 5. What is a ResultSet?
Answer:
A ResultSet is an object returned by executing a SQL query. It represents a table of data and supports cursor movement across rows.
Common methods:
next() – moves to next row
getString("column"), getInt(1) – fetch column data
wasNull() – checks if the last value was SQL NULL

🔹 6. What are the different types of ResultSet?
Answer:

Type:
TYPE_FORWARD_ONLY (default)
TYPE_SCROLL_INSENSITIVE
TYPE_SCROLL_SENSITIVE
Concurrency:
CONCUR_READ_ONLY
CONCUR_UPDATABLE
Statement stmt = conn.createStatement(
  ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY);
  
🔹 7. What is the difference between execute(), executeQuery(), and executeUpdate()?
Method                    	Use	                                  Returns
execute()	                  Any                                   SQL	boolean (true if ResultSet returned)
executeQuery()	            SELECT	                              ResultSet
executeUpdate()	            INSERT/UPDATE/DELETE	                int (rows affected)

🔹 8. What is a CallableStatement?
Answer:
CallableStatement is used to execute stored procedures in the database.
CallableStatement cs = conn.prepareCall("{call getEmployee(?)}");
cs.setInt(1, 1001);
ResultSet rs = cs.executeQuery();

🔹 9. What are JDBC Drivers?
Answer:
Types of JDBC Drivers:
Type 1 – JDBC-ODBC Bridge
Type 2 – Native API Driver
Type 3 – Network Protocol Driver
Type 4 – Thin Driver (Pure Java; widely used)
Most modern applications use Type 4 drivers (e.g., MySQL, PostgreSQL, Oracle).

🔹 10. How do you prevent SQL Injection in JDBC?
Answer:
SQL Injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database.
Use PreparedStatements instead of concatenating SQL strings manually.
PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
ps.setInt(1, 10);
ResultSet rs = ps.executeQuery();

🔹 11. How to handle transactions in JDBC?
Answer:
conn.setAutoCommit(false);
try {
    ps1.executeUpdate();
    ps2.executeUpdate();
    conn.commit();
} catch (Exception e) {
    conn.rollback();
}
setAutoCommit(false) disables auto-commit.

Use commit() to persist and rollback() to undo.

🔹 12. How do you close JDBC resources properly?
Answer:
Always close in finally block or use try-with-resources:
try (Connection conn = DriverManager.getConnection(...);
     PreparedStatement ps = conn.prepareStatement(...);
     ResultSet rs = ps.executeQuery()) {
    // process results
}
🔹 13. What are some common JDBC exceptions?
Answer:
SQLException – generic DB error
SQLIntegrityConstraintViolationException – constraint violation
SQLSyntaxErrorException – invalid SQL

🔹 14. What is connection pooling in JDBC?
Answer:
Connection pooling means reusing database connections instead of creating a new one every time.
Frameworks like HikariCP, Apache DBCP, and C3P0 manage pooling and increase performance.

🔹 15. How can you improve JDBC performance?
Use PreparedStatements.
Batch insert/update (addBatch(), executeBatch()).
Use connection pooling.
Fetch only required columns.
Use efficient ResultSet types.











