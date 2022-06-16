# CSS三大特性

CSS全称 **Cascading Style Sheets**（层叠样式表）

CSS中有三个重要的基础规则，一个是层叠（Cascading）、一个是继承（Inheritance）、一个是优先级。

## 层叠

层叠是 CSS 的一个基本特征，它是一个定义了如何合并来自多个源的属性值的算法。css声明可以有不同的来源。

#### 样式表的来源

- 用户代理样式
  
  浏览器默认设置的样式

- 用户样式表
  
  用户设置的 CSS 多指用户安装插件等工具所设置的 CSS（称为“注入的样式表”），比方说 Adblock 等插件对页面元素隐藏的 CSS 就属于这一类。

- 作者样式表
  
  网页的作者可以定义文档的样式，这是最常见的样式表，作者开发的样式表

#### 哪些css实体会参与层叠计算

只有 CSS 声明，就是属性名值对，会参与层叠计算

@media;@documents;@supports;等会参与层叠计算。

不参与层叠计算的有

@font-face;@keyframes;@import;@charset;

#### 层叠顺序（层叠优先级）

层叠算法是先于优先级算法的。（重要程度越大优先级越高）

|     | 来源              | 重要程度 |
| --- | --------------- | ---- |
| 1   | 用户代理            | 1    |
| 2   | 用户              | 2    |
| 3   | 页面作者            | 3    |
| 4   | css动画           | 4    |
| 5   | 页面作者 !important | 5    |
| 6   | 用户 !important   | 6    |
| 7   | 用户代理 !important | 7    |
| 8   | css transitions | 8    |

#### 重置样式

all 属性让你能够立刻把所有的属性都还原到它们初始（默认）的状态，或是继承自前一个层叠顺序等级的状态，又或是指定一个特定的来源（用户代理、页面作者或者用户），甚至还可以选择完全清除所有的属性。all:initial

#### css动画与层叠

@keyframes不参与层叠。意味着在任何时候 CSS 都是取单一的 @keyframes 的值而不会是某几个 @keyframe 的混合。同时仍应注意用 @keyframes @规则定义的值会覆盖全部普通值，但会被 !important 的值覆盖。

## 优先级

如果层叠顺序相等，则会使用优先级来决定使用哪个值。

浏览器将优先级分为两个部分：HTML行内样式和选择器的样式。

#### 行内样式

行内元素属于
“带作用域的”声明，它会覆盖任何来自样式表或者<style>标签的样式。行内样式没有选择器，因为它们直接作用于所在的元素。

为了在样式表里覆盖行内声明，需要为声明添加!important，这样能将它提升到一个更高
优先级的来源。但如果行内样式也被标记为!important，就无法覆盖它了。

#### 选择器优先级

优先级就是分配给指定的 CSS 声明的一个权重，它由 匹配的选择器中的 每一种选择器类型的 数值 决定。

而当优先级与多个 CSS 声明中任意一个声明的优先级相等的时候，CSS 中最后的那个声明将会被应用到元素上。

不同类型的选择器有不同的优先级，ID选择器比类选择器优先级更高，实际上， ID
选择器的优先级比拥有任意多个类的选择器都高。

|     | 选择器类型                                         | 优先级 |
| --- | --------------------------------------------- | --- |
|     | 类型选择器（h1）、伪元素(::before)                       | 0   |
|     | 类选择器(.example)、属性选择器[type="input"]、伪类(:hover) | 1   |
|     | ID选择器                                         | 2   |

通用选择器（ *）和组合器（ >、 +、 ~）对优先级没有影响；否定伪类也对有衔接没有影响(:not())

#### !important规则

当在一个样式声明中使用一个 `!important` 规则时，此声明将覆盖任何其他声明。虽然，从技术上讲，`!important` 与优先级无关，但它与最终的结果直接相关。使用 `!important` 是一个**坏习惯**，应该尽量避免，因为这破坏了样式表中的固有的级联规则 使得调试找 bug 变得更加困难了。

#### 优先级标记

一个常用的表示优先级的方式是用数值形式来标记，通常用逗号隔开每个数。比如，“1,2,2”
表示选择器由 1 个 ID、 2 个类、 2 个标签组成。优先级最高的 ID 列为第一位，紧接着是类，最后是标签。

## 继承

在 css 中，每个[CSS 属性定义](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Reference)的概述都指出了这个属性是默认继承的 ("Inherited: Yes") 还是默认不继承的 ("Inherited: no")。这决定了当你没有为元素的属性指定值时该如何计算值。

但不是所有的属性都能被继承。默认情况下，只有特定的一些属性能被继承，通常是我们
希望被继承的那些。它们主要是跟文本相关的属性： color、 font、 font-family、 font-size、font-weight、 font-variant、 font-style、 line-height、 letter-spacing、 text-align、text-indent、 text-transform、 white-space 以及 word-spacing。
还有一些其他的属性也可以被继承，比如列表属性： list-style、 list-style-type、list-style-position 以及 list-style-image。表格的边框属性 border-collapse 和 border-spacing 也能被继承。

当元素的一个**继承属性（inherited property****）**没有指定值时，则取父元素的同属性的[计算值 computed value (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value "Currently only available in English (US)")

当元素的一个**非继承属性**没有指定值时，则取属性的[初始值 initial value](https://developer.mozilla.org/zh-CN/docs/Web/CSS/initial_value)（该值在该属性的概述里被指定）。

#### inherit关键字

可以赋值给任意属性，[`inherit`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inherit) 关键字允许显式的声明继承性，它对继承和非继承属性都生效。

#### initial关键字

有时，你需要撤销作用于某个元素的样式。这可以用 initial 关键字来实现。每一个 CSS
属性都有初始（默认）值。如果将 initial 值赋给某个属性，那么就会有效地将其重置为**默认
值**，这种操作相当于硬复位了该值。(all:initital)  (width:initial === width:auto)

需要注意的是initial与auto关键字不同，auto是width等属性的默认值，但不是所有属性的默认值，对很多属性来说甚至不是合法的值。比如border-width: auto 和 padding: auto 是非法的，因此不会生效。

#### unset关键字

unset表示不固定值，特性如下，当前元素浏览器或用户设置的CSS忽略，然后如果是具有继承特性的CSS，如`color`, 则使用继承值；如果是没有继承特性的CSS属性，如`background-color`, 则使用初始值。(all:unset)。

#### 简写属性

大多数简写属性可以省略一些值，只指定我们关注的值。但是要知道，这样做仍然会设置省
略的值，即它们会被隐式地设置为初始值。**这会默默覆盖在其他地方定义的样式**。

易于混淆的简写属性的顺序一般分为两种

上右下坐

    margin、padding等

水平垂直

    background-position、box-shadow等
