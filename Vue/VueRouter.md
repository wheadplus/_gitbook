# VueRouter

就是Vue推出的一个官方路由管理器。

## 基础使用

```js
//跳转
<router-link to="/">Home</router-link> |
<router-link :to="{path: '/about',query: {name: '123'}}">About</router-link>

//渲染出口
<router-view></router-view>

//vue.$route 获取路由参数
vue.$route.query.id
//vue.$router 调用路由方法
vue.$router.go()
vue.$touter.push()
```

## 路由守卫

在路由跳转前后对路由进行操作。

例如将

- 异常url转移到404页面。
- 权限限制，当前用户不能访问的跳转404。
- 打开新页面。

这里只拿`beforeEach`举例

```js
const router = new VueRouter({.})

router.beforeEach((to,from,next) => {
	//例如权限限制
})
```

目前用到的栗子

```js
router.beforeEach((to, from, next) => {
    /* 公共路由 */
    let commonArray = ['/login', '/home',,'/404'];
    //登陆时将用户可访问路由添加在本地localStorage，路由跳转前权限限制。
    let allRoute = commonArray.concat(JSON.parse(localStorage.getItem('routeArr')));
    if (allRoute.contains(to.path)) {/* 是否是公共路由 */
        if (to.path == '/onemap') {
            //特殊页面，特殊处理
           window.open('#/onemap', '_blank');
        } else {
            next()
        }
    } else {
        next('/404');
    }
})
```

## 路由懒加载

> 可以将异步组件定义为返回一个 Promise 的工厂函数 。

一般vue-cli生成的模板里就有得参考。

```js
const router = new VueRouter({
  routes: [
    { path: '/foo', component: () => import('./foo.vue') }
  ]
})
```

## 

## 参考

[vueRouter官网](https://router.vuejs.org/zh/installation.html)