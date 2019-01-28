Vue.js 笔记
=========

## 目录

- [目录](#目录)
- [Vue基础](#Vue基础)
  - [一、Vue.js是什么](#一vuejs是什么)
  - [二、资源](#二资源)
  - [三、Vue实例](#三vue实例)
  - [四、模板语法](#四模板语法)
    - [1. 插值](#1-插值)
    - [2. 缩写](#2-缩写)
      - [2.1 v-bind 缩写](#21-v-bind-缩写)
      - [2.2 v-on 缩写](#22-v-on-缩写)
  - [五、计算属性、方法、侦听器](#五计算属性方法侦听器)
    - [1. 计算属性](#1-计算属性)
    - [2. 方法](#2-方法)
    - [3. 侦听器](#3-侦听器)
    - [4. 计算属性的getter和setter](#4-计算属性的getter和setter)
  - [六、Vue中的样式绑定](#六vue中的样式绑定)
    - [1. Html Class](#1-html-class)
      - [1.1 对象语法](#11-对象语法)
      - [1.2 数组语法](#12-数组语法)
    - [2. 内联样式 Style](#2-内联样式-style)
      - [2.1 对象语法](#21-对象语法)
      - [2.2 数组语法](#22-数组语法)
      - [2.3 自动添加前缀](#23-自动添加前缀)
    - [3. 多重值](#3-多重值)
  - [七、Vue中的条件渲染](#七vue中的条件渲染)
    - [1. 指令](#1-指令)
    - [2. 指令的比较](#2-指令的比较)
    - [3. 用key管理可复用的元素](#3-用key管理可复用的元素)
  - [八、Vue中的列表渲染](#八vue中的列表渲染)
    - [1. 指令v-for](#1-指令v-for)
    - [2. key](#2-key)
    - [3. 数组更新检测](#3-数组更新检测)
      - [3.1 变异方法](#31-变异方法)
      - [3.2 替换数组](#32-替换数组)
      - [3.3 注意事项](#33-注意事项)
    - [4. 对象更改检测注意事项](#4-对象更改检测注意事项)
  - [九、事件处理](#九事件处理)
    - [1. 监听事件](#1-监听事件)
    - [2. 事件处理方法](#2-事件处理方法)
    - [3. 内联处理器中的方法](#3-内联处理器中的方法)
    - [4. 事件修饰符](#4-事件修饰符)
    - [5. 按键修饰符](#5-按键修饰符)
    - [6. 系统修饰键](#6-系统修饰键)
    - [7. exact修饰符](#7-exact修饰符)
    - [8. 鼠标修饰符](#8-鼠标修饰符) 
  - [十、表单的输入绑定](#十表单的输入绑定)
    - [1. 基础用法](#1-基础用法)
    - [2. 值绑定](#2-值绑定)
    - [3. 修饰符](#3-修饰符)
- [组件](#组件)
  - [一、组件基础](#一组件基础)
    - [1. 基本示例](#1-基本示例)
    - [2. 组件的复用](#2-组件的复用)
    - [3. 组件的组织](#3-组件的组织)
    - [4. 通过Prop向子组件传递数据](#4-通过Prop向子组件传递数据)
    - [5. 单个根元素](#5-单个根元素)
    - [6. 通过事件向父级组件发送消息](#6-通过事件向父级组件发送消息)
        - [6.1 使用事件抛出一个值](#61-使用事件抛出一个值)
    - [7. 通过插槽分发内容](#7-通过插槽分发内容)
    - [8. 动态组件](#8-动态组件)
    - [9. 解析DOM模板时的注意事项](#9-解析DOM模板时的注意事项)
  - [二、深入了解组件](#二深入了解组件)
    - [1. 组件注册](#1-组件注册)
      - [1.1 组件名](#11-组件名)
      - [1.2 全局注册](#12-全局注册)
      - [1.3 局部注册](#13-局部注册)
      - [1.4 模块系统](#14-模块系统)
    - [2. Prop](#2-组件的复用)
      - [2.1 Prop的大小写](#21-Prop的大小写)
      - [2.2 Prop类型](#22-Prop类型)
      - [2.3 传递静态或动态Prop](#23-传递静态或动态Prop)
      - [2.4 单向数据流](#24-单向数据流)
      - [2.5 Prop验证](#25-Prop验证)
        - [2.5.1 类型检查](#251-类型检查)
      - [2.6 非Prop的特性](#26-非Prop的特性)
        - [2.6.1 替换/合并已有的特性](#261-替换/合并已有的特性)
        - [2.6.2 禁用特性继承](#262-禁用特性继承)
    - [3. 自定义事件](#3-自定义事件)
      - [3.1 事件名](#31-事件名)
      - [3.2 自定义组件的 v-model](#31-自定义组件-v-model)
      - [3.3 将原生事件绑定到组件](#31-将原生事件绑定到组件)
      - [3.4 .sync 修饰符](#31-.sync-修饰符)
    - [4. 插槽slot](#4-插槽slot)
    - [5. 动态组件](#5-单个根元素)
    - [6. 异步组件](#6-通过事件向父级组件发送消息)
    - [7. 处理边界情况](#7-处理边界情况)
<!-- /TOC -->

<br>

# Vue基础

## 一、Vue.js是什么
- Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的**渐进式框架**。
- Vue 被设计为可以自底向上逐层应用。
- Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。
- 当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

<br>

## 二、资源
- 官方文档 [Vue.js](https://vuejs.org/index.html)
- Github [vuejs](https://github.com/vuejs)

<br>

## 三、Vue实例
一个 Vue 应用由一个通过`` new Vue ``创建的**根 Vue 实例**，以及可选的嵌套的、可复用的组件树组成
```javascript
var vm = new Vue({
  // 选项
})
```
<br>

## 四、模板语法
### 1. 插值
数据绑定最常见的形式就是使用“**Mustache**”语法 (**双大括号**)的文本插值：
```html
<span>Message: {{ msg }}</span>
```
还可以使用``v-text``指令：
```html
<span v-text="msg"></span>
```
若要插入原始HTML，则可以使用``v-html``指令：
```html
<span v-text="rawHtml"></span>
```
### 2. 缩写
对于一些频繁用到的指令来说，就会感到使用繁琐。同时，在构建由 Vue.js 管理所有模板的单页面应用程序 (SPA - single page application) 时，v- 前缀也变得没那么重要了。因此，Vue.js 为 v-bind 和 v-on 这两个最常用的指令，提供了特定简写：
#### 2.1 v-bind 缩写
```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>

<!-- 缩写 -->
<a :href="url"></a>
```
#### 2.2 v-on 缩写
```html
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>

<!-- 缩写 -->
<a @click="doSomething"></a>
```
<br>

## 五、计算属性、方法、侦听器
### 1. 计算属性
- **计算属性是基于它们的依赖进行缓存的**。
- 计算属性会立即返回之前的计算结果，而不必再次执行函数。只有在相关依赖发生改变时它们才会重新求值，
```vue
computed: {
  fullName: function () {
    return this.firstName + " " + this.lastName;
  }
}
```
> 为什么使用缓存？假设我们有一个性能开销比较大的计算属性 A，它需要遍历一个巨大的数组并做大量的计算。
> 然后我们可能有其他的计算属性依赖于 A 。
> 如果没有缓存，我们将不可避免的多次执行 A 的 getter！
> 如果你不希望有缓存，请用方法来替代。

### 2. 方法
每当触发重新渲染时，调用方法将总会再次执行函数。
```vue
methods: {
  fullName: function () {
    return this.firstName + " " + this.lastName;
  }
}	
```

### 3. 侦听器
Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：**侦听属性**.

当需要在数据变化时执行异步或开销较大的操作时，Vue 通过 **watch** 选项提供了一个更通用的方法，来响应数据的变化。
```vue
watch: {
  firstName: function() {
    console.log("computed one time");
    this.fullName = this.firstName + " " + this.lastName;
  },
  lastName: function() {
    console.log("computed one time");
    this.fullName = this.firstName + " " + this.lastName;
  }
}
```

### 4. 计算属性的getter和setter
```vue
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```
<br>

## 六、Vue中的样式绑定

🍃 [示例代码](https://github.com/yeyongzhen/vue_learning)

- 操作元素的 class 列表和内联样式是数据绑定的一个常见需求。
- 在将 v-bind 用于 class 和 style 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。
### 1. Html Class
#### 1.1 对象语法
- 可以传给 ``v-bind:class`` 一个对象
- 可以在对象中传入多个属性
- ``v-bind-class`` 可以与普通 class属性共存
- 绑定对象不必内联定义在模板里，可以是 data 的属性
- 可以绑定一个**返回对象的 计算属性**

#### 1.2 数组语法
- 可以把一个数组传给 ``v-bind:class``
- 可以用三元表达式，根据条件切换列表中的 class
- 在数组语法中也可以使用对象语法

### 2. 内联样式 Style
#### 2.1 对象语法
- ``v-bind:style``
- CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用单引号括起来) 来命名
- 直接绑定一个样式对象会更清晰
- 类似 Class，对象语法常常结合返回对象的计算属性使用。

#### 2.2 数组语法
- ``v-bind:style`` 的数组语法可以将多个样式对象应用到同一个元素上

#### 2.3 自动添加前缀
当 ``v-bind:style`` 使用需要添加**浏览器引擎前缀**的 CSS 属性时，如 ``transform``，Vue.js 会自动侦测并添加相应的前缀。


### 3. 多重值
从 2.3.0 起你可以为 ``style`` 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值，例如：
```HTML
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```
这样写只会渲染数组中最后一个被浏览器支持的值。

在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 ``display: flex``。

<br>

## 七、Vue中的条件渲染
### 1. 指令
- ``v-if``
- ``v-else-if``
- ``v-else``
- ``v-show``

### 2. 指令的比较
- 指令 ``v-else``，``v-else-if`` 必须紧跟在带 ``v-if`` 或 ``v-else-if`` 的元素之后
- 带有 ``v-show`` 的元素始终会被渲染并保留在 DOM 中。只是切换元素的 ``display`` 属性
- ``v-if`` 有更高的切换开销，而 ``v-show`` 有更高的初始渲染开销。
- 若需要**频繁**切换，则使用 ``v-show`` 比较好；
- 若运行时**条件很少改变**，则使用 ``v-if`` 较好

### 3. 用key管理可复用的元素
- Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。
- 给元素添加具有唯一值得 ``key``属性，可表达两个元素是独立的，不要复用它们
```html
<div id="app">
  <!-- input element without key -->
  <div v-if="loginType === 'username'">
    <label>Username</label>
  	<input placeholder="Enter your username">
  </div>
  <div v-else>
    <label>Email</label>
    <input placeholder="Enter your email address">
  </div>

  <!-- input element with key -->
  <div v-if="loginType === 'username'">
    <label>Username with key</label>
  	<input placeholder="Enter your username" key="username-input">
  </div>
  <div v-else>
    <label>Email with key</label>
  	<input placeholder="Enter your email address" key="email-input">
  </div>
</div>
```
```vuejs
new Vue({
  el: "#app",
  data: {
    loginType: 'username'
  }
});
```

<br>

## 八、Vue中的列表渲染
### 1. 指令``v-for``
- 我们用 ``v-for`` 指令根据一组数组的选项列表进行渲染。
- ``v-for`` 指令需要使用 ``item in items`` 形式的特殊语法，``items`` 是源数据数组并且 ``item`` 是数组元素迭代的别名。
- 在 ``v-for`` 块中，我们拥有对父作用域属性的完全访问权限。
- ``v-for`` 还支持一个可选的第二个参数为当前项的 **索引**。
- 可以用``of`` 替代 ``in`` 作为分隔符，它是最接近 JavaScript 迭代器的语法

### 2. ``key``
当 Vue.js 用 ``v-for`` 正在更新已渲染过的元素列表时，默认用 **就地复用** 策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素

这个默认的模式是高效的，但是只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 ``key`` 属性。理想的 ``key`` 值是每项都有的唯一 ``id``。

建议尽可能在使用 ``v-for`` 时提供 ``key``，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

因为它是 Vue 识别节点的一个通用机制，``key`` 并不与 ``v-for`` 特别关联，``key`` 还具有其他用途。

### 3. 数组更新检测
#### 3.1 变异方法
Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下:
- push() 
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

#### 3.2 替换数组
变异方法（mutation method），会改变这些方法调用的原始数组。

非变异方法（non-mutating method）方法，例如：``filter()``，``concat()``和``slice()``。这些不会改变原始数组，但总是返回一个新数组。

#### 3.3 注意事项
由于 JavaScript 的限制，Vue 不能检测以下变动的数组：
1. 当你利用索引直接设置一个项时，例如：``vm.items[indexOfItem] = newValue``
2. 当你修改数组的长度时，例如：``vm.items.length = newLength``

> 总结：改变数组的方式有3种：
> 1. 变异方法
> 2. 改变数组引用
> 3. set 方法

### 4. 对象更改检测注意事项
由于 JavaScript 的限制，**Vue不能检测对象属性的添加或删除**：
- 对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。
- 可以使用 ``Vue.set(object, key, value)`` 方法向嵌套对象添加响应式属性。
```js
var vm = new Vue({
  data: {
    userProfile:{
      name: 'Anika'
    }
  }
})

Vue.set(vm.userProfile, 'age', 27)
或者
vm.$set(vm.userProfile, 'age', 27)
```
为已有对象赋予多个新属性，例如使用 ``Object.assign()`` 或 ``_.extend()``。这种情况下，应该用两个对象的属性创建一个新的对象。
```js
vm.userProfile = Object.assign({}, vm.userProfile, {
    age: 27,
    favoriteColor: 'Vue Green'
})
```
🍃 [v-for with a Component case](https://github.com/yeyongzhen/vue_learning/tree/master/demo/index9.html)

<br>

## 九、事件处理
### 1. 监听事件
-  指令 ``v-on`` 用来监听 DOM 事件
```html
<button v-on:click="count += 1">Add</button>
```
```js
var vm = new Vue({
    el: "#app",
    data: {
        count: 0
    }
})
```

### 2. 事件处理方法
- 指令 ``v-on`` 可以接收一个需要调用的方法名称
```html
<button v-on:click="showMsg">Show</button>
```
```js
var vm = new Vue({
    el: "#app",
    data: {
        message: ''
    },
    methods: {
        showMsg: function () {
            this.message = 'Method Event Handlers'
        }
    }
})
```

### 3. 内联处理器中的方法
- 在内联 JavaScript 代码中调用方法
```html
<button v-on:click="say('Hello')">Say Hello</button>
```
```js
var vm = new Vue({
    el: "#app",
    data: {
        message: ''
    },
    methods: {
        say: function (message) {
            this.message = message
        }
    }
})
```
- 在内联语句中监听 原始DOM 事件
```html
<button v-on:click="warn('access the original dom!', $event)">warn</button>
```
```js
var vm = new Vue({
    el: "#app",
    data: {
        message: ''
    },
    methods: {
        warn: function (message, event) {
            if (event) {
                event.preventDefault()
            }
            alert(message);
        }
    }
})
```

### 4. 事件修饰符
- 方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节

Vue 提供的事件修饰符：
- ``.stop``
- ``.prevent``
- ``.capture``
- ``.self``
- ``.once``
- ``.passive``

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
> 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 
>
> ``v-on:click.prevent.self`` 会阻止所有的点击，而 
>
> ``v-on:click.self.prevent`` 只会阻止对元素自身的点击。

### 5. 按键修饰符
- Vue 允许为 ``v-on`` 在监听键盘事件时添加按键修饰符
```html
<!-- 只有在 `keyCode` 是 13 时调用 `vm.submit()` -->
<input v-on:keyup.13="submit">
```
Vue 为最常用的按键提供了别名：
- ``.enter``
- ``.tab``
- ``.delete``(捕获“删除”和“退格”键)
- ``.esc``
- ``.space``
- ``.up``
- ``.down``
- ``.left``
- ``.right``

```html
<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
```
- 通过全局 ``config.keyCodes`` 对象自定义按键修饰符别名
```js
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

### 6. 系统修饰键
用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器:
- ``.ctrl``
- ``.alt``
- ``.shift``
- ``.meta``

```html
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

### 7. ``.exact``修饰符
``.exact`` 修饰符允许你控制由精确的系统修饰符组合触发的事件。
```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

### 8. 鼠标修饰符
- ``left``
- ``right``
- ``middle``
这些修饰符会限制处理函数仅响应特定的鼠标按钮


<br>

## 十、表单的输入绑定
### 1. 基础用法
- 我们可以用 ``v-model`` 指令在表单 ``input``、``textarea`` 及 ``select`` 元素上创建双向数据绑定
- ``v-model`` 本质上不过是语法糖，负责监听用户的输入事件以更新数据
- ``v-model`` 始终将Vue实例的数据作为数据来源，所以初始值应该通过在 ``data`` 选项中声明

### 2. 值绑定
对于单选按钮，复选框及选择框的选项，v-model 绑定的值通常是静态字符串 (对于复选框也可以是布尔值)。
```html
<!-- 当选中时，`picked` 为字符串 "a" -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` 为 true 或 false -->
<input type="checkbox" v-model="toggle">

<!-- 当选中第一个选项时，`selected` 为字符串 "abc" -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```
但是有时我们可能想把值绑定到 Vue 实例的一个动态属性上，这时可以用 ``v-bind`` 实现，并且这个属性的值可以不是字符串。

### 3. 修饰符
- ``.lazy``
- ``.number``
- ``.trim``

```html
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >

<!-- 自动将用户输入的值转为数值类型 -->
<input v-model.number="age" type="number">

<!-- 自动过滤用户输入的首尾空白字符 -->
<input v-model.trim="msg">
```

<br>

# 组件
## 一、组件基础
### 1. 基本示例
```vue
// 定义一个名为 button-counter 的新组件
Vue.component('button-counter', {
  data: function() {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```
组件是可复用的 Vue 实例，且带有一个名字:该例中组件名是 ``<button-counter>``。可以在一个 Vue 根实例中，将该组件作为自定义元素来使用：
```html
<div id="app">
  <button-counter></button-counter>
</div>
```
```vue
new Vue({
  el: "#app"
})
```
### 2. 组件的复用
- 可以将组件进行任意次数的复用
- 每用一次组件，就会有一个 **新实例** 被创建
- 一个组件的 ``data`` 必须是一个函数，因此每个实例可以维护一份被返回对象的独立拷贝

### 3. 组件的组织
- 通常一个应用会以一棵嵌套的组件树的形式来组织
- 有两种组件的注册类型：**全局注册**和**局部注册**
- 全局注册的组件可以用在其被注册之后的任何新创建的 Vue 根实例，包括其组件树中的所有子组件的模板中

### 4. 通过Prop向子组件传递数据
- Prop 是你可以在组件上注册一些自定义特性
- 当一个值传递给一个 prop 特性的时候，就变成了那个组件实例的一个属性
- 一个组件默认可以拥有任意数量的 prop，任何值都可以传递给prop
- 我们可以使用 ``v-bind`` 来动态传递prop

```html
<blog-post title="My journey with Vue"></blog-post>
<blog-post title="Blogging with Vue"></blog-post>
```
```vue
Vue.component('blog-post', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})
```

### 5. 单个根元素
- 每个根组件必须只有一个根元素

```html
<blog-post
    v-for="post in posts"
    :key="post.id"
    :post="post"
></blog-post>
```
```vue
Vue.component('blog-post', {
    props: ['post'],
    template: '
        <div class="blog-post"
            <h3>{{ post.title }}</h3>
            <div v-html="post.content"></div>
        </div>
    '
})
```

### 6. 通过事件向父级组件发送消息
- Vue 实例提供了一个自定义事件的系统
- 可以调用内建的 ``$emit`` 方法，并传入事件的名字，来向父级组件触发一个事件
- 我们通过 ``v-on`` 在父级组件上监听这个事件，就像监听一个原生 DOM 事件一样

#### 6.1 使用事件抛出一个值
- 可以使用 ``$emit`` 的第二个参数作为一个事件抛出的特定值
- 当在父级组件监听该事件时，通过 ``$event`` 访问被抛出的值
- 如果该事件处理函数是一个方法，那么这个被抛出的值将作为第一个参数传入该方法

```html
<!-- 父级组件 -->
<blog-post
  ...
  v-on:enlarge-text="postFontSize += $event"
></blog-post>

<!-- 子组件中的 button -->
<button v-on:click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```
```vue
<!-- 如果父级组件处理函数是一个方法 -->
methods: {
  onEnlargeText: function (enlargeAmount) {
    this.postFontSize += enlargeAmount
  }
}
```
### 7. 通过插槽分发内容
与HTML元素一样，我们经常需要向一个组件传递内容：
```html
<alert-box>
    Something bad happend.
</alert-box>
```
Vue 自定义的 ``<slot>`` 元素让这变得非常简单:
```vue
Vue.component('alert-box', {
  template: `
    <div class="demo-alert-box">
      <strong>Error!</strong>
      <slot></slot>
    </div>
  `
})
```
### 8. 动态组件
有的时候，在不同组件之间进行动态切换是非常有用的，我们可以通过 Vue 的 ``<component>``元素加一个特殊的 ``is`` 特性来实现:
```html
<!-- 组件会在 `currentTabComponent` 改变时改变 -->
<component v-bind:is="currentTabComponent"></component>
```
在上述示例中，``currentTabComponent`` 可以包括

- 已注册组件的名字，或
- 一个组件的选项对象


### 9. 解析DOM模板时的注意事项
```html
<table>
  <blog-post-row></blog-post-row>
</table>
```
该自定义组件 ``<blog-post-row>`` 会被作为无效的内容提升到外部，并导致最终渲染结果出错。正确写法如下：
```html
<table>
  <tr v-bind:is="blog-post-row"></tr>
</table>
```
注意：**如果是从以下来源使用模板的话，这条限制是不存在的：
- 字符串（例如：``template:'...'``）
- 单文件组件（``.vue``）
- ``<script type="text/x-template">``

<br>

## 二、深入了解组件
### 1. 组件注册
#### 1.1 组件名
定义组件名有两种方式：
- **使用 kebab-case**，引用时使用 ``<my-component-name>``
- **使用 PascalCase**，引用时使用 ``<my-component-name>`` 或者 ``<MyComponentName>``

注意：直接在 DOM（即非字符串的模板） 中使用时，只有 **kebab-case** 是有效的
```vue
// kebab-case
Vue.component('my-component-name', {})

// PascalCase
Vue.component('MyComponentName', {})
```

#### 1.2 全局注册
- 通过 ``Vue.component`` 来创建组件
- 注册后可以在任何新创建的 Vue 根实例（``new Vue``）的模板中
- 在所有子组件中，也可以相互使用

#### 1.3 局部注册
- 通过一个普通的 JavaScript 对象来定义组件
- 通过 ``components`` 选项对象使用
- 局部注册的组件在其子组件中 **不可用**

```vue
var ComponentA = { /* ... */ }
var ComponentB = { /* ... */ }
var ComponentC = { /* ... */ }

new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```
#### 1.4 模块系统
...

### 2. Prop
#### 2.1 Prop的大小写
- HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。
- 当你使用 DOM 中的模板时，camelCase的prop名需要使用其等价的 kebab-case 命名
- 如果使用字符串模板，这个限制就不存在
```vue
Vue.component('blog-post', {
    props: ['postTitle'],
    template: '<h3>{{ postTitle }}</h3>'
})
```
```html
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```
#### 2.2 Prop类型
- 若希望每个 prop 都有指定的类型，可以以对象形式列出 prop
- 该行为不仅为组件提供了文档，还会在遇到错误的类型时从浏览器的控制台提示用户

```vue
props: {
    title: String,
    likes: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object
}
```

#### 2.3 传递静态或动态Prop
可以给 prop 传入一个静态的值：如下
```html
<blog-post title="My journey with Vue"></blog-post>
```
也可以通过 ``v-bind`` 动态赋值，如下
```html
<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post v-bind:title="post.title + ' by ' + post.author.name"></blog-post>
```
除了字符串类型，任何类型的值都可以传递给一个prop
- 传入一个数字
- 传入一个布尔值
- 传入一个数组
- 传入一个对象
- 传入一个对象的所有属性

#### 2.4 单向数据流
所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来不行。

每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。

有两种常见的试图改变一个 prop 的情形：
1. **该 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。**这种情况下最好定义一个本地的 data 属性并将这个 prop 用作其初始值
```vue
props: ['initialCounter'],
data: function () {
  return {
    counter: this.initialCounter
  }
}
```
2. **这个 prop 以一种原始的值传入且需要进行转换。**在这种情况下，最好使用这个 prop 的值来定义一个计算属性
```vue
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```
> 注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变这个对象或数组本身将会影响到父组件的状态

#### 2.5 Prop验证
可以为组件的 prop 指定验证要求。若有一个需求未被满足，则 Vue 会在浏览器控制台中警告你。

为了定制 prop 的验证方式，你可以为 ``props`` 中的值提供一个带有验证需求的对象，而不是一个字符串数组。

```vue
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 匹配任何类型)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```
##### 2.5.1 类型检查
``type`` 可以是以下原生构造函数中的一个：
- ``String``
- ``Number``
- ``Boolean``
- ``Array``
- ``Object``
- ``Date``
- ``Function``
- ``Symbol``

``type`` 还可以是一个自定义的构造函数，并通过 ``instanceof`` 来进行检查
```js
function Person (firstName, lastName) {
  this.firstName = firstName
  this.lastName = lastName
}
```
```vue
Vue.component('blog-post', {
  props: {
    author: Person
  }
})
```
上述代码验证 ``author`` prop 的值是否是通过 ``new Person`` 创建的。

#### 2.6 非Prop的特性
一个非 prop 特性是指传向一个组件，但是该组件并没有相应 prop 定义的特性。

因为显式定义的 prop 适用于向一个子组件传入信息，然而组件库的作者并不总能预见组件会被用于怎样的场景。这也是为什么组件可以接受任意的特性，而这些特性会被添加到这个组件的根元素上。

例如，想象一下你通过一个 Bootstrap 插件使用了一个第三方的 ``<bootstrap-date-input>`` 组件，这个插件需要在其 ``<input>`` 上用到一个 ``data-date-picker`` 特性。我们可以将这个特性添加到你的组件实例上：

```vue
<bootstrap-date-input data-date-picker="activated"></bootstrap-date-input>
```
然后这个 ``data-date-picker="activated"`` 特性就会自动添加到 ``<bootstrap-date-input>`` 的根元素上。

##### 2.6.1 替换/合并已有的特性
若``<bootstrap-date-input>`` 的模板是这样的：
```html
<input type="date" class="form-control">
```
为了定制主题，需要添加一个特别的类名：
```html
<bootstrap-date-input
    data-date-picker="activated"
    class="date-picker-theme-dark"
></bootstrap-date-input>
```
此时，定义了两个不同的 ``class`` 的值：
- ``form-control``，这是在组件的模板内设置好的
- ``date-picker-theme-dark``，这是从父级组件传入的
- 对于大部分特性来说，从外部提供给组件的值会替换掉组件内部设置好的值。例如：传入 ``type="text"`` 会替换掉 ``type="date"``。而 ``class`` 和 ``style`` 特性不同，两边的值会被合并起来，最终的值为：``form-control date-picker-theme-dark``。

##### 2.6.2 禁用特性继承
若不希望组件的根元素集成特性，可以在组件选项中设置 ``inheritAttrs: false``。例如：
```vue
Vue.component('my-component', {
  inheritAttrs: false,
  // ...
})
```
配合实例的 ``$attrs`` 属性使用，该属性包含了传递给一个组件的特性名和特性值：
```js
{
  class: 'username-input',
  placeholder: 'Enter your username'
}
```
```vue
Vue.component('base-input', {
  inheritAttrs: false,
  props: ['label', 'value'],
  template: `
    <label>
      {{ label }}
      <input
        v-bind="$attrs"
        v-bind:value="value"
        v-on:input="$emit('input', $event.target.value)"
      >
    </label>
  `
})
```
这个模式允许你在使用基础组件的时候更像是使用原始的 HTML 元素，而不会担心哪个元素是真正的根元素：
```html
<base-input
  v-model="username"
  class="username-input"
  placeholder="Enter your username"
></base-input>
```

### 3. 自定义事件
#### 3.1 事件名
** 推荐始终使用 kebab-case 的事件名：**
- 事件名不存在任何自动化的大小写转换
- 而触发的事件名需要完全匹配监听这个事件所用的名称
- 事件名不会被作为一个 JavaScript 变量名或属性名
- ``v-on`` 事件监听在 DOM 模板中会被自动转换为全小写

例子：若触发一个 camelCase 名字的事件：
```js
this.$emit('myEvent')
```
监听该名字的 kebab-case 版本是无效的：
```html
<my-component v-on:my-event="doSomething"></my-component>
```
``v-on`` 时间监听器在 DOM 模板中会被自动转换为全小写（因为 HTML是大小写不敏感的），所以``v-on:myEvent`` 将会变成 ``v-on:myevent``--导致 ``myEvent`` 不可能被监听到。

#### 3.2 自定义组件的 ``v-model``
一个组件上的 ``v-model`` 默认会利用名为 ``value`` 的 prop 和名为 ``input`` 的事件，但像单选框、复选框的类型的输入控件可能会将 ``value`` 特性用于不同的目的。``model`` 选项可以用来避免这样的冲突：
```js
Vue.component('base-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `
})
```
```html
<base-checkbox v-model="lovingVue"></base-checkbox>
```
在组件上使用 ``v-model`` 时，``lovingVue`` 会传入名为 ``checked`` 的prop。

#### 3.3 将原生事件绑定到组件
使用 ``v-on`` 的 ``.native`` 修饰符，可以在一个**组件的根元素**上直接监听一个原生事件。
```html
<base-input v-on:focus.native="onFocus"></base-input>
```
但是，当尝试监听一个类似 ``<input>`` 的非常特定的元素时，这并不是好主意。例如：
```html
<!-- 组件的根元素实际上是 <label> 元素 -->
<label>
  {{ label }}
  <input
    v-bind="$attrs"
    v-bind:value="value"
    v-on:input="$emit('input', $event.target.value)"
  >
</label>
```
此时，父级的 ``.native`` 监听器将静默失败，它不会产生任何报错，``onFocus`` 处理函数也不会被调用。

Vue 提供了一个 ``$listeners`` 属性，它是一个对象，里面包含作用在这个组件上的所有监听器，例如：
```js
{
  focus: function (event) { /* ... */ }
  input: function (value) { /* ... */ },
}
```
配合 ``v-on="$listeners"`` 将所有事件监听器指向这个组件的某个特定的子元素。
```js
Vue.component('base-input', {
  inheritAttrs: false,
  props: ['label', 'value'],
  computed: {
    inputListeners: function () {
      var vm = this
      // `Object.assign` 将所有的对象合并为一个新对象
      return Object.assign({},
        // 我们从父级添加所有的监听器
        this.$listeners,
        // 然后我们添加自定义监听器，
        // 或覆写一些监听器的行为
        {
          // 这里确保组件配合 `v-model` 的工作
          input: function (event) {
            vm.$emit('input', event.target.value)
          }
        }
      )
    }
  },
  template: `
    <label>
      {{ label }}
      <input
        v-bind="$attrs"
        v-bind:value="value"
        v-on="inputListeners"
      >
    </label>
  `
})
```
#### 3.4 ``.sync``修饰符




### 4. 插槽slot

### 5. 动态组件

### 6. 异步组件

### 7. 处理边界情况




🚀 [回到顶部](#目录)