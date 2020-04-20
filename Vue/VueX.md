# #  Vuex 是什么？

>Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 [devtools extension](https://github.com/vuejs/vue-devtools)，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。



也就是官方的状态管理中心。

# 什么时候要用Vuex？

- 中大型应用
- 需要管理状态
- 状态太多，eventBus不能满足



# 概念和怎么用？

##  State

就是存放基础状态的地方

声明 state 的参数

```js
 state: {
    infos: {
      age: 18,
      sex: '女性',
      firstName: '张',
      lastName: '三'
    }
  },
```

在组件中获取state

```js
this.$store.state.students
```

## Getter

相当于计算属性，对state的过滤或条件限制

```js
getters: {
    totalName: state => {
      return state.infos.firstName +  state.infos.lastName
    }
  },
```

在组件中获取Getter

```js
computed: {
    totalName() {
      return this.$store.getters.totalName
    }
  },
```

## Mutation

对state的数据进行操作修改。

```js
 mutations: {
    addAge(state) {
     state.infos.age++
    }
  },
```

在组件中只需调用 Mutation 事件

```js
addAge() {
      this.$store.commit('addAge')
},
```

但Mutation 只限于同步函数。异步操作须在Action中使用

## Action

对mutation 进行操作m.接受的参数是context，用来出发mutaion

```js
 actions: {
    addAgeAction(context) {
      // context.commit('addAge')
      //异常操作才使用action，如请求接口后
      setTimeout(() => {
        context.commit('addAge')
      }, 1000);
    }
  },
```

调用 Action

```js
addAgeAction() {
      this.$store.dispatch('addAgeAction')
}
```

## Module

Module就是模块，但状态太多的时候，区分不同模块。

```js
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

```

