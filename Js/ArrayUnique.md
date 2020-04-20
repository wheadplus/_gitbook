# 数组去重

1. set去重

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

然后再转数组，就可以去重

```js
var array = [1,2,1,1,"1"]
function unique(array) {
    return Array.from(new Set(array))
}
unique(array)  //[1,2,"1"]
```

或

```js
function unique(array) {
    return [...new Set(array)]
}
```

2. 遍历

遍历旧数组，如果新数组内没有旧数组元素就添加，最后返回新数组

```js
function unique(arr) {
    let result = []
    arr.map(el => {
        if(result.indexOf(el) == -1) {
            result.push(el)
        }
    })
    return result
}
var z = [1,1,1,2,2,2,3,3,3,1,2,3]
unique(z) //[1,2,3]
```



#  数组降重

就是要把多个层级的数组拍平成一个层级

```js
[1, [2], [3, [[4]]]] 
//[1,2,3,4]
```

递归

```js
function flatten(arr) {
    var newArr = []
    function _flat(arr) {
        arr.forEach(value => {
            if(Array.isArray(value)) {
                _flat(value)
            } else {
                newArr.push(value)
            }
        })
    }
    _flat(arr)
    return newArr
}
flatten(arr) // [1, 2, 3, 4]
```

