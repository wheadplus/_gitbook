# 移动端适配

## 背景（why）

随着手机不断推出，不同屏幕尺寸下网页展示错误成为亟需解决的问题。

## 一些概念（what）

- `viewport `就是屏幕视窗

-  物理像素(`physical pixel`) 就是显示设备中一个最微小的物理部件
-  设备独立像素(`density-independent pixel`) 代表`css`像素
-  设备像素比(`device pixel ratio`) 也就是`dpr`
-  `设备像素比 ＝ 物理像素 / 设备独立像素`



## 怎么做？（how）

### Flexible方案

- 动态改写`<meta>`标签

- 给`html`元素添加`data-dpr`属性，并且动态改写`data-dpr`的值

- 给`html`元素添加`font-size`属性，并且动态改写`font-size`的值
- `css`中使用`rem`布局，文字保持`px`

```js
var metaEl = doc.createElement('meta'); 
var scale = isRetina ? 0.5:1; 
metaEl.setAttribute('name', 'viewport'); 
metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no'); 
if (docEl.firstElementChild) { 
    document.documentElement.firstElementChild.appendChild(metaEl); 
} else { 
    var wrap = doc.createElement('div'); 
    wrap.appendChild(metaEl); 
    documen.write(wrap.innerHTML); 
}
```



### 在vue中使用vw方案

1. 安装插件

   ```
   cnpm i cssnano cssnano-preset-advanced postcss-aspect-ratio-mini postcss-cssnext postcss-import postcss-px-to-viewport postcss-url postcss-viewport-units postcss-write-svg -D
   ```

2. `package.json` 配置 `postcss`

   设计稿宽高在这里设置

   ```
   "postcss": {
       "plugins": {
         "postcss-import": {},
         "postcss-url": {},
         "postcss-aspect-ratio-mini": {},
         "postcss-write-svg": {
           "utf8": false
         },
         "postcss-cssnext": {},
         "postcss-px-to-viewport": {
           "viewportWidth": 375,
           "viewportHeight": 667,
           "unitPrecision": 3,
           "viewportUnit": "vw",
           "selectorBlackList": [
             ".ignore",
             ".hairlines"
           ],
           "minPixelValue": 1,
           "mediaQuery": false
         },
         "postcss-viewport-units": {},
         "cssnano": {
           "preset": "advanced",
           "autoprefixer": false,
           "postcss-zindex": false
         }
       }
     },
   ```

3. `index.html`添加`buggyfill`（兼容性处理）
	
	```
	 <script src="//g.alicdn.com/fdilab/lib3rd/viewport-units-buggyfill/0.6.2/??viewport-units-buggyfill.hacks.min.js,viewport-units-buggyfill.min.js"></script>
	  <script>
	    window.onload = function () {
	      window.viewportUnitsBuggyfill.init({
	        hacks: window.viewportUnitsBuggyfillHacks
	      })
	    }
	  </script> 
	```

4. 页面还是用`px`就可以，编译后会转换为`vw`。100`vw` 等于设计稿宽度。1vw = 设计稿宽度/100。

5. 不需要转换的地方添加类名`.ignore`或`.hairlines`

   ```html
   <div class="box ignore"></div>
   ```

   

### 移动端1px问题

`border-image` 实现

```css
@svg 1px-border { 
    height: 2px; 
    @rect { 
        fill: var(--color, black);
        width: 100%;
        height: 50%; 
    } 
} 
.example { 
    border: 1px solid transparent; 
    border-image: svg(1px-border param(--color #00b1ff)) 2 2 stretch; 
}
```

`background-image`来实现

```css
@svg square { 
    @rect { 
        fill: var(--color, black); 
        width: 100%; 
        height: 100%; 
    } 
} 
#example { 
    background: white svg(square param(--color #00b1ff)); 
}
```



##  总结

- `meta`标签控制网页在移动端的缩放比例

- `flexible` 使用`rem`布局
- 随着`vw`被浏览器更多兼容，以后更多地使用`vw`去适配移动端

## 参考

[使用Flexible实现手淘H5页面的终端适配](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html?expire=1587093220&code=eHzApvhwSsI&sign=75d411212e4b2dd8a2a848648b4e571a#paywall)

[如何在Vue项目中使用vw实现移动端适配](https://www.w3cplus.com/mobile/vw-layout-in-vue.html?expire=1587091975&code=kwgZy2216WI&sign=ab67512fa9aebecead22b009ea7aeaa8#paywall)