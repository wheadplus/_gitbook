

# 组件通信

## 父子组件

父向子 ，通过props传递数据就可以。

子向父，由于vue是单向数据流。这个过程麻烦点。

1. 父组件自定义事件监听儿子传参事件

```vue
<btn-compnent @change="handleTotal"></btn-compnent>
```

2. 子组件通过`Vue.emit()`触发自定义事件`change`并传递参数。

```vue
methods: {
 	emitDataToPapa() {
		this.$emit('change','data')
	}
}
```

3. 在父组件处理儿子传参事件

```js
methods: {
  handleTotal(sonMsg) {
    console.log(sonMsg)
  }
}
```

## 非父子组件通信

使用一个空的`Vue`实例作为中央事件总线：

```vue
var bus = new Vue()
```

在组件A创建监听事件

```js
bus.$on('eventName',function(data){
    //触发后的数据操作
})
```

触发组件B中的事件，传递参数

```js
bus.$emit('eventName','dataToA')
```

