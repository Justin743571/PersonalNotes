# TypeScript

TypeScript（缩写为TS）是一种由微软开发的开源编程语言，它是JavaScript的一个超集。换句话说，TypeScript包含了JavaScript的所有功能，并且在**此基础上提供了额外的静态类型和面向对象的特性**。TypeScript代码最终会被编译成纯JavaScript代码，因此可以运行在任何支持JavaScript的环境中。

以下是一些 TypeScript 的主要特性和优势：

1. **静态类型系统：** TypeScript引入了静态类型检查，开发者可以为变量、函数参数、返回值等指定类型。这有助于在开发过程中发现潜在的错误，提高了代码的可维护性和可读性。

2. **面向对象编程：** TypeScript支持面向对象编程的特性，包括类、接口、继承、泛型等。这使得代码更结构化，可重用性更强，同时也提供了更好的代码提示和文档生成。

3. **ES6+支持：** TypeScript支持ECMAScript 6及以上的标准，包括箭头函数、模板字符串、类、模块等新特性。开发者可以使用最新的JavaScript语法，而无需等待浏览器或Node.js的完全支持。

4. **工具支持：** TypeScript具有强大的开发工具支持，包括丰富的编辑器插件、语法高亮、代码提示、重构等功能。最常用的编辑器之一，Visual Studio Code，对TypeScript的支持尤为出色。

5. **增强的可读性和可维护性：** 静态类型和面向对象的特性使得代码更易于理解和维护。类型提示和文档生成使得代码的接口和使用方法更加清晰。

6. **社区和生态系统：** TypeScript拥有庞大的社区支持，许多开源项目都选择使用TypeScript编写。这也使得开发者能够从社区中获取丰富的资源和解决方案。

总体而言，TypeScript为JavaScript提供了一套强大的工具和特性，使得开发大型应用更加容易，代码更加健壮。 TypeScript可以逐渐引入到现有的JavaScript项目中，并在新项目中得到更广泛的应用。





# 类型

## 一.内置类型

TypeScrip默认情况下不用去声明它的类型，他会自动去识别类型

如果没有初始化变量它会把类型设置any(可以表示任何类型的值)



## 二.any类型

TypeScript 提供了许多内置的数据类型，用于声明变量、函数参数、函数返回值等。以下是 TypeScript 中一些常见的内置类型：

1. **基本类型:**
    - **number:** 表示数字，包括整数和浮点数。
    ```typescript
    let num: number = 5;
    ```

    - **string:** 表示文本字符串。
    ```typescript
    let str: string = "Hello, TypeScript!";
    ```

    - **boolean:** 表示布尔值，即 `true` 或 `false`。
    ```typescript
    let isDone: boolean = false;
    ```

    - **null 和 undefined:** 用于表示空值或未定义的值。
    ```typescript
    let n: null = null;
    let u: undefined = undefined;
    ```

    - **any:** 表示任意类型，适用于不清楚变量类型的情况。使用 `any` 会失去 TypeScript 的类型检查。
    ```typescript
    let x: any = 5;
    x = "Hello";
    ```

2. **复合类型:**
    - **Array:** 表示数组。
    ```typescript
    let numbers: number[] = [1, 2, 3];
    ```

    - **Tuple:** 表示元组，允许存储多个不同类型的元素。
    ```typescript
    let tuple: [number, string] = [1, "Hello"];
    ```

    - **Object:** 表示对象类型。
    ```typescript
    let person: { name: string; age: number } = { name: "John", age: 30 };
    ```

    - **Function:** 表示函数类型。
    ```typescript
    let greet: (name: string) => void = function (name: string) {
      console.log("Hello, " + name + "!");
    };
    ```

3. **高级类型:**
    - **Enum:** 用于创建枚举类型。
    ```typescript
    enum Color {
      Red,
      Green,
      Blue,
    }
    let color: Color = Color.Green;
    ```

    - **Union Types:** 允许一个变量具有多种类型。
    ```typescript
    let value: number | string;
    value = 10;     // 合法
    value = "Hello"; // 合法
    ```

    - **Intersection Types:** 结合多个类型为一个类型。
    ```typescript
    type A = { a: number };
    type B = { b: string };
    let ab: A & B = { a: 1, b: "Hello" };
    ```

    - **Type Assertions:** 允许你告诉编译器变量的实际类型。
    ```typescript
    let someValue: any = "Hello, TypeScript!";
    let strLength: number = (someValue as string).length;
    ```

这只是 TypeScript 内置类型的一小部分，还有其他一些更复杂的类型和概念，具体取决于你的项目需求。通过这些类型，TypeScript 提供了强大的静态类型检查，以提高代码的可读性、可维护性和安全性。



## 三.数组

使用类型声明，在后面的有很大的好处！(提示相关类型方法)

```typescript
let numbers : number[] = [1,2,3,4];
```



## 四.元组

在 TypeScript 中，元组（Tuple）是一种**特殊的数组类型**，**它允许你在一个数组中存储多种类型的元素，而且元素的数量是固定的。每个元素的类型和位置都是预定义的。**

元组的定义使用带有类型的数组形式，例如：

```typescript
let myTuple: [number, string, boolean];
myTuple = [10, "Hello", true];
```

上面的例子中，`myTuple` 是一个包含三种不同类型元素的元组。第一个元素是数字，第二个是字符串，第三个是布尔值。

访问元组的元素可以通过索引，索引从 0 开始：

```typescript
console.log(myTuple[0]); // 输出: 10
console.log(myTuple[1]); // 输出: Hello
console.log(myTuple[2]); // 输出: true
```

元组的长度是固定的，如果你试图赋值一个不符合长度的数组，TypeScript 会发出相应的错误：		

```typescript
myTuple = [1, "Two"]; // 错误，元组长度不匹配
```

元组可以在函数中用于返回多个值：

```typescript
function getPerson(): [string, number] {
  return ["John Doe", 30];
}

const person = getPerson();
console.log(person[0]); // 输出: John Doe
console.log(person[1]); // 输出: 30
```

请注意，使用元组时需要小心，因为元组的每个位置都有固定的类型，而且 TypeScript 不会检查元组中的元素类型是否符合预期。在某些情况下，使用对象或其他数据结构可能更为灵活和类型安全。

## 五.枚举

在 TypeScript 中，枚举（Enum）是一种用户定义的数据类型，它主要用于定义一组命名的常量值。枚举通过关联名称和数值，使代码更具可读性和可维护性。

以下是一个简单的枚举的例子：

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let myColor: Color = Color.Green;
console.log(myColor); // 输出: 1
```

在这个例子中，`Color` 是一个枚举，它包含了三个值：`Red`、`Green` 和 `Blue`。每个值都有一个关联的数值，默认从 0 开始，依次递增。在上面的例子中，`Color.Green` 的值是 1。

你也可以手动指定枚举成员的数值：

```typescript
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}

let myColor: Color = Color.Green;
console.log(myColor); // 输出: 2
```

枚举的值可以是数字或字符串。当枚举的值是数字时，如果没有手动指定数值，它会自动递增；如果手动指定数值，后续的值会在指定值的基础上递增。

你还可以通过枚举的值获取对应的名称，例如：

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let colorName: string = Color[1];
console.log(colorName); // 输出: Green
```

在实际应用中，枚举经常用于代表一组有限的状态或选项，以增加代码的清晰度。例如，你可以使用枚举来表示一周的天数：

```typescript
enum Day {
  Sunday,
  Monday,
  Tuesday,
  Wednesday,
  Thursday,
  Friday,
  Saturday,
}

let today: Day = Day.Wednesday;
console.log(today); // 输出: 3 (Wednesday)
```

总的来说，枚举是 TypeScript 中一个有用的工具，用于提高代码的可读性和可维护性。

## 六.函数

TypeScript 中的函数与 JavaScript 中的函数类似，但 TypeScript 允许你添加类型信息，提供更强大的静态类型检查。以下是 TypeScript 函数的一些基本用法和特性：

### 函数声明

你可以使用 `function` 关键字声明函数，并指定参数和返回值的类型：

```typescript
function add(x: number, y: number): number {
  return x + y;
}
```

这里的 `add` 函数接受两个参数 `x` 和 `y`，都是数字类型，并返回它们的和，返回值类型也被指定为 `number`。

### 可选参数和默认参数

你可以使用问号 `?` 来定义可选参数，并使用 `=` 来定义默认参数值：

```typescript
function greet(name: string, greeting?: string): string {
  if (greeting) {
    return `${greeting}, ${name}!`;
  } else {
    return `Hello, ${name}!`;
  }
}

greet("John");          // 输出: Hello, John!
greet("John", "Hi");    // 输出: Hi, John!
```

### 剩余参数

你可以使用剩余参数（Rest Parameters）来处理不定数量的参数：

```typescript
function concatenateStrings(...args: string[]): string {
  return args.join(" ");
}

const result = concatenateStrings("Hello", "TypeScript", "World");
console.log(result);  // 输出: Hello TypeScript World
```

### 函数类型

你可以使用函数类型来描述函数的形状，这对于定义回调函数等场景非常有用：

```typescript
type MathFunction = (x: number, y: number) => number;

const add: MathFunction = (x, y) => x + y;
const subtract: MathFunction = (x, y) => x - y;
```

### 箭头函数

TypeScript 支持使用箭头函数的语法，这种方式更为简洁，尤其适用于简单的函数：

```typescript
const multiply = (x: number, y: number): number => x * y;
```

### 函数重载

你可以使用函数重载来定义多个函数签名，以应对不同的参数类型和数量：

```typescript
function greet(name: string): string;
function greet(firstName: string, lastName: string): string;
function greet(...args: any[]): string {
  if (args.length === 1) {
    return `Hello, ${args[0]}!`;
  } else if (args.length === 2) {
    return `Hello, ${args[0]} ${args[1]}!`;
  }
  return "Invalid parameters.";
}

console.log(greet("John"));             // 输出: Hello, John!
console.log(greet("John", "Doe"));      // 输出: Hello, John Doe!
```

这样，你可以根据传入的参数类型和数量来选择不同的函数实现。

这只是 TypeScript 函数的一些基础用法，还有其他一些高级特性，例如递归类型、泛型函数等，取决于你的需求和项目的复杂性。

## 七.对象

在 TypeScript 中，对象是一个表示数据结构的值，它可以包含多个属性，每个属性都有一个名称和对应的值。对象在 TypeScript 中可以用于表示复杂的数据，可以包括基本数据类型、数组、函数等。

### 对象字面量

最常见的创建对象的方式是使用对象字面量：

```typescript
let person: { name: string; age: number } = {
  name: "John",
  age: 30,
};
```

这里的 `person` 对象有两个属性：`name` 和 `age`，分别是字符串和数字类型。

### 接口

为了更好地描述对象的形状，可以使用接口（Interface）：

```typescript
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: "John",
  age: 30,
};
```

这样，我们可以通过接口定义对象的类型，提高了代码的可读性和可维护性。

### 可选属性

接口中的属性可以标记为可选，表示该属性可以存在也可以不存在：

```typescript
interface Person {
  name: string;
  age?: number; // 可选属性
}

let person1: Person = {
  name: "John",
};

let person2: Person = {
  name: "Jane",
  age: 25,
};
```

### 只读属性

你可以使用 `readonly` 关键字将属性标记为只读，表示该属性在创建后不可修改：

```typescript
interface Point {
  readonly x: number;
  readonly y: number;
}

let point: Point = { x: 10, y: 20 };
// point.x = 30; // 错误，只读属性不可修改
```

### 函数属性

对象的属性可以是函数：

```typescript
interface Greeter {
  greet: (name: string) => void;
}

let greeter: Greeter = {
  greet: function (name: string) {
    console.log(`Hello, ${name}!`);
  },
};
```

### 类型断言

如果你在对象的值赋给一个变量时，无法确定其确切类型，可以使用类型断言：

```typescript
let someValue: any = "Hello, TypeScript!";
let strLength: number = (someValue as string).length;
```

### 对象解构

你可以使用对象解构来快速提取对象中的属性：

```typescript
let person: { name: string; age: number } = {
  name: "John",
  age: 30,
};

let { name, age } = person;
console.log(name); // 输出: John
console.log(age);  // 输出: 30
```

这只是 TypeScript 中处理对象的一些基本方式，还有更多的高级特性和概念，例如索引签名、嵌套对象、映射类型等，取决于你的需求和项目的复杂性。

# 高级类型

TypeScript 提供了许多高级类型来增强代码的灵活性和可读性。以下是一些常见的高级类型：

### 1. 联合类型（Union Types）

联合类型允许一个变量具有多种类型中的一种：

```typescript
let myVar: string | number;
myVar = "Hello";
myVar = 42;
```

### 2. 交叉类型（Intersection Types）

交叉类型允许将多个类型合并成一个：

```typescript
type A = { a: number };
type B = { b: string };

let ab: A & B = { a: 1, b: "Hello" };
```

### 3. 类型别名（Type Aliases）

类型别名允许给一个类型起一个新的名字，可以更方便地引用复杂的类型：

```typescript
type Point = { x: number; y: number };
let point: Point = { x: 1, y: 2 };
```

### 4. 字面量类型

可以使用字面量类型约束变量的值：

```typescript
let status: "success" | "error";
status = "success"; // 合法
// status = "other"; // 错误
```

### 5. 映射类型（Mapped Types）

映射类型允许创建新类型，它基于已有类型中的属性创建新属性：

```typescript
type Flags = {
  option1: boolean;
  option2: boolean;
};

type ReadonlyFlags = {
  readonly [K in keyof Flags]: boolean;
};
```

### 6. 条件类型（Conditional Types）

条件类型根据某个类型是否满足条件来选择另一种类型：

```typescript
type NonNullable<T> = T extends null | undefined ? never : T;

let value: string | null = /* ... */;
let nonNullableValue: NonNullable<typeof value> = value; // 剔除 null 类型
```

### 7. 索引类型（Index Types）

索引类型用于从对象中提取属性值的类型：

```typescript
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person; // "name" | "age"
type PersonTypes = Person[keyof Person]; // string | number
```

### 8. 可辨识联合类型（Discriminated Unions）

可辨识联合类型是一种通过共享字段来判断联合类型的一种模式：

```typescript
interface Square {
  kind: "square";
  size: number;
}

interface Circle {
  kind: "circle";
  radius: number;
}

type Shape = Square | Circle;

function area(shape: Shape): number {
  switch (shape.kind) {
    case "square":
      return shape.size * shape.size;
    case "circle":
      return Math.PI * shape.radius ** 2;
  }
}
```

这只是 TypeScript 中一些高级类型的简要介绍，还有更多的概念和用法，具体取决于你的项目需求。深入了解这些概念可以帮助你更好地利用 TypeScript 的强大类型系统。

## 一.类型别名

在 TypeScript 中，类型别名（Type Aliases）是一种方式，允许你给一个已有类型起一个新的名字。这对于简化复杂类型、提高代码可读性以及使类型更具表达力都非常有用。

以下是一些使用类型别名的例子：

### 基本用法

```typescript
type ID = number;
let userId: ID = 123;
```

在这个例子中，`ID` 是 `number` 的别名，使代码更易读。

### 复杂类型

```typescript
type Point = {
  x: number;
  y: number;
};

type Shape = {
  name: string;
  color: string;
  coordinates: Point[];
};
```

这里，`Shape` 别名使用了之前定义的 `Point` 别名，使代码更清晰。

### 泛型类型别名

```typescript
type Result<T> = {
  success: boolean;
  data: T;
};

let stringResult: Result<string> = {
  success: true,
  data: "Hello, TypeScript!",
};

let numberResult: Result<number> = {
  success: true,
  data: 42,
};
```

`Result` 是一个接受泛型参数的类型别名，它可以用于不同的数据类型。

### 联合类型别名

```typescript
type Status = "success" | "error";

let response: Status = "success";
```

在这个例子中，`Status` 是一个字符串字面量类型的联合，限定了变量的取值范围。

### 字符串字面量联合类型

```typescript
type Direction = "up" | "down" | "left" | "right";

let move: Direction = "up";
```

`Direction` 是一个字符串字面量联合类型，限定了变量的可能取值。

### 可辨识联合类型别名

```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; size: number };

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.size ** 2;
  }
}
```

在这个例子中，`Shape` 是一个可辨识联合类型别名，通过 `kind` 字段判断联合类型的成员。

类型别名可以用于任何类型，从基础类型到复杂的对象类型，都可以通过类型别名进行命名和组织。使用类型别名可以使代码更清晰、更易维护，并提高代码的可读性。

## 二.联合类型

在 TypeScript 中，联合类型（Union Types）是一种允许一个变量具有多种类型之一的类型。使用联合类型可以增加灵活性，使变量能够接受多种不同类型的值。联合类型使用 `|` 符号来分隔多个类型。

以下是一些联合类型的基本用法：

### 基础联合类型

```typescript
let myVar: string | number;
myVar = "Hello"; // 合法
myVar = 42;      // 合法
// myVar = true;  // 错误，布尔值不是 string 或 number 类型
```

`myVar` 可以是 `string` 类型或 `number` 类型之一。

### 联合类型作为函数参数

```typescript
function displayData(data: string | number): void {
  console.log(data);
}

displayData("Hello"); // 输出: Hello
displayData(42);      // 输出: 42
// displayData(true);  // 错误，布尔值不是 string 或 number 类型
```

### 联合类型在对象中的应用

```typescript
interface Circle {
  kind: "circle";
  radius: number;
}

interface Square {
  kind: "square";
  size: number;
}

type Shape = Circle | Square;

function getArea(shape: Shape): number {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.size ** 2;
  }
}

let circle: Shape = { kind: "circle", radius: 5 };
let square: Shape = { kind: "square", size: 4 };

console.log(getArea(circle)); // 输出: 78.54
console.log(getArea(square)); // 输出: 16
```

在这个例子中，`Shape` 是一个联合类型，它可以是 `Circle` 或 `Square` 中的一种。在 `getArea` 函数中，通过检查 `kind` 属性来确定是哪种形状。

### 联合类型的 null 和 undefined

联合类型常常与 `null` 和 `undefined` 一起使用，表示变量可以接受多种类型值，包括可能为 `null` 或 `undefined`。

```typescript
let myVar: string | null | undefined;
myVar = "Hello";   // 合法
myVar = null;      // 合法
myVar = undefined; // 合法
```

这样的联合类型表达了一个可能是字符串，也可能是 `null` 或 `undefined` 的变量。

使用联合类型时，需要注意确保正确处理所有可能的类型。可以使用类型保护或者类型断言来缩小类型，以确保代码的正确性。

## 三.交叉类型

在 TypeScript 中，交叉类型（Intersection Types）允许将多个类型合并成一个新类型。通过 `&` 符号，你可以将多个类型组合到一起，形成一个包含所有类型成员的新类型。

以下是一些基本的交叉类型用法：

### 基本交叉类型

```typescript
type Person = { name: string; age: number };
type Address = { address: string; city: string };

type PersonWithAddress = Person & Address;

let personWithAddress: PersonWithAddress = {
  name: "John",
  age: 30,
  address: "123 Main St",
  city: "Anytown",
};
```

在这个例子中，`PersonWithAddress` 是一个交叉类型，包含了 `Person` 和 `Address` 两个类型的所有成员。

### 函数中的交叉类型

```typescript
type Logger = {
  log: (message: string) => void;
};

type ConsoleWriter = {
  writeConsole: (message: string) => void;
};

type ConsoleLogger = Logger & ConsoleWriter;

let consoleLogger: ConsoleLogger = {
  log: (message) => console.log(message),
  writeConsole: (message) => console.log(message),
};
```

在这个例子中，`ConsoleLogger` 包含了 `Logger` 和 `ConsoleWriter` 的所有成员，适用于同时记录日志到控制台。

### 多个类型的组合

```typescript
type Car = { brand: string; model: string };
type Electric = { electric: boolean };
type HybridCar = Car & Electric;

let hybridCar: HybridCar = {
  brand: "Toyota",
  model: "Prius",
  electric: true,
};
```

这里，`HybridCar` 是 `Car` 和 `Electric` 的交叉类型，表示一辆混合动力汽车。

### 类型合并

```typescript
type A = { a: number };
type B = { b: string };
type C = { c: boolean };

type ABC = A & B & C;

let abc: ABC = { a: 1, b: "Hello", c: true };
```

在这个例子中，`ABC` 包含了 `A`、`B` 和 `C` 三个类型的所有成员。

交叉类型在一些场景中特别有用，例如在函数重载、React 组件中的属性合并等地方。它允许你创建更灵活的类型，能够同时使用多个类型的特性。需要注意，与联合类型不同，交叉类型是取多个类型的交集。

## 四.字面类型

在 TypeScript 中，字面类型（Literal Types）是指具体的值，而不仅仅是类型的标识。字面类型可以是字符串、数字、布尔值，甚至是联合类型、交叉类型等的特殊形式。

以下是一些字面类型的例子：

### 字符串字面类型

```typescript
let status: "success" | "error";
status = "success"; // 合法
// status = "other"; // 错误，只能是 "success" 或 "error"
```

在这个例子中，`status` 只能是字符串字面类型 "success" 或 "error" 中的一个。

### 数字字面类型

```typescript
let num: 42;
num = 42; // 合法
// num = 1; // 错误，只能是数字字面类型 42
```

在这个例子中，`num` 只能是数字字面类型 42。

### 布尔字面类型

```typescript
let isTrue: true;
isTrue = true; // 合法
// isTrue = false; // 错误，只能是布尔字面类型 true
```

在这个例子中，`isTrue` 只能是布尔字面类型 true。

### 字面类型联合

```typescript
type Gender = "male" | "female";
let gender: Gender = "male"; // 合法
// let gender: Gender = "other"; // 错误，只能是 "male" 或 "female"
```

在这个例子中，`Gender` 是一个字符串字面类型联合，`gender` 变量只能是 "male" 或 "female"。

### 对象字面类型

```typescript
let person: { name: "John"; age: 30 };
person = { name: "John", age: 30 }; // 合法
// person = { name: "Jane", age: 25 }; // 错误，属性值必须是 "John" 和 30
```

在这个例子中，`person` 变量的类型是一个对象，其中 `name` 属性必须是字面类型 "John"，而 `age` 属性必须是数字字面类型 30。

字面类型在 TypeScript 中广泛用于表示一些确定的、具体的值，它们提供了更精确的类型信息，有助于提高代码的可读性和可维护性。

## 五.可null类型

在 TypeScript 中，可以使用联合类型或可选属性的方式表示允许 `null` 值的类型。以下是两种常见的处理可为 `null` 的情况的方式：

### 联合类型

使用联合类型时，可以使用 `null` 或 `undefined` 作为其中一个类型的选项：

```typescript
let myVar: string | null;
myVar = "Hello"; // 合法
myVar = null;    // 合法
// myVar = 42;    // 错误，不能将数字赋给 string | null 类型
```

### 可选属性

在对象类型中，可以使用可选属性来表示某个属性可以为 `null`：

```typescript
interface Person {
  name: string;
  age?: number | null;
}

let john: Person = { name: "John" };
let jane: Person = { name: "Jane", age: null };
let bob: Person = { name: "Bob", age: 25 };
```

在上面的例子中，`age` 是一个可选属性，它可以是数字、`null` 或者 `undefined`。如果不提供 `age` 属性，那么默认为 `undefined`。

这两种方式结合使用时，可以创建一个允许变量既为某个具体类型又为 `null` 或 `undefined` 的类型。这对于处理可能不存在的值非常有用。然而，在使用时需要小心，确保在可能为 `null` 的值上执行操作之前进行适当的检查，以避免运行时错误。

## 六.可选链

可选链（Optional Chaining）是一种 JavaScript 和 TypeScript 中引入的语法特性，用于简化访问可能为 `null` 或 `undefined` 的属性或方法的代码。

在使用可选链时，你可以使用 `?.` 运算符来访问对象的属性或调用方法，如果目标属性或方法不存在，表达式会返回 `undefined`，而不会导致运行时错误。

以下是一个使用可选链的 TypeScript 示例：

```typescript
interface Person {
  name: string;
  age?: number;
  address?: {
    street?: string;
    city?: string;
  };
}

let person: Person | null = /* ... */;

// 使用可选链
let street = person?.address?.street;
console.log(street); // 如果 address 或 street 为 null 或 undefined，将输出 undefined
```

在上面的例子中，如果 `person` 为 `null` 或 `undefined`，或者 `person.address` 为 `null` 或 `undefined`，那么 `street` 将会是 `undefined`。

可选链的优点在于它提供了更加简洁和安全的方式来访问可能不存在的属性或方法，避免了在嵌套的属性和方法中手动进行空值检查。

注意：可选链在 TypeScript 3.7 及以上版本中得到支持。如果你的 TypeScript 版本较旧，可能需要升级 TypeScript 版本才能使用可选链。

## 七.空值合并

空值合并运算符（Nullish Coalescing Operator）是 JavaScript 和 TypeScript 中引入的一种运算符，用于提供更直观、精确的默认值设置，主要解决了在某些情况下对 `null` 或 `undefined` 的默认值设定问题。

这个运算符使用 `??` 表示，其语法为 `a ?? b`，其中 `a` 是一个表达式，如果 `a` 的值为 `null` 或 `undefined`，则表达式的结果是 `b`，否则是 `a` 的值。

以下是一个示例：

```typescript
let defaultValue = "Default Value";
let userInput: string | null = /* 用户输入的值，可能为 null */;

let result = userInput ?? defaultValue;

console.log(result);
```

在上面的例子中，如果 `userInput` 的值为 `null` 或 `undefined`，`result` 将取默认值 `"Default Value"`，否则取 `userInput` 的值。

与传统的逻辑运算符 `||` 不同，空值合并运算符 `??` 仅在左侧的表达式值为 `null` 或 `undefined` 时才会返回右侧的默认值，而不会在左侧的表达式值为其他 falsy 值时返回默认值。

这种特性使得空值合并运算符更适合处理对 `null` 或 `undefined` 的默认值设定，避免了对 falsy 值的误判。

## 八.类型断言

类型断言是 TypeScript 中的一种机制，它允许开发者手动指定变量的类型。这可以用于告诉编译器，开发者有更多的信息，从而在某些情况下绕过编译器的类型检查。类型断言有两种形式：尖括号语法和as语法。

### 尖括号语法

```typescript
let value: any = "Hello, TypeScript!";
let strLength: number = (<string>value).length;
```

在上面的例子中，`<string>` 是一种类型断言的方式，它告诉编译器将 `value` 视为字符串类型，以便可以访问 `length` 属性。不过，**这种方式在 React 或 JSX 中会产生歧义，因此更推荐使用 `as` 语法。**

### as语法

```typescript
let value: any = "Hello, TypeScript!";
let strLength: number = (value as string).length;
```

`as` 语法是另一种类型断言的方式，它与尖括号语法具有相同的效果，但更适合在 JSX/TSX 中使用，因为它不会与 JSX 的语法产生歧义。

### 使用场景

1. **当开发者比编译器更清楚一个值的类型时。**

   ```typescript
   let userInput: any = "Hello, TypeScript!";
   let strLength: number = (userInput as string).length;
   ```

2. **当从一个类型转换为另一个类型时。**

   ```typescript
   let value: any = "42";
   let numericValue: number = (value as unknown) as number;
   ```

3. **在使用第三方库时，或者当 TypeScript 无法正确推断类型时。**

   ```typescript
   const element = document.getElementById("myElement");
   let value: string = (element as HTMLInputElement).value;
   ```

需要注意的是，滥用类型断言可能会导致运行时错误，因此最好确保类型断言的目标类型是正确的。在大多数情况下，应该尽量避免使用类型断言，而是依赖于 TypeScript 的类型推断和类型系统。

## 九.未知类型

未知类型（Unknown Type）是 TypeScript 3.0 引入的一种类型，用于表示一个未知的值的类型。与 `any` 类型不同，`unknown` 类型提供了类型安全，因为在使用未知类型的值时，必须先进行类型检查或类型断言。

```typescript
let userInput: unknown;

userInput = 5;
userInput = "Hello, TypeScript!";

// 编译器会报错，因为不能直接使用未知类型的值
// let userName: string = userInput; // Error: Type 'unknown' is not assignable to type 'string'.

// 使用类型断言
let userName: string = userInput as string;
```

在上面的例子中，**`userInput` 被声明为 `unknown` 类型，可以接受任何类型的值。当我们尝试将其赋值给一个明确的类型（如 `string`）时，TypeScript 编译器会报错，要求我们进行类型检查或类型断言。**

### 类型检查

使用 `typeof` 或其他类型检查机制，可以在使用 `unknown` 类型的值之前进行类型检查：

```typescript
if (typeof userInput === "string") {
  let userName: string = userInput; // OK
}

// 或者使用类型守卫函数
function isString(value: unknown): value is string {
  return typeof value === "string";
}

if (isString(userInput)) {
  let userName: string = userInput; // OK
}
```

### unknown vs any

与 `any` 类型相比，`unknown` 类型提供了更严格的类型检查。使用 `any` 时，可以对其执行任何操作而不会得到类型错误，而使用 `unknown` 时，必须先进行类型检查或类型断言，以确保类型的正确性。

```typescript
let anyValue: any;
let unknownValue: unknown;

let num: number = anyValue; // OK
// let num: number = unknownValue; // Error: Type 'unknown' is not assignable to type 'number'.

let str: string = anyValue; // OK
// let str: string = unknownValue; // Error: Type 'unknown' is not assignable to type 'string'.

// 使用类型断言
let str2: string = unknownValue as string; // OK
```

总的来说，如果你知道一个值的类型是不确定的，但希望在使用它之前进行类型检查，推荐使用 `unknown` 类型，因为它提供了更严格的类型安全性。

## 十.从不类型

"从不类型"（Never Type）是 TypeScript 中的一种特殊的类型，表示那些永远不会发生的值的类型。通常，它用于函数返回值，表明该函数永远不会正常返回。

以下是一些使用 "从不类型" 的例子：

### 函数永不返回

```typescript
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // 无限循环，永不返回
  }
}
```

在这个例子中，`throwError` 函数抛出一个错误，`infiniteLoop` 函数则是一个无限循环，都是不会正常返回的。

### 推断为 "从不类型"

TypeScript 有一些上下文中，编译器能够推断出某个值的类型为 "从不类型"。

```typescript
function unreachableCode(): never {
  throw new Error("This code is unreachable.");
}

let x: number = 5;

if (typeof x === "string") {
  // 在此分支中，编译器会推断 x 的类型为 never
  // 因为在前一个分支中已经将 x 的类型缩小为 number，此分支不可能执行到
  unreachableCode();
}
```

在这个例子中，由于前一个分支将 `x` 的类型缩小为 `number`，所以在后续的 `typeof x === "string"` 分支中，编译器会推断 `x` 的类型为 "从不类型"，因为这个分支不可能执行到。

### 类型守卫中的 "从不类型"

使用类型守卫的情况下，有时也可以推断出 "从不类型"。

```typescript
function isString(value: string | number): value is string {
  return typeof value === "string";
}

function processValue(value: string | number): void {
  if (isString(value)) {
    // 在此分支中，编译器会推断 value 的类型为 string
    console.log(value.toUpperCase());
  } else {
    // 在此分支中，编译器会推断 value 的类型为 never
    // 因为 isString 函数已经将字符串类型排除，这个分支不可能执行到
    console.log(value); // Error: Variable 'value' is used before being assigned.
  }
}
```

在这个例子中，`isString` 函数的类型守卫使得在后续的分支中，`value` 被推断为 "从不类型"，因为字符串类型在前一个分支已经被排除。

总体来说，"从不类型"在一些特殊的情况下，帮助编译器进行更精准的类型推断，同时它的主要用途是表示不会正常返回的函数的返回类型。



 





# 类、接口和面向对象的编程

## 一.创建类

在 TypeScript 中，你可以使用 `class` 关键字来创建类。下面是一个简单的例子，演示了如何创建一个类及其实例：

```typescript
class Animal {
  // 类的属性
  name: string;

  // 类的构造函数
  constructor(name: string) {
    this.name = name;
  }

  // 类的方法
  makeSound(): void {
    console.log("Some generic sound");
  }
}

// 创建 Animal 类的实例
const cat = new Animal("Whiskers");

// 访问实例的属性和调用方法
console.log(cat.name);      // 输出: Whiskers
cat.makeSound();            // 输出: Some generic sound
```

上述代码定义了一个 `Animal` 类，该类有一个属性 `name`，一个构造函数，以及一个方法 `makeSound`。然后，通过 `new` 关键字创建了一个 `Animal` 类的实例 `cat`，并通过实例访问了属性和调用了方法。

在 TypeScript 中，你还可以使用访问修饰符（public、private、protected）来限制属性和方法的访问级别。下面是一个带有私有属性和方法的例子：

```typescript
class Person {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  private greet(): void {
    console.log(`Hello, my name is ${this.name}`);
  }

  introduce(): void {
    this.greet(); // 可以在类内部调用私有方法
    console.log("Nice to meet you!");
  }
}

const person = new Person("John");
person.introduce(); // 输出: Hello, my name is John \n Nice to meet you!
// person.greet(); // 错误，私有方法在类外部不可访问
```

在这个例子中，`Person` 类有一个私有属性 `name` 和一个私有方法 `greet`，而 `introduce` 方法是公共的，可以在类的外部调用。访问私有属性和方法需要在类的内部进行。

## 二.创建对象

在 TypeScript 中，你可以使用类（class）或对象字面量（object literal）的方式创建对象。以下是两种方式的示例：

### 使用类创建对象：

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}

// 创建 Person 对象
const john = new Person("John", 30);

// 调用对象的方法
john.greet();
```

在这个例子中，我们定义了一个 `Person` 类，然后使用 `new` 关键字创建了一个 `Person` 对象 `john`。

### 使用对象字面量创建对象：

```typescript
let person = {
  name: "John",
  age: 30,
  greet: function() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
};

// 调用对象的方法
person.greet();
```

在这个例子中，我们直接使用对象字面量定义了一个对象 `person`，其中包含了 `name`、`age` 和 `greet` 属性。

无论是使用类还是对象字面量，都可以在对象上定义属性和方法。类的优势在于它可以更好地组织和抽象代码，支持继承、封装等面向对象的特性。对象字面量更适合简单的情况，当你只需要创建一个简单的对象时可以选择使用对象字面量。

## 三.只读和可选属性

在 TypeScript 中，你可以使用 `readonly` 关键字来定义只读属性，以及使用 `?` 来定义可选属性。

### 只读属性：

```typescript
interface Person {
  readonly name: string;
  age: number;
}

let john: Person = { name: "John", age: 30 };

// 下面这行代码将会报错，因为 name 是只读属性
// john.name = "Jane";
```

在上述例子中，`name` 属性被标记为 `readonly`，因此在对象被创建之后，就不能再修改 `name` 属性的值。

### 可选属性：

在 TypeScript 中，类中的可选属性可以不被初始化，因为它们的值可以是 `undefined`。可选属性使用 `?` 进行标记，表示在创建对象时可以选择性地提供这些属性，如果未提供，则它们的值默认为 `undefined`。

```typescript
interface Car {
  brand: string;
  model: string;
  year?: number; // 使用 ? 表示可选属性
}

let myCar: Car = { brand: "Toyota", model: "Camry" };

// year 属性是可选的，可以不提供
let anotherCar: Car = { brand: "Honda", model: "Civic", year: 2020 };
```

在上述例子中，`year` 属性被标记为可选，表示在创建 `Car` 对象时，可以选择性地提供 `year` 属性，也可以不提供。

在实际开发中，只读属性和可选属性可以结合使用，以确保对象的某些属性只读，而另一些属性可选。例如：

```typescript
interface Config {
  readonly server: string;
  port?: number;
  apiKey: string;
}

let prodConfig: Config = { server: "prod-server.com", apiKey: "abc123" };
let devConfig: Config = { server: "localhost", port: 3000, apiKey: "dev123" };
```

在这个例子中，`server` 是只读属性，`port` 是可选属性，而 `apiKey` 是必需属性。

## 四.访问控制关键字

在 TypeScript 中，访问控制关键字用于控制类成员（属性和方法）的访问权限。有三个主要的访问控制关键字：`public`、`private`、`protected`。

1. **public：** 没有访问限制，可以在类的内部和外部访问。

   ```typescript
   class Animal {
     public name: string;

     constructor(name: string) {
       this.name = name;
     }
   }

   let cat = new Animal("Whiskers");
   console.log(cat.name); // 可以访问，因为 name 是公共属性
   ```

2. **private：** 只能在类的内部访问，外部无法访问。

   ```typescript
   class Person {
     private age: number;

     constructor(age: number) {
       this.age = age;
     }

     getAge(): number {
       return this.age; // 可以在类的内部访问
     }
   }

   let john = new Person(30);
   // console.log(john.age); // 错误，无法在类的外部访问 private 属性
   console.log(john.getAge()); // 可以通过公共方法访问 private 属性
   ```

3. **protected：** 类的内部和派生类中可以访问，但在类的外部无法访问。

   ```typescript
   class Employee {
     protected salary: number;
   
     constructor(salary: number) {
       this.salary = salary;
     }
   }
   
   class Manager extends Employee {
     getSalary(): number {
       return this.salary; // 可以在派生类中访问 protected 属性
     }
   }
   
   let manager = new Manager(50000);
   // console.log(manager.salary); // 错误，无法在类的外部访问 protected 属性
   console.log(manager.getSalary()); // 可以通过派生类的方法访问 protected 属性
   ```

这些访问控制关键字用于帮助开发者设计更安全和可维护的代码。`public` 是默认的访问修饰符，如果不指定，默认就是 `public`。需要注意的是，TypeScript 的访问控制是在编译时进行的，而不是在运行时。

## 五.参数属性

**在 TypeScript 中，参数属性是一种特殊的语法，允许你在构造函数参数声明的同时声明并初始化类的属性。这样可以简化代码，避免在构造函数中显式地为属性赋值。**

下面是一个使用参数属性的例子：

```typescript
class Person {
  // 使用参数属性，省略了在构造函数中显式声明和赋值的步骤
  constructor(public name: string, public age?: number) {
    // 可选：在构造函数中可以执行其他逻辑
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age || 'unknown'} years old.`);
  }
}

// 创建 Person 类的实例，不需要显式声明和赋值属性
let john = new Person("John", 30);
let jane = new Person("Jane");

john.greet(); // 输出: Hello, my name is John and I'm 30 years old.
jane.greet(); // 输出: Hello, my name is Jane and I'm unknown years old.
```

在上述例子中，`name` 和 `age` 被声明为参数属性。通过在构造函数参数前添加修饰符（`public`、`private`、`protected` 或 `readonly`），可以将它们声明为参数属性。这样，TypeScript 将自动创建和初始化这些属性。

使用参数属性的好处在于，可以通过在构造函数参数上添加修饰符，一步完成属性的声明和初始化，减少了代码的冗余。在大多数情况下，使用参数属性是一种简洁而方便的方式。



## 六.寄存器Setter和Getter

在 TypeScript 或 JavaScript 中，你可以使用属性的 getter 和 setter 来实现对属性的访问和修改的控制。Getter 用于获取属性值，Setter 用于设置属性值。这提供了对类属性的更灵活的访问和修改方式，允许你在获取或设置属性时执行额外的逻辑。

下面是一个使用 getter 和 setter 的 TypeScript 示例：

```typescript
class Circle {
  private _radius: number;

  constructor(radius: number) {
    this._radius = radius;
  }

  // Getter
  get radius(): number {
    return this._radius;
  }

  // Setter
  set radius(value: number) {
    if (value >= 0) {
      this._radius = value;
    } else {
      console.log("Radius must be a non-negative value.");
    }
  }

  // 计算圆的面积
  calculateArea(): number {
    return Math.PI * this._radius ** 2;
  }
}

// 创建 Circle 类的实例
let myCircle = new Circle(5);

// 使用 getter 获取半径
console.log(myCircle.radius); // 输出: 5

// 使用 setter 设置半径
myCircle.radius = 7;

// 使用 getter 获取修改后的半径
console.log(myCircle.radius); // 输出: 7

// 试图使用 setter 设置负值
myCircle.radius = -3; // 输出: Radius must be a non-negative value.

// 计算并输出圆的面积
console.log(myCircle.calculateArea()); // 输出: 153.93804002589985
```

在这个例子中，`Circle` 类有一个私有属性 `_radius`，然后通过 `get radius()` 和 `set radius(value)` 定义了 radius 的 getter 和 setter。Getter 允许你获取 `_radius` 的值，而 setter 允许你设置 `_radius` 的值，并在设置时进行一些额外的逻辑检查（这里是确保半径不为负值）。



## 七.索引签名

在 TypeScript 中，索引签名（Index Signature）是一种允许你使用任意字符串或数字来索引对象属性的机制。通过索引签名，你可以灵活地定义对象的结构，使其能够包含未知名称的属性。

在对象类型中，可以使用 `[key: string]: valueType` 或 `[key: number]: valueType` 来定义索引签名。其中 `key` 表示索引的类型，`valueType` 表示对应索引的值的类型。

以下是一个使用索引签名的示例：

```typescript
// 索引签名为字符串，值为任意类型
interface Dictionary {	
  [key: string]: any;
}

// 创建一个拥有索引签名的对象
let myDictionary: Dictionary = {
  name: "John",
  age: 30,
  city: "New York"
};

// 可以通过任意字符串来索引对象
console.log(myDictionary["name"]); // 输出: John
console.log(myDictionary["age"]);  // 输出: 30
console.log(myDictionary["city"]); // 输出: New York

// 索引签名为数字，值为字符串类型
interface StringArray {
  [index: number]: string;
}

// 创建一个拥有索引签名的数组
let myArray: StringArray = ["Apple", "Banana", "Orange"];

// 可以通过数字索引来访问数组元素
console.log(myArray[0]); // 输出: Apple
console.log(myArray[1]); // 输出: Banana
console.log(myArray[2]); // 输出: Orange
```

在上述例子中，`Dictionary` 接口定义了一个拥有字符串索引签名的对象，可以包含任意类型的属性。而 `StringArray` 接口定义了一个拥有数字索引签名的字符串数组。使用索引签名使得这些对象和数组可以包含未知名称的属性或元素。

需要注意的是，当使用索引签名时，其他具有明确名称的属性的类型也需要符合索引签名的要求。在 `Dictionary` 的例子中，其他属性的类型可以是任意的。在 `StringArray` 的例子中，其他属性（即数字索引之外的属性）的类型需要是字符串。



## 八.静态成员

在 TypeScript 中，静态成员是指属于类本身而不是类的实例的成员。它们使用 `static` 关键字进行定义。静态成员与类直接相关，而不依赖于类的实例。以下是 TypeScript 中静态成员的一些常见概念和用法：

1. **静态属性（Static Properties）：** 静态属性是与类直接关联，而不是与类的实例相关联的属性。它们通过 `static` 关键字定义。

   ```typescript
   class MyClass {
       static staticProperty: number = 0;

       // 其他类成员和方法...
   }
   ```

2. **静态方法（Static Methods）：** 静态方法也是与类直接关联的方法，而不需要依赖于类的实例。它们通过 `static` 关键字定义。

   ```typescript
   class MyClass {
       static staticMethod() {
           // 静态方法的实现...
       }

       // 其他类成员和方法...
   }
   ```

3. **静态成员的访问：** 可以通过类本身来访问静态成员，而不需要创建类的实例。

   ```typescript
   console.log(MyClass.staticProperty); // 访问静态属性
   MyClass.staticMethod(); // 调用静态方法
   ```

4. **静态构造函数（Static Constructor）：** TypeScript 中没有专门的静态构造函数概念，但可以使用类的静态块来进行静态初始化操作。

   ```typescript
   class MyClass {
       static {
           // 静态块的初始化代码...
       }
   
       // 其他类成员和方法...
   }
   ```

静态成员在 TypeScript 中与其他面向对象编程语言类似，提供了类级别的功能，可以用于存储类范围内的信息或执行与类直接相关的操作。使用静态成员时，需要通过类名来访问，而不是通过类的实例。



## 九.继承

在 TypeScript 中，继承是一种面向对象编程的概念，允许一个类（子类）基于另一个类（父类）来创建，从而获得父类的属性和方法。通过继承，子类可以重用父类的代码并进行扩展。以下是 TypeScript 中继承的基本用法和概念：

1. **基本继承语法：** 使用 `extends` 关键字来实现类的继承。

    ```typescript
    class Animal {
        name: string;

        constructor(name: string) {
            this.name = name;
        }

        eat() {
            console.log(`${this.name} is eating.`);
        }
    }

    class Dog extends Animal {
        bark() {
            console.log(`${this.name} is barking.`);
        }
    }

    // 创建一个 Dog 实例
    const myDog = new Dog("Buddy");

    // 调用继承自 Animal 的 eat 方法
    myDog.eat();

    // 调用 Dog 自己的 bark 方法
    myDog.bark();
    ```

2. **构造函数中的 super：** 子类的构造函数中需要调用 `super()` 来调用父类的构造函数，以便初始化继承自父类的属性。

    ```typescript
    class Animal {
        name: string;

        constructor(name: string) {
            this.name = name;
        }

        eat() {
            console.log(`${this.name} is eating.`);
        }
    }

    class Dog extends Animal {
        breed: string;

        constructor(name: string, breed: string) {
            super(name); // 调用父类的构造函数
            this.breed = breed;
        }

        bark() {
            console.log(`${this.name} is barking.`);
        }
    }

    // 创建一个 Dog 实例
    const myDog = new Dog("Buddy", "Golden Retriever");

    // 调用继承自 Animal 的 eat 方法
    myDog.eat();

    // 调用 Dog 自己的 bark 方法
    myDog.bark();
    ```

3. **方法的覆写：** 子类可以覆写从父类继承来的方法，以实现特定于子类的行为。

    ```typescript
    class Animal {
        makeSound() {
            console.log("Some generic sound");
        }
    }

    class Dog extends Animal {
        makeSound() {
            console.log("Woof! Woof!");
        }
    }

    const myDog = new Dog();
    myDog.makeSound(); // 输出: Woof! Woof!
    ```

4. **抽象类和抽象方法：** TypeScript 支持抽象类和抽象方法，抽象类不能直接实例化，而是用于被其他类继承。

    ```typescript
    abstract class Shape {
        abstract draw(): void;
    }
    
    class Circle extends Shape {
        draw() {
            console.log("Drawing a circle");
        }
    }
    
    const myCircle = new Circle();
    myCircle.draw(); // 输出: Drawing a circle
    ```

继承是面向对象编程的基本概念之一，通过合理使用继承，可以提高代码的重用性和可维护性。在设计时，需要注意适度的继承，以避免过度复杂的继承关系。



## 十.多态性

多态性是面向对象编程的一个重要概念，指的是同一个方法名可以被不同的对象调用，而产生不同的行为。多态性分为编译时多态（静态多态性）和运行时多态（动态多态性）两种类型。

### 编译时多态（静态多态性）

编译时多态是通过方法的重载和方法的重写实现的。

1. **方法的重载：** 同一个类中可以定义多个同名的方法，但它们的参数列表不同。编译器在编译时根据方法的参数类型、个数、顺序等信息来选择正确的方法。

    ```typescript
    class MathOperations {
        add(a: number, b: number): number {
            return a + b;
        }

        add(a: string, b: string): string {
            return a + b;
        }
    }

    const mathOps = new MathOperations();
    mathOps.add(1, 2);       // 编译时选择第一个 add 方法
    mathOps.add("1", "2");   // 编译时选择第二个 add 方法
    ```

2. **方法的重写：** 在继承关系中，子类可以重写父类的方法。在编译时，方法的调用会根据引用变量的类型来确定调用的是哪个类中的方法。

    ```typescript
    class Animal {
        makeSound() {
            console.log("Some generic sound");
        }
    }
    
    class Dog extends Animal {
        makeSound() {
            console.log("Woof! Woof!");
        }
    }
    
    const myDog: Animal = new Dog();
    myDog.makeSound(); // 编译时选择 Dog 类中的 makeSound 方法
    ```

### 运行时多态（动态多态性）

运行时多态是通过方法的重写（覆盖）实现的。在运行时，程序根据对象的实际类型来确定调用的方法。

```typescript
class Animal {
    makeSound() {
        console.log("Some generic sound");
    }
}

class Dog extends Animal {
    makeSound() {
        console.log("Woof! Woof!");
    }
}

class Cat extends Animal {
    makeSound() {
        console.log("Meow!");
    }
}

const animals: Animal[] = [new Dog(), new Cat()];

for (const animal of animals) {
    animal.makeSound(); // 运行时根据实际类型调用相应的 makeSound 方法
}
```

在上述例子中，`Animal` 类有一个 `makeSound` 方法，`Dog` 和 `Cat` 类都继承自 `Animal` 类并重写了 `makeSound` 方法。当遍历 `animals` 数组并调用 `makeSound` 方法时，实际调用的是各个对象的具体类型中的 `makeSound` 方法。这展示了运行时多态性的概念。





## 十一,接口

在 TypeScript 中，接口（Interfaces）是一种用于定义对象的结构的抽象概念。接口描述了对象应该具有的属性和方法，但不提供实际的实现。通过实现接口，可以确保对象符合特定的契约或约定。以下是 TypeScript 中接口的基本用法和概念：

### 定义接口

可以使用 `interface` 关键字定义接口：

```typescript
interface Person {
    name: string;
    age: number;
    sayHello(): void;
}
```

上述接口 `Person` 描述了一个具有 `name` 和 `age` 属性，以及一个 `sayHello` 方法的对象。

### 实现接口

使用 `implements` 关键字来实现接口，确保实现类或对象包含接口中定义的所有属性和方法：

```typescript
class Student implements Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    sayHello() {
        console.log(`Hello, I'm ${this.name}.`);
    }
}
```

### 可选属性

接口中的属性可以标记为可选，表示该属性可能存在也可能不存在：

```typescript
interface Car {
    brand: string;
    model: string;
    year?: number; // 可选属性
}
```

### 只读属性

接口中的属性可以标记为只读，表示这些属性只能在创建时被赋值，之后不能被修改：

```typescript
interface Point {
    readonly x: number;
    readonly y: number;
}
```

### 函数类型

接口也可以用于描述函数类型：

```typescript
interface GreetFunction {
    (name: string): string;
}

const greet: GreetFunction = function (name: string): string {
    return `Hello, ${name}!`;
};
```

### 继承接口

一个接口可以继承自另一个接口，从而扩展或组合接口：

```typescript
interface Employee extends Person {
    jobTitle: string;
}

const employee: Employee = {
    name: "John",
    age: 30,
    jobTitle: "Developer",
    sayHello() {
        console.log(`Hello, I'm ${this.name}, a ${this.jobTitle}.`);
    }
};
```

接口在 TypeScript 中用于创建更具表现力和可读性的代码，以确保对象符合特定的约定。接口的使用可以提高代码的可维护性和可拓展性。





# Generics

## 一.泛型类

在 TypeScript 中，你可以创建泛型类，这允许你在类中使用泛型类型参数，以增加类的灵活性。泛型类在类的定义中使用一到多个类型参数，这些类型参数可以在类中的属性、方法、构造函数等地方使用。

以下是一个简单的泛型类的示例：

```typescript
class Box<T> {
  private content: T;

  constructor(content: T) {
    this.content = content;
  }

  getContent(): T {
    return this.content;
  }
}

// 使用泛型类创建不同类型的盒子
let numberBox = new Box<number>(42);
console.log(numberBox.getContent()); // 输出: 42

let stringBox = new Box<string>("Hello, TypeScript!");
console.log(stringBox.getContent()); // 输出: Hello, TypeScript!
```

在上述例子中，`Box` 是一个泛型类，它有一个类型参数 `T`，表示盒子中的内容的类型。在构造函数和方法中，我们使用了这个泛型类型参数。通过在创建 `Box` 实例时传递不同的类型参数，我们可以创建包含不同类型内容的盒子。

泛型类的使用场景通常是需要在类中操作不同类型的数据，而不希望在每个类的实例上重复定义相似的逻辑。泛型类提供了一种灵活的方式来编写通用的代码，同时保持类型安全。

你也可以在泛型类中使用多个类型参数，以满足更复杂的场景。例如：

```typescript
class Pair<K, V> {
  private key: K;
  private value: V;

  constructor(key: K, value: V) {
    this.key = key;
    this.value = value;
  }

  getKey(): K {
    return this.key;
  }

  getValue(): V {
    return this.value;
  }
}

let numberStringPair = new Pair<number, string>(1, "One");
console.log(numberStringPair.getKey());    // 输出: 1
console.log(numberStringPair.getValue());  // 输出: One
```

## 二.泛型函数

泛型函数是 TypeScript 中支持泛型的一种形式，它允许你在函数定义中使用泛型类型参数，以增加函数的灵活性。通过泛型函数，你可以编写具有通用性的函数，使其能够处理不同类型的数据，同时保持类型安全。

以下是一个简单的泛型函数的示例：

```typescript
// 泛型函数，接受一个参数并返回相同的参数
function identity<T>(arg: T): T {
  return arg;
}

// 使用泛型函数
let result1 = identity<number>(42);         // result1 的类型为 number
let result2 = identity<string>("Hello");    // result2 的类型为 string

console.log(result1);  // 输出: 42
console.log(result2);  // 输出: Hello
```

在上述例子中，`identity` 是一个泛型函数，它使用了类型参数 `T`。这个函数接受一个参数 `arg`，并返回相同的参数。通过在函数名后面使用 `<T>` 来指定泛型类型参数，并在调用时通过 `identity<number>` 或 `identity<string>` 明确指定泛型类型。

你也可以不显式指定泛型类型，而由 TypeScript 的类型推断自动推断出泛型类型：

```typescript
let result3 = identity(true);  // result3 的类型为 boolean
console.log(result3);          // 输出: true
```

在这个例子中，TypeScript 根据传入的参数类型自动推断出泛型类型。

泛型函数的应用场景很广泛，例如，你可以使用泛型来编写通用的数组操作函数、Promise 化的函数、函数式编程的工具函数等。

## 三.泛型接口

在 TypeScript 中，你可以创建泛型接口，使接口能够适应多种类型。泛型接口允许你在接口的定义中使用类型参数，从而使接口更具通用性。

以下是一个简单的泛型接口的示例：

```typescript
// 泛型接口定义
interface Pair<T, U> {
  first: T;
  second: U;
}

// 使用泛型接口
let numberStringPair: Pair<number, string> = { first: 1, second: "Two" };
let booleanNumberPair: Pair<boolean, number> = { first: true, second: 42 };

console.log(numberStringPair); // 输出: { first: 1, second: 'Two' }
console.log(booleanNumberPair); // 输出: { first: true, second: 42 }
```

在这个例子中，`Pair` 是一个泛型接口，它有两个类型参数 `T` 和 `U`，分别代表了 `first` 和 `second` 属性的类型。然后我们使用该泛型接口创建了两个不同类型的 `Pair` 实例。

你还可以使用泛型类型参数在接口方法中定义泛型函数：

```typescript
interface TransformFunction<T, U> {
  (input: T): U;
}

let numberToString: TransformFunction<number, string> = function (num) {
  return num.toString();
};

let upperCaseString: TransformFunction<string, string> = function (str) {
  return str.toUpperCase();
};

console.log(numberToString(42));    // 输出: "42"
console.log(upperCaseString("hello"));  // 输出: "HELLO"
```

在这个例子中，`TransformFunction` 是一个泛型接口，它有两个类型参数 `T` 和 `U`，代表输入和输出的类型。我们使用该泛型接口定义了两个不同类型的转换函数。

泛型接口在编写可复用、通用的代码时非常有用，可以适应多种类型的需求。

## 四.泛型约束

泛型约束是 TypeScript 中一种用于限制泛型类型的技术，它可以帮助你在使用泛型时确保某些属性或方法的存在，以增加类型的安全性。

以下是一个简单的泛型约束示例：

```typescript
// 定义一个带有 length 属性的接口
interface Lengthwise {
  length: number;
}

// 泛型函数，接受一个参数，该参数必须有 length 属性
function logLength<T extends Lengthwise>(arg: T): void {
  console.log(arg.length);
}

// 正确使用，因为数组有 length 属性
logLength([1, 2, 3]);  // 输出: 3

// 正确使用，因为字符串有 length 属性
logLength("Hello");    // 输出: 5

// 错误使用，数字没有 length 属性
// logLength(42);      // 错误，类型“number”的参数不能赋给类型“Lengthwise”的参数。
```

在这个例子中，`Lengthwise` 是一个带有 `length` 属性的接口，然后 `logLength` 函数使用了泛型约束 `T extends Lengthwise`，表示传入的参数必须满足 `Lengthwise` 接口的要求。这样，在函数内部就可以放心地使用 `arg.length`，而 TypeScript 编译器会确保传入的参数具有 `length` 属性。

泛型约束可以用于确保泛型类型符合特定的条件，从而避免在使用泛型时发生潜在的错误。

## 五.扩展泛型类

在 TypeScript 中，你可以通过继承泛型类来扩展它。当你继承一个泛型类时，你可以选择保留或覆盖父类的泛型类型参数，并添加自己的属性、方法等。

以下是一个简单的例子，展示了如何扩展泛型类：

```typescript
// 泛型类
class Box<T> {
  private content: T;

  constructor(content: T) {
    this.content = content;
  }

  getContent(): T {
    return this.content;
  }
}

// 扩展泛型类
class ColoredBox<T, U> extends Box<T> {
  color: U;

  constructor(content: T, color: U) {
    super(content);
    this.color = color;
  }

  displayInfo(): void {
    console.log(`Content: ${this.getContent()}, Color: ${this.color}`);
  }
}

// 创建泛型类的实例
let coloredBox = new ColoredBox<string, number>("Apple", 0xff0000);

// 调用扩展的方法
coloredBox.displayInfo(); // 输出: Content: Apple, Color: 16711680

// 调用父类的方法
let content = coloredBox.getContent();
console.log(content);     // 输出: Apple
```

在这个例子中，`ColoredBox` 类继承自泛型类 `Box<T>`，并添加了一个额外的泛型类型参数 `U` 表示颜色的类型。通过使用 `super(content)` 调用父类的构造函数，我们将传入的内容初始化到父类中。然后，`ColoredBox` 类还添加了一个 `displayInfo` 方法，该方法用于显示内容和颜色的信息。

当你使用继承的方式扩展泛型类时，需要注意子类对泛型参数的处理，以确保在使用时类型匹配。

## 六.keyof类型操作符

`keyof` 是 TypeScript 中的一种类型操作符，它用于获取对象类型的所有键（属性名）的联合类型。这个操作符对于访问对象属性时提供了一些类型安全性，因为它确保你只能访问实际存在于对象上的属性。

具体来说，`keyof` 的语法如下：

```typescript
type KeysOfType = keyof ObjectType;
```

其中，`ObjectType` 是你想要获取键的对象类型。这将返回一个包含该对象类型所有键的联合类型。

例如，考虑以下示例：

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type PersonKeys = keyof Person;

// PersonKeys 的类型是 "name" | "age" | "address"
```

在这个例子中，`PersonKeys` 的类型是字符串联合类型，包含了 `Person` 接口中定义的所有属性名。

`keyof` 主要用于在编译时捕获可能的错误，避免在运行时出现无法预测的属性名访问错误。例如，如果你有一个函数接受对象和对象的键作为参数，你可以使用 `keyof` 来确保传递的键是对象实际上存在的属性：

```typescript
function getProperty(obj: Person, key: keyof Person) {
  return obj[key];
}

const person: Person = { name: "John", age: 25, address: "123 Main St" };

const name: string = getProperty(person, "name"); // 正确
const invalidKey: string = getProperty(person, "invalidKey"); // 编译时错误
```

这样，TypeScript 将在编译时捕获到 `invalidKey` 不是 `Person` 接口中定义的属性，避免了潜在的运行时错误。

## 七.映射类型

在 TypeScript 中，类型映射是一种用于在类型级别对现有类型进行转换的技术。它通过使用映射类型（Mapped Types）来实现，通过迭代现有类型的属性，并对它们进行转换或创建新属性。其中，`keyof` 和 `in` 操作符是关键的组成部分。

以下是一些常见的映射类型：

1. **Readonly<T>：** 创建一个新的类型，使传入的类型 `T` 中的所有属性变为只读。

   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   type ReadonlyPerson = Readonly<Person>;
   // 等价于 { readonly name: string; readonly age: number; }
   ```

2. **Partial<T>：** 创建一个新的类型，使传入的类型 `T` 中的所有属性变为可选。

   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   type PartialPerson = Partial<Person>;
   // 等价于 { name?: string; age?: number; }
   ```

3. **Pick<T, K>：** 从类型 `T` 中选取一组键为 `K` 的属性，创建一个新的类型。

   ```typescript
   interface Person {
     name: string;
     age: number;
     address: string;
   }

   type PersonInfo = Pick<Person, "name" | "age">;
   // 等价于 { name: string; age: number; }
   ```

4. **Record<K, T>：** 创建一个新的类型，该类型具有键为 `K`，值为 `T` 的属性。

   ```typescript
   type PhoneNumbers = Record<string, string>;
   // 等价于 { [key: string]: string; }
   ```

5. **Mapped Types：** 你还可以使用映射类型创建自定义的类型转换。

   ```typescript
   type OptionalProps<T> = { [K in keyof T]?: T[K] };
   // 使传入类型 T 中的所有属性变为可选
   ```

这些映射类型提供了一种强大的方式来操作和转换现有类型，使得你能够更灵活地定义和使用类型。映射类型通常与泛型结合使用，以便在不同的上下文中重复使用。



# 装饰器


装饰器是一种 TypeScript 的扩展功能，它允许你在声明类、方法、属性或参数时附加元数据或修改其行为。装饰器的语法是由 `@expression` 组成，其中 `expression` 求值为一个函数，该函数在运行时被调用，并接收一些元数据。

装饰器主要用于在不修改原始代码的情况下，以声明性的方式扩展或修改类、方法、属性等的行为。它们广泛用于框架和库，如 Angular 和Vue.js。

## 一.类装饰器

类装饰器是一种装饰器，用于修饰类声明。它是一种特殊类型的装饰器，接收一个参数，即类的构造函数。类装饰器的目标是类的构造函数本身。它可以用于修改类的行为、添加元数据，或者在类被实例化或继承时执行一些操作。

以下是一个简单的类装饰器的示例：

```typescript
function classDecorator(constructor: Function) {
  console.log("Class decorator called.");
}

@classDecorator
class Example {
  // 类的逻辑
}
```

在这个例子中，`classDecorator` 是一个简单的类装饰器函数。当 `Example` 类被声明时，装饰器被调用，并且输出 "Class decorator called."。类装饰器可以用于许多不同的用途，例如添加类级别的元数据、修改类的构造函数，或者甚至替换整个类定义。

类装饰器的语法如下：

```typescript
function classDecorator(constructor: Function) {
  // 在构造函数上执行一些操作
}

@classDecorator
class Example {
  // 类的逻辑
}
```

如果类装饰器返回一个新的构造函数，那么它将替代原始类的构造函数。这使得你能够在类被实例化之前或之后执行一些自定义逻辑。

```typescript
function classDecorator(constructor: Function) {
  return class extends constructor {
    newProperty = "new property";
  };
}

const decoratedExample = new Example();
console.log(decoratedExample.newProperty); // 输出 "new property"
```

需要注意，类装饰器的执行顺序是从上到下的，从外到内的。也就是说，如果有多个类装饰器，它们将按照书写的顺序依次执行。

```typescript
function firstDecorator(constructor: Function) {
  console.log("First decorator");
}

function secondDecorator(constructor: Function) {
  console.log("Second decorator");
}

@firstDecorator
@secondDecorator
class Example {
  // 类的逻辑
}
// 输出：
// First decorator
// Second decorator
```

总体而言，类装饰器是 TypeScript 中强大的工具，允许你以声明性的方式修改和扩展类的行为。











# 模块



















# 与 JavaScript 集成

# React  with  TypeScript

# Node and Express with TypeScript











