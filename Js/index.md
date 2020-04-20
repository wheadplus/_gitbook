# 数据类型

JavaScript 中每个值都属于某种数据类型。共有`7`种：

- String
- Number
- Boolean
- Null
- Undefined
- Object
- Symbol

其中`Object` 可以细分为`3`种：

- Object
- Array
- Function

## 确定类型

### typeof

```js
typeof 'sss'
"string"
typeof 123
"number"
typeof true
"boolean"
typeof null
"object"
typeof undefined
"undefined"
typeof function(){}
"function"
var obj = {name:'jim'}
undefined
typeof obj   //js设计规范如此，逻辑错误
"object"
typeof  [1,2,3]
"object"
var sy = new Symbol(1,2,3)
typeof Symbol()
"symbol"
```

可以发现 typeof 对于

- null 
- Object
- Array

是无法区分的。

### instanceof 

```js
var o = {};
var a = [];

o instanceof Array // false
a instanceof Array // true
```

