# install typescript
npm install -g typescript

# check version
tsc --version

# initialize typescript
tsc --iniit

# set working path in tsconfig.json
rootDir "./src",
outDir "./dist"


# compile the code
tsc 


# Difference between interface and type in TypeScript
_Exported on 6/19/2025 at 08:30:03 GMT+5 from Cursor (1.0.0)_

---

**User**

what is the difference interface vs type in typscript.

---

**Cursor**

Great question! In TypeScript, both interface and type can be used to describe the shape of an object or a structure, but there are some important differences and use cases for each.

### 1. Syntax and Use

**Interface:**
- Primarily used to describe the shape of objects and classes.
- Can be extended (using extends) and implemented by classes.
- Supports declaration merging (multiple declarations with the same name are merged).

```typescript
interface User {
  id: number;
  name: string;
}
```

**Type Alias:**
- Can describe objects, primitives, unions, intersections, and more.
- Cannot be re-opened to add new properties (no declaration merging).
- More flexible for complex types.

```typescript
type User = {
  id: number;
  name: string;
};
```

### 2. Extending and Implementing

**Interface:**
```typescript
interface Animal {
  name: string;
}
interface Dog extends Animal {
  breed: string;
}
```

**Type:**
```typescript
type Animal = {
  name: string;
};
type Dog = Animal & { breed: string };
```

### 3. Declaration Merging

**Interface:**
```typescript
interface User {
  id: number;
}
interface User {
  name: string;
}
// User now has both id and name
```

**Type:**
```typescript
type User = {
  id: number;
};
// Error if you try to declare another type User
```

### 4. Use Cases

- **Use interface** when you want to define the shape of objects, especially for classes and when you want to take advantage of declaration merging or extending.
- **Use type** when you need to define unions, intersections, or work with primitives and tuples.

### 5. Example from Your Code

You used both in your code:

```typescript
type User = {
  id: number
  name: string
}

interface UserInterface {
  readonly id: number
  name: string
  age?: number
}
```

Both are valid, but if you want to extend or merge, interface is better. If you want to create a union or intersection, type is better.

---

**Summary Table:**

| Feature                | interface | type      |
|------------------------|-----------|-----------|
| Object shape           | ✅        | ✅        |
| Class implementation   | ✅        | ❌        |
| Extending              | ✅        | ✅ (with &)|
| Declaration merging    | ✅        | ❌        |
| Unions/Intersections   | ❌        | ✅        |
| Primitives/tuples      | ❌        | ✅        |

**In modern TypeScript, both are powerful and often interchangeable for objects, but interfaces are preferred for public APIs and class contracts, while types are preferred for more complex type operations.**

```typescript
interface User {
  id: number;
  name: string;
}
```

```typescript
type User = {
  id: number;
  name: string;
};
```

```typescript
interface Animal {
  name: string;
}
interface Dog extends Animal {
  breed: string;
}
```

```typescript
type Animal = {
  name: string;
};
type Dog = Animal & { breed: string };
```

```typescript
interface User {
  id: number;
}
interface User {
  name: string;
}
// User now has both id and name
```

```typescript
type User = {
  id: number;
};
// Error if you try to declare another type User
```

```typescript
type User = {
  id: number
  name: string
}

interface UserInterface {
  readonly id: number
  name: string
  age?: number
}
```

---

**User**

can you give me examples base on summy table. 

---

**Cursor**

Absolutely! Here are examples for each row of the summary table, showing how to use interface and type in TypeScript for each feature:

---

### 1. Object Shape

**interface:**
```typescript
interface Car {
  make: string;
  model: string;
}
const myCar: Car = { make: "Toyota", model: "Corolla" };
```

**type:**
```typescript
type Car = {
  make: string;
  model: string;
};
const myCar: Car = { make: "Toyota", model: "Corolla" };
```

---

### 2. Class Implementation

**interface:**
```typescript
interface Animal {
  name: string;
  speak(): void;
}
class Dog implements Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  speak() {
    console.log("Woof!");
  }
}
```

**type:**  
> You cannot implement a type alias with a class directly (unless it’s a simple object type), so interface is preferred here.

---

### 3. Extending

**interface:**
```typescript
interface Shape {
  color: string;
}
interface Circle extends Shape {
  radius: number;
}
const circle: Circle = { color: "red", radius: 10 };
```

**type:**
```typescript
type Shape = { color: string };
type Circle = Shape & { radius: number };
const circle: Circle = { color: "red", radius: 10 };
```

---

### 4. Declaration Merging

**interface:**
```typescript
interface User {
  id: number;
}
interface User {
  name: string;
}
// User is now: { id: number; name: string }
const user: User = { id: 1, name: "Alice" };
```

**type:**  
> This will cause an error:
```typescript
type User = { id: number };
// type User = { name: string }; // Error: Duplicate identifier 'User'
```

---

### 5. Unions/Intersections

**type:**
```typescript
type Status = "success" | "error" | "loading";
let status: Status = "success";
```

**interface:**  
> Interfaces cannot be used for unions or intersections of primitive types.

---

### 6. Primitives/Tuples

**type:**
```typescript
type Point = [number, number];
const pt: Point = [10, 20];

type Name = string;
const myName: Name = "Arslan";
```

**interface:**  
> Interfaces cannot be used for primitives or tuples.

---

## Summary Table with Examples

| Feature                | interface Example | type Example |
|------------------------|------------------|-------------|
| Object shape           | `interface Car { make: string; }` | `type Car = { make: string; }` |
| Class implementation   | `class Dog implements Animal { ... }` | (Not recommended) |
| Extending              | `interface Circle extends Shape { ... }` | `type Circle = Shape & { ... }` |
| Declaration merging    | `interface User { id: number; } interface User { name: string; }` | (Not possible) |
| Unions/Intersections   | (Not possible) | `type Status = "success" | "error"` |
| Primitives/tuples      | (Not possible) | `type Point = [number, number]` |

Let me know if you want more details or more examples for any row!

```typescript
interface Car {
  make: string;
  model: string;
}
const myCar: Car = { make: "Toyota", model: "Corolla" };
```

```typescript
type Car = {
  make: string;
  model: string;
};
const myCar: Car = { make: "Toyota", model: "Corolla" };
```

```typescript
interface Animal {
  name: string;
  speak(): void;
}
class Dog implements Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  speak() {
    console.log("Woof!");
  }
}
```

```typescript
interface Shape {
  color: string;
}
interface Circle extends Shape {
  radius: number;
}
const circle: Circle = { color: "red", radius: 10 };
```

```typescript
type Shape = { color: string };
type Circle = Shape & { radius: number };
const circle: Circle = { color: "red", radius: 10 };
```

```typescript
interface User {
  id: number;
}
interface User {
  name: string;
}
// User is now: { id: number; name: string }
const user: User = { id: 1, name: "Alice" };
```

```typescript
type User = { id: number };
// type User = { name: string }; // Error: Duplicate identifier 'User'
```

```typescript
type Status = "success" | "error" | "loading";
let status: Status = "success";
```

```typescript
type Point = [number, number];
const pt: Point = [10, 20];

type Name = string;
const myName: Name = "Arslan";
```

