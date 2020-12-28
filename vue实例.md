配置项目Https服务

申请证书：https://freessl.org



CDN原理：



对不同构建版本的解释

| UMD                           | CommonJS           | ES Module (基于构建工具使用) | ES Module (直接用于浏览器) |                        |
| :---------------------------- | :----------------- | :--------------------------- | :------------------------- | ---------------------- |
| **完整版**                    | vue.js             | vue.common.js                | vue.esm.js                 | vue.esm.browser.js     |
| **只包含运行时版**            | vue.runtime.js     | vue.runtime.common.js        | vue.runtime.esm.js         | -                      |
| **完整版 (生产环境)**         | vue.min.js         | -                            | -                          | vue.esm.browser.min.js |
| **只包含运行时版 (生产环境)** | vue.runtime.min.js | -                            | -                          | -                      |

### [术语](https://cn.vuejs.org/v2/guide/installation.html#术语)

- **完整版**：同时包含编译器和运行时的版本。
- **编译器**：用来将模板字符串编译成为 JavaScript 渲染函数的代码。
- **运行时**：用来创建 Vue 实例、渲染并处理虚拟 DOM 等的代码。基本上就是除去编译器的其它一切。
- **[UMD](https://github.com/umdjs/umd)**：UMD 版本可以通过 `<script>` 标签直接用在浏览器中。jsDelivr CDN 的 https://cdn.jsdelivr.net/npm/vue 默认文件就是运行时 + 编译器的 UMD 版本 (`vue.js`)。
- **[CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1)**：CommonJS 版本用来配合老的打包工具比如 [Browserify](http://browserify.org/) 或 [webpack 1](https://webpack.github.io/)。这些打包工具的默认文件 (`pkg.main`) 是只包含运行时的 CommonJS 版本 (`vue.runtime.common.js`)。
- **[ES Module](http://exploringjs.com/es6/ch_modules.html)**：从 2.6 开始 Vue 会提供两个 ES Modules (ESM) 构建文件：
  - 为打包工具提供的 ESM：为诸如 [webpack 2](https://webpack.js.org/) 或 [Rollup](https://rollupjs.org/) 提供的现代打包工具。ESM 格式被设计为可以被静态分析，所以打包工具可以利用这一点来进行“tree-shaking”并将用不到的代码排除出最终的包。为这些打包工具提供的默认文件 (`pkg.module`) 是只有运行时的 ES Module 构建 (`vue.runtime.esm.js`)。
  - 为浏览器提供的 ESM (2.6+)：用于在现代浏览器中通过 `<script type="module">` 直接导入。

* 



Vue 实例

```vue
var vm = new Vue({
  // 选项
})
```



### 模板语法

### [`v-bind` 缩写](https://cn.vuejs.org/v2/guide/syntax.html#v-bind-缩写)

```vue
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
```

### [`v-on` 缩写](https://cn.vuejs.org/v2/guide/syntax.html#v-on-缩写)

```vue
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

### [`v-Show v-if` 缩写](https://cn.vuejs.org/v2/guide/syntax.html#v-on-缩写)

```vue
v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

v-if 使用注意
例子：在使用el-select 复选框选值时，当选择的文本过长会换行
解决方案：文本超长时只显示4个字长，后面...显示

  <el-select class = "optionsContent"
    v-model="value2"
    multiple
    collapse-tags
    style="margin-left: 20px;"
    placeholder="请选择"
    @change="setTagTitle">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
声明周期函数 updated(){
   
}
```

![image-20201018202910039](C:\Users\Administrator\Documents\Typora笔记\vue实例.assets\image-20201018202910039.png)



### [`v-if v-for` 缩写](https://cn.vuejs.org/v2/guide/syntax.html#v-on-缩写)

```vue
当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级
```



### 计算属性、事件监听、方法

```shell
 // 事件监听（watch）vs计算属性（computed）vs方法（method）

​    // 计算属性是基于它们的响应式依赖进行缓存的 如果依赖的内容没有变化，则不会改内容

​    // 如果一个属性值依赖其它多个属性值时 需要监听多个事件 此时比计算属性会显得代码冗余
```

`v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` attribute 的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 `data` 选项中声明初始值。



### vue 生命周期钩子函数



### vue状态管理之vuex

#### 一、组件之间通讯的方式

 **对于父子组件之间**

 **1、通过 prop 属性实现父组件向子组件传递数据**

 ```vue
//例子
子组件定义 props 
   Vue.component('todo-item',{
           props:['todo','todo2'],
           template: '<li>{{ todo.text  }},{{todo2}}</li>'
         });

父组件赋值
   <div id='app2'>
      <todo-item      v-for="item in groceryList"
     :todo="item"
     :todo2="test"
     :key="item.id">
      </todo-item>
    </div>
 ```



 **2、通过在子组件中触发事件实现向父组件传递数据**

```vue
//例子
子组件
<button v-on:click="$emit('enlarge-text')">
  Enlarge text
</button>
//父组件
<div id="blog-posts-events-demo">
  <div :style="{ fontSize: postFontSize + 'em' }">
    <blog-post
      v-on:enlarge-text="postFontSize += 0.1"
    ></blog-post>
  </div>
</div>

//
3、$on监听事件，$emit触发事件
　　现在$dispatch、$broadcast需要配合events使用，在vue2.0上已经被删除了，现在更多的是使用$on监听事件、$emit触发事件。主要分为以下四步：

　　（1）子组件绑定send事件

<template id="bbb">
    <h3>子组件-</h3>
    <input type="button" value="send" @click="send">
</template>
　　（2）子组件通过$emit主动触发事件，发送数据到父组件

methods:{
    send(){//2、子组件通过$.emit主动发送数据a到父级
        this.$emit('child-msg',this.a);
    }
}
　　（3）父组件通过v-on监听子组件触发的事件

<template id="aaa">
    <span>我是父级 -> {{msg}}</span>
    //3、父组件绑定接收事件，接收的一边是子组件里的事件名，一边是父组件里面需要定义的事件名
    <bbb @child-msg="get"></bbb>
</template>
　　（4）父组件接受子组件发送的数据

methods:{
    //4、父组件接收子组件发送的数据，作为参数，改变自己里面数据
    get(msg){
        this.msg=msg;
    }
}
```



  



















### 常规vue 项目框架搭建

* 1、安装Vue脚手架    

* 2、通过Vue脚手架创建项目

​             vue ui 

* 3、配置Vue 路由

* 4 、配置Element-UI组件库

​             安装element

* 5、配置 axios库
* 6、初始化git 远程仓库
* 7、将本地项目托管到GitHub 或码云中

