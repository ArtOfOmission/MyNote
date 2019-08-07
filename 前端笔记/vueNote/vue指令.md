
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

---

# <font color=#42b983>1.2 列表渲染</font>

## <font color=#42b983># v-for</font>

我们可以用 v-for 指令基于一个数组来渲染一个列表。v-for 指令需要使用 item in items 形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名。

### 迭代整数

```html
<div id="app">
  <ul>
    <li v-for="n in 10">
     {{ n }}
    </li>
  </ul>
</div>
```

### 迭代列表

```html
<ul id="app">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
```

> v-for 还支持一个可选的第二个参数，即当前项的索引。

```html
<ul id="app">
  <li v-for="(item, index) in items">
    {{ index }} - {{ item.message }}
  </li>
</ul>
```

```javascript
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

> 也可以用 of 替代 in 作为分隔符，因为它更接近 JavaScript 迭代器的语法：

```html
<div v-for="item of items"></div>
```

### 迭代对象

```html
<ul id="v-for-object" >
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

> 也可以提供第二个的参数为 property 名称 (也就是键名)： 

```html
<div v-for="(value, name) in object">
  {{ name }}: {{ value }}
</div>
```

> 还可以用第三个参数作为索引：

```html
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```

```javascript
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'cys',
      published: '2019-08-06'
    }
  }
})
```

### 过滤与排序

有时，我们想要显示一个数组经过过滤或排序后的版本，而不实际改变或重置原始数据。在这种情况下，可以创建一个计算属性，来返回过滤或排序后的数组。

```html
<div id="app">
    <ul>
        <li v-for="(item,index) in sortItems">
            {{item}}：{{index}}
        </li>
    </ul>
</div>
```

```javascript
var app1 = new Vue({
            el: "#app",
            data: {
                items: [123, 443, 223, 12, 32, 23, 12],
                books: [{
                        name: "唱片奇迹行",
                        price: 48.00
                    },
                    {
                        name: "大话数据结构",
                        price: 36.00
                    },
                    {
                        name: "寻找幸福",
                        price: 57.00
                    },
                ],
            },
            computed: {
                sortItems: function () {
                    //console.log('pass');
                    //return this.items.sort(sortNumber); //sortNumber-正序，sortNumberDesc-倒序
                    return this.items.concat().sort(sortNumber); //sortNumber-正序，sortNumberDesc-倒序

                    //过滤
                    //return this.items.filter(function (number) {
                      //return number % 2 === 0
                    //});

                },
                sortBooks: function () {
                    return sortArrObjectsByKey(this.books.concat(),"price");
                }

            },
            methods: {
                sortItems2: function () {
                    //console.log('pass2'); 
                    //concat() 先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组
                    //return this.items.sort(sortNumberDesc);//sortNumber-正序，sortNumberDesc-倒序
                    return this.items.concat().sort(sortNumberDesc);
                },
            },
        });

```

```javascript

//数组排序方法
function sortNumber(a, b) {
    return a - b;
}
//数组排序方法（倒序）
function sortNumberDesc(a, b) {
    return b - a;
}

//数组对象排序方法
function sortArrObjectsByKey(array, key) {
    return array.sort(function(a, b) {
        let x = a[key];
        let y = b[key];
        return (x < y) ? -1 : ((x > y) ? 1 : 0);
    }) ;
}
```

### 在 ```<template>``` 上使用 v-for

类似于 v-if，你也可以利用带有 v-for 的 ```<template>```来循环渲染一段包含多个元素的内容。比如：

```javascript
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

# <font color = #42b983> 1.3 事件处理</font>


可以用 v-on 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。

## 监听事件

```html
<div id="app">
    <span v-text="point"></span>
    <button v-on:click="point++" class="btn_confirm">加分</button>
    <button v-on:click="point--" class="btn_confirm">减分</button>
</div>
```

## 监听事件处理方法

```html
<div id="app">
    <span v-text="point"></span>
    <button v-on:click="ExtraPoints" class="btn_confirm">加分</button>
    <button v-on:click="DeductionOfPoint" class="btn_confirm">减分</button>
    <input type="text" v-on:keyup.enter="onEnter" v-model="second_point"
    onkeyup="value=value.replace(/[^\d]/g,'')"
    onblur="value=value.replace(/[^\d]/g,'')">

</div>
```

## 在内联 JavaScript 语句中调用方法

```html
<div id="app">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
```

## 访问原始的 DOM 事件

```html
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

```

```javascript
var app = new Vue({
    el: "#app",
    data: {
        point: 0
    },
    methods: {
        ExtraPoints: function () {
            this.point++;
        },
        DeductionOfPoint: function () {
            this.point--;
        },
        onEnter: function () {
            if (this.second_point == "" || !this.second_point) return;
            this.point += parseInt(this.second_point);
        },
        say: function (message) {
          alert(message)
        },
        warn: function (message, event) {
          // 现在我们可以访问原生事件对象
          if (event) event.preventDefault()
          alert(message)
        }
    }
});
```

## 事件修饰符

在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 v-on 提供了事件修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。

- .stop
- .prevent
- .capture
- .self
- .once
- .passive

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>

```
---

# <font color = #42b983> 1.4 表单输入绑定</font>

你可以用 v-model 指令在表单 ```<input>、<textarea> 及 <select> ``` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 v-model 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

## 文本

```html
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

##  多行文本

```html
<span>Multiline message is:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<br>
<textarea v-model="message" placeholder="add multiple lines"></textarea>

```

## 多个复选框，绑定到同一个数组：

```html
<input type="checkbox" id="A" value="A" v-model="word_array">
<label for="A">A</label>
<input type="checkbox" id="B" value="B" v-model="word_array">
<label for="B">B</label>
<input type="checkbox" id="C" value="C" v-model="word_array">
<label for="C">C</label>
<input type="checkbox" id="D" value="D" v-model="word_array">
<label for="D">D</label>
<p>{{word_array}}</p>
```

## 单选按钮

```html
<input type="radio" id="man" name="sex" value="man" v-model="sex">
<label for="man">man</label>
<input type="radio" id="woman" name="sex" value="woman" v-model="sex">
<label for="woman">woman</label>
<br>
<span>{{sex}}</span>
```


```js
var app = new Vue({
    el: "#app",
    data: {
        message: "hello",
        isTrue: true,
        word_array: [],
        sex:"man",
    }
});
```

## 选择框

```html
<select v-model="selected">
  <option disabled value="">请选择</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selected: {{ selected }}</span>
```

```js
new Vue({
  el: '...',
  data: {
    selected: ''
  }
})
```

## 用 v-for 渲染的动态选项：

```html
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
```

```js
new Vue({
  el: '...',
  data: {
    selected: 'A',
    options: [
      { text: 'One', value: 'A' },
      { text: 'Two', value: 'B' },
      { text: 'Three', value: 'C' }
    ]
  }
})
```

---
# <font color = #42b983> 1.5 Class 与 Style 绑定</font>


# 绑定 HTML Class

## <font color = #42b983> 对象语法</font>


我们可以传给 v-bind:class 一个对象，以动态地切换 class：

```html
<div v-bind:class="{ active: isActive }"></div>
```

你可以在对象中传入更多属性来动态切换多个 class。此外，v-bind:class 指令也可以与普通的 class 属性共存。当有如下模板:

```html
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
```

```javascript
data: {
  isActive: true,
  hasError: false
}
```

结果渲染为：

```html



```


绑定的数据对象不必内联定义在模板里：

```html
<div v-bind:class="classObject"></div>
```

```javascript
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```

我们也可以在这里绑定一个返回对象的计算属性。这是一个常用且强大的模式：

```html
<div v-bind:class="classObject"></div>
```

```javascript
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}

```

## <font color = #42b983> 数组语法</font>

我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：

```html
<div v-bind:class="[activeClass, errorClass]"></div>
```

```javascript
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

渲染结果：

```html

```

使用三元表达式切换class：

```html
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

不过，当有多个条件 class 时这样写有些繁琐。所以在数组语法中也可以使用对象语法：

```html
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```


# 绑定内联样式


## 对象语法:

v-bind:style 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名：

```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

```js
data: {
  activeColor: 'red',
  fontSize: 30
}
```

直接绑定到一个样式对象:

```html
<div v-bind:style="styleObject"></div>
```

```js
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

> 同样也可以用计算属性


## 数组语法

v-bind:style 的数组语法可以将多个样式对象应用到同一个元素上：

```html
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```
---
# <font color = #42b983>1.6 v-text与v-html </font>


```html
 <div id="app">
    <!--使用v-text标签更友好，当js丢失或者因网速慢没有及时加载出来时，直接在页面显示{{....}}的问题-->
    <span>{{message}}</span> = <span v-text="message"></span> <br/>
    <!-- 需要注意的是：在生产环境中动态渲染HTML是非常危险的，因为容易导致XSS攻击。所以只能在可信的内容上使用v-html，永远不要在用户提交和可操作的网页上使用-->
    <span v-html="todo"></span>
    <br>
    <p>“Mustache”语法：{{txthtml}}</p>
    <p>v-html指令：<span v-html="txthtml"></span></p>
</div>

```

```js
var vue = new Vue({
    el:'#app',
    data:{
        message:'Hello World!!!!!',
        todo:'<h2>Hello World!</h2>',
        txthtml:'<span style="color:red;">v-html显示</span>',
    }
});
```


# <font color = #42b983>1.7 v-pre & v-cloak & v-once 指令 </font>

```html
<div id="app">
    <p> {{message}}</p>
    <span>在模板中跳过vue的编译，直接输出原始值</span>
    <p v-pre>
        <!--在模板中跳过vue的编译，直接输出原始值-->
        {{message}}
    </p>
    <span>v-cloak 这个指令是防止页面加载时(如网速缓慢。。。)出现 vuejs 的变量名而设计的</span>
    <p v-cloak>
        {{message}}
    </p>
    <span>在第一次DOM时进行渲染，且只会渲染一次</span>
    <p v-once>
        <!--在第一次DOM时进行渲染，且只会渲染一次-->
        {{message}}
    </p>
</div>
```

```js

var app = new Vue({
    el: "#app",
    data: {
        message: "hi,wenyi!",
    }

});

```
