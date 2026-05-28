# Part 1: Foundations – Classes, Objects & Memory

  - [🟢 1. What is a Class in Java?](#-1-what-is-a-class-in-java)
  - [🔵 2. What is an Object in Java?](#-2-what-is-an-object-in-java)
  - [🔴 3. How to Create an Object in Java](#-3-how-to-create-an-object-in-java)
  - [🔴 4. JVM-Level Memory Understanding](#-4-jvm-level-memory-understanding)

---
# Part 2: Object Initialization & Core Keywords
  - [🔵 5. Constructor in Java](#-5-constructor-in-java)
  - [🟢 6. Important Points About Constructors](#-6-important-points-about-constructors)
  - [🟠 7. The this Keyword](#-7-the-this-keyword)
  - [🔵 8. Constructor Chaining](#-8-constructor-chaining-in-java--understanding-object-initialization-flow)
  - [🔵 9. The super Keyword](#-9---understanding-super-in-java--a-beginner-friendly-deep-dive)
---
# Part 3: Core OOP Pillar – Encapsulation
  - [🔴 10. Encapsulation in Java](#-10---encapsulation-in-java--data-hiding--controlled-access)
  - [🔵 11. Access Modifiers in Java](#-11---access-modifiers-in-java--controlling-visibility-encapsulation--inheritance)
---


## 🟢 1. What is a Class in Java?

A **class** is a **blueprint or template** from which objects are created. It defines **properties** (attributes or fields) and **behaviors** (methods) common to all objects of that type. Classes themselves are not objects—they are more like **plans** or **recipes**.

Imagine a bakery. The **recipe for a cake** is the class: it specifies the ingredients (state) and the steps to bake the cake (behavior). Using this recipe, the bakery can bake multiple cakes, each cake being an **object**. Each cake can have its own flavor, number of layers, or type of icing, but all share the same methods like `bake()` or `decorate()`.

```java
class Cake {
    String flavor;
    String icing;
    int layers;

    void bake() { System.out.println("Baking the cake"); }
    void decorate() { System.out.println("Decorating the cake"); }
}

public class Main {
    public static void main(String[] args) {
        Cake myCake = new Cake();
        myCake.flavor = "Chocolate";
        myCake.icing = "Vanilla";
        myCake.layers = 3;

        System.out.println(myCake.flavor);
        System.out.println(myCake.icing);
        System.out.println(myCake.layers);

        myCake.bake();
        myCake.decorate();
    }
}
```

Here, `Cake` is a class (the blueprint), and `myCake` is an object created from it.

---

## 🔵 2. What is an Object in Java?

In Java, an **object** is a real-world entity or instance of a class. Every object has **state** and **behavior**, where the state is represented by variables (also called fields) and the behavior is represented by methods. Objects are like individual “things” in the real world that have characteristics and actions.

For example, consider a car manufacturing unit. The **blueprint or design** of a car is like a Java class. Using this blueprint, the factory can produce multiple cars. Each car produced is a **distinct object** with its own color, model, and engine type. Though all cars are made from the same blueprint, each car object can have **different values** for these properties.

```java
class Car {
    String color;
    String model;
    int year;

    void start() { System.out.println("Car started"); }
    void stop() { System.out.println("Car stopped"); }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.color = "Red";
        myCar.model = "Sedan";
        myCar.year = 2024;

        System.out.println(myCar.color);
        System.out.println(myCar.model);
        System.out.println(myCar.year);

        myCar.start();
        myCar.stop();
    }
}
```
Here, `myCar` is an **object** of the `Car` class. It has its own state (`color`, `model`, `year`) and can perform actions (`start()`, `stop()`).

---
## 🔴 3. How to Create an Object in Java

- Objects are created from classes using the `new` keyword, which **allocates memory** in the heap for the object and calls a **constructor** to initialize it. 
- Each object has its own memory space for storing its state, but methods are shared (since they are defined in the class).

```java
Cake birthdayCake = new Cake();
birthdayCake.flavor = "Strawberry";
birthdayCake.icing = "Chocolate";
birthdayCake.layers = 2;
birthdayCake.bake();
birthdayCake.decorate();
```

Even if we create multiple `Cake` objects, each one has **its own state**, but all use the same methods defined in the class. Think of it like baking multiple cakes from the same recipe: each cake can have a different flavor but follows the same steps to bake.

---
## 🔴 4. JVM-Level Memory Understanding

* When we create an object using `new`, **memory is allocated in the Heap**.
* **Stack memory** stores the **reference variable** pointing to the object.
* Each object has its **own copy of instance variables**, while **methods are shared**.

```
Stack               Heap
┌─────────┐         ┌───────────────┐
│ myCake  │ ──────▶ │ Cake Object   │
└─────────┘         │ flavor="Vanilla"│
                    │ layers=3       │
                    └───────────────┘
```
---
## 🔵 **5. Constructor in Java**

A **constructor** is a **special method** used to initialize objects. It has the same name as the class, **no return type**, and is called automatically when a new object is created.

```java
class Cake {
    String flavor;

    // Constructor
    Cake(String flavor) {
        this.flavor = flavor;
    }

    void printFlavor() {
        System.out.println("Flavor: " + flavor);
    }
}

public class Main {
    public static void main(String[] args) {
        Cake myCake = new Cake("Chocolate"); // constructor called
        myCake.printFlavor();
    }
}
```

* Constructors can be **overloaded**, meaning you can define multiple constructors with **different parameters** to allow different ways of initializing objects.
* You can also use **copy constructors** to create a new object that is a copy of an existing object.
* Within a class, one constructor can call another using `this()`, a process called **constructor chaining**.

---

## 🟢 **6. Important Points About Constructors**

1. Constructors **do not have a return type**, not even `void`.
2. A constructor is called automatically when an object is created.
3. Overloaded constructors allow multiple ways to initialize an object.
4. Copy constructors create a **new object that is identical** to an existing object.
5. `this()` can call another constructor in the same class, avoiding code repetition.

```java
class IceCream {
    String flavor;
    String size;

    IceCream(String flavor) { // default size
        this.flavor = flavor;
        this.size = "Medium";
    }

    IceCream(String flavor, String size) { // overloaded constructor
        this(flavor); // call first constructor
        this.size = size;
    }
}
```

---
## 🟠 **7. The `this` Keyword**

In Java, `this` is a **reference variable** that points to the **current object**. It is useful when:

* You need to differentiate between instance variables and method/constructor parameters with the same name.
* You want to call other methods or return the current object.

**Analogy:** If you are reading a book in a library full of books, you would say “mark the page in **this book**” rather than in some other book. Similarly, `this` refers to **the current object**.

```java
class Cake {
    String flavor;

    Cake(String flavor) {
        this.flavor = flavor; // differentiates instance variable and parameter
    }

    void printFlavor() {
        System.out.println("Flavor: " + this.flavor);
    }
}

public class Main {
    public static void main(String[] args) {
        Cake myCake = new Cake("Vanilla");
        myCake.printFlavor();
    }
}
```

Here, `this.flavor` refers to the **object’s field**, while `flavor` alone refers to the **parameter** passed to the constructor.

---
## 🔵 **8. Constructor Chaining in Java – Understanding Object Initialization Flow**

Constructor chaining is a concept in Java where **one constructor calls another constructor**, either within the same class or from its parent class. This is done to **reuse code, avoid duplication, and ensure proper object initialization**.

When an object is created, Java does not just call one constructor randomly. Instead, it follows a **chain of constructor calls**, starting from the top of the inheritance hierarchy down to the current class. This process ensures that every part of the object is initialized correctly.

Constructor chaining mainly happens using two keywords:

* `this()` → calls another constructor in the same class
* `super()` → calls the constructor of the parent class

---

### 🟣 **8.1 - Using `this()` – Calling Constructor Within Same Class**

The `this()` keyword is used to call another constructor **within the same class**. This is useful when you have multiple constructors and want to reuse initialization logic instead of writing duplicate code.

Let’s understand this with an example:

```java
class Student {
    int id;
    String name;

    // Default constructor
    Student() {
        this(101, "Default"); // calling parameterized constructor
        System.out.println("Default constructor called");
    }

    // Parameterized constructor
    Student(int id, String name) {
        this.id = id;
        this.name = name;
        System.out.println("Parameterized constructor called");
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
    }
}
```

When this program runs, the output will be:

```
Parameterized constructor called
Default constructor called
```

Here, the default constructor calls the parameterized constructor using `this()`. This avoids repeating initialization logic and keeps the code clean.

👉 Important rule:
`this()` must always be the **first statement** inside a constructor.

---
### 🟢  8.2 - Using `super()` – Calling Parent Class Constructor**

The `super()` keyword is used to call the constructor of the **parent class**. This is important in inheritance because the parent class must be initialized before the child class.

Let’s see an example:

```java
class Person {
    Person() {
        System.out.println("Person constructor called");
    }
}

class Student extends Person {
    Student() {
        super(); // calling parent constructor
        System.out.println("Student constructor called");
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
    }
}
```

Output:

```
Person constructor called
Student constructor called
```

Here, when a `Student` object is created, the JVM first calls the `Person` constructor using `super()`, and then executes the `Student` constructor.

👉 Important point:
Even if you don’t write `super()`, Java automatically adds it as the first line.

---

### 🟡 8.3 - Combining `this()` and `super()` – Execution Flow**

You cannot use both `this()` and `super()` in the same constructor because **both must be the first statement**. However, they can still work together indirectly through chaining.

Example:

```java
class Person {
    Person() {
        System.out.println("Person constructor");
    }
}

class Student extends Person {

    Student() {
        this(101); // calls another constructor
        System.out.println("Default Student constructor");
    }

    Student(int id) {
        super(); // calls parent constructor
        System.out.println("Parameterized Student constructor: " + id);
    }
}
```

Output:

```
Person constructor
Parameterized Student constructor: 101
Default Student constructor
```

Here’s what happens internally:

1. `Student()` calls `this(101)`
2. `Student(int id)` calls `super()`
3. Parent constructor executes
4. Then child constructors execute in order

This shows how constructor chaining flows across classes.

---

### 🔴 8.4 - Key Rules You Must Remember (Very Important)**

Constructor chaining follows strict rules in Java:

* `this()` calls constructor of the same class
* `super()` calls constructor of parent class
* Both must be the **first statement** in constructor
* You cannot use both in the same constructor directly
* If not written, `super()` is added automatically

---

### 🔵 8.5 Real-World Understanding**

Think of constructor chaining like **building a house step by step**:

* Parent class → Foundation 🏗️
* Child class → Structure 🏠
* Final object → Complete house

You cannot build walls without laying the foundation first. That’s why `super()` is executed before child constructor logic.

Similarly, `this()` helps reuse internal construction steps within the same class.

---
## 🔵 9 - Understanding `super` in Java – A Beginner-Friendly Deep Dive

In Java, the keyword **`super`** is a **reference variable** that is used to refer to the **immediate parent class object**. It becomes relevant only when **inheritance (IS-A relationship)** is involved. Whenever a class extends another class, Java maintains an internal connection between the child and the parent, and `super` is how the child class talks to its parent.

Think of `super` as saying:
👉 *“I want something from my parent class, not from myself.”*

This is especially important when the child class **overrides** variables, methods, or constructors of the parent class.

---

### 🟢 9.1 - Why Do We Need `super`?

When a child class inherits from a parent class, it automatically gets access to its methods and variables. However, problems arise when the **child class defines members with the same name** as the parent. In such cases, Java gives priority to the **child class**. The `super` keyword allows us to explicitly access the **parent version**.

So, `super` is mainly used in three situations:

1. To access **parent class variables**
2. To call **parent class methods**
3. To invoke **parent class constructors**

We’ll explore each one in detail with examples and diagrams.

---

### 🟣 9.2 - Using `super` to Access Parent Class Variables**

When a child class declares a variable with the **same name** as a variable in the parent class, the parent variable becomes hidden. Java resolves this conflict by letting us use `super.variableName`.

---

### 🧠 **Example: Variable Hiding**

```java
class Animal {
    String color = "White";
}

class Dog extends Animal {
    String color = "Black";

    void displayColor() {
        System.out.println("Dog color: " + color);
        System.out.println("Animal color: " + super.color);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.displayColor();
    }
}
```

Here, both `Animal` and `Dog` have a variable named `color`.

* `color` refers to the **child class variable**
* `super.color` refers to the **parent class variable**

---

### 🧩 **Variable Access Flow Diagram**

```
Dog object
   |
   |-- color (Black)  ← accessed by default
   |
   |-- super.color (White) ← explicitly accessed
```

---

### 🟠 9.3 Using `super` to Call Parent Class Methods

When a child class **overrides** a method from the parent class, the child’s version is executed by default. If we want to call the parent’s version as well, we use `super.methodName()`.

---

### 🧠 **Example: Method Overriding**

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        super.sound(); // parent method
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();
    }
}
```

In this example, the `Dog` class overrides the `sound()` method.
Using `super.sound()` ensures that the **parent behavior is preserved** before adding child-specific behavior.

---

### 🧩 **Method Call Flow Diagram**

```
Dog.sound()
   |
   |-- super.sound()
   |       |
   |       --> Animal.sound()
   |
   --> Dog-specific sound
```

---

### 🔴 9.4 - Using `super` to Call Parent Class Constructors

One of the **most important uses** of `super` is calling the **parent class constructor**. When an object of a child class is created, Java **always constructs the parent class first**, then the child class.

If we don’t explicitly write `super()`, Java automatically inserts a **no-argument parent constructor**.

---

### 🧠 **Example: Constructor Chaining**

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor called");
    }
}

class Dog extends Animal {
    Dog() {
        super(); // calls Animal constructor
        System.out.println("Dog constructor called");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
    }
}
```

---

### 🧩 **Constructor Execution Flow**

```
Dog object creation
        |
        |-- Animal constructor
        |
        |-- Dog constructor
```

---

### 🟣 **Parameterized Constructor with `super`**

If the parent class has a **parameterized constructor**, the child **must** call it explicitly.

```java
class Animal {
    Animal(String type) {
        System.out.println("Animal type: " + type);
    }
}

class Dog extends Animal {
    Dog() {
        super("Mammal");
        System.out.println("Dog constructor");
    }
}
```

Without `super("Mammal")`, the code would **not compile**.

---

### 🟢 9.5 - Rules and Important Points About `super`

The `super()` constructor call **must be the first statement** inside a constructor. Java enforces this rule because the parent must be fully initialized before the child.

The `super` keyword **cannot be used inside a static context** because static members belong to the class, not to an object.

`super` always refers to the **immediate parent**, not to grandparents directly.

---

### 🔵 9.6 - Real-World Analogy for Better Understanding

Imagine a **Company** and an **Employee**.

* The company has general rules
* The employee follows those rules but may have extra responsibilities

When the employee refers to company policies, that’s like using `super`.

```
Company (Parent)
    ↑
Employee (Child)
```

The employee can say:
👉 “Follow company rule” → `super.rule()`

---

### 🧠 9.7 - `super` vs `this` (Quick Conceptual Contrast)

Even though both are reference variables:

* `this` refers to the **current class object**
* `super` refers to the **parent class object**

They help Java resolve **ambiguity** in inheritance scenarios.

---

### 🟣 9.8 - Complete Flow Diagram of `super` Usage

```
        Parent Class
        -------------
        variables
        methods
        constructors
              ↑
              | super
              |
        Child Class
        ------------
        variables
        methods
        constructors
```
---
# 🔴 10 - Encapsulation in Java – Data Hiding & Controlled Access

Encapsulation is one of the most fundamental concepts in Java and a core pillar of Object-Oriented Programming. It refers to the idea of **wrapping data (variables) and methods (functions) together into a single unit**, which is typically a class. More importantly, encapsulation focuses on **data hiding**, meaning the internal state of an object is not directly accessible from outside the class. Instead, access is controlled through well-defined methods.

In simple terms, encapsulation is like a capsule where the internal details are hidden, and only necessary parts are exposed. This helps in protecting the data from unwanted modification and ensures that it is accessed in a controlled and safe manner.

---

### 🟣 10.1 - How Encapsulation Works – Private Fields & Public Methods**

In Java, encapsulation is achieved by declaring class variables as **private** and providing access to them through **public getter and setter methods**. By making variables private, we restrict direct access from outside the class, and by using getters and setters, we control how the data is read and modified.

Let’s understand this with a simple example:

```java
class Student {

    // Private variables (data hiding)
    private int id;
    private String name;

    // Getter method (read access)
    public int getId() {
        return id;
    }

    // Setter method (write access)
    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();

        // Setting values using setters
        s.setId(101);
        s.setName("Rabbani");

        // Getting values using getters
        System.out.println(s.getId());
        System.out.println(s.getName());
    }
}
```

In this example, the variables `id` and `name` are not directly accessible from outside the class because they are private. Instead, we use `setId()` and `setName()` to assign values, and `getId()` and `getName()` to retrieve them. This ensures that all access to the data is controlled.

---

### 🟢 10.2 - Why Encapsulation is Important – Real Understanding

Encapsulation is important because it provides **control, security, and flexibility** in your code. When you hide the internal data and expose only what is necessary, you reduce the chances of accidental or invalid modifications.

For example, imagine you have a bank account class. You would never want someone to directly change the balance variable. Instead, you would provide methods like `deposit()` and `withdraw()` that validate the operation before updating the balance. This is exactly what encapsulation enables.

Let’s see a slightly improved example:

```java
class BankAccount {

    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Here, the `balance` variable is protected. You cannot directly modify it from outside. Instead, all changes go through controlled methods that ensure valid operations. This prevents errors like negative balances or invalid transactions.

Encapsulation also makes your code more maintainable. If you later decide to change how data is stored or validated, you only need to modify the internal implementation of the class without affecting other parts of the program. This improves flexibility and reduces dependencies.

Another key advantage is **data integrity**. Since all updates go through controlled methods, you can enforce rules and constraints, ensuring that the object always remains in a valid state.

---

Encapsulation is not just about using getters and setters—it is about designing your classes in such a way that **data is protected, behavior is controlled, and the internal implementation is hidden from the outside world**. This concept forms the foundation for building secure, maintainable, and scalable Java applications.

---
# 🔵 11 - Access Modifiers in Java – Controlling Visibility (Encapsulation + Inheritance)

Access modifiers in Java define **where a class, method, or variable can be accessed from**. They are extremely important because they help enforce **encapsulation (data hiding)** and also control how members behave in **inheritance**.

In simple terms, access modifiers decide **who can see and use your code**. By using the right modifier, you can protect your data, expose only what is necessary, and design your classes in a clean and secure way.

Java provides four types of access modifiers:

* `private`
* `default` (no keyword)
* `protected`
* `public`

Each of these has a different level of visibility.

---

### 🟣 11.1 - `private` – Accessible Only Within Same Class

The `private` access modifier provides the **highest level of restriction**. A private member can only be accessed **within the same class**. It cannot be accessed outside the class, even by subclasses.

This is mainly used for **data hiding**, which is a core part of encapsulation.

```java
class Person {
    private int age;

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();

        // p.age ❌ not accessible directly
        p.setAge(25);
        System.out.println(p.getAge());
    }
}
```

Here, `age` is private, so it cannot be accessed directly. We use getter and setter methods to control access. Even if another class extends `Person`, it still cannot access `age` directly.

👉 In inheritance:

* Not accessible in subclass ❌
* Only accessible through methods ✔️

---

### 🟢 11.2 - `default` – Accessible Within Same Package

If you don’t specify any modifier, Java uses the **default access modifier** (also called package-private). Members with default access can be accessed **only within the same package**.

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}
```

If another class is in the same package, it can access this method. But if it is in a different package, it cannot.

👉 In inheritance:

* Same package subclass → accessible ✔️
* Different package subclass → not accessible ❌

---

### 🟡 11.3 - `protected` – Accessible in Same Package + Subclasses**

The `protected` modifier is slightly less restrictive than default. It allows access:

* Within the same package
* In subclasses (even if they are in different packages)

```java
class Animal {
    protected void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void display() {
        sound(); // accessible
    }
}
```

Here, the `Dog` class can access the protected method because it is a subclass.

👉 In inheritance:

* Same package → accessible ✔️
* Different package subclass → accessible ✔️
* Non-subclass (different package) → not accessible ❌

---

### 🔴 11.4 - `public` – Accessible Everywhere

The `public` modifier provides the **least restriction**. Public members can be accessed from anywhere in the program, regardless of package or inheritance.

```java
class Animal {
    public void sound() {
        System.out.println("Animal sound");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Animal();
        a.sound(); // accessible everywhere
    }
}
```

👉 In inheritance:

* Accessible everywhere ✔️

---

### 🔵 11.5 - Access Modifiers with Inheritance – Clear Understanding

Let’s combine everything to understand how access modifiers behave in inheritance:

```java
class Parent {
    private int a = 10;
    int b = 20;           // default
    protected int c = 30;
    public int d = 40;
}

class Child extends Parent {
    void display() {
        // System.out.println(a); ❌ not accessible
        System.out.println(b); // depends on package
        System.out.println(c); // accessible
        System.out.println(d); // accessible
    }
}
```

Here’s what happens:

* `private` → not inherited directly
* `default` → only works if same package
* `protected` → works in subclass
* `public` → always accessible

---

### 🟣 11.6 - Real-World Understanding

Think of access modifiers like **security levels in an organization**:

* `private` → Personal locker 🔒
* `default` → Team access 👥
* `protected` → Team + special members (subclasses) 🛡️
* `public` → Open to everyone 🌍

Each level controls how much access others have.

---

### 🟢 11.7 - Why Access Modifiers Are Important

Access modifiers are crucial because they help you:

* Protect sensitive data (Encapsulation)
* Control visibility of methods and variables
* Design clean APIs
* Prevent misuse of code
* Support inheritance safely

In real-world applications, especially large systems, proper use of access modifiers ensures that your code is **secure, maintainable, and scalable**.

---
