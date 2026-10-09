# Rheal Software — C / C++ / Java Tricky Concepts & Interview Question Bank

## Purpose

This file is focused on the **Programming / Logic round and technical interview** for Rheal Software.

The college pattern emphasizes C/C++/Java basics, output prediction, programming logic, pseudocode, OOP and debugging.

Rheal interview reports are especially useful here. A September 2025 Pune report mentions a **C code-snippet round involving `a++` and `++a`**, followed by database and technical rounds. Another Rheal Software Engineer report mentions **pseudocode based on C++, output prediction, OOP concepts and SQL**. A 2026 report mentions basic programming questions, data structures and internal working of concepts.

So this file focuses on **tricky language behavior**, not just normal syntax.

---

# PART 1 — MUST-KNOW TRICKY CONCEPTS

## C / C++

1. `i++` vs `++i`
2. `--i` vs `i--`
3. Operator precedence
4. Short-circuit `&&` and `||`
5. `=` vs `==`
6. `&` vs `&&`
7. `|` vs `||`
8. Bitwise operators
9. Pointer basics
10. Pointer arithmetic
11. Pointer to pointer
12. Array-pointer relationship
13. `*p` vs `p`
14. References
15. Pass by value vs reference
16. `const`
17. `static`
18. Scope
19. Stack vs heap
20. Dynamic memory
21. `new` / `delete`
22. `nullptr`
23. Dangling pointer
24. Memory leak
25. Function overloading
26. Function overriding
27. Virtual functions
28. Constructors/destructors
29. Inheritance order
30. Object slicing
31. Undefined behavior
32. `sizeof(array)` vs `sizeof(pointer)`
33. `a` vs `&a`
34. Virtual destructor
35. RAII

## Java

36. `==` vs `.equals()`
37. String pool
38. String immutability
39. `StringBuilder` vs `StringBuffer`
40. Wrapper classes
41. Autoboxing/unboxing
42. Integer caching
43. `static`
44. `final`
45. `this` vs `super`
46. Overloading vs overriding
47. Dynamic method dispatch
48. Abstract class vs interface
49. `finally`
50. `throw` vs `throws`
51. Checked vs unchecked exceptions
52. `ArrayList` vs array
53. `HashMap`
54. `HashSet`
55. `equals()` and `hashCode()`
56. Pass-by-value in Java
57. Null references
58. Garbage collection
59. Static method hiding
60. Constructor inheritance

---

# PART 2 — C TRICKY OUTPUT QUESTIONS

## Q1. Post-increment

```c
int a = 5;
int b = a++;

printf("%d %d", a, b);
```

### Answer

```text
6 5
```

`a++` returns the old value and then increments.

---

## Q2. Pre-increment

```c
int a = 5;
int b = ++a;

printf("%d %d", a, b);
```

### Answer

```text
6 6
```

---

## Q3. Multiple increments

```c
int a = 5;

printf("%d ", a++);
printf("%d ", ++a);
printf("%d", a);
```

### Answer

```text
5 7 7
```

---

## Q4. Undefined behavior

```c
int i = 5;
int x = i++ + ++i;
```

### Answer

Do **not** calculate this as `11`.

In C, this expression has **undefined behavior** because `i` is modified more than once without the required sequencing.

### Interview lesson

A strong candidate should recognize when a snippet has **no well-defined answer**.

---

## Q5. Operator precedence

```c
int x = 2 + 3 * 4;

printf("%d", x);
```

### Answer

```text
14
```

Multiplication has higher precedence than addition.

---

## Q6. Parentheses

```c
int x = (2 + 3) * 4;

printf("%d", x);
```

### Answer

```text
20
```

---

## Q7. Integer division

```c
int x = 5 / 2;

printf("%d", x);
```

### Answer

```text
2
```

Both operands are integers.

---

## Q8. Floating-point trap

```c
float x = 5 / 2;

printf("%.1f", x);
```

### Answer

```text
2.0
```

`5 / 2` is evaluated as integer division first.

To get `2.5`:

```c
float x = 5.0 / 2;
```

---

## Q9. Modulus

```c
printf("%d", 17 % 5);
```

### Answer

```text
2
```

---

## Q10. Negative remainder

```c
printf("%d", -7 % 3);
```

### Answer

```text
-1
```

---

# PART 3 — SHORT-CIRCUIT AND OPERATORS

## Q11. Short-circuit AND

```c
int x = 0;

if(x != 0 && 10 / x > 2)
    printf("YES");
else
    printf("NO");
```

### Answer

```text
NO
```

The second condition is not evaluated.

---

## Q12. Short-circuit OR

```c
int x = 5;

if(x == 5 || ++x > 10)
    printf("%d", x);
```

### Answer

```text
5
```

`++x` is never executed.

---

## Q13. `&` vs `&&`

What is the difference?

### Answer

```text
&   = bitwise AND
&&  = logical AND
```

---

## Q14. XOR

```c
printf("%d", 5 ^ 3);
```

### Answer

```text
6
```

Binary:

```text
101
011
---
110
```

---

## Q15. Left shift

```c
int x = 4;
printf("%d", x << 1);
```

### Answer

```text
8
```

For this positive integer case, it is equivalent to multiplying by 2.

---

## Q16. Right shift

```c
int x = 16;
printf("%d", x >> 2);
```

### Answer

```text
4
```

---

# PART 4 — POINTERS

## Q17. Basic pointer

```c
int x = 10;
int *p = &x;

printf("%d", *p);
```

### Answer

```text
10
```

---

## Q18. `p` vs `*p`

Given:

```c
int x = 10;
int *p = &x;
```

What do `p` and `*p` represent?

### Answer

```text
p  → address stored in p
*p → value at that address
```

---

## Q19. Modify through pointer

```c
int x = 10;
int *p = &x;

*p = 50;

printf("%d", x);
```

### Answer

```text
50
```

---

## Q20. Pointer to pointer

```c
int x = 10;
int *p = &x;
int **q = &p;

printf("%d", **q);
```

### Answer

```text
10
```

---

## Q21. Pointer arithmetic

```c
int a[] = {10,20,30,40};
int *p = a;

printf("%d", *(p + 2));
```

### Answer

```text
30
```

---

## Q22. Array-pointer equivalence

What does:

```c
a[i]
```

mean in pointer notation?

### Answer

```c
*(a + i)
```

---

## Q23. Pointer indexing

```c
int a[] = {10,20,30};
int *p = a;

printf("%d", p[1]);
```

### Answer

```text
20
```

---

## Q24. `a` vs `&a`

For:

```c
int a[5];
```

what is the conceptual difference?

### Answer

`a` generally becomes a pointer to its first element in expressions.

`&a` is a pointer to the entire array.

Conceptually:

```text
a   → int *
&a  → int (*)[5]
```

---

## Q25. sizeof array vs pointer

```c
int a[5];
int *p = a;

printf("%zu
", sizeof(a));
printf("%zu
", sizeof(p));
```

### Answer

`sizeof(a)` is the size of the entire array.

`sizeof(p)` is the size of the pointer.

On a typical 64-bit system with 4-byte `int`:

```text
20
8
```

---

## Q26. Array parameter trap

```c
void fun(int a[])
{
    printf("%zu", sizeof(a));
}
```

### Question

Does `sizeof(a)` give the original array size?

### Answer

No.

In a function parameter, `a` is adjusted to a pointer.

---

## Q27. Uninitialized pointer

```c
int *p;
*p = 10;
```

### Answer

Wrong.

`p` does not point to a valid object. Dereferencing it causes undefined behavior.

---

## Q28. NULL pointer

```c
int *p = NULL;
printf("%d", *p);
```

### Answer

Undefined behavior because a NULL pointer is dereferenced.

---

## Q29. Dangling pointer

What is a dangling pointer?

### Answer

A pointer that refers to an object whose lifetime has ended or to memory that is no longer valid.

---

## Q30. Memory leak

```c
int *p = malloc(sizeof(int));
p = NULL;
```

### What is the problem?

### Answer

The allocated memory is no longer reachable through `p`, so it cannot be freed through that pointer.

This causes a memory leak.

---

# PART 5 — STORAGE / MEMORY

## Q31. Static local variable

```c
void fun()
{
    static int x = 0;
    x++;
    printf("%d ", x);
}

int main()
{
    fun();
    fun();
    fun();
}
```

### Answer

```text
1 2 3
```

---

## Q32. Local variable shadows global

```c
int x = 10;

int main()
{
    int x = 20;
    printf("%d", x);
}
```

### Answer

```text
20
```

---

## Q33. Stack vs heap

What is the basic difference?

### Answer

**Stack:** automatic/local call-related storage.

**Heap:** dynamically allocated storage.

Exact implementation details depend on the system/runtime.

---

# PART 6 — FUNCTIONS / RECURSION

## Q34. Pass by value

```c
void change(int x)
{
    x = 100;
}

int main()
{
    int a = 10;
    change(a);
    printf("%d", a);
}
```

### Answer

```text
10
```

---

## Q35. Pointer-based modification

```c
void change(int *x)
{
    *x = 100;
}

int main()
{
    int a = 10;
    change(&a);
    printf("%d", a);
}
```

### Answer

```text
100
```

---

## Q36. Recursion

```c
int fun(int n)
{
    if(n == 0)
        return 0;

    return n + fun(n - 1);
}

printf("%d", fun(4));
```

### Answer

```text
10
```

---

# PART 7 — C++ UNIQUE CONCEPTS

## Q37. Reference

```cpp
int x = 10;
int &r = x;

r = 50;

cout << x;
```

### Answer

```text
50
```

---

## Q38. Pointer vs reference

### Answer

Pointer:
- Can be null.
- Can be reassigned.
- Uses dereferencing.

Reference:
- Must bind to an object when initialized.
- Acts as an alias.
- Cannot normally be reseated.

---

## Q39. const variable

```cpp
const int x = 10;
x = 20;
```

### Answer

Compilation error.

---

## Q40. Pointer to const

```cpp
const int x = 10;
const int *p = &x;
```

Can:

```cpp
*p = 20;
```

be performed?

### Answer

No.

---

## Q41. Const pointer

```cpp
int x = 10;
int y = 20;

int *const p = &x;
```

Can `p` later point to `y`?

### Answer

No.

But:

```cpp
*p = 50;
```

is allowed.

---

## Q42. Return type overloading

```cpp
int fun(int x);
double fun(int x);
```

Can these be overloaded?

### Answer

No.

Return type alone cannot distinguish overloaded functions.

---

## Q43. Constructor order

```cpp
class A
{
public:
    A() { cout << "A"; }
};

class B : public A
{
public:
    B() { cout << "B"; }
};

int main()
{
    B obj;
}
```

### Answer

```text
AB
```

---

## Q44. Destructor order

For a derived object, which destructor executes first?

### Answer

```text
Derived destructor
Base destructor
```

---

## Q45. Virtual function

```cpp
class A
{
public:
    virtual void show()
    {
        cout << "A";
    }
};

class B : public A
{
public:
    void show() override
    {
        cout << "B";
    }
};

int main()
{
    A *p = new B();
    p->show();
}
```

### Answer

```text
B
```

Because `show()` is virtual.

---

## Q46. Remove virtual

If `show()` in A is not virtual, then:

```cpp
A *p = new B();
p->show();
```

### Answer

For a non-virtual member function, the call is resolved using the static type of the pointer.

So it calls A's version:

```text
A
```

---

## Q47. Pure virtual function

```cpp
class A
{
public:
    virtual void show() = 0;
};
```

Can you do:

```cpp
A obj;
```

### Answer

No.

A is an abstract class.

---

## Q48. Object slicing

```cpp
class A
{
public:
    int x = 10;
};

class B : public A
{
public:
    int y = 20;
};

B b;
A a = b;
```

### Answer

The derived-specific part is sliced off.

`a` contains only the base-class portion.

---

## Q49. new/delete

```cpp
int *p = new int(10);

cout << *p;

delete p;
```

### Answer

```text
10
```

---

## Q50. new[] / delete[]

For:

```cpp
int *p = new int[5];
```

which should normally be used?

### Answer

```cpp
delete[] p;
```

not:

```cpp
delete p;
```

---

## Q51. Virtual destructor

Why can a base destructor be virtual?

### Answer

If deleting a derived object through a base pointer, a virtual destructor ensures the correct derived destructor is invoked.

---

## Q52. RAII

What does RAII mean?

### Answer

**Resource Acquisition Is Initialization.**

C++ ties resource lifetime to object lifetime, usually acquiring resources in constructors and releasing them in destructors.

---

# PART 8 — JAVA TRICKY CONCEPTS

## Q53. Java pass-by-value

Does Java use pass-by-reference?

### Answer

No.

Java is **always pass-by-value**.

When an object is passed, the value being copied is the object reference.

---

## Q54. Primitive pass-by-value

```java
static void change(int x) {
    x = 100;
}

public static void main(String[] args) {
    int a = 10;
    change(a);
    System.out.println(a);
}
```

### Answer

```text
10
```

---

## Q55. Object reference modification

```java
class Test {
    int x = 10;
}

static void change(Test t) {
    t.x = 100;
}
```

Then:

```java
Test obj = new Test();
change(obj);

System.out.println(obj.x);
```

### Answer

```text
100
```

The copied reference still refers to the same object.

---

## Q56. Reassigning an object reference

```java
static void change(Test t) {
    t = new Test();
    t.x = 100;
}
```

### Answer

The caller's reference is unchanged.

Java copied the reference value into `t`; reassigning `t` does not reassign the caller's variable.

---

## Q57. `==` vs `.equals()`

```java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b);
System.out.println(a.equals(b));
```

### Answer

```text
false
true
```

---

## Q58. String pool

```java
String a = "hello";
String b = "hello";

System.out.println(a == b);
```

### Answer

Typically:

```text
true
```

String literals are interned and may refer to the same pooled object.

---

## Q59. Runtime concatenation

```java
String a = "hello";
String x = "hel";
String b = x + "lo";

System.out.println(a == b);
```

### Answer

Typically:

```text
false
```

The concatenation involves a runtime value.

---

## Q60. String immutability

```java
String s = "hello";

s.concat(" world");

System.out.println(s);
```

### Answer

```text
hello
```

`String` is immutable.

Correct:

```java
s = s.concat(" world");
```

---

## Q61. StringBuilder

Why is `StringBuilder` useful?

### Answer

It is mutable, so repeated modifications can be performed without creating a new immutable String for every change.

---

## Q62. Integer caching

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b);
```

### Answer

Typically:

```text
true
```

because commonly used small Integer values are cached.

---

## Q63. Integer cache trap

```java
Integer a = 200;
Integer b = 200;

System.out.println(a == b);
```

### Answer

Typically:

```text
false
```

Use:

```java
a.equals(b)
```

for value comparison.

---

## Q64. Null unboxing

```java
Integer x = null;
int y = x;
```

### Answer

Runtime:

```text
NullPointerException
```

---

# PART 9 — JAVA OOP

## Q65. Overloading

Same method name with different parameter lists.

### Answer

**Method overloading.**

Usually compile-time polymorphism.

---

## Q66. Overriding

Child class provides a new implementation of an inherited instance method.

### Answer

**Method overriding.**

Used with runtime polymorphism/dynamic dispatch.

---

## Q67. Static method hiding

```java
class A {
    static void show() {
        System.out.println("A");
    }
}

class B extends A {
    static void show() {
        System.out.println("B");
    }
}
```

Is this runtime overriding?

### Answer

No.

Static methods are hidden, not dynamically overridden.

---

## Q68. Final method

Can a child class override a final method?

### Answer

No.

---

## Q69. Final class

```java
final class A {}
```

Can another class extend A?

### Answer

No.

---

## Q70. Final method can be overloaded?

### Answer

Yes.

`final` prevents overriding, not overloading.

---

## Q71. `this`

What does `this` represent?

### Answer

The current object.

---

## Q72. `super`

What does `super` represent?

### Answer

The immediate parent-class portion of the current object and is used to access parent constructors/members.

---

## Q73. Constructor inheritance

Are constructors inherited?

### Answer

No.

A child constructor can invoke a parent constructor using `super(...)`.

---

## Q74. Abstract class constructor

Can an abstract Java class have a constructor?

### Answer

Yes.

The constructor executes as part of constructing a concrete subclass.

---

# PART 10 — JAVA EXCEPTIONS

## Q75. `throw` vs `throws`

### Answer

`throw` actually throws an exception.

```java
throw new Exception();
```

`throws` declares possible exceptions in a method signature.

```java
void fun() throws Exception
```

---

## Q76. finally

What is `finally` used for?

### Answer

It is generally used for cleanup code that should execute whether an exception occurs or not.

---

## Q77. Can finally fail to execute?

### Answer

Yes.

For example, abrupt JVM termination such as:

```java
System.exit(...)
```

can prevent normal finally execution.

---

## Q78. Checked exception

Give examples.

### Answer

Common examples:

```text
IOException
SQLException
```

Checked exceptions generally must be caught or declared.

---

## Q79. Unchecked exception

Examples:

```text
NullPointerException
ArithmeticException
ArrayIndexOutOfBoundsException
```

These are subclasses of `RuntimeException`.

---

# PART 11 — JAVA COLLECTION TRAPS

## Q80. Array vs ArrayList

### Answer

Array:

- Fixed length
- Supports primitive elements directly
- Simple and efficient for fixed-size data

ArrayList:

- Resizable
- Stores objects/reference types
- Provides collection operations

---

## Q81. HashSet duplicates

Can HashSet store duplicate elements?

### Answer

No, logically duplicate elements are not retained.

---

## Q82. HashMap duplicate key

```java
HashMap<Integer, String> map = new HashMap<>();

map.put(1, "A");
map.put(1, "B");
```

### Answer

The second value replaces the first:

```text
1 → B
```

---

## Q83. Null key

Can standard HashMap have a null key?

### Answer

Yes.

A standard `HashMap` permits one null key and multiple null values.

---

## Q84. equals/hashCode

If:

```java
a.equals(b)
```

is true, what must be true about their hash codes?

### Answer

They must return the same hash code.

The reverse is not required: equal hash codes do not necessarily mean the objects are equal.

---

# PART 12 — HIGH-FREQUENCY OUTPUT TRAPS

## Q85.

```cpp
int x = 5;

cout << x++ << " ";
cout << x++ << " ";
cout << ++x;
```

### Answer

```text
5 6 8
```

---

## Q86.

```cpp
int x = 10;

if(x > 5)
    cout << "A";

if(x > 15)
    cout << "B";
else
    cout << "C";
```

### Answer

```text
AC
```

The `else` belongs to the second `if`.

---

## Q87. Dangling else

```cpp
if(true)
    if(false)
        cout << "A";
    else
        cout << "B";
```

### Answer

```text
B
```

The `else` attaches to the nearest unmatched `if`.

---

## Q88. Switch fall-through

```cpp
int x = 1;

switch(x)
{
    case 1:
        cout << "A";
    case 2:
        cout << "B";
        break;
    default:
        cout << "C";
}
```

### Answer

```text
AB
```

---

## Q89. Character arithmetic

```cpp
char c = 'A';

cout << c + 1;
```

### Answer

Typically:

```text
66
```

because the character is promoted to an integer.

---

## Q90. Character increment

```cpp
char c = 'A';

c++;

cout << c;
```

### Answer

```text
B
```

---

# PART 13 — TRICKY DEBUGGING

## Q91.

```cpp
for(int i = 0; i < 10; i++)
{
    for(int j = 0; j < 10; i++)
        cout << "*";
}
```

### Answer

The inner loop increments `i` instead of `j`.

Correct:

```cpp
j++;
```

---

## Q92.

```cpp
int sum;

for(int i = 0; i < 5; i++)
    sum += i;
```

### Answer

`sum` is uninitialized.

Correct:

```cpp
int sum = 0;
```

---

## Q93.

```cpp
int a[5];

cout << a[5];
```

### Answer

Out-of-bounds access.

Valid indexes:

```text
0 1 2 3 4
```

---

## Q94.

```cpp
int x = 10;

if(x = 5)
    cout << "YES";
```

### Answer

`x = 5` is assignment, not comparison.

The assignment expression evaluates to `5`, which is non-zero, so this prints:

```text
YES
```

Correct comparison:

```cpp
if(x == 5)
```

---

## Q95.

```cpp
int i = 10;

while(i > 0)
{
    cout << i;
}
```

### Answer

Infinite loop.

`i` never changes.

---

# PART 14 — C/C++/JAVA DIFFERENCES

## Q96. Is C object-oriented?

### Answer

No. C is primarily procedural.

---

## Q97. Is C++ purely object-oriented?

### Answer

No.

C++ is multi-paradigm.

---

## Q98. Is Java purely object-oriented?

### Answer

It is strongly object-oriented, but it has primitive types, so calling it strictly "purely object-oriented" is an oversimplification.

---

## Q99. Raw pointers

Which languages support raw pointers?

### Answer

```text
C     → Yes
C++   → Yes
Java  → No
```

Java uses object references instead.

---

## Q100. Multiple inheritance

### Answer

```text
C++   → Supports multiple class inheritance
Java  → No multiple class inheritance; multiple interfaces are allowed
C     → No class inheritance
```

---

## Q101. Garbage collection

### Answer

```text
C     → No built-in garbage collector
C++   → No built-in tracing garbage collector
Java  → Garbage collection
```

---

## Q102. Manual memory management

### C

```c
malloc()
free()
```

### C++

```cpp
new
delete
```

Modern C++ also prefers RAII and smart pointers.

### Java

Objects are automatically managed by garbage collection.

---

# PART 15 — CONCEPT QUESTIONS INTERVIEWERS LIKE

## Q103. Why is `++i` sometimes preferred over `i++`?

### Answer

For primitive integers, modern compilers generally optimize both when appropriate.

For iterator objects, postfix increment may need to preserve the old iterator value, while prefix increment can avoid that extra conceptual copy.

---

## Q104. Why is Java String immutable?

### Answer

Immutability supports safe sharing, string pooling, stable hashing, thread-safety properties and security.

---

## Q105. Why should equals and hashCode agree?

### Answer

Hash-based collections use `hashCode()` to locate candidates and `equals()` to determine logical equality.

If two objects are equal, they must have the same hash code.

---

## Q106. Why can memory leaks happen in Java despite garbage collection?

### Answer

Because an object that is no longer logically needed can still be reachable through an unwanted reference. The garbage collector cannot collect reachable objects.

---

## Q107. Why can a C++ base destructor be virtual?

### Answer

To ensure correct derived destruction when deleting through a base pointer.

---

## Q108. What is undefined behavior?

### Answer

Behavior for which the language standard imposes no requirements.

It is different from a normal compilation error.

---

## Q109. Is segmentation fault a C/C++ language rule?

### Answer

No.

A segmentation fault is a common operating-system/runtime manifestation of invalid memory access. The underlying program may have invoked undefined behavior.

---

# PART 16 — TOP 50 TRAPS TO REVISE BEFORE THE TEST

1. `i++` vs `++i`
2. Undefined behavior from unsequenced modifications
3. Integer division
4. Floating-point conversion
5. Operator precedence
6. Short-circuit AND
7. Short-circuit OR
8. `&` vs `&&`
9. `|` vs `||`
10. XOR
11. Left/right shift
12. Pointer vs pointed value
13. `&x`
14. `*p`
15. Pointer arithmetic
16. Pointer to pointer
17. Array vs pointer
18. `sizeof(array)`
19. `sizeof(pointer)`
20. `a` vs `&a`
21. Array function parameters
22. NULL/nullptr
23. Dangling pointer
24. Memory leak
25. Static local
26. Scope
27. Shadowing
28. Pass by value
29. C pointer-based modification
30. C++ reference
31. `const`
32. Const pointer
33. Pointer to const
34. Overloading
35. Overriding
36. Virtual function
37. Pure virtual function
38. Constructor order
39. Destructor order
40. Virtual destructor
41. Object slicing
42. RAII
43. Java pass-by-value
44. Java `==` vs `.equals()`
45. String pool
46. String immutability
47. Integer caching
48. `equals()` / `hashCode()`
49. Static method hiding
50. `final`

---

# PART 17 — RHEAL-FOCUSED PRIORITY

Based on available Rheal interview reports, prioritize these first:

## 🔴 Extremely High Priority

```text
C code snippets
++a / a++
Output prediction
Pseudocode
Pointers
Arrays
Loops
OOP output
Debugging
```

## 🟠 High Priority

```text
Functions
Recursion
References
Static
Scope
Operator precedence
Short-circuit operators
C++ inheritance
Overloading
Overriding
Virtual functions
```

## 🟡 Java Tricky Concepts

```text
String pool
== vs equals
String immutability
Integer caching
Pass-by-value
Static method hiding
Final
Exceptions
Collections
equals/hashCode
```

---

# PART 18 — FINAL OUTPUT-SOLVING METHOD

When a company gives you a code snippet, do NOT immediately calculate.

Use this checklist:

```text
1. Identify the language
2. Identify variable types
3. Check operator precedence
4. Check ++ / --
5. Check short-circuit behavior
6. Check scope/shadowing
7. Check pointer/reference behavior
8. Check array boundaries
9. Check integer vs floating-point division
10. Check static variables
11. Check function parameter passing
12. Check inheritance/polymorphism
13. Check whether behavior is actually defined
14. Only then calculate the output
```

The most dangerous mistake in output questions is assuming that **every code snippet has a normal deterministic answer**.

A strong candidate should be able to answer:

> "This does not have a well-defined output because the program invokes undefined behavior."

That can be more correct than calculating a number.

---

# RHEAL-SPECIFIC SOURCE NOTES

The Rheal-specific priorities in this file are based on publicly reported interview experiences, especially:

- Recent Glassdoor reports mentioning C code snippets, `a++` / `++a`, pseudocode, C++ output prediction, OOP and programming basics.
- Rheal Software careers information describing software-development hiring.

These sources indicate recurring themes, but they do **not** guarantee the exact questions or exact language used in your 2026 campus test.
