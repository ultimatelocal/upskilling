# Typescript

TypeScript, a superset of JavaScript that brings static typing to the world of web development.

## Why Typescript?

### JavaScript's Dynamism:

- JavaScript is a dynamically typed language.
- Variables can change types during runtime.

```
let dynamicVar = "10"; // dynamicVar is initially a string
console.log(typeof dynamicVar); // Output: string

dynamicVar = dynamicVar * 2; // Multiplying a string by a number
console.log(typeof dynamicVar); // Output: number
```

### TypeScript's Solution:

- TypeScript adds static typing to JavaScript.
- Detects errors during development rather than runtime.
  - Static type checking

```
let dynamicVar: string = "10"; // dynamicVar is explicitly a string
console.log(typeof dynamicVar); // Output: string

dynamicVar = dynamicVar * 2; // TypeScript error: Operator '*' cannot be applied to types 'string' and 'number'.

```

## Installation and Configuration

1. Install typescript as dev dependency: `npm install --save-dev typescript`

2. create a `tsconfig.json` file in the project root. This file specifies the compiler options for TypeScript. Here's a basic example:

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true
  }
}
```

- `target` : Specifies the ECMAScript target version. In this case, it's set to ES5.
- `module` : Specifies the module system. CommonJS is a popular choice for Node.js projects.
- `strict` : Enables strict type-checking options.
- `esModuleInterop`: Allows compatibility with CommonJS modules.

## Basic Concepts:

### 1. Type Inference:

TS feature that allows the TypeScript compiler to automatically deduce the type of a variable or expression. This means that you do not have to explicitly specify the type of every variable and expression in your code.

```
const x = 10;
const y = x + 2;

console.log(y); // 12
```

### 2. Type Annotation:

Type annotations are a crucial concept in TypeScript. They allow developers to specify the data types of variables, function parameters, and return types. This can help catch errors during development and improve code readability.

```
const x: number = 10;
const y: number = x + 2;
```

### 3. Interfaces:

Interfaces are used to define the structure of an object. They specify the names and types of the object’s properties and can be used to enforce consistency across multiple objects.

```
interface Person {
    name: string;
    age: number;
}
```

### 4. Type Aliases

Type aliases are sometimes similar to interfaces, but can name primitives, unions, tuples, and any other types that you'd otherwise have to write by hand. Aliasing doesn't actually create a new type - it creates a new name to refer to that type.

```
type Point = {
  x: number;
  y: number;
};

// Exactly the same as the earlier example
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}

printCoord({ x: 100, y: 100 });
```

### 5. Classes:

Classes are a core concept in object-oriented programming, and TypeScript has full support for them. Classes allow developers to define blueprints for objects that share the same properties and methods. They can also include constructors, access modifiers, and inheritance.

```
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
}
```

### 6. Generics

Generics are a powerful feature in TypeScript that allow for the creation of reusable code. They allow developers to create functions and classes that can work with a variety of data types.

```
function identity<T>(arg: T): T {
    return arg;
}
```

### 7. Enums

Enums are a way to define a set of named values. They can improve code readability and help catch errors.

```
enum Color {
    Red = 1,
    Green = 2,
    Blue = 4
}
```

### 8. Union Type

Union types allow you to specify that a variable or expression can have one of a few different types. For example, the following code defines a variable x that can be either a string or a number:

```
const x: string | number;
```

### 9. Intersection type

Intersection types allow you to specify that a variable or expression must have all of the types in a set.

```
type HasName = { name: string };
type HasAge = { age: number };

// Create an intersection type combining both features
type Person = HasName & HasAge;

// Create an object that satisfies the intersection type
const person: Person = {
  name: 'Alice',
  age: 30,
};

console.log(person); // { name: 'Alice', age: 30 }
```

### 10. Type Guards

Type guards are a feature in TypeScript that allow developers to check the type of a variable at runtime. This can be useful when working with union types or other situations where the type of a variable may not be known.

```
if (typeof age === "number") {
    console.log(age * 2);
}
```

### 11. Modules

Modules are a way to organize code into smaller, reusable components. They allow developers to define private and public parts of a codebase and to import and export components between files.

```
// my-class.ts
export class MyClass {}
```

This exports the MyClass class from a module, while:

```
// main.ts
import { MyClass } from "./MyClass";
```

This imports the MyClass class into another module.

## Utility Types:

### 1. Partial\<Type>

The Partial<Type> utility type allows you to make all properties of a type optional. This can be particularly useful when dealing with complex objects where not all properties are required.

```
interface User {
  id: number;
  name: string;
  email: string;
}

const partialUser: Partial<User> = {
  name: "John",
};
```

### 2. Required\<Type>

Conversely, the Required \<Type> utility type ensures that all properties of a type are required.

```
interface Config {
  apiKey: string;
  apiUrl: string;
}

const config: Readonly<Config> = {
  apiKey: "secretKey",
  apiUrl: "https://api.example.com",
};

// Attempting to modify a readonly property will result in a TypeScript error
// config.apiKey = "newKey"; // Error: Cannot assign to 'apiKey' because it is a read-only property.
```

### 3. Pick\<Type, Keys>

The Pick<Type, Keys> utility type selects a subset of properties from the original type based on the specified keys.

```
interface Book {
  title: string;
  author: string;
  pages: number;
  publicationYear: number;
}

const bookSummary: Pick<Book, "title" | "author"> = {
  title: "The Great Gatsby",
  author: "F. Scott Fitzgerald",
};
```

### 3. Omit\<Type, Keys>

The Omit\<Type, Keys> utility type creates a type that excludes the specified keys from the original type.

```
interface Video {
  title: string;
  duration: number;
  resolution: string;
}

const videoPreview: Omit<Video, "resolution"> = {
  title: "Introduction to TypeScript",
  duration: 120,
};
```

### [Click here for more about Utility Types.](https://www.typescriptlang.org/docs/handbook/utility-types.html)

## Typescript Gotchas

1. **"any" Type Overuse** :
   Overusing the any type undermines the benefits of static typing. Try to minimize its usage, and instead, use more specific types or leverage TypeScript's union types.

2. **Understanding "null" and "undefined":** TypeScript has strictNullChecks to prevent null or undefined from being assigned to variables by default. Be aware of how these values are handled, and use strict null checks to catch potential issues early.

3. **Type Assertion Pitfalls (as):** Type assertions (as syntax) should be used with caution, as they essentially tell the compiler to trust the developer's judgment. Improper use may lead to runtime errors.
4. **Implicit "any" with JSX:** JSX can introduce implicit any types if the props are not properly defined. Ensure that JSX props are well-typed to catch issues during development.

## Links and Resources:

- Basic and fundamentals of typescript:

  - https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html#types-by-inference
  - https://www.typescriptlang.org/docs/handbook/2/basic-types.html
  - https://www.typescriptlang.org/docs/handbook/2/generics.html
  - https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases

- Installation and Configuration:
  https://www.typescriptlang.org/download#:~:text=TypeScript%20can%20be%20installed%20through,package%20or%20Visual%20Studio%20extension.

- Extra: [Typescript Best Practices](https://docs.aws.amazon.com/prescriptive-guidance/latest/)
