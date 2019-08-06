
#  <font color=#42b983>Vue.js</font>

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

```!
Vue 不支持 IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有兼容 ECMAScript 5 的浏览器。
```

引入方式

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

---


# <font color=#42b983>Vue 实例</font> 

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统
每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：

```javascript

// 定义一个数据对象
var data = { a: 1 }

var vm = new Vue({
  // 选项
  el："#app",
  data: data
})
```

##  <font color=#42b983># 文本插值</font>


```html
<div id="app">
  {{ message }}
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

---

#  <font color=#42b983>vue指令</font>

指令 (Directives) 是带有 v- 前缀的特殊特性。指令特性的值预期是单个 JavaScript 表达式 (v-for 是例外情况)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

![vue指令](/assets/vue指令.jpg)

# <font color=#42b983>1.1 条件渲染</font>

## <font color=#42b983># v-if、v-else-if、v-else</font>

v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。

```html
<div id="app1">
    <div v-if="isLogin">你好，陈彦森！</div>
    <div v-else>请登录！</div>
</div>
```

因为 v-if 是一个指令，所以必须将它添加到一个元素上。但是如果想切换多个元素呢？ 此时可以把一个```<template>``` 元素当做不可见的包裹元素，并在上面使用 v-if。最终的渲染结果将不包含 ```<template>``` 元素。
 
```html
<div id="app1">
    <template v-if="type=='A'">
        <h1>it's A</h1>
        <p>Paragraph 1</p>
        <p>Paragraph 2</p>
    </template>
    <div v-else-if="type=='B'">
        it's B
    </div>
    <template v-else-if="type=='C'">
        it's C
    </template>
    <template v-else="type=='C'">
        Other
    </template>
</div>

```

```javascript
var app1 = new Vue({
    el: "#app1",
    data: {
        isLogin: true,
        type:"A",
    }
});

```


### 用 <font color=#42b983>key</font> 管理可复用的元素


Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。这么做除了使 Vue 变得非常快之外，还有其它一些好处。例如，如果你允许用户在不同的登录方式之间切换：

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>
```

那么在上面的代码中切换 loginType 将不会清除用户已经输入的内容。因为两个模板使用了相同的元素，```<input>``` 不会被替换掉——仅仅是替换了它的 placeholder。
当然，也可以使”两个元素完全独立，不复用它们“，只需要添加一个具有唯一值的key属性即可。

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```
> 注意，<label> 元素仍然会被高效地复用，因为它们没有添加 key 属性。

---

## <font color=#42b983># v-show</font>

另一个用于根据条件展示元素的选项是 v-show 指令

```html
<div v-show="isShow">v-show指令</div>
```
不同的是带有 v-show 的元素始终会被渲染并保留在 DOM 中。v-show 只是简单地切换元素的 CSS 属性 display。


<font color=F93929 >注意，v-show 不支持``` <template> ```元素，也不支持 v-else。</font>

## <font color=F93929 >v-if</font> VS <font color=F93929 >v-show</font>


>v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

>v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

>相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

>一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

