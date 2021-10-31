配置项目Https服务

申请证书：https://freessl.org

CDN原理：

对不同构建版本的解释

| UMD                                 | CommonJS           | ES Module (基于构建工具使用) | ES Module (直接用于浏览器) |                        |
| :---------------------------------- | :----------------- | :--------------------------- | :------------------------- | ---------------------- |
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

    // 计算属性是基于它们的响应式依赖进行缓存的 如果依赖的内容没有变化，则不会改内容

    // 如果一个属性值依赖其它多个属性值时 需要监听多个事件 此时比计算属性会显得代码冗余
```

`v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` attribute 的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 `data` 选项中声明初始值。 Object.defineProperty() 来劫持各个属性的 setter,getter

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

### vue项目中的小细节

```shell
resolve: {
    // 自动补全的扩展名
    extensions: ['.js', '.vue', '.json'],
    // 默认路径代理
    // 例如 import Vue from 'vue'，会自动到 'vue/dist/vue.common.js'中寻找
    alias: {
        '@': resolve('src'),//目录简写
        '@config': resolve('config'),
        'vue$': 'vue/dist/vue.common.js'
    }
}
```

### npm 命令

```js
默认本地模式：npm install packageName(安装最新版本到本地 node_modules)
全局模式：npm install packageName -g(安装最新版本到node目录下的node_modules)
备注：全局模式 不能直接 require()的方式引用  命令行可以使用

安装到开发依赖并写入 package.json 中
npm install -D  =npm install --save -d


npm install <name> --save 将安装包信息写入 package.json 中， 这样使用npm install方法就可以根据dependencies配置安装所有的依赖包

卸载 npm uninstall packageName
npm root：查看当前包的安装路径
npm root -g：查看全局的包的安装路径

npm list -g
npm list 

package-lock.json 锁定安装依赖的版本号。

// 使用淘宝镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org

如果出现 npm err! Error: connect ECONNREFUSED 127.0.0.1:8087 
$ npm config set proxy null

其它： 
npm（Node Package Manager）是随同node.js 一起安装的包管理工具，为了解决nodejs代码部署上的很多问题，常用以下场景：

允许用户从npm服务器下载别人编写的地方包到本地使用。
允许用户将自己编写的包或明显杭程序上传到NPM服务器供别人使用。
二、npm使用前提

必须先安装node.js，安装地址官网http://nodejs.cn/，安装完成以后通过“node -v”查看版本号

三、第一次git了项目

第一次git上获取项目，记得一定要先npm install 

因为刚下载的项目，没有node_modules，只有通过npm install命令以后会根据package.json  去下载相关依赖包。

四、npm命令大全

1、  npm install 安装模块

   npm install X、npm install X -save、npm install X -save-dev的区别？

   1、npm install X：

        会把X包安装到node_modules目录中，

         不会修改package.json，

         之后运行npm install 命令时，不会自动安装X

   2、npm install X -save:

         会把X包安装至node_modules目录中，

         会在package.json的dependencies属性中添加X，

         之后运行npm install命令会自动安装X到node_modules中

         运行时需要引用的包

   3、npm install X-save-dev

         会把X包安装到node_modules目录中

         会在package.json的devDependencies属性下添加X

         之后运行npm install命令时，会自动安装X到node_modules目录中

         开发过程需要使用的包

2.npm uninstall 卸载模块
3.npm update 更新模块
4.npm outdated 检查模块是否已经过时
5.npm ls 查看安装的模块
6.npm init  在项目中引导创建一个package.json 文件
通过package.json描述包引用情况，以便后续的其他的项目开发或者他人合作使用。
7.npm help  查看某条命令的详细帮助
这个相当方便，会自动打开相应命令的帮助文档。
8.npm root  查看包的安装路径
9.npm config  管理npm的配置路径
10.npm start 启动模块
11.npm stop 停止模块
12.npm restart 重新启动模块
13.npm test 测试模块
14.npm version 查看模块版本
15.npm view 查看模块的注册信息
16.npm adduser 用户登录
17.npm publish 发布模块
18.npm access 在发布的包上设置访问级别
19.npm package.json的语法


实际使用的区别点主要如下(windows下)： 
1. 用npm i安装的模块无法用npm uninstall删除，用npm uninstall i才卸载掉 
2. npm i会帮助检测与当前node版本最匹配的npm包版本号，并匹配出来相互依赖的npm包应该提升的版本号 
3. 部分npm包在当前node版本下无法使用，必须使用建议版本 
4. 安装报错时intall肯定会出现npm-debug.log 文件，npm i不一定
```

### Babel 使用

- 安装Node
- 安装babel

  npm i @babel/core @babel/cli @babel/preset-env

  npm i @babel/polyfill  (为了兼容ie7以前) 可有可无
- 添加脚本 package.json  "build":"babel src -d dest"
- 添加配置 .babelrc(相对文件的配置)

  {

  "presets":["@babel/preset-env"]

  }

  babel.config.js （项目范围的配置）

  module.exports={

  ```
  presets:["@bable/preset-env"]
  ```


  }

### 常规vue 项目框架搭建

* 1、安装Vue脚手架
* 2、通过Vue脚手架创建项目

```
vue ui
```


* 3、配置Vue 路由
* 4 、配置Element-UI组件库

```
安装element
```


* 5、配置 axios库
* 6、初始化git 远程仓库
* 7、将本地项目托管到GitHub 或码云中
