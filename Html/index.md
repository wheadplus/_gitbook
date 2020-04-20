# html语义化

## 背景

在开发过程中，你肯定见过或者自己使用过类似的代码。简单来说就是 一个`div`写到底。

```html
<html>
    <body>
        <div id="header">
            <div class="h_tittle">             
            </div>
            <div class="h_location">
            </div>
        </div>
        
        <div id="main">
            
        </div>
        
        <div id="footer">
            
        </div>
    </body>
</html>
```

写的时候挺舒服的，但是当页面结构复杂的时候，命名各有各的习惯。很难直观地看出结构，所以推出了html语义化，让开发人员更规范。



## 是什么

html语义化就是使用恰当的html标签和class类名让页面结构更清晰。而且方便浏览器识别。

总结就是：

- 用恰当的标签而不是通篇`div`
- 页面结构化

## 怎么做

举个例子，如下用恰当的标签干恰当的事情，结构化。

```html
<html>
    <body>
        <article>
            article = 独立模块
        	<header>
                 header = 头部
                <nav>nav = 导航栏</nav>
            </header>
            <main>
                main = 主要内容
                <section>
                    section = 章节
                    <h5>
                        h5 = 标题
                    </h5>
                    <p>p = 段落</p>
                    <figure>figure = 图例</figure>
                    <figcaption>figcaption = 图例的相关说明</figcaption>
                </section>
                <aside>
                    aside = 侧边栏
                </aside>
            </main>
            
            <footer>footer = 底部</footer>
        </article>
    </body>
</html>
```



[详细标签查询MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)