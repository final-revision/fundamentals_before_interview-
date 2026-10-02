# .NET & ASP.NET Interview Questions and Answers

## Complete Interview Preparation Guide — C#, .NET, ASP.NET Core, Web API, MVC, EF Core, SQL, Security, Testing, Deployment

> **Target:** Fresher / Internship / Junior .NET Developer  
> **How to use:** Start with Sections 1–8 for core interview preparation, then revise Sections 9–18 for deeper questions and project discussions.

---

# Table of Contents

1. .NET Fundamentals
2. .NET Framework vs .NET Core vs Modern .NET
3. C# Fundamentals
4. OOP in C#
5. Advanced C#
6. Collections, Generics and LINQ
7. Exception Handling
8. ASP.NET Core Fundamentals
9. ASP.NET Core Middleware and Request Pipeline
10. Dependency Injection and Configuration
11. ASP.NET Core MVC
12. Web API / REST API
13. Entity Framework Core
14. SQL and Database Questions
15. Authentication, Authorization and Security
16. Async/Await and Performance
17. Testing, Debugging and Logging
18. Deployment, Docker and Production
19. Common Practical Coding Questions
20. Project-Based Interview Questions
21. Rapid-Fire Questions
22. Important Differences to Memorize
23. Final Revision Checklist

---

# 1. .NET Fundamentals

## Q1. What is .NET?

**Answer:**  
.NET is a software development platform from Microsoft used to build applications such as:

- Web applications
- REST APIs
- Desktop applications
- Cloud applications
- Mobile applications
- Background services
- Microservices
- Games and other applications

Modern .NET is cross-platform and can run on Windows, Linux and macOS.

---

## Q2. What is CLR?

**Answer:**  
CLR stands for **Common Language Runtime**.

It is the execution environment for .NET applications. It provides services such as:

- Memory management
- Garbage collection
- Exception handling
- Thread management
- Type safety
- JIT compilation

Example:

```text
C# Code
   ↓
C# Compiler
   ↓
IL / Intermediate Language
   ↓
CLR
   ↓
JIT Compiler
   ↓
Machine Code
```

---

## Q3. What is CTS?

**Answer:**  
CTS stands for **Common Type System**.

It defines how data types are declared and used in the .NET ecosystem.

Examples:

```csharp
int age = 20;
string name = "Digvijay";
bool isActive = true;
```

CTS allows different .NET languages to understand common types.

---

## Q4. What is CLS?

**Answer:**  
CLS stands for **Common Language Specification**.

It defines a set of rules that .NET languages should follow to maintain language interoperability.

For example, C#, VB.NET and F# can interact because they follow common .NET standards.

---

## Q5. What is managed code?

**Answer:**  
Code executed under the control of the CLR is called managed code.

C# code is normally managed code because the CLR handles:

- Memory
- Garbage collection
- Exceptions
- Type safety

---

## Q6. What is unmanaged code?

**Answer:**  
Code that executes outside the CLR is called unmanaged code.

Examples include traditional C/C++ native code.

.NET can interact with unmanaged code using mechanisms such as P/Invoke.

---

## Q7. What is JIT?

**Answer:**  
JIT stands for **Just-In-Time compiler**.

It converts Intermediate Language (IL) into native machine code when the application executes.

---

## Q8. What is garbage collection?

**Answer:**  
Garbage Collection (GC) automatically identifies objects that are no longer reachable and releases their managed memory.

Example:

```csharp
Person p = new Person();
p = null;
```

If no other reference points to the original object, it can eventually be collected by the GC.

---

## Q9. What are GC generations?

**Answer:**

.NET GC commonly uses:

- **Generation 0** — short-lived objects
- **Generation 1** — objects that survived Gen 0
- **Generation 2** — long-lived objects

The idea is that most objects become unused quickly, so collecting younger generations frequently can be efficient.

---

## Q10. What is an assembly?

**Answer:**  
An assembly is a compiled unit of .NET code.

It can be:

- `.dll`
- `.exe`

An assembly contains compiled code and metadata.

---

## Q11. What is a namespace?

**Answer:**  
A namespace organizes related classes, interfaces and other types.

```csharp
namespace MyApplication.Models
{
    public class Employee
    {
    }
}
```

---

## Q12. What is a NuGet package?

**Answer:**  
NuGet is the package management ecosystem for .NET.

It allows developers to install reusable libraries.

Example:

```bash
dotnet add package Microsoft.EntityFrameworkCore
```

---

# 2. .NET Framework vs .NET Core vs Modern .NET

## Q13. What is .NET Framework?

**Answer:**  
.NET Framework is Microsoft's older Windows-focused .NET platform.

It is widely used in legacy enterprise applications, especially older ASP.NET applications.

---

## Q14. What is .NET Core?

**Answer:**  
.NET Core was Microsoft's modern, cross-platform implementation of .NET.

It was designed for:

- Windows
- Linux
- macOS
- High performance
- Cloud applications
- Web APIs

---

## Q15. What is modern .NET?

**Answer:**  
Starting with **.NET 5**, Microsoft unified the product naming under **.NET**.

Examples include:

```text
.NET 5
.NET 6
.NET 7
.NET 8
.NET 9
.NET 10
```

The modern platform is cross-platform and is used for ASP.NET Core applications.

---

## Q16. .NET Framework vs modern .NET

| Feature | .NET Framework | Modern .NET |
|---|---|---|
| Platform | Mainly Windows | Cross-platform |
| Modern development | Legacy-focused | Current platform |
| ASP.NET Core | No | Yes |
| Linux | Limited/not supported as a general runtime | Yes |
| Performance | Older architecture | Modern/high performance |
| Cloud/container usage | Less suitable | Strong support |

---

# 3. C# Fundamentals

## Q17. What is C#?

**Answer:**  
C# is a strongly typed, object-oriented programming language developed by Microsoft for the .NET platform.

It supports:

- OOP
- Generics
- LINQ
- Delegates
- Events
- Async programming
- Pattern matching
- Exception handling

---

## Q18. What is a variable?

**Answer:**

```csharp
int age = 20;
string name = "Digvijay";
```

A variable stores a value in a program.

---

## Q19. Value type vs reference type

**Value types** generally store their value directly.

Examples:

```csharp
int
double
bool
struct
enum
```

**Reference types** contain a reference to an object.

Examples:

```csharp
class
string
array
object
interface
delegate
```

---

## Q20. What is boxing and unboxing?

**Boxing converts a value type to `object`:**

```csharp
int x = 10;
object obj = x;
```

**Unboxing extracts the value type:**

```csharp
int y = (int)obj;
```

Boxing/unboxing can introduce performance and type-safety considerations.

---

## Q21. What is `var`?

**Answer:**  
`var` allows the compiler to infer the type at compile time.

```csharp
var age = 20;
var name = "Digvijay";
```

`var` does not mean the variable is dynamically typed.

---

## Q22. What is `dynamic`?

**Answer:**  
`dynamic` postpones certain type checking until runtime.

```csharp
dynamic value = 10;
value = "Hello";
```

It should be used carefully because some errors that would be caught at compile time can become runtime errors.

---

## Q23. What is `const`?

**Answer:**  
A `const` value cannot change after compilation.

```csharp
const double Pi = 3.14159;
```

---

## Q24. What is `readonly`?

**Answer:**  
A `readonly` field can be assigned during declaration or inside a constructor.

```csharp
class Employee
{
    private readonly int id;

    public Employee(int id)
    {
        this.id = id;
    }
}
```

---

## Q25. What is `static`?

**Answer:**  
A static member belongs to the type rather than an individual object.

```csharp
class MathHelper
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```

Usage:

```csharp
int result = MathHelper.Add(2, 3);
```

---

# 4. OOP in C#

## Q26. What are the four pillars of OOP?

**Answer:**

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

---

## Q27. What is encapsulation?

**Answer:**  
Encapsulation means combining data and behavior inside a class and controlling access to internal state.

```csharp
class BankAccount
{
    private double balance;

    public void Deposit(double amount)
    {
        if (amount > 0)
            balance += amount;
    }

    public double GetBalance()
    {
        return balance;
    }
}
```

---

## Q28. What is abstraction?

**Answer:**  
Abstraction hides implementation details and exposes only what is necessary.

It can be implemented using:

- Interfaces
- Abstract classes

---

## Q29. What is inheritance?

**Answer:**  
Inheritance allows a class to reuse and extend behavior from another class.

```csharp
class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating");
    }
}

class Dog : Animal
{
}
```

---

## Q30. What is polymorphism?

**Answer:**  
Polymorphism means one interface or method call can have different implementations.

Types commonly discussed in C#:

- Compile-time polymorphism — method overloading
- Runtime polymorphism — method overriding

---

## Q31. What is method overloading?

**Answer:**  
Same method name with different parameter lists.

```csharp
int Add(int a, int b)
{
    return a + b;
}

int Add(int a, int b, int c)
{
    return a + b + c;
}
```

---

## Q32. What is method overriding?

**Answer:**  
A derived class provides a different implementation of a virtual/abstract method.

```csharp
class Animal
{
    public virtual void Sound()
    {
        Console.WriteLine("Animal sound");
    }
}

class Dog : Animal
{
    public override void Sound()
    {
        Console.WriteLine("Bark");
    }
}
```

---

## Q33. Abstract class vs interface

| Abstract Class | Interface |
|---|---|
| Can contain implementation | Can define a contract and can also contain default implementations in modern C# |
| Can have fields | Cannot have instance fields |
| Can have constructors | No instance constructors |
| A class can inherit one base class | A class can implement multiple interfaces |
| Useful for shared base behavior | Useful for contracts/capabilities |

---

## Q34. What is an interface?

**Answer:**

```csharp
public interface IPaymentService
{
    void Pay(decimal amount);
}
```

A class implements it:

```csharp
public class PaymentService : IPaymentService
{
    public void Pay(decimal amount)
    {
        Console.WriteLine($"Paid {amount}");
    }
}
```

---

## Q35. What is `virtual`?

**Answer:**  
`virtual` allows a derived class to override a method.

```csharp
public virtual void Print()
{
}
```

---

## Q36. What is `override`?

**Answer:**  
`override` provides a new implementation for a virtual or abstract member.

---

## Q37. What is `sealed`?

**Answer:**  
A sealed class cannot be inherited.

```csharp
sealed class SecurityService
{
}
```

A method can also be sealed when overriding another virtual method.

---

# 5. Advanced C#

## Q38. What is a constructor?

**Answer:**  
A constructor initializes an object.

```csharp
class Employee
{
    public Employee()
    {
        Console.WriteLine("Created");
    }
}
```

---

## Q39. What is constructor overloading?

**Answer:**

```csharp
class Employee
{
    public Employee()
    {
    }

    public Employee(string name)
    {
    }
}
```

---

## Q40. What is a property?

**Answer:**

```csharp
public string Name { get; set; }
```

Properties provide controlled access to data.

---

## Q41. What is an auto-property?

**Answer:**

```csharp
public int Age { get; set; }
```

The compiler automatically creates the backing storage.

---

## Q42. What is a delegate?

**Answer:**  
A delegate represents a reference to a method with a compatible signature.

```csharp
delegate int Operation(int a, int b);
```

Delegates are used in:

- Callbacks
- Events
- LINQ
- Functional programming patterns

---

## Q43. What is an event?

**Answer:**  
An event provides a controlled mechanism for notifying subscribers when something happens.

```csharp
public event EventHandler? Completed;
```

---

## Q44. What is a lambda expression?

**Answer:**

```csharp
x => x * 2
```

Example:

```csharp
var result = numbers.Select(x => x * 2);
```

---

## Q45. What is an extension method?

**Answer:**  
An extension method adds a method to an existing type without modifying its source code or inheriting from it.

```csharp
public static class StringExtensions
{
    public static bool IsLong(this string value)
    {
        return value.Length > 10;
    }
}
```

Usage:

```csharp
bool result = "Hello World".IsLong();
```

---

## Q46. What is a record?

**Answer:**  
A `record` is a reference type designed for data-centric models with value-based equality semantics.

```csharp
public record Employee(int Id, string Name);
```

Records are useful for immutable/data-transfer-style objects.

---

## Q47. What is a nullable reference type?

**Answer:**  
Nullable reference type annotations help the compiler identify possible null-related bugs.

```csharp
string? name = null;
```

The `?` indicates that the reference may be null.

---

## Q48. What is the null-coalescing operator?

```csharp
string result = name ?? "Unknown";
```

If `name` is null, `"Unknown"` is used.

---

## Q49. What is the null-conditional operator?

```csharp
var length = name?.Length;
```

It safely accesses a member when the object may be null.

---

# 6. Collections, Generics and LINQ

## Q50. Array vs List

| Array | List |
|---|---|
| Fixed size | Dynamic size |
| `int[]` | `List<int>` |
| Good for fixed collections | Good for changing collections |

---

## Q51. List vs Dictionary

`List<T>` stores ordered elements.

```csharp
List<string> names = new();
```

`Dictionary<TKey,TValue>` stores key-value pairs.

```csharp
Dictionary<int, string> employees = new();
```

---

## Q52. What are generics?

**Answer:**  
Generics allow reusable, type-safe code.

```csharp
List<int> numbers = new();
List<string> names = new();
```

Benefits:

- Type safety
- Reusability
- Reduced casting
- Better performance in many value-type scenarios

---

## Q53. What is LINQ?

**Answer:**  
LINQ stands for **Language Integrated Query**.

It provides a consistent way to query collections and data sources.

```csharp
var adults = employees
    .Where(e => e.Age >= 18)
    .ToList();
```

---

## Q54. `Where()` vs `Select()`

`Where()` filters data.

```csharp
var result = employees.Where(e => e.Age > 20);
```

`Select()` transforms/projection data.

```csharp
var names = employees.Select(e => e.Name);
```

---

## Q55. `First()` vs `FirstOrDefault()`

`First()` throws an exception if no element exists.

`FirstOrDefault()` returns the default value if no element exists.

---

## Q56. `Single()` vs `First()`

`Single()` expects exactly one matching element and throws if there are zero or multiple matches.

`First()` returns the first matching element.

---

## Q57. What is deferred execution?

**Answer:**  
Some LINQ queries are not executed when they are defined. They execute when enumerated.

```csharp
var query = employees.Where(e => e.Age > 20);

foreach (var employee in query)
{
}
```

Calling `ToList()`, `ToArray()` or similar materialization methods executes the query at that point.

---

# 7. Exception Handling

## Q58. What is an exception?

**Answer:**  
An exception represents an error or exceptional condition during program execution.

---

## Q59. Explain try-catch-finally.

```csharp
try
{
    int result = 10 / 0;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine(ex.Message);
}
finally
{
    Console.WriteLine("Cleanup");
}
```

- `try` — code that may fail
- `catch` — handles an exception
- `finally` — cleanup code that generally runs whether an exception occurs or not

---

## Q60. What is `throw`?

**Answer:**  
`throw` raises an exception.

```csharp
throw new ArgumentException("Invalid value");
```

---

## Q61. Why should you not use exceptions for normal program flow?

**Answer:**  
Exceptions are intended for exceptional conditions. Using them for ordinary branching can make code harder to understand and may add unnecessary overhead.

---

# 8. ASP.NET Core Fundamentals

## Q62. What is ASP.NET Core?

**Answer:**  
ASP.NET Core is Microsoft's modern, cross-platform framework for building:

- Web applications
- REST APIs
- MVC applications
- Real-time applications
- Minimal APIs
- Backend services

---

## Q63. What is ASP.NET?

**Answer:**  
ASP.NET is Microsoft's web development technology/platform on .NET.

ASP.NET Core is the modern cross-platform implementation.

---

## Q64. What is MVC?

**Answer:**

MVC means:

- **Model** — application data/domain
- **View** — user interface
- **Controller** — handles requests and coordinates application logic

Flow:

```text
Browser
   ↓
Controller
   ↓
Model / Service
   ↓
Database
   ↓
Controller
   ↓
View
   ↓
Browser
```

---

## Q65. What is a Controller?

**Answer:**  
A controller handles incoming HTTP requests and returns an HTTP response or view.

Example:

```csharp
public class EmployeeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

---

## Q66. What is `IActionResult`?

**Answer:**  
`IActionResult` represents the result of an MVC controller action.

Examples:

```csharp
return View();
return RedirectToAction("Index");
return NotFound();
return BadRequest();
```

---

## Q67. What is routing?

**Answer:**  
Routing maps an incoming HTTP request to an endpoint.

Example:

```text
GET /api/employees/10
```

may map to:

```csharp
[HttpGet("{id}")]
public IActionResult GetEmployee(int id)
```

---

# 9. ASP.NET Core Middleware and Request Pipeline

## Q68. What is middleware?

**Answer:**  
Middleware is software that participates in processing HTTP requests and responses.

Examples:

- Authentication
- Authorization
- Exception handling
- Logging
- CORS
- Static files

---

## Q69. Explain the ASP.NET Core request pipeline.

```text
HTTP Request
     ↓
Middleware 1
     ↓
Middleware 2
     ↓
Routing
     ↓
Authentication
     ↓
Authorization
     ↓
Controller / Endpoint
     ↓
HTTP Response
```

Middleware can perform work before and after the next component.

---

## Q70. What is `Use()`?

**Answer:**  
`Use()` adds middleware that can call the next middleware.

Conceptually:

```csharp
app.Use(async (context, next) =>
{
    // Before
    await next();
    // After
});
```

---

## Q71. What is `Run()`?

**Answer:**  
`Run()` adds terminal middleware. It does not call the next middleware.

---

## Q72. What is `Map()`?

**Answer:**  
`Map()` branches the pipeline based on a path or condition.

---

## Q73. What is CORS?

**Answer:**  
CORS stands for **Cross-Origin Resource Sharing**.

It controls whether a browser application from one origin can access resources from another origin.

Example:

```text
React frontend:
http://localhost:3000

ASP.NET Core API:
https://localhost:7000
```

These are different origins, so CORS may need to be configured.

---

# 10. Dependency Injection and Configuration

## Q74. What is Dependency Injection?

**Answer:**  
Dependency Injection (DI) means providing an object with the dependencies it needs instead of making it create those dependencies itself.

Example:

```csharp
public class EmployeeController : ControllerBase
{
    private readonly IEmployeeService _service;

    public EmployeeController(IEmployeeService service)
    {
        _service = service;
    }
}
```

---

## Q75. Why use Dependency Injection?

**Answer:**

- Loose coupling
- Better testability
- Easier maintenance
- Easier replacement of implementations
- Cleaner architecture

---

## Q76. What are DI service lifetimes?

### Transient

A new instance is created each time it is requested.

```csharp
services.AddTransient<IEmailService, EmailService>();
```

### Scoped

One instance per scope. In ASP.NET Core, a common scope is an HTTP request.

```csharp
services.AddScoped<IEmployeeService, EmployeeService>();
```

### Singleton

One instance is shared for the application's lifetime.

```csharp
services.AddSingleton<ICacheService, CacheService>();
```

---

## Q77. When should Singleton be used carefully?

**Answer:**  
A singleton may be shared by many requests, so it must be thread-safe and should not directly depend on shorter-lived scoped services.

---

## Q78. What is configuration in ASP.NET Core?

**Answer:**  
Configuration allows applications to read settings from sources such as:

- `appsettings.json`
- Environment variables
- Command-line arguments
- Secret/configuration providers

Example:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "..."
  }
}
```

---

## Q79. What is the Options pattern?

**Answer:**  
The Options pattern maps configuration sections to strongly typed classes.

Example:

```csharp
public class JwtSettings
{
    public string Issuer { get; set; } = "";
}
```

This makes configuration easier to consume and validate.

---

# 11. ASP.NET Core MVC

## Q80. What is Model Binding?

**Answer:**  
Model binding converts incoming HTTP request data into .NET objects or parameters.

Example request:

```text
POST /api/employees
```

with JSON:

```json
{
  "name": "Rahul",
  "age": 22
}
```

ASP.NET Core can bind this JSON to an `Employee` object.

---

## Q81. What is Model Validation?

**Answer:**  
Model validation checks whether incoming data satisfies defined rules.

Example:

```csharp
public class Employee
{
    [Required]
    public string Name { get; set; } = "";

    [Range(18, 60)]
    public int Age { get; set; }
}
```

---

## Q82. What are Data Annotations?

**Answer:**  
Data annotations are attributes used to describe validation or metadata.

Common examples:

```csharp
[Required]
[StringLength(100)]
[Range(1, 100)]
[EmailAddress]
```

---

## Q83. What is Razor?

**Answer:**  
Razor is the syntax used to combine HTML with C# code in ASP.NET Core Razor views/pages.

Example:

```cshtml
<h1>Hello @Model.Name</h1>
```

---

# 12. Web API / REST API

## Q84. What is a Web API?

**Answer:**  
A Web API exposes application functionality over HTTP so that clients such as React, mobile apps or other services can communicate with the backend.

---

## Q85. What is REST?

**Answer:**  
REST is an architectural style commonly used to design HTTP APIs.

Important concepts:

- Resources
- HTTP methods
- Stateless requests
- Standard status codes
- Representation of resources

---

## Q86. Explain HTTP methods.

### GET
Retrieve data.

```http
GET /api/employees
```

### POST
Create data.

```http
POST /api/employees
```

### PUT
Replace/update a resource.

```http
PUT /api/employees/10
```

### PATCH
Partially update a resource.

```http
PATCH /api/employees/10
```

### DELETE
Delete a resource.

```http
DELETE /api/employees/10
```

---

## Q87. What are common HTTP status codes?

| Code | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized / authentication required |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 500 | Internal Server Error |

---

## Q88. 401 vs 403

**401** generally means the request lacks valid authentication credentials.

**403** means the server understood the request but refuses access, commonly because the authenticated user lacks sufficient permissions.

---

## Q89. What is `[ApiController]`?

**Answer:**  
`[ApiController]` enables API-specific behaviors such as automatic model validation responses and improved parameter binding behavior.

Example:

```csharp
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
}
```

---

## Q90. Controller vs ControllerBase

`ControllerBase` provides API-oriented controller functionality.

`Controller` derives from `ControllerBase` and additionally supports MVC views.

For a REST API, `ControllerBase` is commonly used.

---

## Q91. What is DTO?

**Answer:**  
DTO stands for **Data Transfer Object**.

It defines the data sent between client and server.

Example:

```csharp
public class EmployeeDto
{
    public string Name { get; set; } = "";
    public int Age { get; set; }
}
```

DTOs help avoid exposing internal domain/entity structures directly.

---

## Q92. Why use DTOs?

**Answer:**

- Control API response shape
- Avoid exposing sensitive fields
- Separate API contracts from database entities
- Reduce unnecessary data
- Make versioning easier

---

## Q93. What is Swagger/OpenAPI?

**Answer:**  
OpenAPI is a specification for describing HTTP APIs.

Swagger tools can generate interactive API documentation/testing interfaces from an OpenAPI document.

---

# 13. Entity Framework Core

## Q94. What is Entity Framework Core?

**Answer:**  
Entity Framework Core (EF Core) is an ORM for .NET.

ORM means **Object-Relational Mapper**.

It allows developers to work with database data using .NET objects and LINQ.

---

## Q95. What is DbContext?

**Answer:**  
`DbContext` represents a session with the database and provides:

- Database connection/configuration
- Querying
- Change tracking
- Saving changes

Example:

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }
}
```

---

## Q96. What is DbSet?

**Answer:**  
`DbSet<T>` represents a collection/entity set that EF Core can query and persist.

```csharp
public DbSet<Employee> Employees { get; set; }
```

---

## Q97. What is migration?

**Answer:**  
A migration records changes to the EF Core model so the database schema can be updated.

Typical commands:

```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

---

## Q98. Code First vs Database First

### Code First
Define the model in code and generate/update the database schema using migrations.

### Database First
Start from an existing database and generate model classes/context from it.

---

## Q99. What is change tracking?

**Answer:**  
EF Core tracks entity state such as:

- Added
- Modified
- Deleted
- Unchanged
- Detached

When `SaveChanges()` is called, EF Core uses the tracked changes to generate database operations.

---

## Q100. What is eager loading?

**Answer:**  
Eager loading loads related data as part of the query.

```csharp
var employees = context.Employees
    .Include(e => e.Department)
    .ToList();
```

---

## Q101. What is lazy loading?

**Answer:**  
Lazy loading loads related data when the navigation property is accessed.

It can be convenient but can also cause many unexpected database queries if used carelessly.

---

## Q102. What is explicit loading?

**Answer:**  
Explicit loading means explicitly requesting related data after the entity has already been loaded.

---

## Q103. What is `AsNoTracking()`?

**Answer:**  
`AsNoTracking()` tells EF Core not to track returned entities.

```csharp
var employees = context.Employees
    .AsNoTracking()
    .ToList();
```

It is useful for read-only queries because change tracking is unnecessary.

---

## Q104. What is N+1 query problem?

**Answer:**  
The N+1 problem occurs when one query loads a set of records and then an additional query is executed for each record to load related data.

Example:

```text
1 query for employees
+
N queries for departments
=
N+1 queries
```

Use appropriate projection, joins or eager loading to avoid unnecessary database round trips.

---

# 14. SQL and Database Questions

## Q105. What is a primary key?

**Answer:**  
A primary key uniquely identifies each row in a table.

Example:

```sql
CREATE TABLE Employees (
    Id INT PRIMARY KEY,
    Name VARCHAR(100)
);
```

---

## Q106. What is a foreign key?

**Answer:**  
A foreign key establishes a relationship between tables.

```sql
DepartmentId INT REFERENCES Departments(Id)
```

---

## Q107. What is normalization?

**Answer:**  
Normalization organizes data to reduce redundancy and improve data integrity.

Common normal forms:

- 1NF
- 2NF
- 3NF
- BCNF

---

## Q108. What is a JOIN?

**Answer:**  
A JOIN combines related rows from tables.

Common joins:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN

Example:

```sql
SELECT e.Name, d.Name
FROM Employees e
INNER JOIN Departments d
ON e.DepartmentId = d.Id;
```

---

## Q109. What is an index?

**Answer:**  
An index improves lookup performance for suitable queries but requires additional storage and can increase the cost of writes.

---

## Q110. What is a transaction?

**Answer:**  
A transaction groups operations so they can succeed or fail as a unit.

The common ACID properties are:

- Atomicity
- Consistency
- Isolation
- Durability

---

# 15. Authentication, Authorization and Security

## Q111. Authentication vs Authorization

**Authentication:** Who are you?

**Authorization:** What are you allowed to do?

Example:

```text
Login → Authentication
Admin-only endpoint → Authorization
```

---

## Q112. What is JWT?

**Answer:**  
JWT stands for JSON Web Token.

It is commonly used to represent claims between a client and server.

A JWT commonly has:

```text
Header.Payload.Signature
```

---

## Q113. How does JWT authentication work?

Typical flow:

```text
User Login
   ↓
Server validates credentials
   ↓
Server issues JWT
   ↓
Client stores token appropriately
   ↓
Client sends token with API request
   ↓
Server validates token
   ↓
Request is authorized
```

---

## Q114. What is Bearer authentication?

Example:

```http
Authorization: Bearer <token>
```

The server extracts and validates the token according to the configured authentication scheme.

---

## Q115. What is password hashing?

**Answer:**  
Passwords should not be stored as plain text.

A password hashing algorithm derives a one-way representation that can be verified later.

For production applications, use a well-established password hashing/password identity solution rather than inventing your own algorithm.

---

## Q116. What is HTTPS?

**Answer:**  
HTTPS uses TLS to protect HTTP communication against eavesdropping and tampering.

---

## Q117. What is SQL Injection?

**Answer:**  
SQL injection occurs when untrusted input changes the meaning of a SQL query.

Use:

- Parameterized queries
- ORM safely
- Input validation
- Least-privilege database accounts

Never concatenate untrusted input into SQL statements.

---

## Q118. What is XSS?

**Answer:**  
Cross-Site Scripting (XSS) occurs when untrusted content is interpreted as executable browser-side code.

Defenses include:

- Output encoding
- Framework protections
- Input handling
- Content Security Policy where appropriate

---

## Q119. What is CSRF?

**Answer:**  
Cross-Site Request Forgery tricks a user's browser into making an unwanted authenticated request.

Protection depends on the authentication mechanism and application architecture and can include anti-forgery tokens and appropriate cookie settings.

---

## Q120. What is CORS vs CSRF?

**CORS** controls cross-origin browser access.

**CSRF** is an attack where a user's authenticated browser is tricked into sending an unwanted request.

They solve different problems.

---

# 16. Async/Await and Performance

## Q121. What is asynchronous programming?

**Answer:**  
Asynchronous programming allows a program to start an operation and continue other work while waiting for an I/O operation to complete.

Useful for:

- Database calls
- HTTP calls
- File I/O
- Network operations

---

## Q122. What are `async` and `await`?

```csharp
public async Task<Employee?> GetEmployeeAsync(int id)
{
    return await context.Employees.FindAsync(id);
}
```

`async` enables asynchronous method syntax.

`await` asynchronously waits for a task to complete without blocking the current thread in the usual async I/O case.

---

## Q123. Task vs Thread

**Thread:** An execution thread managed by the operating system/runtime.

**Task:** An abstraction representing asynchronous work or a future result.

Async I/O often uses tasks without requiring a dedicated thread to sit idle while waiting for I/O.

---

## Q124. Why use async database operations?

Example:

```csharp
var employees = await context.Employees.ToListAsync();
```

This helps server applications use resources efficiently while waiting for database I/O.

---

## Q125. What is `Task<T>`?

**Answer:**  
`Task<T>` represents an asynchronous operation that eventually produces a result of type `T`.

```csharp
Task<int>
Task<Employee>
```

---

## Q126. What is deadlock?

**Answer:**  
A deadlock occurs when execution becomes stuck because multiple operations are waiting on resources or each other in a circular dependency.

In older synchronization-context scenarios, blocking on async work using `.Result` or `.Wait()` can contribute to deadlocks.

Prefer async all the way.

---

# 17. Testing, Debugging and Logging

## Q127. What is unit testing?

**Answer:**  
Unit testing tests a small unit of application logic in isolation.

Common .NET frameworks include:

- xUnit
- NUnit
- MSTest

---

## Q128. What is integration testing?

**Answer:**  
Integration testing verifies that multiple components work together.

Example:

```text
Controller
   ↓
Service
   ↓
EF Core
   ↓
Database
```

---

## Q129. What is mocking?

**Answer:**  
Mocking replaces a real dependency with a controlled test double.

Example:

```text
Real EmailService → sends email
Mock EmailService → records that Send() was called
```

Popular .NET mocking libraries include Moq and NSubstitute.

---

## Q130. What is logging in ASP.NET Core?

**Answer:**  
ASP.NET Core provides logging abstractions through `ILogger<T>`.

Example:

```csharp
private readonly ILogger<EmployeeService> _logger;

public EmployeeService(ILogger<EmployeeService> logger)
{
    _logger = logger;
}

_logger.LogInformation("Employee created");
```

---

## Q131. Why are structured logs useful?

**Answer:**  
Structured logging stores data as fields instead of only plain text, making logs easier to search, filter and analyze.

---

# 18. Deployment, Docker and Production

## Q132. How do you run an ASP.NET Core application?

Development:

```bash
dotnet run
```

Build:

```bash
dotnet build
```

Publish:

```bash
dotnet publish -c Release
```

---

## Q133. What is Kestrel?

**Answer:**  
Kestrel is the cross-platform web server used by ASP.NET Core.

It can run directly or behind a reverse proxy such as IIS or Nginx.

---

## Q134. What is IIS?

**Answer:**  
IIS is Microsoft's web server for Windows.

ASP.NET Core applications can be hosted behind IIS using the ASP.NET Core hosting model.

---

## Q135. Why use Docker with ASP.NET Core?

**Answer:**  
Docker packages the application and its dependencies into a container image.

Benefits include:

- Consistent environments
- Easier deployment
- Isolation
- Portability
- Reproducibility

Example Dockerfile:

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "MyApi.dll"]
```

> Use the .NET version that matches your application.

---

## Q136. What is environment-specific configuration?

**Answer:**  
Applications commonly have different configuration for development, testing and production.

Examples:

```text
appsettings.json
appsettings.Development.json
appsettings.Production.json
```

Secrets should not be committed to source control.

---

## Q137. What should be considered before deploying an API?

**Answer:**

- HTTPS
- Authentication/authorization
- Secrets management
- Database configuration
- Logging
- Error handling
- Health checks
- CORS
- Rate limiting where appropriate
- Monitoring
- Docker/container configuration
- CI/CD

---

# 19. Common Practical Coding Questions

## Q138. Reverse a string

```csharp
string ReverseString(string input)
{
    return new string(input.Reverse().ToArray());
}
```

---

## Q139. Check palindrome

```csharp
bool IsPalindrome(string input)
{
    string reversed = new string(input.Reverse().ToArray());
    return input == reversed;
}
```

For interview discussions, also explain how to solve it using two pointers.

---

## Q140. Find maximum number

```csharp
int max = numbers.Max();
```

Manual approach:

```csharp
int max = numbers[0];

foreach (int n in numbers)
{
    if (n > max)
        max = n;
}
```

---

## Q141. Count duplicate values using Dictionary

```csharp
var frequency = new Dictionary<int, int>();

foreach (int n in numbers)
{
    if (frequency.ContainsKey(n))
        frequency[n]++;
    else
        frequency[n] = 1;
}
```

---

## Q142. Remove duplicates

```csharp
var unique = numbers.Distinct().ToList();
```

---

## Q143. Find even numbers using LINQ

```csharp
var evenNumbers = numbers
    .Where(n => n % 2 == 0)
    .ToList();
```

---

## Q144. Find employees whose salary is greater than 50,000

```csharp
var result = employees
    .Where(e => e.Salary > 50000)
    .ToList();
```

---

## Q145. Select only employee names

```csharp
var names = employees
    .Select(e => e.Name)
    .ToList();
```

---

## Q146. Find second-highest salary using LINQ

```csharp
var secondHighest = employees
    .Select(e => e.Salary)
    .Distinct()
    .OrderByDescending(s => s)
    .Skip(1)
    .FirstOrDefault();
```

Explain the handling of duplicate salary values and the case where fewer than two distinct salaries exist.

---

# 20. Project-Based Interview Questions

If you have built a React frontend and a .NET backend, interviewers can ask these questions.

## Q147. Explain your project architecture.

**Sample Answer:**

> My application follows a client-server architecture. The React frontend communicates with the ASP.NET Core Web API through HTTP requests. The API uses controllers for request handling, services for business logic, repositories or EF Core for data access, and a relational database for persistent storage.

```text
React Frontend
      ↓ HTTP/JSON
ASP.NET Core Web API
      ↓
Controller
      ↓
Service Layer
      ↓
EF Core
      ↓
SQL Database
```

---

## Q148. Why did you choose ASP.NET Core?

**Sample Answer:**

> I chose ASP.NET Core because it is cross-platform, supports REST APIs, has built-in dependency injection, provides middleware-based request processing, integrates well with Entity Framework Core, and is suitable for modern web applications.

---

## Q149. Why did you use a service layer?

**Answer:**

> The service layer separates business logic from controllers. This keeps controllers smaller, improves testability and makes the business logic easier to reuse.

---

## Q150. How does React communicate with ASP.NET Core?

**Answer:**

React sends HTTP requests using `fetch` or a library such as Axios.

Example:

```javascript
const response = await fetch(
  "https://localhost:7000/api/employees"
);

const data = await response.json();
```

ASP.NET Core returns JSON.

---

## Q151. What if React gives a CORS error?

**Answer:**

> I would verify that the API has a CORS policy allowing the frontend's origin, that the policy is applied correctly in the middleware pipeline, and that the request method and headers are permitted.

Example:

```csharp
builder.Services.AddCors(options =>
{
    options.AddPolicy("Frontend", policy =>
    {
        policy
            .WithOrigins("http://localhost:3000")
            .AllowAnyHeader()
            .AllowAnyMethod();
    });
});
```

---

## Q152. How would you implement login?

**Answer:**

```text
React Login Form
      ↓
POST /api/auth/login
      ↓
ASP.NET Core
      ↓
Validate user
      ↓
Verify password hash
      ↓
Generate authentication token
      ↓
Return authentication result
      ↓
React
```

For production, authentication credentials and tokens must be handled securely.

---

## Q153. How would you protect an endpoint?

Example:

```csharp
[Authorize]
[HttpGet]
public IActionResult GetProfile()
{
    return Ok();
}
```

For role-based authorization:

```csharp
[Authorize(Roles = "Admin")]
```

---

## Q154. How would you handle errors globally?

**Answer:**

> I would use centralized exception-handling middleware or the framework's exception-handling facilities. I would log the exception internally and return a safe, consistent error response without exposing sensitive implementation details.

---

## Q155. How would you improve API performance?

**Answer:**

- Use async I/O
- Select only required columns
- Add appropriate database indexes
- Avoid N+1 queries
- Use `AsNoTracking()` for read-only EF Core queries where appropriate
- Pagination
- Caching where appropriate
- Compression where appropriate
- Avoid unnecessary database calls
- Measure using profiling/monitoring before optimizing

---

## Q156. How would you implement pagination?

Example request:

```http
GET /api/employees?page=2&pageSize=20
```

EF Core concept:

```csharp
var employees = await context.Employees
    .OrderBy(e => e.Id)
    .Skip((page - 1) * pageSize)
    .Take(pageSize)
    .ToListAsync();
```

---

## Q157. How would you secure a production API?

**Answer:**

- HTTPS
- Strong authentication
- Authorization
- Secure password hashing
- Input validation
- Parameterized queries
- Safe error responses
- Secret management
- CORS configuration
- Rate limiting where appropriate
- Logging and monitoring
- Dependency updates
- Secure headers/configuration

---

# 21. Rapid-Fire Questions

## Q158. What is REST?

An architectural style commonly used for HTTP APIs.

## Q159. What is JSON?

A lightweight text-based data interchange format.

## Q160. What is HTTP?

A protocol used for communication between clients and servers.

## Q161. What is HTTPS?

HTTP protected with TLS.

## Q162. What is API endpoint?

A specific URL/route through which an API exposes functionality.

## Q163. What is serialization?

Converting an object/data structure into a transferable representation such as JSON.

## Q164. What is deserialization?

Converting serialized data back into an object/data structure.

## Q165. What is middleware?

A component in the HTTP request/response pipeline.

## Q166. What is DI?

Providing dependencies from outside instead of creating them inside a class.

## Q167. What is ORM?

Object-Relational Mapping.

## Q168. What is EF Core?

Microsoft's ORM for .NET.

## Q169. What is LINQ?

Language Integrated Query.

## Q170. What is DTO?

Data Transfer Object.

## Q171. What is JWT?

JSON Web Token.

## Q172. What is CORS?

A browser security mechanism that controls cross-origin resource sharing.

## Q173. What is Swagger?

A commonly used tooling ecosystem around OpenAPI documentation and API exploration.

## Q174. What is Kestrel?

The cross-platform web server used by ASP.NET Core.

## Q175. What is NuGet?

The package ecosystem/package manager for .NET.

## Q176. What is `IEnumerable<T>`?

An abstraction for enumerating a sequence of values.

## Q177. What is `IQueryable<T>`?

An abstraction for queryable data sources where the query can be translated by the provider, such as EF Core translating LINQ to SQL.

## Q178. What is `ICollection<T>`?

An interface representing a mutable collection abstraction with collection operations.

---

# 22. Important Differences to Memorize

## Q179. `IEnumerable` vs `IQueryable`

| IEnumerable | IQueryable |
|---|---|
| General sequence abstraction | Queryable data-source abstraction |
| Commonly used for in-memory enumeration | Can allow provider-specific query translation |
| LINQ operations can execute in memory | EF Core can translate supported expressions to SQL |

---

## Q180. `IEnumerable` vs `List`

`IEnumerable<T>` is an abstraction for enumeration.

`List<T>` is a concrete mutable collection.

---

## Q181. `AddSingleton` vs `AddScoped` vs `AddTransient`

| Lifetime | Typical behavior |
|---|---|
| Singleton | One instance for application lifetime |
| Scoped | One instance per scope, commonly per HTTP request |
| Transient | New instance each time requested |

---

## Q182. `First` vs `Single`

| First | Single |
|---|---|
| Returns first matching item | Requires exactly one matching item |
| Can have multiple matches | Multiple matches cause exception |
| Zero matches cause exception | Zero matches cause exception |

`FirstOrDefault()` and `SingleOrDefault()` return a default when no item exists, but `SingleOrDefault()` still fails if multiple items match.

---

## Q183. PUT vs PATCH

**PUT:** Usually represents replacing the resource representation.

**PATCH:** Represents a partial modification.

---

## Q184. Authentication vs Authorization

```text
Authentication = Who are you?
Authorization = What can you access?
```

---

## Q185. MVC vs Web API

**MVC:** Commonly used for server-rendered web applications.

**Web API:** Commonly used for HTTP APIs consumed by React, mobile apps or other clients.

ASP.NET Core can support both patterns.

---

## Q186. ViewBag vs ViewData vs TempData

### ViewData

Dictionary-based data passing between controller and view.

### ViewBag

Dynamic wrapper around ViewData.

### TempData

Used for data that needs to survive a redirect/request transition according to the configured TempData provider.

---

# 23. Final Revision Checklist

Before attending a .NET / ASP.NET interview, make sure you can explain these without memorizing blindly.

## C#

- [ ] Variables and data types
- [ ] Value vs reference types
- [ ] `var` vs `dynamic`
- [ ] `const` vs `readonly`
- [ ] Classes and objects
- [ ] Constructors
- [ ] Encapsulation
- [ ] Abstraction
- [ ] Inheritance
- [ ] Polymorphism
- [ ] Interface
- [ ] Abstract class
- [ ] Overloading
- [ ] Overriding
- [ ] Delegates
- [ ] Events
- [ ] Lambda expressions
- [ ] Generics
- [ ] Collections
- [ ] LINQ
- [ ] Exception handling
- [ ] Async/await

## .NET

- [ ] CLR
- [ ] CTS
- [ ] CLS
- [ ] JIT
- [ ] Garbage collection
- [ ] Assemblies
- [ ] NuGet
- [ ] .NET Framework
- [ ] Modern .NET

## ASP.NET Core

- [ ] ASP.NET Core architecture
- [ ] MVC
- [ ] Controllers
- [ ] Routing
- [ ] Middleware
- [ ] Request pipeline
- [ ] Dependency Injection
- [ ] Service lifetimes
- [ ] Configuration
- [ ] Model binding
- [ ] Model validation
- [ ] CORS
- [ ] Web API
- [ ] REST
- [ ] HTTP methods
- [ ] Status codes
- [ ] DTO
- [ ] Swagger/OpenAPI
- [ ] Authentication
- [ ] Authorization

## EF Core

- [ ] DbContext
- [ ] DbSet
- [ ] Migrations
- [ ] Code First
- [ ] Database First
- [ ] Change tracking
- [ ] Eager loading
- [ ] Lazy loading
- [ ] Explicit loading
- [ ] AsNoTracking
- [ ] N+1 query problem

## Database

- [ ] Primary key
- [ ] Foreign key
- [ ] Joins
- [ ] Indexes
- [ ] Normalization
- [ ] Transactions
- [ ] ACID
- [ ] SQL injection

## Production

- [ ] Logging
- [ ] Error handling
- [ ] Testing
- [ ] Docker
- [ ] Kestrel
- [ ] IIS
- [ ] Configuration
- [ ] Environment variables
- [ ] Secrets
- [ ] HTTPS
- [ ] Deployment

---

# Most Important 30 Questions for a Fresher

If the interviewer has limited time, prioritize these:

1. What is .NET?
2. What is CLR?
3. .NET Framework vs modern .NET?
4. What is C#?
5. Explain OOP pillars.
6. Abstract class vs interface.
7. Overloading vs overriding.
8. Value type vs reference type.
9. `var` vs `dynamic`.
10. What is LINQ?
11. What is async/await?
12. What is ASP.NET Core?
13. Explain MVC.
14. What is middleware?
15. Explain request pipeline.
16. What is Dependency Injection?
17. Explain Singleton, Scoped and Transient.
18. What is Web API?
19. Explain REST.
20. GET vs POST vs PUT vs PATCH vs DELETE.
21. Explain HTTP status codes.
22. What is DTO?
23. What is CORS?
24. Authentication vs Authorization.
25. What is JWT?
26. What is Entity Framework Core?
27. What is DbContext?
28. What are migrations?
29. Explain EF Core `AsNoTracking()`.
30. Explain your project architecture.

---

# Interview Answer Strategy

For technical questions, use this structure:

```text
1. Definition
2. Why it is used
3. Small example
4. Real project use case
5. Difference/limitation if relevant
```

Example:

**Interviewer:** What is Dependency Injection?

**Good fresher answer:**

> Dependency Injection is a design technique where a class receives the objects it depends on from an external source instead of creating them itself. ASP.NET Core has built-in dependency injection. It helps reduce coupling and makes code easier to test. For example, instead of creating `EmployeeService` inside a controller, I inject `IEmployeeService` through the controller constructor.

Then stop and let the interviewer ask the next question.

---

# Final Tip

Do not try to memorize every answer word-for-word.

For each topic, understand:

```text
What is it?
      ↓
Why do we need it?
      ↓
How does it work?
      ↓
Where did I use it?
      ↓
What is the alternative/difference?
```

For a fresher .NET interview, being able to explain your own project clearly is especially important. Be ready to draw the architecture and explain one complete request from the React frontend through the ASP.NET Core API, service layer, EF Core and database, and then back to the frontend.
