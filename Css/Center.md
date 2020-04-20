# 元素居中

## 水平居中

1. [行内元素text-aligin](https://jsbin.com/fiwodegeqa/1/edit?html,css,js,output)

```css
.wrapper {
  text-align:center;
}
```

1. [块级元素margin: 0 auto](https://jsbin.com/mikotos/edit?html,css,output)

```css
.content {
  margin:0 auto;
}
```







## 垂直居中

1. [绝对定位](https://jsbin.com/macayoc/1/edit?html,css,output)

```css
.wrapper {
  position:relative;
}

.content {
  position: absolute;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
}
```

2. [flex](https://jsbin.com/sakuyav/edit?html,css,output)

```css
.wrapper {
  display: flex;  /* 弹性布局 */
  align-items: center;  /* 垂直居中 */
  justify-content: center;  /* 水平居中 */
}
```

3.[行内元素单行居中](https://jsbin.com/balunem/1/edit?html,css,output)

注意是单行！

```css
.wrapper {
  height:40px;
  line-height: 40px;
  text-align: center;
}
```

