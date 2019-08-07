## vue中， url变了，但视图没有更新

当在一个SPA里时，你很可能会想着在视图里重复利用一些组件。假设你现在在一个博客文章页面上，然后你想从那个页面跳到另一篇文章上，你会期望相应的内容也改成新的文章的内容，但它却没有变化。

这往往是复用同一个组件的结果，vue还是用了之前的一个实例，这时候组件里`this.$route`是变了，但是相应的那些生命周期事件，比如created(), beforeMounted() 和 mounted()，它们就没有被重新触发。
这个问题，一般有两种解决办法：

要强制vue创建一个新的组件实例，可以在`<router-view>`设置一个unique key：

```js
<router-view :key="$route.fullPath">
```

或者你也可以设置个watch函数，当route路由变了的时候，就触发相应逻辑：

```js
watch: {
    "$route.params.somevalue": {
        handler(somevalue) {
            // do stuff
        },
        immediate: true
    }
}
```
---

## 安装上VuePerformanceDevtool（vue性能开发工具）

这个Chrome扩展可以让你检测vue组件的性能，也是一个非常有用的工具，可以通过这个链接安装：[//chrome.google.com/webstore/detail/vue-performance-devtool/koljilikekcjfeecjefimopfffhkjbne](//chrome.google.com/webstore/detail/vue-performance-devtool/koljilikekcjfeecjefimopfffhkjbne)

安装好了，你得在代码里加上这么一句，才能启用它：

```js
Vue.config.performance = true;
```

记得要将其加在new Vue实例之前，当然了，这样的话，你生产环境上也就开启这个工具了，这往往不是我们想要的，你可以基于环境监测来决定是否开启这个，可以用下面的代码实现：

```js
Vue.config.performance = process.env.NODE_ENV !== 'production'
```