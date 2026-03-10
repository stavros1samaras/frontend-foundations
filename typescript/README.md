# TypeScript - Comprehensive Guide

## Data Types

#### Primitive Types

```typescript
const name: string = "John";
const age: number = 25;
const isActive: boolean = true;
const nothing: null = null;
const undef: undefined = undefined;
const anything: any = "anything you want";
```

#### Arrays

```typescript
// Two syntax styles
const numbers: number[] = [1, 2, 3];
const strings: Array<string> = ["a", "b", "c"];

// Mixed types
let mixedArray: (number | string | boolean)[] = [1, "apple", true];
let mixedArray2: Array<number | string> = [1, "test"];

// Array of objects
let vegetables: Array<{ name: string; price?: number }> = [
  { name: "Tomato", price: 2 },
  { name: "Carrot" },
];

// ReadonlyArray
let readonlyVegetables: ReadonlyArray<{ name: string }> = [{ name: "Tomato" }];
```

#### Tuples

```typescript
// Basic tuple
let userTuple: [string, number] = ["Alice", 25];

// Optional element
let personTuple: [string, number, boolean?] = ["Bob", 30];

// Readonly tuple
const coordinates: readonly [number, number] = [10, 20];
```

#### Union & Intersection Types

```typescript
// Union
const id: string | number = "123";
function processInput(input: string | number | null): string {
  if (typeof input === "string") return input.toUpperCase();
  if (typeof input === "number") return input.toFixed(2);
  return "No input";
}

// Discriminated Unions
type Success = { status: "success"; data: string };
type Error = { status: "error"; code: number };
type Response = Success | Error;

function handleResponse(response: Response): string {
  if (response.status === "success") {
    return response.data;
  } else {
    return `Error code: ${response.code}`;
  }
}
```

#### Literal Types

```typescript
type Direction = "up" | "down" | "left" | "right";
const move: Direction = "up"; // OK

type HttpStatus = 200 | 404 | 500;
const status: HttpStatus = 200; // OK

// Const assertions
const colorsTuple = ["red", "green", "blue"] as const;
type Color = (typeof colorsTuple)[number]; // "red" | "green" | "blue"
```



## Objects and Structures

#### Objects

```typescript
// Basic object type
let car: { model: string; year: number } = { model: "Tesla", year: 2025 };

// Optional properties
let product: { name: string; price?: number } = { name: "Apple" };

// Readonly properties
let vehicle: { readonly id: number; model: string } = { id: 1, model: "BMW" };

// Readonly array of objects
let products: readonly { name: string }[] = [{ name: "Tomato" }];
```

#### Interfaces

```typescript
interface User {
  name: string;
  age: number;
  email?: string; // Optional field
  readonly id: number; // Read-only
}

const user: User = { name: "Maria", age: 30, id: 1 };

// Index signatures
interface StringDict {
  [key: string]: string;
}

const dict: StringDict = { hello: "world", foo: "bar" };
```

#### Interface Inheritance

```typescript
interface Address {
  city: string;
  country: string;
}

interface ExtendedUser extends Address {
  name: string;
  age: number;
}

const userExtended: ExtendedUser = {
  name: "Alice",
  age: 30,
  city: "New York",
  country: "USA",
};
```



### 3. Enums

```typescript
// Numeric enum (starts from 0)
enum Status {
  Pending, // 0
  InProgress, // 1
  Completed, // 2
}
console.log(Status.Pending); // 0

// String enum
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
console.log(Direction.Up); // "UP"

// Mixed enum
enum Mixed {
  No = 0,
  Yes = "YES",
}
const answer: Mixed = Mixed.Yes;
```

### Generics
```ts
type Box<T> = {
  value: T;
};

const a: Box<number> = { value: 10 };
const b: Box<string> = { value: "hello" };
```


## Functions

### Basic Function Types

```typescript
// Standard function
function add(a: number, b: number): number {
  return a + b;
}

// Arrow function
const multiply = (a: number, b: number): number => a * b;

// Optional parameters
function greet(name: string, greeting?: string): string {
  return greeting ? `${greeting}, ${name}` : `Hello, ${name}`;
}

// Default values
function calculateScore(baseScore: number, deductions: number = 0): number {
  return baseScore - deductions;
}

// Rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}

// Object parameter
function createStudent(student: { id: number; name: string }): void {
  console.log(`Welcome, ${student.name}!`);
}

// Void return type
function logMessage(msg: string): void {
  console.log(msg);
}
```

## Classes

```typescript
class Animal {
  name: string;
  protected age: number; // Accessible in derived classes
  private secret: string; // Only in this class

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
    this.secret = "a secret";
  }

  speak(): string {
    return `${this.name} makes sounds`;
  }
}

class Dog extends Animal {
  breed: string;

  constructor(name: string, age: number, breed: string) {
    super(name, age);
    this.breed = breed;
  }

  speak(): string {
    return `${this.name} barks`;
  }
}

const dog = new Dog("Alex", 5, "Golden Retriever");
```

## Advanced Types

### Utility Types

```typescript
// Partial - all fields optional
type PartialUser = Partial<User>;

// Required - all fields required
type RequiredUser = Required<User>;

// Readonly - all fields read-only
type ReadonlyUser = Readonly<User>;

// Pick - select specific fields
type UserPreview = Pick<User, "name" | "age">;

// Omit - exclude fields
type UserWithoutEmail = Omit<User, "email">;

// Record - create object with specific keys
type Permissions = Record<"read" | "write" | "delete", boolean>;
const perms: Permissions = { read: true, write: true, delete: false };
```
