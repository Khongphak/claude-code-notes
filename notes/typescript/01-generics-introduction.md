# TypeScript Generics: Introduction

> Generics let you write reusable, type-safe code that works across multiple types without sacrificing type information.

## What Are Generics?

Without generics, you must either duplicate code for each type or lose type safety by using `any`.
Generics solve this by letting you pass a **type as a parameter** — just like you pass values as function arguments.

```typescript
// Without generics — loses type info
function identity(arg: any): any {
  return arg;
}

// With generics — type is preserved
function identity<T>(arg: T): T {
  return arg;
}

const result = identity<string>("hello"); // result: string
const num = identity(42);                 // result: number (inferred)
```

## Basic Syntax

### Generic Function

```typescript
function firstItem<T>(arr: T[]): T | undefined {
  return arr[0];
}

const first = firstItem([1, 2, 3]); // type: number | undefined
```

### Generic Interface

```typescript
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

const response: ApiResponse<User[]> = {
  data: [...],
  status: 200,
  message: "OK",
};
```

### Generic Class

```typescript
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }
}

const stack = new Stack<number>();
stack.push(1);
stack.push(2);
```

## Common Constraints

Use `extends` to restrict what types `T` can be.

```typescript
// T must have a .length property
function logLength<T extends { length: number }>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength("hello");   // OK — string has .length
logLength([1, 2, 3]); // OK — array has .length
logLength(42);        // Error — number has no .length
```

### keyof Constraint

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Alice", age: 30 };
getProperty(user, "name"); // OK — type: string
getProperty(user, "age");  // OK — type: number
getProperty(user, "role"); // Error — "role" not in user
```

## Built-in Generic Types

| Type | Description | Example |
|---|---|---|
| `Array<T>` | Typed array | `Array<string>` |
| `Promise<T>` | Async result | `Promise<User>` |
| `Partial<T>` | All fields optional | `Partial<Config>` |
| `Required<T>` | All fields required | `Required<Config>` |
| `Readonly<T>` | Immutable object | `Readonly<User>` |
| `Record<K, V>` | Typed dictionary | `Record<string, number>` |
| `Pick<T, K>` | Select fields | `Pick<User, "id" \| "name">` |
| `Omit<T, K>` | Exclude fields | `Omit<User, "password">` |

## When to Use Generics

**Good use cases:**
- Utility functions that operate on arrays, objects, or collections
- Data-fetching wrappers where the response shape varies
- Reusable UI components with typed props
- State management containers (e.g., `Store<T>`)

**Avoid generics when:**
- The function only ever works with one specific type — just use that type
- You find yourself writing `<T extends any>` — that's a sign `any` was the right choice
- The type parameter is not used in both the input and output — it adds no value

## Next

- `02-advanced-generics.md` — Conditional types, infer, mapped types
- `03-utility-types-deep-dive.md` — Building custom utility types
