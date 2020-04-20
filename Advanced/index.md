# 

## 闭包

如果在函数里面可以访问外面的变量，那么这个函数+这些变量 = 闭包



### 闭包+时间

请问下面打印除什么？

```js
for(var i=0;i<6;i++) {
    setTimeout(
    	() => console.log(i)
    )
}
```

6个6。因为六个函数公用一个 i



如果需要打印0，1，2，3，4，5

```js
for(let i= 0;i<6;i++) {
    setTimeout(
    	() => console.log(i)
    )
}
```



### 总结

闭包的作用：

- 生成局部变量。

## this 的确定

```js
let length = 10
function fn(){
    console.log(this.length)
}
//fn.call(undefined, this.length)
let obj = {
    length: 5,
    method(fn){
        fn.call(obj,arguments[0]())
        fn()arguments[0]() 
    }
}  
obj.method(fn, 1)// 输出什么

```

