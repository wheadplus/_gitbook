# BFC

块级格式上下文（Block Formatting Context，BFC）是一种规则，它定义了块级元素的渲染规则。

- 区域内从左到右，不够排列另起一行
- 区域内相邻的两个`div`外边距合并

## 特性

- 内部的块级元素垂直摆放。
- 内部的行内元素水平摆放，放不下另起一行。
- 相邻的两个div，margin合并。

## 产生条件

1. html

2. float元素

3. position absolute 或fixed

4. 行内块级元素 inline-block

5. [更多看mdn](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

   