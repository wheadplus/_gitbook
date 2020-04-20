# 数组方法

## 基本使用

添加

- `push(el)`

- `unshift(el)`

删除

- `splice(index,delectEl,addEl)`

```js
var arr = [3, 4, 5, 6]

var arr2 = arr.splice(1, 2) //从index1开始删除两位
arr // [3, 6]
arr2 // [4, 5]
arr.splice(1,0,7,8,9)//从index1开始删除0位，新增2位

arr //[3, 7, 8, 9, 6]
arr.splice(2,3) //从index2开始删除3位
arr// [3,7]
```



序列

- `reverse()`倒序
- `sort()`排序

```js
var arr = [3, 5, -1, 18, 9, 27]

arr.sort() //默认，元素按照转换为的字符串的各个字符的Unicode位点进行排序。
(6) [-1, 18, 27, 3, 5, 9]
arr.sort((a,b) => a - b) //自定义排列
```



