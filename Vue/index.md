# 响应式原理

Vue 使用 `Object.defineProperty` 把`data`中属性转换为 `getter/setter`

```js
var data = {}
undefined
var _name = 'jim'
//通过Object.defineProperty做了个映射的关系
Object.defineProperty(data,'name',{
    get() {return _name},
    set(value) {
        _name = value
        console.log('更新ui')
    }
})

data.name  // jim
_name // jim
data.name = 'coco'  //调用set，这里可以更新ui
//更新ui
_name // coco


```

### 缺点

新增属性没法触发`set`，也就没有响应式刷新

```js
data.color = 'red' //新增属性没法触发set，也就没有响应式刷新
"red"
```

## vue提供的解决方法

对于已经创建的实例，`Vue` 不允许动态添加根级别的响应式属性。但是，可以使用 `Vue.set(object, propertyName, value)` 方法向嵌套对象添加响应式属性。

```js
Vue.set(vm.someObject, 'b', 2)
```

## Vue3.0新方法Proxy

> **Proxy** 对象用于定义基本操作的自定义行为（如属性查找、赋值、枚举、函数调用等）。

`es6`中新增`Proxy`，使用`Proxy`代理对象。`Proxy`能监听到新增属性。

```js
var data = {name:"jim"}
var dataProxy = new Proxy(data,{
    get(target,key) {
        if(key === 'name') {
            return data.name
        }
    },
    set(target,key,value) {
        data[key] = value
        console.log("更新UI")
    }
})
dataProxy.name //"jim"
dataProxy.name = 'coco'  //更新UI

//新增的color也能监听到
dataProxy.color ='red' // 更新UI
```



## 总结

- `Object.defineProperty`把对象转换为`getter/setter`,当setter更新数据时更新UI
- 但是它无法监听到新增的属性
- Vue可以使用`Vue.set(object, propertyName, value)` 来新增属性，这样也能响应式更新
- `Proxy`为更好的解决方案



## 参考

- [Object.defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

- [Proxy MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)