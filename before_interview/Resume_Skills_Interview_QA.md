# Resume-Based Technical Interview Questions and Answers

## Skills Section: Programming, Core Concepts, Databases, Web Technologies, and Tools

**Purpose:** This guide prepares you for questions an interviewer may
ask after reading your resume's Skills section. It includes direct
technical questions, follow-up questions, practical scenarios, and
HR-style credibility checks.

**Important:** Use these answers as a model, not as scripts to memorize.
Be honest about your actual level of experience. If you list a
technology on your resume, be prepared to explain its fundamentals and
discuss something you have built with it.

------------------------------------------------------------------------

# 1. Questions an Interviewer May Ask First

### Q1. Tell me about your technical skills.

**Sample answer:** "My technical skills include programming in C, C++,
Python, Java, TypeScript, and C#. I understand core concepts such as
OOP, data structures and algorithms, and problem-solving. I have worked
with MySQL and MongoDB for data storage. For web development, I know
HTML, CSS, JavaScript, TypeScript, React, Node.js, Express.js, and
JWT-based authentication. I also use Git, GitHub, VS Code, Visual
Studio, Postman, AWS, and Docker. I am strongest in the technologies I
have used practically, and I continue to improve through projects and
interview practice."

**Follow-up:** Which three skills are you strongest in?\
**Good approach:** Name the skills you can actually demonstrate, explain
why, and give one example for each.

### Q2. Which language are you most comfortable with, and why?

**Sample answer:** "I am most comfortable with \[your strongest
language\] because I have used it for \[specific project, assignments,
or problem-solving\]. I can explain its basic syntax, data types,
control flow, functions, and OOP features, and I have practised solving
problems with it."

Do not claim expertise in every language just because it appears on the
resume.

### Q3. Why have you listed so many programming languages?

**Sample answer:** "Different languages help me understand different
programming approaches. I focus on problem-solving and core concepts
rather than memorizing syntax. I am careful to distinguish between
languages I can use independently and those I am still learning."

### Q4. What is the difference between knowing a technology and being proficient in it?

**Answer:** Knowing a technology may mean understanding its basic syntax
and purpose. Proficiency means being able to use it independently, debug
problems, make design decisions, and explain trade-offs in a real task.

### Q5. Which project best demonstrates your skills?

**Answer framework:** Explain the problem, your responsibility, the
architecture, the technologies used, one difficult technical problem,
how you solved it, and what you would improve. Only describe work you
actually completed.

### Q6. If I ask you to code now, which language will you choose?

**Answer:** Choose the language in which you can solve the problem
clearly and correctly. Explain your logic, edge cases, and time and
space complexity. Do not choose a language merely because it sounds
impressive.

------------------------------------------------------------------------

# 2. Programming Fundamentals

## 2.1 General Programming

### Q7. What is a variable?

**Answer:** A variable is a named reference or storage location used to
represent a value in a program. The exact memory and reference behavior
depends on the language.

### Q8. What is the difference between declaration, initialization, and assignment?

**Answer:** - **Declaration:** Introduces a variable or its name/type,
depending on the language. - **Initialization:** Gives it its initial
value. - **Assignment:** Gives or changes its value after it exists.

Example in C:

``` c
int age;       // declaration
int marks = 90; // declaration and initialization
age = 20;       // assignment
```

### Q9. What is the difference between a compiler and an interpreter?

**Answer:** A compiler translates source code into another form, often
machine code or intermediate code, before or as part of execution. An
interpreter executes instructions through a runtime. Modern languages
may combine compilation and interpretation, so the distinction is not
always absolute. C and C++ commonly use native compilation; Java
compiles to bytecode executed by the JVM; Python commonly compiles to
bytecode and runs it on a virtual machine.

### Q10. What is a syntax error versus a runtime error versus a logical error?

**Answer:** - **Syntax error:** The code violates language grammar. -
**Runtime error:** A problem occurs during execution, such as accessing
an invalid index. - **Logical error:** The program runs but produces the
wrong result.

### Q11. What is the difference between a statically typed and dynamically typed language?

**Answer:** In a statically typed language, type checking is primarily
performed before execution; in a dynamically typed language, types are
associated with values and checked during execution. C, C++, Java, and
C# are statically typed. Python and JavaScript are dynamically typed.
TypeScript adds static type checking to JavaScript development, but its
types are generally erased at runtime.

### Q12. What is the difference between strong typing and static typing?

**Answer:** Static typing concerns when types are checked. Strong typing
concerns how strictly operations respect type distinctions. They are
separate dimensions; a language can be statically typed without having
every possible strictness property associated with "strong typing."

### Q13. What is pass by value versus pass by reference?

**Answer:** Pass by value gives a function a copy of an argument's
value. Pass by reference lets the function access the original variable
through a reference-like mechanism. Language details matter: Java passes
all arguments by value, including object references; C# supports value
passing by default and explicit `ref`/`out`; C++ supports references and
pointers. Python passes object references by assignment, so a function
can mutate a mutable object but cannot rebind the caller's variable.

### Q14. What is recursion?

**Answer:** Recursion is when a function calls itself directly or
indirectly. It needs a base case to stop and a recursive case that makes
progress toward the base case. It can make tree and divide-and-conquer
problems easier to express, but it may use stack space and can overflow
if the recursion is too deep.

### Q15. What is the difference between a loop and recursion?

**Answer:** Loops repeat a block using iteration; recursion repeats work
through function calls. Loops often use less call-stack memory, while
recursion can express tree traversal and divide-and-conquer algorithms
more naturally.

### Q16. What is exception handling?

**Answer:** Exception handling provides a controlled way to respond to
exceptional conditions. Common constructs include `try`,
`catch`/`except`, and `finally`. Exceptions should not be used to hide
programming errors or replace ordinary control flow unnecessarily.

### Q17. What is debugging?

**Answer:** Debugging is the systematic process of finding and fixing
the cause of incorrect behavior. I reproduce the problem, inspect inputs
and state, isolate the relevant code, use logs or a debugger, test a
fix, and check that the fix does not break other cases.

## 2.2 C and C++

### Q18. What is the difference between C and C++?

**Answer:** C is primarily a procedural language. C++ supports
procedural programming as well as object-oriented and generic
programming, including classes, inheritance, templates, and the Standard
Template Library (STL). Both provide low-level control, but C++ has
richer abstractions and resource-management features.

### Q19. What is a pointer?

**Answer:** A pointer stores a memory address. In C and C++, pointers
can be used for dynamic memory, arrays, and low-level operations.
Incorrect pointer use can cause invalid memory access, dangling
pointers, or memory corruption.

### Q20. What is the difference between a pointer and a reference in C++?

**Answer:** A pointer stores an address and can generally be reassigned
or set to `nullptr`. A reference is an alias for an existing object and
must be initialized when declared. References are often preferable when
nullability or reseating is not required.

### Q21. What is a null pointer?

**Answer:** A null pointer does not point to a valid object. In modern
C++, use `nullptr` rather than `NULL` or `0` for a null pointer.
Dereferencing a null pointer is invalid.

### Q22. What is the difference between stack and heap memory?

**Answer:** The stack commonly stores function-call frames and local
variables with automatic lifetime. The heap is used for dynamically
allocated memory whose lifetime is controlled separately. Exact
implementation details vary. In C++, prefer RAII and smart pointers over
manual `new`/`delete` where possible.

### Q23. What is a memory leak?

**Answer:** A memory leak occurs when dynamically allocated memory is no
longer needed but is not released and cannot be reused by the program.
In C++, RAII, containers, and smart pointers help manage resource
lifetimes safely.

### Q24. What is the difference between `malloc()` and `new`?

**Answer:** `malloc()` allocates raw memory and returns a `void*` in C;
it does not call C++ constructors. `new` allocates memory and constructs
an object, returning a typed pointer and throwing an exception on
allocation failure by default. `free()` pairs with `malloc()`, while
`delete` pairs with `new` and `delete[]` with `new[]`. Do not mix these
pairs.

### Q25. What is the difference between an array and a linked list?

**Answer:** Arrays provide fast indexed access, typically O(1), but
inserting in the middle often requires shifting elements, O(n). Linked
lists require traversal for indexed access, O(n), but insertion or
deletion can be O(1) once the relevant node is known. Arrays generally
have better cache locality.

### Q26. What is the difference between `struct` and `class` in C++?

**Answer:** Their main language-level difference is default access:
`struct` members and inheritance are public by default; `class` members
and inheritance are private by default. Both can have constructors,
methods, and other class features.

### Q27. What is the difference between `const` and `#define`?

**Answer:** `const` declares an object that cannot be modified through
that name and participates in the type system. `#define` is a
preprocessor substitution and does not create a typed variable. Prefer
typed constants where appropriate.

### Q28. What is undefined behavior in C/C++?

**Answer:** Undefined behavior means the language standard imposes no
requirements on what happens. Examples can include signed integer
overflow in C++, out-of-bounds access, and dereferencing invalid
pointers. Code that seems to work on one machine may fail under another
compiler or optimization level.

## 2.3 Python

### Q29. What are Python's main characteristics?

**Answer:** Python is a high-level, dynamically typed language with
readable syntax, a large standard library, and a broad ecosystem. It is
used for scripting, automation, backend development, data science, and
machine learning.

### Q30. What is the difference between a list and a tuple?

**Answer:** A list is mutable; a tuple is immutable in its element
references. Lists are useful for collections that change, while tuples
can represent fixed groups of values. A tuple is only hashable if all
its elements are hashable.

### Q31. What is the difference between a set and a dictionary?

**Answer:** A set stores unique elements. A dictionary stores key-value
pairs with unique keys. Both are commonly implemented using hash tables
and provide average-case efficient membership or key lookup.

### Q32. What is the difference between `==` and `is` in Python?

**Answer:** `==` checks value equality; `is` checks object identity. Use
`is None` to test for `None`, but do not use `is` as a general
replacement for `==`.

### Q33. What are mutable and immutable objects?

**Answer:** Mutable objects can be changed after creation, such as lists
and dictionaries. Immutable objects cannot be changed in place, such as
strings, integers, and tuples (though a tuple can contain a mutable
object).

### Q34. What is a list comprehension?

**Answer:** It is a concise way to construct a list from an iterable,
optionally applying a condition.

``` python
squares = [n * n for n in range(1, 6)]
```

### Q35. What is a generator?

**Answer:** A generator yields values lazily, usually with `yield`,
instead of building the entire result in memory at once. It is useful
for processing large sequences or streams.

### Q36. What is the difference between a shallow copy and a deep copy?

**Answer:** A shallow copy creates a new outer container but may share
nested objects. A deep copy recursively copies nested objects, subject
to the object's copying behavior.

### Q37. What is the Global Interpreter Lock (GIL)?

**Answer:** In standard CPython builds, the GIL traditionally allows
only one thread at a time to execute Python bytecode within a process.
Threads can still help with I/O-bound tasks. CPU-bound parallelism may
use multiprocessing or other approaches. Python versions and builds can
differ, so describe the runtime you mean.

## 2.4 Java

### Q38. Why is Java called platform-independent?

**Answer:** Java source is compiled into bytecode, which can run on a
compatible Java Virtual Machine (JVM). The JVM is platform-specific, but
the same bytecode can run on different supported platforms.

### Q39. What is the difference between JDK, JRE, and JVM?

**Answer:** - **JVM:** Executes Java bytecode. - **JRE:** Conceptually
includes the JVM and runtime libraries needed to run Java
applications. - **JDK:** Includes development tools such as the compiler
plus runtime components. Modern Java distributions may package these
components differently.

### Q40. What is the difference between `==` and `.equals()` in Java?

**Answer:** For primitives, `==` compares values. For object references,
`==` checks whether both references refer to the same object.
`.equals()` checks logical equality according to the class's
implementation. For strings, use `.equals()` to compare content.

### Q41. Why is `String` immutable in Java?

**Answer:** Immutability improves safety and predictability, enables
safe sharing and string-pool reuse, and helps with use as map keys.
Repeated concatenation in loops may create many intermediate strings;
`StringBuilder` is often more efficient.

### Q42. What is the difference between an interface and an abstract class?

**Answer:** An abstract class can hold instance state and constructors
and can provide shared implementation. An interface defines a contract
and can include abstract, default, static, and private methods under
modern Java. A class can implement multiple interfaces but extend only
one class.

### Q43. What is the difference between checked and unchecked exceptions?

**Answer:** Checked exceptions must be caught or declared by the
compiler's rules. Unchecked exceptions are subclasses of
`RuntimeException` (or `Error`) and are not subject to that requirement.
Use exceptions to communicate meaningful failure conditions.

### Q44. What is garbage collection?

**Answer:** Garbage collection automatically reclaims memory occupied by
objects that are no longer reachable. It reduces manual
memory-management work, but it does not eliminate every
resource-management concern; files and database connections still need
to be closed.

## 2.5 C# and .NET

### Q45. What is .NET?

**Answer:** .NET is a development platform with a runtime, libraries,
languages, and tools for building web, desktop, cloud, and other
applications. C# is a common language used on .NET.

### Q46. What is the CLR?

**Answer:** The Common Language Runtime executes .NET managed code and
provides services such as garbage collection, exception handling, and
runtime type safety.

### Q47. What is the difference between value types and reference types in C#?

**Answer:** Value-type variables contain their value directly or as part
of their containing storage; reference-type variables hold a reference
to an object. Structs and enums are value types; classes, arrays,
delegates, and strings are reference types. Copying a reference does not
duplicate the referenced object.

### Q48. What is the difference between `var` and `dynamic` in C#?

**Answer:** `var` means the compiler infers a static type at compile
time. `dynamic` defers member/type checking for relevant operations
until runtime. `var` does not make a variable dynamically typed.

### Q49. What is the difference between `IEnumerable` and `IQueryable`?

**Answer:** `IEnumerable<T>` supports in-process enumeration.
`IQueryable<T>` represents queries that a provider may translate, for
example into SQL. Query execution and supported operations depend on the
provider; not every LINQ expression can be translated.

### Q50. What is `async`/`await` in C#?

**Answer:** `async` and `await` make asynchronous code easier to write
and read. They are useful for I/O-bound operations such as HTTP and
database calls. They do not automatically make CPU-bound work faster,
and blocking asynchronous code can cause performance problems.

## 2.6 JavaScript and TypeScript

### Q51. What is the difference between `var`, `let`, and `const`?

**Answer:** - `var` is function-scoped (or global-scoped at top level)
and can be redeclared in the same scope. - `let` is block-scoped and can
be reassigned. - `const` is block-scoped and cannot be reassigned after
initialization. A `const` object can still have its properties mutated
unless it is separately made immutable.

### Q52. What is the difference between `null` and `undefined`?

**Answer:** `undefined` commonly indicates a missing or not-yet-assigned
value. `null` is an explicitly assigned absence of value. Their behavior
differs in comparisons and type checks.

### Q53. What is hoisting?

**Answer:** Hoisting describes how declarations are processed before
execution. Function declarations can be called before their textual
position. `var` declarations are hoisted and initialized to `undefined`;
`let` and `const` are in a temporal dead zone until initialized.

### Q54. What is a closure?

**Answer:** A closure is a function together with access to variables
from its surrounding lexical scope, even after the outer function has
returned. Closures are useful for callbacks, data privacy patterns, and
function factories.

### Q55. What is the event loop?

**Answer:** JavaScript commonly runs synchronous code on a call stack
and uses the event loop to coordinate queued callbacks and asynchronous
work. Promise callbacks use the microtask queue, which is generally
processed before the next task callback. Exact host behavior depends on
the browser or Node.js runtime.

### Q56. What is a Promise?

**Answer:** A Promise represents the eventual success or failure of an
asynchronous operation. It can be pending, fulfilled, or rejected.
`.then()`, `.catch()`, and `async`/`await` help manage its result.

### Q57. What is the difference between `map()`, `filter()`, and `reduce()`?

**Answer:** - `map()` transforms each element and returns a result for
each input. - `filter()` selects elements that pass a condition. -
`reduce()` combines elements into an accumulated result.

### Q58. What is TypeScript, and why use it?

**Answer:** TypeScript is a typed superset of JavaScript that adds
compile-time type checking, interfaces, type aliases, generics, and
better editor tooling. It helps catch many mistakes earlier, especially
in large codebases. Types are generally erased from emitted JavaScript
and do not automatically validate untrusted runtime data.

### Q59. What is the difference between `type` and `interface` in TypeScript?

**Answer:** Both can describe object shapes. Interfaces support
declaration merging and are commonly used for object contracts. Type
aliases can represent unions, intersections, primitives, tuples, and
other type expressions. The choice depends on the modeling need and
project conventions.

### Q60. What are `any` and `unknown` in TypeScript?

**Answer:** `any` largely disables type checking for that value.
`unknown` accepts values of any type but requires narrowing or
validation before most operations. Prefer `unknown` when the type is not
yet known.

### Q61. What is `async`/`await` in JavaScript?

**Answer:** An `async` function returns a Promise. `await` pauses that
function's execution until the awaited Promise settles, without blocking
the entire JavaScript thread. Errors can be handled with `try`/`catch`.

------------------------------------------------------------------------

# 3. Object-Oriented Programming (OOP)

### Q62. What are the four pillars of OOP?

**Answer:** 1. **Encapsulation:** Bundling data and methods while
controlling access. 2. **Abstraction:** Exposing essential behavior
while hiding implementation details. 3. **Inheritance:** Deriving a
class from another to reuse or specialize behavior. 4. **Polymorphism:**
Allowing a common interface to have different implementations.

### Q63. What is a class and what is an object?

**Answer:** A class defines a type and its behavior; an object is an
instance of that class with its own state where applicable.

### Q64. What is encapsulation? Give an example.

**Answer:** Encapsulation controls how internal state is accessed and
changed. For example, a `BankAccount` can keep its balance private and
expose `deposit()` and `withdraw()` methods that validate transactions.

### Q65. What is abstraction?

**Answer:** Abstraction exposes what an object can do without requiring
callers to know its internal implementation. For example, a caller uses
`paymentService.pay()` without needing to know every internal
payment-processing step.

### Q66. What is inheritance? What are its disadvantages?

**Answer:** Inheritance allows a derived class to reuse and specialize
behavior from a base class. Deep or poorly designed inheritance can
create tight coupling and fragile hierarchies. Prefer composition when a
"has-a" relationship fits better than an "is-a" relationship.

### Q67. What is polymorphism?

**Answer:** Polymorphism allows the same operation or interface to
behave differently for different object types. Runtime polymorphism
often uses method overriding and dynamic dispatch; compile-time
polymorphism can include method overloading and templates/generics
depending on the language.

### Q68. What is method overloading versus overriding?

**Answer:** **Overloading** uses the same method name with different
parameter lists in a scope or type. **Overriding** supplies a derived
implementation of an inherited virtual/overridable method. Return type
alone generally does not distinguish overloads.

### Q69. What is a constructor?

**Answer:** A constructor initializes an object when it is created.
Constructors may validate required data and establish class invariants.
Constructors do not normally have a return type; exact syntax differs by
language.

### Q70. Can a constructor be overloaded?

**Answer:** Yes, in languages such as Java, C++, and C#, a class can
define multiple constructors with different parameter lists. Python
typically uses `__init__` and can use defaults or class methods for
alternative creation patterns.

### Q71. What is the `this` or `self` reference?

**Answer:** It refers to the current object in languages that use such a
reference. Java, C++, and C# use `this`; Python instance methods
conventionally use `self` as the first parameter name.

### Q72. What is an abstract class?

**Answer:** An abstract class is intended to be a base class and may
contain abstract methods that derived classes must implement. It may
also contain implemented methods and shared state, depending on the
language.

### Q73. What is an interface?

**Answer:** An interface specifies a contract that implementing classes
agree to provide. It supports programming against abstractions rather
than concrete implementations and makes components easier to test and
replace.

### Q74. What is composition versus inheritance?

**Answer:** Inheritance models an "is-a" relationship; composition
models a "has-a" relationship by placing one object inside or using
another. Composition often reduces coupling and makes behavior easier to
vary.

### Q75. What are SOLID principles?

**Answer:** - **S --- Single Responsibility:** A class or module should
have one primary reason to change. - **O --- Open/Closed:** Be open to
extension without unnecessary modification of stable code. - **L ---
Liskov Substitution:** Subtypes should be usable where their base types
are expected without breaking correctness. - **I --- Interface
Segregation:** Prefer focused interfaces over large interfaces clients
do not need. - **D --- Dependency Inversion:** High-level policy should
depend on abstractions rather than concrete low-level details.

### Q76. What is coupling and cohesion?

**Answer:** Coupling describes how strongly modules depend on each
other; lower coupling is often desirable. Cohesion describes how closely
related a module's responsibilities are; high cohesion is generally
desirable.

### Q77. What is the difference between an exception and an error return?

**Answer:** An error return makes failure explicit in a function's
result and can be appropriate for expected outcomes. Exceptions separate
exceptional control flow from ordinary results. The best choice depends
on language conventions, failure frequency, and API design.

### Q78. Explain SOLID using a project example.

**Answer framework:** Pick one real module. Explain how you separated
responsibilities, used an interface or abstraction, avoided a giant
class, or made a new behavior possible without rewriting unrelated code.
Do not invent a design pattern you did not implement.

------------------------------------------------------------------------

# 4. Data Structures and Algorithms (DSA)

### Q79. What is a data structure?

**Answer:** A data structure organizes data so that operations such as
lookup, insertion, deletion, and traversal can be performed efficiently.

### Q80. What is an algorithm?

**Answer:** An algorithm is a finite, well-defined sequence of steps to
solve a problem or compute a result.

### Q81. What is time complexity?

**Answer:** Time complexity describes how an algorithm's running time
grows with input size, often using Big O notation for an upper-bound
growth rate.

### Q82. What is space complexity?

**Answer:** Space complexity describes how memory usage grows with input
size. When discussing auxiliary space, clarify whether the input storage
itself is excluded.

### Q83. Explain O(1), O(log n), O(n), O(n log n), and O(n²).

**Answer:** - **O(1):** Constant growth, such as accessing an array
element by index. - **O(log n):** Logarithmic growth, such as binary
search in a sorted array. - **O(n):** Linear growth, such as scanning an
array. - **O(n log n):** Typical efficient comparison-sorting growth,
such as merge sort. - **O(n²):** Often nested full loops over the same
input, such as a basic pairwise comparison.

These are growth descriptions; actual runtime also depends on constants,
hardware, and implementation.

### Q84. What is the difference between Big O, Big Omega, and Big Theta?

**Answer:** Big O gives an asymptotic upper bound, Big Omega a lower
bound, and Big Theta a tight asymptotic bound when both upper and lower
bounds match.

### Q85. What is the difference between an array and a linked list?

**Answer:** An array has O(1) indexed access and good cache locality,
but middle insertions/deletions may require O(n) shifts. A linked list
has O(n) access by position, but can insert/delete in O(1) when the node
and required links are already known.

### Q86. What is a stack?

**Answer:** A stack follows Last In, First Out (LIFO). Common operations
are push, pop, and peek. Applications include function calls, undo
operations, expression evaluation, and depth-first search.

### Q87. What is a queue?

**Answer:** A queue follows First In, First Out (FIFO). It is used in
scheduling, breadth-first search, and producer-consumer workflows. A
deque supports operations at both ends.

### Q88. What is a hash table?

**Answer:** A hash table maps keys to storage locations using a hash
function. Lookup, insertion, and deletion are typically O(1) on average,
but collisions and poor hash distribution can worsen performance.

### Q89. What is a collision in hashing?

**Answer:** A collision occurs when two keys map to the same hash-table
location. Common strategies include chaining and open addressing.

### Q90. What is binary search? What condition does it need?

**Answer:** Binary search repeatedly halves the search interval and
takes O(log n) time. It requires the search space to have an appropriate
sorted or monotonic property.

### Q91. Compare merge sort and quicksort.

**Answer:** Merge sort has O(n log n) time in best, average, and worst
cases for typical implementations, and often needs O(n) auxiliary space
for arrays. Quicksort is typically O(n log n) on average, but O(n²) in
the worst case with poor pivot behavior; in-place variants can use less
auxiliary storage. Quicksort often performs well in practice due to
locality.

### Q92. What is a stable sorting algorithm?

**Answer:** A stable sort preserves the relative order of equal-key
elements. Stability matters when sorting records by multiple fields in
successive passes.

### Q93. What is the difference between BFS and DFS?

**Answer:** Breadth-first search explores level by level and commonly
uses a queue; on an unweighted graph it finds shortest paths by number
of edges. Depth-first search explores a path deeply before backtracking
and commonly uses recursion or a stack. Both run in O(V + E) with
adjacency lists.

### Q94. What is dynamic programming?

**Answer:** Dynamic programming solves problems by storing solutions to
overlapping subproblems. It is useful when a problem has overlapping
subproblems and optimal substructure. Approaches include memoization
(top-down) and tabulation (bottom-up).

### Q95. What is a greedy algorithm?

**Answer:** A greedy algorithm makes a locally best choice at each step.
It is correct only when the problem has properties that justify those
choices; a locally optimal choice does not always lead to a global
optimum.

### Q96. What is recursion's time and space complexity?

**Answer:** It depends on the recurrence and number of calls. For
example, binary search has O(log n) time and O(log n) call-stack space
recursively. A naive recursive Fibonacci implementation has exponential
time and O(n) maximum call-stack depth.

### Q97. How do you approach a coding question in an interview?

**Answer:** 1. Clarify inputs, outputs, constraints, and edge cases. 2.
Give a simple approach first. 3. Improve it if necessary and explain the
trade-off. 4. Walk through an example. 5. Write readable code. 6. Test
normal, boundary, and invalid cases. 7. State time and space complexity.

### Q98. What edge cases do you check?

**Answer:** Empty input, one element, duplicates, negative numbers,
already sorted or reverse-sorted data, very large values, invalid input
where relevant, and boundary constraints.

------------------------------------------------------------------------

# 5. Databases: MySQL and MongoDB

## 5.1 Database Fundamentals

### Q99. What is a database?

**Answer:** A database is an organized collection of data managed so it
can be stored, queried, updated, and protected.

### Q100. What is the difference between DBMS and RDBMS?

**Answer:** A DBMS manages data. An RDBMS organizes data primarily in
related tables and commonly supports relational constraints and SQL.
MySQL is an RDBMS; MongoDB is a document-oriented NoSQL database.

### Q101. What is SQL?

**Answer:** SQL is a language used to define, query, and manipulate data
in relational database systems.

### Q102. What is a primary key?

**Answer:** A primary key uniquely identifies each row in a table and
cannot contain `NULL`. A table has one primary-key constraint, which may
consist of multiple columns.

### Q103. What is a foreign key?

**Answer:** A foreign key enforces a relationship by requiring values to
match a referenced key, subject to the database's rules. It helps
maintain referential integrity.

### Q104. What is the difference between primary key and unique key?

**Answer:** A primary key identifies rows and cannot be `NULL`. A unique
constraint prevents duplicate values, but `NULL` handling varies by
database and constraint implementation. A table can have multiple unique
constraints but only one primary-key constraint.

### Q105. What is normalization?

**Answer:** Normalization organizes relational data to reduce
unnecessary duplication and update anomalies. Common forms include 1NF,
2NF, and 3NF.

### Q106. Explain 1NF, 2NF, and 3NF.

**Answer:** - **1NF:** Each field contains an appropriate atomic value;
no repeating groups. - **2NF:** In 1NF, and every non-prime attribute is
fully dependent on the whole candidate key (no partial dependency on
part of a composite candidate key). - **3NF:** In 2NF, and non-key
attributes do not have inappropriate transitive dependencies on
candidate keys; the formal definition is based on functional
dependencies.

### Q107. What is denormalization?

**Answer:** Denormalization intentionally introduces redundancy or
precomputed data to improve selected read patterns. It can speed reads
but increases storage and the complexity of keeping data consistent.

### Q108. What are ACID properties?

**Answer:** - **Atomicity:** A transaction happens as a unit or is
rolled back. - **Consistency:** A transaction preserves defined
integrity rules. - **Isolation:** Concurrent transactions are controlled
according to an isolation level. - **Durability:** Committed changes
persist according to the system's guarantees.

### Q109. What is an index?

**Answer:** An index is an auxiliary data structure that speeds up
selected lookups, filters, joins, or sorts. It consumes storage and adds
work to writes, so indexes should be designed for actual query patterns.

### Q110. What is a transaction?

**Answer:** A transaction is a logical unit of database work that
commits as a whole or rolls back. Transfers between accounts are a
classic example: both sides should succeed together or neither should be
committed.

### Q111. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

**Answer:** `DELETE` removes selected rows and supports a `WHERE`
clause. `TRUNCATE` removes all rows efficiently in systems that support
it, with behavior around logging, identity counters, and rollback
depending on the database. `DROP` removes the table object itself. Exact
behavior is database-specific.

### Q112. What is `NULL` in SQL?

**Answer:** `NULL` represents missing or unknown information, not zero
or an empty string. Use `IS NULL` or `IS NOT NULL`; comparisons such as
`column = NULL` do not work as ordinary equality checks.

### Q113. What is the difference between `WHERE` and `HAVING`?

**Answer:** `WHERE` filters rows before grouping. `HAVING` filters
groups after grouping and is commonly used with aggregate conditions.

### Q114. What is the difference between `GROUP BY` and `ORDER BY`?

**Answer:** `GROUP BY` groups rows so aggregates can be calculated per
group. `ORDER BY` sorts the result set.

## 5.2 SQL Queries and Joins

Assume these example tables:

``` sql
Employee(EmpID, Name, Salary, DeptID, ManagerID)
Department(DeptID, DeptName)
```

### Q115. How do you find the second-highest distinct salary?

**Answer --- using a subquery:**

``` sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);
```

This returns `NULL` if there is no lower distinct salary.

**Alternative --- using `DENSE_RANK()`:**

``` sql
SELECT Salary
FROM (
    SELECT Salary,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
    FROM Employee
) AS ranked
WHERE rnk = 2;
```

If multiple employees share the second-highest salary, this returns each
matching row. Use `SELECT DISTINCT Salary` in the inner query if only
the salary value is required.

### Q116. What is an INNER JOIN?

**Answer:** It returns rows where the join condition matches in both
tables.

``` sql
SELECT e.Name, d.DeptName
FROM Employee e
INNER JOIN Department d
    ON e.DeptID = d.DeptID;
```

### Q117. What is a LEFT JOIN?

**Answer:** It returns every row from the left table and matching rows
from the right table. When no match exists, right-table columns are
`NULL`.

``` sql
SELECT e.Name, d.DeptName
FROM Employee e
LEFT JOIN Department d
    ON e.DeptID = d.DeptID;
```

### Q118. What is a self join?

**Answer:** A self join joins a table to itself using aliases. It can
represent employee-manager relationships.

``` sql
SELECT e.Name AS Employee, m.Name AS Manager
FROM Employee e
LEFT JOIN Employee m
    ON e.ManagerID = m.EmpID;
```

### Q119. What happens if I write `ON e.DeptID = 10` in a join?

**Answer:** This condition does not compare employee department IDs with
the department table. It matches employee rows whose `DeptID` is 10
against every row from the other table that survives the join structure,
because the condition references only `e`. For a simple cross join
between the filtered employees and all department rows, this can produce
many repeated combinations. Usually the intended condition is
`ON e.DeptID = d.DeptID`, with `WHERE e.DeptID = 10` if you also want to
filter employees to department 10.

### Q120. What is the difference between `UNION` and `UNION ALL`?

**Answer:** `UNION` combines results and removes duplicate rows.
`UNION ALL` keeps duplicates and is usually cheaper when deduplication
is unnecessary. Corresponding SELECT statements must have compatible
column counts and types.

### Q121. What is a window function?

**Answer:** A window function calculates a value across related rows
without collapsing them into one row per group. Examples include
`ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, and running totals.

### Q122. Compare `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`.

**Answer:** For values sorted as 100, 100, 90: - `ROW_NUMBER()`: 1, 2,
3 - `RANK()`: 1, 1, 3 - `DENSE_RANK()`: 1, 1, 2

Ties receive the same rank for `RANK()` and `DENSE_RANK()`, but `RANK()`
leaves gaps.

### Q123. How do you find duplicate email addresses?

**Answer:**

``` sql
SELECT Email, COUNT(*) AS Total
FROM Users
GROUP BY Email
HAVING COUNT(*) > 1;
```

### Q124. How do you find employees earning more than their department's average salary?

**Answer:**

``` sql
SELECT e.*
FROM Employee e
WHERE e.Salary > (
    SELECT AVG(e2.Salary)
    FROM Employee e2
    WHERE e2.DeptID = e.DeptID
);
```

### Q125. What is SQL injection, and how do you prevent it?

**Answer:** SQL injection occurs when untrusted input is interpreted as
part of SQL syntax. Use parameterized queries or prepared statements,
avoid concatenating user input into SQL, apply least-privilege database
permissions, and validate input where appropriate. Validation alone is
not a replacement for parameterization.

## 5.3 MongoDB

### Q126. What is MongoDB?

**Answer:** MongoDB is a document-oriented NoSQL database that stores
records as BSON documents, with flexible document structures and
query/index capabilities.

### Q127. What is a document and a collection?

**Answer:** A document is a record made of field-value pairs. A
collection is a group of documents, similar in broad purpose to a
relational table, though documents in a collection need not all have
identical fields.

### Q128. What is the difference between SQL and MongoDB?

**Answer:** Relational databases organize data into tables with defined
relationships and commonly use joins. MongoDB stores documents and can
embed related data or reference other documents. The best choice depends
on relationships, query patterns, consistency needs, and operational
requirements.

### Q129. What is embedding versus referencing in MongoDB?

**Answer:** Embedding stores related data inside one document and can
make related reads atomic and efficient. Referencing stores identifiers
to related documents and can reduce duplication or support independently
managed entities. Choose based on access patterns, size, update
frequency, and consistency requirements.

### Q130. What is an aggregation pipeline?

**Answer:** It processes documents through ordered stages such as
`$match`, `$group`, `$project`, `$sort`, and `$lookup` to filter,
transform, combine, and summarize data.

### Q131. What is an index in MongoDB?

**Answer:** An index supports efficient queries and sorts on selected
fields. Indexes use storage and add write overhead. Check query plans
and actual access patterns when designing them.

### Q132. What is the purpose of MongoDB's `_id` field?

**Answer:** `_id` uniquely identifies a document within a collection.
MongoDB creates an ObjectId by default if the application does not
supply another value.

### Q133. Does MongoDB mean you never need schema validation?

**Answer:** No. Flexible schema does not mean no schema discipline.
Applications can use MongoDB validation rules and application-level
validation to maintain required fields, types, and business constraints.

------------------------------------------------------------------------

# 6. Web Technologies

## 6.1 HTML and CSS

### Q134. What is HTML?

**Answer:** HTML defines the structure and meaning of web content using
elements such as headings, forms, links, and tables.

### Q135. What is semantic HTML?

**Answer:** Semantic HTML uses elements according to their meaning, such
as `header`, `nav`, `main`, `article`, and `footer`. It improves
accessibility, maintainability, and document structure.

### Q136. What is the difference between `div` and `span`?

**Answer:** Both are generic containers. `div` is block-level by
default, while `span` is inline by default. Prefer semantic elements
when they express the content's meaning.

### Q137. What is the difference between `id` and `class`?

**Answer:** An `id` identifies one element uniquely within a document; a
class can be shared by multiple elements. CSS selectors and JavaScript
can use both.

### Q138. What is the CSS box model?

**Answer:** It describes an element's content area, padding, border, and
margin. With `box-sizing: border-box`, declared width and height include
content, padding, and border.

### Q139. What is the difference between Flexbox and CSS Grid?

**Answer:** Flexbox is primarily designed for one-dimensional layout (a
row or column). Grid is designed for two-dimensional row-and-column
layouts. They can be used together.

### Q140. How do you make a website responsive?

**Answer:** Use flexible layouts, relative sizing, media queries,
responsive images, and suitable breakpoints. Test on different viewport
sizes and ensure content remains readable and controls usable.

### Q141. What is CSS specificity?

**Answer:** Specificity helps determine which selector wins when
declarations conflict, along with cascade origin, importance, layers,
and source order. Inline styles and `!important` have special cascade
behavior; avoid relying on them unnecessarily.

### Q142. What is the difference between `display: none` and `visibility: hidden`?

**Answer:** `display: none` removes the element from layout.
`visibility: hidden` hides it but generally preserves its layout space.

## 6.2 React

### Q143. What is React?

**Answer:** React is a JavaScript library for building user interfaces
from reusable components. It updates the UI based on component state and
props.

### Q144. What is a component?

**Answer:** A component is a reusable piece of UI, often written as a
function that returns JSX. It can receive props and manage state.

### Q145. What is JSX?

**Answer:** JSX is a syntax extension that lets developers describe UI
using markup-like expressions in JavaScript. Build tools transform it
into JavaScript calls understood by React.

### Q146. What is the difference between props and state?

**Answer:** Props are inputs passed from a parent component and should
be treated as read-only. State is data managed by a component or hook
that can change over time and trigger re-rendering.

### Q147. What is the `useState` hook?

**Answer:** `useState` adds state to a function component. Updating
state requests a re-render; when the next value depends on the previous
value, use the functional form such as `setCount(c => c + 1)`.

### Q148. What is `useEffect` used for?

**Answer:** `useEffect` synchronizes a component with external systems,
such as subscriptions, browser APIs, or network interactions. Its
dependencies determine when it re-runs. Avoid using effects for values
that can be calculated directly during rendering.

### Q149. Why are keys needed when rendering lists?

**Answer:** Keys help React identify which list items persist, move, or
change between renders. Use stable identifiers where possible; array
indices can cause issues when items are reordered or inserted.

### Q150. What is a controlled component?

**Answer:** A controlled form element gets its value from React state
and updates that state through an event handler. This makes validation
and UI behavior easier to coordinate.

### Q151. What is the Virtual DOM?

**Answer:** It is a conceptual representation of the UI that React uses
to determine updates. It is not accurate to claim that the Virtual DOM
makes every React operation automatically faster; performance depends on
component structure and rendering work.

### Q152. What is prop drilling?

**Answer:** Prop drilling is passing props through multiple intermediate
components that do not need them directly. Possible solutions include
component composition, Context, or a state-management library when
justified.

### Q153. How do you improve React performance?

**Answer:** First measure the problem. Then consider stable keys,
avoiding unnecessary state, splitting large components, memoization when
it actually helps, list virtualization for large lists, and code
splitting. `memo`, `useMemo`, and `useCallback` are not automatic
improvements in every case.

### Q154. How do you handle API calls in React?

**Answer:** Call the API through an appropriate data-fetching approach,
represent loading/success/error states, handle cancellation or stale
responses when needed, validate data, and avoid exposing secrets in
client-side code.

## 6.3 Node.js and Express.js

### Q155. What is Node.js?

**Answer:** Node.js is a JavaScript runtime built on the V8 engine. It
is commonly used for server-side applications and I/O-heavy services.
Its event-driven, non-blocking I/O model can handle many concurrent
connections, but CPU-heavy work can still block an event loop.

### Q156. Is Node.js single-threaded?

**Answer:** JavaScript execution for a typical Node.js application runs
on an event-loop thread, but Node.js also uses operating-system
facilities and a worker pool for some operations and supports worker
threads. Therefore, saying "Node.js is completely single-threaded" is
misleading.

### Q157. What is Express.js?

**Answer:** Express is a web framework for Node.js that provides
routing, middleware, and request/response helpers for building APIs and
web servers.

### Q158. What is middleware in Express?

**Answer:** Middleware is a function that can inspect or modify the
request/response, end the response, or pass control onward using
`next()`. Common uses include authentication, logging, validation, and
error handling.

### Q159. What is the difference between PUT and PATCH?

**Answer:** PUT generally replaces the target resource's representation
and is intended to be idempotent. PATCH applies partial modifications.
Actual API semantics should be documented consistently.

### Q160. What is REST?

**Answer:** REST is an architectural style for networked systems. A
RESTful API typically models resources, uses standard HTTP methods,
communicates representations, and is stateless at the application
interaction level.

### Q161. What are common HTTP methods?

**Answer:** - `GET`: Retrieve a representation. - `POST`: Submit data or
request processing, often creating a resource. - `PUT`: Replace a
resource representation. - `PATCH`: Partially update a resource. -
`DELETE`: Request resource deletion.

### Q162. What are common HTTP status codes?

**Answer:** - `200 OK`: Successful request. - `201 Created`: Resource
created. - `204 No Content`: Success without a response body. -
`400 Bad Request`: Invalid request. - `401 Unauthorized`: Authentication
is missing or invalid. - `403 Forbidden`: The server refuses the
request. - `404 Not Found`: Resource not found. - `409 Conflict`:
Conflict with current resource state. - `422 Unprocessable Content`:
Content cannot be processed semantically, where used. -
`429 Too Many Requests`: Rate limit exceeded. -
`500 Internal Server Error`: Unexpected server failure.

### Q163. How should an Express API handle errors?

**Answer:** Validate input, return appropriate status codes and safe
messages, log diagnostic details on the server, and use centralized
error-handling middleware. Do not expose stack traces, credentials, or
sensitive internals to clients.

### Q164. How do you validate API input?

**Answer:** Validate types, required fields, length, formats, allowed
values, and business rules at the server boundary. Use a validation
library or schema where appropriate. Never rely solely on frontend
validation.

### Q165. What is CORS?

**Answer:** Cross-Origin Resource Sharing is a browser-enforced
mechanism that uses HTTP headers to control which origins can read
responses to cross-origin requests. CORS is not authentication and does
not prevent non-browser clients from calling an API.

### Q166. What is the difference between authentication and authorization?

**Answer:** Authentication answers "Who are you?" Authorization answers
"What are you allowed to do?" A valid login does not automatically grant
permission to every resource or operation.

## 6.4 JWT and Authentication

### Q167. What is JWT?

**Answer:** JSON Web Token is a compact token format commonly used to
convey claims. A signed JWT can provide integrity/authenticity, but its
payload is normally readable and is not encrypted by default.

### Q168. What are the parts of a JWT?

**Answer:** A common signed JWT has three Base64URL-encoded parts:
header, payload, and signature, separated by dots. The header describes
the token type and algorithm; the payload contains claims; the signature
helps verify integrity and issuer authenticity when validated correctly.

### Q169. Is JWT encrypted?

**Answer:** Not necessarily. A typical signed JWT is not encrypted. Do
not place passwords, secret keys, or sensitive private data in its
payload.

### Q170. How does JWT authentication work?

**Answer:** After credentials are verified, the server issues a token.
The client sends it on later requests, often in an
`Authorization: Bearer` header. The server validates the signature,
expiry, issuer/audience where applicable, and authorization rules before
serving protected data.

### Q171. Where should a token be stored in a browser?

**Answer:** The answer depends on the threat model.
JavaScript-accessible storage such as `localStorage` is vulnerable to
token theft if an XSS vulnerability exists. `HttpOnly`, `Secure`,
appropriately configured `SameSite` cookies reduce JavaScript access but
require careful CSRF and cookie configuration. Avoid claiming any
storage method is universally secure.

### Q172. What is an access token versus a refresh token?

**Answer:** An access token is used to access protected resources and is
often short-lived. A refresh token is used to obtain new access tokens
and should be protected more carefully, rotated or revoked according to
the design, and never exposed unnecessarily.

### Q173. What is password hashing, and why not store plain-text passwords?

**Answer:** Passwords should be stored using a dedicated
password-hashing algorithm such as Argon2id, bcrypt, or scrypt with
suitable parameters and salts. Plain-text storage exposes users if the
database is leaked. General-purpose fast hashes such as plain SHA-256
are not appropriate password-storage substitutes.

### Q174. What is rate limiting?

**Answer:** Rate limiting restricts how many requests a client can make
within a period. It can reduce abuse, brute-force attempts, and
accidental overload. It should be combined with authentication,
monitoring, and appropriate per-route policies.

------------------------------------------------------------------------

# 7. Git, GitHub, and Developer Tools

### Q175. What is Git?

**Answer:** Git is a distributed version-control system that records
project history and supports branching, merging, collaboration, and
recovery from mistakes.

### Q176. What is the difference between Git and GitHub?

**Answer:** Git is the version-control tool. GitHub is a hosting and
collaboration platform for Git repositories, with features such as pull
requests, issues, and code review.

### Q177. Explain `git clone`, `git pull`, and `git fetch`.

**Answer:** - `git clone` creates a local copy of a remote repository. -
`git fetch` downloads remote updates without integrating them into the
current branch. - `git pull` fetches and then integrates changes,
typically by merge or rebase depending on configuration.

### Q178. What is the difference between `git add`, `git commit`, and `git push`?

**Answer:** `git add` stages changes; `git commit` records a local
snapshot; `git push` sends local commits to a remote repository.

### Q179. What is a branch?

**Answer:** A branch is a movable reference to a line of development.
Branches allow features or fixes to be developed independently before
integration.

### Q180. What is a merge conflict?

**Answer:** A merge conflict occurs when Git cannot automatically
reconcile overlapping changes. Inspect the conflict markers, decide the
intended combined code, remove markers, run tests, and commit the
resolution.

### Q181. What is `.gitignore`?

**Answer:** It lists untracked files and patterns Git should ignore,
such as build output, local environment files, or dependencies. It does
not automatically stop tracking files already committed.

### Q182. How do you remove a secret accidentally committed to GitHub?

**Answer:** Revoke or rotate the secret immediately; deleting it in a
new commit does not remove it from history. Then follow the
repository-hosting platform's history-cleanup guidance if needed,
coordinate with collaborators, and review logs for misuse. Never put
secrets in a public repository.

### Q183. What is a pull request?

**Answer:** A pull request proposes changes for review and integration.
It enables discussion, automated checks, and code review before merging.

### Q184. What do you use Postman for?

**Answer:** Postman helps send HTTP requests and inspect responses,
headers, status codes, and payloads. It is useful for testing APIs
independently of a frontend, saving request collections, and checking
authentication and error cases.

### Q185. What is the difference between VS Code and Visual Studio?

**Answer:** VS Code is a lightweight, extensible code editor. Visual
Studio is a full IDE with deeper integrated tooling, particularly for
.NET and Windows development. Their exact features depend on edition and
installed extensions.

------------------------------------------------------------------------

# 8. AWS and Cloud Computing

### Q186. What is cloud computing?

**Answer:** Cloud computing provides on-demand access to computing
resources such as servers, storage, databases, networking, and managed
services, typically with usage-based pricing.

### Q187. What are IaaS, PaaS, and SaaS?

**Answer:** - **IaaS:** Rent infrastructure such as virtual machines and
networks. - **PaaS:** Use a managed platform to deploy applications
without managing as much underlying infrastructure. - **SaaS:** Use a
complete application delivered as a service.

### Q188. What is AWS?

**Answer:** Amazon Web Services is a cloud platform offering compute,
storage, networking, databases, identity/security, analytics, and many
other services.

### Q189. What is the difference between EC2 and S3?

**Answer:** EC2 provides virtual compute instances. S3 provides object
storage for files and data objects. S3 is not a traditional mounted
relational database or a general-purpose virtual machine disk.

### Q190. What is IAM?

**Answer:** AWS Identity and Access Management controls identities and
permissions. Follow least privilege: grant only the actions and
resources needed, avoid sharing root credentials, and prefer temporary
credentials/roles where appropriate.

### Q191. What is an AWS Region and Availability Zone?

**Answer:** A Region is a separate geographic area. An Availability Zone
is an isolated location within a Region, designed to help build
fault-tolerant systems. Deploying across multiple AZs can improve
resilience, but application architecture must actually use them
appropriately.

### Q192. What is a VPC?

**Answer:** A Virtual Private Cloud is a logically isolated network in
AWS where you define IP ranges, subnets, routes, and network controls.

### Q193. What is the difference between a security group and a network ACL?

**Answer:** Security groups are stateful controls associated with
network interfaces/resources. Network ACLs operate at the subnet level
and are stateless, so inbound and outbound rules must be considered
separately.

### Q194. What is serverless computing?

**Answer:** Serverless lets developers run code or use managed services
without provisioning and maintaining servers directly. The cloud
provider still operates servers underneath. AWS Lambda is a common
example.

### Q195. How would you deploy a web application to AWS?

**Answer:** First identify the architecture and requirements. A static
frontend might use S3 with CloudFront; a backend might run on a managed
application service, containers, Lambda, or EC2; a database might use
RDS or a suitable managed database. Configure IAM, networking, HTTPS,
secrets, logs, monitoring, backups, and budgets. The exact design
depends on traffic, security, and cost requirements.

### Q196. How do you avoid unexpected AWS charges?

**Answer:** Understand each service's pricing, set billing alerts and
budgets, stop or delete unused resources, inspect storage and
data-transfer costs, use least-privilege access, and regularly review
the billing dashboard. A free tier is not a guarantee that every
configuration is free.

------------------------------------------------------------------------

# 9. Docker and Containers

### Q197. What is Docker?

**Answer:** Docker is a platform and toolset for packaging and running
applications in containers with their dependencies and configuration.

### Q198. What is a container?

**Answer:** A container is an isolated running process that shares the
host operating-system kernel. It is generally lighter than a full
virtual machine, which runs its own guest OS kernel.

### Q199. What is the difference between an image and a container?

**Answer:** An image is a packaged, usually immutable template. A
container is a running or stopped instance created from an image, with
its own writable layer and runtime configuration.

### Q200. What is a Dockerfile?

**Answer:** A Dockerfile describes steps to build an image, using
instructions such as `FROM`, `WORKDIR`, `COPY`, `RUN`, `ENV`, and `CMD`.

### Q201. What is the difference between `CMD` and `ENTRYPOINT`?

**Answer:** `ENTRYPOINT` defines the main executable, while `CMD`
provides default arguments or a default command. They can be combined;
exact behavior depends on shell versus exec form.

### Q202. What is a Docker volume?

**Answer:** A volume persists data outside a container's writable layer
and can be reused across container replacements. This is useful for
database data and other persistent files.

### Q203. What is port mapping in Docker?

**Answer:** Port mapping exposes a container port through a host port,
for example `-p 3000:3000`. It allows clients to reach a service running
inside the container, subject to host/network configuration.

### Q204. What is a multi-stage build?

**Answer:** A multi-stage build uses multiple `FROM` stages so build
tools and intermediate files can be excluded from the final image. It
can reduce image size and limit unnecessary components in production.

### Q205. Why might a Docker container work locally but fail in production?

**Answer:** Potential causes include environment variables, missing
secrets, incorrect port binding, incompatible architecture, network
rules, filesystem permissions, missing files, dependency differences, or
incorrect health checks. Reproduce the environment and inspect logs,
configuration, and container exit status.

### Q206. Is Docker the same as Kubernetes?

**Answer:** No. Docker is commonly used to build and run containers.
Kubernetes orchestrates containerized workloads across a cluster,
handling scheduling, service discovery, scaling, and recovery. They
solve related but different problems.

------------------------------------------------------------------------

# 10. Practical Scenario Questions

### Q207. Your API works in Postman but not in the React frontend. What do you check?

**Answer:** Check the browser console and network tab, API URL, HTTP
method, headers, payload, CORS configuration, authentication token,
status code, and server logs. Confirm that the frontend is not calling
the wrong port or environment.

### Q208. An API is slow. How do you investigate?

**Answer:** Measure the request duration, inspect logs and traces,
separate application time from database and network time, examine query
plans and indexes, check external dependencies, and profile CPU or
memory if needed. Optimize the measured bottleneck rather than guessing.

### Q209. A database query became slow after adding data. Why?

**Answer:** The query may now scan many rows, use an unsuitable index,
sort or join large datasets, or return too much data. Check the
execution plan, cardinality, index selectivity, and query pattern.

### Q210. Users report duplicate records being created. What do you do?

**Answer:** Reproduce the issue, identify whether duplicate requests or
race conditions are possible, enforce suitable database uniqueness
constraints, make operations idempotent where appropriate, and handle
duplicate-key errors cleanly. Frontend button disabling alone is not
enough.

### Q211. A secret appears in a frontend JavaScript bundle. Is it safe because the repository is private?

**Answer:** No. Anything shipped to a browser can be inspected by users.
Move secrets to a trusted backend or secret manager, rotate exposed
credentials, and review access logs.

### Q212. How would you secure a REST API?

**Answer:** Use HTTPS, strong authentication, per-resource
authorization, input validation, parameterized database access, rate
limiting, safe error messages, secure secret management, dependency
updates, logging/monitoring, and appropriate CORS configuration.
Security is layered; no single measure is sufficient.

### Q213. How would you design login and registration?

**Answer:** Validate input on the server, normalize identifiers
consistently, hash passwords with a password-hashing algorithm, enforce
unique accounts, issue short-lived credentials according to the
authentication design, rate-limit sensitive endpoints, and avoid
revealing whether an account exists when that creates a security risk.
Add verification and recovery flows as required.

### Q214. What would you do if you did not know an answer in an interview?

**Answer:** State what you know, explain how you would reason about the
problem, and be clear about what you have not used. For example: "I have
not implemented that feature yet. My current understanding is ... I
would verify the exact behavior in the official documentation and test a
small example." Do not bluff.

### Q215. A technology is listed on your resume, but you have only studied the basics. What should you say?

**Answer:** Be transparent: "I have foundational knowledge of it and
have practised \[specific topics\]. I have not yet used it extensively
in production, but I can explain the fundamentals and am actively
building practical experience." Adjust the wording to match the truth.

------------------------------------------------------------------------

# 11. HR and Resume-Credibility Questions

### Q216. Why should we hire you as a fresher?

**Sample answer:** "I bring a foundation in programming, databases, web
development, and problem-solving. I am willing to learn the team's
stack, take feedback, and work through unfamiliar technical problems
systematically. I can support my skills with examples from my actual
projects and coursework."

### Q217. What is your biggest technical strength?

**Sample answer:** "My biggest strength is \[real strength\]. For
example, in \[real project or assignment\], I used it to \[specific
action\] and learned \[specific result\]."

### Q218. What is one technical weakness you are improving?

**Sample answer:** "I am currently improving \[specific area\]. I
noticed the gap when \[real example\], so I am addressing it through
\[practice plan or project\]." Choose a genuine, manageable development
area.

### Q219. How do you learn a new technology?

**Answer:** Start with the official documentation and core concepts,
build a small working example, use it in a practical task, test edge
cases, and record what you learn. When debugging, reduce the problem to
a minimal reproducible case.

### Q220. Describe a technical challenge you faced.

**Answer framework (STAR):** - **Situation:** What project or problem
were you working on? - **Task:** What were you responsible for? -
**Action:** What did you personally investigate and change? -
**Result:** What improved, and what did you learn?

Use a real example and clearly distinguish your contribution from
teammates' work.

### Q221. How do you handle a disagreement during code review?

**Answer:** Discuss the requirements, correctness, readability,
performance, and maintainability. Use tests or measurements where
possible, listen to alternatives, and follow the team's agreed standards
rather than treating feedback as personal criticism.

### Q222. Are you comfortable learning a different technology stack?

**Answer:** "Yes. I would first learn the language and framework
fundamentals, then the team's architecture, coding standards, tests, and
deployment process. My existing programming and web-development
knowledge should help, but I would not assume that different frameworks
work identically."

### Q223. What do you do when a deadline is close?

**Answer:** Clarify the must-have requirements, break work into small
tasks, communicate risks early, prioritize the highest-impact work, test
critical flows, and avoid hiding blockers until the deadline.

### Q224. How do you ensure your code quality?

**Answer:** Use clear naming and small functions, validate inputs,
handle errors, test normal and edge cases, review changes, use version
control, and follow project conventions. Where available, use automated
tests, linters, and CI checks.

------------------------------------------------------------------------

# 12. Questions You Should Ask the Interviewer

Choose one or two that fit the conversation: 1. What would success look
like for a fresher in the first three months? 2. Which technologies and
tools does the team use most frequently? 3. How are code reviews,
testing, and mentoring handled? 4. What kinds of projects would the
selected candidate work on first? 5. What are the next steps in the
selection process?

------------------------------------------------------------------------

# 13. Last-Minute Revision Checklist

Before the interview, make sure you can explain or demonstrate:

-   [ ] One programming language well: variables, loops, functions,
    arrays, strings, exceptions, and basic coding problems.
-   [ ] OOP: four pillars, overloading versus overriding, interfaces,
    abstract classes, composition, and SOLID.
-   [ ] DSA: arrays, strings, hash maps, stacks, queues, linked lists,
    sorting, binary search, trees/graphs basics, and complexity.
-   [ ] SQL: joins, grouping, subqueries, keys, normalization, indexes,
    transactions, `NULL`, and window functions.
-   [ ] MongoDB: documents, collections, CRUD, embedding versus
    referencing, indexes, and aggregation basics.
-   [ ] Web: HTTP methods/status codes, HTML semantics, CSS responsive
    layout, JavaScript scope/closures/promises, and TypeScript types.
-   [ ] React: components, props/state, hooks, keys, forms, and API
    calls.
-   [ ] Node/Express: routing, middleware, validation, error handling,
    authentication, and REST conventions.
-   [ ] JWT: token structure, validation, expiry, storage trade-offs,
    and authorization.
-   [ ] Git: clone, branch, add, commit, push, pull, merge conflicts,
    `.gitignore`, and secret handling.
-   [ ] AWS: EC2, S3, IAM, Regions/AZs, VPC basics, billing, and
    deployment concepts.
-   [ ] Docker: images, containers, Dockerfile, ports, volumes, and
    multi-stage builds.
-   [ ] Resume projects: architecture, your contribution, database
    design, authentication, error handling, trade-offs, and
    improvements.

## Final advice

An interviewer is unlikely to ask every question in this document. They
will usually start with the technologies you claim to know, then probe
deeper based on your answers. A strong candidate explains concepts
clearly, gives a practical example, acknowledges limitations, and
reasons through unfamiliar problems without bluffing.

**Best preparation method:** For every technology on your resume,
prepare (1) a one-minute explanation, (2) one code or project example,
(3) two common mistakes, and (4) one limitation or trade-off.
