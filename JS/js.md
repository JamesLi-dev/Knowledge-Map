## JS

> 持续更新中……

> **文章主要包含以下内容：**
>
> - 数组常用方法
> - 字符串常用方法
> - 常用遍历方法&高阶函数
> - 常用正则表达式
> - 数学知识
> - JS 小技巧
> - 常用方法封装

### 一、数组常用方法

#### 1.push()

在尾部追加，类似于压栈，原数组会变。

```js
const arr = [1, 2, 3];
arr.push(8);
console.log(arr); // [1, 2, 3, 8]
```

#### 2.pop()

在尾部弹出，类似于出栈，原数组会变。数组的 `push` & `pop` 可以模拟常见数据结构之一：栈。

```js
const arr = [1, 2, 3];
const popVal = arr.pop();
console.log(popVal); // 3
console.log(arr); // [1, 2]

// 数组模拟常见数据结构之一：栈
const stack = [0, 1];
stack.push(2); // 压栈
console.log(stack); // [0, 1, 2]

const popValue = stack.pop(); // 出栈
console.log(popValue); // 2
console.log(stack); // [0, 1]
```

#### 3.unshift()

在头部压入数据，类似于入队，原数组会变。

```js
const arr = [1, 2, 3];
arr.unshift(0);
console.log(arr); // [0, 1, 2, 3]
```

#### 4.shift()

在头部弹出数据，原数组会变。数组的 `push`（入队） & `shift`（出队） 可以模拟常见数据结构之一：队列。

```js
const arr = [1, 2, 3];
const shiftVal = arr.shift();
console.log(shiftVal); // 1
console.log(arr); // [2, 3]

// 数组模拟常见数据结构之一：队列
const queue = [0, 1];
queue.push(2); // 入队
console.log(queue); // [0, 1, 2]

const shiftValue = queue.shift(); // 出队
console.log(shiftValue); // 0
console.log(queue); // [1, 2]
```

#### 5.concat()

`concat`会在当前数组尾部拼接传入的数组，然后返回一个新数组，原数组不变。

```js
const arr = [1, 2, 3];
const arr2 = arr.concat([7, 8, 9]);
console.log(arr); // [1, 2, 3]
console.log(arr2); // [1, 2, 3, 7, 8, 9]
```

#### 6.indexOf()

在数组中寻找该值，找到则返回其下标，找不到则返回`-1`。

```js
const arr = [1, 2, 3];
console.log(arr.indexOf(2)); // 1
console.log(arr.indexOf(0)); // -1
```

#### 7.includes()

在数组中寻找该值，找到则返回`true`，找不到则返回`false`。

```js
const arr = [1, 2, 3];
console.log(arr.includes(2)); // true
console.log(arr.includes(4)); // false
```

#### 8.join()

将数组转化成字符串，并返回该字符串，不传值则默认逗号隔开，原数组不变。

```js
const arr = [1, 2, 3];
console.log(arr.join()); // ‘1, 2, 3’
console.log(arr); // [1, 2, 3]
```

#### 9.reverse()

翻转原数组，并返回已完成翻转的数组，原数组改变。

```js
const arr = [1, 2, 3];
console.log(arr.reverse()); // [3, 2, 1]
console.log(arr); // [3, 2, 1]
```

#### 10.slice(start，end)

从`start` 开始截取到`end`，但是不包括`end`

```js
const arr = [1, 2, 3, 4, 5];
console.log(arr.slice(1, 4)); // [2, 3, 4]
console.log(arr); // [1, 2, 3, 4, 5]
```

#### 11.splice(start, deleteCount, item1, item2……)

- `start`参数 开始的位置
- `deleteCount`要截取的个数
- 后面的`items`为要添加的元素
- 如果`deleteCount`为`0`，则表示不删除元素，从`start`位置开始添加后面的几个元素到原始的数组里面。
- 返回值为由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
- 这个方法会改变原始数组，数组的长度会发生变化

```js
const arr3 = [1, 2, 3, 4, 5, 6, 7, "f1", "f2"];
const arr4 = arr3.splice(2, 3); // 删除第三个元素以后的三个数组元素(包含第三个元素)
console.log(arr4); // [3, 4, 5];
console.log(arr3); // [1, 2, 6, 7, "f1", "f2"]; 原始数组被改变

const arr5 = arr3.splice(2, 0, "wu", "leon");
// 从第2位开始删除0个元素，插入"wu","leon"
console.log(arr5); // [] 返回空数组
console.log(arr3); // [1, 2, "wu", "leon", 6, 7, "f1", "f2"]; 原始数组被改变

const arr6 = arr3.splice(2, 3, "xiao", "long");
// 从第 2 位开始删除 3 个元素，插入"xiao", "long"
console.log(arr6); // ["wu", "leon", 6]
console.log(arr3); //[ 1, 2, "xiao", "long", 7, "f1", "f2"]

const arr7 = arr3.splice(2); // 从第三个元素开始删除所有的元素
console.log(arr7); // ["xiao", "long", 7, "f1", "f2"]
console.log(arr3); // [1, 2]
```

#### 12.sort()

- 对数组的元素进行排序，并返回数组。
- 默认排序顺序是在将元素转换为字符串，然后比较它们的`UTF-16`代码单元值序列时构建的。
- 由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。

```js
const arr = [1, 2, 3];
arr.sort((a, b) => b - a);
console.log(arr); // [3, 2, 1]
```

#### 13.toString()

将数组转化成字符串，并返回该字符串，逗号隔开，原数组不变。

```js
const arr = [1, 2, 3, 4, 5];
console.log(arr.toString()); // ‘1, 2, 3, 4, 5’
console.log(arr); // [1, 2, 3, 4, 5]
```

### 二、字符串常用方法

#### 1.charAt()

返回指定索引位置处的字符。类似于数组用中括号获取相应下标位置的数据。

```js
var str = "abcdefg";
console.log(str.charAt(2)); // 输出 'c'
console.log(str[2]); // 输出 'c'
```

#### 2.concat()

类似数组的 concat()，用来返回一个合并拼接两个或两个以上字符串。原字符串不变。

```js
const str1 = "abcdefg";
const str2 = "1234567";
const str3 = str1.concat(str2);
console.log(str3); // 输出 'abcdefg1234567'
```

#### 3.indexOf()、lastIndexOf()

`indexOf`,返回一个字符在字符串中首次出现的位置,`lastIndexOf`返回一个字符在字符串中最后一次出现的位置。

```js
const str = "abcdcefcg";
console.log(str.indexOf("c")); // 输出 '2'
console.log(str.lastIndexOf("c")); // 输出 '7'
```

#### 4.slice()

提取字符串的片断，并把提取的字符串作为新的字符串返回出来。原字符串不变。

```js
const str = "abcdefg";
console.log(str.slice()); // 输出 'abcdefg', 不传递参数默认复制整个字符串
console.log(str.slice(1)); // 输出 'bcdefg',传递一个，则为提取的起点，然后到字符串结尾
console.log(str.slice(2, str.length - 1)); // 输出'cdef',传递两个，为提取的起始点和结束点
```

#### 5.split()

使用指定的分隔符将一个字符串拆分为多个子字符串数组并返回，原字符串不变。

```js
const str = "A*B*C*D*E*F*G";
console.log(str.split("*")); // 输出 ["A", "B", "C", "D", "E", "F", "G"]
```

#### 6.substr(), substring()

- 这两个方法的功能都是截取一个字符串的片段，并返回截取的字符串。
- `substr`和`substring`这两个方法不同的地方就在于参数二，`substr`的参数二是截取返回出来的这个字符串指定的长度，`substring`的参数二是截取返回这个字符串的结束点，并且不包含这个结束点。而它们的参数一，都是一样的功能，截取的起始位置。
- **注意事项**：`substr`的参数二如果为`0`或者负数，则返回一个空字符串，如果未填入，则会截取到字符串的结尾去。`substring`的参数一和参数二为`NAN`或者负数，那么它将被替换为`0`。

```js
const str = "ABCDEFGHIJKLMN";
console.log(str.substr(2)); // 输出 'CDEFGHIJKLMN'
console.log(str.substring(2)); // 输出 'CDEFGHIJKLMN'

console.log(str.substr(2, 9)); // 输出 'CDEFGHIJK'
console.log(str.substring(2, 9)); // 输出 'CDEFGHI'
```

#### 7.match()

`match()`方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配，并返回一个包含该搜索结果的数组。

```js
const str = "2018年结束了，2019年开始了，2020年就也不远了";
const reg = /\d+/g; // 这里是定义匹配规则，匹配字符串里的1到多个数字
console.log(str.match(reg)); // 输出符合匹配规则的内容，以数组形式返回 ['2018', '2019', '2020']
console.log(str.match("20")); // 不使用正则 ["20", index: 0, input: "2018年结束了，2019年开始了"]
```

**注意事项**:如果`match`方法没有找到匹配，将返回`null`。如果找到匹配，则 `match`方法会把匹配到以数组形式返回，如果正则规则未设置全局修饰符`g`，则 `match`方法返回的数组有两个特性：`input`和`index`。`input`属性包含整个被搜索的字符串。`index`属性包含了在整个被搜索字符串中匹配的子字符串的位置。

#### 8.replace()

`replace`接收两个参数，参数一是需要替换掉的字符或者一个正则的匹配规则，参数二，需要替换进去的字符，仔实际的原理当中，参数二，你可以换成一个回调函数。

```js
const str = "2018年结束了，2019年开始了，2020年就也不远了";
const rex = /\d+/g; // 这里是定义匹配规则，匹配字符串里的1到多个数字
const str1 = str.replace(rex, "****");
console.log(str1); // 输出："****年结束了，****年开始了,****年也不远了"
const str2 = str.replace(rex, function (item) {
  console.log(arguments); // 看下面的图片
  const arr = ["零", "壹", "贰", "叁", "肆", "伍", "陆", "柒", "捌", "玖"];
  let newStr = "";
  item.split("").map(function (i) {
    newStr += arr[i];
  });
  return newStr;
});
console.log(str2); // 输出：贰零壹捌年结束了，贰零壹玖年开始了,贰零贰零年也不远了
```

#### 9.search()

在目标字符串中搜索与正则规则相匹配的字符，搜索到，则返回第一个匹配项在目标字符串当中的位置，没有搜索到则返回一个`-1`。

```js
const str = "2018年结束了，2019年开始了，2020年就也不远了";
const reg = /\d+/i; // 这里是定义匹配规则,匹配字符串里的1到多个数字
console.log(str.search(reg)); // 输出 0  这里搜索到的第一项是从位置0开始的
```

#### 10.toLowerCase(),toUpperCase()

`toLowerCase`把字母转换成小写，`toUpperCase()`则是把字母转换成大写。

```js
const str1 = "abcdefg";
const str2 = "ABCDEFG";
console.log(str2.toLowerCase()); // 输出：'abcdefg'
console.log(str1.toUpperCase()); // 输出：'ABCDEFG'
```

#### 11.includes(), startsWith(), endsWith()

`includes`、`startsWith`、`endsWith`，`es6`的新增方法，`includes` 用来检测目标字符串对象是否包含某个字符，返回一个布尔值，`startsWith`用来检测当前字符是否是目标字符串的起始部分，相对的`endwith`是用来检测是否是目标字符串的结尾部分。

```js
const str = "Excuse me, how do I get to park road?";
console.log(str.includes("how")); // 输出：true
console.log(str.startsWith("Excuse")); // 输出：true
console.log(str.endsWith("?")); // 输出：true
```

#### 12.repeat()

返回一个新的字符串对象，新字符串等于重复了指定次数的原始字符串。接收一个参数，就是指定重复的次数。原字符串不变。

```js
const str = "http";
const str2 = str.repeat(3);
console.log(str); // 输出：'http'
console.log(str2); // 输出：'httphttphttp'
```

### 三、常用遍历方法&高阶函数

#### 1.for()

最常用的`for`循环，经常用的数组遍历，也可以遍历字符串。

```js
const arr = [1, 2, 3];
const str = "abc";
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
  console.log(str[i]);
}
```

#### 2.while() / do while()

`while`、`do while`主要的功能是，当满足`while`后边所跟的条件时，来执行相关业务。这两个的区别是，`while`会先判断是否满足条件，然后再去执行花括号里面的任务，而`do while`则是先执行一次花括号中的任务，再去执行`while`条件，判断下次还是否再去执行`do`里面的操作。也就是说 `**do while**`**至少会执行一次操作**.

```js
while(条件){
     执行...
}
------------
do{
    执行...
}
while(条件)

```

#### 3.forEach()

拷贝一份遍历原数组。

- `return`无法终止循环。不过可以起到`continue`效果。
- 本身是不支持的`continue`与`break`语句的我们可以通过`some`和 `every`来实现。

```js
const arr = [5, 1, 3, 7, 4];
arr.forEach((item, index) => {
  if (item < 2) return;
  console.log(`索引：${index}，数值：${item}`);
  arr[5] = 0;
});
console.log(arr);
// 打印结果：
// 索引：0，数值：5
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [5, 1, 3, 7, 4, 0]
```

#### 4.for...in

- `for...in` 是 ES5 标准， 此方法遍历数组效率低，主要是用来循环遍历对象的属性。
- 遍历数组的缺点：数组的下标`index`值是数字，`for-in`遍历的`index`值`"0","1","2"`等是字符串。
- `Object.defineProperty`，建立的属性，默认不可枚举。

```js
const foo = {
  name: "bar",
  sex: "male",
};
Object.defineProperty(foo, "age", { value: 18 });
for (const key in foo) {
  console.log(`可枚举属性：${key}`);
}
console.log(`age属性：${foo.age}`);
// 打印结果：
// 可枚举属性：name
// 可枚举属性：sex
// age属性：18
```

#### 5.for...of

`for…of`是`ES6`新增的方法，但是`for…of`不能去遍历普通的对象，`**for…of**`**的好处是可以使用**`**break**`**跳出循环。**

- `for-of`这个方法避开了`for-in`循环的所有缺陷
- 与`forEach()`不同的是，它可以正确响应`break`、`continue`和`return`语句
- `for-of`循环不仅支持数组，还支持大多数类数组对象，例如`DOM` **NodeList 对象**[6]。
- - `for-of`循环也支持字符串遍历

```js
// for of 循环直接得到的就是值
const arr = [1, 2, 3];
for (const value of arr) {
  console.log(value);
}
```

**面试官：说一下 **`**for...in**`** 和 **`**for...of**`** 区别？**

```js
（1）for…in 用于可枚举数据，如对象、数组、字符串
（2）for…of 用于可迭代数据，如数组、字符串、Map、Set

```

#### 6.every / some

**返回一个布尔值**。当我们需要判定数组中的元素是否满足某些条件时，可以使用`every` / `some`。这两个的区别是，`every`会去判断判断数组中的每一项，而 `some`则是当某一项满足条件时返回。

```js
// every
const foo = [5, 1, 3, 7, 4].every((item, index) => {
  console.log(`索引：${index}，数值：${item}`);
  return item > 2;
});
console.log(foo);
// every 打印：
// 索引：0，数值：5
// 索引：1，数值：1
// false

// some
const foo = [5, 1, 3, 7, 4].some((item, index) => {
  console.log(`索引：${index}，数值：${item}`);
  return item > 2;
});
console.log(foo);
// some 打印：
// 索引：0，数值：5
// true
```

#### 7.filter()

- `filter`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。
- 它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。
- 该方法不会改变原数组。

```js
const foo = [5, 1, 3, 7, 4].filter((item, index) => {
  console.log(`索引：${index}，数值：${item}`);
  return item > 2;
});
console.log(foo);
// 打印结果：
// 索引：0，数值：5
// 索引：1，数值：1
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [5, 3, 7, 4]
```

#### 8.map()

- `map`即是 “映射”的意思 ，原数组被“映射”成对应新数组。
- `map：`支持`return`，相当与原数组克隆了一份，把克隆的每项改变了，也不影响原数组。

```js
const foo = [5, 1, 3, 7, 4].map((item, index) => {
  console.log(`索引：${index}，数值：${item}`);
  return item + 2;
});
console.log(foo);
// 打印结果：
// 索引：0，数值：5
// 索引：1，数值：1
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [7, 3, 5, 9, 6]
```

#### 9. reduce() / reduceRight()

`reduce` 从左到右将数组元素做“叠加”处理，返回一个值。`reduceRight` 从右到左。

```js
const foo = [5, 1, 3, 7, 4].reduce((total, cur) => {
  console.log(`叠加：${total}，当前：${cur}`);
  return total + cur;
});
console.log(foo);
// 打印结果：
// 叠加：5，当前：1
// 叠加：6，当前：3
// 叠加：9，当前：7
// 叠加：16，当前：4
// 20
```

#### 10.Object,keys 遍历对象的属性

`Object.keys`方法的参数是一个对象，返回一个数组。该数组的成员都是该对象自身的（而不是继承的）所有属性名，且只返回可枚举的属性。

```js
const obj = {
  p1: 123,
  p2: 456,
};
Object.keys(obj); // ["p1", "p2"]
```

#### 11.Object.getOwnPropertyNames() 遍历对象的属性

`Object.getOwnPropertyNames`方法与`Object.keys`类似，也是接受一个对象作为参数，返回一个数组，包含了该对象自身的所有属性名。但它能返回不可枚举的属性。

```js
const arr = ["Hello", "World"];
Object.keys(arr); // ["0", "1"]
Object.getOwnPropertyNames(arr); // ["0", "1", "length"]
```

#### 以上遍历方法的区别：

```js
一：map()，forEach()，filter()循环的共同之处：
  1.forEach，map，filter循环中途是无法停止的，总是会将所有成员遍历完。
  2.他们都可以接受第二个参数，用来绑定回调函数内部的 this 变量，将回调函数内部的 this 对象，指向第二个参数，间接操作这个参数（一般是数组）。

二：map()、filter()循环和forEach()循环的不同：
   forEach 循环没有返回值；map，filter 循环有返回值。

三：map()和filter()都会跳过空位，for 和 while 不会

四：some()和every():
   some()只要有一个是true，便返回true；而every()只要有一个是false，便返回false.

五：reduce()，reduceRight()：
   reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员）。

六：Object对象的两个遍历 Object.keys 与 Object.getOwnPropertyNames：
   他们都是遍历对象的属性，也是接受一个对象作为参数，返回一个数组，包含了该对象自身的所有属性名。但Object.keys不能返回不可枚举的属性；Object.getOwnPropertyNames能返回不可枚举的属性。

```

### 四、常用正则表达式

这里罗列一些我在刷算法题中遇到的正则表达式，如果有时间可认真学一下**正则表达式不要背**[7]。

#### 1.判断字符

```js
由26个英文字母组成的字符串：^[A-Za-z]+$
由26个大写英文字母组成的字符串：^[A-Z]+$
由26个小写英文字母组成的字符串：^[a-z]+$
由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$

```

#### 2.判断数字

```js
数字：^[0-9]*$

```

持续更新，敬请期待……

### 五、数学知识

#### 1.质数

若一个正整数无法被除了`1` 和它自身之外的任何自然数整除，则称该数为质数（或素数），否则称该正整数为合数。

```js
function judgePrime(n) {
  for (let i = 2; i * i <= n; i++) {
    if (n % i == 0) return false;
  }
  return true;
}
```

#### 2.斐波那契数列

```js
function Fibonacci(n) {
  if (n <= 1) return n;
  return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

### 六、JS 小技巧

#### 1、用??代替||，用于判断运算符左侧的值为 null 或 undefined 时，才返回右侧的值

> ??运算符是 ES2020 引入，也被称为 null 判断运算符( Nullish coalescing operator)  
> 它的行为类似||，但是更严

> ||运算符是左边是空字符串或 false 或 0 等 falsy 值，都会返回后侧的值。而??必须运算符左侧的值为 null 或 undefined 时，才会返回右侧的值。因此 0||1 的结果为 1，0??1 的结果为 0

```js
const response = {
  settings: {
    nullValue: null,
    height: 400,
    animationDuration: 0,
    headerText: "",
    showSplashScreen: false,
  },
};

const undefinedValue = response.settings.undefinedValue ?? "some other default"; // result: 'some other default'
const nullValue = response.settings.nullValue ?? "some other default"; // result: 'some other default'
const headerText = response.settings.headerText ?? "Hello, world!"; // result: ''
const animationDuration = response.settings.animationDuration ?? 300; // result: 0
const showSplashScreen = response.settings.showSplashScreen ?? true; // result: false
```

#### 2、使用?.简化&&和三元运算符

> ?.也是 ES2020 引入，有人称为链判断运算符（optional chaining operator）  
> ?.直接在链式调用的时候判断，判断左侧的对象是否为 null 或 undefined，如果是的，就不再往下运算，返回 undefined，如果不是，则返回右侧的值

```js
let street = user.address && user.address.street;

let fooInput = myForm.querySelector("input[name=foo]");
let fooValue = fooInput ? fooInput.value : undefined;

// 简化
let street = user.address?.street;
let fooValue = myForm.querySelector("input[name=foo]")?.value;
```

> 注：常见写法  
> obj?.prop 对象属性  
> obj?.[expr] 对象属性  
> func?.(...args) 函数或对象方法的调用

#### 3、使用 String.prototype.replaceAll()简化 replace 一次性替换所有子字符串

> String.prototype.replaceAll()用法与 String.prototype.replace()类似  
> 但是 replace 仅替换第一次出现的子字符串，而 replaceAll 会替换所有

例如需要替换所有 a 为 A：

```js
// 以前
console.log("aaa".replace(/a/g, "A")); //AAA
// 简化后
console.log("aaa".replaceAll("a", "A")); //AAA
```

#### 4、使用 Array.prototype.at()简化 arr.length

> Array.prototype.at()接收一个正整数或者负整数作为参数，表示获取指定位置的成员
> 参数正数就表示顺数第几个，负数表示倒数第几个，这可以很方便的某个数组末尾的元素

```js
let arr = [1, 2, 3, 4, 5];
// 以前获取最后一位
console.log(arr[arr.length - 1]); //5
// 简化后
console.log(arr.at(-1)); // 5
```

#### 5、使用哈希前缀#将类字段设为私有

> 在类中通过哈希前缀#标记的字段都将被私有，子类实例将无法继承

```js
class ClassWithPrivateField {
  #privateField;
  #privateMethod() {
    return "hello world";
  }
  constructor() {
    this.#privateField = 42;
  }
}

const instance = new ClassWithPrivateField();
console.log(instance.privateField); //undefined
console.log(instance.privateMethod); //undefined
```

#### 6、冻结对象

```js
const oc = { key: 8, color: '#000' }；
Object.freeze(oc);

oc.key = 10; // Error, 不会改变
connsole.log(oc); // { key: 8, color: '#000' }

```

### 七、常用方法封装

> 注：以下是一些常用方法封装，以备不时之需，当然 也可以直接使用 lodash，moment，dayjs 等等这种现成的包实现

#### 1、输入一个值，返回其数据类型

```js
function type(para) {
  return Object.prototype.toString.call(para);
}
```

#### 2、数组去重

```js
function unique1(arr) {
  return [...new Set(arr)];
}

function unique2(arr) {
  var obj = {};
  return arr.filter((ele) => {
    if (!obj[ele]) {
      obj[ele] = true;
      return true;
    }
  });
}

function unique3(arr) {
  var result = [];
  arr.forEach((ele) => {
    if (result.indexOf(ele) == -1) {
      result.push(ele);
    }
  });
  return result;
}
```

#### 3、字符串去重

```js
String.prototype.unique = function () {
  var obj = {},
    str = "",
    len = this.length;
  for (var i = 0; i < len; i++) {
    if (!obj[this[i]]) {
      str += this[i];
      obj[this[i]] = true;
    }
  }
  return str;
};

//去除连续的字符串
function uniq(str) {
  return str.replace(/(\w)\1+/g, "$1");
}
```

#### 4、深拷贝 浅拷贝

```js
//深克隆（深克隆不考虑函数）
function deepClone(obj, result) {
  var result = result || {};
  for (var prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      if (typeof obj[prop] == "object" && obj[prop] !== null) {
        // 引用值(obj/array)且不为null
        if (Object.prototype.toString.call(obj[prop]) == "[object Object]") {
          // 对象
          result[prop] = {};
        } else {
          // 数组
          result[prop] = [];
        }
        deepClone(obj[prop], result[prop]);
      } else {
        // 原始值或func
        result[prop] = obj[prop];
      }
    }
  }
  return result;
}

// 深浅克隆是针对引用值
function deepClone(target) {
  if (typeof target !== "object") {
    return target;
  }
  var result;
  if (Object.prototype.toString.call(target) == "[object Array]") {
    // 数组
    result = [];
  } else {
    // 对象
    result = {};
  }
  for (var prop in target) {
    if (target.hasOwnProperty(prop)) {
      result[prop] = deepClone(target[prop]);
    }
  }
  return result;
}
// 无法复制函数
var o1 = jsON.parse(jsON.stringify(obj1));
```

#### 5、reverse 底层原理和扩展

```js
// 改变原数组
Array.prototype.myReverse = function () {
  var len = this.length;
  for (var i = 0; i < len; i++) {
    var temp = this[i];
    this[i] = this[len - 1 - i];
    this[len - 1 - i] = temp;
  }
  return this;
};
```

#### 6、圣杯模式的继承

```js
function inherit(Target, Origin) {
  function F() {}
  F.prototype = Origin.prototype;
  Target.prototype = new F();
  Target.prototype.constructor = Target;
  // 最终的原型指向
  Target.prop.uber = Origin.prototype;
}
```

#### 7、找出字符串中第一次只出现一次的字母

```js
String.prototype.firstAppear = function () {
  var obj = {},
    len = this.length;
  for (var i = 0; i < len; i++) {
    if (obj[this[i]]) {
      obj[this[i]]++;
    } else {
      obj[this[i]] = 1;
    }
  }
  for (var prop in obj) {
    if (obj[prop] == 1) {
      return prop;
    }
  }
};
```

#### 8、找元素的第 n 级父元素

```js
function parents(ele, n) {
  while (ele && n) {
    ele = ele.parentElement ? ele.parentElement : ele.parentNode;
    n--;
  }
  return ele;
}
```

#### 9、 返回元素的第 n 个兄弟节点

```js
function retSibling(e, n) {
  while (e && n) {
    if (n > 0) {
      if (e.nextElementSibling) {
        e = e.nextElementSibling;
      } else {
        for (e = e.nextSibling; e && e.nodeType !== 1; e = e.nextSibling);
      }
      n--;
    } else {
      if (e.previousElementSibling) {
        e = e.previousElementSibling;
      } else {
        for (
          e = e.previousElementSibling;
          e && e.nodeType !== 1;
          e = e.previousElementSibling
        );
      }
      n++;
    }
  }
  return e;
}
```

#### 10、封装 mychildren，解决浏览器的兼容问题

```js
function myChildren(e) {
  var children = e.childNodes,
    arr = [],
    len = children.length;
  for (var i = 0; i < len; i++) {
    if (children[i].nodeType === 1) {
      arr.push(children[i]);
    }
  }
  return arr;
}
```

#### 11、判断元素有没有子元素

```js
function hasChildren(e) {
  var children = e.childNodes,
    len = children.length;
  for (var i = 0; i < len; i++) {
    if (children[i].nodeType === 1) {
      return true;
    }
  }
  return false;
}
```

#### 12、我一个元素插入到另一个元素的后面

```js
Element.prototype.insertAfter = function (target, elen) {
  var nextElen = elen.nextElenmentSibling;
  if (nextElen == null) {
    this.appendChild(target);
  } else {
    this.insertBefore(target, nextElen);
  }
};
```

#### 13、返回当前的时间（年月日时分秒）

```js
function getDateTime() {
  var date = new Date(),
    year = date.getFullYear(),
    month = date.getMonth() + 1,
    day = date.getDate(),
    hour = date.getHours() + 1,
    minute = date.getMinutes(),
    second = date.getSeconds();
  month = checkTime(month);
  day = checkTime(day);
  hour = checkTime(hour);
  minute = checkTime(minute);
  second = checkTime(second);
  function checkTime(i) {
    if (i < 10) {
      i = "0" + i;
    }
    return i;
  }
  return (
    "" +
    year +
    "年" +
    month +
    "月" +
    day +
    "日" +
    hour +
    "时" +
    minute +
    "分" +
    second +
    "秒"
  );
}
```

#### 14、获得滚动条的滚动距离

```js
function getScrollOffset() {
  if (window.pageXOffset) {
    return {
      x: window.pageXOffset,
      y: window.pageYOffset,
    };
  } else {
    return {
      x: document.body.scrollLeft + document.documentElement.scrollLeft,
      y: document.body.scrollTop + document.documentElement.scrollTop,
    };
  }
}
```

#### 15、获得视口的尺寸

```js
function getViewportOffset() {
  if (window.innerWidth) {
    return {
      w: window.innerWidth,
      h: window.innerHeight,
    };
  } else {
    // ie8及其以下
    if (document.compatMode === "BackCompat") {
      // 怪异模式
      return {
        w: document.body.clientWidth,
        h: document.body.clientHeight,
      };
    } else {
      // 标准模式
      return {
        w: document.documentElement.clientWidth,
        h: document.documentElement.clientHeight,
      };
    }
  }
}
```

#### 16、获取任一元素的任意属性

```js
function getStyle(elem, prop) {
  return window.getComputedStyle
    ? window.getComputedStyle(elem, null)[prop]
    : elem.currentStyle[prop];
}
```

#### 17、绑定事件的兼容代码

```js
function addEvent(elem, type, handle) {
  if (elem.addEventListener) {
    //非ie和非ie9
    elem.addEventListener(type, handle, false);
  } else if (elem.attachEvent) {
    //ie6到ie8
    elem.attachEvent("on" + type, function () {
      handle.call(elem);
    });
  } else {
    elem["on" + type] = handle;
  }
}
```

#### 18、解绑事件

```js
function removeEvent(elem, type, handle) {
  if (elem.removeEventListener) {
    //非ie和非ie9
    elem.removeEventListener(type, handle, false);
  } else if (elem.detachEvent) {
    //ie6到ie8
    elem.detachEvent("on" + type, handle);
  } else {
    elem["on" + type] = null;
  }
}
```

#### 19、取消冒泡的兼容代码

```js
function stopBubble(e) {
  if (e && e.stopPropagation) {
    e.stopPropagation();
  } else {
    window.event.cancelBubble = true;
  }
}
```

#### 20、检验字符串是否是回文

```js
function isPalina(str) {
  if (Object.prototype.toString.call(str) !== "[object String]") {
    return false;
  }
  var len = str.length;
  for (var i = 0; i < len / 2; i++) {
    if (str[i] != str[len - 1 - i]) {
      return false;
    }
  }
  return true;
}
```

#### 21、检验字符串是否是回文

```js
function isPalindrome(str) {
  str = str.replace(/\W/g, "").toLowerCase();
  console.log(str);
  return str == str.split("").reverse().join("");
}
```

#### 22、兼容 getElementsByClassName 方法

```js
Element.prototype.getElementsByClassName =
  Document.prototype.getElementsByClassName = function (_className) {
    var allDomArray = document.getElementsByTagName("*");
    var lastDomArray = [];
    function trimSpace(strClass) {
      var reg = /\s+/g;
      return strClass.replace(reg, " ").trim();
    }
    for (var i = 0; i < allDomArray.length; i++) {
      var classArray = trimSpace(allDomArray[i].className).split(" ");
      for (var j = 0; j < classArray.length; j++) {
        if (classArray[j] == _className) {
          lastDomArray.push(allDomArray[i]);
          break;
        }
      }
    }
    return lastDomArray;
  };
```

#### 23、运动函数

```js
function animate(obj, json, callback) {
  clearInterval(obj.timer);
  var speed, current;
  obj.timer = setInterval(function () {
    var lock = true;
    for (var prop in json) {
      if (prop == "opacity") {
        current = parseFloat(window.getComputedStyle(obj, null)[prop]) * 100;
      } else {
        current = parseInt(window.getComputedStyle(obj, null)[prop]);
      }
      speed = (json[prop] - current) / 7;
      speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);

      if (prop == "opacity") {
        obj.style[prop] = (current + speed) / 100;
      } else {
        obj.style[prop] = current + speed + "px";
      }
      if (current != json[prop]) {
        lock = false;
      }
    }
    if (lock) {
      clearInterval(obj.timer);
      typeof callback == "function" ? callback() : "";
    }
  }, 30);
}
```

#### 24、弹性运动

```js
function ElasticMovement(obj, target) {
  clearInterval(obj.timer);
  var iSpeed = 40,
    a,
    u = 0.8;
  obj.timer = setInterval(function () {
    a = (target - obj.offsetLeft) / 8;
    iSpeed = iSpeed + a;
    iSpeed = iSpeed * u;
    if (Math.abs(iSpeed) <= 1 && Math.abs(a) <= 1) {
      console.log("over");
      clearInterval(obj.timer);
      obj.style.left = target + "px";
    } else {
      obj.style.left = obj.offsetLeft + iSpeed + "px";
    }
  }, 30);
}
```

#### 25、封装自己的 forEach 方法

```js
Array.prototype.myForEach = function (func, obj) {
  var len = this.length;
  var _this = arguments[1] ? arguments[1] : window;
  // var _this=arguments[1]||window;
  for (var i = 0; i < len; i++) {
    func.call(_this, this[i], i, this);
  }
};
```

#### 26、封装自己的 filter 方法

```js
Array.prototype.myFilter = function (func, obj) {
  var len = this.length;
  var arr = [];
  var _this = arguments[1] || window;
  for (var i = 0; i < len; i++) {
    func.call(_this, this[i], i, this) && arr.push(this[i]);
  }
  return arr;
};
```

#### 27、数组 map 方法

```js
Array.prototype.myMap = function (func) {
  var arr = [];
  var len = this.length;
  var _this = arguments[1] || window;
  for (var i = 0; i < len; i++) {
    arr.push(func.call(_this, this[i], i, this));
  }
  return arr;
};
```

#### 28、数组 every 方法

```js
Array.prototype.myEvery = function (func) {
  var flag = true;
  var len = this.length;
  var _this = arguments[1] || window;
  for (var i = 0; i < len; i++) {
    if (func.apply(_this, [this[i], i, this]) == false) {
      flag = false;
      break;
    }
  }
  return flag;
};
```

#### 29、数组 reduce 方法

```js
Array.prototype.myReduce = function (func, initialValue) {
  var len = this.length,
    nextValue,
    i;
  if (!initialValue) {
    // 没有传第二个参数
    nextValue = this[0];
    i = 1;
  } else {
    // 传了第二个参数
    nextValue = initialValue;
    i = 0;
  }
  for (; i < len; i++) {
    nextValue = func(nextValue, this[i], i, this);
  }
  return nextValue;
};
```

#### 30、获取 url 中的参数

```js
function getWindonHref() {
  var sHref = window.location.href;
  var args = sHref.split("?");
  if (args[0] === sHref) {
    return "";
  }
  var hrefarr = args[1].split("#")[0].split("&");
  var obj = {};
  for (var i = 0; i < hrefarr.length; i++) {
    hrefarr[i] = hrefarr[i].split("=");
    obj[hrefarr[i][0]] = hrefarr[i][1];
  }
  return obj;
}
```

#### 31、数组排序

```js
// 快排 [left] + min + [right]
function quickArr(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  var left = [],
    right = [];
  var pIndex = Math.floor(arr.length / 2);
  var p = arr.splice(pIndex, 1)[0];
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] <= p) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }
  // 递归
  return quickArr(left).concat([p], quickArr(right));
}

// 冒泡
function bubbleSort(arr) {
  for (var i = 0; i < arr.length - 1; i++) {
    for (var j = i + 1; j < arr.length; j++) {
      if (arr[i] > arr[j]) {
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
  return arr;
}

function bubbleSort(arr) {
  var len = arr.length;
  for (var i = 0; i < len - 1; i++) {
    for (var j = 0; j < len - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        var temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

#### 32、遍历 Dom 树

```js
// 给定页面上的DOM元素,将访问元素本身及其所有后代(不仅仅是它的直接子元素)
// 对于每个访问的元素，函数讲元素传递给提供的回调函数
function traverse(element, callback) {
  callback(element);
  var list = element.children;
  for (var i = 0; i < list.length; i++) {
    traverse(list[i], callback);
  }
}
```

#### 33、原生 js 封装 ajax

```js
function ajax(method, url, callback, data, flag) {
  var xhr;
  flag = flag || true;
  method = method.toUpperCase();
  if (window.XMLHttpRequest) {
    xhr = new XMLHttpRequest();
  } else {
    xhr = new ActiveXObject("Microsoft.XMLHttp");
  }
  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4 && xhr.status == 200) {
      console.log(2);
      callback(xhr.responseText);
    }
  };

  if (method == "GET") {
    var date = new Date(),
      timer = date.getTime();
    xhr.open("GET", url + "?" + data + "&timer" + timer, flag);
    xhr.send();
  } else if (method == "POST") {
    xhr.open("POST", url, flag);
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    xhr.send(data);
  }
}
```

#### 34、异步加载 script

```js
function loadScript(url, callback) {
  var oscript = document.createElement("script");
  if (oscript.readyState) {
    // ie8及以下版本
    oscript.onreadystatechange = function () {
      if (
        oscript.readyState === "complete" ||
        oscript.readyState === "loaded"
      ) {
        callback();
      }
    };
  } else {
    oscript.onload = function () {
      callback();
    };
  }
  oscript.src = url;
  document.body.appendChild(oscript);
}
```

#### 35、cookie 管理

```js
var cookie = {
  set: function (name, value, time) {
    document.cookie = name + "=" + value + "; max-age=" + time;
    return this;
  },
  remove: function (name) {
    return this.setCookie(name, "", -1);
  },
  get: function (name, callback) {
    var allCookieArr = document.cookie.split("; ");
    for (var i = 0; i < allCookieArr.length; i++) {
      var itemCookieArr = allCookieArr[i].split("=");
      if (itemCookieArr[0] === name) {
        return itemCookieArr[1];
      }
    }
    return undefined;
  },
};
```

#### 36、实现 bind()方法

```js
Function.prototype.myBind = function (target) {
  var target = target || window;
  var _args1 = [].slice.call(arguments, 1);
  var self = this;
  var temp = function () {};
  var F = function () {
    var _args2 = [].slice.call(arguments, 0);
    var parasArr = _args1.concat(_args2);
    return self.apply(this instanceof temp ? this : target, parasArr);
  };
  temp.prototype = self.prototype;
  F.prototype = new temp();
  return F;
};
```

#### 37、实现 call()方法

```js
Function.prototype.myCall = function () {
  var ctx = arguments[0] || window;
  ctx.fn = this;
  var args = [];
  for (var i = 1; i < arguments.length; i++) {
    args.push(arguments[i]);
  }
  var result = ctx.fn(...args);
  delete ctx.fn;
  return result;
};
```

#### 38、实现 apply()方法

```js
Function.prototype.myApply = function () {
  var ctx = arguments[0] || window;
  ctx.fn = this;
  if (!arguments[1]) {
    var result = ctx.fn();
    delete ctx.fn;
    return result;
  }
  var result = ctx.fn(...arguments[1]);
  delete ctx.fn;
  return result;
};
```

#### 39、防抖

```js
function debounce(handle, delay) {
  var timer = null;
  return function () {
    var _self = this,
      _args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function () {
      handle.apply(_self, _args);
    }, delay);
  };
}
```

#### 40、节流

```js
function throttle(handler, wait) {
  var lastTime = 0;
  return function (e) {
    var nowTime = new Date().getTime();
    if (nowTime - lastTime > wait) {
      handler.apply(this, arguments);
      lastTime = nowTime;
    }
  };
}
```

#### 41、requestAnimFrame 兼容性方法

```js
window.requestAnimFrame = (function () {
  return (
    window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    function (callback) {
      window.setTimeout(callback, 1000 / 60);
    }
  );
})();
```

#### 42、cancelAnimFrame 兼容性方法

```js
window.cancelAnimFrame = (function () {
  return (
    window.cancelAnimationFrame ||
    window.webkitCancelAnimationFrame ||
    window.mozCancelAnimationFrame ||
    function (id) {
      window.clearTimeout(id);
    }
  );
})();
```

#### 43、jsonp 底层方法

```js
function jsonp(url, callback) {
  var oscript = document.createElement("script");
  if (oscript.readyState) {
    // ie8及以下版本
    oscript.onreadystatechange = function () {
      if (
        oscript.readyState === "complete" ||
        oscript.readyState === "loaded"
      ) {
        callback();
      }
    };
  } else {
    oscript.onload = function () {
      callback();
    };
  }
  oscript.src = url;
  document.body.appendChild(oscript);
}
```

#### 44、获取 url 上的参数

```js
function getUrlParam(sUrl, sKey) {
  var result = {};
  sUrl.replace(/(\w+)=(\w+)(?=[&|#])/g, function (ele, key, val) {
    if (!result[key]) {
      result[key] = val;
    } else {
      var temp = result[key];
      result[key] = [].concat(temp, val);
    }
  });
  if (!sKey) {
    return result;
  } else {
    return result[sKey] || "";
  }
}
```

#### 45、格式化时间

```js
function formatDate(t, str) {
  var obj = {
    yyyy: t.getFullYear(),
    yy: ("" + t.getFullYear()).slice(-2),
    M: t.getMonth() + 1,
    MM: ("0" + (t.getMonth() + 1)).slice(-2),
    d: t.getDate(),
    dd: ("0" + t.getDate()).slice(-2),
    H: t.getHours(),
    HH: ("0" + t.getHours()).slice(-2),
    h: t.getHours() % 12,
    hh: ("0" + (t.getHours() % 12)).slice(-2),
    m: t.getMinutes(),
    mm: ("0" + t.getMinutes()).slice(-2),
    s: t.getSeconds(),
    ss: ("0" + t.getSeconds()).slice(-2),
    w: ["日", "一", "二", "三", "四", "五", "六"][t.getDay()],
  };
  return str.replace(/([a-z]+)/gi, function ($1) {
    return obj[$1];
  });
}
```

#### 46、验证邮箱的正则表达式

```js
function isAvailableEmail(sEmail) {
  var reg = /^([\w+\.])+@\w+([.]\w+)+$/;
  return reg.test(sEmail);
}
```

#### 47、函数柯里化

```js
//是把接受多个参数的函数变换成接受一个单一参数(最初函数的第一个参数)的函数，并且返回接受余下的参数且返回结果的新函数的技术

function curryIt(fn) {
  var length = fn.length,
    args = [];
  var result = function (arg) {
    args.push(arg);
    length--;
    if (length <= 0) {
      return fn.apply(this, args);
    } else {
      return result;
    }
  };
  return result;
}
```

#### 48、大数相加

```js
function sumBigNumber(a, b) {
  var res = "", //结果
    temp = 0; //按位加的结果及进位
  a = a.split("");
  b = b.split("");
  while (a.length || b.length || temp) {
    //~~按位非 1.类型转换，转换成数字 2.~~undefined==0
    temp += ~~a.pop() + ~~b.pop();
    res = (temp % 10) + res;
    temp = temp > 9;
  }
  return res.replace(/^0+/, "");
}
```

#### 49、单例模式

```js
function getSingle(func) {
  var result;
  return function () {
    if (!result) {
      result = new func(arguments);
    }
    return result;
  };
}
```

#### 50、从 RGB 转换为 HEX

```js
const rgbToHex = (r, g, b) => {
  const toHex = (num) => {
    // 转换为16进制
    const hex = num.toString(16);

    return hex.length === 1 ? `0${hex}` : hex;
  };

  return `#${toHex(r)}${toHex(g)}${toHex(b)}`;
  return;
};

console.log(rgbToHex(46, 32, 67)); // #2e2043
```

#### 51、判断两个字符串是否为互相排列

```js
const isAnagram = (str1, str2) => {
  const normalize = (str) =>
    str.toLowerCase().normalize("NFD").split("").sort().join("");
  return normalize(str1) === normalize(str2);
};

console.log(isAnagram("anagram", "naagram")); // true
console.log(isAnagram("car", "rat")); // false
console.log(isAnagram("heArt", "traEH")); // true
```

#### 52、判断两个字符串是否为相反回文字符串

```js
const isReverse = (str1, str2) => {
  const normalize = (str) =>
    str.toLowerCase().normalize("NFD").split("").reverse().join("");
  return normalize(str1) === str2;
};

console.log(isReverse("anagram", "naagram")); // false
console.log(isReverse("tar", "rat")); // tre
```
