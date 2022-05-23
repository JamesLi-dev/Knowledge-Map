<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [我的 TS](#%E6%88%91%E7%9A%84-ts)
  - [常用 TS 知识点](#%E5%B8%B8%E7%94%A8-ts-%E7%9F%A5%E8%AF%86%E7%82%B9)
    - [1、泛型](#1%E6%B3%9B%E5%9E%8B)
    - [Identities 接口](#identities-%E6%8E%A5%E5%8F%A3)
    - [泛型类](#%E6%B3%9B%E5%9E%8B%E7%B1%BB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<!--
 * @Author: liboya
 * @Date: 2022-05-19 15:33:11
 * @LastEditors: 李博雅 1273319367@qq.com
 * @LastEditTime: 2022-05-23 21:44:41
 * @FilePath: /Knowledge-Map/TS/ts.md
 * @Description: 
 * 
 * Copyright (c) 2022 by 李博雅 1273319367@qq.com, All Rights Reserved. 
-->
## 我的 TS 

> 持续更新中……

> **文章主要包含以下内容：**
>
> - 常用 TS 知识点
> - 

### 常用 TS 知识点

#### 1、泛型

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