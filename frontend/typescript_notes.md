# 1. Get Started

## 1.1 What is TypeScript?

*TypeScript is a programming language to address **shortcommings** of **JavaScript**.*

**Benefits:**
- Static typing
- Code completion
- Refactoring
- Shorthand notations

**STATICALLY-TYPED (C++, C#, Java)**
```cpp
int number = 10;
number = 'a'; // Error!
```

**DYNAMICALLY-TYPED (JavaScript, Python, Ruby)**

```JavaScript
let number = 10;
number = 'a'; // OK
Math.round(number); // Might be crashed! 
```

***TypeScript == JavaScript with Type Checking***
- **Type checking**
- **Code completion**
- **Refactoring**
- **New features**

**Drawbacks**:**
- Compliation (.ts -> compiler -> .js, tanspliation)
- Dicipline in coding

## 1.2 Setting Up the Development Environment

```sh
npm i -g typescript
```

```sh
tsc -v
```
```
Version 4.7.3
```

## 1.3 Configuring the TypeScript Compiler

```sh
 tsc --init
`=> 
Created a new tsconfig.json with:
                                                                             TS
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true


You can learn more at https://aka.ms/tsconfig
```

```json
    /* Modules */
    "module": "commonjs" /* Specify what module code is generated. */,
    "rootDir": "./src" /* Specify the root folder within your source files. */,
```

```json
    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
    "outDir": "./dist",  
    "removeComments": true 
    //
    //
    "noEmitOnError": true 
```

## 1.4 Debugging TypeScript Applications

```json
    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    "sourceMap": true,  
```

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "pwa-node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/src/index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json", // Add this line
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
}
```

# 2 Fundamentals

## 2.1 Introduction

- **The any Type**
- **Arrays**
- **Tuples**
- **Enums**
- **Functions**
- **Objects**

## 2.2 Built-in Types

**JavaScript**
- number
- string
- boolean
- null
- undefined
- object

**TypeScript**
- any
- unknown
- never
- enum
- tuple

```JavaScript
let sales: number = 123_456_789;
let course: string = "TypeScript";
let is_published: boolean= true;
let level; // any
```
*Actually we don't need to explicitly declare the type'*
```JavaScript
let sales = 123_456_789;
let course = "TypeScript";
let is_published = true;
```

## 2.3 The any Type

***To avoid using any type as possible!***

```JavaScript
function render(document: any) {
  console.log(document);
}
```

## 2.4 Strict Compiler Option

## 2.5 Arrays

```JavaScript
let numbers: number[] = [];
```

## 2.6 Tuples

```JavaScript
let user: [number, string] = [1, "Lawjune"];
```

## 2.7 Enums

```JavaScript
// const small = 1;
// const medium = 2;
// const large = 3;

// PascalCase
const enum Size {
  Small = 1,
  Medium,
  Large,
}

let mySize: Size = Size.Medium;
console.log(mySize);
```
*When you add the `const`, the tsc will optimize the codes.*

## 2.8 Functions

*Always annotate your functions.*

```json
    /* Type Checking */
    "strict": true /* Enable all strict type-checking options. */,
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    "noUnusedParameters": true,  
	// "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    "noImplicitReturns": true /*
```

```JavaScript
function calculate_tax(income: number, tax_year?: number): number {
  if ((tax_year || 2022) < 2022) return income * 2;
  return income * 3;
}
```

**Better Approach**
```JavaScript
function calculate_tax(income: number, tax_year = 2022): number {
  if (tax_year < 2022) return income * 2;
  return income * 3;
}
```

## 2.9 Objects

```JavaScript
let employee: {
  readonly id: number;
  name: string;
  retired: (date: Date) => void;
} = {
  id: 1,
  name: "Lawjune",
  retired: (date: Date) => {
    console.log(date);
  },
};
```

# 3 Advanced Types

## 3.1 Introduction

- **Type alias**
- **Unions and intersections**
- **Type narrowing**
- **Nullable types**
- **The unknown type**
- **The never type**

## 3.2 Type Aliases

```JavaScript
type Employee = {
  readonly id: number;
  name: string;
  retired: (date: Date) => void;
};

let employee: Employee = {
  id: 1,
  name: "Lawjune",
  retired: (date: Date) => {
    console.log(date);
  },
};
```

## 3.3 Union Types

```JavaScript
type Employee = {
  readonly id: number;
  name: string;
  retired: (date: Date) => void;
};

let employee: Employee = {
  id: 1,
  name: "Lawjune",
  retired: (date: Date) => {
    console.log(date);
  },
};
```

## 3.4 Intersection Types

```JavaScript
type Draggable = {
  drag: () => void;
};

type Resizable = {
  resize: () => void;
};

type UIWidget = Draggable & Resizable;

let textBox: UIWidget = {
  drag: () => {},
  resize: () => {},
};
```

## 3.5 Literal Types

```JavaScript
type Quantity = 40 | 70;
let quantity: Quantity = 70;

type Metric = "cm" | "inch";
```

## 3.6 Nullable Types

```JavaScript
function greet(name: string | null | undefined) {
  if (name) console.log(name.toUpperCase());
  else console.log("Hola!");
}

greet(null);
```

## 3.7 Optional Chaining

```JavaScript
type Customer = {
  birthday?: Date;
};

function get_customer(id: number): Customer | null | undefined {
  return id === 0 ? null : { birthday: new Date() };
}

let customer = get_customer(1);
// Optional property access operator
console.log(customer?.birthday?.getFullYear());

// Optional property access operator
// customer?.[0];

// Optional call
let log: any = null;
log?.("a");
```

## 3.8 The Nullish Coaelscing Operator

```JavaScript
let speed: number | null = null;
let ride = {
  // Falsy (undefined, null, '', false 0)
  // Nullish coalescing operator
  speed: speed ?? 30,
};
```

## 3.9 Type Assertions

```JavaScript
let phone = <HTMLInputElement>document.getElementById("phone");
```

## 3.10 The unknown Type

```JavaScript
function render(document: unknown) {
  // Narrowing
  if (typeof document === "string") {
    document.toUpperCase();
  }
}
```

## 3.11 The never Type

```json
    "allowUnreachableCode": false 
```

```javascript
function process_event(): never {
  while (true) {
    // Read a message from a queue
  }
}

process_event();
console.log("Hello World"); // Complaint error
```

# 4 Object-oriented Programming

## 4.1 Introduction

- **Introduction to OOP** 
- **Classes**
- **Constructors**
- **Properties and methods**
- **Access control keywords**
- **Getters and setters**
- **Static members**
- **Index signatures**
- **Inheritance**
- **Polymorphism**
- **Abstract classes**
- **Interfaces**

## 4.2 What is Object-oriented Programming

## 4.3 Creating Classes

*A **class** is a **blueprint** for creating objects.*

```JavaScript
class Account {
  id: number;
  owner: string;
  balance: number;

  constructor(id: number, owner: string, balance: number) {
    this.id = id;
    this.owner = owner;
    this.balance = balance;
  }

  deposit(amount: number): void {
    if (amount <= 0) throw new Error("Invalid amount");
    this.balance += amount;
  }
}
```

## 4.4 Creating Objects

```JavaScript
class Account {
  id: number;
  owner: string;
  balance: number;

  constructor(id: number, owner: string, balance: number) {
    this.id = id;
    this.owner = owner;
    this.balance = balance;
  }

  deposit(amount: number): void {
    if (amount <= 0) throw new Error("Invalid amount");
    this.balance += amount;
  }
}

let account = new Account(1, "Lawjune", 0);
account.deposit(100);
console.log(account instanceof Account);

// Union
// if (typeof some_obj == 'number') {}
```

## 4.5 Read-only and Optional Properties

```JavaScript
class Account {
  readonly id: number;
  owner: string;
  balance: number;
  nickname?: string;
.....
```

## 4.6 Access Control Keywords

public, private, protected


## 4.7 Parameter Properties

```JavaScript
class Account {
  //   readonly id: number;
  //   owner: string;
  //   private _balance: number;
  nickname?: string;

  constructor(
    public readonly id: number,
    public owner: string,
    private _balance: number
  ) {
    // this.id = id;
    // this.owner = owner;
    // this._balance = balance;
  }
```

## 4.8 Getters and Setters

```JavaScript
class Account {
  nickname?: string;

  constructor(
    public readonly id: number,
    public owner: string,
    private _balance: number
  ) {}

  deposit(amount: number): void {
    if (amount <= 0) throw new Error("Invalid amount");
    this._balance += amount;
  }

  get balance(): number {
    return this._balance;
  }
  set balance(value: number) {
    if (value < 0) throw new Error("Invalid value");
    this._balance = value;
  }
}

let account = new Account(1, "Lawjune", 0);
account.deposit(100);
console.log(account.balance);

```

## 4.9 Index Signatures

```JavaScript
class SeatAssignment {
  // Index signature property
  [seatNumber: string]: string;
}

let seats = new SeatAssignment();
seats.A1 = "Jun Luo";
seats["A2"] = "Cheryl Tan";
```

## 4.10 Static Members

```JavaScript
class Ride {
  private static _activeRides: number = 0;

  start() {
    Ride._activeRides++;
  }
  stop() {
    Ride._activeRides--;
  }

  static get activeRides(): number {
    return Ride._activeRides;
  }
}

let ride1 = new Ride();
ride1.start();

let ride2 = new Ride();
ride2.start();

console.log(Ride.activeRides);
```
```output
2
```

## 4.11 Inheritance

```JavaScript
class Person {
  constructor(public firstName: string, public lastName: string) {}

  get fullName(): string {
    return this.firstName + " " + this.lastName;
  }

  walk() {
    console.log("Walking...");
  }
}

class Student extends Person {
  constructor(public studenId: number, firstName: string, lastName: string) {
    super(firstName, lastName);
  }

  takeTest() {
    console.log("Taking a test...");
  }
}

let student = new Student(1, "Jun", "Luo");
console.log(student.fullName);
student.takeTest();
```
```output
Jun Luo
Taking a test...
```

## 4.12 Method Overriding

```JavaScript
......
class Teacher extends Person {
  override get fullName(): string {
    return "Professor " + super.fullName;
  }
}

let teacher = new Teacher("Jun", "Luo");
console.log(teacher.fullName);
```
```output
Professor Jun Luo
```

## 4.13 Polymorphism

[Poly] means *Many*
[morph] means *Form*
***Polymorphism means many different forms.**

```JavaScript
......
class Princial extends Person {
  override get fullName(): string {
    return "Princial " + super.fullName;
  }
}

printNames([
  new Student(1, "Jun", "Luo"),
  new Teacher("Cheryl", "Tan"),
  new Princial("Bing", "Xu"),
]);

function printNames(people: Person[]) {
  for (let person of people) console.log(person.fullName);
}
```

**Open Closed Principle**
*Classes should be open for extension and closed for modification.*


## 4.14 Private vs Protected Members

*Protected members are inheritant, but not recommemd to use it.*

## 4.15 Abstract Classes and Methods

```JavaScript
abstract class Shape {
  constructor(public color: string) {}

  abstract render(): void;
}

class Circle extends Shape {
  constructor(public radius: number, color: string) {
    super(color);
  }

  override render(): void {
    console.log("Rendering a circle.");
  }
}

// let shape = new Shape(); // Error
```

## 4.16 Interfaces

***Classes** -> Blueprints for creating objects*
***Interfaces** -> To define the shape of objects*

```JavaScript
interface Calendar {
  name: string;
  addEvent(): void;
  removeEvent(): void;
}

interface CloudCalendar extends Calendar {
  sync(): void;
}

class GoogleCalendar implements Calendar {
  constructor(public name: string) {}

  addEvent(): void {
    throw new Error("Method not implemented.");
  }
  removeEvent(): void {
    throw new Error("Method not implemented.");
  }
}
```

# 5 Generics

## 5.1 Introduction

- **Generic classes**
- **Generic functions**
- **Generic interfaces**
- **Generic constraints**
- **Type mapping**

## 5.2 Understanding the Problem

## 5.3 Generic Classes

```JavaScript
class KeyValuePair<K, V> {
  constructor(public key: K, public value: V) {}
}

// let pair = new KeyValuePair<string, string>("1", "a");
let pair = new KeyValuePair("1", "a");
```

## 5.4 Generic Functions

```JavaScript
class ArrayUtils {
  static wrapInArray<T>(value: T) {
    return [value];
  }
}

let number = ArrayUtils.wrapInArray(1);
```

## 5.5 Generic Interfaces

```JavaScript
// http://mywesite.com/users
// http://mywesite.com/products

interface Result<T> {
  data: T | null;
  error: string | null;
}

function fetch<T>(url: string): Result<T> {
  // console.log(`Fetching url: ${url}`);
  return { data: null, error: null };
}

interface User {
  username: string;
}

interface Product {
  title: string;
}

let user_reuslt = fetch<User>("/users");
console.log(user_reuslt.data?.username);

let product_result = fetch<Product>("/products");
console.log(product_result.data?.title);
```

## 5.6 Generic Constraints

```JavaScript
function echo<T>(value: T): T {
  return value;
}

echo("1");
```

```JavaScript
function echo<T extends number | string>(value: T): T {
  return value;
}

// echo(true); // error
```

```JavaScript
function echo<T extends { name: string }>(value: T): T {
  return value;
}

echo({ name: "a" });
```

```JavaScript
interface Person {
  name: string;
}

function echo<T extends Person>(value: T): T {
  return value;
}

echo({ name: "a" });
```

```JavaScript
class Person {
  constructor(public name: string) {}
}

function echo<T extends Person>(value: T): T {
  return value;
}

echo({ name: "a" });
```

```JavaScript
class Person {
  constructor(public name: string) {}
}

class Customer extends Person {}

function echo<T extends Person>(value: T): T {
  return value;
}

echo(new Customer("a"));
```

## 5.7 Extending Generic Classes

```JavaScript
interface Product {
  name: string;
  price: number;
}

class Store<T> {
  private _objects: T[] = [];

  add(obj: T): void {
    this._objects.push(obj);
  }

  get objects(): T[] {
    return this._objects;
  }
}

let store = new Store<Product>();

class ProductObject implements Product {
  constructor(public name: string, public price: number) {}
}

store.add(new ProductObject("a", 10));
store.add(new ProductObject("b", 20));

// Pass on the generic type parameter
class CompressibleStore<T> extends Store<T> {
  compress() {}
}
let compress_store = new CompressibleStore<Product>();
compress_store.compress();

// Restrict the generic type parameter
class SearchableStore<T extends { name: string }> extends Store<T> {
  find(name: string): T | undefined {
    return this.objects.find((o) => o.name === name);
  }
}

// Fixed the generic type parameter
class ProductStore extends Store<Product> {
  filterByCategory(category: string): Product[] {
    return [];
  }
}
````

## 5.8 The keyof Operator

```JavaScript
interface Product {
  name: string;
  price: number;
}

class Store<T> {
  private _objects: T[] = [];

  add(obj: T): void {
    this._objects.push(obj);
  }

  // T is product
  // keyof T => 'name' | 'price'
  find(property: keyof T, value: unknown): T | undefined {
    return this._objects.find((obj) => obj[property] === value);
  }

  get objects(): T[] {
    return this._objects;
  }
}

let store = new Store<Product>();
store.add({ name: "a", price: 14 });
console.log(store.find("name", "a"));
console.log(store.find("price", 14));
```
```js
{ name: 'a', price: 14 }
{ name: 'a', price: 14 }
```

## 5.9 Type Mapping

```JavaScript
interface Product {
  name: string;
  price: number;
}

type ReadOnlyProduct = {
  readonly [K in keyof Product]: Product[K];
};

let product: ReadOnlyProduct = {
  name: "a",
  price: 1,
};

product.name = 14; // error
```

*Generic way*
```JavaScript
interface Product {
  name: string;
  price: number;
}

type Optional<T> = {
  [K in keyof T]?: T[K];
};

type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};

type ReadOnly<T> = {
  readonly [K in keyof T]: T[K];
};

let product: ReadOnly<Product> = {
  name: "a",
  price: 1,
};

product.name = 14; // error
```

*Google "TypeScript utility types"*


# 6 Decorators

## 6.1 Introduction

- **What are decorators**
- **Class decorators**
- **Method decorators**
- **Property decorators**
- **Accessor decorators**
- **Parameter decorators**

## 6.2 What Are Decorators

```json
    /* Language and Environment */
    "target": "es2016" /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */,
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    "experimentalDecorators": true,  
```

## 6.3 Class Decorators

```JavaScript
function Component(constructor: Function) {
  console.log("Component decorator called.");
  constructor.prototype.uniqueId = Date.now();
  constructor.prototype.insertInDom = () => {
    console.log("Inserting the com in the DOM");
  };
}

@Component
class ProfileComponent {}
```
```output
Component decorator called.
```
*Even though we didn't call the funciton of the component, this decorator is called once.'

## 6.4 Parameterized Decorators

```JavaScript
// Decorator factory
function Component(value: number) {
  return (constructor: Function) => {
    console.log("Component decorator called.");
    constructor.prototype.options = value;
    constructor.prototype.uniqueId = Date.now();
    constructor.prototype.insertInDom = () => {
      console.log("Inserting the com in the DOM");
    };
  };
}

@Component(14)
class ProfileComponent {}
```

```JavaScript
type ComponentOptions = {
  selector: string;
};

// Decorator factory
function Component(options: ComponentOptions) {
  return (constructor: Function) => {
    console.log("Component decorator called.");
    constructor.prototype.options = options;
    constructor.prototype.uniqueId = Date.now();
    constructor.prototype.insertInDom = () => {
      console.log("Inserting the com in the DOM");
    };
  };
}

@Component({ selector: "#my-profile" })
class ProfileComponent {}
```

## 6.5 Decorator Composition

```JavaScript
function Pipe(constructor: Function) {
  console.log("Pipe decorator called");
  constructor.prototype.pipe = true;
}

type ComponentOptions = {
  selector: string;
};

// Decorator factory
function Component(options: ComponentOptions) {
  return (constructor: Function) => {
    console.log("Component decorator called.");
    constructor.prototype.options = options;
    constructor.prototype.uniqueId = Date.now();
    constructor.prototype.insertInDom = () => {
      console.log("Inserting the com in the DOM");
    };
  };
}

@Component({ selector: "#my-profile" })
@Pipe
// f(g(x)) 
class ProfileComponent {}
```
```output
Pipe decorator called
Component decorator called.
```

## 6.6 Method Decorators

```JavaScript
function Log(target: any, methodName: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value as Function;
  descriptor.value = function (message: string) {
    console.log("Before");
    original.call(this, message);
    console.log("After");
  };

  console.log("target: " + JSON.stringify(target));
  console.log("methodName: " + methodName);
}

class Person {
  @Log
  say(message: string) {
    console.log("Person says " + message);
  }
}

let person = new Person();
person.say("Hello");
```
```output
target: {}
methodName: say
Before
Person says Hello
After
```

```JavaScript
function Log(target: any, methodName: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value as Function;
  // Can not use arrow function
  descriptor.value = function (...args: any) {
    console.log("Before");
    original.call(this, ...args);
    console.log("After");
  };

  console.log("target: " + JSON.stringify(target));
  console.log("methodName: " + methodName);
}

class Person {
  @Log
  say(message: string) {
    console.log("Person says " + message);
  }
}

let person = new Person();
person.say("Hello");
```
```output
target: {}
methodName: say
Before
Person says Hello
After
```

## 6.6 Accessor Decorators - Title

























































































































