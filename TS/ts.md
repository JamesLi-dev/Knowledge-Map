<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [我的 TS](#%E6%88%91%E7%9A%84-ts)
  - [常用 TS 知识点](#%E5%B8%B8%E7%94%A8-ts-%E7%9F%A5%E8%AF%86%E7%82%B9)
    - [泛型](#%E6%B3%9B%E5%9E%8B)
    - [Identities 接口](#identities-%E6%8E%A5%E5%8F%A3)
    - [泛型类](#%E6%B3%9B%E5%9E%8B%E7%B1%BB)
    - [泛型约束](#%E6%B3%9B%E5%9E%8B%E7%BA%A6%E6%9D%9F)
    - [泛型参数默认类型](#%E6%B3%9B%E5%9E%8B%E5%8F%82%E6%95%B0%E9%BB%98%E8%AE%A4%E7%B1%BB%E5%9E%8B)
    - [泛型条件类型](#%E6%B3%9B%E5%9E%8B%E6%9D%A1%E4%BB%B6%E7%B1%BB%E5%9E%8B)
    - [泛型工具类型](#%E6%B3%9B%E5%9E%8B%E5%B7%A5%E5%85%B7%E7%B1%BB%E5%9E%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 我的 TS 

> 持续更新中……

> **文章主要包含以下内容：**
>
> - 常用 TS 知识点
> - 

### 常用 TS 知识点

#### 泛型

```typescript
function identity <T>(value: T) : T {
  return value;
}

console.log(identity<number>(1)) // 1
```

首次看到 `<T>` 语法会感到陌生。但这没什么可担心的，就像传递参数一样，我们传递了我们想要用于特定函数调用的类型

![](https://mmbiz.qpic.cn/mmbiz_jpg/jQmwTIFl1V2OIQYkcbC47bzUibZnCtyvAKMoqse9icPvlrWw9JmPg1zFxBwIf8nPCKXyibo3Fe8TITE05hrxOzWxQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

例如上图`<T>`内部的`T`成为类型变量，也就是`type`, 实际上 `T` 可以使用任何有效名称代替。除了`T` 之外，还有一下常见的泛型变量：
* `K（Key）`：表示对象中的键类型；
* `V（Value）`：表示对象中的值类型；
* `E（Element）`：表示元素类型。

其实并不是只能定义一个类型变量，我们可以引入希望定义的任何数量的类型变量。比如我们引入一个新的类型变量 `U`，用于扩展我们定义的 `identity` 函数：

```typescript
function identity <T, U>(value: T, message: U) : T {
  console.log(message);
  return value;
}

console.log(identity<Number, string>(68, "Semlinker"));
```

![](https://mmbiz.qpic.cn/mmbiz_jpg/jQmwTIFl1V2OIQYkcbC47bzUibZnCtyvAKryFACqVIOopKUrJ9Na0LYIxWvg11vBiaPmnaChjx9bgCubiadcmiawrA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

除了为类型变量显式设定值之外，另一种方式是让编译器自动选择这些类型，从而使代码更简洁。我们可以完全省略尖括号，比如：

```typescript
function identity <T, U>(value: T, message: U) : T {
  console.log(message);
  return value;
}

console.log(identity(68, "Semlinker"));
```
对于上述代码，编译器足够聪明，能够知道我们的参数类型，并将它们赋值给 T 和 U，而不需要开发人员显式指定它们。下面我们来看张动图，直观地感受一下类型传递的过程：

![](https://mmbiz.qpic.cn/mmbiz_gif/jQmwTIFl1V2OIQYkcbC47bzUibZnCtyvAiaqr1qesqrV6Z6D6ia2FIdHaMfXfkS3tXlT0jraroXsm2k2MASChhxQw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如上所述，是返回一个变量的函数，如下是返回两个类型的对象或数组的函数：

```typescript
function identity <T, U>(value: T, message: U) : [T, U] {
  return [value, message];
}

或者使用 ES6 剪头函数

const identity<T, U> = (value: T, message: U) : [T, U] => {
  return [value, message];
}

返回对象
const identity<T, U> = (value: T, message: U) : {T, U} => {
  return {value, message};
}
```

#### Identities 接口

```typescript
interface Identities<V, M> {
  value: V,
  message: M
}
```
如上，我们引用了 `V`, `M` 两个类型变量，下面我们将上面的 `Identities` 接口 作为 函数的返回类型：

```typescript
function identity<T, U> (value: T, message: U): Identities<T, U> {
  console.log(value + ": " + typeof (value));
  console.log(message + ": " + typeof (message));
  let identities: Identities<T, U> = {
    value,
    message
  };
  return identities;
}

console.log(identity(68, "Semlinker"));
// 68: number
// Semlinker: string
// {value: 68, message: "Semlinker"}
```

#### 泛型类

这个我们只需在类名后使用 `<T, ...>` 这样的语法来定义任意多个类型变量，如下：

```typescript
interface GenericInterface<U> {
  value: U
  getIdentity: () => U
}

class IdentityClass<T> implements GenericInterface<T> {
  value: T

  constructor(value: T) {
    this.value = value
  }

  getIdentity(): T {
    return this.value
  }
}

const numberClass = new IdentityClass<number>(68);
console.log(numberClass.getIdentity()); // 68

const stringClass = new IdentityClass<string>("Semlinker!");
console.log(stringClass.getIdentity()); // Semlinker!
```

解读下上面的代码，如下：
* 在实例化 `IdentityClass` 对象时，我们传入 `number` 类型和构造函数参数值 68；
* 之后在 `IdentityClass` 类中，类型变量 `T` 的值变成 `number` 类型；
* `IdentityClass` 类实现了 `GenericInterface<T>`，而此时 `T` 表示 `number` 类型，因此等价于该类实现了 `GenericInterface<number>` 接口；
* 而对于 `GenericInterface<U>` 接口来说，类型变量 `U` 也变成了 `number`。这里我有意使用不同的变量名，以表明类型值沿链向上传播，且与变量名 `U` 和 `T` 无关。

使用场景：
* 当你的函数、接口或类 需要处理 `多种数据类型` 时；
* 当函数、接口或类在 `多个地方使用该数据类型` 时。


#### 泛型约束

泛型约束的作用: 当我们希望限制每个类型变量接受的类型数量，就需要用到泛型约束了。

先看一个例子：

```typescript
function identity<T>(arg: T): T {
  // Property 'length' does not exist on type 'T'.(2339)
  console.log(arg.length); // Error
  return arg;
}
```
上面这个例子，是想用到 `length` 这个属性的时候，这种情况，编译器没法确认 `T` 类型一定包含 `length` 属性，所以，我们需要做的就是使变量类型 `extends` 一个包含我们所需属性的接口，如下：

```typescript
interface Length {
  length: number;
}
// T extends Length : 告诉编译器 T 包含 length:number 属性
function identity<T extends Length>(arg: T): T {
  console.log(arg.length); // 可以获取length属性
  return arg;
}
```

需要注意的是，当我们使用不含有 `length` 的属性对象作为参数调用这个函数时，TS 会提示错误：

```typescript
identity(68); // Error
// Argument of type '68' is not assignable to parameter of type 'Length'.(2345)
```

还有一种方式，我们可以将变俩ing设置为数组类型，也可以解决该问题，如下：

```typescript
function identity<T>(arg: T[]): T[] {
  console.log(arg.length);  
  return arg; 
}
```

此外 ，我们还可以使用 `,` 来  分割多重约束类型，例： `<T extends Length, Type2, Type3>` 。


泛型约束的另一个常见的使用场景就是检查对象上的键是否存在。这就涉及到 `keyof` 操作符，该操作符可以用于获取某种类型的所有键，其返回类型是联合类型。 如下：

```typescript
interface Person {
  name: string;
  age: number;
  location: string;
}

type K1 = keyof Person; // "name" | "age" | "location"
type K2 = keyof Person[];  // number | "length" | "push" | "concat" | ...
type K3 = keyof { [x: string]: Person };  // string | number
```

通过 `keyof` 操作符，我们就可以获取指定类型的所有键，之后我们就可以结合前面介绍的 `extends` 约束，即限制输入的属性名包含在 `keyof` 返回的联合类型中。具体的使用方式如下：

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```
在以上的 `getProperty` 函数中，我们通过 `K extends keyof T` 确保参数 `key` 一定是对象中含有的键，这样就不会出现运行时错误。这是一个类型安全的解决方案，与简单调用 `let value = obj[key];` 是不同的。

具体使用如下：

```typescript
enum Difficulty {
  Easy,
  Intermediate,
  Hard
}

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

let tsInfo = {
   name: "Typescript",
   supersetOf: "Javascript",
   difficulty: Difficulty.Intermediate
}
 
let difficulty: Difficulty = 
  getProperty(tsInfo, 'difficulty'); // OK

let supersetOf: string = 
  getProperty(tsInfo, 'superset_of'); // Error
```

在以上示例中，对于 getProperty(tsInfo, 'superset_of') 这个表达式，TypeScript 编译器会提示以下错误信息：

```typescript
Argument of type '"superset_of"' is not assignable to parameter of type '"difficulty" | "name" | "supersetOf"'.
```

#### 泛型参数默认类型

直接上代码：

```typescript
interface Person<T=string> {
  id: T;
}

const p0: Person = { id: "lolo" };
const p1: Person<number> = { id: 28 };
```
泛型参数默认类型与普通函数默认值类似，对应的语法很简单，即 `<T=Default Type>`。

泛型参数的默认类型遵循以下规则：
- 有默认类型的类型参数被认为是可选的。
- 必选的类型参数不能在可选的类型参数后。
- 如果类型参数有约束，类型参数的默认类型必须满足这个约束。
- 当指定类型实参时，你只需要指定必选类型参数的类型实参。未指定的类型参数会被解析为它们的默认类型。
- 如果指定了默认类型，且类型推断无法选择一个候选类型，那么将使用默认类型作为推断结果。
- 一个被现有类或接口合并的类或者接口的声明可以为现有类型参数引入默认类型。
- 一个被现有类或接口合并的类或者接口的声明可以引入新的类型参数，只要它指定了默认类型。

#### 泛型条件类型

条件类型会以一个条件表达式进行类型关系检测，从而在两种类型中选择其一：
```typescript
T extends U ? X : Y
```
以上表达式的意思是：若 `T` 能够赋值给 `U`，那么类型是 `X`，否则为 `Y`。在条件类型表达式中，我们通常还会结合 `infer` 关键字，实现类型抽取：

```typescript
interface Dictionary<T = any> {
  [key: string]: T;
}
 
type StrDict = Dictionary<string>

type DictMember<T> = T extends Dictionary<infer V> ? V : never
type StrDictMember = DictMember<StrDict> // string
```

在上面示例中，当类型 `T` 满足 `T extends Dictionary` 约束时，我们会使用 `infer` 关键字声明了一个类型变量 `V`，并返回该类型，否则返回 `never` 类型。

> 在 TypeScript 中，never 类型表示的是那些永不存在的值的类型。例如， never 类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型。
另外，需要注意的是，没有类型是 never 的子类型或可以赋值给 never 类型（除了 never 本身之外）。即使 any 也不可以赋值给 never。

条件类型还有一个特性：

>分布式条件类型。当检测的类型是由 ”裸类型“（指该类型未被包装过） 组成的联合类型时，条件类型会被自动分发成联合类型。以 `T extends U ? X : Y` 条件类型为例，当类型参数的为 `A | B | C` 时，该条件类型将会被解析为 `(A extends U ? X : Y) | (B extends U ? X : Y) | (C extends U ? X : Y)`。 示例如下：

```typescript
type TypeName<T> = T extends string
  ? "string"
  : T extends number
  ? "number"
  : T extends boolean
  ? "boolean"
  : T extends undefined
  ? "undefined"
  : T extends Function
  ? "function"
  : "object";

type T10 = TypeName<string | (() => void)>; // "string" | "function"
type T12 = TypeName<string | string[] | undefined>; // "string" | "object" | "undefined"
type T11 = TypeName<string[] | number[]>; // "object"
```

#### 泛型工具类型

为了方便开发者 TypeScript 内置了一些常用的工具类型，比如 Partial、Required、Readonly、Record 和 ReturnType 等。出于篇幅考虑，这里我们只简单介绍其中几个常用的工具类型。

1、`Partial` 
`Partial<T>` 的作用就是将某个类型里的属性全部变为可选项 `?`。

```typescript
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```
`Partial` 类型被称为映射类型，用于把已有的类型转换成新的类型。在以上代码中，我们首先通过 `keyof T` 拿到 `T` 的所有属性名，然后使用 `in` 进行遍历，将值赋给类型变量 `P`，最后通过 `T[P]` 取得属性 `P` 对应的类型。中间的 `?` 号，表示将属性变为可选。例：

```typescript
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
  title: "Learn TS",
  description: "Learn TypeScript"
};

const todo2 = updateTodo(todo1, {
  description: "Learn TypeScript Handbook"
});

// 我们利用 Partial<T> 工具类型，定义 fieldsToUpdate 的类型为 Partial<Todo>
// {
//    title?: string | undefined;
//    description?: string | undefined;
// }

type Foo = {
 a: number;
 b?: string;
 c: boolean;
}

// 测试用例 支持把给定的 keys 对应的属性变成可选的 'a' | 'b'
type SomeOptional = SetOptional<Foo, 'a' | 'b'>;
// 
// type SomeOptional = {
//  a?: number; // 该属性已变成可选的
//  b?: string; // 保持不变
//  c: boolean; 
// }
```


2、`Record`

`Record<K extends keyof any, T>` 的作用是将 `K` 中所有的属性的值转化为 `T` 类型。

```typescript
type Record<K extends keyof any, T> = {
  [P in K]: T;
};

// 例：
interface PageInfo {
  title: string;
}

type Page = "home" | "about" | "contact";

const x: Record<Page, PageInfo> = {
  about: { title: "about" },
  contact: { title: "contact" },
  home: { title: "home" }
};
```

3、`Pick`

`Pick<T, K extends keyof T>` 的作用是将某个类型中的子属性挑出来，变成包含这个类型部分属性的子类型。

```typescript
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
  title: "Learn TS",
  completed: false,  // 如果值不是boolean 那编辑器会提示错误
};
```
<!-- 
如何定义一个 ConditionalPick 工具类型，支持根据指定的 Condition 条件来生成新的类型，对应的使用示例如下：

```typescript
interface Example {
 a: string;
 b: string | number;
 c: () => void;
 d: {};
}

// 测试用例：
type StringKeysOnly = ConditionalPick<Example, string>;
//=> { a: string }
``` -->

4、`Exclude`

`Exclude<T, U>` 的作用是将某个类型中属于另一个的类型移除掉。

```typescript
type Exclude<T, U> = T extends U ? never : T;
```

如果 `T` 能赋值给 `U` 类型的话，那么就会返回 `never` 类型，否则返回 `T` 类型。最终实现的效果就是将 `T` 中某些属于 `U` 的类型移除掉。

```typescript
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">; // "c"
type T2 = Exclude<string | number | (() => void), Function>; // string | number
```
由以上结果可知，Exclude 工具类型利用了前面介绍的分布式条件类型的特性。

5、`ReturnType`

`ReturnType<T>` 的作用是用于获取函数 `T` 的返回类型。

```typescript
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;

type T0 = ReturnType<() => string>; // string
type T1 = ReturnType<(s: string) => void>; // void
type T2 = ReturnType<<T>() => T>; // {}
type T3 = ReturnType<<T extends U, U extends number[]>() => T>; // number[]
type T4 = ReturnType<any>; // any
type T5 = ReturnType<never>; // any
type T6 = ReturnType<string>; // Error
type T7 = ReturnType<Function>; // Error
```