<!--
 * @Author: liboya
 * @Date: 2022-05-19 15:32:15
 * @LastEditors: 李博雅 1273319367@qq.com
 * @LastEditTime: 2022-05-23 21:03:21
 * @FilePath: /Knowledge-Map/CSS/css.md
 * @Description:
 *
 * Copyright (c) 2022 by 李博雅 1273319367@qq.com, All Rights Reserved.
-->

## 我的 CSS

> 持续更新中……

> **文章主要包含以下内容：**
>
> -

### 选择器

#### 逻辑选择器

在 CSS 选择器家族中，新增这样一类比较新的选择器 -- 逻辑选择器，目前共有 4 名成员：

`:is`, `:where`, `:not`, `:has`

1、`:is` 伪类选择器

`:is()` CSS 伪类函数将选择器列表作为参数，并选择该列表中任意一个选择器可以选择的元素。

在之前，对于多个不同父容器的同个子元素的一些共性样式设置，可能会出现如下 `CSS` 代码：

```css
header p:hover,
main p:hover,
footer p:hover {
  color: red;
  cursor: pointer;
}

// k可以改写为：
:is(header, main, footer) p:hover {
  color: red;
  cursor: pointer;
}
```

下面的动图更形象的展示

![](https://mmbiz.qpic.cn/mmbiz_gif/SMw0rcHsoNIw1PBAKps0oNC3cyRY9NTQ2XZFZDicpXmsIKKG0lqDUY5ico31o4q8kxwbjHMp76hbkxqJoKZCfl5g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

同时也是支持多层级 层叠连用

```html
<div>
  <i>div i</i>
</div>
<p>
  <i>p i</i>
</p>
<div>
  <span>div span</span>
</div>
<p>
  <span>p span</span>
</p>
<h1>
  <span>h1 span</span>
</h1>
<h1>
  <i>h1 i</i>
</h1>
```

```css
div span,
div i,
p span,
p i {
  color: red;
}

/* 使用 `:is` 之后： */
:is(div, p) :is(span, i) {
  color: red;
}
```


然而，他并不是万能的，`:is` 是不支持【伪元素】，例如：

> 注意，仅仅是不支持伪元素，伪类，譬如 :focus、:hover 是支持的。

```css
div p::before,
div p::after {
    content: "";
    //...
}

/* 上面的就不支持写为下面 */
div p:is(::before, ::after) {
    content: "";
    //...
}
```

`:is` 选择器的优先级

```html
<div>
    <p class="test-class" id="test-id">where & is test</p>
</div>
<div>
    <p class="test-class">where & is test</p>
</div>

```

```css
/* 此时，由于 div :is(p) 可以看成 div p，优先级是没有 div .test-class 高的，因此，被选中的文本的颜色是不会发生变化的。 */
div :is(p) {
    color: blue;
}

/* 如果想加上#text-id */
div :is(p, #text-id) {
    color: blue;
}
```

对于 `div :is(p, #text-id)`，`is:()` 内部有一个 `id` 选择器，因此，被该条规则匹配中的元素，全部都会应用 `div #id` 这一级别的选择器优先级。这里非常重要，再强调一下，对于 `:is()` 选择器的优先级，我们不能把它们割裂开来看，它们是一个整体，优先级取决于选择器列表中优先级最高的选择器


`:is` 的别名 `:matches()` 与 `:any()`

`:is()` 是最新的规范命名，在之前，有过有同样功能的选择，分别是：

```css
:is(div, p) span {}
// 等同于
:-webkit-any(div, p) span {}
:-moz-any(div, p) span {}
:matches(div, p) span {}
```


2、`:where` 伪类选择器

了解了 `:is` 后，我们可以再来看看 `:where`，它们两个有着非常强的关联性。`:where` 同样是将选择器列表作为其参数，并选择可以由该列表中的选择器之一选择的任何元素。

还是这个例子：

```css
:where(header, main, footer) p:hover {
  color: red;
  cursor: pointer;
}

/* 上面的css，等同于： */
header p:hover,
main p:hover,
footer p:hover {
  color: red;
  cursor: pointer;
}
```
上面的样式看上去和 `:is` 貌似一样啊，下面来说下两者的区别：

