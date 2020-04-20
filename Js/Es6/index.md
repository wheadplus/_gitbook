# Es6

ECMAScript 6 新引入了一些语法特性（语法糖），个人觉得主要记住一些语法糖还有重要部分如`Promise`，不用全记住。其他有需要用到的时候再看看即可。

## 详细教程

- [阮一峰es6](https://es6.ruanyifeng.com/#README)
- [MDNes6连接导航-jirengu整理](https://fangyinghang.com/es-6-tutorials/)

如果已经懂了概念，直接看[阮一峰Es6编程风格](https://es6.ruanyifeng.com/#docs/module-loader)，就可以知道语法糖的使用。

这里葫芦依样下，全当总结复习，不做具体验证。

## let 和 const

let取代var

- 不存在变量提升
- 不允许重复声明

const 常量

- 拥有let的特性
- 声明后常量,内存地址所保存的数据不得改动
  - number,字符串、布尔值不能修改
  - Object 不能修改，但它的属性可以修改。

```js
const animal = {}
animal = {name: ""}
//报错不能修改 Uncaught TypeError: Assignment to constant variable.
animal.name = 'jim'
//修改属性成功，"jim"
```

## 结构赋值

```js
let a = 1
let b = 2
let c = 3
//偷懒写法
let  [a,b,c] = 1,2,3

let obj = {name: 'jim',age:12}

let name = obj.name
let age = obj.age
//偷懒写法
let {name,age} = obj

//默认值
function sayName(name='jim') {
    return name
}
sayName() // jim
```



## 箭头函数

箭头函数的`this`就是外层环境的 `this`，有了它就不用声明_this 来保存`this`的具体值

```js
let fn = () => {
    console.log(this)
}
```

## 数组的扩展

`...` 

```js
let arr = [1,2,3]
let arr2 = [...arr]  
```

`concat()`合并成一个新数组

```js
let arr = [1,2,3],arr2 = ['a','b','c']
let arr3 = arr.concat(arr2)
//也可以
let arr3 = [...arr,...arr2]
```

`Array.from` 判断是否数组,成功返回一模一样的数组，否则空数组

```js
Array.from([1, 2, 3])
// [1, 2, 3]
Array.from({name:"jim"})
//[]
Array.from(function fn() {})
//[]
```

`find()`和`findIndex()`

找元素和找下表，好用，注意找不到返回值不同即可。

```js
[1,2,3,4,55].find(el => el >2)
//3
[1,2,3,4,55].find(el => el >100)
//undefined
[1,2,3,4,55].findIndex(el => el >2)
//2
[1,2,3,4,55].findIndex(el => el >100)
//-1
```

`includes`表示某个数组是否包含给定的值

```js
[1,2,3,4,55].includes(1)
//true
[1,2,3,4,55].includes(11)
//false
```

这里只列举了我常用的。详细看[ES6-array](https://es6.ruanyifeng.com/#docs/array)

