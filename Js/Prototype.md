# 原型和原型链

原型表示一个类/对象的继承关系。

```js
function Person(name,age) {
    this.name = 'jim'
    this.age = age
}
Person.prototype.sayName = function() {
	console.log(this.name)
}
var p1 = new Person()
p1.sayName()

```

![原型链.png](http://ww1.sinaimg.cn/mw690/8afe7f49gy1gdvh7a9zrbj20c608njrg.jpg)

- 通过函数定义了类 `Person`, 类（函数）自动获取熟悉`prototype`
- 每个类的实例如`p1`都会有个内部属性`__proto__`

## 原型链

原型链就是对象上的`__proto__`，通过原型链可以获得基础方法。

```
var str = [1,2,3,4]
str.push()
```

.push() 方法就是通过 `str.__proto__`获取的。通过constructor可以看出它的原型是Array。

![原型链2.png](http://ww1.sinaimg.cn/mw690/8afe7f49gy1gdvh7jkj99j20ca0iegm1.jpg)



`.toString`则是通过`Array.__proto__`找到的。

![原型链3.png](http://ww1.sinaimg.cn/mw690/8afe7f49gy1gdvh7qzwhfj20cj0hr3z2.jpg)

## 总结

- 实例通过`__proto__`获取类上的方法。

- 可以通过`__proto__.constructor`可以知道实例的父类

  