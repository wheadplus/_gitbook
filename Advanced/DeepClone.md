## 如何实现深拷贝

首先`js`的基本类型有

- String
- Number
- Boolean
- Null
- underfnd
- Object
- Symbol

深拷贝需要能够复制以上的类型,对于引用类型（Object）也能复制完整对象，而不是只复制引用指针。

## JSON序列化反序列化

```js
JSON.parser(JSON.Stringify(xxxx))
```

### 缺点

不支持Function,环，正则，时间等特殊情况。

## 递归深拷贝

1. 能过复制基础类型的深拷贝

```js
//能过复制基础类型的深拷贝
function deepClone(source) {
  if (source instanceof Object) {
    let dist
    if (source instanceof Array) {
      dist = new Array()
    } else if (source instanceof Function) {
      dist = function () {
        return source.apply(this, arguments)
      }
    } else {
      dist = new Object()
    }
    for (let key in source) {
      dist[key] = deepClone(source[key])
    }
    return dist
  } else {
    // console.log(typeof source, source)
    return source
  }
}

module.exports = deepClone
```

2.能够复制环、正则、date，过滤原型

```js

//能够复制环、正则、date，过滤原型
//cache全局，会被污染。所以使用对象的方式，把cache单独使用。
let cache = []

function deepClone(source) {
  if (source instanceof Object) {
    let cacheDist = findCache(source)
    if (cacheDist) {
      //有缓存
      return cacheDist
    } else {
      //无缓存

      let dist
      if (source instanceof Array) {
        dist = new Array()
      } else if (source instanceof Function) {
        dist = function () {
          return source.apply(this, arguments)
        }
      } else if (source instanceof RegExp) {
        //source、flags 为 源模式文本和标志
        dist = new RegExp(source.source, source.flags)
      } else if (source instanceof Date) {
        dist = new Date(source)
      } else {
        dist = new Object()
      }
      cache.push([source, dist]) //添加到缓存
      for (let key in source) {
        if (source.hasOwnProperty(key)) { // 跳过原型
          dist[key] = deepClone(source[key])
        }
      }
      return dist
    }
  } else {
    // console.log(typeof source, source)
    return source
  }
}

//cache 保存 [source,copy]
function findCache(source) {
  for (let i = 0; i < cache.length; i++) {
    if (cache[i][0] === source) {
      return cache[i][1]
    }
  }
  return undefined
}

module.exports = deepClone
```

3.独立缓存，防止cache互相污染。

```js
class DeepCloner {
  constructor() {
    this.cache = []
  }
  clone(source) {
    if (source instanceof Object) {
      let distCache = this.findCache(source)
      if (distCache) {
        return distCache
      } else {
        let dist
        if (source instanceof Array) {
          dist = new Array()
        } else if (source instanceof Function) {
          dist = function () {
            // arguments 函数参数 ，使用call的话，  ...arguments
            return source.apply(this, arguments)
          }
        } else if(source instanceof RegExp) {
          //.source .flag 为正则的属性 
          dist = new RegExp(source.source, source.flags)
        } else if(source instanceof Date) {
          dist = new Date(source)
        }else {
          dist = new Object()
        }
        this.cache.push([source, dist]) //push [source, dist] 是为了findCache()比较，
        for (let key in source) {
          if (source.hasOwnProperty(key)) { //  跳过原型
            dist[key] = this.clone(source[key])
          }
        }
        return dist
      }
    }
    return source
  }

  findCache(source) {
    for (let i = 0; i < this.cache.length; i++) {
      if (this.cache[i][0] === source) {
        return this.cache[i][1]
      }
    }
    return undefined
  }
}

module.exports = DeepCloner
```



## 总结

深拷贝的要点：

- 递归
- 判断类型
- 检查环（也叫循环引用）
  - 环 `obj.self = obj`
- 需要忽略原型