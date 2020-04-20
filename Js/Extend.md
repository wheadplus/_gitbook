# 继承

> 继承是指一个对象直接使用另一对象的属性和方法。

在calss语法之前。只能自己实现。方法很多。

所以继承，做了两件事：

- 得到一个类的属性
- 得到一个类的方法

### 属性获取

通过call/apply 绑定属性

```js
function Animal(color) {
    this.color = color
}
Animal.prototype.move = function () {}

function Dog(color,name) {
    Animal.call(this,color)
    Animal.apply(this,arguments)//多个属性时用apply
    this.name = name
}
```

### 方法获取

```js
Dog.prototype = Object.create(Animal.prototype)
//Object.create(Animal.prototype) 创建一个空对象 空对象.__proto__ 指向Animal 
//Dog.prototype 通过该空对象获取了animal的方法
```

注意！Dog.prototype的方法必须在Object.create()之后不然会被覆盖。

然后把constructor指向自己的ok了。

```js
Dog.prototype.constructor = Dog
```

### 总结

完整版如下

```js
fuction Animal(color) {
    this.color = color
}
Animal.prototype.move = function() {}

function Dog(color,name) {
    //获取属性
    Animal.call(this,color)
    //Animal.apply(this,arguments)多个属性用apply
    this.name = name
}
//获取方法
Dog.prototype = Object.create(Animal.prototype)
Dog.prototype.constructor = Dog
```

## class

es6推出class之后就方便了，跟java类似。

```js
class Animal{
	constructor(color) {
		this.color = color
	}
	move(){}
}
class Dog extends Animal {
	constructor(color,name){
		super(color)
		this.name = name
	}
	say() {}
}
```

##  总结

继承就是要一个类的属性和方法。es6推出class后，使用它继承就可以了。

