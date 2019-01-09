Vue.js 笔记
=========

## 目录

- [目录](#目录)
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
<!-- /TOC -->

## 一、Vue.js是什么
- Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的**渐进式框架**。
- Vue 被设计为可以自底向上逐层应用。
- Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。
- 当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 二、资源
- 官方文档 [Vue.js](https://vuejs.org/index.html)
- Github [vuejs](https://github.com/vuejs)

## 三、Vue实例
一个 Vue 应用由一个通过`` new Vue ``创建的**根 Vue 实例**，以及可选的嵌套的、可复用的组件树组成
```javascript
var vm = new Vue({
  // 选项
})
```

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
## 六、Vue中的样式绑定

🍃 [示例代码]()

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


## 七、Vue中的条件渲染
waiting to record...    




🚀 [回到顶部](#目录)