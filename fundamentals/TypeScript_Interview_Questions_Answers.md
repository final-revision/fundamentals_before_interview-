# TypeScript Interview Questions & Answers

## Complete TypeScript Interview Guide for JavaScript Developers

> **Target:** Fresher / Internship / Junior Frontend Developer  
> **Assumption:** You already know JavaScript. This guide focuses on what changes when moving from JavaScript to TypeScript, what interviewers commonly ask, and how TypeScript is used in React/Angular/Node.js projects.

---

# Table of Contents

1. TypeScript Fundamentals
2. JavaScript vs TypeScript
3. Type System
4. Variables and Type Inference
5. Functions
6. Objects, Interfaces and Type Aliases
7. Union and Intersection Types
8. Arrays, Tuples and Enums
9. Special Types
10. Type Narrowing and Type Guards
11. Generics
12. Classes and OOP
13. Advanced TypeScript
14. Utility Types
15. Functions and Advanced Generics
16. Modules
17. Error Handling
18. Async/Await and Promises
19. TypeScript with JavaScript
20. TypeScript with React
21. TypeScript with Node.js / Express
22. TypeScript Configuration
23. Compilation and Build Process
24. Common Coding Questions
25. Project-Based Interview Questions
26. Common Tricky Questions
27. Rapid-Fire Questions
28. Most Important Questions for Freshers
29. Final Revision Checklist

---

# 1. TypeScript Fundamentals

## Q1. What is TypeScript?

**Answer:**

TypeScript is a strongly typed programming language developed by Microsoft.

It is a superset of JavaScript, meaning valid JavaScript code is generally valid TypeScript code.

TypeScript adds features such as:

- Static type checking
- Interfaces
- Type aliases
- Generics
- Enums
- Access modifiers
- Advanced type system
- Better tooling and autocomplete

Example:

```typescript
let name: string = "Digvijay";
let age: number = 21;
```

TypeScript code is compiled/transformed into JavaScript that can run in JavaScript environments.

---

## Q2. Why was TypeScript created?

**Answer:**

JavaScript is dynamically typed, so some type-related errors are discovered only when the program runs.

Example JavaScript:

```javascript
function add(a, b) {
    return a + b;
}

add(10, "20");
```

This may produce unexpected behavior.

TypeScript allows us to specify expected types:

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

Now:

```typescript
add(10, "20");
```

produces a compile-time type error.

---

## Q3. Is TypeScript a replacement for JavaScript?

**Answer:**

No.

TypeScript extends JavaScript.

```text
JavaScript
    +
Static Type System
    +
Additional TypeScript Features
    ↓
TypeScript
    ↓
Compiled/Transformed JavaScript
```

The browser ultimately executes JavaScript.

---

## Q4. Is TypeScript strongly typed?

**Answer:**

TypeScript provides static type checking, but it is important to understand that TypeScript's types are primarily checked at compile time.

At runtime, the JavaScript output does not retain TypeScript's static type system.

Example:

```typescript
let age: number = 21;
```

The type annotation helps the compiler, but it is not a runtime validation mechanism.

---

## Q5. What is a superset?

**Answer:**

A superset contains everything from the original language plus additional features.

Since TypeScript builds on JavaScript:

```text
JavaScript
   ↑
TypeScript
```

Most JavaScript syntax can be used in TypeScript.

---

# 2. JavaScript vs TypeScript

## Q6. Difference between JavaScript and TypeScript

| JavaScript | TypeScript |
|---|---|
| Dynamically typed | Statically type-checked |
| Type errors often discovered at runtime | Many type errors discovered before runtime |
| No compilation required for normal browser execution | Usually transpiled/compiled to JavaScript |
| Smaller type system | Rich type system |
| Interfaces not part of JS type system | Interfaces supported |
| Generics not available in this form | Generics supported |
| Suitable for scripting and applications | Useful for large maintainable applications |

---

## Q7. Does TypeScript run directly in the browser?

**Answer:**

Normally, browsers execute JavaScript, not TypeScript source.

Typical flow:

```text
.ts file
   ↓
TypeScript compiler / build tool
   ↓
.js file
   ↓
Browser
```

Modern tools such as Vite, Angular CLI and other bundlers/transpilers handle this process automatically.

---

## Q8. What is transpilation?

**Answer:**

Transpilation converts source code from one language level/form into another compatible form.

For TypeScript:

```text
TypeScript
    ↓
JavaScript
```

The TypeScript compiler (`tsc`) performs type checking and can emit JavaScript.

---

## Q9. What is `tsc`?

**Answer:**

`tsc` is the TypeScript compiler.

Example:

```bash
npx tsc
```

It can:

- Type-check TypeScript
- Compile TypeScript
- Generate JavaScript
- Generate declaration files when configured

---

# 3. Type System

## Q10. What are basic TypeScript types?

Common types include:

```typescript
string
number
boolean
bigint
symbol
null
undefined
object
```

Example:

```typescript
let name: string = "John";
let age: number = 21;
let active: boolean = true;
```

---

## Q11. How do you specify a variable's type?

```typescript
let username: string = "Digvijay";
let age: number = 21;
let isActive: boolean = true;
```

Syntax:

```typescript
let variableName: type = value;
```

---

## Q12. What is type inference?

**Answer:**

TypeScript can automatically determine a variable's type from its initial value.

```typescript
let age = 21;
```

TypeScript infers:

```typescript
age: number
```

Therefore, this is invalid:

```typescript
age = "hello";
```

---

## Q13. Explicit typing vs inference

Explicit:

```typescript
let age: number = 21;
```

Inference:

```typescript
let age = 21;
```

Both result in `age` being treated as a number.

---

## Q14. What is contextual typing?

**Answer:**

TypeScript can infer a type from the context where an expression is used.

Example:

```typescript
const numbers = [1, 2, 3];

numbers.forEach((number) => {
    console.log(number);
});
```

TypeScript knows `number` is a number because of the array's type.

---

## Q15. What is type annotation?

**Answer:**

A type annotation explicitly specifies a type.

```typescript
let username: string;
let age: number;
```

---

## Q16. What is type assertion?

**Answer:**

A type assertion tells TypeScript how you want it to treat a value.

```typescript
const value: unknown = "Hello";

const length = (value as string).length;
```

Another syntax:

```typescript
const length = (<string>value).length;
```

The `as` syntax is preferred in modern code because angle-bracket assertions can conflict with JSX.

---

## Q17. Does type assertion convert a value?

**Answer:**

No.

This is extremely important.

```typescript
const value = "123" as unknown as number;
```

The assertion does not actually convert the string into a number.

Type assertions only affect TypeScript's understanding of the value.

For actual conversion:

```typescript
const value = Number("123");
```

---

# 4. Variables and Type Inference

## Q18. `let` vs `const` in TypeScript

They behave similarly to JavaScript.

```typescript
let age = 21;
age = 22;
```

`const` cannot be reassigned:

```typescript
const name = "Digvijay";
```

TypeScript adds static type checking on top.

---

## Q19. What is literal type?

A literal type represents a specific literal value.

```typescript
let direction: "left" | "right";

direction = "left";
```

This is useful when a variable should accept only a fixed set of values.

---

## Q20. What is `as const`?

`as const` creates readonly literal types rather than widening values.

```typescript
const user = {
    role: "admin"
} as const;
```

The role becomes:

```typescript
"admin"
```

rather than general `string`.

---

# 5. Functions

## Q21. How do you type function parameters?

```typescript
function add(a: number, b: number) {
    return a + b;
}
```

---

## Q22. How do you specify a function return type?

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

Syntax:

```typescript
function name(parameters): returnType {
}
```

---

## Q23. How do you type an arrow function?

```typescript
const add = (a: number, b: number): number => {
    return a + b;
};
```

---

## Q24. What is an optional parameter?

Use `?`.

```typescript
function greet(name?: string) {
    console.log(name);
}
```

The parameter can be omitted.

---

## Q25. What is a default parameter?

Same concept as JavaScript:

```typescript
function greet(name: string = "Guest") {
    console.log(name);
}
```

---

## Q26. What is a rest parameter in TypeScript?

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((total, n) => total + n, 0);
}
```

---

## Q27. How do you type a callback function?

```typescript
function process(
    value: number,
    callback: (result: number) => void
) {
    callback(value);
}
```

---

## Q28. What is function overload?

Function overloads allow multiple call signatures for a function.

```typescript
function getValue(value: string): string;
function getValue(value: number): number;

function getValue(value: string | number): string | number {
    return value;
}
```

The implementation signature must be compatible with the overload signatures.

---

# 6. Objects, Interfaces and Type Aliases

## Q29. How do you type an object?

```typescript
const user: {
    name: string;
    age: number;
} = {
    name: "Digvijay",
    age: 21
};
```

For reusable structures, interfaces or type aliases are usually better.

---

## Q30. What is an interface?

An interface defines the shape/contract of an object.

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}
```

Usage:

```typescript
const user: User = {
    id: 1,
    name: "Digvijay",
    email: "test@example.com"
};
```

---

## Q31. What is a type alias?

A type alias gives a name to a type.

```typescript
type User = {
    id: number;
    name: string;
};
```

---

## Q32. Interface vs type

Both can describe object shapes.

Interface:

```typescript
interface User {
    name: string;
}
```

Type:

```typescript
type User = {
    name: string;
};
```

Interfaces are especially useful for object-oriented contracts and declaration merging.

Type aliases are especially flexible for unions, intersections, tuples and other type expressions.

Example:

```typescript
type Status = "loading" | "success" | "error";
```

---

## Q33. Can interfaces be extended?

Yes.

```typescript
interface Person {
    name: string;
}

interface Employee extends Person {
    employeeId: number;
}
```

---

## Q34. Can a type alias be combined?

Yes, using intersections.

```typescript
type Person = {
    name: string;
};

type Employee = Person & {
    employeeId: number;
};
```

---

## Q35. What is an optional property?

```typescript
interface User {
    name: string;
    age?: number;
}
```

`age` may be absent.

---

## Q36. What is a readonly property?

```typescript
interface User {
    readonly id: number;
    name: string;
}
```

TypeScript prevents assignment to `id` through that typed reference.

---

## Q37. What is index signature?

It describes objects with dynamic keys.

```typescript
interface Scores {
    [subject: string]: number;
}

const scores: Scores = {
    math: 90,
    science: 85
};
```

---

# 7. Union and Intersection Types

## Q38. What is a union type?

A union allows a value to be one of several types.

```typescript
let id: string | number;

id = 10;
id = "ABC";
```

---

## Q39. Why are union types useful?

They model values that legitimately have different possible forms.

Example:

```typescript
type Status = "loading" | "success" | "error";
```

This is safer than using a generic string:

```typescript
let status: string;
```

---

## Q40. What is an intersection type?

An intersection combines multiple types.

```typescript
type Person = {
    name: string;
};

type Employee = {
    employeeId: number;
};

type EmployeeDetails = Person & Employee;
```

Now:

```typescript
const employee: EmployeeDetails = {
    name: "John",
    employeeId: 101
};
```

---

## Q41. Union vs intersection

```text
Union:        A OR B
Intersection: A AND B
```

Example:

```typescript
type ID = string | number;
```

means string OR number.

```typescript
type Employee = Person & Job;
```

means it must satisfy both types.

---

# 8. Arrays, Tuples and Enums

## Q42. How do you define an array?

```typescript
let numbers: number[] = [1, 2, 3];
```

Alternative:

```typescript
let numbers: Array<number> = [1, 2, 3];
```

---

## Q43. How do you define an array of objects?

```typescript
interface Employee {
    id: number;
    name: string;
}

const employees: Employee[] = [
    { id: 1, name: "A" },
    { id: 2, name: "B" }
];
```

---

## Q44. What is a tuple?

A tuple represents an array with a known number and order of elements.

```typescript
let user: [number, string] = [1, "John"];
```

The first value is a number and the second is a string.

---

## Q45. Tuple vs array

Array:

```typescript
string[]
```

Can contain many strings.

Tuple:

```typescript
[string, number]
```

Has a defined structure and position-specific types.

---

## Q46. What is an enum?

Enums define named constants.

```typescript
enum Role {
    Admin,
    User,
    Guest
}
```

Usage:

```typescript
let role: Role = Role.Admin;
```

For many application cases, string literal unions are also a simple alternative:

```typescript
type Role = "admin" | "user" | "guest";
```

---

# 9. Special Types

## Q47. What is `any`?

`any` disables most static type checking for a value.

```typescript
let value: any = 10;
value = "hello";
value = true;
```

It should be used carefully because it removes many benefits of TypeScript.

---

## Q48. What is `unknown`?

`unknown` represents a value whose type is not known yet.

Unlike `any`, you must narrow or otherwise safely establish its type before performing most operations.

```typescript
let value: unknown = "Hello";

if (typeof value === "string") {
    console.log(value.length);
}
```

---

## Q49. `any` vs `unknown`

| any | unknown |
|---|---|
| Allows almost anything | Requires type checking before most operations |
| Reduces type safety | Preserves type safety |
| Easier but risky | Safer for uncertain data |

**Interview answer:** Prefer `unknown` when the type is genuinely unknown.

---

## Q50. What is `never`?

`never` represents a value that never occurs.

Example:

```typescript
function fail(message: string): never {
    throw new Error(message);
}
```

It can also appear in exhaustive checking.

---

## Q51. What is `void`?

`void` is commonly used for functions that don't return a useful value.

```typescript
function logMessage(message: string): void {
    console.log(message);
}
```

---

## Q52. `null` vs `undefined`

Both are JavaScript values.

TypeScript can distinguish them depending on compiler settings, especially `strictNullChecks`.

```typescript
let value: string | null = null;
```

---

## Q53. What is `object` type?

`object` represents non-primitive values.

For example:

```typescript
let user: object = {
    name: "John"
};
```

For real applications, a specific interface/type is usually more useful than generic `object`.

---

# 10. Type Narrowing and Type Guards

## Q54. What is type narrowing?

Type narrowing means reducing a broad type to a more specific type based on runtime checks.

Example:

```typescript
function print(value: string | number) {
    if (typeof value === "string") {
        console.log(value.toUpperCase());
    } else {
        console.log(value.toFixed(2));
    }
}
```

---

## Q55. What is `typeof` type guard?

```typescript
if (typeof value === "string") {
    // value is string here
}
```

---

## Q56. What is `instanceof`?

Used to check whether an object is an instance of a class/constructor.

```typescript
if (error instanceof Error) {
    console.log(error.message);
}
```

---

## Q57. What is the `in` operator for narrowing?

```typescript
if ("email" in user) {
    console.log(user.email);
}
```

It can help distinguish object types based on property presence.

---

## Q58. What is a custom type guard?

A function can return a type predicate.

```typescript
function isString(value: unknown): value is string {
    return typeof value === "string";
}
```

Usage:

```typescript
if (isString(value)) {
    console.log(value.toUpperCase());
}
```

---

# 11. Generics

## Q59. What are generics?

Generics allow reusable code to work with different types while preserving type information.

```typescript
function identity<T>(value: T): T {
    return value;
}
```

Usage:

```typescript
identity<number>(10);
identity<string>("Hello");
```

---

## Q60. Why use generics instead of `any`?

With `any`:

```typescript
function identity(value: any): any {
    return value;
}
```

Type information is lost.

With generics:

```typescript
function identity<T>(value: T): T {
    return value;
}
```

The input and output types remain connected.

---

## Q61. Generic interface

```typescript
interface ApiResponse<T> {
    data: T;
    success: boolean;
    message: string;
}
```

Usage:

```typescript
const response: ApiResponse<User> = {
    data: {
        id: 1,
        name: "John"
    },
    success: true,
    message: "Success"
};
```

---

## Q62. Generic constraints

You can restrict what types a generic accepts.

```typescript
function getLength<T extends { length: number }>(value: T): number {
    return value.length;
}
```

This works for strings and arrays because they have a `length` property.

---

## Q63. Generic class

```typescript
class Box<T> {
    constructor(public value: T) {}

    getValue(): T {
        return this.value;
    }
}

const box = new Box<number>(10);
```

---

# 12. Classes and OOP

## Q64. Does TypeScript support classes?

Yes.

```typescript
class Employee {
    constructor(
        public name: string,
        public salary: number
    ) {}
}
```

---

## Q65. What are access modifiers?

TypeScript supports:

- `public`
- `private`
- `protected`

Example:

```typescript
class Employee {
    public name: string;
    private salary: number;
    protected department: string;

    constructor(
        name: string,
        salary: number,
        department: string
    ) {
        this.name = name;
        this.salary = salary;
        this.department = department;
    }
}
```

---

## Q66. What is `public`?

A public member can be accessed from outside the class.

```typescript
employee.name;
```

---

## Q67. What is `private`?

A private member can only be accessed within the class according to TypeScript's type system.

```typescript
class Employee {
    private salary = 50000;
}
```

---

## Q68. What is `protected`?

A protected member can be accessed inside the class and its subclasses.

---

## Q69. What is `readonly` in classes?

```typescript
class User {
    readonly id: number;

    constructor(id: number) {
        this.id = id;
    }
}
```

The property cannot be reassigned through that class type after initialization.

---

## Q70. What is an abstract class?

An abstract class cannot be instantiated directly and can define abstract members.

```typescript
abstract class Animal {
    abstract sound(): void;

    move(): void {
        console.log("Moving");
    }
}
```

---

## Q71. What is an interface implementation?

```typescript
interface Payment {
    pay(amount: number): void;
}

class UpiPayment implements Payment {
    pay(amount: number): void {
        console.log(`Paid ${amount}`);
    }
}
```

---

# 13. Advanced TypeScript

## Q72. What is `keyof`?

`keyof` produces a union of property names of a type.

```typescript
interface User {
    id: number;
    name: string;
}

type UserKeys = keyof User;
```

`UserKeys` becomes:

```typescript
"id" | "name"
```

---

## Q73. What is indexed access type?

```typescript
interface User {
    id: number;
    name: string;
}

type UserName = User["name"];
```

`UserName` is `string`.

---

## Q74. What is `typeof` in a type position?

TypeScript's `typeof` can extract the type of an existing value.

```typescript
const user = {
    id: 1,
    name: "John"
};

type User = typeof user;
```

---

## Q75. What is `typeof` in JavaScript vs TypeScript?

Runtime JavaScript:

```typescript
typeof value
```

checks the runtime type category.

TypeScript type position:

```typescript
type User = typeof user;
```

extracts a static type from a value.

---

## Q76. What is `infer`?

`infer` is used inside conditional types to infer a type.

Example:

```typescript
type ReturnTypeOf<T> =
    T extends (...args: any[]) => infer R ? R : never;
```

It extracts the return type of a function type.

---

## Q77. What are conditional types?

Conditional types select one type or another based on a condition.

```typescript
type IsString<T> =
    T extends string ? true : false;
```

---

## Q78. What are mapped types?

Mapped types create new types by transforming properties of an existing type.

Example:

```typescript
type ReadonlyUser<T> = {
    readonly [K in keyof T]: T[K];
};
```

---

## Q79. What are template literal types?

They allow types based on template string patterns.

```typescript
type EventName = `on${string}`;
```

Examples:

```typescript
let event: EventName = "onclick";
```

---

## Q80. What is declaration merging?

Some declarations, especially interfaces, can be combined when they have the same name.

```typescript
interface User {
    name: string;
}

interface User {
    age: number;
}
```

The resulting `User` has both properties.

---

# 14. Utility Types

## Q81. What are utility types?

Utility types are built-in generic types that transform existing types.

Common ones:

- `Partial`
- `Required`
- `Readonly`
- `Pick`
- `Omit`
- `Record`
- `Exclude`
- `Extract`
- `NonNullable`
- `ReturnType`
- `Parameters`

---

## Q82. What is `Partial<T>`?

Makes all properties optional.

```typescript
interface User {
    name: string;
    age: number;
}

type UpdateUser = Partial<User>;
```

Equivalent conceptually to:

```typescript
{
    name?: string;
    age?: number;
}
```

Useful for update operations.

---

## Q83. What is `Required<T>`?

Makes optional properties required.

```typescript
type RequiredUser = Required<User>;
```

---

## Q84. What is `Readonly<T>`?

Makes properties readonly.

```typescript
type ReadonlyUser = Readonly<User>;
```

---

## Q85. What is `Pick<T, K>`?

Selects specific properties.

```typescript
type UserPreview = Pick<User, "name" | "age">;
```

---

## Q86. What is `Omit<T, K>`?

Removes selected properties.

```typescript
type PublicUser = Omit<User, "password">;
```

This is very useful for preventing sensitive fields from being represented in a particular type.

---

## Q87. What is `Record<K, T>`?

Creates an object type with keys `K` and values `T`.

```typescript
type Scores = Record<string, number>;
```

---

## Q88. What is `Exclude<T, U>`?

Removes from `T` those union members assignable to `U`.

```typescript
type Status = "loading" | "success" | "error";

type WithoutError = Exclude<Status, "error">;
```

Result:

```typescript
"loading" | "success"
```

---

## Q89. What is `Extract<T, U>`?

Keeps only union members from `T` that are assignable to `U`.

---

## Q90. What is `ReturnType<T>`?

Extracts the return type of a function.

```typescript
function getUser() {
    return {
        id: 1,
        name: "John"
    };
}

type User = ReturnType<typeof getUser>;
```

---

## Q91. What is `Parameters<T>`?

Extracts a function's parameter types as a tuple.

```typescript
function add(a: number, b: number) {
    return a + b;
}

type Params = Parameters<typeof add>;
```

`Params` becomes:

```typescript
[number, number]
```

---

# 15. Functions and Advanced Generics

## Q92. What is a generic function?

```typescript
function first<T>(items: T[]): T | undefined {
    return items[0];
}
```

---

## Q93. Generic constraints with `keyof`

A useful pattern is:

```typescript
function getProperty<T, K extends keyof T>(
    object: T,
    key: K
): T[K] {
    return object[key];
}
```

Usage:

```typescript
const user = {
    name: "John",
    age: 21
};

getProperty(user, "name");
getProperty(user, "age");
```

TypeScript prevents invalid keys.

---

## Q94. What is a generic default?

```typescript
interface ApiResponse<T = string> {
    data: T;
}
```

If no type argument is supplied, `string` is used as the default.

---

## Q95. What is a function type?

```typescript
type AddFunction = (a: number, b: number) => number;
```

Usage:

```typescript
const add: AddFunction = (a, b) => a + b;
```

---

# 16. Modules

## Q96. What is a module?

A module is a file with its own scope that can export and import values/types.

```typescript
export interface User {
    id: number;
}
```

Import:

```typescript
import { User } from "./models";
```

---

## Q97. Named export vs default export

Named:

```typescript
export const add = () => {};
```

Import:

```typescript
import { add } from "./math";
```

Default:

```typescript
export default function add() {}
```

Import:

```typescript
import add from "./math";
```

---

## Q98. Can types be imported separately?

Yes.

```typescript
import type { User } from "./types";
```

This makes the intent clear and can prevent unnecessary runtime import behavior.

---

# 17. Error Handling

## Q99. How do you type errors in a catch block?

Modern TypeScript can treat caught errors as `unknown` under strict configurations.

Safe approach:

```typescript
try {
    // code
} catch (error) {
    if (error instanceof Error) {
        console.log(error.message);
    }
}
```

---

## Q100. Why is `unknown` useful for errors?

JavaScript allows anything to be thrown:

```typescript
throw "Something went wrong";
```

or:

```typescript
throw new Error("Something went wrong");
```

Therefore, assuming that every caught value is an `Error` is unsafe without checking.

---

# 18. Async/Await and Promises

## Q101. How do you type a Promise?

```typescript
async function getUser(): Promise<User> {
    const response = await fetch("/api/user");
    return response.json();
}
```

A more precise API implementation should validate external data when runtime validation is required; TypeScript alone does not validate JSON at runtime.

---

## Q102. How do you type an async function that returns nothing?

```typescript
async function saveUser(): Promise<void> {
    // ...
}
```

---

## Q103. What is the return type of an async function?

An async function always returns a `Promise`.

```typescript
async function getNumber(): Promise<number> {
    return 10;
}
```

---

## Q104. How do you type `fetch()` response data?

You can specify the expected compile-time shape:

```typescript
interface User {
    id: number;
    name: string;
}

async function getUser(): Promise<User> {
    const response = await fetch("/api/user");
    return response.json();
}
```

Important: the TypeScript annotation does not validate that the server actually returned a `User` at runtime.

---

# 19. TypeScript with JavaScript

## Q105. Can existing JavaScript be converted to TypeScript?

Yes.

A common migration approach:

```text
JavaScript files
      ↓
Add TypeScript
      ↓
Rename files to .ts/.tsx gradually
      ↓
Add types incrementally
      ↓
Enable stricter compiler options over time
```

---

## Q106. What is `allowJs`?

It allows JavaScript files to be included in a TypeScript project.

Example:

```json
{
    "compilerOptions": {
        "allowJs": true
    }
}
```

---

## Q107. What is `checkJs`?

`checkJs` enables type checking for JavaScript files in supported project configurations.

---

## Q108. What is JSDoc?

JSDoc can provide type information in JavaScript files.

Example:

```javascript
/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a, b) {
    return a + b;
}
```

This allows TypeScript tooling to provide type checking without converting the file to `.ts`.

---

# 20. TypeScript with React

Since you already know JavaScript and React, these are especially important.

## Q109. Why use TypeScript with React?

**Answer:**

TypeScript helps catch mistakes in:

- Props
- State
- Event handlers
- API responses
- Component interfaces
- Hooks
- Function parameters

It also improves autocomplete and refactoring.

---

## Q110. How do you type React props?

```tsx
interface UserCardProps {
    name: string;
    age: number;
}

function UserCard({ name, age }: UserCardProps) {
    return (
        <div>
            {name} - {age}
        </div>
    );
}
```

---

## Q111. How do you type optional React props?

```tsx
interface ButtonProps {
    text: string;
    disabled?: boolean;
}
```

---

## Q112. How do you type `useState`?

Often TypeScript infers the type:

```tsx
const [count, setCount] = useState(0);
```

For more complex cases:

```tsx
interface User {
    id: number;
    name: string;
}

const [user, setUser] = useState<User | null>(null);
```

---

## Q113. How do you type an array state?

```tsx
const [users, setUsers] = useState<User[]>([]);
```

---

## Q114. How do you type an input change event?

```tsx
const handleChange = (
    event: React.ChangeEvent<HTMLInputElement>
) => {
    console.log(event.target.value);
};
```

---

## Q115. How do you type a button click event?

```tsx
const handleClick = (
    event: React.MouseEvent<HTMLButtonElement>
) => {
    console.log("Clicked");
};
```

---

## Q116. How do you type form submit?

```tsx
const handleSubmit = (
    event: React.FormEvent<HTMLFormElement>
) => {
    event.preventDefault();
};
```

---

## Q117. What is `.tsx`?

`.tsx` is used for TypeScript files that contain JSX.

```text
.ts  → TypeScript
.tsx → TypeScript + JSX
```

---

## Q118. How do you type children in React?

A common option is:

```tsx
import type { ReactNode } from "react";

interface CardProps {
    children: ReactNode;
}
```

---

## Q119. How do you type a React component's return value?

A component can often rely on inference.

You can also explicitly use:

```tsx
function App(): JSX.Element {
    return <h1>Hello</h1>;
}
```

Depending on the React/type package version, `React.ReactNode` or other appropriate types may also be used. In many cases, inference is preferred.

---

## Q120. How do you type API data in React?

```typescript
interface Product {
    id: number;
    name: string;
    price: number;
}

async function getProducts(): Promise<Product[]> {
    const response = await fetch("/api/products");
    return response.json();
}
```

Remember: this describes the expected shape at compile time; external data should be validated at runtime when the boundary is untrusted.

---

# 21. TypeScript with Node.js / Express

## Q121. Why use TypeScript with Node.js?

It provides:

- Static type checking
- Better IDE support
- Better refactoring
- Safer API contracts
- Better maintainability
- Stronger structure for large backend projects

---

## Q122. How do you type an Express request?

Example:

```typescript
import { Request, Response } from "express";

app.get("/users", (req: Request, res: Response) => {
    res.json([]);
});
```

---

## Q123. How do you type request body?

```typescript
interface CreateUserBody {
    name: string;
    email: string;
}

app.post(
    "/users",
    (req: Request<{}, {}, CreateUserBody>, res: Response) => {
        const { name, email } = req.body;
        res.json({ name, email });
    }
);
```

---

## Q124. Why should request data still be validated?

TypeScript types disappear at runtime.

A client can send:

```json
{
    "name": 123
}
```

even if your TypeScript type says:

```typescript
interface CreateUserBody {
    name: string;
}
```

Therefore, runtime validation is needed at external boundaries.

Libraries such as Zod can be used for runtime validation.

---

# 22. TypeScript Configuration

## Q125. What is `tsconfig.json`?

`tsconfig.json` defines compiler/project settings for a TypeScript project.

Example:

```json
{
    "compilerOptions": {
        "target": "ES2022",
        "module": "ESNext",
        "strict": true,
        "outDir": "./dist"
    },
    "include": ["src"]
}
```

---

## Q126. What is `strict`?

`strict` enables a broad set of strict type-checking options.

It helps catch more errors during development.

For interview purposes:

> Strict mode makes TypeScript's type checking more rigorous and is generally recommended for new projects.

---

## Q127. What is `noImplicitAny`?

It reports errors when TypeScript would otherwise infer an implicit `any` type in situations covered by the option.

---

## Q128. What is `strictNullChecks`?

It makes `null` and `undefined` distinct types that must be handled explicitly where appropriate.

Example:

```typescript
let name: string = null;
```

Under strict null checking, this is an error.

Correct:

```typescript
let name: string | null = null;
```

---

## Q129. What is `noImplicitReturns`?

It checks that functions do not accidentally have missing return statements in paths where a value is expected.

---

## Q130. What is `target`?

`target` specifies the JavaScript language version that TypeScript should emit.

Example:

```json
{
    "compilerOptions": {
        "target": "ES2022"
    }
}
```

---

## Q131. What is `module`?

`module` controls the module system of emitted JavaScript or how module code is handled.

Examples can include:

```text
ESNext
CommonJS
NodeNext
```

The appropriate choice depends on the project's runtime and tooling.

---

## Q132. What is `outDir`?

It specifies where compiled output is generated.

```json
{
    "compilerOptions": {
        "outDir": "./dist"
    }
}
```

---

## Q133. What is `rootDir`?

It indicates the root directory of the input source files for compilation and influences output structure.

---

## Q134. What is `include`?

It specifies files/directories that should be included in the TypeScript project.

```json
{
    "include": ["src/**/*"]
}
```

---

## Q135. What is `exclude`?

It specifies files/directories that should be excluded from project processing.

---

# 23. Compilation and Build Process

## Q136. Explain TypeScript compilation.

Typical process:

```text
TypeScript Source
       ↓
Type Checking
       ↓
Transpilation
       ↓
JavaScript Output
       ↓
Bundling (if build tool is used)
       ↓
Browser / Node.js
```

---

## Q137. What happens to TypeScript types after compilation?

TypeScript's static type annotations are generally erased from emitted JavaScript.

Example:

```typescript
const age: number = 21;
```

can become:

```javascript
const age = 21;
```

---

## Q138. Does TypeScript improve runtime performance?

Not directly.

TypeScript primarily improves developer experience and compile-time correctness.

Runtime performance depends mainly on the emitted JavaScript and the environment.

---

## Q139. What is source map?

Source maps allow debugging tools to map generated JavaScript back to original TypeScript source.

Example configuration:

```json
{
    "compilerOptions": {
        "sourceMap": true
    }
}
```

---

# 24. Common Coding Questions

## Q140. Create a typed function to add two numbers.

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

---

## Q141. Create a typed function to check even number.

```typescript
function isEven(n: number): boolean {
    return n % 2 === 0;
}
```

---

## Q142. Find maximum number.

```typescript
function findMax(numbers: number[]): number {
    return Math.max(...numbers);
}
```

---

## Q143. Remove duplicates.

```typescript
function removeDuplicates(numbers: number[]): number[] {
    return [...new Set(numbers)];
}
```

---

## Q144. Count frequencies.

```typescript
function frequency(numbers: number[]): Map<number, number> {
    const result = new Map<number, number>();

    for (const number of numbers) {
        result.set(
            number,
            (result.get(number) ?? 0) + 1
        );
    }

    return result;
}
```

---

## Q145. Find users by age.

```typescript
interface User {
    name: string;
    age: number;
}

function getAdults(users: User[]): User[] {
    return users.filter(user => user.age >= 18);
}
```

---

## Q146. Get only names.

```typescript
function getNames(users: User[]): string[] {
    return users.map(user => user.name);
}
```

---

## Q147. Create a generic identity function.

```typescript
function identity<T>(value: T): T {
    return value;
}
```

---

## Q148. Create a generic API response.

```typescript
interface ApiResponse<T> {
    data: T;
    success: boolean;
}

const response: ApiResponse<User> = {
    data: {
        name: "John",
        age: 21
    },
    success: true
};
```

---

## Q149. Safely handle unknown input.

```typescript
function printValue(value: unknown): void {
    if (typeof value === "string") {
        console.log(value.toUpperCase());
    } else if (typeof value === "number") {
        console.log(value.toFixed(2));
    }
}
```

---

## Q150. Create a union for API status.

```typescript
type Status =
    | "loading"
    | "success"
    | "error";
```

---

# 25. Project-Based Interview Questions

## Q151. Why did you use TypeScript in your React project?

**Sample Answer:**

> I used TypeScript because it provides static type checking and makes the React application easier to maintain. I used interfaces or type aliases for component props and API response models, typed state and event handlers, and used union types for fixed states such as loading, success and error. This helped catch many mistakes during development before runtime.

---

## Q152. How did you type React props?

**Sample Answer:**

> I created interfaces or type aliases for component props. For example, a UserCard component can accept a `UserCardProps` type containing name, email and other required fields. This gives me autocomplete and compile-time checking when using the component.

---

## Q153. How did you type API responses?

**Sample Answer:**

> I created TypeScript interfaces representing the expected API response and used those types in service functions and component state. I also understand that TypeScript does not validate external JSON at runtime, so for critical external data I would use runtime validation as well.

---

## Q154. What if the backend API changes a property?

**Answer:**

TypeScript can identify many compile-time usages that need updating if the shared type is updated.

For example:

```typescript
interface User {
    id: number;
    fullName: string;
}
```

If the backend changes `fullName` to `name`, TypeScript can reveal affected frontend code after the model is updated.

For stronger API contract synchronization, teams can generate types from an OpenAPI specification or share schemas where appropriate.

---

## Q155. How did TypeScript help you during development?

**Sample Answer:**

> It helped me catch incorrect function arguments, missing object properties, incorrect component props and incorrect state assignments before running the application. It also improved autocomplete and made refactoring safer.

---

## Q156. What is one disadvantage of TypeScript?

**Answer:**

There is an initial learning curve and additional type definitions to maintain.

There can also be complexity when working with advanced generic and conditional types.

However, for larger applications, the improved tooling and maintainability can be valuable.

---

## Q157. Would you use `any` in a project?

**Sample Answer:**

> I would avoid `any` unless there is a specific reason. If the type is genuinely unknown, I prefer `unknown` and then narrow it safely. If a third-party library has incomplete typings, I might temporarily use a controlled escape hatch, but I would try to improve the type definition rather than spreading `any`.

---

## Q158. How would you migrate a JavaScript React project to TypeScript?

**Sample Answer:**

```text
1. Install TypeScript and required type packages
2. Configure tsconfig.json
3. Convert files gradually
4. Rename .js → .ts and .jsx → .tsx where appropriate
5. Type component props
6. Type state and events
7. Type API models
8. Remove unnecessary any
9. Enable stricter options gradually
10. Fix remaining type errors
```

---

# 26. Common Tricky Questions

## Q159. Does TypeScript prevent all runtime errors?

**Answer:**

No.

TypeScript catches many type-related problems before runtime, but it cannot prevent every runtime problem.

Example:

```typescript
const user = JSON.parse(input) as User;
```

The assertion does not validate the actual JSON.

Runtime validation may still be necessary.

---

## Q160. `any` vs `unknown` — which is safer?

`unknown` is safer because operations generally require narrowing first.

---

## Q161. Interface vs class

An interface describes a type contract.

A class defines an actual runtime constructor and behavior.

```typescript
interface User {
    name: string;
}
```

vs

```typescript
class User {
    constructor(public name: string) {}
}
```

The class exists at runtime; the interface is primarily a compile-time type construct.

---

## Q162. Interface vs type — which should you use?

There is no universal winner.

Use the one that best expresses the design.

Interface is convenient for object contracts and extension/declaration merging.

Type aliases are particularly useful for unions, intersections and complex type expressions.

---

## Q163. Is TypeScript object-oriented?

**Answer:**

TypeScript supports object-oriented programming features such as:

- Classes
- Interfaces
- Inheritance
- Encapsulation
- Abstract classes
- Access modifiers

But TypeScript also supports functional and other programming styles.

---

## Q164. What is structural typing?

**Answer:**

TypeScript primarily uses structural typing.

Two types are compatible when their structures are compatible, rather than requiring the same explicit nominal type identity.

Example:

```typescript
interface User {
    name: string;
}

const person = {
    name: "John"
};

const user: User = person;
```

This works because the structure matches.

---

## Q165. What is excess property checking?

When assigning an object literal directly to a target type, TypeScript performs additional checks for unexpected properties.

```typescript
interface User {
    name: string;
}

const user: User = {
    name: "John",
    age: 21
};
```

This can produce an error because `age` is not part of `User`.

---

## Q166. What is type widening?

TypeScript may widen a literal to a broader type depending on how a value is declared.

For example:

```typescript
let status = "success";
```

may be inferred as `string`, while:

```typescript
const status = "success";
```

can retain the literal type `"success"`.

`as const` can be used when you need literal and readonly inference.

---

## Q167. What is discriminated union?

A discriminated union uses a common literal property to distinguish among object variants.

```typescript
type Result =
    | { status: "success"; data: string }
    | { status: "error"; error: string };

function handle(result: Result) {
    if (result.status === "success") {
        console.log(result.data);
    } else {
        console.log(result.error);
    }
}
```

This is a powerful pattern for API and UI state modeling.

---

## Q168. What is exhaustive checking?

You can use `never` to ensure all variants of a union have been handled.

```typescript
function assertNever(value: never): never {
    throw new Error(`Unexpected value: ${value}`);
}
```

This helps detect missing cases when a union changes.

---

# 27. Rapid-Fire Questions

## Q169. What is TypeScript?

A statically type-checked superset of JavaScript.

## Q170. What file extension is used?

`.ts`

For JSX:

`.tsx`

## Q171. What is `tsc`?

TypeScript compiler.

## Q172. What is `any`?

A type that disables most static type checking for a value.

## Q173. What is `unknown`?

A type-safe representation of an unknown value that requires narrowing before most operations.

## Q174. What is `never`?

Represents values that never occur.

## Q175. What is `void`?

Commonly used for functions that do not return a useful value.

## Q176. What is interface?

A compile-time contract describing a type's structure.

## Q177. What is type alias?

A named type expression.

## Q178. What is union?

`A | B` means A or B.

## Q179. What is intersection?

`A & B` means the value must satisfy both types.

## Q180. What are generics?

A way to write reusable type-safe code parameterized by types.

## Q181. What is type inference?

Automatic determination of a value's type.

## Q182. What is type narrowing?

Reducing a broad type to a more specific type through checks.

## Q183. What is type assertion?

A compile-time instruction telling TypeScript how to treat a value.

## Q184. Does type assertion convert data?

No.

## Q185. What is `keyof`?

Gets the keys of a type as a union.

## Q186. What is `typeof` in a type position?

Gets the type of a value.

## Q187. What is `Partial`?

Makes all properties optional.

## Q188. What is `Pick`?

Selects specific properties.

## Q189. What is `Omit`?

Removes specific properties.

## Q190. What is `Record`?

Creates an object type from keys and a value type.

## Q191. What is `ReturnType`?

Extracts the return type of a function.

## Q192. What is `Parameters`?

Extracts function parameter types as a tuple.

## Q193. What is `.tsx`?

TypeScript file containing JSX.

## Q194. Does TypeScript run in browser directly?

Normally no; it is transformed into JavaScript.

## Q195. Does TypeScript guarantee runtime type safety?

No. External/untrusted data requires runtime validation when necessary.

---

# 28. Most Important Questions for Freshers

If the interviewer gives limited time, prepare these first.

1. What is TypeScript?
2. Why use TypeScript instead of JavaScript?
3. JavaScript vs TypeScript?
4. Does TypeScript run in the browser?
5. What is transpilation?
6. What is `tsc`?
7. What is type inference?
8. What is type annotation?
9. What is type assertion?
10. `any` vs `unknown`
11. `never` vs `void`
12. Interface vs type
13. Union vs intersection
14. Optional properties
15. Readonly properties
16. Arrays and tuples
17. Enums
18. Type narrowing
19. Type guards
20. Generics
21. Generic constraints
22. Function overloads
23. `keyof`
24. `typeof`
25. Utility types
26. `Partial`
27. `Pick`
28. `Omit`
29. `Record`
30. `ReturnType`
31. `strict`
32. `strictNullChecks`
33. `tsconfig.json`
34. TypeScript with React
35. Typing React props
36. Typing `useState`
37. Typing React events
38. Typing API responses
39. Runtime validation
40. Explain how TypeScript helped in your project

---

# 29. Final Revision Checklist

## JavaScript → TypeScript

- [ ] Type annotations
- [ ] Type inference
- [ ] Union types
- [ ] Intersection types
- [ ] Literal types
- [ ] `any`
- [ ] `unknown`
- [ ] `never`
- [ ] `void`
- [ ] Type assertions
- [ ] Type narrowing
- [ ] Type guards

## Object Modeling

- [ ] Interfaces
- [ ] Type aliases
- [ ] Optional properties
- [ ] Readonly properties
- [ ] Index signatures
- [ ] Structural typing
- [ ] Discriminated unions

## Functions

- [ ] Parameter types
- [ ] Return types
- [ ] Optional parameters
- [ ] Default parameters
- [ ] Rest parameters
- [ ] Callback types
- [ ] Function overloads
- [ ] Generic functions

## Generics

- [ ] Generic functions
- [ ] Generic interfaces
- [ ] Generic classes
- [ ] Generic constraints
- [ ] `keyof`
- [ ] Indexed access types
- [ ] `infer`

## Utility Types

- [ ] Partial
- [ ] Required
- [ ] Readonly
- [ ] Pick
- [ ] Omit
- [ ] Record
- [ ] Exclude
- [ ] Extract
- [ ] NonNullable
- [ ] ReturnType
- [ ] Parameters

## React

- [ ] Props
- [ ] State
- [ ] `useState`
- [ ] Event handlers
- [ ] Form events
- [ ] Children
- [ ] API response types
- [ ] `.tsx`
- [ ] Generic components
- [ ] Context types

## Node / Backend

- [ ] Express Request/Response types
- [ ] Request body types
- [ ] API response types
- [ ] Error typing
- [ ] Runtime validation

## Configuration

- [ ] `tsconfig.json`
- [ ] `strict`
- [ ] `strictNullChecks`
- [ ] `noImplicitAny`
- [ ] `target`
- [ ] `module`
- [ ] `outDir`
- [ ] `rootDir`
- [ ] `include`
- [ ] `exclude`

---

# Interview Answer Strategy

Because you already know JavaScript, do not answer TypeScript questions as if TypeScript were a completely different language.

Use this approach:

```text
JavaScript concept
      ↓
What TypeScript adds
      ↓
Small code example
      ↓
Why it helps
      ↓
How you used it in React/project
```

### Example

**Interviewer:** What is TypeScript?

**Good answer:**

> TypeScript is a superset of JavaScript developed by Microsoft. Since I already know JavaScript, I think of TypeScript as JavaScript plus a static type system and additional type features such as interfaces, generics and utility types. It helps catch many type-related errors during development and improves autocomplete and refactoring. The TypeScript code is ultimately transformed into JavaScript for execution.

---

# Important Things You Should Be Able to Explain Without Memorizing

## 1. `any` vs `unknown`

```typescript
let a: any = 10;
a.foo.bar; // TypeScript generally allows this

let b: unknown = 10;
// b.foo; // Error until narrowed
```

Remember:

```text
any     → maximum flexibility, minimum safety
unknown → maximum uncertainty, but type-safe handling
```

---

## 2. Interface vs Type

```typescript
interface User {
    name: string;
}
```

```typescript
type User = {
    name: string;
};
```

Both can model objects.

Use type aliases when you need things such as:

```typescript
type Status = "loading" | "success" | "error";
```

Use interfaces when an object contract and extension/declaration merging are useful.

---

## 3. Union vs Intersection

```typescript
type ID = string | number;
```

Means:

```text
string OR number
```

While:

```typescript
type Employee = Person & Job;
```

Means:

```text
Person AND Job
```

---

## 4. Type Assertion Does Not Convert Data

Wrong understanding:

```typescript
const number = "123" as number;
```

A type assertion does not perform runtime conversion.

Actual conversion:

```typescript
const number = Number("123");
```

---

## 5. TypeScript Does Not Validate API Data Automatically

This:

```typescript
const user: User = await response.json();
```

does not prove that the server actually returned a valid `User`.

For untrusted external data:

```text
API Response
    ↓
Runtime Validation
    ↓
Trusted Application Type
```

Libraries such as Zod can be used for runtime validation.

---

# Final 1-Day Revision Order

If your interview is tomorrow and you already know JavaScript, study in this order:

### Priority 1 — Must Know

```text
TypeScript basics
↓
Type inference
↓
Interfaces
↓
Type aliases
↓
Union / Intersection
↓
any / unknown / never / void
↓
Type narrowing
↓
Generics
```

### Priority 2 — Very Important

```text
Utility Types
↓
keyof
↓
typeof
↓
Function typing
↓
Async/Promise typing
↓
tsconfig.json
↓
strict mode
```

### Priority 3 — React Focus

```text
Props
↓
useState
↓
Events
↓
API responses
↓
Children
↓
Generic components
↓
.ts vs .tsx
```

### Priority 4 — Advanced

```text
Conditional Types
↓
Mapped Types
↓
infer
↓
Template Literal Types
↓
Declaration Merging
↓
Advanced Generic Constraints
```

---

# Final Interview Tip

Since you already know JavaScript and React, interviewers may not spend much time asking:

> "What is a variable?"

Instead, they are more likely to test whether you understand **why TypeScript is useful on top of JavaScript**.

Be especially ready for:

```text
JavaScript → TypeScript migration
JavaScript types → TypeScript types
any vs unknown
interface vs type
union vs intersection
type narrowing
generics
utility types
API response typing
React props/state/events
tsconfig
runtime validation
```

The strongest answer pattern is:

> **"I know how this works in JavaScript, and TypeScript adds compile-time type safety around it."**

That demonstrates that you understand TypeScript rather than simply memorizing syntax.
