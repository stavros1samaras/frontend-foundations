# TypeScript - Comprehensive Guide

# Introduction

TypeScript is an open-source programming language built on top of JavaScript that adds static type declarations. It allows developers to write safer and more maintainable code.



# Core Concepts

## 1. Data Types

## Primitive Types
```typescript
// String
const name: string = "John";

// Number
const age: number = 25;

// Boolean
const isActive: boolean = true;

// Null and Undefined
const nothing: null = null;
const undef: undefined = undefined;

// Any (avoid if possible)
const anything: any = "anything you want";
```

## Complex Types
```typescript
// Array
const numbers: number[] = [1, 2, 3];
const strings: Array<string> = ["a", "b", "c"];

// Tuple
const tuple: [string, number] = ["hello", 42];

// Union
const id: string | number = "123";

// Intersection
type Admin = { role: "admin" };
type User = { name: string };
type AdminUser = Admin & User;
```

## 2. Interfaces

```typescript
interface User {
  name: string;
  age: number;
  email?: string; // Optional field
  readonly id: number; // Read-only
}

const user: User = {
  name: "Maria",
  age: 30,
  id: 1
};

// Extending Interface
interface Admin extends User {
  permissions: string[];
}
```

## 3. Types

```typescript
type Point = {
  x: number;
  y: number;
};

type ID = string | number;

type Status = "pending" | "active" | "inactive";

const status: Status = "active";
```

## 4. Classes

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

## 5. Enums

```typescript
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE"
}

enum Direction {
  Up = 1,
  Down = 2,
  Left = 3,
  Right = 4
}

const favoriteColor: Color = Color.Blue;
```



# Functions

## Basic Declarations

```typescript
// With parameter and return types
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
function createUser(name: string, role: string = "user"): object {
  return { name, role };
}

// Rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}
```



## Generics

```typescript
// Generic function
function identity<T>(value: T): T {
  return value;
}

const result1: string = identity("hello");
const result2: number = identity(42);

// Generic class
class Box<T> {
  private contents: T;

  constructor(value: T) {
    this.contents = value;
  }

  getValue(): T {
    return this.contents;
  }
}

const stringBox = new Box<string>("hello");
const numberBox = new Box<number>(123);

// Generic constraints
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```






# Utility Types

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

const perms: Permissions = {
  read: true,
  write: true,
  delete: false
};
```








# Best Practices

1. **Avoid `any`**: Use `unknown` or generics instead
2. **Enable `strict` mode**: Activate in `tsconfig.json`
3. **Declare types explicitly**: Helps code comprehension
4. **Use interfaces**: For public APIs
5. **Use types**: For internal implementations


**Last Updated**: March 2026
