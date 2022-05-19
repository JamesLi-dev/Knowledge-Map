## JS 基础扫盲

> **文章主要包含以下内容：**
>  
> - 数组常用方法
> - 字符串常用方法
> - 常用遍历方法&高阶函数
> - 常用正则表达式
> - 数学知识


### 一、数组常用方法

#### 1.push()

在尾部追加，类似于压栈，原数组会变。

```
const arr = [1, 2, 3]
arr.push(8)
console.log(arr) // [1, 2, 3, 8]
复制代码
```

#### 2.pop()

在尾部弹出，类似于出栈，原数组会变。数组的 `push` & `pop` 可以模拟常见数据结构之一：栈。

```
const arr = [1, 2, 3]
const popVal = arr.pop()
console.log(popVal) // 3
console.log(arr) // [1, 2]

// 数组模拟常见数据结构之一：栈
const stack = [0, 1]
stack.push(2) // 压栈
console.log(stack) // [0, 1, 2]

const popValue = stack.pop() // 出栈
console.log(popValue) // 2
console.log(stack) // [0, 1]
复制代码
```

#### 3.unshift()

在头部压入数据，类似于入队，原数组会变。

```
const arr = [1, 2, 3]
arr.unshift(0)
console.log(arr) // [0, 1, 2, 3]
复制代码
```

#### 4.shift()

在头部弹出数据，原数组会变。数组的 `push`（入队） & `shift`（出队） 可以模拟常见数据结构之一：队列。

```
const arr = [1, 2, 3]
const shiftVal = arr.shift()
console.log(shiftVal) // 1
console.log(arr) // [2, 3]

// 数组模拟常见数据结构之一：队列
const queue = [0, 1]
queue.push(2) // 入队
console.log(queue) // [0, 1, 2]

const shiftValue = queue.shift() // 出队
console.log(shiftValue) // 0
console.log(queue) // [1, 2]
复制代码
```

#### 5.concat()

`concat`会在当前数组尾部拼接传入的数组，然后返回一个新数组，原数组不变。

```
const arr = [1, 2, 3]
const arr2 = arr.concat([7, 8, 9])
console.log(arr) // [1, 2, 3]
console.log(arr2) // [1, 2, 3, 7, 8, 9]
复制代码
```

#### 6.indexOf()

在数组中寻找该值，找到则返回其下标，找不到则返回`-1`。

```
const arr = [1, 2, 3]
console.log(arr.indexOf(2)) // 1
console.log(arr.indexOf(0)) // -1
复制代码
```

#### 7.includes()

在数组中寻找该值，找到则返回`true`，找不到则返回`false`。

```
const arr = [1, 2, 3]
console.log(arr.includes(2)) // true
console.log(arr.includes(4)) // false
复制代码
```

#### 8.join()

将数组转化成字符串，并返回该字符串，不传值则默认逗号隔开，原数组不变。

```
const arr = [1, 2, 3]
console.log(arr.join()) // ‘1, 2, 3’
console.log(arr) // [1, 2, 3]
复制代码
```

#### 9.reverse()

翻转原数组，并返回已完成翻转的数组，原数组改变。

```
const arr = [1, 2, 3]
console.log(arr.reverse()) // [3, 2, 1]
console.log(arr) // [3, 2, 1]
复制代码
```

#### 10.slice(start，end)

从`start` 开始截取到`end`，但是不包括`end`

```
const arr = [1, 2, 3, 4, 5]
console.log(arr.slice(1, 4)) // [2, 3, 4]
console.log(arr) // [1, 2, 3, 4, 5]
复制代码
```

#### 11.splice(start, deleteCount, item1, item2……)

- `start`参数 开始的位置
- `deleteCount`要截取的个数
- 后面的`items`为要添加的元素
- 如果`deleteCount`为`0`，则表示不删除元素，从`start`位置开始添加后面的几个元素到原始的数组里面。
- 返回值为由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
- 这个方法会改变原始数组，数组的长度会发生变化

```
const arr3 = [1, 2, 3, 4, 5, 6, 7, "f1", "f2"];
const arr4 = arr3.splice(2, 3) // 删除第三个元素以后的三个数组元素(包含第三个元素)
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
console.log(arr7);// ["xiao", "long", 7, "f1", "f2"]
console.log(arr3); // [1, 2]
复制代码
```

#### 12.sort()

- 对数组的元素进行排序，并返回数组。
- 默认排序顺序是在将元素转换为字符串，然后比较它们的`UTF-16`代码单元值序列时构建的。
- 由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。

可参考 **MDN：Sort**[5]

```
const arr = [1, 2, 3]
arr.sort((a, b) => b - a)
console.log(arr) // [3, 2, 1]
复制代码
```

#### 13.toString()

将数组转化成字符串，并返回该字符串，逗号隔开，原数组不变。

```
const arr = [1, 2, 3, 4, 5]
console.log(arr.toString()) // ‘1, 2, 3, 4, 5’
console.log(arr) // [1, 2, 3, 4, 5]
复制代码
```

### 二、字符串常用方法

#### 1.charAt()

返回指定索引位置处的字符。类似于数组用中括号获取相应下标位置的数据。

```
var str = 'abcdefg'
console.log(str.charAt(2)) // 输出 'c' 
console.log(str[2]) // 输出 'c'
复制代码
```

#### 2.concat()

类似数组的concat()，用来返回一个合并拼接两个或两个以上字符串。原字符串不变。

```
const str1 = 'abcdefg'
const str2 = '1234567'
const str3 = str1.concat(str2)
console.log(str3) // 输出 'abcdefg1234567'
复制代码
```

#### 3.indexOf()、lastIndexOf()

`indexOf`,返回一个字符在字符串中首次出现的位置,`lastIndexOf`返回一个字符在字符串中最后一次出现的位置。

```
const str = 'abcdcefcg'
console.log(str.indexOf('c')) // 输出 '2'
console.log(str.lastIndexOf('c')) // 输出 '7'
复制代码
```

#### 4.slice()

提取字符串的片断，并把提取的字符串作为新的字符串返回出来。原字符串不变。

```
const str = 'abcdefg'
console.log(str.slice()) // 输出 'abcdefg', 不传递参数默认复制整个字符串
console.log(str.slice(1)) // 输出 'bcdefg',传递一个，则为提取的起点，然后到字符串结尾
console.log(str.slice(2, str.length-1)) // 输出'cdef',传递两个，为提取的起始点和结束点
复制代码
```

#### 5.split()

使用指定的分隔符将一个字符串拆分为多个子字符串数组并返回，原字符串不变。

```
const str = 'A*B*C*D*E*F*G'
console.log(str.split('*')) // 输出 ["A", "B", "C", "D", "E", "F", "G"]
复制代码
```

#### 6.substr(), substring()

- 这两个方法的功能都是截取一个字符串的片段，并返回截取的字符串。
- `substr`和`substring`这两个方法不同的地方就在于参数二，`substr`的参数二是截取返回出来的这个字符串指定的长度，`substring`的参数二是截取返回这个字符串的结束点，并且不包含这个结束点。而它们的参数一，都是一样的功能，截取的起始位置。
- **注意事项**：`substr`的参数二如果为`0`或者负数，则返回一个空字符串，如果未填入，则会截取到字符串的结尾去。`substring`的参数一和参数二为`NAN`或者负数，那么它将被替换为`0`。

```
const str = 'ABCDEFGHIJKLMN'
console.log(str.substr(2))  // 输出 'CDEFGHIJKLMN'
console.log(str.substring(2)) // 输出 'CDEFGHIJKLMN'

console.log(str.substr(2, 9))  // 输出 'CDEFGHIJK'
console.log(str.substring(2, 9))  // 输出 'CDEFGHI'
复制代码
```

#### 7.match()

`match()`方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配，并返回一个包含该搜索结果的数组。

```
const str = '2018年结束了，2019年开始了，2020年就也不远了'
const reg = /\d+/g  // 这里是定义匹配规则，匹配字符串里的1到多个数字
console.log(str.match(reg))  // 输出符合匹配规则的内容，以数组形式返回 ['2018', '2019', '2020']
console.log(str.match('20'))  // 不使用正则 ["20", index: 0, input: "2018年结束了，2019年开始了"]
复制代码
```

**注意事项**:如果`match`方法没有找到匹配，将返回`null`。如果找到匹配，则 `match`方法会把匹配到以数组形式返回，如果正则规则未设置全局修饰符`g`，则 `match`方法返回的数组有两个特性：`input`和`index`。`input`属性包含整个被搜索的字符串。`index`属性包含了在整个被搜索字符串中匹配的子字符串的位置。

#### 8.replace()

`replace`接收两个参数，参数一是需要替换掉的字符或者一个正则的匹配规则，参数二，需要替换进去的字符，仔实际的原理当中，参数二，你可以换成一个回调函数。

```
const str = '2018年结束了，2019年开始了，2020年就也不远了'
const rex = /\d+/g  // 这里是定义匹配规则，匹配字符串里的1到多个数字
const str1 = str.replace(rex, '****') 
console.log(str1) // 输出："****年结束了，****年开始了,****年也不远了"
const str2 = str.replace(rex, function(item){
    console.log(arguments)  // 看下面的图片
    const arr = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖']
    let newStr = ''
    item.split('').map(function(i){
            newStr += arr[i]
    })     
    return newStr       
})
console.log(str2) // 输出：贰零壹捌年结束了，贰零壹玖年开始了,贰零贰零年也不远了
复制代码
```

#### 9.search()

在目标字符串中搜索与正则规则相匹配的字符，搜索到，则返回第一个匹配项在目标字符串当中的位置，没有搜索到则返回一个`-1`。

```
const str = '2018年结束了，2019年开始了，2020年就也不远了'
const reg = /\d+/i  // 这里是定义匹配规则,匹配字符串里的1到多个数字
console.log(str.search(reg)) // 输出 0  这里搜索到的第一项是从位置0开始的
复制代码
```

#### 10.toLowerCase(),toUpperCase()

`toLowerCase`把字母转换成小写，`toUpperCase()`则是把字母转换成大写。

```
const str1 = 'abcdefg'
const str2 = 'ABCDEFG'
console.log(str2.toLowerCase())  // 输出：'abcdefg'
console.log(str1.toUpperCase())  // 输出：'ABCDEFG'
复制代码
```

#### 11.includes(), startsWith(), endsWith()

`includes`、`startsWith`、`endsWith`，`es6`的新增方法，`includes` 用来检测目标字符串对象是否包含某个字符，返回一个布尔值，`startsWith`用来检测当前字符是否是目标字符串的起始部分，相对的`endwith`是用来检测是否是目标字符串的结尾部分。

```
const str = 'Excuse me, how do I get to park road?'
console.log(str.includes('how')) // 输出：true
console.log(str.startsWith('Excuse')) // 输出：true
console.log(str.endsWith('?')) // 输出：true
复制代码
```

#### 12.repeat()

返回一个新的字符串对象，新字符串等于重复了指定次数的原始字符串。接收一个参数，就是指定重复的次数。原字符串不变。

```
const str = 'http'
const str2 = str.repeat(3)
console.log(str) // 输出：'http'
console.log(str2) // 输出：'httphttphttp'
复制代码
```

### 三、常用遍历方法&高阶函数

#### 1.for()

最常用的`for`循环，经常用的数组遍历，也可以遍历字符串。

```
const arr = [1, 2, 3]
const str = 'abc'
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i])
    console.log(str[i])
}
复制代码
```

#### 2.while() / do while()

`while`、`do while`主要的功能是，当满足`while`后边所跟的条件时，来执行相关业务。这两个的区别是，`while`会先判断是否满足条件，然后再去执行花括号里面的任务，而`do while`则是先执行一次花括号中的任务，再去执行`while`条件，判断下次还是否再去执行`do`里面的操作。也就是说 `**do while**`**至少会执行一次操作**.

```
while(条件){
     执行...
}
------------
do{
    执行...
}
while(条件)
复制代码
```

#### 3.forEach()

拷贝一份遍历原数组。

- `return`无法终止循环。不过可以起到`continue`效果。
- 本身是不支持的`continue`与`break`语句的我们可以通过`some`和 `every`来实现。

```
const arr = [5,1,3,7,4]
arr.forEach((item, index) => {
    if (item < 2) return
    console.log(`索引：${index}，数值：${item}`)
    arr[5] = 0
})
console.log(arr)
// 打印结果：
// 索引：0，数值：5
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [5, 1, 3, 7, 4, 0]
复制代码
```

#### 4.for...in

- `for...in` 是 ES5 标准， 此方法遍历数组效率低，主要是用来循环遍历对象的属性。
- 遍历数组的缺点：数组的下标`index`值是数字，`for-in`遍历的`index`值`"0","1","2"`等是字符串。
- `Object.defineProperty`，建立的属性，默认不可枚举。

```
const foo = {
    name: 'bar',
    sex: 'male'
}
Object.defineProperty(foo, "age", { value : 18 })
for(const key in foo){
    console.log(`可枚举属性：${key}`)
}
console.log(`age属性：${foo.age}`)
// 打印结果：
// 可枚举属性：name
// 可枚举属性：sex
// age属性：18
复制代码
```

#### 5.for...of

`for…of`是`ES6`新增的方法，但是`for…of`不能去遍历普通的对象，`**for…of**`**的好处是可以使用**`**break**`**跳出循环。**

-  `for-of`这个方法避开了`for-in`循环的所有缺陷 
-  与`forEach()`不同的是，它可以正确响应`break`、`continue`和`return`语句 
-  `for-of`循环不仅支持数组，还支持大多数类数组对象，例如`DOM` **NodeList对象**[6]。 
-  
   - `for-of`循环也支持字符串遍历

```
// for of 循环直接得到的就是值
const arr = [1, 2, 3]
for (const value of arr) {
 console.log(value)
}
复制代码
```

**面试官：说一下 **`**for...in**`** 和 **`**for...of**`** 区别？**

```
（1）for…in 用于可枚举数据，如对象、数组、字符串
（2）for…of 用于可迭代数据，如数组、字符串、Map、Set
复制代码
```

#### 6.every / some

**返回一个布尔值**。当我们需要判定数组中的元素是否满足某些条件时，可以使用`every` / `some`。这两个的区别是，`every`会去判断判断数组中的每一项，而 `some`则是当某一项满足条件时返回。

```
// every
const foo = [5,1,3,7,4].every((item, index) => {
    console.log(`索引：${index}，数值：${item}`)
    return item > 2
})
console.log(foo)
// every 打印：
// 索引：0，数值：5
// 索引：1，数值：1
// false
复制代码
// some
const foo = [5,1,3,7,4].some((item, index) => {
    console.log(`索引：${index}，数值：${item}`)
    return item > 2
})
console.log(foo)
// some 打印：
// 索引：0，数值：5
// true
复制代码
```

#### 7.filter()

- `filter`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。
- 它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。
- 该方法不会改变原数组。

```
const foo = [5,1,3,7,4].filter((item,index) => {
    console.log(`索引：${index}，数值：${item}`)
    return item > 2
})
console.log(foo)
// 打印结果：
// 索引：0，数值：5
// 索引：1，数值：1
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [5, 3, 7, 4]
复制代码
```

#### 8.map()

- `map`即是 “映射”的意思 ，原数组被“映射”成对应新数组。
- `map：`支持`return`，相当与原数组克隆了一份，把克隆的每项改变了，也不影响原数组。

```
const foo = [5,1,3,7,4].map((item,index) => {
    console.log(`索引：${index}，数值：${item}`)
    return item + 2
})
console.log(foo)
// 打印结果：
// 索引：0，数值：5
// 索引：1，数值：1
// 索引：2，数值：3
// 索引：3，数值：7
// 索引：4，数值：4
// [7, 3, 5, 9, 6]
复制代码
```

#### 9. reduce() / reduceRight()

`reduce` 从左到右将数组元素做“叠加”处理，返回一个值。`reduceRight` 从右到左。

```
const foo = [5,1,3,7,4].reduce((total, cur) => {
    console.log(`叠加：${total}，当前：${cur}`)
    return total + cur
})
console.log(foo)
// 打印结果：
// 叠加：5，当前：1
// 叠加：6，当前：3
// 叠加：9，当前：7
// 叠加：16，当前：4
// 20
复制代码
```

#### 10.Object,keys遍历对象的属性

`Object.keys`方法的参数是一个对象，返回一个数组。该数组的成员都是该对象自身的（而不是继承的）所有属性名，且只返回可枚举的属性。

```
const obj = {
  p1: 123,
  p2: 456
};
Object.keys(obj) // ["p1", "p2"]
复制代码
```

#### 11.Object.getOwnPropertyNames() 遍历对象的属性

`Object.getOwnPropertyNames`方法与`Object.keys`类似，也是接受一个对象作为参数，返回一个数组，包含了该对象自身的所有属性名。但它能返回不可枚举的属性。

```
const arr = ['Hello', 'World'];
Object.keys(arr) // ["0", "1"]
Object.getOwnPropertyNames(arr) // ["0", "1", "length"]
复制代码
```

#### 以上遍历方法的区别：

```
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
复制代码
```

### 四、常用正则表达式

这里罗列一些我在刷算法题中遇到的正则表达式，如果有时间可认真学一下**正则表达式不要背**[7]。

#### 1.判断字符

```
由26个英文字母组成的字符串：^[A-Za-z]+$
由26个大写英文字母组成的字符串：^[A-Z]+$
由26个小写英文字母组成的字符串：^[a-z]+$
由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
复制代码
```

#### 2.判断数字

```
数字：^[0-9]*$
复制代码
```

持续更新，敬请期待……

### 五、数学知识

#### 1.质数

若一个正整数无法被除了`1` 和它自身之外的任何自然数整除，则称该数为质数（或素数），否则称该正整数为合数。

```
function judgePrime(n) {
    for (let i = 2; i * i <= n; i++) {
        if (n % i == 0) return false
    }
    return true
}
复制代码
```

#### 2.斐波那契数列

```
function Fibonacci(n) {
    if (n <= 1) return n  
    return Fibonacci(n - 1) + Fibonacci(n - 2)
}
复制代码
```

## 1. 打乱数组顺序

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1hTIkFLPdXy7bRcC6bdNfBlicppNJAE2XS17bbxLv9oWYJFHBnscThqg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=gWiwk&originHeight=221&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code1.png

## 2. 去除数字之外的所有字符

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1j8u7r3V4KueHJU9dc9RJn3W3vJ4MKIl8pAxxOGRLTWFSKt7XEO63Kw/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=vEh83&originHeight=227&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code20.png

## 3. 反转字符串或者单词

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1lBH3JWdPF58ayye2y4GMqlCRGbkEdVTMeUoBKJZKSWicVTP6DPxarOQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=HQ1rQ&originHeight=372&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code2.png

## 4. 将十进制转换为二进制或十六进制

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1iaib3X8eH8pHNqDDVfUb9fCGJpJ5WZwNHPaBSiaNURyVmV6WoF7ibibYdJQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=i5UAl&originHeight=281&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code3.png

## 5. 合并多个对象

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1W96E9eY69ZXiaiciaTR6uMiaO9R14CFcTQ4P444ZxyJ9ickxMDLZSicPqZOQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=tzxO8&originHeight=494&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code4.png

## 6. `===` 和 `==` 的区别

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1aFEE4ic0s7hvx38r3LhicvWASicnBRicreHJ8SuNX7iajYBLBibsdzJsoaBw/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=DkrwM&originHeight=352&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code5.png

## 7. 解构赋值

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1rdATYE5nE5l0gniaNa5W9RNibFuP3cjlK972tttNvn5NflCBibibJrd8Zw/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=PLcjm&originHeight=401&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code6.png

## 8. 交换变量的值

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1s3FSFgn8rY5ULtVPK2aET2yKaBz17ElBELcbD1Gu0UYFMt4GtqdlYg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=zh3Cb&originHeight=294&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code7.png

## 9-1. 判断回文字符串

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1okFTWyO7mUDNiaAXPf37ktSmKJ2usrF7Rj4haL7tXvmFKCibWjrNqvcA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=qrWQm&originHeight=338&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code21.png

> 回文字符串: 正着写和反着写都一样的字符串 (特别感谢**@浮生阁阁主**[1]勘误)


## 9-2 判断两个字符串是否为互相排列

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1UVO0L6FJoHGm7ibz4gx2iabYBJK5mdzHhb2xbOckPccx4MXcLFUFValA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=Rhe91&originHeight=367&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code8.png

> 判断两个字符串是否为互相排列: 给定两个字符串,一个是否是另一个的排列


## 10. 可选链操作符

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1hKmc6ibBCGXuagIRP0AqmT3QRQ7dW9zdfGDySjvuSZ6pte9klwpV32A/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=Sl7va&originHeight=402&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code9.png

> MDN: **可选链**操作符( `?.` )允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。`?.` 操作符的功能类似于 `.` 链式操作符，不同之处在于，在引用为空(nullish ) (`null` 或者 `undefined`) 的情况下不会引起错误，该表达式短路返回值是 `undefined`。与函数调用一起使用时，如果给定的函数不存在，则返回 `undefined`


例如：

```
if (res && res.data && res.data.success) {   
   //code
} 
复制代码
```

相当于：

```
if (res?.data?.success) {
  // code
}
复制代码
```

## 11. 三目运算符

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1PFHO0ESGLuJ71HaLWVHZY9El4KibZqgrkjNGp5YicmyJ8wX00u6XpIjQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=lEKIG&originHeight=216&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code10.png

## 12. 从数组中随机选择一个值

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1B6Eup41Uz6ayVHMYd7SBsJplPLeJ1z9cibGGAicP3XgfZCC28GLBpBFA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=E3e6x&originHeight=195&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code11.png

## 13. 冻结对象

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1KSuiaallAwajYVnsFwVafIuibD7BTPHL0HxFWvu48EJeEdiaYmLjJoaxg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=PDlk4&originHeight=265&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code12.png

## 14. 删除数组重复的元素

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1kibqOOk02MdnSXuBiaQ9QulVX0KkBDZnIv7aELDRBXpw9jb2tEyJrXCg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=aZs10&originHeight=213&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code13.png

## 15. 保留指定位小数

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl10un8IUiayTyvvUhehPkiaMygbS1r7d4qhMlN850S2EnTt1zX7dFzZVdA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=uXB5n&originHeight=319&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code14.png

## 16. 清空数组

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1c6IG5hgc3MeMWpP0Q6N69O7DBaGowhse3m82FcBvImYQE7ZrruQHIg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=A3L27&originHeight=238&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code15.png

## 17. 从 `RGB` 转换为 `HEX`

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1TUOSUXaDDPGt3ykRAVuteJKY3uu6qphZicCC9MM7cc2d2eNEciaxl6dQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=qP8AW&originHeight=304&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code16.png

## 18. 从数组中获取最大值和最小值

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1EVzex86uS8ciaL6vA0XTTQialwdngriaF6fmgbBUicM1TNEJeYGH2R8ZiaA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=krQ3z&originHeight=263&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code17.png

## 19. 空值合并运算符

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl12zLFtdN7icZL5UibgHl22rgAmx5ib549WglNzwafou81FnfWDia4YaymnA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=eYz1p&originHeight=360&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)code18.png

> MDN: **空值合并操作符**（`??`）是一个逻辑操作符，当左侧的操作数为 `null` 或者 `undefined` 时，返回其右侧操作数，否则返回左侧操作数。


## 20. 过滤数组中值为 `false` 的值

![](https://mmbiz.qpic.cn/mmbiz/pfCCZhlbMQSUnObcz8MDKKFlMlTudyl1ObjYlljzevaHqMdKls2PdpOKl6USVGLJNEdzy5XMBUtBQWguap2MHA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1#crop=0&crop=0&crop=1&crop=1&id=Jso2n&originHeight=215&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
