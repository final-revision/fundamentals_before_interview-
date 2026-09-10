# OOP Concepts — Fresher Interview Questions & Answers

A practical interview-preparation guide covering **Object-Oriented Programming (OOP)** from basic concepts to tricky and scenario-based questions.

> **Important:** OOP examples use Java-style syntax because Java is commonly used in fresher interviews. The concepts also apply to languages such as C++, C#, Python, and others, although some features differ between languages.

---

# 1. OOP Basics

### Q1. What is OOP?

**Answer:** OOP stands for Object-Oriented Programming. It is a programming paradigm that organizes software around **objects**, which contain data and behavior.

**Example:** A `Car` object can have data such as `color` and `speed`, and behavior such as `start()` and `stop()`.

---

### Q2. What are the main principles of OOP?

The four major principles are:

1. **Encapsulation** — wrapping data and methods together and controlling access.
2. **Abstraction** — hiding unnecessary implementation details.
3. **Inheritance** — allowing a class to acquire properties and behavior from another class.
4. **Polymorphism** — allowing the same interface/method concept to behave differently in different situations.

**Easy memory trick: E-A-I-P**

---

### Q3. What is a class?

**Answer:** A class is a blueprint or template used to create objects. It defines the data and behavior that objects of that type can have.

```java
class Student {
    String name;

    void study() {
        System.out.println("Studying");
    }
}
```

---

### Q4. What is an object?

**Answer:** An object is an instance of a class. It represents a concrete entity and contains its own state while using the behavior defined by its class.

```java
Student s1 = new Student();
```

Here, `s1` is an object/reference to a `Student` instance.

---

### Q5. Class vs Object?

| Class | Object |
|---|---|
| Blueprint | Instance of a class |
| Logical definition | Runtime entity |
| Does not represent one specific instance | Represents a specific instance |
| Example: `Student` | Example: `new Student()` |

---

### Q6. What is a method?

**Answer:** A method is a block of code defined inside a class that performs a particular operation.

```java
void display() {
    System.out.println("Hello");
}
```

---

### Q7. What is a constructor?

**Answer:** A constructor is a special class member used to initialize an object when it is created.

```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }
}
```

---

### Q8. Constructor vs Method?

| Constructor | Method |
|---|---|
| Initializes an object | Performs an operation |
| Has the same name as the class in Java | Can have any valid method name |
| Has no return type | Can have a return type |
| Called during object creation | Called explicitly or through program flow |
| Cannot be overridden in Java | Can be overridden |

---

# 2. Encapsulation

### Q9. What is Encapsulation?

**Answer:** Encapsulation means bundling data and the methods that operate on that data inside a class while restricting direct access to the internal state when appropriate.

A common implementation is using `private` fields and public methods.

```java
class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
}
```

---

### Q10. Why is encapsulation important?

**Answer:**
- Protects internal data
- Prevents uncontrolled modification
- Improves maintainability
- Allows validation
- Reduces coupling
- Makes the class easier to use safely

---

### Q11. Is encapsulation the same as data hiding?

**Answer:** They are related but not exactly identical.

- **Encapsulation:** Bundling data and behavior together and controlling access.
- **Data hiding:** Restricting direct access to implementation details or internal state.

Encapsulation is a broader concept.

---

# 3. Abstraction

### Q12. What is Abstraction?

**Answer:** Abstraction means exposing only the essential behavior of an object while hiding unnecessary implementation details.

**Real-life example:** When you use an ATM, you select "Withdraw Cash." You do not need to know the internal banking/network operations.

---

### Q13. How can abstraction be achieved in Java?

Common mechanisms include:

1. Abstract classes
2. Interfaces

---

### Q14. What is an abstract class?

**Answer:** An abstract class is a class declared with `abstract`. It cannot be instantiated directly and can contain both abstract and concrete methods.

```java
abstract class Animal {
    abstract void sound();

    void eat() {
        System.out.println("Eating");
    }
}
```

---

### Q15. What is an abstract method?

**Answer:** An abstract method is declared without an implementation in an abstract class.

```java
abstract void sound();
```

A concrete subclass normally provides the implementation.

---

### Q16. Can an abstract class have a constructor?

**Answer:** **Yes.**

An abstract class cannot be instantiated directly, but its constructor can run as part of constructing an object of a concrete subclass.

---

### Q17. Can an abstract class have normal methods?

**Answer:** **Yes.** An abstract class can contain both abstract methods and concrete methods.

---

# 4. Interface

### Q18. What is an interface?

**Answer:** An interface defines a contract that implementing classes agree to follow. In modern Java, interfaces can also contain `default`, `static`, and private methods with implementations, subject to Java language rules.

```java
interface Payment {
    void pay();
}
```

---

### Q19. Why are interfaces used?

**Answer:**
- Define contracts
- Support loose coupling
- Enable multiple type inheritance
- Improve flexibility
- Make systems easier to test and extend

---

### Q20. Abstract class vs Interface?

| Abstract Class | Interface |
|---|---|
| Can contain instance state | Fields are constants (`public static final`) |
| Can have constructors | Cannot have constructors |
| Can have concrete methods | Can have abstract/default/static/private methods depending on Java version |
| A class extends one class | A class can implement multiple interfaces |
| Represents a shared base/partial implementation | Commonly represents a capability or contract |

---

# 5. Inheritance

### Q21. What is Inheritance?

**Answer:** Inheritance allows one class to derive from another class and reuse or extend its accessible fields and methods.

```java
class Animal {
    void eat() {
        System.out.println("Eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking");
    }
}
```

`Dog` inherits accessible behavior from `Animal`.

---

### Q22. Why is inheritance used?

**Answer:**
- Code reuse
- Extensibility
- Modeling an "is-a" relationship
- Supporting runtime polymorphism

---

### Q23. What are common types of inheritance?

Common conceptual forms are:

1. Single inheritance
2. Multilevel inheritance
3. Hierarchical inheritance
4. Multiple inheritance
5. Hybrid inheritance

**Important:** Java classes do **not** support multiple inheritance of classes. Java supports multiple inheritance of type through interfaces.

---

### Q24. What is single inheritance?

**Answer:** One child class inherits from one parent class.

`Animal → Dog`

---

### Q25. What is multilevel inheritance?

**Answer:** A class inherits from a class that itself inherits from another class.

`Animal → Mammal → Dog`

---

### Q26. What is hierarchical inheritance?

**Answer:** Multiple child classes inherit from the same parent class.

`Animal → Dog`  
`Animal → Cat`

---

### Q27. Why doesn't Java support multiple inheritance through classes?

**Answer:** A major reason is ambiguity, commonly illustrated by the **diamond problem**, where a class could inherit the same method through multiple parent classes and the language would need to determine which implementation to use.

Java avoids this for classes and provides interfaces as a mechanism for multiple inheritance of type.

---

# 6. Polymorphism

### Q28. What is Polymorphism?

**Answer:** Polymorphism means "many forms." It allows the same method/interface concept to represent different behavior depending on the situation.

Two commonly discussed forms in Java are:

- Compile-time polymorphism — method overloading
- Runtime polymorphism — method overriding

---

### Q29. What is Method Overloading?

**Answer:** Method overloading means having multiple methods with the same name but different parameter lists in the same class.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

---

### Q30. What is Method Overriding?

**Answer:** Method overriding occurs when a subclass provides its own implementation of an inherited method with a compatible signature.

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

---

### Q31. Overloading vs Overriding?

| Overloading | Overriding |
|---|---|
| Usually same class | Usually parent-child relationship |
| Different parameter list | Same method signature |
| Resolved at compile time | Resolved at runtime |
| Return type alone cannot overload a method | Return type may be covariant |
| Does not require inheritance | Requires inheritance/subtyping |

---

### Q32. Can we overload a method by changing only its return type?

**Answer:** **No.**

This is invalid because the compiler cannot distinguish calls based only on return type.

```java
int add(int a, int b)
double add(int a, int b)   // Invalid overload
```

---

### Q33. Can static methods be overridden?

**Answer:** **No, not in the polymorphic overriding sense.**

Static methods belong to the class rather than being dynamically dispatched based on the object. A subclass can define a static method with the same signature, which is called **method hiding**.

---

### Q34. Can private methods be overridden?

**Answer:** **No.**

Private methods are not inherited by subclasses, so they cannot be overridden.

---

### Q35. Can final methods be overridden?

**Answer:** **No.**

A `final` method cannot be overridden by a subclass.

---

# 7. Access Modifiers

### Q36. What are access modifiers?

In Java, the main access levels are:

- `private`
- default/package-private
- `protected`
- `public`

---

### Q37. Explain access modifiers.

| Modifier | Same Class | Same Package | Subclass (other package) | Everywhere |
|---|---|---|---|---|
| private | Yes | No | No | No |
| default | Yes | Yes | No* | No |
| protected | Yes | Yes | Yes, with rules | No |
| public | Yes | Yes | Yes | Yes |

`*` Package-private members are accessible only within the same package.

---

### Q38. Which access modifier provides the most restricted access?

**Answer:** `private`.

---

### Q39. What is the default access modifier in Java?

**Answer:** If no access modifier is written for a class member, it has **package-private** access.

---

# 8. Important Keywords

### Q40. What is `this`?

**Answer:** `this` refers to the current object.

```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }
}
```

---

### Q41. What is `super`?

**Answer:** `super` refers to the immediate superclass and can be used to access superclass members or invoke a superclass constructor.

```java
super();
super.display();
```

---

### Q42. What is `static`?

**Answer:** `static` means a member belongs to the class rather than to individual instances.

```java
class Counter {
    static int count = 0;
}
```

---

### Q43. What is `final`?

**Answer:** The meaning depends on where it is used:

- **final variable:** cannot be reassigned after initialization
- **final method:** cannot be overridden
- **final class:** cannot be extended

```java
final class A {
}
```

---

# 9. Association, Aggregation and Composition

### Q44. What is Association?

**Answer:** Association represents a general relationship between two classes.

**Example:** A `Teacher` teaches a `Student`.

---

### Q45. What is Aggregation?

**Answer:** Aggregation is a weak "has-a" relationship where the contained object can exist independently of the container.

**Example:** A `Department` has `Professor` objects, but professors can exist independently of a particular department.

---

### Q46. What is Composition?

**Answer:** Composition is a strong "has-a" relationship where the contained object's lifecycle is strongly tied to the containing object.

**Example:** A `House` has `Room` objects. In a conceptual model, rooms are considered parts of the house.

---

### Q47. Aggregation vs Composition?

| Aggregation | Composition |
|---|---|
| Weak has-a relationship | Strong has-a relationship |
| Parts can exist independently | Parts are strongly owned by the whole |
| Looser lifecycle dependency | Strong lifecycle dependency |
| Example: Team → Player | Example: Order → OrderLine |

---

# 10. Object Relationships

### Q48. What is an "is-a" relationship?

**Answer:** It represents inheritance/subtyping.

**Example:**

`Dog is an Animal.`

---

### Q49. What is a "has-a" relationship?

**Answer:** It represents composition or aggregation.

**Example:**

`Car has an Engine.`

---

### Q50. Inheritance vs Composition — which is preferred?

**Answer:** Neither is universally better, but **composition is often preferred when the relationship is about using behavior rather than representing a true subtype**.

A common design principle is:

> **Prefer composition over inheritance when inheritance does not represent a genuine "is-a" relationship.**

---

# 11. Important OOP Tricky Questions

## Q51. TRICKY: Is Java 100% object-oriented?

**Answer:** **No.**

Java is strongly object-oriented, but it has primitive data types such as `int`, `char`, `boolean`, and `double` that are not objects.

Java provides wrapper classes such as `Integer`, `Character`, `Boolean`, and `Double`.

---

## Q52. TRICKY: Can we create an object of an abstract class?

**Answer:** **No, not directly.**

```java
abstract class Animal {}

Animal a = new Animal(); // Compile-time error
```

However, a reference of an abstract class type can point to an object of a concrete subclass.

```java
Animal a = new Dog();
```

---

## Q53. TRICKY: Can an abstract class have zero abstract methods?

**Answer:** **Yes.**

A class can be declared `abstract` even if it contains no abstract methods. Such a class cannot be instantiated directly.

---

## Q54. TRICKY: Can an interface have variables?

**Answer:** **Yes.**

Interface fields are implicitly:

```java
public static final
```

Therefore, they are constants rather than ordinary instance variables.

---

## Q55. TRICKY: Can a constructor be inherited?

**Answer:** **No.**

Constructors belong to the class in which they are declared. A subclass does not inherit the parent's constructors.

---

## Q56. TRICKY: Can a constructor be overridden?

**Answer:** **No.**

Constructors are not inherited, so they cannot be overridden.

---

## Q57. TRICKY: Can a constructor be overloaded?

**Answer:** **Yes.**

```java
class Student {
    Student() {}

    Student(String name) {}
}
```

This is constructor overloading.

---

## Q58. TRICKY: Can a constructor be `static`?

**Answer:** **No.**

A constructor is used to initialize an instance, while `static` members belong to the class.

---

## Q59. TRICKY: Can a constructor be `final`?

**Answer:** **No.**

`final` prevents overriding, but constructors cannot be overridden in the first place.

---

## Q60. TRICKY: Can a constructor be `private`?

**Answer:** **Yes.**

Private constructors are useful in patterns such as Singleton or when a class controls how instances are created.

---

## Q61. TRICKY: Can a class be both `abstract` and `final`?

**Answer:** **No.**

- `abstract` means the class is intended to be extended.
- `final` means the class cannot be extended.

These purposes conflict.

---

## Q62. TRICKY: Can we overload `main()`?

**Answer:** **Yes.**

You can define additional overloaded `main()` methods, but the JVM looks for the standard entry-point signature:

```java
public static void main(String[] args)
```

---

## Q63. TRICKY: Can `main()` be overridden?

**Answer:** No, `main()` is static, so it is not overridden. A subclass can declare another static method with the same signature, resulting in method hiding.

---

## Q64. TRICKY: What happens if a parent reference points to a child object?

```java
Animal a = new Dog();
```

**Answer:** This is **upcasting**.

The reference type controls which members are accessible at compile time, while overridden instance methods are dynamically dispatched at runtime.

---

## Q65. TRICKY: What is upcasting?

**Answer:** Converting or assigning a subclass object to a superclass reference.

```java
Dog d = new Dog();
Animal a = d;
```

This is generally safe and does not require an explicit cast.

---

## Q66. TRICKY: What is downcasting?

**Answer:** Converting a superclass reference back to a subclass reference.

```java
Animal a = new Dog();
Dog d = (Dog) a;
```

The cast is valid only when the object actually refers to a compatible `Dog` object; otherwise a `ClassCastException` can occur.

---

## Q67. TRICKY: Which method is called here?

```java
class Animal {
    void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog");
    }
}

Animal a = new Dog();
a.sound();
```

**Answer:**

```text
Dog
```

Because `sound()` is an overridden instance method and Java uses **runtime method dispatch**.

---

## Q68. TRICKY: What happens with overloaded methods?

```java
void print(Animal a) {}
void print(Dog d) {}

Animal a = new Dog();
print(a);
```

**Answer:** The `print(Animal)` overload is selected because **overload resolution is based primarily on the compile-time type of the reference**.

This is a very important difference:

- **Overloading → compile time**
- **Overriding → runtime**

---

## Q69. TRICKY: Can a subclass reduce the visibility of an overridden method?

**Answer:** **No.**

For example, if the parent method is `public`, the overriding method cannot be `protected` or `private`.

It can maintain or increase accessibility, subject to Java's overriding rules.

---

## Q70. TRICKY: Can an overridden method change its return type?

**Answer:** It can use a **covariant return type**.

Example:

```java
class Animal {
    Animal get() {
        return new Animal();
    }
}

class Dog extends Animal {
    @Override
    Dog get() {
        return new Dog();
    }
}
```

`Dog` is a subtype of `Animal`, so this is valid.

---

## Q71. TRICKY: Can private methods have the same name in parent and child?

**Answer:** **Yes.**

Because private methods are not inherited, a child method with the same signature is a separate method, not an override.

---

## Q72. TRICKY: What is method hiding?

**Answer:** Method hiding occurs when a subclass declares a static method with the same signature as a static method in the parent class.

Static methods are resolved based on the reference/class context rather than runtime object dispatch.

---

## Q73. TRICKY: What is the difference between `==` and `.equals()`?

**Answer:**

For objects:

- `==` compares whether two references point to the same object.
- `.equals()` is a method intended to compare logical equality when the class overrides it appropriately.

Example:

```java
String a = new String("Hello");
String b = new String("Hello");

System.out.println(a == b);       // false
System.out.println(a.equals(b));  // true
```

---

## Q74. TRICKY: Why should `hashCode()` be overridden when `equals()` is overridden?

**Answer:** Java's general contract requires that if two objects are equal according to `equals()`, they must return the same hash code.

This is especially important when objects are used in hash-based collections such as `HashMap` and `HashSet`.

---

## Q75. TRICKY: Is `String` mutable in Java?

**Answer:** **No. `String` is immutable.**

Once a `String` object is created, its contents cannot be changed. Operations that appear to modify a string create another string object instead.

---

## Q76. TRICKY: Why is String immutable?

**Answer:** Immutability provides useful properties such as:

- Security
- Thread-safety benefits
- String pool optimization
- Stable hash codes
- Safe sharing between components

---

## Q77. TRICKY: What is immutable vs mutable?

**Answer:**

**Immutable:** Object state cannot be changed after creation.

**Mutable:** Object state can be changed after creation.

**Examples:**
- `String` → immutable
- `StringBuilder` → mutable

---

# 12. Scenario-Based OOP Questions

### Q78. You are designing a banking application. How would you use encapsulation?

**Answer:**

Keep account balance private and expose controlled operations such as `deposit()` and `withdraw()`.

```java
class Account {
    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}
```

This prevents external code from directly setting an invalid balance.

---

### Q79. How would you model different types of employees?

**Answer:**

Create a common `Employee` abstraction and specialized subclasses such as `Developer` and `Manager`.

```text
Employee
   |
   +-- Developer
   |
   +-- Manager
```

Overridden methods can provide specialized behavior.

---

### Q80. When would you use an interface instead of inheritance?

**Answer:**

Use an interface when you want to define a capability or contract that can be implemented by otherwise unrelated classes.

Example:

```java
interface Payable {
    void pay();
}
```

Both `Employee` and `Vendor` could implement `Payable` even if they do not share the same class hierarchy.

---

### Q81. Give a real-world example of polymorphism.

**Answer:**

Consider payment methods:

```text
Payment
  |
  +-- CreditCardPayment
  +-- UpiPayment
  +-- CashPayment
```

Each implementation can provide its own `pay()` behavior while client code works with the common `Payment` abstraction.

---

### Q82. Why is abstraction useful in large applications?

**Answer:**

It reduces complexity by allowing developers to work with a simpler interface instead of understanding every implementation detail. It also makes implementations replaceable without changing all client code.

---

### Q83. Why can excessive inheritance be a problem?

**Answer:**

Deep inheritance hierarchies can create:

- Tight coupling
- Difficult maintenance
- Fragile base-class problems
- Hard-to-understand behavior
- Unwanted inherited behavior

Composition can often provide more flexibility.

---

# 13. Common Fresher Coding Questions

### Q84. Create a simple class and object.

```java
class Student {
    String name;

    void display() {
        System.out.println(name);
    }
}

class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.name = "Rahul";
        s.display();
    }
}
```

---

### Q85. Demonstrate encapsulation.

```java
class Employee {
    private int salary;

    public void setSalary(int salary) {
        if (salary >= 0) {
            this.salary = salary;
        }
    }

    public int getSalary() {
        return salary;
    }
}
```

---

### Q86. Demonstrate inheritance.

```java
class Animal {
    void eat() {
        System.out.println("Eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking");
    }
}
```

---

### Q87. Demonstrate method overloading.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

---

### Q88. Demonstrate method overriding.

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

---

# 14. Rapid-Fire Interview Questions

### Q89. What is OOP?
Programming organized around objects containing state and behavior.

### Q90. What is a class?
A blueprint/template for objects.

### Q91. What is an object?
An instance of a class.

### Q92. What is encapsulation?
Bundling data and behavior while controlling access to internal state.

### Q93. What is abstraction?
Showing essential behavior while hiding implementation details.

### Q94. What is inheritance?
Deriving a class from another class to reuse/extend behavior.

### Q95. What is polymorphism?
One interface/concept taking multiple forms.

### Q96. What is overloading?
Same method name with different parameter lists.

### Q97. What is overriding?
A subclass providing a new implementation of an inherited instance method.

### Q98. Can constructors be inherited?
No.

### Q99. Can constructors be overloaded?
Yes.

### Q100. Can constructors be overridden?
No.

### Q101. Can static methods be overridden?
No; they can be hidden.

### Q102. Can private methods be overridden?
No.

### Q103. Can final methods be overridden?
No.

### Q104. Can an abstract class have a constructor?
Yes.

### Q105. Can an abstract class have concrete methods?
Yes.

### Q106. Can an abstract class have no abstract methods?
Yes.

### Q107. Can an interface have fields?
Yes; interface fields are implicitly `public static final`.

### Q108. Can Java classes support multiple inheritance?
No.

### Q109. Can Java support multiple inheritance through interfaces?
Yes, a class can implement multiple interfaces.

### Q110. What is `this`?
Reference to the current object.

### Q111. What is `super`?
Reference to the immediate superclass.

### Q112. What is `final` class?
A class that cannot be extended.

### Q113. What is composition?
A strong has-a relationship.

### Q114. What is aggregation?
A weaker has-a relationship where parts can exist independently.

### Q115. What is upcasting?
Treating a subclass object as a superclass reference.

### Q116. What is downcasting?
Casting a superclass reference to a compatible subclass type.

### Q117. What is dynamic method dispatch?
Runtime selection of an overridden instance method based on the actual object.

### Q118. What is the difference between `==` and `.equals()`?
`==` compares references for objects; `.equals()` can compare logical equality when implemented accordingly.

---

# 15. Top 20 Questions You MUST Know

If you have very little time before an interview, prepare these first:

1. What is OOP?
2. What are the four pillars of OOP?
3. Class vs Object?
4. Encapsulation with example
5. Abstraction with example
6. Inheritance and its types
7. Polymorphism
8. Overloading vs Overriding
9. Abstract class vs Interface
10. Why doesn't Java support multiple class inheritance?
11. What is `this`?
12. What is `super`?
13. What is `static`?
14. What is `final`?
15. Constructor vs Method
16. Can constructors be inherited/overridden?
17. Can static/private/final methods be overridden?
18. `==` vs `.equals()`
19. Composition vs Inheritance
20. Upcasting vs Downcasting

---

# 16. Interview Traps to Remember

> **Trap 1:** Return type alone cannot overload a method.

> **Trap 2:** Constructors are neither inherited nor overridden, but they can be overloaded.

> **Trap 3:** Static methods are hidden, not overridden.

> **Trap 4:** Private methods are not overridden because they are not inherited.

> **Trap 5:** `final` methods cannot be overridden.

> **Trap 6:** An abstract class can have constructors and concrete methods.

> **Trap 7:** An abstract class can contain zero abstract methods.

> **Trap 8:** Java supports multiple interfaces but not multiple inheritance of classes.

> **Trap 9:** Overloading is resolved at compile time; overriding uses runtime dispatch for instance methods.

> **Trap 10:** For objects, `==` checks reference identity, while `.equals()` checks logical equality when the class defines it appropriately.

---

# 17. Final OOP Revision Map

```text
                    OOP
                     |
        +------------+------------+
        |            |            |
   Encapsulation  Abstraction  Inheritance
        |            |            |
   Data + Methods  Hide detail   Reuse/extend
        |            |            |
        +------------+------------+
                     |
                Polymorphism
                     |
             +-------+-------+
             |               |
         Overloading      Overriding
         Compile Time     Runtime
```

## The one-line memory trick

**Encapsulation = Protect**

**Abstraction = Hide**

**Inheritance = Reuse**

**Polymorphism = Many Forms**

---

# Final Interview Advice

Do not memorize OOP definitions only.

For each concept, prepare:

1. **Definition**
2. **Real-world example**
3. **Code example**
4. **Difference from related concepts**
5. **One tricky question**

For a fresher interview, if you can confidently explain **Encapsulation, Abstraction, Inheritance, Polymorphism, Overloading, Overriding, Abstract Class, Interface, Composition, Access Modifiers, `this`, `super`, `static`, `final`, and the tricky questions**, you have a strong OOP foundation.
