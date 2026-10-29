# From Express.js to ASP.NET Core: A Practical Migration Guide

A practical guide for a MERN/Express developer who wants to become a
.NET backend developer before starting a new ASP.NET Core project.

------------------------------------------------------------------------

## 1. The big picture: what changes when you move to .NET?

You already understand important backend concepts from Express.js:
routes, controllers, middleware, request/response handling,
authentication, database access, validation, and REST APIs. Those
concepts still exist in ASP.NET Core. The main change is **how the
framework organizes and provides them**.

  -------------------------------------------------------------------------------
  Concept                 Express.js / Node.js    ASP.NET Core
  ----------------------- ----------------------- -------------------------------
  Language                JavaScript or           C#
                          TypeScript              

  Web framework           Express                 ASP.NET Core

  App startup             `app.js` / `server.js`  `Program.cs`

  Route definition        `app.get(...)`,         Controller attributes or
                          `router.post(...)`      Minimal API route mappings

  Controller              Express                 C# controller class, or
                          route/controller        endpoint handler
                          function                

  Middleware              `app.use(...)`          `app.Use...()` and custom
                                                  middleware

  Dependency injection    Often manual or via a   Built into ASP.NET Core
                          package                 

  Request DTO /           Objects + validation    C# DTOs + validation attributes
  validation              libraries               or other validators

  ORM / database layer    Mongoose, Prisma,       Entity Framework Core (EF
                          Sequelize               Core), or Dapper

  Database                MongoDB commonly in     SQL Server is common in .NET,
                          MERN                    but PostgreSQL, MySQL and
                                                  MongoDB are also possible

  Authentication          JWT libraries,          ASP.NET Core
                          Passport, custom        Authentication/Authorization,
                          middleware              JWT bearer authentication,
                                                  Identity

  Configuration           `.env`, config files    `appsettings.json`, environment
                                                  variables, user secrets

  API documentation       Swagger packages        OpenAPI/Swagger tooling

  Package manager         npm                     NuGet

  Build/run               `npm run dev`           `dotnet run`

  Tests                   Jest, Vitest, Supertest xUnit, NUnit or MSTest;
                                                  integration testing tools

  Deployment              Node hosting /          IIS, Azure, Linux hosting,
                          containers              containers, or other cloud
                                                  hosting
  -------------------------------------------------------------------------------

**Key idea:** you are not starting from zero. Your backend knowledge
transfers; you mainly need to learn C# conventions, ASP.NET Core's
request pipeline, dependency injection, EF Core, and .NET tooling.

------------------------------------------------------------------------

## 2. What exactly is .NET, C#, and ASP.NET Core?

These terms are related, but they do not mean the same thing.

-   **C#** is the programming language. You write classes, methods,
    models, services, and business logic in C#.
-   **.NET** is the development platform/runtime and its libraries. It
    provides the runtime, base class libraries, tooling, and
    project/build system.
-   **ASP.NET Core** is the web framework built on .NET. It is used to
    build REST APIs, web applications, real-time services, and backend
    systems.
-   **Entity Framework Core (EF Core)** is an object-relational mapper
    (ORM). It maps C# objects to relational database tables and helps
    query/update them.
-   **NuGet** is the package ecosystem/tooling used to add .NET
    libraries to a project.
-   **Visual Studio** is a full-featured IDE for .NET. **Visual Studio
    Code** can also be used with the C# Dev Kit and .NET SDK.

For a backend API, your usual stack could be:

**C# + ASP.NET Core Web API + EF Core + SQL Server + JWT
authentication + Swagger/OpenAPI + xUnit**

This is a common learning stack, not a requirement. You can still use
MongoDB if that fits your project.

------------------------------------------------------------------------

## 3. What makes ASP.NET Core special?

### 3.1 Built-in dependency injection (DI)

In Express, you may import a database service directly into a controller
or pass it manually. ASP.NET Core has a built-in DI container. You
register services in `Program.cs`, then request them through a
constructor.

``` csharp
// Program.cs
builder.Services.AddScoped<IProductService, ProductService>();
```

``` csharp
public class ProductsController : ControllerBase
{
    private readonly IProductService _productService;

    public ProductsController(IProductService productService)
    {
        _productService = productService;
    }
}
```

Why it matters: - Reduces tight coupling. - Makes unit testing easier. -
Makes it clear which dependencies a class needs. - Provides service
lifetimes: **Transient**, **Scoped**, and **Singleton**.

Typical meanings: - **Transient:** a new instance each time it is
requested. - **Scoped:** one instance per HTTP request in a typical web
API. - **Singleton:** one instance for the application's lifetime.

Do not register a service as Singleton if it depends on a scoped service
such as a typical EF Core `DbContext`.

### 3.2 Middleware pipeline

ASP.NET Core processes requests through an ordered pipeline. Middleware
can inspect a request, call the next middleware, and inspect the
response on the way back.

``` csharp
var app = builder.Build();

app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();
app.Run();
```

Order matters. For example, authentication normally runs before
authorization. Error handling, CORS, routing, authentication, and
authorization must be configured thoughtfully.

Express comparison:

``` js
app.use(cors());
app.use(express.json());
app.use("/api/products", productRoutes);
```

The idea is similar, but ASP.NET Core has a more integrated hosting and
middleware model.

### 3.3 Strong typing and compile-time checks

C# is statically typed. The compiler can catch many type errors before
the application runs. You define types for request DTOs, responses,
entities, and service interfaces.

This does not eliminate runtime errors, but it makes many mistakes
easier to detect earlier.

### 3.4 Controllers and attributes

ASP.NET Core controllers are usually classes. Attributes such as
`[ApiController]`, `[Route]`, `[HttpGet]`, and `[Authorize]` describe
how endpoints behave.

``` csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(new[] { "Keyboard", "Mouse" });
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok(new { Id = id });
    }
}
```

`[controller]` is a route token. Here, the controller name becomes
`products`. `Ok(...)` returns HTTP 200. Other common helpers include
`CreatedAtAction(...)`, `BadRequest(...)`, `NotFound(...)`, and
`NoContent()`.

### 3.5 Configuration is environment-aware

Settings often live in `appsettings.json`, with environment-specific
files such as `appsettings.Development.json`. Environment variables and
user secrets can override settings.

``` json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

Do not commit database passwords, production API keys, or JWT signing
secrets to source control. Use user secrets for local development and
environment variables or a secret manager in deployment.

### 3.6 Built-in hosting, logging, and diagnostics

ASP.NET Core includes a standard hosting model, structured logging
abstractions, configuration, environment support, and health/diagnostic
integrations. You can use these instead of assembling every foundational
feature from separate packages.

### 3.7 Multiple API styles

You can build APIs with: - **Controller-based APIs:** good for learning
structured APIs and larger projects. - **Minimal APIs:** endpoint
definitions with less ceremony, often useful for small services or
lightweight APIs.

For your first transition project, controller-based Web API is a clear
choice because its controller/service/repository separation is easy to
compare with an Express project.

------------------------------------------------------------------------

## 4. What does a .NET Web API project look like?

A simple project may begin with a structure like this:

``` text
MyApp/
├── Controllers/
│   └── ProductsController.cs
├── Models/
│   └── Product.cs
├── DTOs/
│   ├── CreateProductDto.cs
│   └── ProductResponseDto.cs
├── Data/
│   └── AppDbContext.cs
├── Services/
│   ├── IProductService.cs
│   └── ProductService.cs
├── Repositories/                 # Optional
│   ├── IProductRepository.cs
│   └── ProductRepository.cs
├── Middleware/                   # Optional custom middleware
├── Properties/
├── appsettings.json
├── appsettings.Development.json
├── Program.cs
└── MyApp.csproj
```

This is an example, not a mandatory folder layout. Small APIs may use
fewer folders; larger systems may split code into multiple projects.

### What each important file/folder does

-   `Program.cs`: configures services and the HTTP request pipeline,
    then starts the app.
-   `.csproj`: project configuration, target framework, package
    references, and build settings.
-   `Controllers/`: HTTP endpoints; reads request data and returns HTTP
    responses.
-   `DTOs/`: shapes of data accepted from or returned to clients.
-   `Models/` or `Entities/`: domain/database entity classes.
-   `Data/`: EF Core `DbContext` and database configuration.
-   `Services/`: business logic, such as complaint assignment or user
    registration.
-   `Repositories/`: optional data-access abstraction. Do not add this
    layer automatically if it adds no value.
-   `Middleware/`: custom request-pipeline logic, if needed.
-   `appsettings.json`: non-secret configuration defaults.

### A typical request flow

``` text
React frontend
    |
    | HTTP request (JSON + optional Bearer token)
    v
ASP.NET Core middleware pipeline
    |
    v
Controller / API endpoint
    |
    v
Service (business rules)
    |
    v
EF Core DbContext / data-access layer
    |
    v
Database (e.g. SQL Server or PostgreSQL)
    |
    v
HTTP response (status code + JSON)
    |
    v
React frontend
```

Not every project needs a repository layer. A controller should
generally not contain all business logic or complex database operations.

------------------------------------------------------------------------

## 5. Controllers, services, repositories, entities, and DTOs

These are common terms you will see in .NET codebases.

### Controller

The HTTP layer. It reads route/query/body data, calls the service, and
returns the right status code and response.

### Service

The business-logic layer. It decides what should happen, checks business
rules, and coordinates operations.

### Repository / data-access layer

An optional layer that isolates database queries. EF Core's `DbContext`
already provides repository/unit-of-work-like capabilities, so a custom
repository is not always necessary.

### Entity

A domain object that may be stored in the database. For EF Core, an
entity often maps to a database table.

### DTO (Data Transfer Object)

A type designed for API input/output. DTOs let you control which fields
a client can send or see.

**Why not return the entity directly for everything?** - It can expose
internal fields accidentally. - Input fields and output fields often
differ. - API contracts should not have to mirror the database schema. -
It helps validate client input separately from persistence rules.

A useful mental model:

``` text
Request DTO -> Controller -> Service -> DbContext/Repository -> Entity/database
Response DTO <- Controller <- Service <- Entity/database
```

------------------------------------------------------------------------

## 6. Your first ASP.NET Core project: create and run it

Install the current supported **.NET SDK** and a suitable editor (Visual
Studio or VS Code with C# support). Verify installation:

``` bash
dotnet --info
dotnet --list-sdks
```

Create a controller-based API:

``` bash
dotnet new webapi --use-controllers -n MyFirstApi
cd MyFirstApi
dotnet run
```

Template options can differ by SDK version. If `--use-controllers` is
not recognized by your installed SDK, check `dotnet new webapi --help`
and use the controller option available in that version.

Useful CLI commands:

``` bash
dotnet restore       # Restore NuGet dependencies
dotnet build         # Compile the project
dotnet run           # Run the app
dotnet watch run     # Run with development-time file watching
dotnet test          # Run tests in the solution/project
dotnet add package <PackageName>
dotnet new --list    # List installed templates
```

When the application starts, read the terminal output for the actual
local URL and port. Open its API documentation endpoint if the template
includes Swagger/OpenAPI UI, or test endpoints using Postman or curl. Do
not assume the port is always the same.

### What is `Program.cs`?

A simplified example:

``` csharp
var builder = WebApplication.CreateBuilder(args);

// Register framework services.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
// Add Swagger/OpenAPI services as appropriate for your template and SDK.

// Register your own services and database context here.
// builder.Services.AddScoped<IProductService, ProductService>();

var app = builder.Build();

// Configure middleware here.
// app.UseHttpsRedirection();
// app.UseAuthentication();
// app.UseAuthorization();

app.MapControllers();
app.Run();
```

Generated templates may contain additional code, including OpenAPI
setup. Learn the generated file instead of deleting code just because it
looks unfamiliar.

------------------------------------------------------------------------

## 7. Learn the C# features you need from a JavaScript background

You do not need to master every C# feature before building an API. Focus
on these first:

1.  **Types and variables:** `int`, `decimal`, `string`, `bool`,
    `DateTime`, nullable types such as `string?`.
2.  **Methods and classes:** constructors, properties, access modifiers,
    `static`, `public`, `private`.
3.  **Collections:** arrays, `List<T>`, `Dictionary<TKey, TValue>`,
    `IEnumerable<T>`.
4.  **Object-oriented programming:** encapsulation, inheritance,
    interfaces, composition, polymorphism.
5.  **Interfaces:** for example, `IEmailService` and its implementation
    `EmailService`.
6.  **Generics:** types such as `List<Product>` and `Task<Product?>`.
7.  **Exception handling:** `try`, `catch`, custom exceptions, and
    appropriate error handling.
8.  **LINQ:** query and transform collections and data sources with
    methods such as `Where`, `Select`, `Any`, `FirstOrDefault`, and
    `OrderBy`.
9.  **Async/await:** asynchronous database and network operations.
10. **Nullable reference types:** understand when a value may be absent
    and handle that explicitly.
11. **Records and DTOs:** useful for data-oriented types, although
    ordinary classes are also common.
12. **Access modifiers and namespaces:** understand what code can access
    and how files are organized.

### JavaScript versus C# examples

JavaScript:

``` js
const total = prices.reduce((sum, price) => sum + price, 0);
```

C# with LINQ:

``` csharp
decimal total = prices.Sum();
```

JavaScript:

``` js
const user = users.find(u => u.id === id);
```

C#:

``` csharp
var user = users.FirstOrDefault(u => u.Id == id);
```

JavaScript asynchronous call:

``` js
const user = await userService.getById(id);
```

C# asynchronous call:

``` csharp
var user = await userService.GetByIdAsync(id);
```

C# methods commonly use the `Async` suffix when they return a task and
perform asynchronous work. `Task<T>` represents an asynchronous
operation that eventually produces a `T`; `Task` represents one that
does not return a value.

### Important C# differences

-   C# uses `PascalCase` for public types and methods in common
    conventions; local variables and parameters usually use `camelCase`.
-   Use `decimal` for many financial values rather than binary
    floating-point types.
-   `==` behaves according to the type's equality implementation;
    understand value versus reference equality.
-   `null` is explicit, and nullable reference types help identify
    potential null issues.
-   C# uses `using` directives for namespaces; `using`
    statements/declarations can also manage disposable resources.
-   `var` infers a compile-time type; it does **not** make the variable
    dynamically typed.
-   `await` should generally be used instead of blocking asynchronous
    work with `.Result` or `.Wait()` in web request paths.

------------------------------------------------------------------------

## 8. Routing and HTTP responses: Express to ASP.NET Core

Express:

``` js
router.get("/:id", async (req, res) => {
  const item = await service.getById(req.params.id);
  if (!item) return res.status(404).json({ message: "Not found" });
  return res.json(item);
});
```

ASP.NET Core controller:

``` csharp
[HttpGet("{id:int}")]
public async Task<ActionResult<ProductResponseDto>> GetById(int id)
{
    var product = await _productService.GetByIdAsync(id);

    if (product is null)
        return NotFound(new { message = "Not found" });

    return Ok(product);
}
```

Common status codes:

  -----------------------------------------------------------------------------
  Status                        Meaning                 Typical use
  ----------------------------- ----------------------- -----------------------
  `200 OK`                      Successful request      Read or update returns
                                                        a result

  `201 Created`                 Resource created        Successful POST

  `204 No Content`              Success with no         Successful delete
                                response body           

  `400 Bad Request`             Invalid input           Validation or malformed
                                                        request

  `401 Unauthorized`            Authentication          Invalid or absent
                                missing/invalid         credentials

  `403 Forbidden`               Authenticated but not   Insufficient permission
                                permitted               

  `404 Not Found`               Resource does not exist Unknown ID

  `409 Conflict`                Conflicting state       Duplicate or
                                                        incompatible update

  `500 Internal Server Error`   Unexpected server       Unhandled server-side
                                failure                 problem
  -----------------------------------------------------------------------------

Use meaningful HTTP status codes. Do not return `200 OK` for every
outcome.

------------------------------------------------------------------------

## 9. Database and EF Core: an important design decision

In MERN, you likely used MongoDB and Mongoose. In .NET, many business
applications use a relational database and EF Core. You can choose the
database according to your project requirements.

### Option A: SQL Server + EF Core

A natural learning choice for many ASP.NET Core roles, especially in
Microsoft-oriented environments.

### Option B: PostgreSQL or MySQL + EF Core

Also valid relational database choices. Confirm the required EF Core
provider and version compatibility.

### Option C: MongoDB

You can continue using MongoDB with the MongoDB .NET/C# driver. You do
not have to switch to SQL just because you are moving to ASP.NET Core.

### What EF Core does

EF Core maps C# entities to relational tables, tracks changes,
translates LINQ queries to database queries, and supports migrations.

Example entity:

``` csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public decimal Price { get; set; }
}
```

Example DbContext:

``` csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    {
    }

    public DbSet<Product> Products => Set<Product>();
}
```

Registration (provider and connection string must match your database):

``` csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")));
```

This example needs the SQL Server EF Core provider package and the
appropriate `using Microsoft.EntityFrameworkCore;` directive. Keep the
actual connection string in local secrets/environment configuration for
sensitive environments.

### Migrations

Migrations help keep the relational database schema aligned with your EF
Core model.

Common commands, after installing the EF Core CLI tool and
provider/design packages as needed:

``` bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

The exact setup depends on the EF Core version, installed tools, and
project structure. Review generated migrations before applying them,
particularly against a production database.

### EF Core concepts to learn

-   `DbContext` and `DbSet<T>`
-   Entity relationships: one-to-one, one-to-many, many-to-many
-   LINQ queries and projections
-   Tracking versus `AsNoTracking()`
-   Async calls such as `ToListAsync()` and `SaveChangesAsync()`
-   Migrations
-   Transactions and concurrency
-   Query performance and indexes
-   Avoiding N+1 query patterns

Do not use MongoDB-style document modeling and SQL relational modeling
interchangeably; each database has different strengths and trade-offs.

------------------------------------------------------------------------

## 10. Authentication and authorization

Your Express experience with JWT transfers well conceptually.

Typical flow:

1.  User sends credentials to a login endpoint.
2.  Server validates the credentials against stored password hashes.
3.  Server issues a signed access token if authentication succeeds.
4.  Client sends `Authorization: Bearer <token>` on protected requests.
5.  ASP.NET Core validates the token.
6.  `[Authorize]` or policy/role rules restrict access to protected
    endpoints.

Example controller attributes:

``` csharp
[Authorize]
[HttpGet("profile")]
public IActionResult GetProfile()
{
    return Ok(new { message = "Authenticated request" });
}
```

For role-based access:

``` csharp
[Authorize(Roles = "Admin")]
[HttpDelete("{id:int}")]
public IActionResult DeleteProduct(int id)
{
    return NoContent();
}
```

These examples assume authentication has been configured correctly in
`Program.cs`. Attributes alone do not implement authentication.

Security checklist: - Never store plain-text passwords; use a proven
password-hashing system or ASP.NET Core Identity. - Validate token
issuer, audience, signing key, and expiration. - Keep signing secrets
out of source control. - Use HTTPS in deployment. - Enforce
authorization on the server, not just by hiding UI buttons. - Validate
and authorize uploaded files and other user-provided content. - Use
short-lived access tokens and an appropriate refresh-token strategy when
needed. - Do not put sensitive data in JWT payloads; signed tokens are
not automatically encrypted.

------------------------------------------------------------------------

## 11. Validation, errors, logging, and API documentation

### Validation

Use request DTOs and validation. For example:

``` csharp
using System.ComponentModel.DataAnnotations;

public class CreateProductDto
{
    [Required]
    [StringLength(100, MinimumLength = 2)]
    public string Name { get; set; } = string.Empty;

    [Range(0.01, 1000000)]
    public decimal Price { get; set; }
}
```

With `[ApiController]`, invalid model input typically results in an
automatic `400 Bad Request` response. More complex validation may
require custom validators or service-level business rules.

### Error handling

Use centralized exception handling and consistent problem responses
instead of exposing stack traces to clients. Log technical details
server-side while returning safe, useful messages to clients.

### Logging

Use `ILogger<T>` for structured logs. Avoid logging passwords, tokens,
or sensitive personal data.

### API documentation

OpenAPI/Swagger tooling can describe endpoints, parameters, response
schemas, and authentication requirements. Package and template defaults
vary across .NET versions, so follow the current template's setup rather
than copying old tutorial instructions blindly.

------------------------------------------------------------------------

## 12. How to organize a real project

A simple project can keep everything in one ASP.NET Core Web API
project. For a larger project, a layered structure might look like this:

``` text
GovResolve.sln
├── GovResolve.Api/
│   ├── Controllers/
│   ├── Middleware/
│   ├── Program.cs
│   └── appsettings.json
├── GovResolve.Application/
│   ├── DTOs/
│   ├── Interfaces/
│   └── Services/
├── GovResolve.Domain/
│   ├── Entities/
│   └── Enums/
├── GovResolve.Infrastructure/
│   ├── Data/
│   ├── Repositories/
│   └── ExternalServices/
└── GovResolve.Tests/
```

This is one possible layered architecture, not a requirement. Multiple
projects add structure but also complexity. Start with a clean single
API project unless you have a real reason to split the solution.

### What belongs where?

-   **API:** HTTP endpoints, authentication setup, request pipeline,
    API-specific configuration.
-   **Application:** use cases and business rules orchestration.
-   **Domain:** core entities and domain rules that should not depend on
    web/database frameworks.
-   **Infrastructure:** database implementation, email providers, file
    storage, external APIs.
-   **Tests:** unit tests and integration tests.

Avoid creating interfaces and layers for every tiny class just to
imitate an architecture diagram. Add abstractions where they clarify
responsibilities, enable testing, or isolate change.

------------------------------------------------------------------------

## 13. Testing in .NET

You should test business logic and important API behavior.

-   **Unit tests:** test a method or service in isolation, often with
    fakes or mocks.
-   **Integration tests:** test the API with its routing, middleware,
    and dependencies.
-   **Database tests:** verify persistence behavior using an appropriate
    test database or test setup.

Common tools include xUnit, NUnit, MSTest, and
`Microsoft.AspNetCore.Mvc.Testing`. A good first milestone is to test a
service's business rules and one endpoint's success and failure paths.

------------------------------------------------------------------------

## 14. Deployment: what is different?

An ASP.NET Core app can run on Windows or Linux and can be
containerized. Common hosting options include IIS, Azure App Service,
Linux servers, and Docker-based platforms.

Typical production considerations: - Publish with `dotnet publish`. -
Configure production environment variables and secrets. - Configure the
database and apply reviewed migrations using a controlled process. - Use
HTTPS and proper authentication/authorization settings. - Add logging,
health checks, monitoring, and backups where appropriate. - Keep the
runtime and dependencies supported and patched.

A development machine's `appsettings.Development.json` should not be
treated as production configuration. Never commit production secrets.

------------------------------------------------------------------------

## 15. Common mistakes when moving from Express to .NET

1.  **Putting all logic in controllers.** Keep controllers focused on
    HTTP; move business rules into services.
2.  **Skipping async database methods.** Use asynchronous EF Core
    operations for I/O-bound request work.
3.  **Using `new` for every dependency.** Learn DI and constructor
    injection.
4.  **Returning database entities everywhere.** Use DTOs where they
    create a clearer and safer API contract.
5.  **Adding a repository layer without a reason.** EF Core may be
    enough for a small application.
6.  **Treating authentication as authorization.** Knowing who the user
    is does not automatically mean they can perform every action.
7.  **Ignoring middleware order.** Authentication, authorization, error
    handling, and CORS must be configured intentionally.
8.  **Hardcoding secrets.** Use development secrets and deployment
    secret management.
9.  **Using synchronous/blocking calls for asynchronous I/O.** Prefer
    `async`/`await`.
10. **Copying old tutorials without checking versions.** .NET templates
    and OpenAPI packages change; follow documentation for your installed
    SDK.
11. **Overengineering the first project.** Start with a small API, then
    introduce more layers when the needs become clear.
12. **Thinking you must abandon MongoDB.** You can use MongoDB with
    .NET; SQL Server plus EF Core is simply a common alternative.

------------------------------------------------------------------------

## 16. A practical 3-week learning plan

Assume about 1--2 focused hours per day. Move faster or slower depending
on your existing C# comfort.

### Week 1 --- C# and ASP.NET Core foundations

-   Day 1: .NET SDK, CLI, project templates, `Program.cs`, run an API.
-   Day 2: C# classes, properties, constructors, interfaces, access
    modifiers.
-   Day 3: collections, generics, LINQ, nullable types.
-   Day 4: `async`/`await`, `Task<T>`, exceptions.
-   Day 5: controllers, routes, route/query/body binding, status codes.
-   Day 6: middleware pipeline, configuration, dependency injection.
-   Day 7: build a small in-memory CRUD API and test it in Postman.

### Week 2 --- Database and production-quality API basics

-   Day 8: choose SQL Server or another database; learn connection
    configuration.
-   Day 9: EF Core `DbContext`, entities, `DbSet`, LINQ.
-   Day 10: migrations and relationships.
-   Day 11: DTOs, validation, centralized error handling.
-   Day 12: authentication and authorization fundamentals.
-   Day 13: logging and OpenAPI/Swagger documentation.
-   Day 14: tests and refactoring.

### Week 3 --- Build a complete small project

-   Day 15: write requirements and design the entity relationships.
-   Day 16: create the database model and CRUD endpoints.
-   Day 17: implement service-layer business rules.
-   Day 18: add validation and error handling.
-   Day 19: add authentication and role/ownership checks if needed.
-   Day 20: test, document, and fix edge cases.
-   Day 21: publish locally or to a suitable hosting platform and
    prepare a README.

**Readiness checkpoint:** you should be able to explain the request
pipeline, DI lifetimes, controller/service responsibilities, EF Core
migrations, DTO validation, and how a JWT is validated before you begin
a bigger project.

------------------------------------------------------------------------

## 17. Best first project for your transition

Since you already understand MERN and have worked on a citizen
complaint-management idea, you could build a smaller version of
**GovResolve** as an ASP.NET Core Web API. Reusing familiar requirements
lets you focus on the new backend framework rather than learning an
entirely new domain.

Suggested first scope: 1. Register/login users. 2. Create a complaint
with category, description, area, and optional evidence URL. 3. List a
user's complaints. 4. View complaint details and status. 5. Allow an
authorized municipal staff member to change status. 6. Validate inputs
and return proper status codes. 7. Add filtering by status/category and
basic pagination. 8. Add audit fields such as `CreatedAt` and
`UpdatedAt`. 9. Write tests for permissions and status transitions.

Possible stack: - C# and ASP.NET Core Web API - EF Core + SQL Server
**or** MongoDB with the official .NET driver - JWT bearer authentication
or ASP.NET Core Identity - React frontend, which you can keep using -
Swagger/OpenAPI and Postman - xUnit for tests

Important design rules: - A citizen should not be able to mark their own
complaint as resolved. - Staff permissions should be enforced in the
backend. - Validate file uploads and restrict file type/size if files
are uploaded. - Store evidence in an appropriate file/object-storage
service rather than saving large files directly in a relational database
by default. - Decide explicitly whether complaints are hidden, archived,
or deleted after a period; do not silently delete records needed for
accountability. - Protect location and personal data.

Start with authentication, complaint CRUD, and role-based authorization.
Add duplicate detection, municipal dashboards, notifications, and
prediction features only after the core API is correct.

------------------------------------------------------------------------

## 18. Quick self-check before starting your project

You are ready to begin a small ASP.NET Core API when you can answer
these questions in your own words:

-   [ ] What is the difference between C#, .NET, and ASP.NET Core?
-   [ ] What is configured in `Program.cs`?
-   [ ] What is middleware, and why does its order matter?
-   [ ] What is dependency injection? What do Scoped, Transient, and
    Singleton mean?
-   [ ] What is the difference between a controller and a service?
-   [ ] Why use DTOs rather than accepting database entities directly?
-   [ ] What do `async`, `await`, and `Task<T>` mean?
-   [ ] What does EF Core's `DbContext` do?
-   [ ] What are migrations?
-   [ ] How are authentication and authorization different?
-   [ ] How do you return `400`, `401`, `403`, `404`, and `201`
    appropriately?
-   [ ] How will you keep secrets out of Git?
-   [ ] How will you test the API?

You do not need perfect answers to every advanced topic. If you
understand the fundamentals and can build a small CRUD API
independently, start the project and learn the next concepts as the
requirements demand.

------------------------------------------------------------------------

## 19. Recommended official resources

Use documentation that matches the SDK you install.

-   .NET documentation: https://learn.microsoft.com/dotnet/
-   ASP.NET Core documentation: https://learn.microsoft.com/aspnet/core/
-   C# documentation: https://learn.microsoft.com/dotnet/csharp/
-   EF Core documentation: https://learn.microsoft.com/ef/core/
-   .NET CLI reference: https://learn.microsoft.com/dotnet/core/tools/
-   ASP.NET Core Web API tutorial:
    https://learn.microsoft.com/aspnet/core/tutorials/first-web-api
-   C# fundamentals:
    https://learn.microsoft.com/dotnet/csharp/tour-of-csharp/

### Final advice

Do not try to learn every .NET technology before building something.
Learn the core C# syntax, create a controller-based ASP.NET Core Web
API, connect a database, implement validation and authentication, and
write tests. Your Express/MERN experience already gives you a useful
foundation in APIs and backend architecture.
