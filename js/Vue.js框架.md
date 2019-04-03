## Vue.js框架

#### 一：**概念**

Vue.js 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注**视图层**，不仅易于上手，还便于与第三方库或既有项目整合。

```js
// Vue.js 是以数据驱动的框架， 关心视图层。其核心设计模式是： MVVM
M： Model （数据层）
V：View （视图层）

C： Controller (控制层)

```

![1553909132195](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1553909132195.png)



​								MVC视图层

DOM的操作 （取值， 赋值）， 事件的驱动， 监听， JS的解析等都封装在 ViewModel: 视图数据层 （也可以理解为控制器 Controller）。 所以，我们只操作**数据** （Data）就可以了。

#### 二： 指令

​	指令概念： 

​		什么是指令？  指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊特性。可能你已经猜到了，它们会在渲染的 DOM 上应用特殊的响应式行为。

​	1： 声明式渲染：核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 。

```html
 <!-- 对dom节点赋值用 `{{  }}` 来进行赋值，文本插值。-->

<div id="warp">
    {{ message }}  
</div>         
```

```js
// js的语法: 通过new关键字来创建一个vue实例

var vm = new Vue ({
    el: "#warp",
    // data: 里面的数据都会和 DOM 已经被建立了关联，所有东西都是响应式的。data外的数据，不会关联
    data: function () {
        return {
             message: "hello vue"
        }
    }
});
```

​	2： **v-bind** 指令来绑定DOM节点属性： v-bind:节点名="变量名"；冒号是变量赋值。

```html
<div id="warp">
    {{ message }} 
    
	<!-- header-->
     <header v-bind:title="headerTitle">
         {{ headerTitle }}
     </header>   
</div>      
```

```js
var vm = new Vue ({
    el: "#warp",
    data: function () {
        return {
            message: "hello vue",
            headerTitle: "我是header标签title值"
        }
    }
})；
```

​	3：条件与循环

​		条件：控制切换一个**DOM节点**或者是**DOM结构**是否**显示**。 v-if="false/ true"

```html
<div id="warp">
    {{ message }} 
    
	<!-- header-->
     <!-- v-bind: dom节点的属性 -->   
     <header v-bind:title="headerTitle">
         {{ headerTitle }}
     </header>   
         
     <!-- v-if：控制切换一个DOM节点是否显示： true: 显示，false： 为隐藏  --> 
     <nav class="my-nav" 
          v-bind:title="navMessageTitle"
          v-if="flag"
     >
         {{ navMessage }}
     </nav>   
</div>    
```

```js
var vm = new Vue ({
    el: "#warp",
    data: function () {
        return {
            message: "hello vue",
            headerTitle: "我是header标签title值",
            navMessage: "我是导航标签",
            navMessageTitle: "我是导航标签title",
            flag: true
        }
    }
})；
```

​	循环指令： v-for="(value, index) in arr"          v-for可以绑定数组的数据来渲染一个项目列表。value是遍历数组的元素， index是遍历数组的下标。

```html
<div id="warp">
    {{ message }} 
    
	<!-- header-->
     <!-- v-bind: dom节点的属性 -->   
     <header v-bind:title="headerTitle">
         {{ headerTitle }}
     </header>   
         
     <!-- v-if：控制切换一个DOM节点是否显示： true: 显示，false： 为隐藏  --> 
     <nav class="my-nav" 
          v-bind:title="navMessageTitle"
          v-if="flag"
     >
         {{ navMessage }}
     </nav>
         
      <!-- 循环： v-for -->   
     <div >
         <ul>
             <!-- 要循环的html结构 -->
             <li 
                 v-for="(value, index) in list"
                 :key="index"
              >
                 {{ value.text }}
             </li>
         </ul>
     </div>   
</div>    
```

```js
var vm = new Vue ({
    el: "#warp",
    data: function () {
        return {
            message: "hello vue",
            headerTitle: "我是header标签title值",
            navMessage: "我是导航标签",
            navMessageTitle: "我是导航标签title",
            flag: true,
            list: [
                { text: "学好vue" },
                { text: "学好js"  },
                { text: "学好HTML"},
                { text: "学好css" },
                { text: "妈妈再也不用担心我找不到工作了"}
            ]
            
        }
    }
})；
```

4： 操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是属性，所以我们可以用 `v-bind` 处理它们；

```html
<div id="warp">
    {{ message }} 
    
	<!-- header-->
     <!-- v-bind: dom节点的属性 -->   
     <header v-bind:title="headerTitle">
         {{ headerTitle }}
     </header>   
         
     <!-- v-if：控制切换一个DOM节点是否显示： true: 显示，false： 为隐藏  --> 
     <nav class="my-nav" 
          v-bind:title="navMessageTitle"
          v-if="flag"
     >
         {{ navMessage }}
     </nav>
         
      <!-- 循环： v-for -->   
     <div >
         <ul>
             <!-- 要循环的html结构 -->
             <li 
                 v-for="(value, index) in list"
                 :key="index"
              >
                 {{ value.text }}
             </li>
         </ul>
     </div>   
    <!--  class 与 style -->
    <!-- 数组语法 -->
   <div v-bind:class="[activeClass, comeClass]">
       我是class与style
    </div>
    
</div>    
```

```js
var vm = new Vue ({
    el: "#warp",
    data: function () {
        return {
            message: "hello vue",
            headerTitle: "我是header标签title值",
            navMessage: "我是导航标签",
            navMessageTitle: "我是导航标签title",
            flag: true,
            list: [
                { text: "学好vue" },
                { text: "学好js"  },
                { text: "学好HTML"},
                { text: "学好css" },
                { text: "妈妈再也不用担心我找不到工作了"}
            ],
            activeClass: "my-class",
            comeClass: "ny-common-class"
        }
    }
})；
```
0000


三： 事件驱动

​	为了让用户和你的应用进行交互，我们可以用  **`v-on`**  或者 *@*  指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法， 添加事件的驱动监听， 写在vue实例中的methods对象中。

```html
<div id="warp">
    {{ message }} 
    
	<!-- header-->
     <!-- v-bind: dom节点的属性 -->   
     <header v-bind:title="headerTitle">
         {{ headerTitle }}
     </header>   
         
     <!-- v-if：控制切换一个DOM节点是否显示： true: 显示，false： 为隐藏  --> 
     <nav class="my-nav" 
          v-bind:title="navMessageTitle"
          v-if="flag"
     >
         {{ navMessage }}
     </nav>
         
      <!-- 循环： v-for -->   
     <div >
         <ul>
             <!-- 要循环的html结构 -->
             <li 
                 v-for="(value, index) in list"
                 :key="index"
              >
                 {{ value.text }}
             </li>
         </ul>
     </div>   
    
    <!-- 添加事件驱动： v-on/@ 指令 -->
    <div 
         class="my-footer"
         v-on:click="handleAddClick"
    >
        <span 
             class="my-footer-span"
              v-if="spanFlag"
         >
         	我是footer下的span标签   
        </span>
    </div>
    
</div>    
```

```js
var vm = new Vue ({
    el: "#warp",
    data: function () {
        return {
            message: "hello vue",
            headerTitle: "我是header标签title值",
            navMessage: "我是导航标签",
            navMessageTitle: "我是导航标签title",
            flag: true,
            list: [
                { text: "学好vue" },
                { text: "学好js"  },
                { text: "学好HTML"},
                { text: "学好css" },
                { text: "妈妈再也不用担心我找不到工作了"}
            ],
            spanFlag: true
            
        }
    },
    // 添加事件监听
    methods: {
        handleAddClick: function () {
            console.log(this);
        }
    }
})；
```

四：双向数据绑定指令 **v-model** 表单输入和应用状态之间的双向绑定。 也就是数据关联。

```html
<div id="app">
    <p> {{ message }} </p>
    <input v-model="inputMessage">
</div>
```

```js
var vm = new Vue ({
    el: "#app",
    data: function () {
        return {
            message: ""
        }
    }
})
```



五： 组件化系统

​	**概念**： 组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、**独立**和通常可**复用** 的组件构建大型应用。仔细想想，应用界面DOM结构都可以抽象为一个组件树。



![Component Tree](https://cn.vuejs.org/images/components.png)

在HTML中， 每个DOM结构，都可以看成一个独立的组件， 如果结构相同， 我们自需写一个组件，可以全局复用。

组件命名规范： 单词之间， 可以用  `一`  来进行连接。 

在 Vue 里，一个组件本质上是一个拥有预定义选项的一个 Vue 实例。**注意**： 我们首先先去生成，注册后组件，才能够使用。

```php

// 先注册组件， 然后，才能通过new关键字来进行创建vue实例,才能用。
Vue.component ("button-click", {
    name: "button-click",
    data: function () {
        return {
            count: 1
        }
    },
    template: `<button type="button" @click="handleAddCount" >{{ count }}</button>`,
    methods: {
        handleAddCount () {
            this.count++;
        }
    }
});


var vm = new Vue({
    el: "#warp",
    data: function () {
        return {
            .....
        }
    }
})
```

六： 父组件 /   父作用域与子组件的传值： 组件与组件的数据传递机制。

​	从父作用域将数据传到子组件， 我们使用的是  **prop** 

```js
Vue.component("my-component", {
    name: "my-component",
    data: function () {
        return {
            message: "我是自定义组件"
        }
    },
    // prop: 是数组类型， 数组里面存储的元素，是要从父作用域 / 父组件来传递的变量数据。
    prop：["todo"],
    template: "<li> {{ todo }} </li>"          
})
```























