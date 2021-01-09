基础知识

## 样式声明

可以通过多种方式定义样式表。

### 外部样式

使用 `link` 标签引入外部样式文件，需要注意以下几点。

- link 标签放在 `head` 标签内部
- 样式文件要以 `.css` 为扩展名
- 一个页面往往需要引入多个样式文件

| 属性 | 说明                               |
| ---- | ---------------------------------- |
| rel  | 定义当前文档与被链接文档之间的关系 |
| href | 外部样式文件                       |
| type | 文档类型                           |

> link 还有其他属性会在其他章节单独讲解

```html
<link rel="stylesheet" href="houdunren.css" type="text/css">
```

### 嵌入样式

使用 `style` 标签可以在文档内部定义样式规则。

```html
<style>
	body {
		background: red;
	}
</style
```

### 内联样式

可以为某个标签单独设置样式。

```html
<h1 style="color:green;">houdunren.com</h1>
```

### 导入样式

使用 `@import` 可以在原样式规则中导入其他样式表，可以在外部样式、`style`标签中使用。

可以使用以下两种方式导入

```css
@import "hd.css"
@import url("hd.css")
```

导入样式要放在样式规则前面定义。

```text
<style>
	@import url("hdcms.css");
	body {
		background: red;
	}
</style1>
```

##  其他细节

### 空白

在样式规则中可以随意使用空白，空白只是看不见但同样占用空间，所以可以结合其他工具如 `webpack` 等将`css` 压缩为一行。

### 注释

注释是对定义样式规则的说明，便于后期维护理解。

```text
...
body {
	/* 这是注释的使用 */
	background: red;
}
...
```

### 错误

样式规则如果存在错误，解析器会选择忽略，并不会影响其他样式规则。

以下代码的`houdunren:red` 是无效样式但不影响后面的 `font-size:100px;` 规则使用。

```css
h1 {
    houdunren: red;
    font-size: 100px;
}
```



# 选择器



样式是做用在元素标签上的，通过本章将可以随意查找元素来应用样式。

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#基本选择器)基本选择器

| 选择器          | 示例       | 描述                           |
| :-------------- | ---------- | :----------------------------- |
| .class          | .intro     | 选择 class="intro" 的所有元素  |
| #id             | #firstname | 选择 id="firstname" 的所有元素 |
| *               | *          | 选择所有元素                   |
| element         | p          | 选择所有元素                   |
| element,element | div,p      | 选择所有元素和所有元素         |
| element element | div p      | 选择元素内部的所有元素         |
| element>element | div>p      | 选择父元素为元素的所有元素     |
| element+element | div+p      | 选择紧接在元素之后的所有元素   |

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#标签选择)标签选择

使用 `*` 可为所有元素设置样式。

```css
* {
    text-decoration: none;
    color: #6c757d;
}
```

根据标签为元素设置样式

```css
h1 {
	color: red;
}
```

同时设置多个元素组合

```css
h1,h2 {
    color: red;
}
```

元素在多个组件中存在

```text
h1,h2 {
    color: red;
}
h1,h3{
    background: #dcdcdc;
}
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#类选择器)类选择器

类选择器是为一类状态声明样式规则，下面是把文本居中定义为类样式。

```text
.text-center {
    text-align: center;
}
...

<h1 class="text-center">houdunren.com</h1>
<h2 class="text-center">hdcms.com</h2>
```

将类选择器指定为具体标签

```text
.help-block {
    background: red;
}

span.help-block {
    font-size: 12px;
    color: #aaa;
    background: none;
}
...

<span class="help-block">感谢访问后盾人</span>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#id选择器)ID选择器

为有 id 属性的元素设置样式

```text
#container {
    background: red;
}

...
<h1 id="container">houdunren.com</h1>
```

> 文档中ID应该是唯一的，虽然为多个元素设置同一个ID也可以产生样式效果，但这是不符合规范的。
>
> 建议优先使用类选择器

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#结构选择器)结构选择器

| 选择器           | 示例  | 描述                               |
| :--------------- | ----- | :--------------------------------- |
| element element  | div p | 选择元素内部的所有元素             |
| element>element  | div>p | 选择父元素为元素的所有元素         |
| element+element  | div+p | 选择紧接在元素之后的元素           |
| element~element2 | p~ul  | 选择元素同级并在元素后面的所有元素 |

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#后代选择器)后代选择器

HTML中元素是以父子级、兄弟关系存在的。后代选择器指元素后的元素（不只是子元素，是后代元素）。

```text
main article h2,main h1 {
    color: green;
}
...

<main>
	<article>
		<h2 name="houdunren">houdunren.com</h2>
		<aside>
			<h2>houdunwang.com</h2>
		</aside>
	</article>
	<h2 name="hdcms.com">hdcms.com</h2>
	<h1>后盾人</h1>
</main>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#子元素选择)子元素选择

子元素选择器中选择子元素，不包括孙级及以下元素。

```text
main article>h2 {
    color: green;
}
...

<main>
	<article>
		<h2 name="houdunren">houdunren.com</h2>
		<aside>
			<h2>houdunwang.com</h2>
		</aside>
	</article>
	<h2 name="hdcms.com">hdcms.com</h2>
	<h1>后盾人</h1>
</main>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#紧邻兄弟元素)紧邻兄弟元素

用于选择紧挨着的同级兄弟元素。

```text
main article+h2 {
    color: green;
}
...

<main>
	<article>
		<h2 name="houdunren">houdunren.com</h2>
		<aside>
			<h2>houdunwang.com</h2>
		</aside>
	</article>
	<h2 name="hdcms.com">hdcms.com</h2>
	<h1>后盾人</h1>
</main>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#后面兄弟元素)后面兄弟元素

用于选择后面的所有兄弟元素。

```text
main article~* {
    color: green;
}
...

<main>
	<article>
		<h2 name="houdunren">houdunren.com</h2>
		<aside>
			<h2>houdunwang.com</h2>
		</aside>
	</article>
	<h2 name="hdcms.com">hdcms.com</h2>
	<h1>后盾人</h1>
</main>
```

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#属性选择器)属性选择器

根据属性来为元素设置样式也是常用的场景。

| 选择器              | 示例               | 描述                                                        |
| :------------------ | ------------------ | :---------------------------------------------------------- |
| [attribute]         | [target]           | 带有 target 属性所有元素                                    |
| [attribute=value]   | [target=_blank]    | targe 属性 等于"_blank" 的所有元素                          |
| [attribute~=value]  | [title~=houdunren] | title 属性包含单词 "houdunren" 的所有元素                   |
| [attribute\|=value] | [title\|=hd]       | `title 属性值为 "hd"的单词，或hd-cms` 以`-`连接的的独立单词 |
| [attribute*=value]  | a[src*="hdcms"]    | src 属性中包含 "hdcms" 字符的每个 元素                      |
| [attribute^=value]  | a[src^="https"]    | src 属性值以 "https" 开头的每个 元素                        |
| [attribute$=value]  | a[src$=".jpeg"]    | src 属性以 ".jpeg" 结尾的所有 元素                          |

为具有 `class` 属性的h1标签设置样式

```text
h1[class] {
    color: red;
}
...

<h1 class="container">houdunren.com</h1>
```

约束多个属性

```text
h1[class][id] {
    color: red;
}
...

<h1 class="container" id >houdunren.com</h1>
```

具体属性值设置样式

```text
a[href="https://www.houdunren.com"] {
    color: green;
}
...

<a href="https://www.houdunren.com">后盾人</a>
<a href="">HDCMS</a>
```

`^` 以指定值开头的元素

```text
h2[name^="hdcms"] {
    color: red;
}
...

<h2 name="houdunren">houdunren.com</h2>
<h2 name="hdcms.com">hdcms.com</h2>
```

`$` 以指定值结尾的元素

```text
<h2 name="houdunren">houdunren.com</h2>
<h2 name="hdcms.com">hdcms.com</h2>
...

h2[name$="com"] {
    color: red;
}
```

`*` 属性内部任何位置出现值的元素

```text
h2[name*="houdunren"] {
    color: red;
}
...

<h2 name="houdunren">houdunren.com</h2>
<h2 name="houdunren.com">hdcms.com</h2>
```

`~` 属性值中包含指定词汇的元素

```text
h2[name~="houdunren"] {
    color: red;
}
...

<h2 name="houdunren">houdunren.com</h2>
<h2 name="houdunren web">hdcms.com</h2>
```

`|` 以指定值开头或以属性连接破折号的元素

```text
h2[name|="houdunren"] {
    color: red;
}
...

<h2 name="houdunren">houdunren.com</h2>
<h2 name="houdunren-web">hdcms.com</h2>
```

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#伪类选择器)伪类选择器

为元素的不同状态或不确定存在的元素设置样式规则。

| 状态                 | 示例                  | 说明                                       |
| -------------------- | --------------------- | ------------------------------------------ |
| :link                | a:link                | 选择所有未被访问的链接                     |
| :visited             | a:visited             | 选择所有已被访问的链接                     |
| :hover               | a:hover               | 鼠标移动到元素上时                         |
| :active              | a:active              | 点击正在发生时                             |
| :focus               | input::focus          | 选择获得焦点的 input 元素                  |
| :root                | :root                 | 选择文档的根元素即html。                   |
| :empty               | p:empty               | 选择没有子元素的每个元素（包括文本节点）。 |
| :first-child         | p:first-child         | 选择属于父元素的第一个子元素的每个元素     |
| :last-child          | p:last-child          | 选择属于其父元素最后一个子元素每个元素。   |
| :first-of-type       | p:first-of-type       | 选择属于其父元素的首个元素的每个元素       |
| :last-of-type        | p:last-of-type        | 选择属于其父元素的最后元素的每个元素。     |
| :only-of-type        | p:only-of-type        | 选择属于其父元素唯一的元素的每个元素。     |
| :only-child          | p:only-child          | 选择属于其父元素的唯一子元素的每个元素。   |
| :nth-child(n)        | p:nth-child(2)        | 选择属于其父元素的第二个子元素的每个元素。 |
| :nth-child(odd)      | p:nth-child(odd)      | 选择属于其父元素的奇数元素。               |
| :nth-child(even)     | p:nth-child(even)     | 选择属于其父元素的偶数元素。               |
| :nth-of-type(n)      | p:nth-of-type(2)      | 选择属于其父元素第二个元素的每个元素。     |
| :nth-last-child(n)   | p:nth-last-child(2)   | 同上，从最后一个子元素开始计数。           |
| :nth-last-of-type(n) | p:nth-last-of-type(2) | 同上，但是从最后一个子元素开始计数。       |
| :not(selector)       | :not(p)               | 选择非元素的每个元素                       |

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#超链接伪类):超链接伪类

定义链接的不同状态

```text
a:link {
    color: red
}

a:visited {
    color: green
}

a:hover {
    color: blue
}

a:active {
    color: yellow
}
...

<a href="https://www.houdunren.com">后盾人</a>
```

不只是链接可以使用伪类，其他元素也可以使用。下面是对表单的点击与获取焦点状态的样式设置。

```text
input:focus {
    background: green;
}

input:hover {
    background: blue;
}

input:active {
    background: yellow;
}
...

<input type="text">
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#target):target

用于控制具有锚点目标元素的样式

```text
div {
	height: 900px;
}

div:target {
	color: red;
}
...

<a href="#hdcms">hdcms</a>
<div></div>
<div id="hdcms">
	hdcms内容管理系统
</div>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#root):root

根元素选择伪类即选择html

```text
:root {
    font-size: 100px;
}
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#empty):empty

没有内容和空白的元素。下面第一个p标签会产生样式，第二个不会因为有空白内容

```text
:empty {
    border: solid 2px red;
}
...

<p></p>
<p> </p>
```

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#结构伪类)结构伪类

下面来通过结构伪类选择器选择树状结构中的标签元素。

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#first-child):first-child

选择元素中`span` 标签并且是第一个。

```text
article span:first-child {
    color: red;
}
...

<article>
	<span>houdunren.com</span>
	<aside>
		<span>houdunwang.com</span>
		<span>hdcms.com</span>
	</aside>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#first-of-type):first-of-type

选择类型是`span` 的第一个元素

```text
article span:first-of-type {
    color: red;
}
...

<article>
	<span>houdunren.com</span>
	<aside>
		<strong>hdcms.com</strong>
		<span>houdunwang.com</span>
	</aside>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#last-child):last-child

选择元素中`span` 标签并且是最后一个。

```text
article span:last-child {
    color: red;
}
...

<article>
  <span>houdunren.com</span>
  <aside>
    <strong>hdcms.com</strong>
    <span>houdunwang.com</span>
  </aside>
  <span>hdphp.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#last-of-type):last-of-type

选择类型为`span` 的最后一个元素

```text
article span:last-of-type {
    color: red;
}
...

<article>
  <span>houdunren.com</span>
  <aside>
  	<span>houdunwang.com</span>
  	<strong>hdcms.com</strong>
  </aside>
  <span>hdphp.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#only-child):only-child

选择是唯一子元素的`span` 标签

```text
article span:only-child {
    color: red;
}
...

<article>
	<span>houdunren.com</span>
	<aside>
		<span>houdunwang.com</span>
	</aside>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#only-of-type):only-of-type

选择同级中类型是`span` 的唯一子元素

```text
article span:only-of-type {
    color: red;
}
...

<article>
	<span>houdunren.com</span>
	<aside>
		<span>houdunwang.com</span>
		<span>hdcms.com</span>
	</aside>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#nth-child-n):nth-child(n)

选择第二个元素并且是span标签的

```text
article span:nth-child(2) {
    color: red;
}
...

<article>
  <span>houdunren.com</span>
  <aside>
    <span>houdunwang.com</span>
    <span>hdcms.com</span>
  </aside>
  <span>hdphp.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#nth-of-type-n):nth-of-type(n)

选择第二个`span` 元素，不管中间的其他元素

```text
article span:nth-of-child(2) {
    color: red;
}
...

<article>
  <span>houdunren.com</span>
  <aside>
    <span>houdunwang.com</span>
    <span>hdcms.com</span>
  </aside>
  <span>hdphp.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#计算数量)计算数量

n为0/1/2/3... ，下面是隔列变色

```text
table tr>td:nth-child(2n+1) {
    background: green;
    color: white;
}
...

<table border="1">
  <tr>
    <td>houdunren.com</td>
    <td>hdcms.com</td>
    <td>后盾人</td>
    <td>houdunwang.com</td>
    <td>hdcms</td>
  </tr>
</table>
```

从第三个开始设置样式

```text
table tr>td:nth-child(n+3) {
    background: rgb(128, 35, 2);
    color: white;
}
```

设置前三个元素

```text
table tr>td:nth-child(-n+3) {
    background: rgb(128, 35, 2);
    color: white;
}
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#奇数元素)奇数元素

选择奇数单元格

```text
table tr>td:nth-child(odd) {
    background: green;
    color: white;
}
...

<table border="1">
  <tr>
    <td>houdunren.com</td>
    <td>hdcms.com</td>
    <td>后盾人</td>
    <td>houdunwang.com</td>
    <td>hdcms</td>
  </tr>
</table>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#偶数元素)偶数元素

选择偶数单元格

```text
table tr>td:nth-child(even) {
    background: green;
    color: white;
}
...

<table border="1">
  <tr>
    <td>houdunren.com</td>
    <td>hdcms.com</td>
    <td>后盾人</td>
    <td>houdunwang.com</td>
    <td>hdcms</td>
  </tr>
</table>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#nth-last-child-n):nth-last-child(n)

从最后一个元素开始获取

```text
table tr>td:nth-last-child(2n+1){
    background: green;
    color: white;
}
...

<table border="1">
  <tr>
    <td>houdunren.com</td>
    <td>hdcms.com</td>
    <td>后盾人</td>
    <td>houdunwang.com</td>
    <td>hdcms</td>
  </tr>
</table>
```

取最后两个元素

```text
main>ul li:nth-last-child(-n+2) {
	color: red;
}
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#nth-last-of-type-n):nth-last-of-type(n)

从最后一个元素开始选择`span` 标签 。

```text
article span:nth-last-of-type(1) {
    background: red;
    color: white;
}
...

<article>
  <aside>
  	<span>houdunren.com</span>
  	<span>houdunwang.com</span>
  	<strong>hdcms.com</strong>
  </aside>
	<span>hdphp.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#not-selector):not(selector)

排除第一个li元素

```text
ul li:not(:nth-child(1)) {
    background: red;
}
...

<ul>
  <li>houdunren.com</li>
  <li>hdcms.com</li>
  <li>后盾人</li>
</ul>
```

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#表单伪类)表单伪类

| 选择器    | 示例           | 说明                        |
| --------- | -------------- | --------------------------- |
| :enabled  | input:enabled  | 选择每个启用的 input 元素   |
| :disabled | input:disabled | 选择每个禁用的 input 元素   |
| :checked  | input:checked  | 选择每个被选中的 input 元素 |
| :required | input:required | 包含`required`属性的元素    |
| :optional | input:optional | 不包含`required`属性的元素  |
| :valid    | input:valid    | 验证通过的表单元素          |
| :invalid  | input:invalid  | 验证不通过的表单            |

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#表单属性样式)表单属性样式

```text
input:enabled {
    background: red;
}

input:disabled {
    background: #dddddd;
}

input:checked+label {
    color: green;
}
...

<input type="text" disabled>
<input type="text" name="info">

<input type="radio" name="sex" checked id="boy">
<label for="boy">男</label>
<input type="radio" name="sex" checked id="girl">
<label for="girl">女</label>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#表单必选样式)表单必选样式

```text
input:required {
    border: solid 2px blue;
}

input:optional {
	background: #dcdcdc; 
	border: none;
}
...

<input type="text" name="title" required>
<input type="text" name="name">
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#表单验证样式)表单验证样式

```text
input:valid {
    border: solid 1px green;
}

input:invalid {
    border: solid 1px red;
}
...

<form>
<input type="email">
<button>保存</button>
</form>
```

## [#](https://houdunren.gitee.io/note/css/2 选择器.html#字符伪类)字符伪类

| 状态           | 示例           | 说明                         |
| -------------- | -------------- | ---------------------------- |
| ::first-letter | p:first-letter | 选择每个元素的首字母         |
| ::first-line   | p:first-line   | 选择每个元素的首行           |
| ::before       | p:before       | 在每个元素的内容之前插入内容 |
| ::after        | p:after        | 在每个元素的内容之后插入内容 |

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#首字母大写)首字母大写

```text
p::first-line {
 font-size: 20px;
}
...

<p>
 后盾人不断更新视频教程
</p>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#段落首行处理)段落首行处理

```text
p::first-letter {
    font-size: 30px;
}
...

<p>
	后盾人不断更新视频教程
</p>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#在元素前添加)在元素前添加

```text
span::before {
    content: '⇰';
    color: red;
}
span::after {
    content: '⟲';
    color: green;
}
...

<span>后盾人</span>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#搜索框示例)搜索框示例

![image-20190813223919156](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAKgAAAAhCAYAAABN9OCkAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwcDLIMpgwCCemFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgsOZfwzRZF+Qzt3+54WAqkncZUjwK4UlKLk4H0HyBOSy4oKmFgYEwBspXLSwpA7A4gW6QI6Cggew6InQ5hbwCxkyDsI2A1IUHOQPYNIFsgOSMRaAbjCyBbJwlJPB2JDbUXBHhcXH18FEKNTAzNPQg4l3RQklpRAqKd8wsqizLTM0oUHIGhlKrgmZesp6NgZGBoycAACnOI6s83wGHJKMaBECsQY2CwdGFgYF6MEEuSYmDYDnS/JCdCTGU5AwN/BAPDtoaCxKJEuAMYv7EUpxkbQdjc2xkYWKf9//85nIGBXZOB4e/1//9/b////+8yoPm3GBgOfAMAkoFdEFXeaFAAAAIdSURBVHgB7Zs7roJAFIaP5FZGrIxbsLCyobUnsdQ94Ba0cQ+6BXdhQ2JiQk3UwthYmthgYeV1uOFGg0SYwMB4/kkICDPn8Z0/w9Pa/dEIDQQqSsCoaFwICwRCAhAohFBpAhBopcuD4H6eEez3++ef2AaBXAl0Op3M9l4EKkbLGMnsFQPYEZCd/HCKZycVvRKGQPWqF7toIVB2JdcrYQhUr3qxixYCZVfydAmfz2eazWbkOE66AQX1it3FF+QHZjUiEAQB9Xo9qtfrNJlMSo0cAi0VfzWdL5dLOp1OdL1eQ5GWGSVO8WXSr6jv7XZLo9EoUZzH45Eul4uS6CFQJZj1cmKaJgkRJrXD4UCDwSCcYZP65LUfAs2L5BfZsW2bPM+j+XxO4nr0XVuv1zQcDul2u707nN8+8T1o1Ha7XbSJNXMCi8VCfCccLu12+/68NBqN/2Pj8TgVKVlt1YT1SO7ifSnexUc0sBaPmnzfj82SYnadTqf0ECptNhvqdrsfYclqC3fxH9Hy7dBqtajf78cAGIYRitN13VTijBnIsAPXoBlgoesfgWazSavVKnxWWjQTzKBFE/5C+5ZlKcsKM6gy1HAkQwAClaGGMcoIQKDKUMORDAEIVIYaxigjAIEqQw1HMgQgUBlqGKOMQOwxk+y/75RFDEesCLy86mSVOZLVggBO8VqUiW+QECjf2muROQSqRZn4BgmB8q29Fpn/Ai4t44Qm/srhAAAAAElFTkSuQmCC)

```text
div {
    border: solid 1px #ddd;
    width: 150px;
}

div>input[type="text"] {
    border: none;
    outline: none;
}

div>input[type="text"]+span:after {
    content: "\21AA";
    font-size: 14px;
    cursor: pointer;
}
...

<div>
	<input type="text"><span></span>
</div>
```

### [#](https://houdunren.gitee.io/note/css/2 选择器.html#添加属性内容)添加属性内容

```text
h2::before {
	content: attr(title);
}
...

<h2 title="
```

# 元素权重

元素会被多个样式一层层作用，这就是层叠样式表的来源。如果多个样式做用在元素上就会产生优先级权重问题。

使用类、ID、伪类都有不同的权重，具体应用哪条规则要看权限大小。

- 相同权重的规则应用最后出现的
- 可以使用 `!important` 强制提升某个规则的权限

## [#](https://houdunren.gitee.io/note/css/3 元素权重.html#权重应用)权重应用

| 规则            | 粒度 |
| --------------- | ---- |
| ID              | 0100 |
| class，类属性值 | 0010 |
| 标签,伪元素     | 0001 |
| *               | 0000 |
| 行内样式        | 1000 |

下面是ID权限大于CLASS的示例

```text
<style>
  .color {
  	color: red;
  }

  #hot {
  	color: green;
  }
</style>
    
<h2 class="color" id="hot">HDCMS</h2>
```

属性权重的示例

```text
<style>
  /* 权重:0021 */
  h2[class="color"][id] {
		color: red;
  }

  /* 权重:0012 */
  article h2[class="color"] {
  	color: blue;
  }
</style>

<article>
	<h2 class="color" id="hot">HDCMS</h2>
</article>
```

行级权重优先级最高

```text
<style>
  /* 权重:0012 */
  article h2[class="color"] {
  	color: blue;
  }

  #hot {
  	color: black;
  }
</style>

<h2 class="color" id="hot" style="color:green;">HDCMS</h2>
```

## [#](https://houdunren.gitee.io/note/css/3 元素权重.html#强制优先级)强制优先级

有时在规则冲突时，为了让某个规则强制有效可以使用 !important。

```text
<style>
  h2 {
 	 color: red !important;
  }

  h2 {
 	 color: green;
  }
</style>

<h2>HDCMS</h2>
```

两条规则权限一样，默认应用第二个规则，但第一个规则使用了`!important` 提升了权限，所以被应用。

## [#](https://houdunren.gitee.io/note/css/3 元素权重.html#less)LESS

为了使 CSS 更易维护和扩展，并减少在书写规则时对权重的思考，使用LESS是不错的主意。

很多软件提供了自动生成LESS的功能，下面是在VSCODE中使用的方法。

1. 安装插件 [easy-less 编译LESS](https://marketplace.visualstudio.com/items?itemName=mrcrowl.easy-less)
2. 编辑扩展名为 `.less` 的文件将自动生成同名的 `.css` 文件。

下面是一个LESS的示例

```text
main {
    article {
        h1 {
            color: red;
        }
    }
}
```

将生成 `css` 文件如下

```text
main article h1 {
  color: red;
}
```

## [#](https://houdunren.gitee.io/note/css/3 元素权重.html#继承规则)继承规则

子元素可以继承父元素设置的样式。

- 子元素并不是全部样式。比如边框、高度等并不会继承。
- 继承的规则没有权重

```text
<style>
  article {
    color: red;
    border: solid 1px #ddd;
  }
</style>
...

<article>
	<h2>hdcms <span>内容管理系统</span></h2>
</article>
```

上例中 h2 标签没有设置颜色样式，将继承 `html` 的颜色，并且边框没有产生继承。

## [#](https://houdunren.gitee.io/note/css/3 元素权重.html#通配符)通配符

在开发中使用`*` 选择器会有一个问题。因为通配符的权限为0，而继承的规则没有权重，看以下代码产生的问题。

```text
<style>
  * {
  	color: red;
  }

  h2 {
  	color: blue;
  }
</style>

<article>
	<h2>hdcms <span>内容管理系统</span></h2>
</article>
```

`h2` 中的span并没有继承 `h2` 的颜色，就是因为继承没有权重。而使用了 `*` 权重为0的规则。

# 文本控制

## 文本基础

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#字体设置)字体设置

可以定义多个字体，系统会依次查找，比如 `'Courier New'` 字体不存在将使用 `Courier` 以此类推。

要使用通用字体，比如你电脑里有 `后盾人宋体` 在你电脑可以正常显示，但不保证在其他用户电脑可以正常，因为他们可能没有这个字体。

```text
font-family: 'Courier New', Courier, monospace;
```

**自定义字体**

可以声明自定义字段，如果客户端不存在将下载该字体，使用方式也是通过 `font-family` 引入。

```text
<style>
  @font-face {
  	font-family: "houdunren";
  	src: 	url("SourceHanSansSC-Light.otf") format("opentype"),
  				url("SourceHanSansSC-Heavy.otf") format("opentype");
  }

  span {
  	font-family: 'houdunren';
  }
</style>
```

| 字体  | 格式              |
| ----- | ----------------- |
| .otf  | opentype          |
| .woff | woff              |
| .ttf  | truetype          |
| .eot  | Embedded-opentype |

不建议使用中文字体，因为文件太大且大部分是商业字体。

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#字重定义)字重定义

字重指字的粗细定义。取值范围 `normal | bold | bolder | lighter | 100 ~900`。

400对应 `normal`,700对应 `bold` ，一般情况下使用 bold 或 normal 较多。

```text
<style>
span {
	font-weight: bold;
}

strong:last-child {
	font-weight: normal;
}
</style>
...

<span>houdunren.com</span>
<strong>hdcms.com</strong>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本字号)文本字号

字号用于控制字符的显示大小，包括 `xx-small | x-small | small | meidum | large | x-large | xx-large`。

**百分数**

百分数是子元素相对于父元素的大小，如父元素是20px，子元素设置为 200%即为你元素的两倍大小。

```text
<style>
  article {
  	font-size: 20px;
  }

  span {
  	font-size: 500%;
  }
</style>
...

<article>
	<span>houdunren.com</span>
</article>
```

**em**

em单位等同于百分数单位。

```text
<style>
  article {
  	font-size: 20px;
  }

  span {
  	font-size: 5em;
  }
</style>
...

<article>
	<span>houdunren.com</span>
</article>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本颜色)文本颜色

**字符串颜色**

可以使用如 `red | green` 等字符颜色声明

```text
color:red;
```

**使用十六进制网页颜色**

```text
color:#ddffde
```

如果颜色字符相同如 `#dddddd` 可以简写为 `#ddd`

**使用RGB颜色**

```text
color:rgb(38, 149, 162);
```

**透明颜色**

透明色从 `0~1` 间，表示从透明到不透明

```text
color:rgba(38, 149, 162,.2);
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#行高定义)行高定义

```text
div {
	line-height: 2em;
}
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#倾斜风格)倾斜风格

字符的倾斜样式控制

```text
<style>
  span {
  	font-style: italic;
  }

  em {
  	font-style: normal;
  }
</style>
...

<span>houdunren.com</span>
<hr>
<em>hdcms.com</em>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#组合定义)组合定义

可以使用 `font` 一次将字符样式定义，但要注意必须存在以下几点：

- 必须有字体规则
- 必须有字符大小规则

```text
span {
	font: bold italic 20px/1.5 'Courier New', Courier, monospace;
}
...

<span>houdunren.com</span>
```

> 上例中的 20px 为字体大小，1.5为1.5倍行高定义

## [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本样式)文本样式

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#大小转换)大小转换

小号大写字母

```text
span {
	font-variant: small-caps;
}
...

<span>houdunren.com</span>
```

字母大小写转换

```text
<style>
h2 {
  /* 首字母大小 */
  text-transform: capitalize;

  /* 全部大小 */
  text-transform: uppercase;

  /* 全部小写 */
  text-transform: lowercase;
  }
</style>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本线条)文本线条

添加隐藏删除线

```text
a {
	text-decoration: none;
}

span.underline {
	text-decoration: underline;
}

span.through {
	text-decoration: line-through;
}

span.overline {
	text-decoration: overline;
}
...

<a href="">houdunren.com</a>
<hr>
<span class="underline">下划线</span>
<hr>
<span class="through">删除线</span>
<hr>
<span class="overline">上划线</span>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#阴影控制)阴影控制

参数顺序为：颜色，水平偏移，垂直偏移，模糊度。

![image-20190816173740680](https://houdunren.gitee.io/note/assets/img/image-20190816173740680.5ca4bee3.png)

```text
<style>
  h2 {
  	text-shadow: rgba(13, 6, 89, 0.8) 3px 3px 5px;
  }
</style>
...

<h2>houdunren.com</h2>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#空白处理)空白处理

使用 `white-space` 控制文本空白显示。

| 选项     | 说明                                    |
| -------- | --------------------------------------- |
| pre      | 保留文本中的所有空白，类似使用 pre 标签 |
| nowrap   | 禁止文本换行                            |
| pre-wrap | 保留空白，保留换行符                    |
| pre-line | 空白合并，保留换行符                    |

```text
h2 {
	white-space: pre;
	width: 100px;
	border: solid 1px #ddd;
}
...

<h2>hou        dunren     .com</h2>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本溢出)文本溢出

溢出文本容器后换行处理

```text
h2 {
  overflow-wrap: break-word;
  width: 100px;
	border: solid 1px #ddd;
}
...

<h2>houdunren.com</h2>
```

溢出内容末尾添加 `...`

```text
h2 {
  width: 100px;
  border: solid 1px #ddd;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
...

<h2>houdunren.com</h2>
```

## [#](https://houdunren.gitee.io/note/css/4 文本控制.html#段落控制)段落控制

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#文本缩进)文本缩进

控制元素部的文本、图片进行缩进操作

```text
<style>
  p {
	  text-indent: 2em;
  }
</style>
<p>
后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</p>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#水平对齐)水平对齐

使用 `left|right|center` 对文本进行对齐操作

```text
h2 {
	text-align: center;
}
...
<h2>houdunren.com</h2>
```

为了让段落内容看得舒服，需要设置合适的行高

```text
p {
	text-indent: 2em;
	line-height: 2em;
}
...
<p>
后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</p>
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#垂直对齐)垂直对齐

使用 `vertical-align` 用于定义内容的垂直对齐风格，包括`middle | baseline | sub | super` 等。

**图像在段落中居中对齐**

```text
img {
	height: 50px;
	width: 50px;
	vertical-align: middle;
}
...

<p>
<img src="houdunren.jpg">后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</p>
```

**顶部与底部对齐**

`bottom | top` 相对于行框底部或顶部对齐。

```text
h2>span {
	vertical-align: bottom;
	font-size: 12px;
}
...

<h2>houdunren.com <span>hdcms</span></h2>
```

**使用单位对齐**

可以使用具体数值设置对齐的位置。

```text
h2>span {
	vertical-align: -20px;
	font-size: 12px;
}
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#字符间隔)字符间隔

**单词与字符间距**

使用 `word-spacing` 与 `letter-spacing` 控制单词与字符间距。

```text
h2 {
	word-spacing: 2em;
	letter-spacing: 3em;
}
```

### [#](https://houdunren.gitee.io/note/css/4 文本控制.html#排版模式)排版模式

| 模式          | 说明                                     |
| ------------- | ---------------------------------------- |
| horizontal-tb | 水平方向自上而下的书写方式               |
| vertical-rl   | 垂直方向自右而左的书写方式               |
| vertical-lr   | 垂直方向内内容从上到下，水平方向从左到右 |

![image-20190816183805169](https://houdunren.gitee.io/note/assets/img/image-20190816183805169.311a6bb3.png)

```html
div {
  height: 200px;
  border: solid 1px #ddd;
  writing-mode: vertical-rl;
}
...

<div>
后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</div>
```

# 盒子模型

## 盒子模型

![image-20190817163854641](https://houdunren.gitee.io/note/assets/img/image-20190817163854641.0f6c1947.png)

下而是基本使用示例

```text
<style>
  a {
    display: inline-block;
    border: solid 1px #ddd;
    text-align: center;
    padding: 10px 20px;
    margin-right: 30px;
  }
</style>
...

<a href="">MYSQL</a>
<a href="">LINUX</a>
<a href="">PHP</a>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#外边距)外边距

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#声明定义)声明定义

边距顺序依次为：上、右、下、左。

![image-20190817185522220](https://houdunren.gitee.io/note/assets/img/image-20190817185522220.41d1113e.png)

```text
<style>
  main {
    border: solid 1px red;
    width: 500px;
    height: 500px;
    margin: 0 auto;
  }

  h2 {
    border: solid 2px green;
    width: 300px;
    height: 300px;
    margin: 50px 80px 100px 150px;
  }
</style>
...

<main>
<h2>houdunren.com</h2>
</main>
```

下例定义上下`50px`边距，左右`80px`边距

```text
 margin: 50px 80px;
```

下面将边距全部定义为 `100px`

```text
margin:100px;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#居中设置)居中设置

`margin` 设置auto 后，浏览器会自动

```text
<style>
article {
	border: solid 1px red;
}

h2,h3 {
	border: solid 10px #ddd;
}

h2 {
  width: 300px;
  margin-left: 200px;
  margin-right: 200px;
}

h3 {
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}
</style>
...

<article>
<h2>houdunren.com</h2>
<h3>hdcms.com</h3>
</article>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#负值设置)负值设置

```text
<style>
  main {
    border: solid 1px red;
    width: 300px;
    margin: 0 auto;
  }

  h2 {
    border: solid 2px green;
    margin-left: -50px;
    margin-right: -50px;
    text-align: center;
  }
</style>
...

<main>
	<h2>houdunren.com</h2>
</main>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#边距合并)边距合并

相邻元素的纵向外边距会进行合并

```text
<style>
	h2 {
    border: solid 2px green;
    margin-bottom: 20px;
  }

  h3 {
    border: solid 2px green;
    height: 20px;
  }
</style>
...

<h2>houdunren.com</h2>
<h2>hdcms.com</h2>
<h3></h3>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#内边距)内边距

内边距使用 `padding` 进行定义，使用语法与 `margin` 相似。

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#基本使用)基本使用

```text
<style>
  a {
    padding: 10px 30px;
    border: solid 1px #ddd;
    border-radius: 5px;
  }

  a:hover {
    background: rgb(3, 78, 110);
    color: white;
  }
</style>
...

<a href="">MYSQL</a>
<a href="">CSS</a>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#box-sizing)BOX-SIZING

宽度与高度包括内边距与边框。

```text
h2 {
  border: solid 10px #ddd;
  height: 60px;
  width: 200px;
  padding:50px;
  box-sizing: border-box;
}
...

<h2>houdunren.com</h2>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#边框设计)边框设计

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#样式选择)样式选择

| 类型   | 描述                                                  |
| :----- | :---------------------------------------------------- |
| none   | 定义无边框。                                          |
| dotted | 定义点状边框。在大多数浏览器中呈现为实线。            |
| dashed | 定义虚线。在大多数浏览器中呈现为实线。                |
| solid  | 定义实线。                                            |
| double | 定义双线。双线的宽度等于 border-width 的值。          |
| groove | 定义 3D 凹槽边框。其效果取决于 border-color 的值。    |
| ridge  | 定义 3D 垄状边框。其效果取决于 border-color 的值。    |
| inset  | 定义 3D inset 边框。其效果取决于 border-color 的值。  |
| outset | 定义 3D outset 边框。其效果取决于 border-color 的值。 |

一次定义四个边

```text
h2 {
	border-style: double;
}
```

样式顺序为上、右、下、左，可以分别进行定义

```text
h2 {
	border-style: outset solid dotted double;
	border-width: 8px;
}
```

单独设置一边样式

| 规则                | 说明 |
| ------------------- | ---- |
| border-top-style    | 顶边 |
| border-right-style  | 右边 |
| border-bottom-style | 下边 |
| border-left-style   | 左边 |
| border-style        | 四边 |

```text
h2 {
	border-top-style: double;
	border-width: 8px;
}
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#边框宽度)边框宽度

边框可以通过以下规则来设置

| 规则                | 说明 |
| ------------------- | ---- |
| border-top-width    | 顶边 |
| border-right-width  | 右边 |
| border-bottom-width | 下边 |
| border-left-width   | 左边 |
| border-width        | 四边 |

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#边框颜色)边框颜色

| 规则                | 说明 |
| ------------------- | ---- |
| border-top-color    | 顶边 |
| border-right-color  | 右边 |
| border-bottom-color | 下边 |
| border-left-color   | 左边 |
| border-color        | 四边 |

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#简写规则)简写规则

| 规则          | 说明 |
| ------------- | ---- |
| border-top    | 顶边 |
| border-right  | 右边 |
| border-bottom | 下边 |
| border-left   | 左边 |
| border        | 四边 |

设置底部边框

```text
border-bottom: solid 5px red;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#行元素边框)行元素边框

行元素也可以进行边框设置

```text
em {
	border-bottom: solid 2px red;
}
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#圆角边框)圆角边框

使用 `border-radius` 规则设置圆角，可以使用`px | %` 等单位。也支持四个边分别设置。

| 选项                       | 说明 |
| -------------------------- | ---- |
| border-top-left-radius     | 上左 |
| border-top-right-radius    | 上右 |
| border-bottom-left-radius  | 下载 |
| border-bottom-right-radius | 下右 |

```text
h2 {
	border-radius: 10px;
	border: solid 2px red;
}
```

通过边框绘制圆

```text
div {
  width: 100px;
  height: 100px;
  border: solid 3px red;
  border-radius: 50%;
}
```

定义不同边

```text
border-radius: 10px 30px 50px 100px;
```

行元素绘制圆角

![image-20190817193835791](https://houdunren.gitee.io/note/assets/img/image-20190817193835791.b20aec8a.png)

```text
em {
	border-radius: 50%;
	border-bottom: solid 2px red;
}
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#轮廓线)轮廓线

元素在获取焦点时产生，并且轮廓线不占用空间。可以使用伪类 `:focus` 定义样式。

- 轮廓线显示在边框外面
- 轮廓线不影响页面布局

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#线条样式)线条样式

| 值     | 描述                                                |
| :----- | :-------------------------------------------------- |
| none   | 默认。定义无轮廓。                                  |
| dotted | 定义点状的轮廓。                                    |
| dashed | 定义虚线轮廓。                                      |
| solid  | 定义实线轮廓。                                      |
| double | 定义双线轮廓。双线的宽度等同于 outline-width 的值。 |
| groove | 定义 3D 凹槽轮廓。此效果取决于 outline-color 值。   |
| ridge  | 定义 3D 凸槽轮廓。此效果取决于 outline-color 值。   |
| inset  | 定义 3D 凹边轮廓。此效果取决于 outline-color 值。   |
| outset | 定义 3D 凸边轮廓。此效果取决于 outline-color 值。   |

```text
outline-style: double;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#线宽设置)线宽设置

```text
outline-width: 10px;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#线条颜色)线条颜色

```text
outline-color: red;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#组合定义)组合定义

```text
outline: red solid 2px;
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#表单轮廓线)表单轮廓线

表单默认具有轮廓线，但有时并不好看，使用以下样式规则去除。

```text
input:focus {
	outline: none;
}
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#display)DISPLAY

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#控制显示隐藏)控制显示隐藏

使用 `display` 控制元素的显示机制。

| 选项         | 说明                        |
| ------------ | --------------------------- |
| none         | 隐藏元素                    |
| block        | 显示为块元素                |
| inline       | 显示为行元素，不能设置宽/高 |
| inline-block | 行级块元素，允许设置宽/高f  |

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#行转块元素)行转块元素

```text
a {
  border: solid 1px #ddd;
  display: block;
  margin-bottom: 5px;
}
...

<a href="">houdunren.com</a>
<a href="">houdunren.com</a>
<a href="">houdunren.com</a>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#块转为行元素)块转为行元素

```text
ul>li {
  display: inline;
  padding: 5px 10px;
  border: solid 1px #ddd;
}

ul>li:hover {
  background: green;
  color: white;
  cursor: pointer;
}
...

<ul>
<li>hdcms.com</li>
<li>houdunren.com</li>
<li>后盾人</li>
</ul>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#行级块使用)行级块使用

```text
a {
  display: inline-block;
  width: 30%;
  height: 50px;
  border: solid 1px #ddd;
  text-align: center;
  line-height: 3em;
}
...

<a href="">MYSQL</a>
<a href="">LINUX</a>
<a href="">PHP</a>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#visibility)VISIBILITY

控制元素的显示隐藏，在隐藏后空间位也保留。

![image-20190822213523648](data:image/png;base64,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)

```text
<style>
	article {
    padding: 30px;
    border: solid 2px red;
    width: 200px;
  }
  article div {
    width: 100px;
    height: 100px;
    border: solid 2px red;
    padding: 20px;
  }
  article div:nth-of-type(1) {
    visibility: hidden;
  }
</style>

<article>
	<div></div>
	<div></div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#溢出控制)溢出控制

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#隐藏控制)隐藏控制

| 选项   | 说明                                                 |
| ------ | ---------------------------------------------------- |
| hidden | 溢出内容隐藏                                         |
| scroll | 显示滚动条（有些浏览器会一直显示，有些在滚动时显示） |
| auto   | 根据内容自动处理滚动条                               |

**溢出隐藏**

![image-20190822210806149](https://houdunren.gitee.io/note/assets/img/image-20190822210806149.53098d3a.png)

```text
div {
  width: 400px;
  height: 100px;
  border: solid 2px #ddd;
  padding: 20px;
  overflow: hidden;
}
```

**溢出产生滚动条**

不同浏览器处理方式不同，有些直接显示出来，有些在滚动时才显示。

![image-20190822210842353](https://houdunren.gitee.io/note/assets/img/image-20190822210842353.e45f2ebb.png)

```text
div {
  width: 400px;
  height: 100px;
  border: solid 2px #ddd;
  padding: 20px;
  overflow: scroll;
}
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#文本溢出)文本溢出

**单行文本溢出**

![image-20190822211257747](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAcgAAABXCAYAAACA5tXIAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDGIMhgxiCcmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisHo35nyq0l2u+fd+g+ZftWDWmehTAlZJanAyk/wBxenJBUQkDA2MKkK1cXlIAYncA2SJFQEcB2XNA7HQIewOInQRhHwGrCQlyBrJvANkCyRmJQDMYXwDZOklI4ulIbKi9IMDr464Q6hMS5Bju6eJKwL0kg5LUihIQ7ZxfUFmUmZ5RouAIDKVUBc+8ZD0dBSMDQ0sGBlCYQ1R/vgEOS0YxDoRYgRgDg8UMoOBDhFg80A/b5RgY+PsQYmpA/wp4MTAc3FeQWJQIdwDjN5biNGMjCJt7OwMD67T//z+HMzCwazIw/L3+///v7f///13GwMB8i4HhwDcAR71hseitBrYAABypSURBVHgB7ZwDlCRJ14Zjdmdt25i1bdu2bdu2bdv2ztrmrG3b9eUT/39ro6Mjs7Ora2qnct57TnVmRgbfuHEVkd2rlpETCQEhIASEgBAQAh0QGKTDkx6EgBAQAkJACAgBj4AUpBhBCAgBISAEhEACASnIBChKEgJCQAgIASEgBSkeEAJCQAgIASGQQEAKMgGKkoSAEBACQkAISEGKB4SAEBACQkAIJBDoHaf169cvTtKzEBACQkAICIHKIdCnT5/CMcmDLIRHL4WAEBACQmBgRaCTB2lAdKVZLZ+uQkAICAEhIATaCYGykVJ5kO00q+qrEBACQkAItAwBKciWQa2GhIAQEAJCoJ0QkIJsp9lSX4WAEBACQqBlCEhBtgxqNSQEhIAQEALthIAUZDvNlvoqBISAEBACLUNACrJlUKshISAEhIAQaCcEpCDbabbUVyEgBISAEGgZAlKQLYNaDQkBISAEhEA7ISAF2U6zpb4KASEgBIRAyxCQgmwZ1GpICAgBISAE2gkBKch2mi31VQgIASEgBFqGgBRky6BWQ0JACAgBIdBOCEhBttNsqa9CQAgIASHQMgSkIFsGtRoSAkJACAiBdkJACrKdZkt9FQJCQAgIgZYhIAXZMqjVkBAQAkJACLQTAlKQ7TRb6qsQEAJCQAi0DAEpyJZBrYaEgBAQAkKgnRCQgmyn2VJfhYAQEAJCoGUISEG2DGo1JASEgBAQAu2EgBRkO82W+ioEhIAQEAItQ0AKsmVQqyEhIASEgBBoJwQGaAX5888/9wjLb7/91v31119d1vH222+79957r8t8qQxffPGFe/rpp93ff/+det0WaTfffLP7+OOPG+5rrVZzn3zyifvnn39y6/j+++/dSy+9lPueF5R/55133FdffVWYr3++pO3nnnuufzaRrBt8Hn/8cffnn38m33eV+Msvv7h7773X/frrrz7riy++6N56662uinV6f+utt7rPPvvMp1Nnd9Yg83f//fc71t1/RV9//bV75pln/qvm3SuvvNIln3e3c6yvzz//vGHeyGvv999/d/fcc0+dZ/LyDczpvVs9eCabhffTTz+5H3/80S9ArjD2m2++6d544w336quvOhY46TDG6KOPXu8mAhRhzsKlHlvEP/zwg/voo4/cu+++61B41AGdcsopbuutt66XT93stddebthhh3Xnnntu6nVh2lFHHeWuvPLKhhVsYeUtePnEE0+45ZZbzl111VVu1VVXbajFgw8+2O2///5un332cdyn6OGHH3bLLLOMN1gGHXTQVBaHkphkkkncfvvt5w488MBkHkt88skn3aOPPmqPpa5DDjmk22KLLXLzwjcLLLCA56Pdd9/dHX744a5Xr165+Zv1AiNuzTXX9IIdvh1llFFKVQ3fmTGBoXbQQQe5Aw44wI066qjutNNOc8MPP7xbZ5116nVtuOGGbuihh64/c7PZZpu5RRdd1M89a405uu2229ySSy7p1w3r8I477nCjjTZah3Kph/vuu8/X9cILL7iRRhoplaWexpjvvvvu+nOZm/nnn79T/+Ny1157rdtll10c8qAr+u2339xQQw3lhhtuODfCCCPkZkeu7Ljjju64447LzWMv4FvG369fP0vKvTJ3GOYmy5CJ3HMlHVlHPSbLjj32WLfTTjvV6+tp/7/77js/XxdffHGdTzCQmP8Urb766m6++eZLvapsWssVJILn6KOP7gQoSpCFPdlkk7l5553XbbLJJm7yySf3iivMfNhhh3lFRn6U2ogjjuiGGWYYn+Whhx5yG220kVtqqaXceOON538TTDBBWDx5j/eH8CxDKHHzhFD2Z511lmeaG2+8sVPx6aabzk066aQd0rGuGT+KCZp77rn94osFyg033OCoE6FteEw00UQd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)

```text
div {
  width: 400px;
  height: 100px;
  border: solid 2px #ddd;
  padding: 20px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

**多行文本溢出控制**

![image-20190822212007695](https://houdunren.gitee.io/note/assets/img/image-20190822212007695.0de35203.png)

```text
div {
  width: 200px;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}
```

## [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#尺寸定义)尺寸定义

可以使用多种方式为元素设置宽、高尺寸。

| 选项           | 说明             |
| -------------- | ---------------- |
| width          | 宽度             |
| height         | 高度             |
| min-width      | 最小宽度         |
| min-height     | 最小高度         |
| max-width      | 最大宽度         |
| max-height     | 最大高度         |
| fill-available | 撑满可用的空间   |
| fit-content    | 根据内容适应尺寸 |

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#min-max)min&max

正文中不希望图片太大造成溢出窗口，也不希望太小影响美观，使用以下代码可以做到约束。

![image-20190822205823322](https://houdunren.gitee.io/note/assets/img/image-20190822205823322.95f03715.png)

```text
<style>
	div {
    width: 600px;
    border: solid 2px #ddd;
    padding: 20px;
  }
  div img {
    min-width: 50%;
    max-width: 90%;
  }
</style>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#fill-available)fill-available

在`chrome` 浏览器中使用前缀 `-webkit` 书写样式。

下面是行块元素可以撑满可用空间后的效果。

![image-20190928120513013](data:image/png;base64,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)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
        }

        main {
            background: #9b59b6;
            height: 100px;
            padding: 20px;
            box-sizing: border-box;
        }

        span {
            background: #e67e22;
            display: inline-block;
            width: -webkit-fill-available;
            height: -webkit-fill-available;
        }
    </style>
</head>

<body>
    <main>
        <span>
            houdunren.com
        </span>
    </main>
</body> 
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#fit-content)fit-content

下面是根据内容自动适应宽度，让元素居中显示的效果。

![image-20190928112415984](data:image/png;base64,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)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
        }

        h2 {
            text-align: center;
            background: #f1c40f;
            width: fit-content;
            margin: auto;
        }
    </style>
</head>

<body>
    <h2>houdunren.com</h2>
</body>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#min-content)min-content

使用`min-content` 将容器尺寸按最小元素宽度设置。

![image-20190928113203223](data:image/png;base64,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)

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
        }

        main {
            width: min-content;
            margin: auto;
        }

        div {
            margin-bottom: 20px;
            background: #f1c40f;
            word-break: break-all;
            padding: 10px;
        }

        div:nth-child(1) {
            width: 100px;
        }
    </style>
</head>

<body>
    <main>
        <div>houdunren.com</div>
        <div>hdcms.com</div>
    </main>
</body>
```

### [#](https://houdunren.gitee.io/note/css/5 盒子模型.html#max-content)max-content

容器尺寸按子元素最大宽度设置。

![image-20190928113523718](https://houdunren.gitee.io/note/assets/img/image-20190928113523718.9c10a85d.png)

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
        }

        main {
            width: max-content;
            margin: auto;
        }

        div {
            margin-bottom: 20px;
            background: #f1c40f;
            word-break: break-all;
            padding: 10px;
        }
    </style>
</head>

<body>
    <main>
        <div>在线视频教程学习网站。houdunren.com</div>
        <div>hdcms.com</div>
    </main>
</body>
```

# 背景处理

## 背景样式

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景颜色)背景颜色

背景颜色可以使用 `rga | rgba | 十六进制` 等颜色格式

```text
<style>
  h2 {
		background-color: red;
  }
</style>
...

<h2>houdunren.com</h2>
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景图片)背景图片

可以使用 `png| gif |jpeg` 等图片做为背景使用

```text
background-image: url(icon-s.jpg);
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景裁切)背景裁切

| 选项        | 说明                 |
| ----------- | -------------------- |
| border-box  | 包括边框             |
| padding-box | 不含边框，包括内边距 |
| content-box | 内容区域             |

```text
background-clip: border-box;
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景重复)背景重复

用于设置背景重复的规则

| 选项      | 说明                 |
| --------- | -------------------- |
| repeat    | 水平、垂直重复       |
| repeat-x  | 水平重复             |
| repeat-y  | 垂直重复             |
| no-repeat | 不重复               |
| space     | 背景图片对称均匀分布 |

```text
background-repeat: repeat-y
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景滚动)背景滚动

用于设置在页面滚动时的图片处理方式

| 选项   | 说明     |
| ------ | -------- |
| scroll | 背景滚动 |
| fixed  | 背景固定 |

```text
background-attachment: fixed;
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景位置)背景位置

用于设置背景图片的水平、垂直定位。

| 选项   | 说明     |
| ------ | -------- |
| left   | 左对齐   |
| right  | 右对齐   |
| center | 居中对齐 |
| top    | 顶端对齐 |
| bottom | 底部对齐 |

居中对齐

```text
background-position: center;
或
background-position: 50% 50%;
```

水平居右，垂直居中

```text
background-position: right center;
或
background-position: 100% 50%;
```

使用具体数值定义

```text
background-position: 100px 100px;
也支持使用负值
background-position: -200px 100px;
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#背景尺寸)背景尺寸

| 选项    | 说明                                       |
| ------- | ------------------------------------------ |
| cover   | 背景完全覆盖，可能会有背景溢出             |
| contain | 图片不溢出的放在容器中，可能会漏出部分区域 |

指定数值定义宽高尺寸

```text
background-size: 50% 100%;
或
background-size: 200px 200px;
```

宽度固定高度自动

```text
background-size: 50% auto;
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#多个背景)多个背景

后定义的背景置于底层

```text
background-image: url(xj-small.png), url(bg.png);
```

多属性定义

```text
background-image: url(xj-small.png), url(bg.png);
background-repeat: no-repeat;
background-position: top left, right bottom;
```

可以一次定义多个背景图片。

```text
background: url(xj-small.png) left 50% no-repeat,
                url(bg.png) right 100% no-repeat red;
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#组合设置)组合设置

可以使用一条指令设置背景

```text
background: red url(xj-small.png) no-repeat right 50% fixed;
```

## [#](https://houdunren.gitee.io/note/css/6 背景处理.html#盒子阴影)盒子阴影

可以使用 `box-shadow` 对盒子元素设置阴影，参数为 `水平偏移,垂直偏移,模糊度,颜色` 构成。

![image-20190818221126973](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQQAAADyCAYAAACrtLu6AAAMSWlDQ1BJQ0MgUHJvZmlsZQAASImVVwdYU8kWnltSSWiBCEgJvYlSpEsJoUUQkCrYCEkgocSQEETsLssquHYRARu6KqLoWgBZK+paF8HuWh6KqCjrYsGGypsUWNf93nvfO9839/45c85/SubeOwOATg1PKs1FdQHIkxTI4iNCWJNS01ikLkAAIwEV6AJ7Hl8uZcfFRQMoQ/e/y9sbAFHer7oouf45/19FTyCU8wFA4iDOEMj5eRAfBAAv4UtlBQAQfaDeemaBVImnQGwggwlCLFXiLDUuUeIMNa5U2STGcyDeDQCZxuPJsgDQboZ6ViE/C/Jo34LYVSIQSwDQIUMcyBfxBBBHQjwqL2+GEkM74JDxFU/W3zgzhjl5vKxhrK5FJeRQsVyay5v1f7bjf0termIohh0cNJEsMl5ZM+zbrZwZUUpMg7hXkhETC7E+xO/FApU9xChVpIhMUtujpnw5B/YMMCF2FfBCoyA2hThckhsTrdFnZIrDuRDDFYIWiQu4iRrfxUJ5WIKGs0Y2Iz52CGfKOGyNbwNPpoqrtD+tyElia/hviYTcIf43xaLEFHXOGLVQnBwDsTbETHlOQpTaBrMpFnFihmxkinhl/jYQ+wklESFqfmxapiw8XmMvy5MP1YstFom5MRpcVSBKjNTw7ObzVPkbQdwslLCThniE8knRQ7UIhKFh6tqxdqEkSVMv1iktCInX+L6S5sZp7HGqMDdCqbeC2FRemKDxxQML4IJU8+Mx0oK4RHWeeEY2b3ycOh+8CEQDDggFLKCAIwPMANlA3Nbb1At/qWfCAQ/IQBYQAheNZsgjRTUjgdcEUAz+gEgI5MN+IapZISiE+s/DWvXVBWSqZgtVHjngMcR5IArkwt8KlZdkOFoyeAQ14n9E58Ncc+FQzv1Tx4aaaI1GMcTL0hmyJIYRQ4mRxHCiI26CB+L+eDS8BsPhjvvgvkPZ/mVPeEzoIDwkXCd0Em5PFy+SfVMPC0wAnTBCuKbmjK9rxu0gqyceggdAfsiNM3ET4IKPhZHYeBCM7Qm1HE3myuq/5f5bDV91XWNHcaWglBGUYIrDt57aTtqewyzKnn7dIXWuGcN95QzPfBuf81WnBfAe9a0lthg7gJ3FTmLnsSNYE2Bhx7Fm7BJ2VImHV9Ej1SoaihavyicH8oj/EY+nianspNy13rXH9ZN6rkBYpHw/As4M6SyZOEtUwGLDN7+QxZXwR49iubu6+QKg/I6oX1OvmarvA8K88Jcu/wQAvmVQmfWXjmcNwOHHADDe/qWzfgUfjxUAHG3nK2SFah2uvBDg10kHPlHGwBxYAwdYjzvwAv4gGISB8SAWJIJUMA12WQTXswzMBHPAQlAKysEKsBZUgU1gK9gJ9oD9oAkcASfBr+AiaAfXwR24errBc9AH3oIBBEFICB1hIMaIBWKLOCPuiA8SiIQh0Ug8koqkI1mIBFEgc5DvkHJkFVKFbEHqkJ+Rw8hJ5DzSgdxGHiA9yCvkI4qhNNQANUPt0DGoD8pGo9BEdCqaheajxWgJugytRGvR3WgjehK9iF5HO9HnaD8GMC2MiVliLpgPxsFisTQsE5Nh87AyrAKrxRqwFvg/X8U6sV7sA07EGTgLd4ErOBJPwvl4Pj4PX4pX4TvxRvw0fhV/gPfhXwh0ginBmeBH4BImEbIIMwmlhArCdsIhwhn4NHUT3hKJRCbRnugNn8ZUYjZxNnEpcQNxL/EEsYPYRewnkUjGJGdSACmWxCMVkEpJ60m7ScdJV0jdpPdkLbIF2Z0cTk4jS8iLyBXkXeRj5CvkJ+QBii7FluJHiaUIKLMoyynbKC2Uy5RuygBVj2pPDaAmUrOpC6mV1AbqGepd6mstLS0rLV+tiVpirQValVr7tM5pPdD6QNOnOdE4tCk0BW0ZbQftBO027TWdTrejB9PT6AX0ZfQ6+in6ffp7bYb2aG2utkB7vna1dqP2Fe0XOhQdWx22zjSdYp0KnQM6l3V6dSm6drocXZ7uPN1q3cO6N3X79Rh6bnqxenl6S/V26Z3Xe6pP0rfTD9MX6Jfob9U/pd/FwBjWDA6Dz/iOsY1xhtFtQDSwN+AaZBuUG+wxaDPoM9Q3HGuYbFhkWG141LCTiTHtmFxmLnM5cz/zBvPjCLMR7BHCEUtGNIy4MuKd0UijYCOhUZnRXqPrRh+NWcZhxjnGK42bjO+Z4CZOJhNNZppsNDlj0jvSYKT/SP7IspH7R/5uipo6mcabzjbdanrJtN/M3CzCTGq23uyUWa850zzYPNt8jfkx8x4LhkWghdhijcVxi2csQxablcuqZJ1m9VmaWkZaKiy3WLZZDljZWyVZLbLaa3XPmmrtY51pvca61brPxsJmgs0cm3qb320ptj62Itt1tmdt39nZ26XY/WDXZPfU3siea19sX29/14HuEOSQ71DrcM2R6OjjmOO4wbHdCXXydBI5VTtddkadvZzFzhucO0YRRvmOkoyqHXXThebCdil0qXd5MJo5Onr0otFNo1+MsRmTNmblmLNjvrh6uua6bnO946bvNt5tkVuL2yt3J3e+e7X7NQ+6R7jHfI9mj5djnccKx24ce8uT4TnB8wfPVs/PXt5eMq8Grx5vG+907xrvmz4GPnE+S33O+RJ8Q3zn+x7x/eDn5Vfgt9/vT38X/xz/Xf5Px9mPE47bNq4rwCqAF7AloDOQFZgeuDmwM8gyiBdUG/Qw2DpYELw9+AnbkZ3N3s1+EeIaIgs5FPKO48eZyzkRioVGhJaFtoXphyWFVYXdD7cKzwqvD++L8IyYHXEikhAZFbky8ibXjMvn1nH7xnuPnzv+dBQtKiGqKuphtFO0LLplAjph/ITVE+7G2MZIYppiQSw3dnXsvTj7uPy4XyYSJ8ZNrJ74ON4tfk782QRGwvSEXQlvE0MSlyfeSXJIUiS1JuskT0muS36XEpqyKqVz0phJcyddTDVJFac2p5HSktO2p/VPDpu8dnL3FM8ppVNuTLWfWjT1/DSTabnTjk7Xmc6bfiCdkJ6Sviv9Ey+WV8vrz+Bm1GT08Tn8dfzngmDBGkGPMEC4SvgkMyBzVebTrICs1Vk9oiBRhahXzBFXiV9mR2Zvyn6XE5uzI2cwNyV3bx45Lz3vsERfkiM5PcN8RtGMDqmztFTame+Xvza/TxYl2y5H5FPlzQUGcMN+SeGg+F7xoDCwsLrw/czkmQeK9IokRZdmOc1aMutJcXjxT7Px2fzZrXMs5yyc82Aue+6Weci8jHmt863nl8zvXhCxYOdC6sKchb8tcl20atGb71K+aykxK1lQ0vV9xPf1pdqlstKbP/j/sGkxvli8uG2Jx5L1S76UCcoulLuWV5R/WspfeuFHtx8rfxxclrmsbbnX8o0riCskK26sDFq5c5XequJVXasnrG5cw1pTtubN2ulrz1eMrdi0jrpOsa6zMrqyeb3N+hXrP1WJqq5Xh1TvrTGtWVLzboNgw5WNwRsbNpltKt/0cbN4860tEVsaa+1qK7YStxZufbwtedvZn3x+qttusr18++cdkh2dO+N3nq7zrqvbZbpreT1ar6jv2T1ld/ue0D3NDS4NW/Yy95bvA/sU+579nP7zjf1R+1sP+BxoOGh7sOYQ41BZI9I4q7GvSdTU2Zza3HF4/OHWFv+WQ7+M/mXHEcsj1UcNjy4/Rj1WcmzwePHx/hPSE70ns052tU5vvXNq0qlrpyeebjsTdebcr+G/njrLPnv8XMC5I+f9zh++4HOh6aLXxcZLnpcO/eb526E2r7bGy96Xm9t921s6xnUcuxJ05eTV0Ku/XuNeu3g95nrHjaQbt25Oudl5S3Dr6e3c2y9/L/x94M6Cu4S7Zfd071XcN71f+y/Hf+3t9Oo8+iD0waWHCQ/vdPG7nj+SP/rUXfKY/rjiicWTuqfuT4/0hPe0P5v8rPu59PlAb+kfen/UvHB4cfDP4D8v9U3q634pezn4aulr49c73ox909of13//bd7bgXdl743f7/zg8+Hsx5SPTwZmfiJ9qvzs+LnlS9SXu4N5g4NSnoyn2gpgcKCZmQC82gEAPRXuHdoBoE5Wn/NUgqjPpioE/hNWnwVV4gXAjmAAkhYAEA33KBvhsIWYBu/KrXpiMEA9PIaHRuSZHu5qLho88RDeDw6+NgOA1ALAZ9ng4MCGwcHP22CytwE4ka8+XyqFCM8Gm8coUXv3C/Ct/BuksX9wSo4AMwAAAAlwSFlzAAAWJQAAFiUBSVIk8AAACtBJREFUeAHt3AlSG9sSBFAxeSHsf03sAgKCwd+XHxf1E8YmnGohUkcRet2aSl2ndJOWsd/Zz1+XjQsBAgR+CZxTIECAwBQQCFPClgABZwg+AwQIbAWcIWwt7BE4eQGBcPIfAQAEtgICYWthj8DJCwiEk/8IACCwFRAIWwt7BE5eQCCc/EcAAIGtgEDYWtgjcPICAuHkPwIACGwFBMLWwh6BkxcQCCf/EQBAYCsgELYW9gicvIBAOPmPAAACW4HL7e5+9m5ubvZTSBUCxQLX19dH2Z0zhKMci4Mi8DUCez9DmG0cawLO47Ml8BUCx34GvVogfAW29yTwXQT+9n8uPDs7+5JWBMKXsHvTUxf4WyCMx5ehsNxf004grKmrNoEPBJ6fnz94ZPMWBCMEdoNg9/aHRf7xAYHwj3BeRiAReHx8/O3L54If2/Pz89dAWO7vnjn8tkhwp0AI8LyUwL8K3N/fv3vpbhhcXFy8hsLYjssMiHcv3OMdAmGPmEoR+KzA3d3du6eOQJhnA2PxX15evl7HWcHYH5dx/7jM8Hi9scf/CIQ9YipF4LMCt7e37546A2GcEYwAuLq62ry8vLw+bz727kV7vkMg7BlUOQKfEfhTIMwwmH/wOM4KRkiMMwV/hvAZXc8h8M0EdgNhngHMrwozDEYQzDOGsR2PrxkKzhC+2QfJ4XYIPDw8vGtkhMJY9MswmF8bxleHEQTzslYoCIQpbEvggAK/+7XjCIT5ZwYjGJ6enl7DYRkGy1BY43AFwhqqahL4i8A8C1g+bQTCuIyvBTMERgDMEJjb5Wv2vS8Q9i2qHoFPCMwzgfnUGQYzAH63nc9dc+ufP6+pqzaBTwrs/vTfvf3JMvHTBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR4BgdAzS50QiAUEQkyoAIEeAYHQM0udEIgFBEJMqACBHgGB0DNLnRCIBQRCTKgAgR6By7Vaubm5Wau0ugQIrCTgDGElWGUJfEeBvZ8hXF9fvzn8/PlzM67Pz8+bx8fHzf39/ebu7m5ze3v7dn14eHh9bDzn5eXl7bV2CBA4vIAzhMObe0cCRysgEI52NA6MwOEFBMLhzb0jgaMV+NJAODs7+w/M7u3/POgGgWKB3c/+7u1Dtb73P1T804GPJv90Ha/9Kog/HbfHCBxC4E9r41Dr4mCBMBtaNn1+fr65uLh4++3C+I2EC4FTFRhrY6yHcR1rY7lWhslcQ2v6HCQQZiNjO0Pg8vJyM67j143jMu4XCGuOWu1jFxjrY4TBXBtjuwyHcfxzLa3Vy6qBMA5+LvIZBmPhj0avrq7ewmA0Pf4OwnjufP5aDatL4BgFxvqYa2Ssjx8/fryukbE/1sy4jsfnZbk/79vHdtVAGAe4bHSm324YPD09CYN9TFONby0w18r8gbkMheWZwlphMPBWD4TxJrPReXYw/0biaHKGg7ODIeVyygJznSx/cI71Mc8S5uNrGh0kEEYDo5nR6PxKMMJh3B7h4OvCmiNW+7sIzAU/vyKMIJjXsVbG42tfVg+E2cRoclxGgzMcxv4Mg/HYDIux70Lg1ATmWhnb+QNzuR3747H5vDV8Vg+EedCzyXF77I/FvzxjEAZTyvaUBeZin+tlbJf7a9uc/VqIB/nl/3yb5Xa5v3aj6hP4LgLLUFjuj+Oft9fq5aBnCMsmRmMzEJb32ydA4P8Cy8W/3F/T52BnCB81IRQ+knH/KQscKgB2jQ92hrD7xvP2VzU+39+WAIGtwJf+a8ftYdgjQOAYBATCMUzBMRA4EgGBcCSDcBgEjkFAIBzDFBwDgSMREAhHMgiHQeAYBATCMUzBMRA4EoH/AYzlNlHEbJmjAAAAAElFTkSuQmCC)

```text
box-shadow: 10px 10px 5px rgba(100, 100, 100, .5);
```

## [#](https://houdunren.gitee.io/note/css/6 背景处理.html#颜色渐变)颜色渐变

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#线性渐变)线性渐变

激变一般用在背景颜色中使用

```text
background: linear-gradient(red, green);
```

渐变角度

```text
background: linear-gradient(30deg, red, green);
```

向右渐变

```text
background: linear-gradient(to right, red, green)
```

向左渐变

```text
background: linear-gradient(to left, red, green);
```

左上渐变

```text
background: linear-gradient(to top left, red, green);
```

右下渐变

```text
background: linear-gradient(to right bottom, red, green);
```

设置多个颜色

```text
background: linear-gradient(red, rgb(0, 0, 200), green, rgba(122, 211, 100, 0));
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#径向渐变)径向渐变

设置渐变

```text
background: radial-gradient(red, blue, green);
```

设置渐变宽度与高度

```css
background: radial-gradient(100px 200px, red, blue, green);
```

左下渐变

```css
background: radial-gradient(at bottom left, red, blue);
```

右下渐变

```css
background: radial-gradient(at bottom right, red, blue);
```

左侧向中心渐变

```css
background: radial-gradient(at center left, red, blue);
```

底部向中心渐变

```css
background: radial-gradient(at 50% 100%, red, blue);
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#标识位)标识位

颜色未指定标识时，颜色会平均分布。

红色与蓝色在50%gc 60%间发生激变.

![image-20190818201418874](https://houdunren.gitee.io/note/assets/img/image-20190818201418874.876f48d4.png)

```css
background: linear-gradient(45deg, red 50%, blue 0%);
```

标识位相同时将没有过渡效果

![image-20190818203701681](https://houdunren.gitee.io/note/assets/img/image-20190818203701681.104054ec.png)

```css
background: linear-gradient(45deg, red 0,red 50%, blue 50%);
```

径向标识位绘制小太阳

![image-20190818235947336](https://houdunren.gitee.io/note/assets/img/image-20190818235947336.94846de5.png)

```css
width: 150px;
height: 150px;
background: radial-gradient(red 0, yellow 30%, black 60%, black 100%);
```

通过在两个颜色间中间点定义过渡位置

```css
background: linear-gradient(45deg, red, 50%, blue);
```

\###渐变重复

下例定义从0到25为蓝色,25px到50px的红色，并进行重复后产生渐变的进度条。

![image-20190818203349935](https://houdunren.gitee.io/note/assets/img/image-20190818203349935.08146f12.png)

```css
background: repeating-linear-gradient(90deg, blue, 25px, yellow 25px, 25px, red 50px);
```

### [#](https://houdunren.gitee.io/note/css/6 背景处理.html#径向重复)径向重复

![image-20190818235802316](https://houdunren.gitee.io/note/assets/img/image-20190818235802316.e6ae0312.png)

```css
width: 200px;
height: 200px;
backgrou
```

# 数据样式

## 表格

## 表格

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

表格可以非常快速的部署数据，灵活控制表格样式是必要的。表格不能设置外边距。

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#定制表格)定制表格

除了使用 `table` 标签绘制表格外，也可以使用样式绘制。

| 样式规则           | 说明         |
| ------------------ | ------------ |
| table              | 对应 table   |
| table-caption      | 对应 caption |
| table-row          | 对表 tr      |
| table-row-group    | 对应 tbody   |
| table-header-group | 对应 thead   |
| table-footer-group | 对应 tfoot   |

![image-20190819143313891](https://houdunren.gitee.io/note/assets/img/image-20190819143313891.eb8094c1.png)

```text
<style>
	.table {
    display: table;
    border: solid 1px #ddd;
  }

  .table nav {
    display: table-caption;
    text-align: center;
    background: black;
    color: white;
    padding: 10px;
  }

  .table section:nth-of-type(1) {
    font-weight: bold;
    display: table-header-group;
    background: #555;
    color: white;
  }

  .table section:nth-of-type(2) {
    display: table-row-group;
  }

  .table section:nth-of-type(3) {
    display: table-footer-group;
    background: #f3f3f3;
  }

  .table section ul {
    display: table-row;
  }

  .table section ul li {
    padding: 10px;
    display: table-cell;
    border: solid 1px #ddd;
  }
</style>

<article class="table">
        <nav>后盾人在线教程</nav>
        <section>
            <ul>
                <li>标题</li>
                <li>说明</li>
            </ul>
        </section>
        <section>
            <ul>
                <li>后盾人</li>
                <li>houdunren.com</li>
            </ul>
            <ul>
                <li>开源系统</li>
                <li>hdcms.com</li>
            </ul>
        </section>
        <section>
            <ul>
                <li>不断更新视频</li>
                <li>努力加油</li>
            </ul>
        </section>
</article>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#表格标题)表格标题

通过 `caption-side` 可以设置标题位置，值可以设置为 `top | bootom`。

![image-20190819133516640](https://houdunren.gitee.io/note/assets/img/image-20190819133516640.a7ca8fa9.png)

```text
<style>
  table caption {
    background: black;
    color: white;
    padding: 10px;
    caption-side: top;
  }
</style>

<table border="1">
        <caption>后盾人线上视频课程</caption>
        <tr>
            <td>houdunren.com</td>
            <td>后盾人</td>
        </tr>
</table>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#内容对齐)内容对齐

水平对齐使用 `text-align` 文本对齐规则

```text
<style>
	table tr td {
    height: 100px;
    text-align: center;
  }
</style>
```

垂直对齐使用 `vertical-align` 处理

| 属性   | 说明     |
| ------ | -------- |
| top    | 顶对齐   |
| middle | 垂直居中 |
| bottom | 底部对齐 |

```text
<style>
	table tr td {
    height: 100px;
    vertical-align: bottom;
    text-align: center;
  }
</style>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#颜色设置)颜色设置

为表格设置颜色与普通标签相似，可以为 `table | thead | tbody | caption | tfoot| tr| td` 设置颜色样式。

![image-20190819145908071](https://houdunren.gitee.io/note/assets/img/image-20190819145908071.d26a4066.png)

```text
<style>
	table tr {
    color: white;
  }
  table tr:nth-child(odd) {
    background: red;
  }
  table tr td:nth-child(even) {
    background: #067db4;
  }
</style>
```

使用选择器设置表格隔行变色

![image-20190820130542137](https://houdunren.gitee.io/note/assets/img/image-20190820130542137.16023728.png)

```text
<style>
        table thead tr {
            background: #118d68;
            color: #fff;
        }

        table tbody tr:nth-child(odd) {
            background: #1bb385;
            color: white;
        }
</style>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#边框间距)边框间距

设置单元格间距，设置间距上下10px ，左右 50px。

```text
table {
    border-spacing: 50px 10px;
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#边框合并)边框合并

默认表格边框间是有间距的，以下示例将边框合并形成细线表格。

![image-20190819141518119](data:image/png;base64,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)

```text
table {
  border-collapse: collapse;
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#隐藏单元格)隐藏单元格

![image-20190819142210720](https://houdunren.gitee.io/note/assets/img/image-20190819142210720.eb9c32b2.png)

```text
<style>
  table {
      empty-cells: hide;
  }
</style>
...

<table border="1">
        <tr>
            <td>在线教程</td>
            <td>houdunren.com</td>
        </tr>
        <tr>
            <td></td>
            <td>hdcms.com</td>
        </tr>
</table>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#无边框表格)无边框表格

![image-20190820130113657](https://houdunren.gitee.io/note/assets/img/image-20190820130113657.fe67c238.png)

```text
<style>
        table {
            border: none;
            border-collapse: collapse;
        }

        table td {
            border: none;
            border-right: solid 1px #ddd;
            border-bottom: solid 1px #ddd;
        }

        table tr:first-child td {
            border-top: solid 1px #ddd;
        }

        table td:last-child {
            border-right: none;
        }
</style>
...
<table border="1">
        <thead>
            <tr>
                <td>编号</td>
                <td>标题</td>
                <td>网址</td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>在线社区</td>
                <td>houdunren.com</td>
            </tr>
            <tr>
                <td>2</td>
                <td>开源系统</td>
                <td>hdcms.com</td>
            </tr>
        </tbody>
</table>
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#数据表格)数据表格

可以为表格元素使用伪类控制样式，下例中使用 `hover` 伪类样式

![image-20190820152827000](https://houdunren.gitee.io/note/assets/img/image-20190820152827000.3ce6ee55.png)

```text
<style>
        table,
        td {
            border: none;
            font-size: 14px;
            border-collapse: collapse;
        }

        table tr:hover {
            background: #ddd;
            cursor: pointer;
        }

        table td {
            border-top: solid 1px #ccc;
            padding: 10px;
        }
</style>
    
<table border="1">
        <thead>
            <tr>
                <td>编号</td>
                <td>标题</td>
                <td>网址</td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>在线社区</td>
                <td>houdunren.com</td>
            </tr>
            <tr>
                <td>2</td>
                <td>开源系统</td>
                <td>hdcms.com</td>
            </tr>
            <tr>
                <td>3</td>
                <td>开发实战</td>
                <td>houdunwang.com</td>
            </tr>
</table>
```

## [#](https://houdunren.gitee.io/note/css/7 数据样式.html#列表)列表

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#列表符号)列表符号

使用 `list-style-type` 来设置列表样式，规则是继承的，所以在`ul` 标签上设置即可。

| 值                   | 描述                                                        |
| :------------------- | :---------------------------------------------------------- |
| none                 | 无标记。                                                    |
| disc                 | 默认。标记是实心圆。                                        |
| circle               | 标记是空心圆。                                              |
| square               | 标记是实心方块。                                            |
| decimal              | 标记是数字。                                                |
| decimal-leading-zero | 0开头的数字标记。(01, 02, 03, 等。)                         |
| lower-roman          | 小写罗马数字(i, ii, iii, iv, v, 等。)                       |
| upper-roman          | 大写罗马数字(I, II, III, IV, V, 等。)                       |
| lower-alpha          | 小写英文字母The marker is lower-alpha (a, b, c, d, e, 等。) |
| upper-alpha          | 大写英文字母The marker is upper-alpha (A, B, C, D, E, 等。) |
| lower-greek          | 小写希腊字母(alpha, beta, gamma, 等。)                      |
| lower-latin          | 小写拉丁字母(a, b, c, d, e, 等。)                           |
| upper-latin          | 大写拉丁字母(A, B, C, D, E, 等。)                           |
| hebrew               | 传统的希伯来编号方式                                        |
| armenian             | 传统的亚美尼亚编号方式                                      |
| georgian             | 传统的乔治亚编号方式(an, ban, gan, 等。)                    |
| cjk-ideographic      | 简单的表意数字                                              |
| hiragana             | 标记是：a, i, u, e, o, ka, ki, 等。（日文片假名）           |
| katakana             | 标记是：A, I, U, E, O, KA, KI, 等。（日文片假名）           |
| hiragana-iroha       | 标记是：i, ro, ha, ni, ho, he, to, 等。（日文片假名）       |
| katakana-iroha       | 标记是：I, RO, HA, NI, HO, HE, TO, 等。（日文片假名）       |

隐藏列表符号

```text
ul {
  list-style-type: none;
}
```

自定义列表样式

```text
ul li {
  /* list-style-image: url(xj-small.png);
  list-style-image: radial-gradient(10px 10px, red, black); */
  
  list-style-image: linear-gradient(45deg, red, black);
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#符号位置)符号位置

控制符号显示在内容外面还是内部

| 选项    | 说明 |
| ------- | ---- |
| inside  | 内部 |
| outside | 外部 |

```text
ul {
  list-style-position: inside;
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#组合定义)组合定义

可以一次定义列表样式

```text
ul {
    list-style: circle inside;
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#背景符号)背景符号

![image-20190819164427052](https://houdunren.gitee.io/note/assets/img/image-20190819164427052.dd5e42c1.png)

```text
ul li {
  background: url(xj-small.png) no-repeat 0 6px;
  background-size: 10px 10px;
  list-style-position: inside;
  list-style: none;
  text-indent: 15px;
}
```

多图背景定义

![image-20190820155342265](https://houdunren.gitee.io/note/assets/img/image-20190820155342265.cdf87900.png)

```text
<style>
        ul {
            list-style-type: none;
        }

        ul li {
            background-image: url(xj-small.png), url(houdunren.jpg);
            background-repeat: no-repeat, repeat;
            background-size: 10px 10px, 100%;
            background-position: 5px 7px, 0 0;
            text-indent: 20px;
            border-bottom: solid 1px #ddd;
            margin-bottom: 10px;
            padding-bottom: 5px;

        }
</style>
```

## [#](https://houdunren.gitee.io/note/css/7 数据样式.html#追加内容)追加内容

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#基本使用)基本使用

使用伪类 `::before` 向前添加内容，使用 `::after` 向后面添加内容。

```text
a::after {
  content: " (坚持努力) ";
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#提取属性)提取属性

使用属性值添加内容，可以使用标准属性与自定义属性。

```text
<style>
  a::after {
    content: attr(href);
  }
</style>

<a href="houdunren.com">后盾人</a>
```

通过属性值添加标签提示

![image-20190819170234330](data:image/png;base64,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)

```text
a {
    position: relative;
}

a:hover {
    &::before {
        content: "URL: "attr(data-url);
        background: #555;
        color: white;
        position: absolute;
        top: 20px;
        padding: 3px 10px;
        border-radius: 10px;
    }
}
```

### [#](https://houdunren.gitee.io/note/css/7 数据样式.html#自定义表单)自定义表单

![image-20190820165451079](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAW0AAABhCAYAAAAdtPDtAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDCIMAgzmCYmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgsQaVW2xc+dm6301/ycx+oP4mpHgVwpaQWJwPpP0CcllxQVMLAwJgCZCuXlxSA2B1AtkgR0FFA9hwQOx3C3gBiJ0HYR8BqQoKcgewbQLZAckYi0AzGF0C2ThKSeDoSG2ovCPC4uPr4KIQamRiaexBwLumgJLWiBEQ75xdUFmWmZ5QoOAJDKVXBMy9ZT0fByMDQkoEBFOYQ1Z9vgMOSUYwDIVYgxsBg6cLAwLwYIZYkxcCwHeh+SU6EmMpyBgb+CAaGbQ0FiUWJcAcwfmMpTjM2grC5tzMwsE77//9zOAMDuyYDw9/r////3v7//99lQPNvMTAc+AYAMHldbXTDSqwAACVySURBVHgB7Z0FoCTFEYb7nXBocCdwuHsgSHAIFiy4BC64BgsW7HCXBJdAkAQNTnA4XENwd3fXs0l/9bbmenpndmf33Xu3e6+KvOtpq+n5p6e6uqp605F4ckaGgCFgCBgCbYFAn7YYpQ3SEDAEDAFDQBAwoW0TwRAwBAyBNkLAhHYbvSwbqiFgCBgCJrRtDhgChoAh0EYImNBuo5dlQzUEDAFDwIS2zQFDwBAwBNoIARPabfSybKiGgCFgCJjQtjlgCBgChkAbIWBCu41elg3VEDAEDAET2jYHDAFDwBBoIwRMaLfRy7KhGgKGgCFgQtvmgCFgCBgCbYRAjwrtH374oS40X375pbvxxhvd66+/XrctDV599VV3//33u59++qlm+//+97/uvvvuc43+PhZ8n3jiiZq8u1L5ySefuCFDhrgPP/ywK2x6Rd9nn33WXXLJJe6VV15p6nl5l7feemvh3Prf//7n7rnnnrpzKbw5Y+H9DR8+PCy2a0Og2xDo122cI8Y33XSTO/vss91+++3nlllmmbT2559/Tq+5ePvtt90555zjNt54YzfDDDNk6vr27ev69csO+T//+Y+744473JlnnulmnHHGTHvN3Hbbbe60006T7AsvvOB23HFHraqb7rTTTu7TTz916667rtt2223rtm+0waOPPirPu8MOO7i11lqrdHcWqq4sJiuuuKJbcMEFS9+vFRo+88wz7oorrnBvvvmmO+SQQxoe0nPPPedOP/10t/LKK7s99tijqv/f/vY3edeXX355VV1RwbXXXitKw9xzz+2mnnpqaTZy5MhSi/BEE03kfvGLX6SsUUD4Topo++23dxdccEFRdVq+wQYbuGmnnTbN28XYhUBWAnbjs0088cTC/bjjjnNffPGFW2edddxjjz3mDj/88Ny78nHyF9JCCy3kjjzyyLDIvfzyyw5h/stf/jJTrpmHHnpIBPYEE0zgJpxwQvkoJp10UlkUtE2t9OCDD3Z//vOf3XXXXeemmmoqt/baa9dqPlrq0L4ZY//+/Qv5IbDvuuuuwvp6FTPNNFOh0P78889F6Mwyyyxu/PHHr2KFVvniiy+6559/3iF4FllkkbpCgoXvqaeecjzbPPPMI38DBgzI8GYXBM8imnXWWaWKefP000/Le89r26dPH+Ef13F/aIklloirZE4yRoQd86QrxKKy++6712Wx9NJLuwMOOCBt9/7778s7ZT6HNGLECMluuOGGDgWkHq2wwgp130c9Hlbfugj0mNBGu55++ullkp533nnus88+c2ussYbbcsstM+hgJkBznm222dxSSy2VqUOIQAiNq6++Wq7feecdN84442QEPB/lwIEDHdvdo48+WupPOukk0Wp23nln2WKj4ay++urCo9Y/3BMtnX7nnnuuY+Eo0uhr8aGOcaNRM77tttsutzmmIXYa8QcdN95mm23cJptsEhdLHtPSscceKzwGDRqU22byySfPLccEcdBBBzkEBWks4BBIaKkqSJQJuLAAIzBjOvHEE8WEEJczxvnmmy8thuf++++f5mtdHHjggbWqZZGNd2VPPvmk9Fl44YWr+j7++ONStthii1XVNVowySSTlNo1zTnnnLms2QmGcxNcWaiYs5dddlnah+c54YQTHHOB3YNS3kKrdZa2PwI9JrSBCgHIFvRPf/qTQwNGYP/qV78SrU2hHHfcceUSbQftWAmtjLbQsGHD3KWXXqpVbujQoZk8Hw1bYcwxaC0IBzW1ILwxeZxxxhnugw8+cFtvvbXr6OhIeeVdsNggtBHebE8HDx6c16xuGfbSjz/+2L322muFbfn42GE8+OCDIngwy+QRH3C4tQ7bfP3115Ll4y27TUbLvOaaa8SfEPIKr1lQ9957bxHYiy++uFtuueXEnHDD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3uhTI6AxfYSExj7ffPOFRXJ9zz33uCeffNJtvPHGVXUU4GCsR6+99po0ue6669xpp51Wr3nd+p9//tk98cQT7tFHH3UTTzyxYxeQ5xD9+OOPxe6OE3baaad1Cy20kFtggQUy/OGBk3X11Vd3448/flqXJIm79tpr3WSTTeaWX375tJyLxx57TO7ft29ft9RSS+Xi1ghf7OE//fSTmFYwfT300EOywDFenk2JNjfffLObccYZxZRFu8cff9ytuuqqbpFFFpFmH374oTzzyy+/7AYOHOgWX3xxMZPl8VhwwQXlOfBNYNJhDswzzzzatGbK7on7Yz7DXDbXXHO5FVdc0fXpkw2mAkewoB0+GPgvueSSbpJJJkn541d5+OGH3aKLLirjGDJkiDi7eXYwgOfnn38uc513ybtea6213IABA1IedmEINISAn5g9Stdff33iB9j0nxdm6XhfeeUV4XPRRRelZeHFVlttlXjHY1jU8PUxxxyTjvWZZ55puD8dHnzwQeHhnabJMsssk/JTHC6//PIMX2/WSfzCVNVu++23T7wdP2270UYbSRvvKE3LuBg2bJiUe2GYlvudQrL11ltX8dx3333TMXnBJO0b4esFWeJ9DonftVTx3myzzdL78954Xi+kE/ros/soHmlz5ZVXpmVaR+oXyioejM8vVFXtzzrrrLRt0YV3dCfeV1LVF6y8AE67+V1a4v0gVe14Vi+Y03bXXHONtDnkkEMEh3Ds3oeReKWh6l3y/OF7TJnZhSFQAgFXos1obaIf5x133JH4SI+G/nwER2YsodD22o4IaIS0/ukHpHlN+RjLUihkjz322LLdMu1UaDMeBIYPHUxuu+225A9/+IN88AhofTY+ch33KaecknitPPHRNqmg2X///VPejQjXo48+WvgidFgkvIaawF/vRdqs0FYee+yxR3LnnXcmgwcPTgXVTTfdJONVoU1bnnevvfZKbrnlluStt95KEKRafuGFF0qeMTJWyu+9994qHrxL3gc4shjqGD766KMUn/gCQak8t9lmm8T7VRLmIwsJ/f2uJO2y3nrrpWXMVfA66KCD0vv4XYG0VaFN/1VWWSXxjvHk9NNPT5+fchYY3uH555+feAe78KCNkSHQDAI9LrQRWExkHzPdzHgzfUKh7U0hwhdt0tu3C//4aBCcZQiByVjRGP2WVhYDv80v0zXT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)

```text
<style>
        body {
            padding: 80px;
        }

        .field {
            position: relative;
        }

        input {
            border: none;
            outline: none;
        }

        .field::after {
            content: '';
            background: linear-gradient(to right, white, red, green, blue, white);
            height: 30px;
            position: relative;
            width: 100%;
            height: 1px;
            display: block;
            left: 0px;
            right: 0px;
        }

        .field:hover::before {
            content: attr(data-placeholder);
            position: absolute;
            top: -20px;
            left: 0px;
            color: #555;
            font-size: 12px;
        }
</style>

...
<div class="field" data-placeholder="请输入少于100字的标题">
        <input type="text" id="name">
    </div>
```

#  浮动布局

## 浮动布局

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 CSS 中，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。

![image-20190820202101608](https://houdunren.gitee.io/note/assets/img/image-20190820202101608.da68a2a0.png)

在网站开发中需要一行排列多个元素，使用浮动可以方便实现。下面是使用浮动排列多个元素

![image-20190820202250078](https://houdunren.gitee.io/note/assets/img/image-20190820202250078.fc6d8674.png)

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#float)FLOAT

使用浮动可以控制相邻元素间的排列关系。

| 选项  | 说明     |
| ----- | -------- |
| left  | 向左浮动 |
| right | 向右浮动 |
| none  | 不浮动   |

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#文档流)文档流

没有设置浮动的块元素是独占一行的。

![image-20190820202706957](data:image/png;base64,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)

浮动是对后面元素的影响，下图中第二个元素设置浮动对第一个元素没有影响

![image-20190820202706957](data:image/png;base64,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)

```text
div:first-of-type {
    border: solid 2px red;
}

div:last-of-type {
 		float: left;
    background: green;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#丢失空间)丢失空间

如果只给第一个元素设置浮动，第二个元素不设置，后面的元素会占用第一个元素空间。

![image-20190820202823601](data:image/png;base64,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)

```text
div:first-of-type {
    float: left;
    border: solid 2px red;
}

div:last-of-type {
    background: green;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#使用浮动)使用浮动

两个元素都设置浮动后，会并排显示

![image-20190820202913929](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAWkAAAC9CAYAAABxo4zDAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDCIMhgwsCSmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsis122+YvYPLIzOz48X+lJhGIepHgVwpaQWJwPpP0CcnlxQVMLAwJgCZCuXlxSA2B1AtkgR0FFA9hwQOx3C3gBiJ0HYR8BqQoKcgewbQLZAckYi0AzGF0C2ThKSeDoSG2ovCPD6uCuE+oQEOYZ7urgScC/JoCS1ogREO+cXVBZlpmeUKDgCQylVwTMvWU9HwcjA0JKBARTmENWfb4DDklGMAyFWIMbAYDEDKPgQIRYP9MN2OQYG/j6EmBrQvwJeDAwH9xUkFiXCHcD4jaU4zdgIwubezsDAOu3//8/hDAzsmgwMf6////97+///f5cxMDDfYmA48A0A7i9gVM3FyEcAAAd7SURBVHgB7dkxahthGEVRO3EdcOUNZjfZZyBViixANinNFIb3X5jiqLPw9xiOzEUkz4+P15MXAQIECNxS4Nstn8pDESBAgMB/AZH2h0CAAIEbC4j0jT8cj0aAAAGR9jdAgACBGwuI9I0/HI9GgACBlyuCx+vb1dveI3B7gR8/v9/+GT0ggSuBf79+X7395Jv0JYs3CRAgcA8Bkb7H5+ApCBAgcCkg0pcs3iRAgMA9BC7/Tfrzoz3//fP5LT8TuIWA/z+5xcfgIUIB36RDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVBApENc0wQIEFgFRHoVdE+AAIFQQKRDXNMECBBYBUR6FXRPgACBUECkQ1zTBAgQWAVEehV0T4AAgVDg5Svbj9e3r/ya3yFAgACBwwK+SR8GNUeAAIGTAiJ9UtMWAQIEDguI9GFQcwQIEDgp8Pz4eJ0ctEWAAAEC5wR8kz5naYkAAQLHBUT6OKlBAgQInBMQ6XOWlggQIHBcQKSPkxokQIDAOQGRPmdpiQABAscFRPo4qUECBAicExDpc5aWCBAgcFzgHRDEEZ7LfH0gAAAAAElFTkSuQmCC)

```text
div:first-of-type {
    float: left;
    border: solid 2px red;
}

div:last-of-type {
    float: left;
    background: green;
}
```

为第二个元素设置右浮动时将移动到右边

![image-20190820203052185](data:image/png;base64,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)

```text
div:first-of-type {
    float: left;
    border: solid 2px red;
}

div:last-of-type {
    float: right;
    background: green;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#浮动边界)浮动边界

浮动元素边界不能超过父元素的padding

![image-20190820203619915](data:image/png;base64,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)

```text
main {
    width: 400px;
    border: solid 2px black;
    overflow: auto;
    padding: 50px;
    background-color: antiquewhite;
    background-clip: content-box;
}

div {
    width: 100px;
    height: 100px;
    box-sizing: border-box;
}

div:first-of-type {
    float: left;
    border: solid 2px red;
}

div:last-of-type {
    float: right;
    background: green;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#浮动转块)浮动转块

元素浮动后会变为块元素包括行元素如 `span`，所以浮动后的元素可以设置宽高

```text
a {
    float: left;
    width: 300px;
}
```

## [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#清除浮动)清除浮动

不希望元素受浮动元素影响时，可以清除浮动。

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#clear)CLEAR

CSS提供了 `clear` 规则用于清除元素浮动影响。

| 选项  | 说明               |
| ----- | ------------------ |
| left  | 左边远离浮动元素   |
| right | 右连远离浮动元素   |
| both  | 左右都远离浮动元素 |

使用清除浮动

![image-20190820210600975](data:image/png;base64,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)

```text
<style>
	div {
    width: 200px;
    height: 200px;
    margin-bottom: 10px;
  }

  div.green {
      border: solid 2px green;
      float: left;
  }

  div.red {
      border: solid 2px red;
      float: right;
  }

  div.blue {
      background: blue;
      clear: both;
  }
</style>
...

<div class="green"></div>
<div class="red"></div>
<div class="blue"></div>
```

在父元素内部最后面添加一个没有高度的了元素，并使用`clear:both` 。

```text
<style>
	.clearfix {
      clear: both;
      height: 0;
  }

  div {
      width: 200px;
      height: 200px;
      margin-bottom: 10px;
  }


  div.green {
      border: solid 2px green;
      float: left;
  }

  div.red {
      border: solid 2px red;
      height: 200px;
      float: left;
  }

  div.blue {
      background: blue;
  }
</style>

<article>
        <div class="green"></div>
        <div class="red"></div>
        <div class="clear"></div>
    </article>
    <div class="blue"></div>
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#after)AFTER

使用 `::after` 伪类为父元素添加后标签，实现清除浮动影响。

```text
.clearfix::after {
    content: "";
    display: block;
    clear: both;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#overflow)OVERFLOW

子元素使用浮动后将不占用空间，这时父元素高度为将为零。通过添加父元素并设置 `overflow` 属性可以清除浮动。

将会使用父元素产生 `BFC` 机制，即父元素的高度计算会包括浮动元素的高度。

```text
<style>
  article {
      overflow: hidden;
  }
...
```

## [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#页面布局)页面布局

![image-20190820213928554](https://houdunren.gitee.io/note/assets/img/image-20190820213928554.46a77552.png)

完成页面布局注意以下几点

1. 首先根据设计稿确定页面大小（主要指宽度，移动端不需要考虑），如 1200px 宽度
2. 水平分割页面主要区域
3. 每个区域中按以上两步继续细分

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#父容器)父容器

一组浮动元素要放在一个父容器中，如下图绿线指父容器，里面的红线为浮动子元素。

![image-20190820204502017](https://houdunren.gitee.io/note/assets/img/image-20190820204502017.b380cffa.png)

下面是上图的布局结构代码

```text
<style>
	article {
      background: #f3f3f3;
      width: 1020px;
      height: auto;
      overflow: auto;
      padding: 20px;
  }

  article.hot section {
      background: #fff;
      box-shadow: 0 0 5px #777;
      height: 300px;
      width: 500px;
  }

  article.hot section:first-of-type {
      float: left;
  }

  article.hot section:last-of-type {
      float: right;
  }

  article.swiper section {
      height: 200px;
      background: #fff;
      box-shadow: 0 0 5px #777;
  }

  article.swiper section:first-of-type {
      width: 200px;
      float: left;
  }

  article.swiper section:last-of-type {
      width: 820px;
      float: left;
  }
</style>
...

 <article class="hot">
        <section></section>
        <section></section>
</article>
<article class="swiper">
        <section></section>
        <section></section>
</article>
```

## [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#形状浮动)形状浮动

通过形状浮动可以让内容围绕图片，类似于我们在word 中的环绕排版。要求图片是有透明度的PNG格式。

![image-20190822131434976](https://houdunren.gitee.io/note/assets/img/image-20190822131434976.2ad35431.png)

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#距离控制)距离控制

| 选项        | 说明       |
| ----------- | ---------- |
| margin-box  | 外边距环绕 |
| padding-box | 内边距环绕 |
| border-box  | 边线环绕   |
| content-box | 内容环绕   |

**外边距环绕**

![image-20190822133517672](https://houdunren.gitee.io/note/assets/img/image-20190822133517672.7e51545d.png)

```text
<style>
  span.shape {
      float: left;
      width: 100px;
      height: 100px;
      padding: 30px;
      margin: 30px;
      border: solid 30px green;
      shape-outside: margin-box;
  }
</style>
...


<p>
  <span class="shape"></span>
  后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。
  除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</p>
```

**边框环绕**

![image-20190822133612903](https://houdunren.gitee.io/note/assets/img/image-20190822133612903.e9fc34f6.png)

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    padding: 30px;
    margin: 30px;
    border: solid 30px green;
    shape-outside: border-box;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#显示区域)显示区域

| 选项    | 说明   |
| ------- | ------ |
| circle  | 圆形   |
| ellipse | 椭圆   |
| polygon | 多边形 |

**圆形**

![image-20190822134841106](https://houdunren.gitee.io/note/assets/img/image-20190822134841106.8d7a1948.png)

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    padding: 30px;
    margin: 30px;
    background: red;
    clip-path: circle(50% at center);
}
```

**椭圆**

![image-20190822135121997](https://houdunren.gitee.io/note/assets/img/image-20190822135121997.ac6b0d9d.png)

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    padding: 30px;
    margin: 30px;
    background: red;
    clip-path: ellipse(50% 80% at 100% 0);
}
```

**多边形**

![image-20190822135238497](https://houdunren.gitee.io/note/assets/img/image-20190822135238497.4227ee56.png)

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    padding: 30px;
    margin: 30px;
    background: red;
    clip-path: polygon(50% 0, 100% 100%, 0 100%)
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#内移距离)内移距离

使用 `inset` 属性控制环绕向内移动的距离。

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    padding: 30px;
    margin: 30px;
    background: red;
    shape-outside: inset(50px 30px 80px 50px) padding-box;
}
```

### [#](https://houdunren.gitee.io/note/css/8 浮动布局.html#环绕模式)环绕模式

| 选项    | 说明     |
| ------- | -------- |
| circle  | 圆形环绕 |
| ellipse | 椭圆环绕 |
| url     | 图片环绕 |
| polygan | 多边环绕 |

**圆形环绕**

![image-20190822131434976](https://houdunren.gitee.io/note/assets/img/image-20190822131434976.2ad35431.png)

```text
img {
    padding: 20px;
    float: left;
    shape-outside: circle(50%) padding-box;
}
```

**椭圆环绕**

![image-20190822131415117](https://houdunren.gitee.io/note/assets/img/image-20190822131415117.fa6114d5.png)

```text
img {
    padding: 20px;
    float: left;
    shape-outside: ellipse(80px 70px) padding-box;
}
```

**图片环绕**

![image-20190822131725161](https://houdunren.gitee.io/note/assets/img/image-20190822131725161.96aba0e9.png)

```text
img {
    float: left;
    shape-outside: url(xj.png);
}
```

**多边环绕**

![image-20190822132344769](https://houdunren.gitee.io/note/assets/img/image-20190822132344769.220f7596.png)

```text
span.shape {
    float: left;
    width: 100px;
    height: 100px;
    background: red;
    clip-path: polygon(50px 0px, 0 100px, 100px 100px);
    shape-outside: polygon(50px 0px, 0 100px, 100px 100px);
}
```

# 定位布局

## 绝对定位和相对定位理解

<div ——————————— position:relative; 不是最近的祖先定位元素，不是参照物<div—————————-没有设置为定位元素，不是参照物<div———————- position:relative 参照物<div box1<div box2 ——–position:absolute; top:50px; left:120px;<div box3效果图：

![img](https://pic002.cnblogs.com/images/2012/422101/2012072618164674.jpg)

为改变参照物（橘色框）后的效果
层级关系为：
<div ——————————— position:relative;最近的祖先定位元素，参照物
<div—————————-没有设置为定位元素，不是参照物
<div———————-没有设置为定位元素，不是参照物
<div box1
<div box2 ——–position:absolute; top:50px; left:120px;
<div box3
效果图：

![img](https://pic002.cnblogs.com/images/2012/422101/2012072618180663.jpg)

**参照物为最顶级的元素情况**。
层级关系为：
<div ———————————没有设置为定位元素，不是参照物
<div—————————-没有设置为定位元素，不是参照物
<div———————-没有设置为定位元素，不是参照物
<div box1
<div box2 ——–position:absolute; top:50px; left:120px;
<div box3
效果图：

![img](https://pic002.cnblogs.com/images/2012/422101/2012072618185065.jpg)

 

**仅使用margin属性布局绝对定位元素的情况**
此情况，margin-bottom 和margin-right的值不再对文档流中的元素产生影响，因为该元素已经脱离了文档流。另外，不管它的祖先元素有没有定位，都是以文档流中原来所在的位置上偏移参照物。 
图9中，使用margin属性布局相对定位元素。
层级关系为：
<div ——————————— position:relative; 不是参照物
<div—————————-没有设置为定位元素，不是参照物
<div———————-没有设置为定位元素，不是参照物
<div box1
<div box2 ——–position:absolute; margin-top:50px; margin-left:120px;
<div box3
效果图：

![img](https://pic002.cnblogs.com/images/2012/422101/2012072618431998.jpg)

IE6的情况下，box2前面没有兄弟节点，则margin-left的值会出现双倍边距，见图10。
层级关系为：
<div ——————————— position:relative; 不是参照物
<div—————————-没有设置为定位元素，不是参照物
<div———————-没有设置为定位元素，不是参照物
<div box1
<div box2 ——–position:absolute; margin-top:50px; margin-left:60px;
<div box3
效果图：

![img](https://pic002.cnblogs.com/images/2012/422101/2012072618451464.jpg)

 

## 基础知识

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

定位的基本思想很简单，它允许你定义元素框相对于其正常位置应该出现的位置，或者相对于父元素、另一个元素甚至浏览器窗口本身的位置。

轮播图是典型的定位应用

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-6564594.a6376fc9.gif)

下面弹出的二维码也可以使用定位处理

![image-20190824004005166](https://houdunren.gitee.io/note/assets/img/image-20190824004005166.4cea0ef6.png)

下面是抖音软件截图，如果布局类似的页面页面中的图标可以使用定位处理

![Screenshot_20190824-002832](https://houdunren.gitee.io/note/assets/img/Screenshot_20190824-002832-6578191.f1438d3e.jpg)

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#定位类型)定位类型

| 选项     | 说明                 |
| -------- | -------------------- |
| static   | 默认形为，参考文档流 |
| relative | 相对定位             |
| absolute | 绝对定位             |
| fixed    | 固定定位             |
| sticky   | 粘性定位             |

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#位置偏移)位置偏移

可以为部分类型的定位元素设置`上、下、左、右` 的位置偏移。

| 选项   | 说明     |
| ------ | -------- |
| top    | 距离顶边 |
| bottom | 距离下边 |
| left   | 距离左部 |
| right  | 距离右边 |

![image-20190823115357066](data:image/png;base64,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)

```text
<style>
  body {
    padding: 50px;
  }

  article {
      width: 300px;
      height: 200px;
      border: solid 6px blueviolet;
      margin: 20px;
  }

  div {
      font-size: 25px;
      background: #f2a67d;
      padding: 10px;
      position: absolute;
      top: 0;
  }
</style>
...

<article>
	<div>houdunren.com</div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/9 定位布局.html#相对定位)相对定位

相对定位是相对于元素原来的位置控制，当元素发生位置偏移时，原位置留白。

![image-20190823124004671](https://houdunren.gitee.io/note/assets/img/image-20190823124004671.a7965d39.png)

```text
<style>
  body {
    padding: 50px;
  }
  article {
    width: 400px;
    height: 200px;
    border: solid 10px blueviolet;
    font-size: 14px;
    padding: 30px;
  }
  article img {
    width: 50px;
    position: relative;
    top: -20px;
  }

</style>
...

<article>
        <img src="xj.png" alt="">
        后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
</article>
```

## [#](https://houdunren.gitee.io/note/css/9 定位布局.html#绝对定位)绝对定位

绝对定义不受文档流影响，就像漂浮在页面中的精灵，绝对定位元素拥有行内块特性。

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#参照元素)参照元素

如果父级元素设置了 `relative | fixed | sticky` ，绝对定位子元素将参数此父元素进行定位。

![image-20190823115305218](data:image/png;base64,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)

```text
<style>
	body {
    padding: 50px;
  }

  article {
      width: 400px;
      height: 100px;
      border: solid 6px blueviolet;
      position: relative;
  }

  div {
      font-size: 25px;
      background: #f2a67d;
      padding: 10px;
      position: absolute;
      top: 0;
      left: 0px;
  }
</style>
...

<article>
	<div>houdunren.com</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#默认位置)默认位置

如果没有为定位元素设置偏移，将受父元素的padding等属性影响。但使用定位一般都会设置偏移位置。

![image-20190823120052751](data:image/png;base64,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)

```text
body {
    padding: 50px;
}

article {
    width: 400px;
    height: 100px;
    border: solid 6px blueviolet;
    position: relative;
    padding: 20px;
}

div {
    background: #f2a67d;
    padding: 5px;
    position: absolute;
    top: 50px;
    left: 50px;
}
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#设置尺寸)设置尺寸

可以通过定位的偏移值设置元素的尺寸。

![image-20190823115220514](data:image/png;base64,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)

```text
<style>
	body {
    padding: 50px;
  }
  article {
    width: 400px;
    height: 100px;
    border: solid 6px blueviolet;
    position: relative;
  }
  div {
    font-size: 25px;
    background: #f2a67d;
    padding: 10px;
    position: absolute;
    top: 50%;
    left: 50%;
    right: 0;
    bottom: 0;
  }
</style>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#居中定位)居中定位

通过将 `left` 设置为50% ,并向左偏移子元素宽度一半可以实现水平居中，垂直居中使用方式类似。

![image-20190823122408750](data:image/png;base64,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)

```text
<style>
  body {
    padding: 50px;
  }
  article {
    width: 400px;
    height: 400px;
    border: solid 6px blueviolet;
    position: relative;
  }
  div {
    width: 200px;
    height: 200px;
    background: #f2a67d;
    position: absolute;
    left: 50%;
    margin-left: -100px;
    top: 50%;
    margin-top: -100px;
  }

</style>

<article>
        <div></div>
    </article>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#滚动行为)滚动行为

固定定位元素会随滚动条发生滚动。

![Untitled](data:image/gif;base64,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)

```text
<style>
  body {
    padding: 50px;
  }
  main {
    width: 300px;
    height: 200px;
    border: solid 10px blueviolet;
    position: relative;
    overflow: scroll;
  }
  main article {
    height: 600px;
  }
  main article div {
    width: 200px;
    height: 200px;
    position: absolute;
  }
  main article div:nth-of-type(1) {
    background: red;
    left: 0px;
    z-index: 2;
  }
</style>
...

<main>
	<article>
		<div></div>
	</article>
</main>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#图标定位)图标定位

有了绝对定位我们可以很方便的控制元素在任何位置的摆放。

![image-20190823224657620](https://houdunren.gitee.io/note/assets/img/image-20190823224657620.495f7702.png)

```text
* {
  padding: 0;
  margin: 0;
}
main {
  height: 3000px;
  padding: 100px;
}
main div {
  width: 300px;
  border: solid 6px blueviolet;
  padding: 0;
  overflow: hidden;
  position: relative;
}
main div img {
  max-width: 300px;
  float: left;
}
main div span {
  display: inline-block;
  width: 30px;
  height: 30px;
  text-align: center;
  color: white;
  line-height: 2em;
  border-radius: 50%;
  background: blueviolet;
  position: absolute;
  top: 10px;
  left: 10px;
  box-shadow: 0 0 5px rgba(100, 100, 100, 0.8);
}

...

<main>
    <div>
        <span>热</span>
        <img src="houdunren.jpg" alt="">
    </div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/9 定位布局.html#纵向重叠)纵向重叠

如果元素重叠在一起，可以使用 `z-index` 控制元素的上下层级，数值越大越在上面。

父级子元素设置 `z-index` 没有意义，子元素永远在父元素上面的。

![image-20190823125921966](https://houdunren.gitee.io/note/assets/img/image-20190823125921966.c8372c6e.png)

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#层级改变)层级改变

![image-20190823190234595](data:image/png;base64,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)

```text
<style>
	body {
    padding: 50px;
  }

  article {
    width: 200px;
    height: 200px;
    border: solid 10px blueviolet;
    position: relative;
    cursor: pointer;
  }

  article:hover div:nth-of-type(2) {
    z-index: 2;
  }

  article div {
    width: 200px;
    height: 200px;
    position: absolute;
  }

  article div:nth-of-type(1) {
    background: red;
    left: 0px;
    z-index: 2;
  }

  article div:nth-of-type(2) {
    background: green;
    left: 50px;
    top: 50px;
  }
</style>
...

<article>
	<div></div>
	<div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#购物车)购物车

因为事件捕获特性（请在JS系统课程了解）所要以把父级的 `z-index` 放在最下面。

![Untitled](data:image/gif;base64,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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  main {
    width: 600px;
    padding: 100px;
    margin: 0 auto;
  }
  main article {
    width: 150px;
    position: relative;
    cursor: pointer;
    font-size: 14px;
    color: #555;
  }
  main article:hover div:nth-of-type(1) {
    border-bottom: none;
  }
  main article:hover div:nth-of-type(2) {
    display: block;
  }
  main article div {
    box-sizing: border-box;
    height: 50px;
    line-height: 3.5em;
    text-align: center;
    border: solid 2px blueviolet;
    background: white;
  }
  main article div:nth-of-type(1) {
    position: relative;
    z-index: 2;
  }
  main article div:nth-of-type(2) {
    display: none;
    position: absolute;
    right: 0;
    top: 48px;
    left: -150px;
    z-index: 1;
  }
</style>
...

<main>
    <article>
        <div>我的购物车</div>
        <div>购物车中暂无产品</div>
    </article>
</main>
```

## [#](https://houdunren.gitee.io/note/css/9 定位布局.html#固定定位)固定定位

元素相对于页面固定定位在某个位置，固定定位元素不会在滚动时改变位置 ，使用`position: fixed` 产生固定定位。

![image-20190823192657943](data:image/png;base64,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)

```text
<style>
  header {
    height: 60px;
    border-bottom: solid 5px #7f35c9;
    box-shadow: 0 5px 8px rgba(100, 100, 100, 0.6);
    position: fixed;
    top: 0px;
    left: 0px;
    right: 0px;
  }
  article {
    height: 3000px;
    margin-top: 80px;
    background: #f3f3f3;
    border: solid 5px #ddd;
  }
</style>
...

<header></header>
<article></article>
```

## [#](https://houdunren.gitee.io/note/css/9 定位布局.html#粘性定位)粘性定位

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#同级定位)同级定位

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-6569622.3d5e17b2.gif)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  main {
    padding: 30px;
    font-size: 14px;
  }
  main article {
    width: 400px;
    height: 100px;
    border: solid 5px blueviolet;
    overflow: scroll;
  }
  main article h2 {
    background: #db1f77;
    color: white;
    text-indent: 20px;
    position: sticky;
    top: 0;
  }
  main article h2:nth-of-type(1) {
    background: blueviolet;
  }
  main article section {
    height: 300px;
  }
</style>
...

<main>
    <article>
        <section></section>
        <h2>后盾人</h2>
        <section></section>
        <h2>HOUDUNREN</h2>
        <section></section>
    </article>
</main>
```

### [#](https://houdunren.gitee.io/note/css/9 定位布局.html#非同级定位)非同级定位

不属于同一个父元素设置粘性定位时，后面的元素挤掉原来位置的元素如下例。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-6568610.bd18d466.gif)

```html
<style>
  * {
    padding: 0;
    margin: 0;
  }
  main {
    padding: 30px;
    font-size: 14px;
  }
  main article {
    width: 400px;
    border: solid 5px blueviolet;
    height: 200px;
    overflow: scroll;
  }
  main article section:nth-of-type(odd) h2 {
    background: blueviolet;
  }
  main article section h2 {
    background: #db1f77;
    color: white;
    text-indent: 20px;
    position: sticky;
    top: 0;
  }
  main article section p {
    padding: 20px;
  }
</style>
...

<main>
    <article>
        <section>
            <h2>hdcms.com</h2>
            <p>
                后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
            </p>
        </section>
        <section>
            <h2>后盾人</h2>
            <p>
                后盾人隶属于北京后盾计算机技术培训有限责任公司，是专注于培养中国互联网精英PHP程序语言专业人才的专业型培训机构，拥有七年培训行业经验。后盾人拥有国内一线的讲师和技术团队，团队成员项目经验均在8年以上，团队曾多次为国内外上市集团、政府机关的大型项目提供技术支持，其中包括新浪、搜狐、腾讯、宝洁公司、联想、丰田、工商银行、中国一汽等众多大众所熟知的知名企业。
            </p>
        </section>
        <section>
            <h2>houdunwang.com</h2>
            <p>
                后盾人自2010年创立至今，免费发布了大量高质量视频教程，视频在优酷、土豆、酷六等视频网站均有收录，很多技术爱好者受益其中。除了免费视频外，后盾人还为大家提供了面授班、远程班、公益公开课、VIP系列课程等众多形式的学习途径。后盾人有一群认真执着的老师，他们一心为同学着想，将真正的知识传授给大家是后盾人永远不变的追求。
            </p>
        </section>
    </article>
</main>
```



# 弹性布局

## 了解弹性

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

Flex 是 Flexible Box 的缩写，意为"弹性布局"，可以轻松的控制元素排列、对齐和顺序的控制。

现在的终端类型非常多，使用弹性盒模型可以让元素在不同尺寸终端控制尺寸。

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#响应体验)响应体验

通过下面小米移动端中间区域水平排列元素，来体验一下响应布局带来的便利性。

![image-20190826121529633](https://houdunren.gitee.io/note/assets/img/image-20190826121529633.ee1de0d0.png)

![image-20190826122919354](data:image/png;base64,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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  div.container {
    display: flex;
    height: 100vh;
    justify-content: space-evenly;
  }
  div.container div {
    border: solid 1px #ddd;
  }
  div.container div:nth-of-type(1) {
    min-width: 80px;
    background: #4E9166;
  }
  div.container div:nth-of-type(2) {
    flex: 1;
    background: #ddd;
  }
</style>
...

<div class="container">
    <div></div>
    <div></div>
</div>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#布局对比)布局对比

下面通过微信界面的例子来对比传统布局与弹性布局的不同。

![Screenshot_20190826-115538](https://houdunren.gitee.io/note/assets/img/Screenshot_20190826-115538-6791965.97ee5101.jpg)

#### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#传统布局)传统布局

```text
<style>
	* {
    padding: 0;
    margin: 0;
  }
  main,
  footer {
    border: solid 1px #ddd;
    box-sizing: border-box;
  }
  main {
    background: #ddd;
    height: 100vh;
    padding-bottom: 55px;
    background-clip: content-box;
  }
  footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 50px;
  }
  footer div {
    width: 33%;
    float: left;
    text-align: center;
    line-height: 3em;
    height: 100%;
    background: linear-gradient(to bottom, #f3f3f3, #eee, #f3f3f3);
    cursor: pointer;
  }
  footer div:nth-child(n+2) {
    border-left: solid 1px #ddd;
  }
</style>
...

<body>
    <main></main>
    <footer>
        <div>1</div>
        <div>2</div>
        <div>3</div>
    </footer>
</body>
```

#### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#弹性布局)弹性布局

```text
<style>
	* {
    padding: 0;
    margin: 0;
  }
  body {
    display: flex;
    flex-direction: column;
    height: 100vh;
  }
  main {
    border: solid 1px #ddd;
    background: #ddd;
    background-clip: content-box;
    margin-bottom: 5px;
    flex: 1;
  }
  footer {
    flex: 0;
    display: flex;
    justify-content: space-evenly;
    border-top: solid 1px #ddd;
    min-height: 50px;
  }
  footer div {
    flex: 1;
    text-align: center;
    line-height: 3em;
    background: linear-gradient(to bottom, #f3f3f3, #eee, #f3f3f3);
    cursor: pointer;
  }
  footer div:nth-child(n+2) {
    border-left: solid 1px #ddd;
  }
</style>
...
<body>
    <main></main>
    <footer>
        <div>1</div>
        <div>2</div>
        <div>3</div>
    </footer>
</body>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#弹性盒子)弹性盒子

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#声明定义)声明定义

容器盒子里面包含着容器元素，使用 `display:flex` 或 `display:inline-flex` 声明为弹性盒子。

**声明块级弹性盒子**

![image-20190826013111496](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABA0AAACaCAYAAADCUbEFAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABIwSURBVHgB7d1fqFRVGwfg1zqmUDcJImh2EZVWoORNQRFSQXSRGN1lF5YFKtGdURqYUJQG/YGUqFCjCKIQvCgRhfJCQUSCQPIERWSGUFGEGGZ1vvYWP86f0W/1ueacs9d6BuzM7FmzZr3Pu8fwd9bMTBn65xIuBAgQIECAAAECBAgQIECAAIFRApeMuu0mAQIECBAgQIAAAQIECBAgQKAVEBo4EQgQIECAAAECBAgQIECAAIGeAkKDniwOEiBAgAABAgQIECBAgAABAkID5wABAgQIECBAgAABAgQIECDQU0Bo0JPFQQIECBAgQIAAAQIECBAgQEBo4BwgQIAAAQIECBAgQIAAAQIEegoIDXqyOEiAAAECBAgQIECAAAECBAgIDZwDBAgQIECAAAECBAgQIECAQE8BoUFPFgcJECBAgAABAgQIECBAgAABoYFzgAABAgQIECBAgAABAgQIEOgpIDToyeIgAQIECBAgQIAAAQIECBAgIDRwDhAgQIAAAQIECBAgQIAAAQI9BQZ6Hh12cPfu3cNuuUqAAAECBAgQIECAAAECBAh0XeCee+5JKsFOgyQmgwgQIECAAAECBAgQIECAQH0CQoP6eq5iAgQIECBAgAABAgQIECCQJPA/354wfJbU7QvDH+M6AQIECBAgQIAAAQIECBAgMPEC/8/HD9hpMPF9swICBAgQIECAAAECBAgQIDApBYQGk7ItFkWAAAECBAgQIECAAAECBCZeQGgw8T2wAgIECBAgQIAAAQIECBAgMCkFhAaTsi0WRYAAAQIECBAgQIAAAQIEJl5AaDDxPbACAgQIECBAgAABAgQIECAwKQWEBpOyLRZFgAABAgQIECBAgAABAgQmXkBoMPE9sAICBAgQIECAAAECBAgQIDApBYQGk7ItFkWAAAECBAgQIECAAAECBCZeQGgw8T2wAgIECBAgQIAAAQIECBAgMCkFBvqxqvU3DPZjWnMSIECAAAECBAiMEtjw5bxRR9wkQIAAAQL5BOw0yGdpJgIECBAgQIAAAQIECBAgUJSA0KCodiqGAAECBAgQIECAAAECBAjkE+jL2xOGL8+WueEarhOION/bd7xWnB0EvD6cAwRSBc73/5LUxxtHgAABAgRSBew0SJUyjgABAgQIECBAgAABAgQIVCYgNKis4colQIAAAQIECBAgQIAAAQKpAkKDVCnjCBAgQIAAAQIECBAgQIBAZQJCg8oarlwCBAgQIECAAAECBAgQIJAqIDRIlTKOAAECBAgQIECAAAECBAhUJiA0qKzhyiVAgAABAgQIECBAgAABAqkCQoNUKeMIECBAgAABAgQIECBAgEBlAkKDyhquXAIECBAgQIAAAQIECBAgkCogNEiVMo4AAQIECBAgQIAAAQIECFQmIDSorOHKJUCAAAECBAgQIECAAAECqQJCg1Qp4wgQIECAAAECBAgQIECAQGUCQoPKGq5cAgQIECBAgAABAgQIECCQKiA0SJUyjgABAgQIECBAgAABAgQIVCYgNKis4colQIAAAQIECBAgQIAAAQKpAkKDVCnjCBAgQIAAAQIECBAgQIBAZQJCg8oarlwCBAgQIECAAAECBAgQIJAqIDRIlTKOAAECBAgQIECAAAECBAhUJiA0qKzhyiVAgAABAgQIECBAgAABAqkCQoNUKeMIECBAgAABAgQIECBAgEBlAkKDyhquXAIECBAgQIAAAQIECBAgkCogNEiVMo4AAQIECBAgQIAAAQIECFQmIDSorOHKJUCAAAECBAgQIECAAAECqQJCg1Qp4wgQIECAAAECBAgQIECAQGUCQoPKGq5cAgQIECBAgAABAgQIECCQKiA0SJUyjgABAgQIECBAgAABAgQIVCYgNKis4colQIAAAQIECBAgQIAAAQKpAkKDVCnjCBAgQIAAAQIECBAgQIBAZQJCg8oarlwCBAgQIECAAAECBAgQIJAqIDRIlTKOAAECBAgQIECAAAECBAhUJiA0qKzhyiVAgAABAgQIECBAgAABAqkCQoNUKeMIECBAgAABAgQIECBAgEBlAkKDyhquXAIECBAgQIAAAQIECBAgkCogNEiVMo4AAQIECBAgQIAAAQIECFQmIDSorOHKJUCAAAECBAgQIECAAAECqQJCg1Qp4wgQIECAAAECBAgQIECAQGUCQoPKGq5cAgQIECBAgAABAgQIECCQKiA0SJUyjgABAgQIECBAgAABAgQIVCYgNKis4colQIAAAQIECBAgQIAAAQKpAgOpA40rQ2Dnzp3x+eefx5o1a+Lyyy8voyhVELhIgR07dsSePXviq6++ijlz5sSdd94ZDz30UAwM+CvyImk9vOMCf/75Z7z77rvx6aefxvHjx2P27Nlx2223xfLly2P69Okdr87yCRAgQIAAgRQBOw1SlAoYc+bMmdiwYUMsXbq0/Xnq1KkCqlICgYsT+Pvvv2PZsmXxwAMPxHvvvRe//vpr+w+khx9+OBYvXhynT5++uCfwaAIdFvj999/b18EjjzzSvi6+//779nWyatWqWLhwYfz2228drs7SCRAgQIAAgVQBoUGqVIfHvf3223HVVVfFs88+2+EqLJ1AfoF33nkn3n///XjwwQfjxx9/jMOHD8eJEyfa36Lu378/Xn755fxPakYCHRFYv359NK+DlStXtrsMBgcH29fHihUr2l05Gzdu7EgllkmAAAECBAhcjIDQ4GL0OvLY7du3x7x58+LQoUPR/MbIhQCBswKvvvpqe+X111//71brWbNmxVNPPdUe37t3LyoCVQoMDQ1FE6o1l+eff759W0JzvXl9PPPMM83VOHDgQPvTfwgQIECAAIGyBbxht+z+ttU1Ow3mz59fQaVKJJAu0LxX+4svvmi3X1955ZUjHnjddde1t3/66acRx90gUIvAH3/8EU888URce+21MWPGjBFlX3LJ2d83TJ06dcRxNwgQIECAAIEyBYQGZfZ1RFXDA4PmPdwuBAhETJkyJT755JP2N6ejPfbt29ceuuWWW0bf5TaBKgSmTZsW69atG1NrE6S98MIL7fElS5aMud8BAgQIECBAoDwBoUF5PVURAQIJApdeemnce++9Y0b+8MMP8eijj7bHH3/88TH3O0CgRoGXXnopPvzww/Ztbk39a9eujeYDEV0IECBAgACB8gV8pkH5PVYhAQKJAs2Hvt18883xzTffxObNm2PBggWJjzSMQNkCM2fOjKuvvjquuOKKttAmXPvll1/KLlp1BAgQIECAQCsgNHAiECBQvcBff/0VL774Ytx+++3RfB3pjh07YvXq1dW7ACBwTmD58uXx0Ucfxc8//xxvvPFGNB+we+4DQ8+N8ZMAAQIECBAoU0BoUGZfVUWAQKJA813z9913Xzz99NNx6623xpEjR+L+++9PfLRhBMoUaHYS7Ny5M7777rsRBV522WXRfOVi8zW+H3zwQZw+fXrE/W4QIECAAAEC5QkIDcrrqYoIEEgUaP7Bc/fdd8euXbvisccei88++6zdgp34cMMIFCvw7bffxtKlS2Pbtm1jahwYGIiFCxfGyZMn2505YwY4QIAAAQIECBQlIDQoqp2KIUDg3whs2rSp/WC3lStXxptvvhnNJ8a7ECAQsWjRopZhy5YtMfqrR48ePRoff/xx3HjjjTH660rZESBAgAABAuUJ+PaE8nqqIgIEEgSarx9tQoPm0nwn/ZNPPjnmUc2Hv61Zs2bMcQcIlC4wffr0eOutt9odODfddFMsW7Ys7rjjjhgcHIznnnuuLf+1114rnUF9BAgQIECAwD8CQoNKT4Pm6+ZcCNQscPz48XZ7dWOwdevWnhTN+7aFBj1pHKxAoPnq0TNnzrSB2iuvvBLNn+Zy/fXXR7MD4a677qpAQYkECBAgQICAtydUdg40708dGhqKGTNmVFa5cgmMFJg7d277WmheD+f7c+zYsZEPcotAZQKrVq1qv1rx66+/joMHD8aJEyfa3QYCg8pOBOUSIECAQNUCdhpU3X7FEyBAgACBCws0H3x4zTXXtH8uPNK9BAgQIECAQIkCdhqU2FU1ESBAgAABAgQIECBAgACBDAJCgwyIpiBAgAABAgQIECBAgAABAiUKCA1K7KqaCBAgQIAAAQIECBAgQIBABgGhQQZEUxAgQIAAAQIECBAgQIAAgRIFhAYldlVNBAgQIECAAAECBAgQIEAgg4DQIAOiKQgQIECAAAECBAgQIECAQIkCQoMSu6omAgQIECBAgAABAgQIECCQQUBokAHRFAQIECBAgAABAgQIECBAoEQBoUGJXVUTAQIECBAgQIAAAQIECBDIICA0yIBoCgIECBAgQIAAAQIECBAgUKKA0KDErqqJAAECBAgQIECAAAECBAhkEBAaZEA0BQECBAgQIECAAAECBAgQKFFAaFBiV9VEgAABAgQIECBAgAABAgQyCAgNMiCaggABAgQIECBAgAABAgQIlCggNCixq2oiQIAAAQIECBAgQIAAAQIZBIQGGRBNQYAAAQIECBAgQIAAAQIEShQQGpTYVTURIECAAAECBAgQIECAAIEMAkKDDIimIECAAAECBAgQIECAAAECJQoIDUrsqpoIECBAgAABAgQIECBAgEAGAaFBBkRTECBAgAABAgQIECBAgACBEgWEBiV2VU0ECBAgQIAAAQIECBAgQCCDgNAgA6IpCBAgQIAAAQIECBAgQIBAiQJCgxK7qiYCBAgQIECAAAECBAgQIJBBQGiQAdEUBAgQIECAAAECBAgQIECgRAGhQYldVRMBAgQIECBAgAABAgQIEMggIDTIgGgKAgQIECBAgAABAgQIECBQooDQoMSuqokAAQIECBAgQIAAAQIECGQQEBpkQDQFAQIECBAgQIAAAQIECBAoUUBoUGJX1USAAAECBAgQIECAAAECBDIICA0yIJqCAAECBAgQIECAAAECBAiUKCA0KLGraiJAgAABAgQIECBAgAABAhkEhAYZEE1BgAABAgQIECBAgAABAgRKFBAalNhVNREgQIAAAQIECBAgQIAAgQwCQoMMiKYgQIAAAQIECBAgQIAAAQIlCggNSuyqmggQIECAAAECBAgQIECAQAYBoUEGRFMQIECAAAECBAgQIECAAIESBYQGJXZVTQQIECBAgAABAgQIECBAIIOA0CADoikIECBAgAABAgQIECBAgECJAkKDEruqJgIECBAgQIAAAQIECBAgkEFAaJAB0RQECBAgQIAAAQIECBAgQKBEAaFBiV1VEwECBAgQIECAAAECBAgQyCAgNMiAaAoCBAgQIECAAAECBAgQIFCigNCgxK6qiQABAgQIECBAgAABAgQIZBAQGmRANAUBAgQIECBAgAABAgQIEChRQGhQYlfVRIAAAQIECBAgQIAAAQIEMggMZJjjglOsv2Hwgve7kwCBswJeK84EAucX8Po4v417CBAgQIAAAQL9FLDToJ+65iZAgAABAgQIECBAgAABAh0WEBp0uHmWToAAAQIECBAgQIAAAQIE+inQl7cnbPhyXj/XbG4CBAgQIECAAAECBAgQIEBgHATsNBgHZE9BgAABAgQIECBAgAABAgS6KCA06GLXrJkAAQIECBAgQIAAAQIECIyDgNBgHJA9BQECBAgQIECAAAECBAgQ6KKA0KCLXbNmAgQIECBAgAABAgQIECAwDgJCg3FA9hQECBAgQIAAAQIECBAgQKCLAkKDLnbNmgkQIECAAAECBAgQIECAwDgICA3GAdlTECBAgAABAgQIECBAgACBLgoIDbrYNWsmQIAAAQIECBAgQIAAAQLjICA0GAdkT0GAAAECBAgQIECAAAECBLooIDToYtesmQABAgQIECBAgAABAgQIjIPAwL95jt27d/+b4cYSIECAAAECBAgQIECAAAECHRaw06DDzbN0AgQIECBAgAABAgQIECDQTwGhQT91zU2AAAECBAgQIECAAAECBDosMGXon0uH12/pBAgQIECAAAECBAgQIECAQJ8E7DToE6xpCRAgQIAAAQIECBAgQIBA1wWEBl3voPUTIECAAAECBAgQIECAAIE+CQgN+gRrWgIECBAgQIAAAQIECBAg0HUBoUHXO2j9BAgQIECAAAECBAgQIECgTwJCgz7BmpYAAQIECBAgQIAAAQIECHRdQGjQ9Q5aPwECBAgQIECAAAECBAgQ6JOA0KBPsKYlQIAAAQIECBAgQIAAAQJdF/gP4ECUj/B5JaMAAAAASUVORK5CYII=)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  article {
    height: 150px;
    margin-left: 100px;
    margin-top: 100px;
    outline: solid 5px silver;
    display: flex;
    padding: 20px;
  }
  article div {
    outline: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
    line-height: 5em;
    width: 300px;
  }
</style>
...

<article>
  <div>1</div>
	<div>2</div>
	<div>3</div>
</article>
```

**声明内联级弹性盒子**

![image-20190826013016826](data:image/png;base64,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)

```text
<style>
  ...
  article {
   	...
    display: inline-flex;
    ...
  }
  ...
</style>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-direction)flex-direction

用于控制盒子元素排列的方向。

| 值             | 描述                           |
| :------------- | :----------------------------- |
| row            | 从左到右水平排列元素（默认值） |
| row-reverse    | 从右向左排列元素               |
| column         | 从上到下垂直排列元素           |
| column-reverse | 从下到上垂直排列元素           |

**row-reverse**

![image-20190825153527624](data:image/png;base64,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//33x/xXX3316O2T+MknnwwTTzxxDB3ynUUWWSQst9xy8cG/6667wnvvvRdHGSuuuGKYbrrp4vX5DqOQv/76KzzxxBNhrrnmCssvv3wYb7zx4vla/zz33HPh2WefjSOPZZZZJo5eUjpCl9wfZSWPlVdeOY5mOM89U35GPJSf+cVVV1015k/54LTGGmuE2WefPV2uUtt67errr78O9957b2C7+OKL/+++Ga3dd999gfY000wzBbgzWsRSHdJWiAzAj3ZBWJm6YCSYbce04aFDh4annnoq8Jk2Ms888/wvz3QA8aE9MY/MdNeCCy4Yxh577Hi63vNA9Ip65n54nmhjTFHQxrjeyy+/HM8ttthisYwpvyptb7jhhnjvvd3TzjvvHJ+7lG6qqaaKz3naf+aZZ+LHBRZYIB2K28kmm2yk/bRDP4S9/vrr8fmvwkhfwU+167ZpBOg099prryjGiNall14aQ+50iHRuBx98cOws6STpCK+55prAw7rhhhvGjpcpgey8KyJKR80xOrx99tknLrpZdtllAyJHh5AMQTjnnHOiSCbB58HlGB04HfuVV14ZO1se/HfffTdccskl4cQTTwzzzjtvuPrqq8OHH34YO2bChog2nSlzgiz44fNjjz0W7+nYY4+NjgrfwRFAUBZeeOFwxx13xOkFjmdDjamMF110Ubjuuuui6CA4l19+edhqq63iHyOSvffeOyYlLzp5+B1zzDHRsaH8l112WSz/QgstFPO65ZZbovATAsWBuummm+I1EKgqWb12xQIu2sUkk0wSnTSmd7KLuBil7b///jFETB298sorsU0cd9xxkSt1hSNAm8H5vO2228IDDzwQ2wehZBwp6uG8886LzhajRIQY8cZBu/baa8Nuu+0WGI3mjTo78sgjo1NGnQ0ZMiQ6eCeccEKvzwP3RdulzeCksliNvHh2nn/++dhmb7311vhsHHjggfmsK7HPaJx23ZvlHezVVlstOs08FxjPJ04WA4Zk66+/fgz7p/3sFqFP9vTTTwf6m043Bb/Ta7ANy0/niqin1a9bbrll7DwRfASaUcnpp58eR1EUHwE+//zzRxL5nm7r9ttvj04CHSCCjLGwB8ehUaN8hx56aPc6g+222y6WD8HHGIXRKSO42IUXXhjFng4fQcEOOuigKOqnnXZa3Cf8d8UVV8TziDbXpEPOjzQZnSP2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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  body {
    margin: 100px;
    font-size: 14px;
    color: #555;
  }
  article {
    width: 500px;
    border: solid 5px silver;
    display: flex;
    box-sizing: border-box;
    padding: 10px;
    flex-direction: row-reverse;
  }
  article * {
    border: solid 5px blueviolet;
    padding: 10px;
    margin: 10px;
  }
</style>
...

<article>
	<h4>后盾人</h4>
	<span>hdcms.com</span>
	<p>houdunren.com</p>
</article>
```

**column-reverse**

![image-20190825153716282](data:image/png;base64,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P35zSkQAAQQQQKBsAmVZ3Jfvbsu50CFffdiHAAIIIIBAFAJJW9BOjz+KViUPBBBAAAEEAhEg8AfSUFQTAQQQQACBKAQI/FEokgcCCCCAAAKBCBD4A2koqokAAggggEAUAgT+KBTJAwEEEEAAgUAECPyBNBTVRAABBBBAIAoBAn8UiuSBAAIIIIBAIAIE/kAaimoigAACCCAQhQCBPwpF8kAAAQQQQCAQAQJ/IA1FNRFAAAEEEIhCgMAfhSJ5IIAAAgggEIgAgT+QhqKaCCCAAAIIRCFA4I9CkTwQQAABBBAIRCC4wL9lyxabP3++/fDDD0UT79ixw12zdevWoq/hRAQQQAABBCpRILjAv2rVKrvlllts+/btRbeHHhZ0zbp164q+hhMRQAABBBCoRIHgAn8lNgL3hAACCCCAQFwCTeIqKOpytm3bZi+99JKtXbvWRo0aZb17984UsWvXLps3b54tX77cqqurbcCAAZlj/s2SJUvs3XfftZYtW9rQoUOtT58+7pCu+fLLL61Hjx62YMEC69Chgx133HHWunVre/HFF+2rr76qV15dXZ3V1tbaW2+9ZXo/fPhw69u3ry9mj1c/VbFmzRobOHCgHXHEEdaqVavMeR9//LEtXrzYdA86rvx8eu6559w+1Vv1OPzww+2oo46yTz/91BYuXGgHHHCAjRw50po3b+4v4RUBBBBAAIF6AsEG/muuucbatGnjbubpp5+2Sy65xM444ww393/FFVe4B4Jhw4a5YD179ux6N33ffffZE088YT179rTOnTvbgw8+aOedd577UdB94IEHrHHjxnbooYfa888/b88++6x7APj++++tRYsWpvImT55sJ554ot16663uAWHIkCFu+uHxxx+3iRMn2imnnFKvTG18/fXX7jqtORg8eLDdfffd7nqVr3wffvhhmzVrlnsY0APJTTfdZIMGDbKpU6e6vGbMmOHq1bFjR2vXrp3NmTPHRowYYW+++aarqx4M/vnPf7r7qaqqctfwCwEEEEAAgWyBYAO/AuekSZPcvUybNs318BX4FfxWrlxpCu5dunRxxxU4tU9JvXkF/YsvvtjGjRvn9im433HHHTZ27Fi3rV/Ks1+/frZixQq7/PLLXV7Tp093x3VM5Sjwv/rqqy74Xn311e7YU089Za+99lrewP+Pf/zDGjVq5IJ727Ztbffu3fbb3/7WHn30UTeKoKA/YcIEO/30011eS5cuNeXry9BOjSbcfPPN7vh1113njukBQaMa33zzjbuvTz75xI0MuJP4hQACCCCAQJZAsIFfQdcnDdUrOGqoXUP4Gqb3QV/nHHvssfb222+7099//333esIJJ7hX/Ro9erQL8grKShrWV9BX0hSCev/qWft02GGH2aJFi9zmr3/9azeqsHHjRjfMrmmB7AcIf41e33vvPZePgr6S8lUvXsP6Gr5X0vU+qQ46V9MIvvzjjz/eH3ajAZoa8FMZumfVXQ8MmiYgIYAAAgggkCvwn0iXuzeA7e7du2dqmT1HvnnzZss+ppMOPPDAzLmbNm2yZs2auaFyv1PD4grwGm5X0jB7dlKAzp43b9q0aeawphWuv/56N2Vwzz33uOkCjTbkSxriz66LztGwfbdu3Uz1Ujkaws9Omo7YsGFDZpef3tAO1cM/rPgTsuvm9/GKAAIIIICAFwg28PsbyH3db7/93GK77P2+l699Or5z587M0L/2aaHdZZdd5tYFaLvYpJ661gPsv//+duWVV9pDDz3k1hloKkHz+blJQV4jEtnprrvusnvvvdd69erlhv61uNAnfVfBZ5995hbt+X28IoAAAggg8L8IVFzgP/nkk00962eeecYN/euz+wrEPh155JGux68h9i+++MJ9tv/22293CwW7du3qTyvqVb3r119/3a0P0JcDqVyNHmhEoX379u5BQiMC/sFjzJgxbrhfi/J0rhYSqp5ama96aVh/5syZppX/ejjRCILWAeRbKFhUBTkJAQQQQACBHIFg5/gLrVrXvLhW1d95552m3rSSFvEp+OsaDePfcMMNVlNTk1kcqAVzWqWvlC9fDadn788eXv/d735nWvR3zjnnuOsVvPUJA00NaPhePXh99E7rAs4++2z3XnXTj6YWVDc/R69Fg1OmTLHx48e7vPQAoW2tWciXVCdND+Sm7LrmHmMbAQQQQCDdAlU/LYiryyaYO3du9qZ7r8VvUaYp/ZftkV1NbfUe+/6XHeopr1692s2fK4DmS/oOAD0I+MV2+c4pdt+3337rTu3UqVO9S1SP3OCs3r5GIjR/ny9Ir1+/3vTRwUIBv14BbCCAAAIIJFogjpi3L7E72B7/3lpZwVZz7w2lfR3abyiv3IDvz80N+tqvnr7m9AslrQUgIYAAAgggUAqBipvj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)

```text
article {
	...
	flex-direction: column-reverse;
	...
}
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-wrap)flex-wrap

flex-wrap 属性规定flex容器是单行或者多行，同时横轴的方向决定了新行堆叠的方向。

| 选项         | 说明                                             |
| :----------- | :----------------------------------------------- |
| nowrap       | 元素不拆行或不拆列（默认值）                     |
| wrap         | 容器元素在必要的时候拆行或拆列。                 |
| wrap-reverse | 容器元素在必要的时候拆行或拆列，但是以相反的顺序 |

**行元素换行**

![image-20190825160555944](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAf4AAAEsCAYAAAAimdEBAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABZHSURBVHgB7d1biFXVHwfwZY5RGSVRiJA3MP9lkQpGEAUZ1CDUSxfwQYguUJCEQb100YToAkaT9BBiFBRkDz0UQQ4RPUh/Ei3KoH+GkZCiIqndyCv+/3vzn8OMzuTe4+6cvdb6HJjcs8/aa6/f5+fp6z5zzpkJJ/93C24ECBAgQIBAFgLnZFGlIgkQIECAAIFSQPD7i0CAAAECBDIS6Bte6+Dg4PBvbRMgQIAAAQIRC/T395+2elf8p5HYQYAAAQIE0hUQ/On2VmUECBAgQOA0AcF/GokdBAgQIEAgXQHBn25vVUaAAAECBE4TEPynkdhBgAABAgTSFRjxqv6xyhztVYFjjbWfAAECBAgQ6K5AnXflueLvbm+cjQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3BQR/d72djQABAgQI9FRA8PeU38kJECBAgEB3Bfq6e7oQBgcHu31K5yPQFYH+/v5GzuMx0gijSSISaOqxE1HJPV1q14O/qPbfK2b1tGgnJ9C0wA0DOxud0mOkUU6TtVig6cdOi0ttzdI81d+aVlgIAQIECBD45wUE/z9v7AwECBAgQKA1AoK/Na2wEAIECBAg8M8LCP5/3tgZCBAgQIBAawR68uK+0apf/Z9/jbbbPgKtE1h11faerMljpCfsTtqgQK8eOw2WkMRUrviTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBAR/NSejCBAgQIBAEgKCP4k2KoIAAQIECFQTEPzVnIwiQIAAAQJJCAj+JNqoCAIECBAgUE1A8FdzMooAAQIECCQhIPiTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBAR/NSejCBAgQIBAEgKCP4k2KoIAAQIECFQTEPzVnIwiQIAAAQJJCAj+JNqoCAIECBAgUE1A8FdzMooAAQIECCQhIPiTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBAR/NSejCBAgQIBAEgKCP4k2KoIAAQIECFQTEPzVnIwiQIAAAQJJCAj+JNqoCAIECBAgUE1A8FdzMooAAQIECCQhIPiTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBAR/NSejCBAgQIBAEgKCP4k2KoIAAQIECFQTEPzVnIwiQIAAAQJJCAj+JNqoCAIECBAgUE1A8FdzMooAAQIECCQhIPiTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBAR/NSejCBAgQIBAEgKCP4k2KoIAAQIECFQTEPzVnIwiQIAAAQJJCPQlUYUiRhU4efJk2LJlSzhy5EiYO3dumDp16qjj7CSQq8Dx48fD1q1bw44dO8LOnTtD8ZiZOXNm+Xi5/vrrw4QJE3KlUXfCAoI/0eYePXo0PP/88+X/1IoSH3744XD77bcnWq2yCNQXKIJ+9erVYf/+/SMO3rx5c/n9tGnTwhNPPFH+I2DEAN8QiFzAU/2RN3C05e/Zsyc8+uijndAfbYx9BHIW2LZtW1i+fHkn9CdPnhzmz58frrnmmnDeeeeVNMXjqAj+3bt350yl9gQFXPEn1NRvvvkmvPfee6H4n5obAQKjC5w4cSKsWbOmc+eyZcvC0qVLO98XT/9v2LCh/CrGPvvss2HdunWe9u8I2YhdwBV/7B0ctv6VK1d2Qn/ixIlhyZIlw+61SYBAIfDhhx+GAwcOlBi33XbbiNAvdvb19YXiHwOLFi0qxxRX/nv37i23/YdACgKCP4UunlLDggULwvr168PixYtPuce3BAh89dVXHYR77723s33qxi233NLZ9cMPP3S2bRCIXcBT/bF3cNj6i6uUIuwvvfTScu+pL1oaNtQmgWwFfv7557L24nFy8cUXj+lwwQUXdO47ePBgZ9sGgdgFBH/sHRy2/nvuuWfYdzYJEBhNYCjEp0+fPtrdnX3bt2/vbM+ZM6ezbYNA7AKCP/YOWj8BArUEPvjggzOO/+uvv8rXAgwNFPxDEv5MQcDP+FPoohoIEGhUYGBgIPz555/lnLfeemvnLX6NnsRkBHok4Iq/R/BOS4BA+wSOHTsWXnrppfDFF1+Uiyve3//QQw+1b6FWROAsBAT/WeA5lACBdAR27doVnnnmmc6H+hQf5PPCCy+42k+nxSr5v4Dg91eBAIHsBT799NOwdu3aUHxgT3ErPq63CP2hd8hkDwQgKQHBn1Q7FUOAQB2B4hdYFT/P37RpU+ewO+64IzzwwAPlB/l0dtogkJCA4E+omUohQKC6wKFDh8Jjjz3WeWr/3HPPLZ/qX7hwYfVJjCQQoYDgj7BplkyAwNkJFB/ZW/wiqyL8i9sVV1wRVq1aFaZMmXJ2EzuaQAQCgj+CJlkiAQLNChS/pGco9K+77rrw1FNPeWq/WWKztVjA+/hb3BxLI0CgeYHi5/lDv8FyxowZQr95YjO2XMAVf8sbZHkECDQr8O6773YmnDdvXihe0X+m29y5c8Ps2bPPNMz9BKIQEPxRtMkiCRBoQuDkyZNh9+7dnak2btwYiq8z3ZYuXSr4z4Tk/mgEPNUfTavObqGTJk06uwkcTSABgV9++aXzXv065Xj81NEytu0Crvjb3qGzWF/xNOZHH310FjM4lEBaAsUH8nhMpNVT1dQXcMVf38wRBAgQIEAgWgHBH23rLJwAAQIECNQXEPz1zRxBgAABAgSiFRD80bbOwgkQIECAQH0BwV/fzBEECBAgQCBaAcEfbessnAABAgQI1BcQ/PXNHEGAAAECBKIVEPzRts7CCRAgQIBAfQHBX9/MEQQIECBAIFoBwR9t6yycAAECBAjUFxD89c0cQYAAAQIEohUQ/NG2zsIJECBAgEB9AcFf38wRBAgQIEAgWgHBH23rLJwAAQIECNQXEPz1zRxBgAABAgSiFRD80bbOwgkQIECAQH0BwV/fzBEECBAgQCBaAcEfbessnAABAgQI1BcQ/PXNHEGAAAECBKIVEPzRts7CCRAgQIBAfQHBX9/MEQQIECBAIFoBwR9t6yycAAECBAjUFxD89c0cQYAAAQIEohUQ/NG2zsIJECBAgEB9AcFf38wRBAgQIEAgWgHBH23rLJwAAQIECNQXEPz1zRxBgAABAgSiFRD80bbOwgkQIECAQH0BwV/fzBEECBAgQCBaAcEfbessnAABAgQI1BcQ/PXNHEGAAAECBKIVEPzRts7CCRAgQIBAfQHBX9/MEQQIECBAIFoBwR9t6yycAAECBAjUFxD89c0cQYAAAQIEohUQ/NG2zsIJECBAgEB9AcFf38wRBAgQIEAgWgHBH23rLJwAAQIECNQXEPz1zRxBgAABAgSiFehry8pXXbW9LUuxDgKtFPAYaWVbLIpAdAKu+KNrmQUTIECAAIHxCwj+8ds5kgABAgQIRCcg+KNrmQUTIECAAIHxCwj+8ds5kgABAgQIRCfQkxf33TCwMzooCybQTQGPkW5qOxeBvAS6Hvz9/f15CauWQE0Bj5GaYIYTIFBLwFP9tbgMJkCAAAECcQsI/rj7Z/UECBAgQKCWgOCvxWUwAQIECBCIW0Dwx90/qydAgAABArUEBH8tLoMJECBAgEDcAoI/7v5ZPQECBAgQqCUg+GtxGUyAAAECBOIWEPxx98/qCRAgQIBALQHBX4vLYAIECBAgELeA4I+7f1ZPgAABAgRqCQj+WlwGEyBAgACBuAUEf9z9s3oCBAgQIFBLQPDX4jKYAAECBAjELSD44+6f1RMgQIAAgVoCgr8Wl8EECBAgQCBuAcEfd/+sngABAgQI1BIQ/LW4DCZAgAABAnEL9HV7+YODg90+pfMR6KlAf39/T8/v5AQIEBgu0PXgL07+7xWzhq/BNoFkBW4Y2JlsbQojQCBOAU/1x9k3qyZAgAABAuMSEPzjYnMQAQIECBCIU0Dwx9k3qyZAgAABAuMSEPzjYnMQAQIECBCIU6AnL+4bjWr1f/412m77CEQjsOqq7dGs1UIJEMhXwBV/vr1XOQECBAhkKCD4M2y6kgkQIEAgXwHBn2/vVU6AAAECGQoI/gybrmQCBAgQyFdA8Ofbe5UTIECAQIYCgj/DpiuZAAECBPIVEPz59l7lBAgQIJChgODPsOlKJkCAAIF8BQR/vr1XOQECBAhkKCD4M2y6kgkQIEAgXwHBn2/vVU6AAAECGQoI/gybrmQCBAgQyFdA8Ofbe5UTIECAQIYCgj/DpiuZAAECBPIVEPz59l7lBAgQIJChgODPsOlKJkCAAIF8BQR/vr1XOQECBAhkKCD4M2y6kgkQIEAgXwHBn2/vVU6AAAECGQoI/gybrmQCBAgQyFdA8Ofbe5UTIECAQIYCgj/DpiuZAAECBPIVEPz59l7lBAgQIJChgODPsOlKJkCAAIF8BQR/vr1XOQECBAhkKCD4M2y6kgkQIEAgXwHBn2/vVU6AAAECGQoI/gybrmQCBAgQyFdA8Ofbe5UTIECAQIYCgj/DpiuZAAECBPIVEPz59l7lBAgQIJChgODPsOlKJkCAAIF8BQR/vr1XOQECBAhkKCD4M2y6kgkQIEAgXwHBn2/vVU6AAAECGQoI/gybrmQCBAgQyFdA8Ofbe5UTIECAQIYCgj/DpiuZAAECBPIV6Mu39PQr37dvX9i8eXPYuXNn2L9/f7jwwgvD9OnTw9VXXx3mz5+fPoAKCRAgQOA0AcF/Gkn8O44dOxbeeeed8P77749ZzJw5c8KKFSvCrFmzxhzjDgIECBBIT8BT/en1NKxZs2ZE6E+bNi0sXLgwzJ49O0ycOLGseMeOHeHxxx8Pv/76a4ICSiJAgACBsQRc8Y8lE+n+wcHB8Pnnn5erv+yyy8LKlSvLwB8q57fffguvvPJK2LJlSzh8+HB49dVXyzFD9/uTAAECBNIWcMWfWH83bNhQVlRc2b/44osjQr+446KLLgpPPvlkmDJlSjnu66+/Lv/0HwIECBDIQ0DwJ9Tn4mq+eBFfcbvpppvC1KlTR61u0qRJYdGiReV9R48eDQcPHhx1nJ0ECBAgkJ6Ap/oT6mkR4JdffnlZ0Y033vi3lU2YMKFzf/EPATcCBAgQyENA8CfU55kzZ4bXX3/9jBUdP348fPnll+W4yZMnl2/zO+NBBhAgQIBAEgKCP4k2Vi+i+HHA2rVrw4EDB8qD7r777uoHG0mAAAEC0QsI/uhb+PcF/P7772FgYCCcOHEi7N27N+zZs6fcLo66+eabg+D/ez/3EiBAIDUBwZ9aR0+p58iRI+Wn952yO8ybNy88+OCDYfjP+k8d43sCBAgQSE/Aq/rT6+mIioqf4S9durS8si9e6V+8t7+4fffdd+H+++8PP/7444jxviFAgACBtAVc8afd33D++eeHZcuWjajys88+Cy+//HIo3sr39NNPh7fffjv09fmrMALJNwQIEEhUwBV/oo39u7IWL14c7rrrrnJI8RqATZs2/d1w9xEgQIBAQgKCP6FmFh/Xu379+vDWW2+dsarh7/P/6aefzjjeAAIECBBIQ8Dzu2n0sazi+++/D5988km5vWTJkjE/ua8YMPxDe4qn/N0IECBAIA8BV/wJ9bn4DXxDt61btw5tjvrnt99+29l/5ZVXdrZtECBAgEDaAoI/of5ee+21nWrWrVsX9u3b1/l++Ebx4T1vvvlmZ9eCBQs62zYIECBAIG0BwZ9Qf4vfuDf0Cv7iA3seeeSRsHHjxvDHH3+UVR46dCh8/PHH5fv3h57ev/POOzu/qS8hCqUQIECAwBgCfsY/Bkysu4v37G/btq38Onz4cHjttdfKr9HqmT9/frjvvvtGu8s+AgQIEEhUQPAn2NjnnnsuFK/wf+ONN0IR/qfeig/1Wb58efmre0+9z/cECBAgkLaA4E+wv+ecc04oXtXf399f/px/165d5S/lmTp1apgxY0a45JJLEqxaSQQIECBQRUDwV1GKdEzxD4Bp06aVX5GWYNkECBAg0LCAF/c1DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYQPA3DGo6AgQIECDQZgHB3+buWBsBAgQIEGhYoK/h+cY93aqrto/7WAcSIECAAAEC1QRc8VdzMooAAQIECCQhIPiTaKMiCBAgQIBANQHBX83JKAIECBAgkISA4E+ijYogQIAAAQLVBHry4r4bBnZWW51RBAgQIECAQKMCXQ/+/v7+RgswGQECBAgQIFBdwFP91a2MJECAAAEC0QsI/uhbqAACBAgQIFBdQPBXtzKSAAECBAhELyD4o2+hAggQIECAQHUBwV/dykgCBAgQIBC9gOCPvoUKIECAAAEC1QUEf3UrIwkQIECAQPQCgj/6FiqAAAECBAhUFxD81a2MJECAAAEC0QsI/uhbqAACBAgQIFBdQPBXtzKSAAECBAhELyD4o2+hAggQIECAQHUBwV/dykgCBAgQIBC9gOCPvoUKIECAAAEC1QUEf3UrIwkQIECAQPQCgj/6FiqAAAECBAhUFxD81a2MJECAAAEC0QsI/uhbqAACBAgQIFBdoK/K0MHBwSrDjCFAgAABAgRaLuCKv+UNsjwCBAgQINCkgOBvUtNcBAgQIECg5QKCv+UNsjwCBAgQINCkgOBvUtNcBAgQIECg5QKCv+UNsjwCBAgQINCkwIST/7s1OaG5CBAgQIAAgfYKuOJvb2+sjAABAgQINC4g+BsnNSEBAgQIEGivgOBvb2+sjAABAgQINC4g+BsnNSEBAgQIEGivwH8BxXwb0oMdavYAAAAASUVORK5CYII=)

```text
<style>
	* {
    padding: 0;
    margin: 0;
    outline: solid 1px silver;
    padding: 10px;
    margin: 10px;
  }
  head {
    display: block;
  }
  body {
    font-size: 14px;
    color: #555;
  }
  article {
    width: 500px;
    border: solid 5px silver;
    box-sizing: border-box;
    padding: 10px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  article div {
    border: solid 5px blueviolet;
    padding: 30px 80px;
    margin: 10px;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

**水平排列反向换行**

![image-20190825160933131](data:image/png;base64,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vqNHj4aDBw+OOs5GAgQIEEhLwFP9afWzDPArr7yyrOrmm28+Y3UTJkxo3V/8Q8CFAAECBNIXEPyJ9XjmzJnhzTffPGtVx48fD19//XU5bvLkyeXb/M46yQACBAgQiF5A8EffwnMvoPh1wLp168KBAwfKyffee++578QMAgQIEIhSQPBH2bZzW/Sff/4Z1q5dG06cOBH27t0b9uzZU14v9nLrrbcGwX9unkYTIEAgZgHBH3P3Kq79yJEj5af3jRw+b9688PDDD4dTf9c/cozbBAgQIJCWgFf1p9XPUaspfoe/dOnS8sy+eKV/8d7+4vLDDz+EBx98MPz888+jzrORAAECBNITcMafXk/bKrrwwgvDsmXLhm3/4osvwquvvhqKt/I9++yz4d133w19ff46DENygwABAgkKOONPsKlVSlq8eHG45557yqHFawA2b95cZZoxBAgQIBC5gOCPvIEjl198XO+GDRvCO++8M/Kuttunvs//l19+abvfBgIECBBIT8Bzu4n19McffwyfffZZWdWSJUtO+8l9xYBTP7SneMrfhQABAgTSF3DGn1iPi2/gG7ps27Zt6Oqof37//fet7VdffXXruisECBAgkK6A4E+st9dff32rovXr14d9+/a1bp96pfjwnrfffru1acGCBa3rrhAgQIBAugKCP7HeFt+4N/QK/uIDex577LGwadOm8Ndff5WVHjp0KHz66afl+/eHnt6/++67W9/UlxiHcggQIEBghIDf8Y8ASeFm8Z797du3lz+HDx8Ob7zxRvkzWm3z588PDzzwwGh32UaAAAECCQoI/gSbWpT0wgsvhOIV/m+99VYown/kpfhQn+XLl5df3TvyPrcJECBAIF0BwZ9ob88777xQvKq/v7+//D3/rl27yi/lmTp1apgxY0a47LLLEq1cWQQIECBwJgHBfyadBO4r/gEwbdq08ieBcpRAgAABAh0KeHFfh4CmEyBAgACBmAQEf0zdslYCBAgQINChgODvENB0AgQIECAQk4Dgj6lb1kqAAAECBDoUEPwdAppOgAABAgRiEhD8MXXLWgkQIECAQIcCgr9DQNMJECBAgEBMAoI/pm5ZKwECBAgQ6FBA8HcIaDoBAgQIEIhJQPDH1C1rJUCAAAECHQoI/g4BTSdAgAABAjEJCP6YumWtBAgQIECgQwHB3yGg6QQIECBAICYB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)

```text
...
flex-direction: row;
flex-wrap: wrap-reverse;
...
```

**垂直元素换行**

![image-20190825161232847](data:image/png;base64,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x44d4c033wxXX311t99G8wS8sah5NS1d0bPPPhvefvvtboBed911peM0EiBQLvD777+Hjz76qNNZvI/g4Ycf/keAFh1nnHFGeOyxx7pPsG3btu62jWYKCNFm1jW6qnnz5oUnnngi3HrrrdExOggQGCvw+eefdxtvvPHGMDRUfiGveHPR3LlzO2N37tzZ3cdGMwXKXwXNXGurV7VixYpwyy23hMWLF7faweIJTFbg0KFD3Xfdnn/++eN6munTp49rnEH5CgjRfGs3oZlffvnlExpvMAEC/xS44oorQvGVeuzduzf8/PPPnWGLFi1KDdefuYDLuZkX0PQJEBgcgW+//bbzu9LRGV1//fWjm743VMCZaEMLa1kECEy9wJdffhlee+21UHz05fvvv++8K3f0qHfeeWc488wzR//re0MFhGhDC2tZBAhMvUBx6Xbr1q1jDnTDDTeE4eHhMe0amifgcm7zampFBAgcJ4Hid54rV64M1157bed2fzNmzOgcufhM9r333huKj8V4NFvAmWiz62t1BAhMoUDxudDia/Tx119/heeee65zk4XiBifFzRncUnNUp5nfnYk2s65WRYBADQInnnhiKH4XunDhws7Ri/vrjt4isIbpOORxEHAmehyQHYIAgfwFihvLF7fMLO6V2+v3ncW9ci+99NLwzTffdBZdvGO3+AsvHs0UEKLNrKtVESDQZ4H333+/8/nPmTNn9gzR4rDH3mShuMTr0VwBl3ObW1srI0CgjwKjdykq/nbo6F9riT39F1980e3yt3q7FI3cEKKNLKtFESDQb4ELLrig+5SPPvpoOHz4cPf/x24UN50fvfF8cQ/dOXPmHNttu2ECQrRhBbUcAgSmRuCSSy4J55xzTufJizPRu+++O3z22WehuFx79OjRzt8P3bx5c1i3bl13Avfff39320YzBfxOtJl1tSoCBPosULxhqPjzZ7fffnsYvaS7Zs2a6FFWrVoVli5dGu3X0QwBZ6LNqGOlVRz7JohKT2RnAg0XmDVrVnj++ec7N1eILbX43OimTZs6N2GIjdHeHAFnos2p5YRXsmXLlgnvYwcCbRco3p1bnI3edNNNnfvlFjdVOHjwYOfPpC1YsCAU/R7tERCi7am1lRIg0EeB4sYKxVln8eXRXgGXc9tbeysnQIAAgYoCQrQioN0JECBAoL0CQrS9tbdyAgQI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)

```text
...
flex-direction: column;
flex-wrap: wrap;
...
```

**垂直元素反向换行**

![image-20190825161338307](data:image/png;base64,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bRMQom2ruPUSIECAQGUCQrQySgciQIAAgbYJCNG2Vdx6CRAgQKAyASFaGaUDESBAgEDbBIRo2ypuvQQIECBQmYAQrYzSgQgQIECgbQJCtG0Vt14CBAgQqExAiFZG6UAECBAg0DYBIdq2ilsvAQIECFQmIEQro3QgAgQIEGibgBBtW8WtlwABAgQqExCilVE6EAECBAi0TUCItq3i1kuAAAEClQkI0cooHYgAAQIE2iYgRNtWceslQIAAgcoEhGhllA5EgAABAm0TEKJtq7j1EiBAgEBlAkK0MkoHIkCAAIG2CQjRtlXcegkQIECgMgEhWhmlAxEgQIBA2wSEaNsqbr0ECBAgUJmAEK2M0oEIECBAoG0CQrRtFbdeAgQIEKhMQIhWRulABAgQINA2ASHatopbLwECBAhUJiBEK6N0IAIECBBom4AQbVvFrZcAAQIEKhMQopVROhABAgQItE1AiLat4tZLgAABApUJCNHKKB2IAAECBNomIETbVnHrJUCAAIHKBIRoZZQORIAAAQJtExCibau49RIgQIBAZQJCtDJKByJAgACBtgkI0bZV3HoJECBAoDKBocqOVNGBFs/cWNGRHIYAAT9PngMEeivgSrS3vo5OgAABAg0WEKINLq6lESBAgEBvBYRob30dnQABAgQaLCBEG1xcSyNAgACB3gr09caiOUs393Z1jk6gRQJ+nlpUbEsdGIG+hejw8PDAIJgIgboL+HmqewXNv64CXs6ta+XMmwABAgT6LiBE+14CEyBAgACBugoI0bpWzrwJECBAoO8CQrTvJTABAgQIEKirgBCta+XMmwABAgT6LiBE+14CEyBAgACBugoI0bpWzrwJECBAoO8CQrTvJTABAgQIEKirgBCta+XMmwABAgT6LiBE+14CEyBAgACBugoI0bpWzrwJECBAoO8CQrTvJTABAgQIEKirgBCta+XMmwABAgT6LiBE+14CEyBAgACBugoI0bpWzrwJECBAoO8CQrTvJTABAgQIEKirgBCta+XMmwABAgT6LjDU9xmYAAECxy0wMjJy3MdwAAJ1FhgeHu7L9IVoX9idlED1Ap//69zqD+qIBGogMGfp5r7N0su5faN3YgIECBCou4AQrXsFzZ8AAQIE+iYgRPtG78QECBAgUHcBIVr3Cpo/AQIECPRNwI1FfaN3YgK9F3jq3xf2/iTOQGAcBRbP3DiOZ4ufypVo3MgIAgQIECCQKyBEc1l0EiBAgACBuIAQjRsZQYAAAQIEcgWEaC6LTgIECBAgEBcQonEjIwgQIECAQK6AEM1l0UmAAAECBOICQjRuZAQBAgQIEMgVEKK5LDoJECBAgEBcQIjGjYwgQIAAAQK5AkI0l0UnAQIECBCICwjRuJERBAgQIEAgV0CI5rLoJECAAAECcQEhGjcyggABAgQI5AoI0VwWnQQIECBAIC4gRONGRhAgQIAAgVwBIZrLopMAAQIECMQFhGjcyAgCBAgQIJArIERzWXQSIECAAIG4gBCNGxlBgAABAgRyBYRoLotOAgQIECAQFxCicSMjCBAgQIBAroAQzWXRSYAAAQIE4gJCNG5kBAECBAgQyBUQorksOgkQIECAQFxAiMaNjCBAgAABArkCQjSXRScBAgQIEIgLCNG4kREECBAgQCBXQIjmsugkQIAAAQJxASEaNzKCAAECBAjkCgjRXBadBAgQIEAgLiBE40ZGECBAgACBXAEhmsuikwABAgQIxAWEaNzICAIECBAgkCsgRHNZdBIgQIAAgbiAEI0bGUGAAAECBHIFhGgui04CBAgQIBAXEKJxIyMIECBAgECugBDNZdFJgAABAgTiAkPxIUYQIECAwD8Ftm7dGjZs2BC+//77sHv37nD66aeHc889N1x++eXhzDPP/Odw3zdUQIg2tLCWRYBAbwQOHToUVq5cGVatWpV7gtdeey3ceuutYf78+WHixIm5Y3Q2R0CINqeWVkKAwDgILFy4MHz33XfpmaZPnx6mTp0afv3117Bly5ZO/7vvvht27doVFixYkI7TaKaAEG1mXa2KAIEeCHz44YdpgJ5xxhlhyZIl4eyzz07PtHnz5vDkk0+GnTt3hk8++SRcddVVnZd30wEajRNwY1HjSmpBBAj0QuDAgQPhpZdeSg/9/PPPHxWgyYbkd6JJiB55rF279kjTvw0VEKINLaxlESBQrUByI9H+/fs7B7322ms7NxLlnSEJ0ilTpnQ2bdq0KW+IvgYJCNEGFdNSCBDoncCR33cmZ5g9e/YxTzRp0qTO9j/++OOY42ysv4AQrX8NrYAAgXEQ2LZtW3qWadOmpe1/NpK7d5Or1uSR3HTk0WwBNxY1u75WR4BARQJ33XVXSL5ijzVr1qRDZs6cmbY1mingSrSZdbUqAgT6IPDTTz+FN998s3PmCRMmhJtvvrkPs3DK8RQQouOp7VwECDRWIHn3ogcffDBd3z333OOdi1KN5ja8nNvc2loZAQLjIHD48OHw9ttvh7feeis927x588INN9yQfq/RXAEh2tzaWhkBAj0W+O2338LTTz8dNm7cmJ4puQK95ZZb0u81mi0gRJtdX6sjQKBHAuvXr+8E6L59+zpnmDx5cli8eHGYMWNGj87osIMoIEQHsSrmRIDAQAt88MEHYfny5ekc586dGx566KFw5O9D0w0ajRcQoo0vsQUSIFClwOrVq8OKFSvSQz788MPh6quvTr/XaJeAEG1Xva2WAIHjEEg+O/RIgCZ/wvLMM8+EWbNmHccR7Vp3AX/iUvcKmj8BAuMicPDgwfDss8+m51q0aJEATTXa23Al2t7aWzkBAiUEvvnmm7Bjx47OHieffHLYs2dPGBkZOeYRTjzxxJD8uYtHcwWEaHNra2UECFQokP1Elj///DMsW7ZsTEcXomNiqu0gL+fWtnQmToDAeAokb+lX9pH83tSj2QKuRJtdX6sjQKAigUcffTQkXx4EsgKuRLMa2gQIECBAoISAEC2BZSgBAgQIEMgKCNGshjYBAgQIECghIERLYBlKgAABAgSyAkI0q6FNgAABAgRKCAjREliGEiBAgACBrIAQzWpoEyBAgACBEgJCtASWoQQIECBAICsgRLMa2gQIECBAoISAEC2BZSgBAgQIEMgKCNGshjYBAgQIECghIERLYBlKgAABAgSyAkI0q6FNgAABAgRKCAjREliGEiBAgACBrIAQzWpoEyBAgACBEgJCtASWoQQIECBAICsgRLMa2gQIECBAoISAEC2BZSgBAgQIEMgKCNGshjYBAgQIECghIERLYBlKgAABAgSyAkI0q6FNgAABAgRKCAjREliGEiBAgACBrIAQzWpoEyBAgACBEgJCtASWoQQIECBAICsgRLMa2gQIECBAoISAEC2BZSgBAgQIEMgKCNGshjYBAgQIECghIERLYBlKgAABAgSyAkI0q6FNgAABAgRKCAjREliGEiBAgACBrIAQzWpoEyBAgACBEgJCtASWoQQIECBAICsgRLMa2gQIECBAoISAEC2BZSgBAgQIEMgKCNGshjYBAgQIECghIERLYBlKgAABAgSyAkI0q6FNgAABAgRKCAjREliGEiBAgACBrIAQzWpoEyBAgACBEgJDJcYaSoBAzQQWz9xYsxmbLoF6CbgSrVe9zJYAAQIEBkhAiA5QMUyFAAECBOolIETrVS+zJUCAAIEBEhCiA1QMUyFAgACBegm4sahe9TJbAoUCc5ZuLtxmAwECvREQor1xdVQC4yowPDw8rudzMgIE/hbwcq5nAgECBAgQ6FJAiHYJZzcCBAgQICBEPQcIECBAgECXAkK0Szi7ESBAgAABIeo5QIAAAQIEuhQQol3C2Y0AAQIECAhRzwECBAgQINClgBDtEs5uBAgQIEBAiHoOECBAgACBLgWEaJdwdiNAgAABAkLUc4AAAQIECHQpIES7hLMbAQIECBAQop4DBAgQIECgSwEh2iWc3QgQIECAgBD1HCBAgAABAl0KCNEu4exGgAABAgSEqOcAAQIECBDoUkCIdglnNwIECBAgIEQ9BwgQIECAQJcCQrRLOLsRIECAAAEh6jlAgAABAgS6FBCiXcLZjQABAgQICFHPAQIECBAg0KWAEO0Szm4ECBAgQECIeg4QIECAAIEuBYRol3B2I0CAAAECQtRzgAABAgQIdCkgRLuEsxsBAgQIEBgqQzAyMlJmuLEECBAgQKDRAq5EG11eiyNAgACBXgoI0V7qOjYBAgQINFpAiDa6vBZHgAABAr0UEKK91HVsAgQIEGi0gBBtdHktjgABAgR6KXDC4f8+enkCxyZAgAABAk0VcCXa1MpaFwECBAj0XECI9pzYCQgQIECgqQJCtKmVtS4CBAgQ6LmAEO05sRMQIECAQFMFhGhTK2tdBAgQINBzgf8ANFcB7bcJYxsAAAAASUVORK5CYII=)

```text
flex-direction: column;
flex-wrap: wrap-reverse;
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-flow)flex-flow

`flex-flow` 是 `flex-direction` 与 `flex-wrap` 的组合简写模式。

下面是从右向左排列，换行向上拆分行。

![image-20190825163652754](data:image/png;base64,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)

```text
flex-flow: row-reverse wrap-reverse;
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#轴说明)轴说明

**水平排列**

下面是使用 `flex-flow: row wrap` 的主轴与交叉轴说明。

![image-20190825175808514](https://houdunren.gitee.io/note/assets/img/image-20190825175808514.241ce400.png)

下面是使用 `flex-flow: row-reverse wrap-reverse` 的主轴与交叉轴说明。

![image-20190825180523789](https://houdunren.gitee.io/note/assets/img/image-20190825180523789.c688ac2e.png)

**垂直排列**

下面是使用 `flex-flow: column wrap` 的主轴与交叉轴说明。

![image-20190825181547815](https://houdunren.gitee.io/note/assets/img/image-20190825181547815.ddd72467.png)

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#justify-content)justify-content

用于控制元素在主轴上的排列方式，再次强调是主轴的排列方式。

| 选项          | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| flex-start    | 元素紧靠主轴起点                                             |
| flex-end      | 元素紧靠主轴终点                                             |
| center        | 元素从弹性容器中心开始                                       |
| space-between | 第一个元素靠起点，最后一个元素靠终点，余下元素平均分配空间   |
| space-around  | 每个元素两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍 |
| space-evenly  | 元素间距离平均分配                                           |

水平排列元素，并使用 `justify-content: flex-end` 对齐到主轴终点

![image-20190825185352912](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAlEAAACFCAYAAAB7TK3OAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAAA4ISURBVHgB7d1JiBzVHwfwl7/jgtvBFTFEI2gMGuO+L6CIF4+CiAsqghG9JOQgisaIKBIhiAdRQRTReHCNBxkP4ilxJwaCmShiiCKuuKKCcf6+ki6jmar01HRNv1f9KYjTqa1/7/MrnG+qqqvnTP41BRMBAgQIECBAgMC0BP43rbWtTIAAAQIECBAgUAgIUQ4EAgQIECBAgEADASGqAZpNCBAgQIAAAQJClGOAAAECBAgQINBAQIhqgGYTAgQIECBAgMDYVATj4+NTzTaPAAECBAgQIDBSApdccknleJ2JqqSxgAABAgQIECBQLSBEVdtYQoAAAQIECBCoFBCiKmksIECAAAECBAhUCwhR1TaWECBAgAABAgQqBaa8sXyqteturJpqffMIECBAgAABAjkJTPeDdc5E5dRdtRIgQIAAAQLJCAhRybRCIQQIECBAgEBOAkJUTt1SKwECBAgQIJCMgBCVTCsUQoAAAQIECOQkIETl1C21EiBAgAABAskICFHJtEIhBAgQIECAQE4CQlRO3VIrAQIECBAgkIyAEJVMKxRCgAABAgQI5CQgROXULbUSIECAAAECyQgIUcm0QiEECBAgQIBATgJCVE7dUisBAgQIECCQjIAQlUwrFEKAAAECBAjkJCBE5dQttRIgQIAAAQLJCAhRybRCIQQIECBAgEBOAkJUTt1SKwECBAgQIJCMgBCVTCsUQoAAAQIECOQkIETl1C21EiBAgAABAskICFHJtEIhBAgQIECAQE4CQlRO3VIrAQIECBAgkIzAWDKVKITALAusWDgxy+/o7QYhsPLDBYPYTbkPx0FJkdULx0FW7Wqt2EEfB9Mt1Jmo6YpZnwABAgQIECDwl4AQ5TAgQIAAAQIECDQQEKIaoNmEAAECBAgQICBEOQYIECBAgAABAg0E3FjeAM0m3RUY9k2K3ZVtNrJh3fTtOGjWr7a2chy0JZvXfod1HNQpORNVp2MZAQIECBAgQKBCQIiqgDGbAAECBAgQIFAnIETV6VhGgAABAgQIEKgQEKIqYMwmQIAAAQIECNQJCFF1OpYRIECAAAECBCoEhKgKGLMJECBAgAABAnUCQlSdjmUECBAgQIAAgQoBIaoCxmwCBAgQIECAQJ2AEFWnYxkBAgQIECBAoEJAiKqAMZsAAQIECBAgUCcgRNXpWEaAAAECBAgQqBAQoipgzCZAgAABAgQI1AkIUXU6lhEgQIAAAQIEKgSEqAoYswkQIECAAAECdQJCVJ2OZQQIECBAgACBCgEhqgLGbAIECBAgQIBAnYAQVadjGQECBAgQIECgQkCIqoAxmwABAgQIECBQJzBWt9AyAgTyFPjiiy/Cxx9/HPbcc89w+umn5zkIVTcS2LRpU9i8eXPR/99++y0cdthh4cgjjwznn39+2GuvvRrt00Z5CUxOTob169cXx8DWrVtD/PshhxwS5s6dGy644IKw33775TWghKsVohJujtIINBHYsGFDWLFiRdi+fXvxS/O5555rshvbZCbw008/hQceeCC89957U1b+6KOPhptuuilcdNFFUy43sxsCW7ZsCatWrQrxH1JTTY899li4/PLLwxVXXBHmzJkz1SrmTUNAiJoGllUJpCzw559/hldeeSXE/0maRkvgxx9/DNdff32IZ57itMcee4T58+eHvffeO2zbti188803xbLVq1cXvzgvvPDC0QIakdHGs07Lli0rRxvPPB5xxBHFGenPPvssfPfdd8U/rp555pkQ/39x1VVXlet60UxAiGrmZisCyQjEMxBr164NL774YvlLNJniFDIrAvEsUy9AnXrqqeHWW2/916W7devWhfvvv7/4Bfrggw+GE044IRx00EGzUps3mR2B33//Pdxxxx3lm8UzTfGM09jYP7/m33zzzXDfffcVx8Gzzz5bXOKdN29euY0X0xdwY/n0zWxBICmB1157LaxZs6b8JRp/Qcb7YEyjIfDJJ5+EN954oxjswQcfXFzK/e+9T2effXa44YYbinXiZd633nprNHBGaJTvvvtucaYpDvniiy8OV1555b8CVJx/5plnFpd04+s4ffDBB3+/8N/GAkJUYzobEkhLYJ999glLliwJ9957b9h3333TKk41rQls3Lix3PeNN95YeZ9LvKG4N8X7ZkzdEoghqjddffXVvZc7/TznnHPKeRMTE+VrL5oJ/HOer9n2tiJAYMgCCxYsCLfddls466yzKn+BDrlEb9+iwKefflru/bjjjitf//fFjmen4r0xpm4JxMt28dN3Bx54YDjggAP6Glz89K5pZgJC1Mz8bE1g6ALHH3/80GtQwPAE4g3DcYo3k9d9dD0+8qI3HX300b2XfnZE4Oabb+5rJDteynUc9EVWu5IQVctjIQECBNIWiI816Gd6+umny9WOPfbY8rUXoyPwzjvvhIceeqgYcLz8f+65547O4FsaqRDVEqzdEiBAIBWB8fHx8ibiQw89NJxyyimplKaOFgVeffXVEO+V+uGHH8Lnn38e4id54xQD1F133eXeyQHYC1EDQLQLAgQIpCrwwgsvhMcff7ws7/bbbw+77bZb+XcvuisQP3Sw4+W73khvueWWsHDhwt5f/ZyBgBA1AzybEiBAIFWBX3/9tXg21I6f2lq6dGk46qijUi1ZXQMWiJ/IPPzww8PPP/8c4r1z8dsM4hSfGRYv7cXjwVPLZ4YuRM3Mz9YECBBITuCjjz4Kd955Z3n5Jt50Hr8KaPHixcnVqqD2BOJzoeKf3hQ/lXn33XcX36n3+uuvh2OOOSZceumlvcV+NhDwnKgGaDYhQIBAqgLxyfXxDEPv/pd4E3m8nCdApdqx2asrPvoghqje5dz41HLTzASciZqZn60JECCQhED8LrT4lR7r168v67n22mvDZZddVv7di24KfP311+Hll18uBnfGGWeERYsWVQ50//33DzFYb9q0KXz//ffhjz/+2OnJ5pUbW7CTgBC1E4kZBAgQyEtgcnKy+N603td4xE9f3XPPPcFzgPLqY9Nq44NUX3rppWLzL7/8sjZExZV233338q2EqJKi0QuX8xqx2YgAAQLpCDz//PPlIwziFws//PDDAlQ67Wm9kviQ1d4XSsdP5MVgVDXFZZs3by4Wx8t7Oz7Jvmob86sFhKhqG0sIECCQvMBXX30VnnrqqaLOeAP5qlWr+v7aj+QHp8C+BU466aRi3V9++SU88sgjlds98cQT5ZeVn3zyyZXrWdCfgMt5/TlZiwABAkkKrF27Nmzfvr2obf78+eH999/fZZ3xrIUHbu6SKasVrrvuurBu3boQQ1R8yOa3334brrnmmjBv3rwQ75fbunVr8QGD3iXfGLjjctPMBISomfnZmgABAkMV2LJlS/n+ExMTIf7Z1RTvlRKidqWU1/J4w/jKlSvD8uXLi8LffvvtEP9MNcVP58VHYPT7RcVT7cO8vwVcznMkEOiwQO+jzB0e4sgPbdu2bdM2iGchTN0TiJ+6i5fyTjvttMrBnXfeeeHJJ58MJ554YuU6FvQv4ExU/1bWJJCNwOrVq7OpVaEzE1izZs3MdmDrTgnEJ5THB6vGy3rx+/Lik8rjP6biZb25c+f+65N5nRr4kAYjRA0J3tsSIECAAIG2BOJjLuITyeMfU3sCLue1Z2vPBAgQIECAQIcFhKgON9fQCBAgQIAAgfYEhKj2bO2ZAAECBAgQ6LCAENXh5hoaAQIECBAg0J6AENWerT0TIECAAAECHRYQojrcXEMjQIAAAQIE2hMQotqztWcCBAgQIECgwwJCVIeba2gECBAgQIBAewJCVHu29kyAAAECBAh0WECI6nBzDY0AAQIECBBoT0CIas/WngkQIECAAIEOCwhRHW6uoREgQIAAAQLtCQhR7dnaMwECBAgQINBhASGqw801NAIECBAgQKA9ASGqPVt7JkCAAAECBDosIER1uLmGRoAAAQIECLQnIES1Z2vPBAgQIECAQIcFhKgON9fQCBAgQIAAgfYExtrbtT0TyE9gxcKJ/IpW8cAFHAcDJ81yh46DLNs2q0U7EzWr3N6MAAECBAgQ6IqAENWVThoHAQIECBAgMKsCQtSscnszAgQIECBAoCsCQlRXOmkcBAgQIECAwKwKuLF8Vrm9WUoCKz9ckFI5ahmSgONgSPCJva3jILGGZFKOM1GZNEqZBAgQIECAQFoCQlRa/VANAQIECBAgkImAEJVJo5RJgAABAgQIpCUgRKXVD9UQIECAAAECmQgIUZk0SpkECBAgQIBAWgJCVFr9UA0BAgQIECCQiYAQlUmjlEmAAAECBAikJSBEpdUP1RAgQIAAAQKZCAhRmTRKmQQIECBAgEBaAkJUWv1QDQECBAgQIJCJgBCVSaOUSYAAAQIECKQlIESl1Q/VECBAgAABApkICFGZNEqZBAgQIECAQFoCQlRa/VANAQIECBAgkImAEJVJo5RJgAABAgQIpCUgRKXVD9UQIECAAAECmQgIUZk0SpkECBAgQIBAWgJCVFr9UA0BAgQIECCQiYAQlUmjlEmAAAECBAikJTDWbznj4+P9rmo9AgQIECBAgEDnBZyJ6nyLDZAAAQIECBBoQ0CIakPVPgkQIECAAIHOCwhRnW+xARIgQIAAAQJtCAhRbajaJwECBAgQINB5gTmTf02dH6UBEiBAgAABAgQGLOBM1IBB7Y4AAQIECBAYDQEhajT6bJQECBAgQIDAgAWEqAGD2h0BAgQIECAwGgJC1Gj02SgJECBAgACBAQsIUQMGtTsCBAgQIEBgNASEqNHos1ESIECAAAECAxb4P7kbAgPtAhcCAAAAAElFTkSuQmCC)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 10px;
  }
  body {
    font-size: 14px;
    color: #555;
  }
  article {
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-flow: row wrap;
    justify-content: flex-end;
  }
  article div {
    width: 80px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

使用 `space-evenly` 平均分配容器元素

![image-20190825185730386](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAlEAAACCCAYAAABmSZ12AAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAAA3ISURBVHgB7d1JiBzVHwfwl79jCIILIUFF0YhLjIoE3HC7KQoi6sHlIHgQFEk8KO4LMQeDiIgi0SR6URRBBRW8DIKCihAXRMUl6CHEhIgbLoe4R38F0/SYrp5M/TNd9V5/CoKdrnr93vv8Ks53aut5O/9dkoUAAQIECBAgQGBWAv+b1dY2JkCAAAECBAgQqASEKDsCAQIECBAgQKCBgBDVAE0TAgQIECBAgIAQZR8gQIAAAQIECDQQEKIaoGlCgAABAgQIEJioI5icnKxb5X0CBAgQIECAwNgInHfeeQPn6kjUQBZvEiBAgAABAgSGCwhRw32sJUCAAAECBAgMFBCiBrJ4kwABAgQIECAwXECIGu5jLQECBAgQIEBgoEDtheWDtq67sGrQtt4jQIAAAQIECOQmMJsb6xyJyq26xkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QkCI6kQZDIIAAQIECBDITUCIyq1ixkuAAAECBAh0QmCiE6Po6CBWLdvU0ZEZ1jCB1Z8tHba6yHX21TzLOm77qv3UfpqnQP2oHYmqt7GGAAECBAgQIFArIETV0lhBgAABAgQIEKgXEKLqbawhQIAAAQIECNQKCFG1NFYQIECAAAECBOoFXFhebzNwzbhdCDoQoUNvulC1vhj21XqbNtbYVwer208Hu7T1rv10dvKORM3Oy9YECBAgQIAAgUpAiLIjECBAgAABAgQaCAhRDdA0IUCAAAECBAgIUfYBAgQIECBAgEADASGqAZomBAgQIECAAAEhyj5AgAABAgQIEGggIEQ1QNOEAAECBAgQICBE2QcIECBAgAABAg0EhKgGaJoQIECAAAECBIQo+wABAgQIECBAoIGAENUATRMCBAgQIECAgBBlHyBAgAABAgQINBAQohqgaUKAAAECBAgQEKLsAwQIECBAgACBBgJCVAM0TQgQIECAAAECQpR9gAABAgQIECDQQECIaoCmCQECBAgQIEBAiLIPECBAgAABAgQaCEw0aKNJAQI7duxI7733XjWTU045JS1YsKCAWZlCCQI//fRT+uCDD9IXX3yRtm3blvbZZ5+0ZMmStHz58nTMMceUMEVzKEDg119/TW+88UbavHlz+vrrr9O8efPSoYcemo444oh09tlnp7322quAWZrCTAJC1ExCBa7/9ttv080335y+++67anbr1q2r/vEXOFVTykzgrbfeSg8++GD6/fffp408flg99dRT6dRTT00rV65MCxcunLbeXwiMUuC1115Ljz76aIog1b9s3Lix+uv69evT9ddfn84444z+1V4XKOB0XoFFHTalDz/8MF177bW9ADVsW+sIjFLg2WefTffdd18vQC1evDidfPLJ6aijjur9Vv/OO++kG2+8Mf3xxx+jHJq+CPQEJicnq6A/FaAOOOCAdMIJJ6Rjjz22d0T/l19+SWvWrEkff/xxr50XZQo4ElVmXafN6s8//0yvv/56eu6559L27dunrfMXAl0QiP3ymWeeqYYSp0HuvvvuKkBNjS1O8T3wwAPVab44grphw4a0YsWKqdX+S2AkAlu2bEmPPPJI1Vfsp7fccks688wze33H/2tfeOGF9PTTT1fvrV69Oj3//PPVqb7eRl4UJeBIVFHlHDyZ+If/8MMP9wJUnAqJ66CmljiXbyHQpsDatWt73cep5jgC1b/sv//+6c4770z77rtv9Xb8UmAhMGqBl19+udflTTfdNC1AxYqJiYl0xRVXpNNPP73aLo5Wbd26tdfGi/IEhKjyalo7o/jN6YILLkhPPPFEOvLII2u3s4LAqAU+/fTTqssDDzwwnXXWWQO7j5sfTjvttGpd/HCKo1MWAqMUeP/996vu4hReXDxet/Sv+/LLL+s2834BAk7nFVDEmaYQ/+DjOqhzzz23d85+pjbWExiVwM8//9y7DurEE08c2m3cqTe1/PjjjymOUFkIjEJg586dKf5fGmF+pgvG+4/uz58/fxTD00dLAkJUS/Cj7DZO31144YWj7FJfBHZboP90x2GHHTa03aZNm3rr43ZyC4FRCUQweuihh3aru7fffru3XdwYYSlXQIgqt7ZmRiALgeOOOy698sorM441nhs1FaIOOeSQ3h17Mza0AYERCcSF5S+++GJ68803qx7jrr04RW0pV0CIKre2ZkagGIG4Buree+/tzefKK6/svfaCQJsCjz32WIpn733//ffpq6++6p2ajiOld9xxR5tD0/cIBISoESDrggCB5gLxSIP+h8OedNJJQy/qbd6TlgRmLxAPgo3nQvUvcR3Ubbfdlvbbb7/+t70uUMDdeQUW1ZQIlCIQD9e85pprqt/0Y05L/v36lwhUFgJdEYhHGlx++eXVjTtT1z/FE/fjyfqvvvpqV4ZpHHMk4EjUHMH6WAIEmgv89ddf6fHHH592rVQ81DCezbP33ns3/2AtCexhgYsuumjaJ8a1e7fffnv1lTDxfL6lS5emmW6YmPYB/pKVgCNRWZXLYAmUL/DNN99UTyOfutg8nm92ww03VD+YBKjy65/7DI8++ujqiftT84hvirCUK+BIVLm1NTMC2Ql8/vnn6dZbb01xJCqWuAvvnnvuSQcffHB2czHgsgQ++uijFKeXY7n44ovTokWLaicYzzuL8B/78ebNm2u3syJ/ASEq/xqaAYEiBOLLWu+6665egIqn68f1UPHDyEKgbYF4Qv5LL71UDSPuvDv//PNrh9T/sM3ffvutdjsr8hdwOi//GpoBgewFduzYkeLLWqeOQF199dXpuuuuE6Cyr2w5E+h/mv677747dGLxqIOpfXnZsmVDt7UybwEhKu/6GT2BIgQ2bNhQXYgbk4mn619yySVFzMskyhGIrxiaOoW3cePG1P9U8v5Z/v333+n+++/vvfXfL9PurfCiCAGn84ooo0kQyFcgbgfvvxU8roOanJyccULxZcTxXWYWAqMSiMdrxDV7saxZs6YK+3F3XoSrOJr6ySefpLVr1/YeyRFf9N7/ZcSjGqd+RicgRI3OWk8ECAwQ+O+Ft+vWrRuw1a5vxXUpQtSuLt6ZO4Hjjz8+XXXVVenJJ5+sOomveIk/g5bYN1etWpX6r48atJ338hYQovKu3x4ZvdvG9wijD2kosGXLlkYt7beN2DT6PwUuvfTSFI8xiK972bZt2y6fFjdCxMM3L7vssjQx4UfsLkCFvaHChRV0d6cT3z3m+8d2V8t2cylwzjnnpPhjIZCLwPLly9P69evTDz/8kLZu3Zq2b9+e4pqpww8/PB100EGOPuVSyD0wTiFqDyD6CAIECBAYP4GFCxem+NN/5974KYz3jN2dN971N3sCBAgQIECgoYAQ1RBOMwIECBAgQGC8BYSo8a6/2RMgQIAAAQINBYSohnCaESBAgAABAuMtIESNd/3NngABAgQIEGgoIEQ1hNOMAAECBAgQGG8BIWq862/2BAgQIECAQEMBIaohnGYECBAgQIDAeAsIUeNdf7MnQIAAAQIEGgoIUQ3hNCNAgAABAgTGW0CIGu/6mz0BAgQIECDQUECIaginGQECBAgQIDDeAkLUeNff7AkQIECAAIGGAkJUQzjNCBAgQIAAgfEWEKLGu/5mT4AAAQIECDQUEKIawmlGgAABAgQIjLeAEDXe9Td7AgQIECBAoKGAENUQTjMCBAgQIEBgvAUmxnv6s5/9qmWbZt9ICwItCNhXW0DX5awF7KezJtOgQwKORHWoGIZCgAABAgQI5CMgROVTKyMlQIAAAQIEOiQgRHWoGIZCgAABAgQI5CMgROVTKyMlQIAAAQIEOiTgwvIhxVj92dIha60i0B0B+2p3amEk9QL203oba/IUcCQqz7oZNQECBAgQINCygBDVcgF0T4AAAQIECOQpIETlWTejJkCAAAECBFoWEKJaLoDuCRAgQIAAgTwFhKg862bUBAgQIECAQMsCQlTLBdA9AQIECBAgkKeAEJVn3YyaAAECBAgQaFlAiGq5ALonQIAAAQIE8hQQovKsm1ETIECAAAECLQsIUS0XQPcECBAgQIBAngJCVJ51M2oCBAgQIECgZQEhquUC6J4AAQIECBDIU0CIyrNuRk2AAAECBAi0LCBEtVwA3RMgQIAAAQJ5CghRedbNqAkQIECAAIGWBYSolgugewIECBAgQCBPASEqz7oZNQECBAgQINCygBDVcgF0T4AAAQIECOQpIETlWTejJkCAAAECBFoWmJhN/5OTk7PZ3LYECBAgQIAAgWIFHIkqtrQmRoAAAQIECMylgBA1l7o+mwABAgQIEChWQIgqtrQmRoAAAQIECMylgBA1l7o+mwABAgQIEChWYN7Of5diZ2diBAgQIECAAIE5EnAkao5gfSwBAgQIECBQtoAQVXZ9zY4AAQIECBCYIwEhao5gfSwBAgQIECBQtsA/7qr8fD4/sYAAAAAASUVORK5CYII=)

```text
...
article {
  border: solid 5px silver;
  box-sizing: border-box;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-evenly;
}
...
```

垂直排列时对齐到主轴终点

![image-20190825185912164](data:image/png;base64,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)

```text
...
article {
  height: 400px;
  border: solid 5px silver;
  box-sizing: border-box;
  display: flex;
  flex-flow: column wrap;
  justify-content: flex-end;
}
...
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#align-items)align-items

用于控制容器元素在交叉轴上的排列方式。

| 选项       | 说明                           |
| :--------- | :----------------------------- |
| stretch    | 元素被拉伸以适应容器（默认值） |
| center     | 元素位于容器的中心             |
| flex-start | 元素位于容器的交叉轴开头       |
| flex-end   | 元素位于容器的交叉轴结尾       |

**拉伸适应交叉轴**

如果设置了 `width | height | min-height | min-width | max-width | max-height` ，将影响`stretch` 的结果，因为 `stretch` 优先级你于宽高设置。

![image-20190825200555744](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVYAAADUCAYAAADHoAvkAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAAA6ESURBVHgB7d1byGVzHwfw/7zGIacLx0ROxZicz2eK5MalkhxCCnFDLkSMkUiU5EIokRwunF3ocSFXzoTSa5AIyTHHUJh3ftu7t8f7Pvu/n9/M3mvW3uuzajxr9m/99/qvz3/vr/Ws0yxZvWYqJgIECBAYm8C/xvZO3ogAAQIEegKC1QeBAAECYxYQrGMG9XYECBAQrD4DBAgQGLOAYB0zqLcjQICAYPUZIECAwJgFli70fnNzcwu97DUCBAgQ+K/AySefPNTCHutQGgUCBAisnYBgXTs3rQgQIDBUQLAOpVEgQIDA2gkI1rVz04oAAQJDBRY8ebXQ0rUDtQst7zUCBAjMikD2hL491lkZedtBgEBrBARra4ZCRwgQmBUBwTorI2k7CBBojYBgbc1Q6AgBArMiIFhnZSRtBwECrREQrK0ZCh0hQGBWBATrrIyk7SBAoDUCgrU1Q6EjBAjMioBgnZWRtB0ECLRGQLC2Zih0hACBWREQrLMykraDAIHWCAjW1gyFjhAgMCsCgnVWRtJ2ECDQGgHB2pqh0BECBGZFYNGPDVyXDV6xfNW6NNd2kQIr/71sUUsaj0UxrfNCxmOdCcf6Bosdj3Gs1B7rOBS9BwECBOYJCNZ5GGYJECAwDgHBOg5F70GAAIF5AoJ1HoZZAgQIjEOgkZNXC3W0yQPJC61/2l8b9wko47FunwjjsW5+42497vHI9s8ea1bM8gQIEBghIFhHACkTIEAgKyBYs2KWJ0CAwAgBwToCSJkAAQJZAcGaFbM8AQIERggI1hFAygQIEMgKCNasmOUJECAwQkCwjgBSJkCAQFZAsGbFLE+AAIERAoJ1BJAyAQIEsgKCNStmeQIECIwQEKwjgJQJECCQFRCsWTHLEyBAYISAYB0BpEyAAIGsgGDNilmeAAECIwQE6wggZQIECGQFBGtWzPIECBAYISBYRwApEyBAICuw3v5plmxHm17+888/Lx988EHZeOONy2GHHdb06q1vjcA777xT3n333d44/Prrr2WHHXYou+66aznuuOPKJptswqhBgdWrV5cXX3yxNxYff/xxib9vt912ZaeddirHH3982WKLLRrsTftXJVgXGKM333yzrFixovzxxx+9L/AjjzyywFJempTAjz/+WG655Zby+uuvL7iKu+66q1x00UXlxBNPXLDuxfEKvPfee+Xmm28usbOx0HT33XeX0047rZx++ullyZIlCy3SudcE67wh//PPP8vTTz9d4oNiWj8CP/zwQznvvPNK7KHGtNFGG5XddtutbLrppuWTTz4pX3/9da9266239r7EJ5xwwvrpaEfWGnunl1122WBr4zeFXXbZpfeb3Kefflq+/fbb3g7Igw8+WOL7c+aZZw6W7fKMYF0z+rGH9NRTT5XHH3988IXu8odifW577I32Q/WQQw4pV1xxxT9+7X/hhRfKTTfd1Psy33bbbWW//fYr22yzzfrs8syu+7fffitXX331YPtijzT2TJcu/Ts2XnrppXLjjTf2xuPhhx/uHabZeeedB226OuPk1ZqRf/bZZ8tDDz00+ELHlzWO55maFfjwww/L888/31vptttu2zsc87/HUo866qhy/vnn95aJQzUvv/xys53s0Npee+213h5pbPJJJ51UzjjjjH+Earx+xBFH9A7LxHxMb7311l8zHf+vYJ33Adhss83KhRdeWG644Yay+eabz6uYbULg7bffHqzmggsuGHq8Lk6W9Kc4/meajEAEa38666yz+rP/9/Poo48evLZq1arBfJdn/t6n77DCsmXLypVXXlmOPPLIoV/mDvM0tukfffTRYF177733YP5/Z+bvxcYxPtNkBOJX/jjrv/XWW5etttpqUSuJq2hMpQjWNZ+CffbZx2ehBQJxMiSmOGFV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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  head {
    display: block;
  }
  body {
    font-size: 14px;
    color: #555;
  }
  article {
    height: 200px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    align-items: stretch;
  }
  article div {
    width: 80px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

**对齐到交叉轴的顶部**

![image-20190825200726661](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVIAAADTCAYAAADTTpsmAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAAA5iSURBVHgB7d1bqKXzGwfw3/yNQ04XjomcijE5n88UyY1LJRkyk0LckAsRYyQSJbkQSiSHC2cX2i7kyplQYpAIyTHHUJj//Nb/v5ZnzeztXevZe+299no/b4151nrXs973/fz2/nrXeg+zZN36qZgIECBAIC3wn3SnRgIECBDoCAhSPwgECBCYpYAgnSWgdgIECAhSPwMECBCYpcDS6fqnpqame9pzBAgQIPB/gdNPP71nYY+0R6EgQIBATkCQ5tx0ESBAoCcgSHsUCgIECOQEBGnOTRcBAgR6AtMebOrNDUX8YjU8rSRAgMDECzQdgLdHOvE/AjaQAIFRCwjSUQt7fwIEJl5AkE78ENtAAgRGLSBIRy3s/QkQmHgBQTrxQ2wDCRAYtYAgHbWw9ydAYOIFBOnED7ENJEBg1AKCdNTC3p8AgYkXEKQTP8Q2kACBUQsI0lELe38CBCZeQJBO/BDbQAIERi0gSEct7P0JEJh4AUE68UNsAwkQGLWAIB21sPcnQGDiBQa+jd5sJFYvXzubdr0DCqx5b9lArzQeAzHN+kXGY9aEc/oGg45HZqH2SDNqeggQIBAEBGnAUBIgQCAjIEgzanoIECAQBARpwFASIEAgIzAvB5umW7FRfvE73fIm7bm5PmBkPGb3E2I8Zuc3191zPR5N62ePtEnIfAIECDQICNIGILMJECDQJCBIm4TMJ0CAQIOAIG0AMpsAAQJNAoK0Sch8AgQINAgI0gYgswkQINAkIEibhMwnQIBAg4AgbQAymwABAk0CgrRJyHwCBAg0CAjSBiCzCRAg0CQgSJuEzCdAgECDgCBtADKbAAECTQKCtEnIfAIECDQICNIGILMJECDQJCBIm4TMJ0CAQIOAIG0AMpsAAQJNAoK0Sch8AgQINAgI0gYgswkQINAksGD/1EjTii30/C+//LJ89NFHZfPNNy9HHXXUQq9OK5f/7rvvlvfff78zDr///nvZZZddyp577llOOumkssUWW7TSZKE2et26deWll17qjMWnn35a6uOddtqp7LbbbuXkk08u22yzzUKt2lgsV5BOMwxvvfVWWb16dfnrr786v7CPPvroNK/y1KgEfv7553LrrbeWN954Y9pF3H333eXiiy8up5566rTzPTm3Ah988EG55ZZbSt25mG665557yllnnVXOPvvssmTJkuleMvHPCdIwxH///Xd55plnSv3BMC2MwE8//VRWrVpV6h5onTbbbLOy1157lS233LJ89tln5dtvv+3Mu+222zq/tKeccsrCrGhLllr3Pi+//PLe1tZPAnvssUfnk9rnn39evv/++84Ox0MPPVTq78+KFSt6r21TIUjXj3bdA3r66afLE0880fsFbtMPwThta93b7IboEUccUa688sq+j/Evvvhiufnmmzu/vLfffns56KCDyg477DBOmzAx6/LHH3+Ua665prc9dY+z7nkuXfpPbLz88svlpptu6ozHI4880vnaZffdd+/1tKVwsGn9SD/33HPl4Ycf7v0C11/O+n2caX4FPv744/LCCy90Frrjjjt2vl7Z8LvQ4447rlxwwQWd19SvXl555ZX5XckWLe3111/v7HHWTT7ttNPKOeec0xei9fljjjmm8zVLrev09ttv/69o2X8FaRjwrbbaqlx00UXlxhtvLFtvvXWYo5wPgXfeeae3mAsvvHDG79vqwY3uVL+/M41GoAZpdzr33HO75UZ/H3/88b3n1q5d26vbVPyzj96mrd5gW5ctW1auuuqqcuyxx874y7tBi4cjEPjkk09677r//vv36g2LuJdav6MzjUagfoSvR+W33377st122w20kHqWSxsnQbp+1A844IA2jv3YbXM9eFGneoDp306nqaeldad99tmnW/p7jgUuueSSgd4x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)

```text
...
flex-direction: row;
align-items: flex-start;
...
```

**对齐到交叉轴底部**

![image-20190825200749905](data:image/png;base64,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gbYCwrStlPUIECAwRECYDsGxiAABAm0FhGlbKesRIEBgiIAwHYJjEQECBNoKCNO2UtYjQIDAEAFhOgTHIgIECLQVEKZtpaxHgACBIQLCdAiORQQIEGgrIEzbSlmPAAECQwSE6RAciwgQINBWQJi2lbIeAQIEhggI0yE4FhEgQKCtQMg/W9J246LW++KLL8qHH35YNt5443LYYYdFbUanx33nnXfKe++91+vDb7/9VnbYYYey6667luOOO65ssskmnbaZdPGrV68uL774Yq8Xn3zySak/b7fddmWnnXYqxx9/fNliiy0mvUlTOZ4wXactb775ZlmxYkX5888/e7+0jzzyyDpr+HEhBX766adyyy23lNdff71xmLvuuqtcdNFF5cQTT2xcbuZ4Bd5///1y8803l7qD0TTdfffd5bTTTiunn356WbJkSdMqnZknTNe2+q+//ipPP/10qW8OU4zAjz/+WM4777xS90TrtNFGG5XddtutbLrppuXTTz8t33zzTW/Zrbfe2vvFPeGEE2I2tCOj1r3Qyy67bFBt/USwyy679D6xffbZZ+W7777r7XQ8+OCDpf7+nHnmmYN1u/ig82Fa94Seeuqp8vjjjw9+ibv4RpiGmuteZz9IDznkkHLFFVf86yP9Cy+8UG666abeL/Btt91W9ttvv7LNNttMw6an24bff/+9XH311YO66p5n3QNduvSfyHjppZfKjTfe2OvHww8/3DsEs/POOw+e07UHnT8B9eyzz5aHHnpo8Etcf0Hr8TnTZAU++uij8vzzz/cG3XbbbXuHWtY9NnrUUUeV888/v7dOPQzz8ssvT3YjOzTaa6+91tvzrCWfdNJJ5YwzzvhXkNb5RxxxRO+QS31cp7feeuvvBx39b+fDtN/3zTbbrFx44YXlhhtuKJtvvnl/tr8nJPD2228PRrrgggvmPP5WT3j0p3o8z7QwAjVM+9NZZ53Vf7je30cfffRg3qpVqwaPu/jgn332Lla/puZly5aVK6+8shx55JFz/gJ3lGaiZX/88ceD8fbee+/B43UfzN5brcfsTAsjUD/O17P1W2+9ddlqq61aDVK//dLlqfNhus8++3S5/1NTez2hUad60mnYV23qV9b60x577NF/6O8xC1x88cWtXnH2oZau96PzYdrqHWOlBReoX4dqMz3wwAOD1fbaa6/BYw8mL/Dqq6+W22+/vTdwPUx2zDHHTH4jpmhEYTpFzbApwwVmZmYGJzm23377cvDBBw9/gqVjFXjmmWdKPZb6ww8/lM8//7zUb8LUqQbptdde2/lzDcJ0rG83L7ZQAo899li55557Bi9/1VVXlQ022GDwswcLL1BPEs7+WN8f8ZJLLinLly/v/9jZv4VpZ1u/OAr/9ddfe98tnX12+dJLLy2777774igg0VbWb1LsuOOO5eeffy71GHe9WrBO9bu/9SN/7UuXr4ISpone7NlK+eCDD8o111wz+DhZT07VS33333//bKUuinrq90rrn/5Uv01x3XXX9a7Zf+6558qee+5ZTjnllP7izv3te6ada/niKLhekVb3dPrH5erJpvoxX5BOT//qV6ZqmPYPt9SroLo82TPtcvensPZ6jXe9RLHepag/nXPOOeXUU0/t/+jvBRb4+uuvy5NPPtkb5fDDDy/77rvvnCNuueWWpf6Prt7l6/vvvy9//PHHeldKzfnkZAuEabKGLuZy6q3d6vXg/csS61ni66+/vnT9+4uT7mm9MOKJJ57oDfvll18ODdO60oYbbjjYxC6HqY/5g7eBB9ECjz766CBI6w1M7rjjDkEa0JR60UT/BjL1DH4NyLmmuqzed7ZO9WP/7CvU5npO1vnCNGtnF1ldX331Vbn//vt7W11PNNV7aLa9jHGRlbooNvfAAw/sbecvv/xS7rzzzjm3+d577x3cJOiggw6ac70uLPAxvwtdXgQ11tsg1jtB1anew/SNN974n1td9558cf9/Mv1fK5x77rml3vKwhmn9sv63335bzj777FJvsVePa9d7ndYTgv1DMvV/gHV5lydh2uXuT1Hts+8AVe8+1OYORPVYqjBdmCbWE0srV64sl19+eW+AV155pdQ/TVM9m1+/wtb1TxI+5je9O9bO63/lY8gqFo1JoN5Jf9Sp7g2ZFk6gnqWvH/EPPfTQOQc59thjy3333VcOOOCAOdfpygJ7pg2drv8shmmyAvUG3abpE6hXPNULJerH/Xo9fr3yqe5k1I/79RZ9s8/kT9/WT3aLhOlkvY1GYFEK1K+p1Suc6h9Ts4CP+c0u5hIgQGAkAWE6EpeVCRAg0CwgTJtdzCVAgMBIAsJ0JC4rEyBAoFlAmDa7mEuAAIGRBITpSFxWJkCAQLOAMG12MZcAAQIjCQjTkbisTIAAgWYBYdrsYi4BAgRGEhCmI3FZmQABAs0CwrTZxVwCBAiMJCBMR+KyMgECBJoFhGmzi7kECBAYSUCYjsRlZQIECDQLCNNmF3MJECAwkoAwHYnLygQIEGgWEKbNLuYSIEBgJAFhOhKXlQkQINAsEPLPlqxYvqp5a8wNEdCPEPY5B9WPOWmmeoE906luj40jQGCxCAjTxdIp20mAwFQLCNOpbo+NI0BgsQgI08XSKdtJgMBUCyz4CaiV7y6baoCubZx+TFfH9WO6+jGfrbFnOh89zyVAgMBaAWHqrUCAAIExCAjTMSB6CQIECAhT7wECBAiMQUCYjgHRSxAgQECYeg8QIEBgDALCdAyIXoIAAQLC1HuAAAECYxAQpmNA9BIECBAQpt4DBAgQGIOAMB0DopcgQICAMPUeIECAwBgEhOkYEL0EAQIEhKn3AAECBMYg0OoWfDMzM2MYyksQIEAgr4A907y9VRkBAhMUEKYTxDYUAQJ5BYRp3t6qjACBCQoI0wliG4oAgbwCS1avmfKWpzICBAhMRsCe6WScjUKAQHIBYZq8wcojQGAyAsJ0Ms5GIUAguYAwTd5g5REgMBmB/wLclgKfWrxOfQAAAABJRU5ErkJggg==)

```text
flex-direction: row;
align-items: flex-end;
```

**对齐到交叉轴中心**

![image-20190825200825585](data:image/png;base64,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)

```text
flex-direction: row;
align-items: center;
```

纵向排列时交叉轴排列

![image-20190825201614169](data:image/png;base64,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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }

  article {
    height: 400px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  article div {
    height: 50px;
    min-width: 100px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
  <div>1</div>
  <div>2</div>
  <div>3</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#align-content)align-content

只适用于多行显示的弹性容器，它的作用是当flex容器在交叉轴上有多余的空间时，对元素的对齐处理。

| 选项          | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| stretch       | 将空间平均分配给元素                                         |
| flex-start    | 元素紧靠主轴起点                                             |
| flex-end      | 元素紧靠主轴终点                                             |
| center        | 元素从弹性容器中心开始                                       |
| space-between | 第一个元素靠起点，最后一个元素靠终点，余下元素平均分配空间   |
| space-around  | 每个元素两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍 |
| space-evenly  | 元素间距离平均分配                                           |

**水平排列在交叉轴中居中排列**

![image-20190825203551187](data:image/png;base64,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8MILo/edfPLJ7YEHHmgnnnjiUFYz5zoKKNR1BPvxzbtHJv/85z/bX/7yl/H/oX58G3/OFrjqqqvG2Z955pnt73//+w++vH/88cfb7373u9FXLaeffnp7++2323bbbZeNsky386TUIoO/995720UXXTT+P9Spp57aDj300EXeqw8fisCbb77ZbrzxxtG4Bx10ULv11lt/UKbdO37729+OSra73n0r6F//+ld31SVQQKFOKNSdd9559CX/3Xff3bbaaqsJ3au76bvAc889Nx7xmmuuaStWrBj/+ftXjj/++PEfX3755fF1V7IEfMm/yDz32WeftmrVqnbEEUe09dbz36dFcg7uw1evXj2e+cADDxxf//GV7z/D//HHH//43f4cIqBQFxnkL37xi0Xegw8fskD3/dDu0j0RtcUWW8y5Svfk1Myl+4+wS6aAQs3M1VZTErj//vvnddL1118/vt3+++8/vu5KloCvUbPytE0PBe6555521113jSY7+OCD22GHHdbDKY00CQGFOglF90FgDoGbb765dT/5MXPpfgpg5UpfGM54pP1boaYlap9eCHzxxRejX/L4wx/+MJ6n+/bAHnvsMf6zK3kC/lOZl6mNigW613HofpD/rbfeGk3SPWH10EMPte7LfZdsAY9Qs/O13ZQFbrnllrbXXnuNy7T73f033nhDmU45h6rjFGqVvHOjBLrXcjj33HPbOeecM97rpptuat2X+VtvvfX4ba5kC/iSPztf201B4Ntvv21nnHHG+Jn87rfmui/x99xzzymc7og+CSjUPqVhlkEKdM/kz/xYVPczpo899tjoB/0HuYyhFyXgS/5F8fng5S7w0UcftUsuuWTE0D359MgjjyjTZfxJ4RHqMg7f6osXuO2220avINXdU/caqM8888xP3mn30n1+uP8nmQZ5A4U6yNgM3ReB7q87mbl03zft/vmpS/fKUwr1p5SG+X5f8i9hbhtssMES3ru77oPAq6++us5jdH/XmEumgEeoS5Drww8/vAT36i77KPD9l+/r43xmmq6AR6jT9XYaAQLBAgo1OFyrESAwXQGFOl1vpxEgECygUIPDtRoBAtMVUKjT9XYaAQLBAgo1OFyrESAwXQGFOl1vpxEgECygUIPDtRoBAtMVUKjT9XYaAQLBAgo1OFyrESAwXQGFOl1vpxEgECygUIPDtRoBAtMV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BOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBRRqfQYmIEAgREChhgRpDQIE6gUUan0GJiBAIERAoYYEaQ0CBOoFFGp9BiYgQCBEQKGGBGkNAgTqBVbOd4RVq1bN96ZuR4AAgWUp4BHqsozd0gQILIWAQl0KVfdJgMCyFFCoyzJ2SxMgsBQCCnUpVN0nAQLLUmDF/767LMvNLU2AAIEJC3iEOmFQd0eAwPIVUKjLN3ubEyAwYQGFOmFQd0eAwPIVUKjLN3ubEyAwYQGFOmFQd0eAwPIVUKjLN3ubEyAwYYH/AxWQAPe4uhR5AAAAAElFTkSuQmCC)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  article {
    height: 500px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: flex-start;
    align-content: center;
  }
  article div {
    width: 90px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
  <div>1</div>
  <div>2</div>
  <div>3</div>
</article>
```

**垂直排列时交叉轴的排列**

![image-20190825204416667](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVYAAAE2CAYAAAA6W7rZAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABL8SURBVHgB7d1bqFRlGwfw17AyKbMiiTAwC0ooLTsXQdHBDkjHC6EDGnZRRBYGXRSEFUaBYVEXURZRFEVkByK0om5Mgqg8o3YgEukiCMEiKP2+bw3fDFl767j30vd9n/0bqFl7Zs16n+f3yN/lnPao//zvklwIECBAoDWBA1o7kgMRIECAQEdAsPqDQIAAgZYFBGvLoA5HgAABwerPAAECBFoWGD3Q8ZYtWzbQzW4jQIAAgf8LzJgxY1ALZ6yD0riDAAECQxMQrENz8ygCBAgMKiBYB6VxBwECBIYmIFiH5uZRBAgQGFRgwBevBtp7d0/UDrS/2wgQIBBFYG9f0HfGGmXy+iBAoBgBwVrMKBRCgEAUAcEaZZL6IECgGAHBWswoFEKAQBQBwRplkvogQKAYAcFazCgUQoBAFAHBGmWS+iBAoBgBwVrMKBRCgEAUAcEaZZL6IECgGAHBWswoFEKAQBQBwRplkvogQKAYAcFazCgUQoBAFAHBGmWS+iBAoBgBwVrMKBRCgEAUgb6/NjBKw/ujj4embNwfy4RdY8GGk/rqjXNfTIPu1K/zoAdwx6ACzlgHpXEHAQIEhiYgWIfm5lEECBAYVECwDkrjDgIECAxNQLAOzc2jCBAgMKiAF68GpWn3Di8UDOzZ9gtQnPeP88CruLUr4Iy1K+GaAAECLQkI1pYgHYYAAQJdAcHalXBNgACBlgQEa0uQDkOAAIGugGDtSrgmQIBASwKCtSVIhyFAgEBXQLB2JVwTIECgJQHB2hKkwxAgQKArIFi7Eq4JECDQkoBgbQnSYQgQINAVEKxdCdcECBBoSUCwtgTpMAQIEOgKCNauhGsCBAi0JCBYW4J0GAIECHQFBGtXwjUBAgRaEhCsLUE6DAECBLoCgrUr4ZoAAQItCQjWliAdhgABAl0Bv5qlKzGCrn/66ae0du3aNGbMmHTxxRePoM73bas7d+5MH3/8cVqzZk3auHFjan4+7rjj0gknnJBmzpyZDj/88H1bgKMXIyBYixnF/ink888/TzNmzEjbt29PEydOTE3IugxfYPXq1enOO+9MK1asGPBghx56aFq4cGG666670qhRowbcx41xBARrnFnutpMdO3akV155Jc2ZM2e3+7lz7wU2b96cpk2b1ntg8xfWGWeckQ455JC0fv361IRu8xfZ3XffnZo53HPPPb19bcQU8BxrzLn2utq2bVt66qmn0qRJk4RqT6W9jT/++CPdeOONvQMuXrw4/fDDD+mdd95Jr7/+elq1alX66KOPUnPG2lzuvffe9O233/b2txFTQLDGnGuvqzfffLNzhrRly5bObbNmzUoXXHBB734bwxP47LPPOmekzVHuv//+NG/evDR69K7/ELz00kvT888/31uoeTrGJbaAYI093153kydP7jwV0JxFHXnkkb3bbQxPoAnW7mX+/PndzX9dX3HFFb3bvvnmm962jZgCu/7VGrPHEd1V89zfsmXLUnPWdMAB/h5t+w/DgQcemC666KJ07LHHpqOPPnrQw//9Bavm3RgusQUEa+z5prPPPjt4h3nbe+SRR/oqoHkbVvcyderU7qbroAJOYYIOVlvlCDRPF8yePbtTUPOUzFVXXVVOcSrZJwLOWPcJq4OOZIHmeexPP/00/fLLL2ndunVp06ZNHY4mVN966600bty4kcwzInoXrCNizJrcnwIrV67c5V0A3bWfeeaZdPrpp3d/dB1YQLAGHq7W8ghcc8016fjjj0/Ne4i/++679Oqrr3YKaZ4CaN458MQTT3ghMc9o9tuqgnW/UVtopAhccsklqfmve3nyySc7H8744IMP0qJFi9Jpp52Wbr755u7drgMKePEq4FC1VJZA8zas5uPE3U9fPfbYY2UVqJrWBQRr66QOOFIEtm7d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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  article {
    height: 300px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: flex-start;
    align-content: center;
  }
  article div {
    min-width: 50px;
    min-height: 80px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#弹性元素)弹性元素

放在容器盒子中的元素即为容器元素。

- 不能使用float与clear规则
- 弹性元素均为块元素
- 绝对定位的弹性元素不参与弹性布局

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#align-self)align-self

用于控制单个元素在交叉轴上的排列方式，`align-items` 用于控制容器中所有元素的排列，而 `align-self` 用于控制一个弹性元素的交叉轴排列。

| 选项       | 说明                   |
| :--------- | :--------------------- |
| stretch    | 将空间平均分配给元素   |
| flex-start | 元素紧靠主轴起点       |
| flex-end   | 元素紧靠主轴终点       |
| center     | 元素从弹性容器中心开始 |

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  article {
    height: 400px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  article div {
    height: 50px;
    min-width: 50px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
  article div:nth-of-type(1) {
    align-self: flex-start;
  }
  article div:nth-of-type(3) {
    align-self: flex-end;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-grow)flex-grow

用于将弹性盒子的可用空间，分配给弹性元素。可以使用整数或小数声明。

下例中为三个DIV 弹性元素设置了1、3、6 ，即宽度分成10等份，第三个元素所占宽度为`(宽度/(1+3+6)) X 6`。

![image-20190827162143519](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 50px;
        padding-top: 15px;
    }

    article {
        border: solid 5px silver;
        width: 550px;
        height: 100px;
        display: flex;
        flex-direction: row;
    }

    article * {
        flex-grow: 1;
        width: 100px;
        height: 100px;
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        box-sizing: border-box;
        font-size: 35px;
        color: white;
    }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

如果弹性元素设置了宽度，将把（弹性盒子-弹性元素宽度和）后按照 `flex-grow` 进行分配 。

![image-20190825220703377](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAkQAAADbCAYAAACMT47lAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABJDSURBVHgB7d17qGVzGwfwn9cgt3IpNESMjFtEjUQujRqJXAohiiSGf9xC+WMaSm4lUUrxB5lCwh9oCimXGCLkMnKnTC6j3EIur99622MfzuU9zn72epb1WXXMPvuynmd9npnje9Zea+31fv9jKRYCBAgQIECAQI8F/tPjbbfpBAgQIECAAIFGQCDyF4EAAQIECBDovYBA1Pu/AgAIECBAgAABgcjfAQIECBAgQKD3AvOmEli5cuVUD7mfAAECBAgQINA5gSOPPHLKnu0hmpLGAwQIECBAgEBfBASivkzadhIgQIAAAQJTCghEU9J4gAABAgQIEOiLgEDUl0nbTgIECBAgQGBKgSkPqp7sFdMdjDTZ891HgAABAgQIEGhDYLYnh9lD1MaU1CRAgAABAgRSCQhEqcahGQIECBAgQKANAYGoDXU1CRAgQIAAgVQCAlGqcWiGAAECBAgQaENAIGpDXU0CBAgQIEAglYBAlGocmiFAgAABAgTaEBCI2lBXkwABAgQIEEglIBClGodmCBAgQIAAgTYEBKI21NUkQIAAAQIEUgkIRKnGoRkCBAgQIECgDQGBqA11NQkQIECAAIFUAgJRqnFohgABAgQIEGhDYFYf7vpPGly2x+p/8jKvSSSw/K2FM3ZjzjMSpX+COacfkQYJ9Fbg//n5NFcce4jmKuj1BAgQIECAQOcFBKLOj9AGECBAgAABAnMVEIjmKuj1BAgQIECAQOcFBKLOj9AGECBAgAABAnMVCD+oerIGx3Fw1GR13TezwCgPjjbnmb3beoY5tyWvLgECMwmM8ufTTLWGH7eHaFjDbQIECBAgQKCXAgJRL8duowkQIECAAIFhAYFoWMNtAgQIECBAoJcCAlEvx26jCRAgQIAAgWEBgWhYw20CBAgQIECglwICUS/HbqMJECBAgACBYQGBaFjDbQIECBAgQKCXAgJRL8duowkQIECAAIFhAYFoWMNtAgQIECBAoJcCAlEvx26jCRAgQIAAgWEBgWhYw20CBAgQIECglwICUS/HbqMJECBAgACBYQGBaFjDbQIECBAgQKCXAgJRL8duowkQIECAAIFhAYFoWMNtAgQIECBAoJcC83q51SPc6K+//rq88sorZeutty777rvvCNdsVRkEXnrppfLqq6+WN954o2y66aZl4cKF5dBDDy077rhjhvb0QCC1wLffflsef/zxsnr16vLJJ5+U+fPnlwULFpQlS5aUrbbaKnXvmuufgEA0h5m/++675eijjy7vvPNOWbRoUVm1atUc1ualmQTWrl1bli5dWu67775J21q+fHm54ooryoYbbjjp4+4k0HeBBx54oJx//vnl888//xvFZpttVuq/oYsvvvhvj7mDQFsCAtE/kP/ll1/KQw89VM4666zy3Xff/YM1eElmgR9++KEJuO+//37T5kknnVT233//Uu9/+OGHy2uvvVaWLVvWfH/ttddm3hS9EWhF4JFHHiknnnhiU7uGnzPPPLPssMMOZc2aNWXFihVNSLrkkkuava7nnntuKz0qSuCvAo4h+qvIDN/feeedZeeddy71f5LC0AxYHX34+uuvL4Mw9OijjzZ7iereoKuuuqq8/PLLpf4gr8t1113XvF3a0c3UNoEQgS+//LKccsopzboXL15cPv7443LLLbeUyy+/vNx0002l7lmv99flvPPOa36xaL7xHwItCwhEsxxADUSffvpp86r6P8T6j9zy7xGoe4Hqrvy6XHTRReWoo46asHHrr79+ueaaa0r9rbcuzzzzzITHfUOg7wJPPPHEul8W77rrrrLllltOINl8883LzTffvO6+enyehUAGAYFollPYfvvtm/e933777XLZZZeVDTbYYJZr8PTMAu+999669s4+++x1t4dv1OOGDjjg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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  article {
    width: 600px;
    position: relative;
    height: 200px;
    border: solid 5px silver;
    display: flex;
  }
  article div {
    min-height: 80px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
  article div:nth-of-type(1) {
    width: 100px;
    flex-grow: 1;
  }
  article div:nth-of-type(2) {
    width: 100px;
    flex-grow: 3;
  }
  article div:nth-of-type(3) {
    width: 300px;
    flex-grow: 6;
  }
</style>
...
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-shrink)flex-shrink

与 `flex-grow` 相反 `flex-shrink` 是在弹性盒子装不下元素时定义的缩小值。

下例在600宽的弹性盒子中放了 1000 宽的弹性元素。并为最后两个元素设置了缩放，最后一个元素的缩放比例为 500 -( ( (1000-600) / (100X1+400x3+500X6) ) x 3 ) X 500 = 220.9，计算公式说明如下：

```text
缩小比例 = 不足的空间 / (元素 1 宽度 x 缩小比例) + (元素 2 宽度 x 缩小比例) ...
最终尺寸 = 元素三宽度 - (缩小比例 x  元素 3 的宽度) X 元素宽度
```

![image-20190827172855382](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }
    body {
        padding-left: 50px;
        padding-top: 15px;
    }
    article {
        border: solid 5px silver;
        width: 400px;
        height: 120px;
        display: flex;
        padding: 10px;
        box-sizing: content-box;
    }
    article div:nth-child(1) {
        flex-shrink: 0;
    }
    article div:nth-child(2) {
        flex-shrink: 1;
    }
    article div:nth-child(3) {
        flex-shrink: 3;
    }
    article * {
        width: 200px;
        height: 100px;
        overflow: hidden;
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        border: solid 1px blueviolet;
        box-sizing: border-box;
        font-size: 30px;
        color: white;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex-basis)flex-basis

flex-basis 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。

可以是长度单位，也可以是百分比。`flex-basis`的优先级高于`width、height`属性。

**优先级**

flex-basis 优先级大于 width、height。

![image-20190825233755635](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAloAAAC+CAYAAADtEaFXAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABCdSURBVHgB7d1ryGXTHwfwNX+PF+Sa2wvEjMswyWVKKWrwZsxQIilqvJiS1BCKhNKEcgnNiyl3o9SMKLyhh3LL5QVNLjEMzcRQk8m8QJTLDGv3f45Z4+znec7MWsdez/nsGs7aZ53fWfuzFr722efsWdv/3oKNAAECBAgQIEAgu8D/sldUkAABAgQIECBAoBEQtCwEAgQIECBAgEAhAUGrEKyyBAgQIECAAAFByxogQIAAAQIECBQSGJuq7vj4+FRdPE+AAAECBAgQGCmBhQsXTut4ndGaFpNOBAgQIECAAIHBBQStwc28ggABAgQIECAwLQFBa1pMOhEgQIAAAQIEBheY8hqtnUtO9zPJnV+nTYAAAQIECBCoVWBXr1l3RqvWGTduAgQIECBAoPMCglbnp8gACRAgQIAAgVoFBK1aZ864CRAgQIAAgc4LCFqdnyIDJECAAAECBGoVELRqnTnjJkCAAAECBDovIGh1fooMkAABAgQIEKhVQNCqdeaMmwABAgQIEOi8gKDV+SkyQAIECBAgQKBWAUGr1pkzbgIECBAgQKDzAoJW56fIAAkQIECAAIFaBQStWmfOuAkQIECAAIHOCwhanZ8iAyRAgAABAgRqFRC0ap054yZAgAABAgQ6LzA2rBHefuIXw3or70OAAAECBKoTWL5ubnVjNuCpBZzRmtpIDwIECBAgQIDALgkIWrvE5kUECBAgQIAAgakFBK2pjfQgQIAAAQIECOySwNCu0dp5dD6L3lkkT3uqa+G453FWZTgC1vNwnL3LfyMw1fr+b0blXXMLOKOVW1Q9AgQIECBAgMD/BQQtS4EAAQIECBAgUEhA0CoEqywBAgQIECBAQNCyBggQIECAAAEChQQErUKwyhIgQIAAAQIEBC1rgAABAgQIECBQSEDQKgSrLAECBAgQIEBA0LIGCBAgQIAAAQKFBAStQrDKEiBAgAABAgQELWuAAAECBAgQIFBIQNAqBKssAQIECBAgQEDQsgYIECBAgAABAoUEBK1CsMoSIECAAAECBAQta4AAAQIECBAgUEhA0CoEqywBAgQIECBAQNCyBggQIECAAAEChQQErUKwyhIgQIAAAQIEBC1rgAABAgQIECBQSEDQKgSrLAECBAgQIEBA0LIGCBAgQIAAAQKFBAStQrDKEiBAgAABAgQELWuAAAECBAgQIFBIQNAqBKssAQIECBAgQEDQsgYIECBAgAABAoUEBK1CsMoSIECAAAECBAQta4AAAQIECBAgUEhA0CoEqywBAgQIECBAQNCyBggQIECAAAEChQQErUKwyhIgQIAAAQIEBC1rgAABAgQIECBQSEDQKgSrLAECBAgQIEBA0LIGCBAgQIAAAQKFBAStQrDKEiBAgAABAgQELWuAAAECBAgQIFBIQNAqBKssAQIECBAgQEDQsgYIECBAgAABAoUEBK1CsMoSIECAAAECBAQta4AAAQIECBAgUEhA0CoEqywBAgQIECBAQNCyBggQIECAAAEChQQErUKwyhIgQIAAAQIEBC1rgAABAgQIECBQSEDQKgSrLAECBAgQIEBA0LIGCBAgQIAAAQKFBAStQrDKEiBAgAABAgQELWuAAAECBAgQIFBIQNAqBKssAQIECBAgQEDQsgYIECBAgAABAoUEBK1CsMoSIECAAAECBAQta4AAAQIECBAgUEhA0CoEqywBAgQIECBAYAzB9AU2btwY4p9jjjkmHHXUUdN/oZ4zUuCHH34I7777bvj444/D5s2bm3Vx0kknhXPOOSfsscceM/KYHdTMFdi0aVN46623wvr168PWrVvD7Nmzw/HHHx8WLlwY9txzz5l74I6MQGEBQWuawC+//HJYvHhx0/uWW24Jd9111zRfqdtMFHjhhRfCkiVLws8///yvwzv99NPDQw89FObPn/+v5+wg0DWB33//Pdx7773htttu6zu0OXPmhJUrV4bzzjuv7/N2EiAwuYCgNblP+PHHH5t/ycRwZSMQBR577LFw5ZVXNhjxP0IXXXRROOyww8Lnn38ennjiifD++++HBQsWhHXr1oUjjjgCGoFOC8SAFYNW3ObNmxcuuOCCcMABBzRntlatWhU2bNgQFi1aFNauXRtOO+20Th+LwRHoooCg1TIrf/75Z7jxxhvDgw8+2NLD7lEU2LJlS7j++uubQz///PPD6tWrw7777tujuPnmm5szWfFM17Jly0I882Uj0FWB119/vReybrrppuZM/djYP/9ZiCHs1FNPbc7c3nDDDSH2txEgMJiAi+FbvOLp9ImQtc8++4SXXnopnHHGGS297R4VgfiR4MTHhQ8//HASsqLBcccdF+6+++6G48UXXwzbtm0bFRrHWaHAs88+24z65JNP/lfIik/E61Hvu+++ps8bb7wR/vjjj+axvxAgMH0BQavFKl7MHE+j33///eHrr79uTp23dLV7hAQ++eST5mgvvfTScPjhh/c98lNOOaW3/5tvvuk99oBA1wTGx8ebIV1yySVhxzNZO47zhBNO6DXjF0BsBAgMJvDPOeLBXjfje8dv2Xz66acz/jgd4GACH330UfOCGMLbtu+++6731EEHHdR77AGBrgnEs67bt2+f9FrCr776qhl2PLN/6KGHdu0QjIdA5wUErc5PkQF2SeDxxx8P8WPl+BFh2/bMM880T8Wvxu94/VZbf/sJ/FcC8edIJtvi2fxbb7216RLP4s6aNWuy7p4jQKCPgKDVB8UuAm0CZ511VttTzf4Ysp5//vnm8VVXXTVpX08S6JpADFZx/f7000/Ntw6ffvrpZojxGq4HHniga8M1HgJVCAhaVUyTQdYgEL+BePnllzdDjb+lde2119YwbGMk0BP48ssve9+qndgZPyZ/7733wt577z2xy98JEBhAwMXwA2DpSqCfwK+//hquueaaXsiKHxk+99xzrRcX96thH4EuCMQL3x955JHmG9dxTcfrsj777LMQ/8ch/j6cjQCBwQWc0RrczCsI9ATiGYD4ja14G564XXjhheHJJ58MBx54YK+PBwRqEYg/sDvxY7xxzHfccUe4+OKLw2uvvRbOPffcEL/osd9++9VyOMZJoBMCzmh1YhoMokaB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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
  }
  article {
    width: 600px;
    position: relative;
    height: 150px;
    margin-left: 100px;
    margin-top: 100px;
    outline: solid 5px silver;
    display: flex;
    padding: 20px;
  }
  article div {
    outline: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
    line-height: 5em;
  }
  article div:nth-of-type(1) {
    flex-basis: 100px;
    width: 200px;
  }
  article div:nth-of-type(2) {
    flex-basis: 200px;
  }
  article div:nth-of-type(3) {
    flex-basis: 200px;
  }
</style>
...

<article>
  <div>1</div>
  <div>2</div>
  <div>3</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#flex)flex

flex是flex-grow、flex-shrink 、flex-basis缩写组合。

> 建议使用 flex 面不要单独使用 flex-grow / flew-shrink / flex-basis 。

下例定义平均分配剩余空间，并不进行尺寸缩小，基础尺寸为200px。

![image-20190825234839683](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAlUAAAC/CAYAAADXRil/AAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAABCqSURBVHgB7d17yN7jHwfwa789/iDHnP4YYQ5DclgpRTn8M0aJpKa2P5SkRigSSstWDiF/rJxNKUThH3ooh+Xwx7QcYmzaYtQi/kCUw8b1ree23+x+tvFc1/18P9frWw/37vu767o+r88t7+f7/d73d8aWv7ZkI0CAAAECBAgQ+E8C//tPf9tfJkCAAAECBAgQ6ASEKm8EAgQIECBAgMAUCAhVU4BoCAIECBAgQIDA2DCC8fHxYS95ngABAgQIECDQpMC8efOG1u1I1VAaLxAgQIAAAQIEdl5AqNp5K3sSIECAAAECBIYKCFVDabxAgAABAgQIENh5gaHXVG07xGTnELfd158JECBAgAABAhEEduUac0eqInRcDQQIECBAgMDIBYSqkbfAAggQIECAAIEIAkJVhC6qgQABAgQIEBi5gFA18hZYAAECBAgQIBBBQKiK0EU1ECBAgAABAiMXEKpG3gILIECAAAECBCIICFURuqgGAgQIECBAYOQCQtXIW2ABBAgQIECAQAQBoSpCF9VAgAABAgQIjFxAqBp5CyyAAAECBAgQiCAgVEXoohoIECBAgACBkQsIVSNvgQUQIECAAAECEQSEqghdVAMBAgQIECAwcoGx0iu47bjPSk9hfAIECBAgQIDApAJL1syZ9PWpeNGRqqlQNAYBAgQIECDQvIBQ1fxbAAABAgQIECAwFQJC1VQoGoMAAQIECBBoXqD4NVXbCtc4p7ntnP5MYKoEdnSNoPf3VEkbp4aA93MNZXOMSmBH7+8S63KkqoSqMQkQIECAAIHmBISq5lquYAIECBAgQKCEgFBVQtWYBAgQIECAQHMCQlVzLVcwAQIECBAgUEJAqCqhakwCBAgQIECgOQGhqrmWK5gAAQIECBAoISBUlVA1JgECBAgQINCcgFDVXMsVTIAAAQIECJQQEKpKqBqTAAECBAgQaE5AqGqu5QomQIAAAQIESggIVSVUjUmAAAECBAg0JyBUNddyBRMgQIAAAQIlBISqEqrGJECAAAECBJoTEKqaa7mCCRAgQIAAgRICQlUJVWMSIECAAAECzQkIVc21XMEECBAgQIBACQGhqoSqMQkQIECAAIHmBISq5lquYAIECBAgQKCEgFBVQtWYBAgQIECAQHMCQlVzLVcwAQIECBAgUEJAqCqhakwCBAgQIECgOQGhqrmWK5gAAQIECBAoISBUlVA1JgECBAgQINCcgFDVXMsVTIAAAQIECJQQEKpKqBqTAAECBAgQaE5AqGqu5QomQIAAAQIESggIVSVUjUmAAAECBAg0JyBUNddyBRMgQIAAAQIlBISqEqrGJECAAAECBJoTEKqaa7mCCRAgQIAAgRICQlUJVWMSIECAAAECzQkIVc21XMEECBAgQIBACQGhqoSqMQkQIECAAIHmBISq5lquYAIECBAgQKCEgFBVQtWYBAgQIECAQHMCQlVzLVcwAQIECBAgUEJAqCqhakwCBAgQIECgOQGhqrmWK5gAAQIECBAoISBUlVA1JgECBAgQINCcgFDVXMsVTIAAAQIECJQQEKpKqBqTAAECBAgQaE5AqGqu5QomQIAAAQIESggIVSVUjUmAAAECBAg0JyBUNddyBRMgQIAAAQIlBISqEqrGJECAAAECBJoTEKqaa7mCCRAgQIAAgRICQlUJVWMSIECAAAECzQkIVc21XMEECBAgQIBACQGhqoSqMQkQIECAAIHmBISq5lquYAIECBAgQKCEgFBVQtWYBAgQIECAQHMCY81V3EjBGzZsSPnnyCOPTIcddlgjVSszksB3332X3nnnnfThhx+mTZs2de/lE044IZ199tlp5syZkUpVSwMCGzduTCtXrkxr165N33//fTriiCPSMccck+bNm5d22223BgTaKFGoCtjn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)

```text
* {
  padding: 0;
  margin: 0;
}
article {
  width: 600px;
  position: relative;
  height: 150px;
  margin-left: 100px;
  margin-top: 100px;
  outline: solid 5px silver;
  display: flex;
  padding: 20px;
}
article div {
  outline: solid 5px blueviolet;
  text-align: center;
  font-size: 28px;
  line-height: 5em;
  flex: 1 0 100px;
}
```

### [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#order)order

用于控制弹性元素的位置，默认为 `order:0` 数值越小越在前面，可以负数或整数。

下面是通过J动态改变order属性产生移动效果，因为本章节是讲CSS所以JS功能没有完善，只是体验一下order。

![image-20190827221628335](https://houdunren.gitee.io/note/assets/img/image-20190827221628335.1553b286.png)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 50px;
        padding-top: 15px;
    }

    article {
        border: solid 5px silver;
        width: 400px;
        height: 400px;
        padding: 10px;
        display: flex;
        flex-direction: column;

    }

    article section {
        order: 1;
        flex: 1 0 100px;
        padding: 10px;
        background: blueviolet;
        background-clip: content-box;
        display: flex;
        flex-direction: column;
        text-align: center;
        color: white;
    }

    article section div {
        flex: 1;
    }

    article section div {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    article section span {
        flex: 0;
        background: #000;
        padding: 20px;
        cursor: pointer;
    }
</style>

<article>
    <section>
        <div>houdunren.com</div>
        <span onclick="up(this)">up</span>
    </section>
    <section>
        <div>hdcms.com</div>
        <span onclick="up(this)">up</span>
    </section>
</article>

<script>
    function up(el) {
        el.parentElement.style.order = getOrder(el.parentElement) * 1 - 1;
        console.log(getOrder(el.parentElement))
    }

    function getOrder(el) {
        return getComputedStyle(el, null).order;
    }
</script>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#弹性文本)弹性文本

文本节点也在弹性布局操作范围内。

![image-20190828131005994](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAaQAAAB3CAYAAABMkTQAAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDNwMsgy8CRmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsis0ID/a2umFk/OXnzEv2lV7mNM9SiAKyW1OBlI/wHitOSCohIGBsYUIFu5vKQAxO4AskWKgI4CsueA2OkQ9gYQOwnCPgJWExLkDGTfALIFkjMSgWYwvgCydZKQxNOR2FB7QYDHxdXHRyHUyMTQ3IOAc0kHJakVJSDaOb+gsigzPaNEwREYSqkKnnnJejoKRgaGlgwMoDCHqP58AxyWjGIcCLECMQYGSxcGBubFCLEkKQaG7UD3S3IixFSWMzDwRzAwbGsoSCxKhDuA8RtLcZqxEYTNvZ2BgXXa//+fwxkY2DUZGP5e////9/b///8uA5p/i4HhwDcAfW9fWQRhS5cAAA6JSURBVHgB7d0HjJTFG8fx5xAFC0jAEisgCif2liBGpahojEAQ7CVGxRI0EaIQI+WUGCEaiIKNRGMksYEoUQHrP5ZYogFLEAPxxAZYKPbK/fmNzvru7nu3u8McL7f3neTYt83M7mfffZ93yi41DZuSkRBAAAEEEMhYoE3G9VM9AggggAACToCAxImAAAIIILBVCBCQtoq3gSeBAAIIINA2jWBibX3aZrYhgAACCCAQRaBuWfeicmghFZGwAQEEEEAgCwECUhbq1IkAAgggUCRAQCoiYQMCCCCAQBYCBKQs1KkTAQQQQKBIIHVSQ9FRmzakDUClHcc2BBBAAAEEkgLlTpSjhZRUYxkBBBBAIDMBAlJm9FSMAAIIIJAUICAlNVhGAAEEEMhMgICUGT0VI4AAAggkBQhISQ2WEUAAAQQyEyAgZUZPxQgggAACSQECUlKDZQQQQACBzAQISJnRUzECCCCAQFKAgJTUYBkBBBBAIDMBAlJm9FSMAAIIIJAUICAlNVhGAAEEEMhMgICUGT0VI4AAAggkBQhISQ2WEUAAAQQyEyAgZUZPxQgggAACSQECUlKDZQQQQACBzAQISJnRUzECCCCAQFKAgJTUYBkBBBBAIDMBAlJm9FSMAAIIIJAUICAlNVhGAAEEEMhMgICUGT0VI4AAAggkBQhISQ2WEUAAAQQyEyAgZUZPxQgggAACSQECUlKDZQQQQACBzAQISJnRUzECCCCAQFKAgJTUYBkBBBBAIDMBAlJm9FSMAAIIIJAUICAlNVhGAAEEEMhMoG1mNVMxAikCE2vrU7ayqbkE6pZ1b66iKReBigVoIVVMRgYEEEAAgeYQoIXUHKqUudkC3LlvNmGTBdASbZKHnRkJ0ELKCJ5qEUAAAQTyBQhI+R6sIYAAAghkJEBAygieahFAAAEE8gUISPkerCGAAAIIZCRAQMoInmoRQAABBPIFCEj5HqwhgAACCGQkQEDKCJ5qEUAAAQTyBQhI+R6sIYAAAghkJEBAygieahFAAAEE8gUISPkerCGAAAIIZCRAQMoInmoRQAABBPIFCEj5HqwhgAACCGQkEPXHVVevXm2ffvqprVixwoYOHWodO3Ys+bJ+/vln+/LLL+2rr76yzz//3A466CA75phjGs331FNP2bbbbmunn356o8ewAwEEEEDgH4GWdF2uOCDNnDnTvvjiC/vxxx/thx9+sA0bNphe8LJly9y23r17W48ePaxr16524okn5s6Jiy66yL755hv76aef3HF6/Pbbb92yDjr00EOte/fubn9TAemll15ygY6AlKNt1QvLly93NzT9+/ffYg46/z/66CM77bTTtlidVIRAUwLVcl2uOCDddttt1q9fPzvwwANdS2bvvfe2Pffc0/116tSpUTO1bKZMmWIKWDvuuKPtsMMO9sEHH9j111/vAlyjGQt2/PHHH9a+ffuCray2VoFFixbZgw8+aO+9994WI3jrrbds1KhRtmbNmi1WJxUh0JRAtVyXKw5IQrn88svthBNOaMondZ8uHgpCPq1cudLd3V511VV+k3u84IIL7Ljjjsvb5lfq6+ttr7328qs8IoAAAghsEqiG63JQQJo6darNnj275ElwxRVX2FFHHZU77vDDDze1qHxau3atHXnkkXnHaN8uu+ziDyl6fP/99+23336zCRMmFO1jQ+sV0Pjjk08+6cYXzzrrLNt1111zGBqnnDt3rn3yySe2zz772ODBg12LXgcsXbrUdJOT7AJWd5xulvw2tYTmzZvnuqYLuwZL5dd+jauqR+Hpp592vQNnnnlm7hx/+eWXbeedd7Y///zTnnvuOevbt6+deuqpri71KmhstVevXjZs2DDXq6Dn/Mgjj7jj1Cr88MMP7aSTTrJjjz3W2rRhjpJ8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)

```text
<style>
    article {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        height: 100vh;
        align-items: center;
        font-size: 14px;
    }
</style>

<article>
    后盾人
    <span>houdunren</span>
    后盾人
</article>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#绝对定位)绝对定位

绝对定位的弹性元素不参与弹性布局

![image-20190825215220729](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVgAAADXCAYAAABf/Un5AAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDJwMfAxSCTmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisVrZM4er5jJxT0jeu+3mzzx9TPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOD1cVcI9QkJcgz3dHEl4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBoSUDAyjMIao/3wCHJaMYB0KsQIyBwWIGUPAhQiwe6IftcgwM/H0IMTWgfwW8GBgO7itILEqEO4DxG0txmrERhM29nYGBddr//5/DGRjYNRkY/l7////39v///y5jYGC+xcBw4BsAvTZgQZTtpjMAAA88SURBVHgB7d1pqG3jHwfw5+oaM4sk6hrq75Z5HlJkuMaML7xAiBeGDCEvvNA1RhHihcwRGSLkxRHxBimZuV1CusILJYWU6e9ZtbZ9nGfvMzxr77OevT6rOPs8a+9n/dbnd+737rvWXuss+fufJVgIECBAoHGBtRqf0YQECBAgUAkIWD8IBAgQGJGAgB0RrGkJECAgYP0MECBAYEQCAnZEsKYlQIDA0mEEU1NTw1ZbR4AAgc4LrFixYqCBd7ADaawgQIBAnoCAzfPzagIECAwUELADaawgQIBAnoCAzfPzagIECAwUGHqSK/WqYQd0U883RoAAgUkRmO+Jf+9gJ6Xz9oMAgdYJCNjWtURBBAhMioCAnZRO2g8CBFonIGBb1xIFESAwKQLzPsk1KTtuP+YucO3y1XN/smfOEFi56n8zxgx0Q8A72G702V4SILAIAgJ2EdBtkgCBbggI2G702V4SILAIAgJ2EdBtkgCBbgg4ydWNPje+l07cpEmdEEy7dHXUO9iudt5+EyAwcgEBO3JiGyBAoKsCArarnbffBAiMXEDAjpzYBggQ6KqAk1x9nXeCog9jlocpq0k58ZXat1k4hq5uer6hG2vBykn5OWiC0jvYJhTNQYAAgYSAgE2gGCJAgEATAgK2CUVzECBAICEgYBMohggQINCEgJNcsyg6YB9C107SpH4k5vpzkLKa62tT2237WGp/217zOOvzDnac2rZFgECnBARsp9ptZwkQGKeAgB2ntm0RINApAQHbqXbbWQIExikgYMepbVsECHRKQMB2qt12lgCBcQoI2HFq2xYBAp0SELCdaredJUBgnAIuNBintm2NRGDNmjXh448/Duutt1447LDDRrINkxJYiICAXYia17RG4M033wwrVqwIP//8c9h2221DDFsLgbYIOETQlk6oY14Cf/75Z3j44YfDwQcfXIXrvF7syQTGJCBgxwRtM80I/PTTT+HOO+8My5YtC+ecc04zk5qFwIgEBOyIYE07GoGnnnoqXHbZZeGbb76pNnD66adX72JHszWzEsgTELB5fl69SAI77LBDePTRR8MTTzwRNt9880WqwmYJDBdwkmu4j7UtE9h9993D1NRUOOKII8Jaa3l/0LL2KOc/AgL2PyC+bbfAfvvt1+4CVUegT8BbgD4MDwkQINCkgIBtUtNcBAgQ6BNwiKAPo40P33nnnfDee++FDz/8MPz666/Vx5N23nnncNxxx4UNNtigjSWrqWGBv/76K7zyyivho48+CqtXrw7x++222y7suOOO4YQTTgibbLJJw1s0XVMCArYpyYbniZ/3vPTSS8MjjzySnDletXTXXXeFk08+Obne4GQIxL9YL7zwwvDGG28kd2jDDTcMN910U7j44ovDkiVLks8xuHgCAnbx7Adu+ccffwy77bZb77OeW221VTjwwAPDxhtvHD755JPw7rvvVutOOeWU8Nxzz4WTTjpp4FxWlCvw+eefh/ipiXqJf6nuvffeYf311w+ffvpp9a+aeInwJZdcEuKVbfHzwZZ2CQjYdvWjqua6667rhevZZ58d7rnnnmmHA15++eVw6qmnVpeInnnmmSH+Qdx6661buCdKWqjAb7/9Fk477bTey++4445w0UUXhaVL//0jGw8bxH/BxJC9/PLLw/HHHx922mmn3ms8WHwBJ7kWvwfTKli1alWIf5jisu+++4YHH3xwWrjG8aOOOqoK3fg4/uF69dVX40PLBAm8/vrr1TvUuEtXX311dbioP1zjePws8H333RcfVku88Y2lXQICtl39CG+99VavonhsbdBxtXhyo14++OCD+qGvEyIQA7ZerrjiivrhjK9HH310b+z999/vPfagHQL//nujHfV0vop4lrhe9tlnn/rhjK/9nyD4/vvv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)

```text
<style>
  * {
    padding: 0;
    margin: 0;
    padding: 10px;
    margin: 5px;
  }
  article {
    position: relative;
    height: 400px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    justify-content: space-evenly;
    align-items: flex-start;
  }
  article div {
    min-width: 50px;
    min-height: 80px;
    border: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
  }
  article div:nth-of-type(1) {
    position: absolute;
    top: 0;
  }
</style>
...

<article>
  <div>1</div>
  <div>2</div>
  <div>3</div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#微信公众号)微信公众号

下面来开发类似微信公众号布局，包括底部二级菜单的弹性布局。

![image-20190828170233608](https://houdunren.gitee.io/note/assets/img/image-20190828170233608.f95b411a.png)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        display: flex;
        flex-direction: column;
        height: 100vh;
        color: #666;
    }

    main {
        flex: 1;
    }

    footer {
        height: 50px;
        background: blueviolet;
        display: flex;
        justify-content: space-evenly;
    }

    footer section {
        display: flex;
        flex: 1 0;
        flex-direction: column-reverse;
        border-right: solid 1px #555;
        border-top: solid 1px #555;
    }

    footer section:last-child {
        border-right: none;
    }

    footer section h4 {
        flex: 0 0 50px;
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        cursor: pointer;
        color: white;
    }

    footer section ul {
        text-align: center;
        display: flex;
        flex-direction: column;
        border: solid 1px #555;
        margin-bottom: 5px;
        border-radius: 5px;
        margin: 5px;
    }

    footer section ul li {
        flex: 1 0 50px;
        border-bottom: solid 1px #555;
        display: flex;
        flex-direction: column;
        justify-content: center;
        cursor: pointer;
    }

    footer section ul li:last-child {
        border: none;
    }
</style>
...

<main></main>
<footer>
    <section>
        <h4>教程</h4>
        <ul>
            <li>PHP</li>
            <li>LINUx</li>
        </ul>
    </section>
    <section>
        <h4>直播</h4>
    </section>
</footer>
```

## [#](https://houdunren.gitee.io/note/css/10 弹性布局.html#自动空间)自动空间

在弹性布局中对元素使用`margin-right:auto` 等形式可以自动撑满空间。下例为第一个ul设置 `margin-right:auto` 表示右侧空间自动撑满，第二个ul靠近父元素右边界。

![image-20190930003328902](data:image/png;base64,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BRQYmMDcmQvSwjvvHdibatqaftLfTrfawpk77rgjfexjH0snnHBCRwdCs2fPTh//+Mc7ftxOn9g43jOe8Yw80L300kvTvvvum26++eZE4LLnnnvGJmnhwoXphhtuSHfeeWcenPLCEUcckQ477LAcjvAaoQyD/W9+85v5fQQotCc84Qn59lWvelUOZ84///xEKMEt2/z9739PW221VfrMZz6TvvCFLyT8x40bl99T/kOY85WvfCU/9ahHPSo973nPS0uWLEmf+tSnclCxzTbb9G1+wQUXpNNPP321A/e+jQd4h9CAQf95552XA63Vvf2MM85IhFr08Wc/+1nfpr/85S+zI+HOf//73/Tud7+777WPfvSjaeedd86P//Wvf6XPf/7zfa/Fnd/+9rc5NCBkaWy8n0CGRogQlSNvfvObs/d6662XHnjggUTQ9YIXvCCHQu9617vSyJEjG3dV6WPO81//+tccAq1px/SZz/3sZz97lU0JS7g+dtppp7TrrrvmsPB3v/tdDvVW2fB/D3B88pOfnD784Q/nIKfZNuVzXOf80H74wx/ma/lXv/pVIpDjPBEiEgZyTf/oRz9KkyZNKt/ufQUUUEABBRRQQAEFFGhRYM6N81p8Zz1vq6O/tYUzDIL4yzkDq07+lXr+/Pn5uB/60Ic6etw6LimCmdtuuy0PPPfff//0rGc9KxGCEH5QbUBFxyabbJIWL16cK1rKPl5++eW5CoLnvvzlLyeCiC996UuJwSyN4GbTTTd9SHXH8OHD04YbbpjDhREjRqS77747v49Qh8E7jXAoGv2iSmXKlCnpFa94RR60MzA/8sgjY5P09re/PVfRxBPtGjRTfXLMMcfk/uy2225xuDXeUhX0xCc+Mb3whS/M78WT/hM2cI0T4FANQqi08cYb9+0PK/wb28yZM3PFUbPXCDYIbQg3+R0iiCHQ+OlPf5oraN761rfm6hCqbqiWef3rX58e85jH5L41Hmcwj48//vj02c9+9iG7KEO/xhf//Oc/p8c97nG5cosA7Pvf/37jJvkxn5HrlBYVV9z/2te+liuDuB+NCiyCumOPPTaNGTMmns63fG4qcagoimAGuzlz5uTghWv497//fdpiiy363scxqMiiwsumgAIKKKCAAgoooIAC1QjMndH5SpTB9LyO/tYWzgwGyveuncDJJ5+cq07YmgqlchDK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)

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            width: 1200px;
            margin: 0 auto;
        }

        nav {
            display: flex;
            border: solid 1px green;
            margin-top: 20px;
            align-items: center;
            height: 60px;
            box-shadow: 0 0 5px rgba(0, 0, 0, .2);
            background: #f3f3f3;
        }

        ul {
            list-style: none;
        }

        ul:nth-child(1) {
            display: flex;
            align-items: center;
            margin-right: auto;
        }

        ul:nth-child(1)>li {
            margin: 0 10px;
        }

        ul:nth-child(2)>li {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #9b59b6;
        }
    </style>
</head>

<body>
    <div class="container">
        <nav>
            <ul>
                <li>houdunren</li>
                <li>视频教程</li>
                <li>每晚直播</li>
                <li>在线文档</li>
            </ul>
            <ul>
                <li>
                </li>
            </ul>
        </nav>
    </div>
</body>
```

# 栅格系统

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#栅格介绍)栅格介绍

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#名词解释)名词解释

CSS 网格布局(Grid Layout) 是CSS中最强大的布局系统。 这是一个二维系统，这意味着它可以同时处理列和行。

栅格系统与FLEX弹性布局有相似之处理，都是由父容器包含多个项目元素的使用。

![image-20190829232951627](https://houdunren.gitee.io/note/assets/img/image-20190829232951627.f7b99ef2.png)

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#兼容性)兼容性

下面是栅格系统兼容性数据，所以在根据项目使用的场景决定是否使用栅格布局。

![1.png](https://houdunren.gitee.io/note/assets/img/1240.269752ce.png)

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#声明容器)声明容器

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#块级容器)块级容器

![image-20190829144825641](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAaoAAADxCAYAAACasfN2AAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDLwMNgyKCUmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisO4J/Dnxfv/IxX7Bils89/UuY6lEAV0pqcTKQ/gPE6ckFRSUMDIwpQLZyeUkBiN0BZIsUAR0FZM8BsdMh7A0gdhKEfQSsJiTIGci+AWQLJGckAs1gfAFk6yQhiacjsaH2ggCvj7tCqE9IkGO4p4srAfeSDEpSK0pAtHN+QWVRZnpGiYIjMJRSFTzzkvV0FIwMDC0ZGEBhDlH9+QY4LBnFOBBiBWIMDBYzgIIPEWLxQD9sl2Ng4O9DiKkB/SvgxcBwcF9BYlEi3AGM31iK04yNIGzu7QwMrNP+//8czsDArsnA8Pf6//+/t////3cZAwPzLQaGA98AKQFiLoqX2IEAABDwSURBVHgB7d1JiCTFGgfwmHFfxg3x5AqO7aB4EBRBBZeD4kEPrigiyNxUEFS8uDXihhu44c6IICjiQUEQV1AUBHexbUVtUQ+KIriLS7+O9FVT3VM1RkZ1RWS990touyrzi/yyflHwN6uzclbNLyzBQoAAAQIEOiqwuqPH5bAIECBAgEAjIKi8EQgQIECg0wKCqtPT4+AIECBAQFB5DxAgQIBApwXGGlQ///zzSC/++++/D3/++ee/7uOTTz4Jc3Nz/1qngAABAgQmT2BV26v+4kWCv/zyS/jpp5/Cjz/+GGIYxd/fffdd+Pjjj8NHH30UPvjgg/Duu+8267/++uuw2267Lcp8+umn4auvvmrGxf3En7iPH374IXz55Zfhs88+CzF44j7icscdd4TzzjtvcfygB6effnrYfvvtwwMPPDBos3UECBAgMMECm7c99ksvvTTceOONGw2LYbTrrruGtWvXhiOPPDKsX78+7Lfffk2A9Bdfe+21TaDE+hguO+20U9huu+2akpdffjmce+654YQTTgh77LFH87PXXnv1Dx/4+K+//gpbb731wG1WEiBAgMBkC7QOqvhyDz/88HDPPfc0AbPzzjuHHXbYIaxatSpZ4pxzzgkbNmxYUj87Oxv233//cMUVV4SUcOofHM/u2o7pH+8xAQIECHRXICuoYjAdcMAB2a/qoYceCq+99tqS8fEjwLgcccQRYdttt12y7e677w5HH330knX9T956662wzz779K/ymAABAgT+RwSyguqVV14JJ554YjLBddddtyTY4hnZxRdfvGT8q6++2nykePvtty9ZH58ceOCBG63rrYhnU99880144oknwl133dXqzK63D78JECBAoLsCrYPq77//DjvuuGNYt25d8qvaZpttltTuu+++zceHzz333OL6eDFG/LvVr7/+urguPjjjjDM2GT4zMzNNfQyreGZ18MEHLxnvCQECBAhMtkDroIqBcNRRR4UbbrhhpFcer+w788wzw2GHHRY222yzZl/xQow777yzeRwvTY9X/p122mmL2wc1fPDBB5uAi2Mfe+wxQTUIyToCBAhMsEDroIqXlx9zzDHNS3788cfDpu5pGy+wOOWUU5bwxEvZd9lll8V1Tz/9dNhqq60Wn/cexI8XjzvuuN7Tgb9jaMa/X910001hzz33bELt/PPPD7vvvvvAeisJECBAYPIEWgdV/K5UvIQ8LqeeempYs2ZNWP7RXtwWP8KLobQ8yD788MNw1llnxZJm6Q+t3rrU37feemtzCfwFF1zQ9IkBddVVV4X7778/dRfqCBAgQKDjAq3uTBHDJ57F9F8KHr9kG7/Uu/zn4Ycf3uilx79vxS8Cx79R9Zb4Rd/ffvtto58XXnihVzLw95NPPhmuv/765oxqyy23bM7K7rvvvuY7Wk899dTAMVYSIECAwOQJtDqjevPNN5tX2B9UbV5yvCNFXOKl5L///nvzOP69q/c3qmbFf/8TL64Ytrz//vvhpJNOav7G1X/Z+vHHHx/id7TiFYmvv/56OOSQQ4btwnoCBAgQmBCBVkEVz1gOOuigJWdEbV7nI4880pTHO1a89957zeObb745xDOi5cvbb7898NZJ8W9XJ598cnPV4G233bZ8WIjHGM/cjj322PD8888Lq42ErCBAgMBkCSQH1bfffhviF3WX308vfswWPw5cvvTOvnrr48eG11xzTbjssssWb5kUt8Uv/m6xxRa9ssXf8arA/iWGzy233BIuueSScPbZZ4d777134G2T4r42LNz1In5P69BDDw3xe1nxXoFt7pzR39djAgQIEKgrkBxUL774YnPhRLwBbP/yzDPPhDfeeKN/VfM4Blv/8tJLLzUXV8QLH/qX+N2nQSGyfPyjjz7ahNT09HS4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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding: 200px;
    }

    article {
        width: 400px;
        height: 200px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: 50% 50%;
        grid-template-columns: 25% 25% 25% 25%;
    }

    article div {
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        border: solid 1px #ddd;
    }
</style>

后盾人
<article>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#行级容器)行级容器

![image-20190829144939743](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAd8AAADgCAYAAABCW2yUAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDLwMNgyKCUmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisO4J/Dnxfv/IxX7Bils89/UuY6lEAV0pqcTKQ/gPE6ckFRSUMDIwpQLZyeUkBiN0BZIsUAR0FZM8BsdMh7A0gdhKEfQSsJiTIGci+AWQLJGckAs1gfAFk6yQhiacjsaH2ggCvj7tCqE9IkGO4p4srAfeSDEpSK0pAtHN+QWVRZnpGiYIjMJRSFTzzkvV0FIwMDC0ZGEBhDlH9+QY4LBnFOBBiBWIMDBYzgIIPEWLxQD9sl2Ng4O9DiKkB/SvgxcBwcF9BYlEi3AGM31iK04yNIGzu7QwMrNP+//8czsDArsnA8Pf6//+/t////3cZAwPzLQaGA98AKQFiLoqX2IEAABDtSURBVHgB7d1rqGXzGwfw34z7/ZpXLqNwTOSFIoVyKSMvKPdISt7hFRK5TXLLrdxyN1KK5AWlptyKKOUSchzCSbwgUu4K85/f+nvO7H1mz9n7rNnn2duZz6r5P3uvvdZ61vr8Jt//2nutNUvWrJ2KiQABAgQIEEgTWJrWSSMCBAgQIECgERC+/iIQIECAAIFkAeGbDK4dAQIECBAQvv4OECBAgACBZAHhmwyuHQECBAgQ2HxTJFi9evWmeNiOmQABAgSSBFasWDFnJ2e+c/L4kAABAgQIDF9A+A7f1BYJECBAgMCcAsJ3Th4fEiBAgACB4QsI3+Gb2iIBAgQIEJhTYJO84KqXyLJly3rNNo8AAQIECMwpMD09PefnvT4Uvh0qExMTHe+8HJXA1NRU09p4jGoEuvsaj26PUb8zHqMege7+MR7dc/u/87VzfyNLECBAgACBoQoI36Fy2hgBAgQIEOgvIHz7G1mCAAECBAgMVUD4DpXTxggQIECAQH8B4dvfyBIECBAgQGCoAsJ3qJw2RoAAAQIE+gsI3/5GliBAgAABAkMVEL5D5bQxAgQIECDQX0D49jeyBAECBAgQGKqAJ1y14Lxu+f+fwNRi1U16lZWTC/MEMePR7q+V8WjntlBrGY+Fkm233YUaj9gbZ74hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAgB4RsSKgECBAgQSBIQvknQ2hAgQIAAgRAQviGhEiBAgACBJAHhmwStDQECBAgQCAHhGxIqAQIECBBIEhC+SdDaECBAgACBEBC+IaESIECAAIEkAeGbBK0NAQIECBAIAeEbEioBAgQIEEgSEL5J0NoQIECAAIEQEL4hoRIgQIAAgSQB4ZsErQ0BAgQIEAiBBQnfX3/9Nbbfqv7444/lr7/+6rvu559/Xqanp/suZwECBAgQIDBOApsPujNr1qwpv/32W/nll1/Kzz//XGrA1vrDDz+Uzz77rHz66afl448/Lh988EEz/9tvvy177LHHzOa/+OKL8s033zTr1e3UP3UbP/30U/n666/Ll19+WWqY1m3U6d577y0XXXTRzPq9Xlx11VVl++23L48++mivj80jQIAAAQJjKTBw+F5xxRXltttuW+8gasDuvvvuZf/99y9HH310ufDCC8sBBxzQhGLnwjfddFMTknX5Gpg777xz2W677ZpFXn/99XLBBReUk046qey1117Nn3322adz9Z6v//7777L11lv3/MxMAgQIECAwrgIDh289gCOPPLI8+OCDTWjusssuZccddyxLliwZ+NjOP//8smrVqq7lp6amyoEHHliuvfbaMkjgdq5cz8Lnu07n+m1fr5ycaLuq9RZAwHgsAOpGbNJ4bATeAqxqPBYAdQibnFf41rA96KCDWrd94oknyltvvdW1fv36uU5HHXVU2Xbbbbs+e+CBB8qxxx7bNa/zzXvvvVf23XffzlleEyBAgACBsReYV/i+8cYb5eSTTx74oG6++eausK5nzpdddlnX+m+++WbzdfY999zTNb++Ofjgg9ebFzPqWe93331XnnvuuXL//ffP6ww8tqESIECAAIFRCAwcvv/880/ZaaedyvLlywfez2222aZr2f3226/56vqll16amV8v2Kq/A//+++8z8+qLs88+e85AnZycbJavAVzPgA899NCu9b0hQIAAAQLjKjBw+NaQO+aYY8qtt966UcdSr2g+55xzyhFHHFE222yzZlv1Yq377ruveV1vM6pXPJ955pkzn/dq+NhjjzWhXdd95plnhG8vJPMIECBAYCwFBg7feqvQcccd1xzEs88+W+qtRxua6kVYp59+etfH9bakXXfddWbeiy++WLbaaquZ9/GifrW9YsWKeNuz1v8jUH8Pvv3228vee+/dBPXFF19c9txzz57Lm0mAAAECBMZJYODwrffy1tuB6nTGGWeUHXbYocz+Wrl+Vr8+rkE7O5w/+eSTcu6559ZFmqkziGPeoPWuu+5qbme65JJLmj41dK+//vryyCOPDLoJyxEgQIAAgZEJDPSEqxqo9Wyz87ae+mCL+iCN2X+efPLJ9Q6m/l5cH75Rf/ONqT5c448//ljvzyuvvBKL9KzPP/98ueWWW5oz3y233LI5e3744Yebe4hfeOGFnuuYSYAAAQIExklgoDPfd999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)

```text
display: inline-grid;
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#划分行列)划分行列

栅格有点类似表格，也 `行` 和 `列`。使用 `grid-template-columns` 规则可划分列数，使用 `grid-template-rows` 划分行数。

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#固定宽度)固定宽度

下面是使用固定宽度划分两行三列的的示例，当容器宽度过大时将漏白。

![image-20190829142948605](data:image/png;base64,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)

```text
<style>
	* {
    padding: 0;
    margin: 0;
  }
  body {
    padding: 200px;
  }
  article {
    width: 300px;
    height: 200px;
    border: solid 5px silver;
    display: grid;
    grid-template-rows: 100px 100px;
    grid-template-columns: 100px 100px 100px;
  }
  article div {
    background: blueviolet;
    background-clip: content-box;
    padding: 10px;
    border: solid 1px #ddd;
  }

</style>
...

<article>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#百分比)百分比

可以使用使用百分比自动适就容器。

![image-20190829144703978](data:image/png;base64,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)

```text
display: grid;
grid-template-rows: 50% 50%;
grid-template-columns: 25% 25% 25% 25%;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#重复设置)重复设置

使用 `repeat` 统一设置值，第一个参数为重复数量，第二个参数是重复值

![image-20190829145121820](data:image/png;base64,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)

```text
grid-template-rows: repeat(2, 50%);
grid-template-columns: repeat(2, 50%);
```

可以设置多个值来定义重复，下面定义了四列，以 `100%、20px` 重复排列。

![image-20190829145709624](data:image/png;base64,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)

```text
display: grid;
grid-template-rows: repeat(2, 50%);
grid-template-columns: repeat(2, 100px 50px);
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#自动填充)自动填充

自动填充是根据容器尺寸，自动设置元素尺寸。

![image-20190829150350983](data:image/png;base64,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)

```text
width: 300px;
height: 200px;
display: grid;
grid-template-rows: repeat(auto-fill, 100px);
grid-template-columns: repeat(auto-fill, 100px);
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#比例划分)比例划分

使用 `fr` 单位设置元素在空间中所占的比例，下面按`1份-2份` 分成两组共四列。

#### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#单位组合)单位组合

![image-20190829151215601](data:image/png;base64,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)

```text
width: 300px;
height: 200px;
display: grid;
grid-template-rows: 1fr 2fr;
grid-template-columns: 100px 1fr 2fr;
```

#### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#重复定义)重复定义

![image-20190829150823388](data:image/png;base64,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)

```text
width: 300px;
height: 100px;
display: grid;
grid-template-rows: repeat(2, 1fr);
grid-template-columns: repeat(2, 1fr 2fr);
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#组合定义)组合定义

`grid-tempalte` 是 `grid-template-rows`、`grid-template-columns`、`grid-template-areas` 的三个属性的简写。

下面是使用 `grid-template` 同时声明 `grid-template-rows、grid-template-columns`。

```text
grid-template: 100px 1fr / 50px 1fr
```

下面是使用`grid-template` 定义 `grid-template-areas` ，有关`grid-template-areas`的使用方法会在下面介绍。

![image-20190928152734183](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMsAAAFcCAYAAABm70p8AAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAySDDwMdgySCQmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsiseYuX31V67HS+SSmbJyrqCSemehTAlZJanAyk/wBxenJBUQkDA2MKkK1cXlIAYncA2SJFQEcB2XNA7HQIewOInQRhHwGrCQlyBrJvANkCyRmJQDMYXwDZOklI4ulIbKi9IMDr464Q6hMS5Bju6eJKwL0kg5LUihIQ7ZxfUFmUmZ5RouAIDKVUBc+8ZD0dBSMDQ0sGBlCYQ1R/vgEOS0YxDoRYgRgDg8UMoOBDhFg80A/b5RgY+PsQYmpA/wp4MTAc3FeQWJQIdwDjN5biNGMjCJt7OwMD67T//z+HMzCwazIw/L3+///v7f///13GwMB8i4HhwDcAxllgywZ74XAAAA52SURBVHgB7ZwxkiVHEYZnNsYQHjahM3ABDLkY4OgARIBM7oDDGbDwuAAuF5ANgY2pkMDBHAdjtPWG7K1XU/WqM7dr4nX+3xjb3dVZ1f1/WV+83addPT4/P788ND8vL2+GLhW98d5YKR6NN4/aLr3120ROJAg8Pj66co7qe+O9sfKwdvypfYPepv2csXr93jr1fc4hMCJwa++0m7qsUdfX9218NmZr1HVXsthC9Qu3Y+21LVrPqc979fV9O99bZ/UctQjUm7ZNXu+dXp3dr++Nxuqa8pxSZ2ObLDa5fpF2rL22xeo5ozGr6a1h9zhCYERgtG9sI9u8uq53bzZW5o9qNlnsYXasH1rGZte9mtFYGe/9tM/o1TCmR6DdvDWBds/UtXZvz1hbU1/b8y6y2KI2aNfffff9/4f6f+D/VG9ne4+319u7CnXqBLx/6J/xel3vyy9/dvXbrzKrOPFkYtgy7fVP/vy13ZI6fvHVNw9ffPU7qcyEfXj44Yf/bBiKC/UnzIftzseTVpSPI/VtziEgQOB6z9dOXMlSk6iL6nHOIZCdwGjvb7LUBfV5djDkg0CPQO2AnV9ksYsyqT7vLcIYBFQI1C6U8+2TRQUAOSEQJfChtccWqsdtjCMEFAjUe78+55NFoftkPITAJkttUH1+yFNYBAInI1A7YOebLJbFbpTrj3+m4QcCUgTqPV+7UCBcZGkHpegQFgI7CBRHrj5Zamnq8x1rUQKBNATqvV+fX8mSJi1BILCAwNVXx7Z+bZONcYSAEoGeA9snS++mEhyyQmBEwNzYZBkVMg4BCLwSeCOLWWRHQEFAjYDtfTta/jey2A2OEIDANQFkuebBFQSGBC6y2MeNHYfV3ICAGAFzohy7nyxWIMaFuBDYCPQc6MqyzeDf4H9CwZkIgfFfiJzIIsKHmBDYQQBZdkCiBAKFALKwDyCwk0D374btnEsZBKQIbJ8s9qd/O0pRICwEOgTMBTtusrS1VtCOcw2B7ARGe38oS3Yg5IOAlwCyeIlRL0sAWWRbT3AvAWTxEqNelgCyyLae4F4CyOIlRr0sAWSRbT3BvQSQxUuMelkCyCLbeoJ7CSCLlxj1sgSQRbb1BPcSQBYvMeplCSCLbOsJ7iWALF5i1MsSQBbZ1hPcSwBZvMSolyWALLKtJ7iXALJ4iVEvSwBZZFtPcC8BZPESo16WALLItp7gXgLI4iVGvSwBZJFtPcG9BJDFS4x6WQLIItt6gnsJIIuXGPWyBJBFtvUE9xJAFi8x6mUJIIts6wnuJYAsXmLUyxJAFtnWE9xLAFm8xKiXJYAssq0nuJcAsniJUS9LAFlkW09wLwFk8RKjXpYAssi2nuBeAsjiJUa9LAFkkW09wb0EkMVLjHpZAsgi23qCewkgi5cY9bIEkEW29QT3EkAWLzHqZQkgi2zrCe4lgCxeYtTLEkAW2dYT3EsAWbzEqJclgCyyrSe4lwCyeIlRL0sAWWRbT3AvAWTxEqNelgCyyLae4F4CyOIlRr0sAWSRbT3BvQSQxUuMelkCyCLbeoJ7CSCLlxj1sgSQRbb1BPcSQBYvMeplCSCLbOsJ7iWALF5i1MsSQBbZ1hPcSwBZvMSolyWALLKtJ7iXALJ4iVEvSwBZZFtPcC8BZPESo16WALLItp7gXgLI4iVGvSwBZJFtPcG9BJDFS4x6WQLIItt6gnsJIIuXGPWyBJBFtvUE9xJAFi8x6mUJIIts6wnuJYAsXmLUyxJAFtnWE9xLAFm8xKiXJYAssq0nuJcAsniJUS9LAFlkW09wL4Gn2YSf/uHbWUnK+//4678e/v6bv6XMNgv127/8clYieZ9PFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEECWCDXmSBJAFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEECWCDXmSBJAFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEECWCDXmSBJAFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEECWCDXmSBJAFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEECWCDXmSBJAFsm2EzpCAFki1JgjSQBZJNtO6AgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEJjI8hhZkzkQODGB8Z6fyPJy4tC8OgQiBMZ7fiJL5GHMgUBOAsiSs6+kWkAAWRZAZcmcBJAlZ19JtYAAsiyAypI5CUxkGX+NlhMHqSAw3vMTWcZfowEVAjkJjPf8RJacOEgFgQgBZIlQY44kAWSRbDuhIwSQJUKNOZIEkEWy7YSOEJjIMv4aLfIw5kDg/gmM9/xElvHXaPcfmjeEQITAeM9PZIk8jDkQyEkAWXL2lVQLCCDLAqgsmZMAsuTsK6kWEECWBVBZMieBiSzjr9Fy4iAVBMZ7fiLL+Gs0oEIgJ4Hxnp/IkhMHqSAQIYAsEWrMkSSALJJtJ3SEALJEqDFHkgCySLad0BECE1nGX6NFHsYcCNw/gfGen8gy/hrt/kPzhhCIEBjv+YkskYcxBwI5CSBLzr6SagEBZFkAlSVzEkCWnH0l1QICyLIAKkvmJIAsOftKqgUEkGUBVJbMSQBZcvaVVAsIIMsCqCyZkwCy5OwrqRYQQJYFUFkyJwFkydlXUi0ggCwLoLJkTgLIkrOvpFpAAFkWQGXJnASQJWdfSbWAALIsgMqSOQkgS86+kmoBAWRZAJUlcxJAlpx9JdUCAsiyACpL5iSALDn7SqoFBJBlAVSWzEkAWXL2lVQLCCDLAqgsmZMAsuTsK6kWEECWBVBZMicBZMnZV1ItIIAsC6CyZE4CyJKzr6RaQABZFkBlyZwEkCVnX0m1gACyLIDKkjkJPM1i/emf385KUt7/9//++/Dwq5TRCBUkgCxBcJmn/fHh15njhbPx27AwOiaqEUAWtY6TN0wAWcLomKhGAFnUOk7eMAFkCaNjohoBZFHrOHnDBJAljI6JagSQRa3j5A0TQJYwOiaqEUAWtY6TN0wAWcLomKhGAFnUOk7eMAFkCaNjohoBZFHrOHnDBJAljI6JagSQRa3j5A0TQJYwOiaqEUAWtY6TN0wAWcLomKhGAFnUOk7eMAFkCaNjohoBZFHrOHnDBJAljI6JagSQRa3j5A0TQJYwOiaqEUAWtY6TN0xgIstjeGEmQuCcBMZ7fiLLOePy1hBYQQBZVlBlzZQEkCVlWwm1ggCyrKDKmikJIEvKthJqBQFkWUGVNVMSQJaUbSXUCgLIsoIqa6YkgCwp20qoFQSQZQVV1kxJAFlStpVQKwggywqqrJmSALKkbCuhVhCYyPKy4pmsCYE7JjDe8xNZ7jgTrwaBdyaALO8MnMedlwCynLd3vPk7E0CWdwbO485LAFnO2zve/J0JTGQZ/3vkd35PHgeBdyIw3vMTWd7p/XgMBE5AYCLL+DvnE2TjFSEQIDDe8xNZAs9iCgSSEkCWpI0l1vEEkOV4pqyYlACyJG0ssY4ngCzHM2XFpASQJWljiXU8AWQ5nikrJiWALEkbS6zjCUxkGf+n/+NfhRUhcA8Exnt+Iss9vDzvAIH7IIAs99EH3uIEBJDlBE3iFe+DALLcRx94ixMQQJYTNIlXvA8CyHIffeAtTkAAWU7QJF7xPghMZBn/Q5j7eH3eAgJHExjv+YksR78I60HgvAQmsoz/a+Z5I/PmELhFYLznJ7KMP5JuPY57EDgvgfGen8hy3si8OQSOJoAsRxNlvbQEkCVtawl2NAFkOZoo66UlgCxpW0uwowkgy9FEWS8tAWRJ21qCHU0AWY4mynppCSBL2tYS7GgCyHI0UdZLSwBZ0raWYEcTQJajibJeWgITWcZ/AzMtEYKJExjv+aEsj4/jSeI0iZ+cwGjvb7JYgR2T8yAeBKYEzAU7frCT6UwKICBOYPtkEedAfAhMCSDLFBEFEHglgCzsBAjsJIAsO0FRBoGuLPyhn42hTqDnwEUWu2FHdVDkh4ARMCfKsfvJYoUcIQCBTwSQ5RMLziBwk8AbWeqPnZszuQmBpARGDryRJWl+YkHgswlssphNn70iC0AgGQFzo/t3w+xmsszEgcBuAj0Htk+W3atQCAFRAley1DbV56JsiC1KoN779flFlnpAlA+xIXCTQHHk6pOlVNfi8I8lb/LjZkIC9Z6vXShRN1nqG/V5Qh5EgsCUQO2AnW+yTGdTAAFxAldfHZtBhUl9Ls6I+GIE6r1fn/PJIrYRiBsncJGltqc+jy/LTAicn0DtQjnfPlnaG+ePSgIIxAn0fNhkaZeti9t7XEMgM4HR3r+S5W0R/1fKzJuCbD0C13u+duKpXLy8vGyz2uvf//wX2z1OIKBEoBal5H58fn6+mFILU254r3tzRmNlvPfTPrNXw5gegXbT3iLQq90z1tb0rp9GDy7F9ebtXZe5bc1ozJ5T19uYHdsXtHGOEBgRuLVnevf2jPVqyvM3WUpBu5Hbsfa6LDAaK/fKT2/N1zvXv7Z113e5UidQ9tmen1t1vXvtWHtdnmljmyw22G7aUliP2cTZmAWz+nJdz7H7dqzrbIwjBPYQmO2d3v3I2JUs5cXKIu2mtoXr8VtjZZ26tlyXH5vzenX9a6/+uoIrZQK39k6Py6i+N94bK2u242++DauL2g1cJvfGypzReLlnP22NjZdj+2L1Pc4hcIvAnr0zqumN98bK8y+fLOVmbyP3xm2htt7Gy6LtvTJWfuqa15HXX0f1dQ3nEBjtnxGZW/Wje7fGt9+GlaLepr01Xl5yNMcC9O7bPTuOXtDuc4TAXgKzvXTr/uiejf8IMpAF1+R6q+8AAAAASUVORK5CYII=)

```text
grid-template: "header . ."
            ". main ."
            "footer footer .";
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#minmax)minmax

使用 `minmax` 方法可以设置取值范围，下列在行高在 `最小100px ~ 最大1fr` 间取值。

![image-20190829151644654](data:image/png;base64,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)

```text
width: 300px;
height: 300px;
display: grid;
grid-template-rows: 100px minmax(100px, 1fr);
grid-template-columns: 100px 1fr;
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#间距定义)间距定义

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#行间距)行间距

使用 `row-gap` 设置行间距。

![image-20190829152837070](data:image/png;base64,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)

```text
width: 300px;
height: 200px;
display: grid;
grid-template-rows: repeat(2, 1fr);
grid-template-columns: repeat(3, 1fr);
row-gap: 30px;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#列间距)列间距

使用 `column-gap` 定义列间距。

![image-20190829152940142](data:image/png;base64,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)

```text
width: 300px;
height: 200px;
display: grid;
grid-template-rows: repeat(2, 1fr);
grid-template-columns: repeat(3, 1fr);
column-gap: 20px;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#组合定义-2)组合定义

使用 `gap` 规则可以一次定义行、列间距，如果间距一样可以只设置一个值。

**设置行列间距为20px与10px**

![image-20190829153208166](data:image/png;base64,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)

```text
width: 300px;
height: 200px;
display: grid;
grid-template-rows: repeat(2, 1fr);
grid-template-columns: repeat(3, 1fr);
gap: 20px 10px;
```

**统一设置行列间距为20px**

![image-20190829153241158](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAUEAAADeCAYAAACjSbITAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDLwMNgyKCUmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisO4J/Dnxfv/IxX7Bils89/UuY6lEAV0pqcTKQ/gPE6ckFRSUMDIwpQLZyeUkBiN0BZIsUAR0FZM8BsdMh7A0gdhKEfQSsJiTIGci+AWQLJGckAs1gfAFk6yQhiacjsaH2ggCvj7tCqE9IkGO4p4srAfeSDEpSK0pAtHN+QWVRZnpGiYIjMJRSFTzzkvV0FIwMDC0ZGEBhDlH9+QY4LBnFOBBiBWIMDBYzgIIPEWLxQD9sl2Ng4O9DiKkB/SvgxcBwcF9BYlEi3AGM31iK04yNIGzu7QwMrNP+//8czsDArsnA8Pf6//+/t////3cZAwPzLQaGA98AKQFiLoqX2IEAAAlHSURBVHgB7d1BahxJEAVQe/BBtGt8Eh/L6Fg6iehd38RjGYM3vcgS9YmIrKfVTFOKjHy/+UiYRl9//f764osAAQIXFfjvovd2bQIECPwRUILeCAQIXFpACV46fpcnQEAJeg8QIHBpASV46fhdngCBb88I3t7enr3sNQIECIwV+PHjx9Pd/ST4lMWLBAhcRUAJXiVp9yRA4KmAEnzK4kUCBK4ioASvkrR7EiDwVODpP4w8e/Ll5eXZy147QeB2u50w5d+I+/3+73/812kCcjqNMj7o8Xgsn7Fcgh8Tz34TLG+58YOpwpLVuW8aOZ3rmZx2NCu/DifTMJsAgfYCSrB9RBYkQCApoASTumYTINBeQAm2j8iCBAgkBZRgUtdsAgTaCyjB9hFZkACBpIASTOqaTYBAewEl2D4iCxIgkBRQgkldswkQaC9w6BMjq7f5+d3Htl7fz/0o3Kr90eeunpWcjr5j6p5PZeUnwbpMnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAMBJdggBCsQIFAnoATr7J1MgEADASXYIAQrECBQJ6AE6+ydTIBAAwEl2CAEKxAgUCegBOvsnUyAQAOBb4kdXt9vibFmBgRkFUANjJRTAPXvSD8J5mxNJkBggIASHBCSFQkQyAkowZytyQQIDBBQggNCsiIBAjkBJZizNZkAgQECSnBASFYkQCAnoARztiYTIDBAQAkOCMmKBAjkBJRgztZkAgQGCBz6xMj9fh9wJSt+CMhqxvtATvU5LZfg7eajcPVxrW0gqzWn6qfklEvg8XgsD/fr8DKVBwkQ2FFACe6YqjsRILAsoASXqTxIgMCOAkpwx1TdiQCBZQEluEzlQQIEdhRQgjum6k4ECCwLKMFlKg8SILCjgBLcMVV3IkBgWUAJLlN5kACBHQWU4I6puhMBAssCSnCZyoMECOwooAR3TNWdCBBYFlCCy1QeJEBgRwEluGOq7kSAwLKAElym8iABAjsKKMEdU3UnAgSWBZTgMpUHCRDYUUAJ7piqOxEgsCygBJepPEiAwI4Cy39jxB+EycV/9t+akFUmKzllXKunLpfgx6JnvwmqL9/h/FRhyercdOV0rmdy2tGs/DqcTMNsAgTaCyjB9hFZkACBpIASTOqaTYBAewEl2D4iCxIgkBRQgkldswkQaC+gBNtHZEECBJICSjCpazYBAu0FlGD7iCxIgEBSQAkmdc0mQKC9wKFPjKze5uf3++qj2z73+n4bcberZyWnEW/TP0umsvKT4Jz3gE0JEAgIKMEAqpEECMwRUIJzsrIpAQIBASUYQDWSAIE5AkpwTlY2JUAgIKAEA6hGEiAwR0AJzsnKpgQIBASUYADVSAIE5ggowTlZ2ZQAgYCAEgygGkmAwBwBJTgnK5sSIBAQUIIBVCMJEJgjoATnZGVTAgQCAkowgGokAQJzBJTgnKxsSoBAQEAJBlCNJEBgjoASnJOVTQkQCAgowQCqkQQIzBFQgnOysikBAgEBJRhANZIAgTkCSnBOVjYlQCAgoAQDqEYSIDBHQAnOycqmBAgEBJRgANVIAgTmCCjBOVnZlACBgIASDKAaSYDAHAElOCcrmxIgEBBQggFUIwkQmCOgBOdkZVMCBAICSjCAaiQBAnMElOCcrGxKgEBAQAkGUI0kQGCOgBKck5VNCRAICCjBAKqRBAjMEVCCc7KyKQECAQElGEA1kgCBOQJKcE5WNiVAICCgBAOoRhIgMEdACc7JyqYECAQElGAA1UgCBOYIKME5WdmUAIGAgBIMoBpJgMAcASU4JyubEiAQEFCCAVQjCRCYI6AE52RlUwIEAgJKMIBqJAECcwSU4JysbEqAQEBACQZQjSRAYI6AEpyTlU0JEAgIKMEAqpEECMwRUIJzsrIpAQIBASUYQDWSAIE5AkpwTlY2JUAgIKAEA6hGEiAwR0AJzsnKpgQIBASUYADVSAIE5ggowTlZ2ZQAgYCAEgygGkmAwBwBJTgnK5sSIBAQUIIBVCMJEJgjoATnZGVTAgQCAkowgGokAQJzBJTgnKxsSoBAQEAJBlCNJEBgjoASnJOVTQkQCAgowQCqkQQIzBFQgnOysikBAgGBb4GZX17fb4mxZgYEZBVADYyUUwD170g/CeZsTSZAYICAEhwQkhUJEMgJKMGcrckECAwQUIIDQrIiAQI5ASWYszWZAIEBAkpwQEhWJEAgJ6AEc7YmEyAwQEAJDgjJigQI5ASUYM7WZAIEBggc+sTI/X4fcCUrfgjIasb7QE71OS2X4OPxqN920w3YzghWTjNyOrqlX4ePinmeAIGtBJTgVnG6DAECRwWU4FExzxMgsJWAEtwqTpchQOCowNdfv7+OfpPnCRAgsIuAnwR3SdI9CBD4lIAS/BSbbyJAYBcBJbhLku5BgMCnBJTgp9h8EwECuwgowV2SdA8CBD4l8D98I2Zz3zGNHAAAAABJRU5ErkJggg==)

```text
gap: 20px;
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#栅格命名)栅格命名

栅格线可以使用命名与编号找到，方便控制指定栅格，或将内容添加到指定栅格中。

![image-20190829235441431](https://houdunren.gitee.io/note/assets/img/image-20190829235441431.1a1f67fe.png)

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#独立命名)独立命名

可以为每个栅格独立命名来进行调用。

![image-20190830154931726](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-top: 50px;
    }

    article {
        margin: 0 auto;
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: [r1-start] 100px [r1-end r2-start] 100px [r2-end r3-start] 100px [r3-end];

        grid-template-columns: [c1-start] 100px [c1-end c2-start] 100px [c2-start c3-start] 100px [c3-end];
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
        color: white;
    }

    div:first-child {
        grid-row-start: r2-start;
        grid-column-start: c1-end;
        grid-row-end: r2-end;
        grid-column-end: c3-start;
    }
</style>
...

<article>
	<div>后盾人</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#自动命名)自动命名

对于重复设置的栅格系统会自动命名，使用时使用 `c 1、c 2` 的方式定位栅格。

![image-20190831132454288](https://houdunren.gitee.io/note/assets/img/image-20190831132454288.0d5e0c5f.png)

```text
<style>
    article {
        margin: 0 auto;
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: repeat(3, [r-start] 100px [r-end]);
        grid-template-columns: repeat(3, [c-start] 100px [c-end]);
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
        color: white;
    }

    div:first-child {
        grid-row-start: r-start 2;
        grid-column-start: c-start 2;
        grid-row-end: r-start 2;
        grid-column-end: c-end 2;
    }
</style>
...

<article>
	<div>houdunren</div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#元素定位)元素定位

| 选项              | 说明         |
| ----------------- | ------------ |
| grid-row-start    | 行开始栅格线 |
| grid-row-end      | 行结束栅格线 |
| grid-column-start | 列开始栅格线 |
| grid-column-end   | 列结束栅格线 |

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#根据栅格线)根据栅格线

通过设置具体的第几条栅格线来设置区域位置，设置的数值可以是正数和负数。

![image-20190831131522612](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAAGNCAYAAAAGkJbSAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDPwM3AyaCdmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisxAt1NgqTxWeGzcnmfKXoUoWpHgVwpaQWJwPpP0CcllxQVMLAwJgCZCuXlxSA2B1AtkgR0FFA9hwQOx3C3gBiJ0HYR8BqQoKcgewbQLZAckYi0AzGF0C2ThKSeDoSG2ovCPC4uPr4KIQamRiaexBwLumgJLWiBEQ75xdUFmWmZ5QoOAJDKVXBMy9ZT0fByMDQkoEBFOYQ1Z9vgMOSUYwDIVYgxsBg6cLAwLwYIZYkxcCwHeh+SU6EmMpyBgb+CAaGbQ0FiUWJcAcwfmMpTjM2grC5tzMwsE77//9zOAMDuyYDw9/r////3v7//99lQPNvMTAc+AYAR0Zc4r2qW8AAABn9SURBVHgB7dx7jKZXXQfwM3tvd7vbbrcXerEsUCwXuRSictFaIC6WkhgVuSoxBjVeaOKNPwypNQQ1RiN/mHAxiESEKJYAobgpWBArKFCgFFjb0Ja2dNtuu9du977jc57lncy8M7vs2c70Ob85n9csO/O+73me3/l863znve3EZHdJLgQIECBA4CQFlpzk/dyNAAECBAj0AorDfwgECBAgUCSgOIq43JkAAQIEFIf/BggQIECgSGDZXPfevHnzXFe7jgABAgQaE9i0adOsHXvEMYvEFQQIECBwIgHFcSIdtxEgQIDALAHFMYvEFQQIECBwIgHFcSIdtxEgQIDALAHFMYvEFQQIECBwIoE531V1vAVzvbp+vPu6ngABAgTiCJS8m9Yjjji5mpQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiO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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 200px;
        padding-top: 200px;
    }

    article {
        border: solid 5px blueviolet;
        width: 400px;
        height: 400px;
        display: grid;
        grid-template-rows: repeat(4, 1fr);
        grid-template-columns: repeat(4, 1fr);
    }

    article div {
        background: blueviolet;
        grid-row-start: 2;
        grid-row-end: 4;
        grid-column-start: 2;
        grid-column-end: 4;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 35px;
        color: white;
    }
</style>
...

<article>
    <div>后盾人</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#根据栅格命名)根据栅格命名

![image-20190831131522612](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAAGNCAYAAAAGkJbSAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDPwM3AyaCdmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisxAt1NgqTxWeGzcnmfKXoUoWpHgVwpaQWJwPpP0CcllxQVMLAwJgCZCuXlxSA2B1AtkgR0FFA9hwQOx3C3gBiJ0HYR8BqQoKcgewbQLZAckYi0AzGF0C2ThKSeDoSG2ovCPC4uPr4KIQamRiaexBwLumgJLWiBEQ75xdUFmWmZ5QoOAJDKVXBMy9ZT0fByMDQkoEBFOYQ1Z9vgMOSUYwDIVYgxsBg6cLAwLwYIZYkxcCwHeh+SU6EmMpyBgb+CAaGbQ0FiUWJcAcwfmMpTjM2grC5tzMwsE77//9zOAMDuyYDw9/r////3v7//99lQPNvMTAc+AYAR0Zc4r2qW8AAABn9SURBVHgB7dx7jKZXXQfwM3tvd7vbbrcXerEsUCwXuRSictFaIC6WkhgVuSoxBjVeaOKNPwypNQQ1RiN/mHAxiESEKJYAobgpWBArKFCgFFjb0Ja2dNtuu9du977jc57lncy8M7vs2c70Ob85n9csO/O+73me3/l863znve3EZHdJLgQIECBA4CQFlpzk/dyNAAECBAj0AorDfwgECBAgUCSgOIq43JkAAQIEFIf/BggQIECgSGDZXPfevHnzXFe7jgABAgQaE9i0adOsHXvEMYvEFQQIECBwIgHFcSIdtxEgQIDALAHFMYvEFQQIECBwIgHFcSIdtxEgQIDALAHFMYvEFQQIECBwIoE531V1vAVzvbp+vPu6ngABAgTiCJS8m9Yjjji5mpQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiOKmIwBAECBOIIKI44WZmUAAECVQgojipiMAQBAgTiCCiOOFmZlAABAlUIKI4qYjAEAQIE4ggojjhZmZQAAQJVCCiO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)

```text
<style>
    article {
        margin: 0 auto;
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: [r1-start] 100px [r1-end r2-start] 100px [r2-end r3-start] 100px [r3-end];
        grid-template-columns: [c1-start] 100px [c1-end c2-start] 100px [c2-start c3-start] 100px [c3-end];

    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
    }

    div:first-child {
        grid-row-start: r1-end;
        grid-column-start: c2-start;
        grid-row-end: r3-start;
        grid-column-end: c3-start;
    }
</style>
...

<article>
	<div>houdunren</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#根据自动命名)根据自动命名

对于重复设置的栅格系统会自动命名，使用时使用 `c 1、c 2` 的方式定位栅格。

![image-20190831132454288](https://houdunren.gitee.io/note/assets/img/image-20190831132454288.0d5e0c5f.png)

```text
<style>
    article {
        margin: 0 auto;
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: repeat(3, [r-start] 100px [r-end]);
        grid-template-columns: repeat(3, [c-start] 100px [c-end]);
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
        color: white;
    }

    div:first-child {
        grid-row-start: r-start 2;
        grid-column-start: c-start 2;
        grid-row-end: r-start 2;
        grid-column-end: c-end 2;
    }
</style>
...

<article>
	<div>houdunren</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#根据偏移量)根据偏移量

使用 `span` 可以设置移动单元格数量，数值只能为正数。

- [ ] 设置在 `grid-*-end` 表示 `grid-*-end` 栅格线是从 `grid-*-start` 移动几个单元格
- [ ] 设置在 `grid-*-start` 表示 `grid-*-start` 栅格线是从 `grid-*-end` 移动几个单元格

为 `grid-*-end` 设置栅格线

![image-20190831171434085](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY0AAAGQCAYAAABS7zyUAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAwSDPwM3AyaCdmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisxAt1NgqTxWeGzcnmfKXoUoWpHgVwpaQWJwPpP0CcllxQVMLAwJgCZCuXlxSA2B1AtkgR0FFA9hwQOx3C3gBiJ0HYR8BqQoKcgewbQLZAckYi0AzGF0C2ThKSeDoSG2ovCPC4uPr4KIQamRiaexBwLumgJLWiBEQ75xdUFmWmZ5QoOAJDKVXBMy9ZT0fByMDQkoEBFOYQ1Z9vgMOSUYwDIVYgxsBg6cLAwLwYIZYkxcCwHeh+SU6EmMpyBgb+CAaGbQ0FiUWJcAcwfmMpTjM2grC5tzMwsE77//9zOAMDuyYDw9/r////3v7//99lQPNvMTAc+AYAR0Zc4r2qW8AAABErSURBVHgB7dxNjpxFEARQQL4IO27iYyGONTdhx1H4W0IjDVJnfhHp5x2jVlXUC4tgjDXf//7nr+/8IkCAAAECnxD44ROf8RECBAgQIPC3gNHwG4EAAQIEPi1gND5N5YMECBAgYDT8HiBAgACBTwsYjU9T+SABAgQIfPknwcfHxz+/5J8JECBA4BsT+Pr168sX+07jJYsvEiBAgMArAaPxSsXXCBAgQOClgNF4yeKLBAgQIPBKwGi8UvE1AgQIEHgpYDResvgiAQIECLwS+Nffnnr1ob++9l//J/2/Pu/rBAgQIJAv8H//xqzvNPI7lZAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpBCBAgkC9gNPI7kpAAAQIxAkYjpgpB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)

```text
<style>
    article {
        margin: 0 auto;
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: repeat(3, 1fr);
        grid-template-columns: repeat(3, 1fr);
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
        color: white;
        font-size: 25px;
    }

    div:first-child {
        grid-row-start: 2;
        grid-column-start: 2;
        grid-row-end: span 1;
        grid-column-end: span 1;
    }
</style>
...

<article>
	<div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#简写模式)简写模式

可以使用 `grid-row` 设置行开始栅格线，使用 `grid-column` 设置结束栅格线。

上例中的居中对齐元素，可以使用以下简写的方式声明（推荐）。

```text
grid-row: 2/4;
grid-column: 2/4;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#grid-area)grid-area

`grid-area`更加简洁是同时对 `grid-row` 与 `grid-column` 属性的组合声明。

语法结构如下：

```text
grid-row-start/grid-column-start/grid-row-end/grid-column-end。
```

下面是将元素定位在中间的示例。

![image-20190928153819574](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        width: 100vw;
        height: 100vh;
        display: grid;
        grid-template: repeat(3, 1fr)/repeat(3, 1fr);
    }

    header {
        grid-area: 2/2/3/3;
        background: #e67e22;
    }
</style>

<body>
    <header></header>
</body>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#bootstrap)BOOTSTRAP

下面是bootstrap栅格系统的开发，根据指定的样式自动设置栅格大小。

![image-20190830124033140](https://houdunren.gitee.io/note/assets/img/image-20190830124033140.86f72379.png)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-top: 200px;
    }

    .container {
        margin: 0 auto;
        border: solid 5px silver;
        width: 1020px;
        height: 320px;
    }

    .row {
        display: grid;
        grid-template-columns: repeat(12, 1fr);
        gap: 10px 10px;
    }

    div {
        background: blueviolet;
        height: 100px;
        background-clip: content-box;
        padding: 10px;
        box-sizing: border-box;
        border: solid 1px blueviolet;
        font-size: 35px;
    }

    .c-1 {
        grid-column: span 1;
    }

    .c-2 {
        grid-column-end: span 2;
    }

    .c-3 {
        grid-column-end: span 3;
    }

    .c-4 {
        grid-column-end: span 4;
    }

    .c-5 {
        grid-column-end: span 5;
    }

    .c-6 {
        grid-column-end: span 6;
    }

    .c-7 {
        grid-column-end: span 7;
    }

    .blue {
        background: #904FA9;
    }

    .green {
        background: #EEBC31;
    }
</style>
...

<article class="container">
    <section class="row">
        <div class="c-1 blue">1</div>
        <div class="c-3 blue">3</div>
        <div class="c-6 blue">6</div>
        <div class="c-2 blue">2</div>
    </section>
    <section class="row">
        <div class="c-4 green">4</div>
        <div class="c-4 green">4</div>
        <div class="c-4 green">4</div>
    </section>
</article>
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#元素附加)元素附加

通过 `grid-area` 属性可以将元素放在指定区域中。`grid-area`由`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end` 的简写模式。

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#编号附加)编号附加

下例中将元素放在容器的中心位置中的栅格中。

![image-20190830152122321](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVIAAAFWCAYAAAA7RBX5AAAEGWlDQ1BrQ0dDb2xvclNwYWNlR2VuZXJpY1JHQgAAOI2NVV1oHFUUPrtzZyMkzlNsNIV0qD8NJQ2TVjShtLp/3d02bpZJNtoi6GT27s6Yyc44M7v9oU9FUHwx6psUxL+3gCAo9Q/bPrQvlQol2tQgKD60+INQ6Ium65k7M5lpurHeZe58853vnnvuuWfvBei5qliWkRQBFpquLRcy4nOHj4g9K5CEh6AXBqFXUR0rXalMAjZPC3e1W99Dwntf2dXd/p+tt0YdFSBxH2Kz5qgLiI8B8KdVy3YBevqRHz/qWh72Yui3MUDEL3q44WPXw3M+fo1pZuQs4tOIBVVTaoiXEI/MxfhGDPsxsNZfoE1q66ro5aJim3XdoLFw72H+n23BaIXzbcOnz5mfPoTvYVz7KzUl5+FRxEuqkp9G/Ajia219thzg25abkRE/BpDc3pqvphHvRFys2weqvp+krbWKIX7nhDbzLOItiM8358pTwdirqpPFnMF2xLc1WvLyOwTAibpbmvHHcvttU57y5+XqNZrLe3lE/Pq8eUj2fXKfOe3pfOjzhJYtB/yll5SDFcSDiH+hRkH25+L+sdxKEAMZahrlSX8ukqMOWy/jXW2m6M9LDBc31B9LFuv6gVKg/0Szi3KAr1kGq1GMjU/aLbnq6/lRxc4XfJ98hTargX++DbMJBSiYMIe9Ck1YAxFkKEAG3xbYaKmDDgYyFK0UGYpfoWYXG+fAPPI6tJnNwb7ClP7IyF+D+bjOtCpkhz6CFrIa/I6sFtNl8auFXGMTP34sNwI/JhkgEtmDz14ySfaRcTIBInmKPE32kxyyE2Tv+thKbEVePDfW/byMM1Kmm0XdObS7oGD/MypMXFPXrCwOtoYjyyn7BV29/MZfsVzpLDdRtuIZnbpXzvlf+ev8MvYr/Gqk4H/kV/G3csdazLuyTMPsbFhzd1UabQbjFvDRmcWJxR3zcfHkVw9GfpbJmeev9F08WW8uDkaslwX6avlWGU6NRKz0g/SHtCy9J30o/ca9zX3Kfc19zn3BXQKRO8ud477hLnAfc1/G9mrzGlrfexZ5GLdn6ZZrrEohI2wVHhZywjbhUWEy8icMCGNCUdiBlq3r+xafL549HQ5jH+an+1y+LlYBifuxAvRN/lVVVOlwlCkdVm9NOL5BE4wkQ2SMlDZU97hX86EilU/lUmkQUztTE6mx1EEPh7OmdqBtAvv8HdWpbrJS6tJj3n0CWdM6busNzRV3S9KTYhqvNiqWmuroiKgYhshMjmhTh9ptWhsF7970j/SbMrsPE1suR5z7DMC+P/Hs+y7ijrQAlhyAgccjbhjPygfeBTjzhNqy28EdkUh8C+DU9+z2v/oyeH791OncxHOs5y2AtTc7nb/f73TWPkD/qwBnjX8BoJ98VQNcC+8AABjNSURBVHgB7d0JjCxV1Qfw++CB7G4sCgoquMQFRHGN4hY1IokENUHiEv0E/YxLXEAl0Yj6aYIajWhEURRxi0vAiIK7GBGNGjdEjSiuqKiAkKiA0F+dkurXM294zky/uX36zq+Sx/RUV/U993d6/lNdVe+xYdQtxUKAAAECqxbYZtV72pEAAQIEegFB6o1AgACBKQUE6ZSAdidAgIAg9R4gQIDAlAKCdEpAuxMgQECQeg8QIEBgSgFBOiWg3QkQILBxKYKzzz57qdXWESBAYN0LHH744ZsZOCLdjMQKAgQIrExAkK7My9YECBDYTECQbkZiBQECBFYmsOQ50sUvsdQ5gcXb+J4AAQItCiznmpEj0hY7b04ECFQVEKRVuQ1GgECLAoK0xa6aEwECVQUEaVVugxEg0KKAIG2xq+ZEgEBVAUFaldtgBAi0KCBIW+yqOREgUFVAkFblNhgBAi0KCNIWu2pOBAhUFRCkVbkNRoBAiwKCtMWumhMBAlUFBGlVboMRINCigCBtsavmRIBAVQFBWpXbYAQItCggSFvsqjkRIFBVQJBW5TYYAQItCgjSFrtqTgQIVBUQpFW5DUaAQIsCgrTFrpoTAQJVBQRpVW6DESDQooAgbbGr5kSAQFUBQVqV22AECLQoIEhb7Ko5ESBQVUCQVuU2GAECLQoI0ha7ak4ECFQVEKRVuQ1GgECLAoK0xa6aEwECVQUEaVVugxEg0KKAIG2xq+ZEgEBVAUFaldtgBAi0KCBIW+yqOREgUFVAkFblNhgBAi0KCNIWu2pOBAhUFRCkVbkNRoBAiwKCtMWumhMBAlUFBGlVboMRINCigCBtsavmRIBAVQFBWpXbYAQItCggSFvsqjkRIFBVQJBW5TYYAQItCgjSFrtqTgQIVBUQpFW5DUaAQIsCgrTFrpoTAQJVBQRpVW6DESDQooAgbbGr5kSAQFUBQVqV22AECLQoIEhb7Ko5ESBQVUCQVuU2GAECLQoI0ha7ak4ECFQVEKRVuQ1GgECLAoK0xa6aEwECVQUEaVVugxEg0KKAIG2xq+ZEgEBVAUFaldtgBAi0KCBIW+yqOREgUFVAkFblNhgBAi0KCNIWu2pOBAhUFRCkVbkNRoBAiwKCtMWumhMBAlUFBGlVboMRINCigCBtsavmRIBAVQFBWpXbYAQItCggSFvsqjkRIFBVQJBW5TYYAQItCgjSFrtqTgQIVBUQpFW5DUaAQIsCgrTFrpoTAQJVBQRpVW6DESDQooAgbbGr5kSAQFUBQVqV22AECLQoIEhb7Ko5ESBQVUCQVuU2GAECLQoI0ha7ak4ECFQVEKRVuQ1GgECLAoK0xa6aEwECVQUEaVVugxEg0KKAIG2xq+ZEgEBVAUFaldtgBAi0KCBIW+yqOREgUFVgY9XR1ulgx2+4eJ3O3LQzCJw0OiBDGU3XIEgrtdebuRK0YRYI+CW+gGPNvvHRfs1ovTABAutFQJCul06bJwECayYgSNeM1gsTILBeBATpeum0eRIgsGYCgnTNaL0wAQLrRUCQrpdOmycBAmsmIEjXjNYLEyCwXgTcR5qk0+73S9KIOSvD/ck5GuaINEcfVEGAwBwLCNI5bp7SCRDIISBIc/RBFQQIzLGAIJ3j5imdAIEcAoI0Rx9UQYDAHAsI0jluntIJEMghIEhz9GGzKnbZb9ty5Ol7lSNO3XOz56wgQCCXgPtIc/Wjr2afQ3co/3vu3mX7Hbcpo1EpZx1zWcIqlUSAwCAgSAeJBF933nfbctj/7V4OOXrXssFnhQQdUQKB5QkI0uU5rflWBx+7WznqlD3Lhg3/GeqG60dlm21v/GbNRzcAAQLTCDjumUZvK+67x/7b9SEaH+UvOO2qcs5rr9iKr+6lCBBYSwFBupa6K3jtSy+8tpz/3qvKiftcUs78H+dEV0BnUwIzF/DRfuYt+E8BF55xdYk/FgIE5k/AEen89UzFBAgkExCkyRqiHAIE5k9AkM5fz1RMgEAyAUGarCHKIUBg/gQE6fz1TMUECCQTEKTJGqIcAgTmT0CQzl/PVEyAQDIBQZqsIcohQGD+BATp/PVMxQQIJBMQpMkaohwCBOZPQJDOX89UTIBAMgF/1z5ZQ4Zyznvt5SX+WAgQyC/giDR/j1RIgEByAUGavEHKI0Agv4Agzd8jFRIgkFxAkCZvkPIIEMgvIEjz90iFBAgkFxCkyRukPAIE8gsI0vw9UiEBAskFBGnyBimPAIH8AoI0f49USIBAcgFBmrxByiNAIL+AIM3fIxUSIJBcQJAmb5DyCBDILyBI8/dIhQQIJBcQpMkbpDwCBPILCNL8PVIhAQLJBQRp8gYpjwCB/AKCNH+PVEiAQHIBQZq8QcojQCC/gCDN3yMVEiCQXECQJm+Q8ggQyC8gSPP3SIUECCQXEKTJG6Q8AgTyCwjS/D1SIQECyQUEafIGKY8AgfwCgjR/j1RIgEByAUGavEHKI0Agv4Agzd8jFRIgkFxAkCZvkPIIEMgvIEjz90iFBAgkFxCkyRukPAIE8gsI0vw9UiEBAskFBGnyBimPAIH8AoI0f49USIBAcgFBmrxByiNAIL+AIM3fIxUSIJBcQJAmb5DyCBDILyBI8/dIhQQIJBcQpMkbpDwCBPILCNL8PVIhAQLJBQRp8gYpjwCB/AKCNH+PVEiAQHIBQZq8QcojQCC/gCDN3yMVEiCQXECQJm+Q8ggQyC8gSPP3SIUECCQXEKTJG6Q8AgTyCwjS/D1SIQECyQUEafIGKY8AgfwCgjR/j1RIgEByAUGavEHKI0Agv4Agzd8jFRIgkFxAkCZvkPIIEMgvIEjz90iFBAgkFxCkyRukPAIE8gsI0vw9UiEBAskFBGnyBimPAIH8AoI0f49USIBAcgFBmrxByiNAIL+AIM3fIxUSIJBcQJAmb5DyCBDILyBI8/dIhQQIJBcQpMkbpDwCBPILCNL8PVIhAQLJBQRp8gYpjwCB/AKCNH+PVEiAQHIBQZq8QcojQCC/gCDN3yMVEiCQXECQJm+Q8ggQyC8gSPP3SIUECCQXEKTJG6Q8AgTyCwjS/D1SIQECyQUEafIGKY8AgfwCgjR/j1RIgEByAUGavEHKI0Agv4Agzd8jFRIgkFxAkCZvkPIIEMgvIEjz90iFBAgkFxCkyRukPAIE8gsI0vw9UiEBAskFBGnyBimPAIH8AoI0f49USIBAcgFBmrxByiNAIL+AIM3fIxUSIJBcQJAmb5DyCBDILyBI8/dIhQQIJBcQpMkbpDwCBPILCNL8PVIhAQLJBQRp8gYpjwCB/AKCNH+PVEiAQHIBQZq8QcojQCC/gCDN3yMVEiCQXECQJm+Q8ggQyC8gSPP3SIUECCQXEKTJG6Q8AgTyCwjS/D1SIQECyQUEafIGKY8AgfwCgjR/j1RIgEByAUGavEHKI0Agv4Agzd8jFRIgkFxAkCZvkPIIEMgvIEjz90iFBAgkFxCkyRukPAIE8gsI0vw9UiEBAskFBGnyBimPAIH8AoI0f49USIBAcgFBmrxByiNAIL+AIM3fIxUSIJBcQJAmb5DyCBDILyBI8/dIhQQIJBcQpMkbpDwCBPILCNL8PVIhAQLJBQRp8gYpjwCB/AKCNH+PVEiAQHIBQZq8QcojQCC/gCDN3yMVEiCQXECQJm+Q8ggQyC+wMX+J66PCk0YHrI+JmiWBBgUckTbYVFMiQKCugCCt6200AgQaFBCkDTbVlAgQqCsgSOt6G40AgQYFBGmDTTUlAgTqCgjSut5GI0CgQQFB2mBTTYkAgboC7iOt5H38hosrjWQYAgRqCwjSCuJutq+AbAgCMxTw0X6G+IYmQKANAUHaRh/NggCBGQoI0hniG5oAgTYEBGkbfTQLAgRmKCBIZ4hvaAIE2hAQpG300SwIEJihgCCdIb6hCRBoQ0CQttFHsyBAYIYCgnSG+IYmQKANAUHaRh/NggCBGQoI0hniG5oAgTYEBGkbfTQLAgRmKCBIZ4hvaAIE2hAQpG300SwIEJihgCCdIb6hCRBoQ0CQttFHsyBAYIYCgnSG+IYmQKANAUHaRh/NggCBGQoI0hniG5oAgTYEBGkbfTQLAgRmKCBIZ4hvaAIE2hAQpG300SwIEJihgCCdIb6hCRBoQ0CQttFHsyBAYIYCgnSG+IYmQKANAUHaRh/NggCBGQoI0hniG5oAgTYEBGkbfTQLAgRmKCBIZ4hvaAIE2hAQpG300SwIEJihgCCdIb6hCRBoQ0CQttFHsyBAYIYCG2c4tqEJ9AL//ve/yzXXXFPiq4XAagU2btxYbnazm5X4WnupP2LtGRovtcC//vWvPkRTF6m4uRCIX8TxJ8J0hx12qFqzj/ZVuQ02KTAciU6u85jAtAKz+HQjSKftmv1XLRBveAuBtRCo/d4SpGvRRa+5LAHnRJfFZKNVCNR+bwnSVTTJLgQIEJgUEKSTGh4TIEBgFQKCdBVodiFAgMCkgCCd1PCYAAECqxAQpKtAswsBAgQmBQTppIbHBAgQWIWAIF0Fml0IECAwKSBIJzU8Ti/wu9/9rlxwwQWp6vzjH//Y11T73sVUCOu8GEG6zt8A8zb9D3/4w+Vxj3tcuf7669OUftZZZ/U1/f3vf09Tk0LqCgjSut5GI0CgQQFB2mBTTYkAgboC/hm9ut5G24oC3/zmN8vXvva1Eh+pH/rQh5bDDz98s1f/xS9+Uc4999zyy1/+suy3337lEY94RLn3ve893i7Ob370ox8tRxxxRLnTne40Xh8P3va2t5X73Oc+5dBDDx2v/8Mf/lDio/yvfvWr/nUe//jHj58bHpx//vnl29/+dnnJS14yrOq//uY3vymf+tSnypOf/ORy+9vfvvz85z8vn/3sZ8uxxx5bfvrTn5Yvf/nL5W9/+1u53/3u12+zYcOGBfs9/elP7/f50pe+VPbYY4/yvOc9r3/+r3/9a1/TRRddVG5zm9uURz7ykeWQQw4Zjx3nlT/xiU+Upz71qeXPf/5z+eIXv1hiHgcddFA5+uijl/Xvd5533nklvGP//fffvzzlKU8pu++++3iMePCPf/yjn99PfvKT/p+yC+cnPOEJZZttNh2vhfUuu+zSm376058uF154YXnAAx7Q9y7++bsf/ehH5Qtf+EL505/+VB784AeXI488csEYab8ZLbF85jOfGU3+WWITqwhMLXDllVeOVvrn5S9/+aj7YRp1ITe65S1vOXrgAx84uu1tb9uv64JlweudfPLJo+6Hc3SLW9xidP/733/Uhc+o+6EenXDCCePtulDq9/3Yxz42XjfUtN12241e+MIXjtd3gTy61a1uNdp+++1HBx988OgOd7jD6C53ucvoxS9+cf8aXVj32x533HH991dcccV433jNLoD79WeffXa//rTTTuu/P+mkk0Y3v/nNR12gjLqA7dc98YlPHO877NcF6agL19G+++47etrTntY/H/V34TnabbfdRg95yENG3S+LfptXvepV4/3jZznM3vCGN/QWXVCP7njHO/brHv7wh4+3G+Y9+fXyyy/vx4r9o7bw3nnnnUe77rrr6POf//x43+985zujO9/5zqPuH1UedQE9uutd79q/fheGo0suuWS8XYx92GGHjbpffKN73vOeo7vf/e79dk960pNGH/rQh8YOe++9d7/+BS94wXjfybqW83jqN+iNLzCZhfF4qWXTr4q0Ua8wApsEhqO0OJKLo5k42vzxj39c4sjwXe96V/n973/fb/zrX/+6vPSlLy2P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)

```text
<style>
    article {
        margin: 0 auto;
        width: 400px;
        height: 400px;
        border: solid 5px silver;
        display: grid;
        grid-template-rows: repeat(4, 100px);
        grid-template-columns: repeat(4, 100px);
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        border: solid 1px blueviolet;
        font-size: 30px;
        color: white;
    }

    article div:first-child {
        grid-area: 2/2/4/4;
    }
</style>
...

<article class="container">
    <div>1</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#命名附加)命名附加

同样是上面的例子可以使用栅格线命名来附加元素。

```text
article {
    margin: 0 auto;
    width: 400px;
    height: 400px;
    border: solid 5px silver;
    display: grid;
    grid-template-rows: repeat(auto-fill, [r] 100px);
    grid-template-columns: repeat(auto-fill, [l] 100px);
}

article div {
    background: blueviolet;
    background-clip: content-box;
    padding: 10px;
    border: solid 1px blueviolet;
    font-size: 30px;
    color: white;
}
article div:first-child {
		grid-area: r 2/l 2/r 4/l 4;
}
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#区域声明)区域声明

区域是由多个单元格构成，使用 `grid-template-areas`可以定义栅格区域，并且栅格区域必须是矩形的。

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#区域布局)区域布局

下面是使用栅格区域布局移动端页面结构

![image-20190829195447976](data:image/png;base64,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)

```text
<style>
    body {
        width: 100vw;
        height: 100vh;
        display: grid;
        grid-template-rows: 80px 1fr 50px;
        grid-template-columns: 100px 1fr 50px 60px;
        grid-template-areas: "header header header header"
            "nav main main aside"
            "footer footer footer footer";
    }

    main {
    		/* 完整的写法，推荐使用下面的简写方式*/
				/* grid-area: main-start/main-start/main-end/main-end; */
        grid-area: main;
        background: #E9EEEF;
    }

    header {
        background: #2EC56C;
        grid-area: header;
    }

    nav {
        background: #E1732C;
        grid-area: nav;
    }

    aside {
        grid-area: aside;
        background: #EEBC31;
    }

    footer {
        grid-area: footer;
        background: #904FA9;
    }
</style>
...

<body>
    <header></header>
    <nav></nav>
    <main></main>
    <aside></aside>
    <footer></footer>
</body>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#区域命名)区域命名

系统会为区域自动命名，上例中的会产生 `header-start` 水平与垂直同名的起始区域与 `header-end`水平与垂直同名的区域终止。

![image-20190830000855557](https://houdunren.gitee.io/note/assets/img/image-20190830000855557.d60b8b01.png)

下面使用区域命名部署的效果

![image-20190831222934932](data:image/png;base64,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7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv4Cw679DJyBAICAg7AJISggQ6C8g7Prv0AkIEAgICLsAkhICBPoLCLv+O3QCAgQCAsIugKSEAIH+AsKu/w6dgACBgICwCyApIUCgv8CHrznCZ198/JqXeQ0BAgQOE/DO7jB6NyZAYE8BYbentnsRIHCYgLA7jN6NCRDYU0DY7antXgQIHCYg7A6jd2MCBPYUEHZ7arsXAQKHCQx/9eS///7xzd//+O1hQ7kxAQIEsgWGYffr337w5le/8aYvG1s/AgSOExiG3TTOn/72u+OmcmcCBAi8QuDzz767+ipv367SeIIAgXsSEHb3tE1nIUDgqoCwu0rjCQIE7klA2N3TNp2FAIGrAsLuKo0nCBC4JwFhd0/bdBYCBK4KXP3Vk6uv+OmJTz/5+qWnPUeAAIHNBF779zTP3tk9PT1tNqDGBAgQ2FNgnWfPYbe+uOdA7kWAAIEtBeZ8O3tnt+UN9SZAgMCRAsLuSH33JkBgNwFhtxu1GxEgcKSAsDtS370JENhNYBB2fiK7m74bESCwkcBljp3Cbv6JxUZ31pYAAQK7Cyxz7YPlg90ncUMCBAjsIDDl3Omd3Q73cwsCBAgcJiDsDqN3YwIE9hR4Drv5W9n5854DuBcBAgS2EJjzbP7snd0WynoSIFBOQNiVW4mBCBDYQuAUdvNbvS1uoicBAgSOEFjm2insjhjEPQkQILCXwNnv2S1TcK8B3IcAAQJbCCzzbPraO7stlPUkQKCcwHPYnSdguRkNRIAAgZsEln90fc630zu7+cJNHRUTIECgsMAy1171P9x57f/worCJ0QgQuHMBP6C48wU7HoFHFVi+q5u+Pn0b+6ggzk2AwGMIXPyA4jGO7ZQECDyKwPwO7/TObr7wKADOSYDA/Qssc+0UdtOxl0/cP4MTEiBwzwLrPDv7AcW7g1/+7fZ7BnE2AgTuUeA8x6bge/7Vk+mLt2/fnk78v//8+OYff/729NgXBAgQ6CLw5ZdfnY06v8N7+v77708ptwy8qfp9j0c1165N10cf63uMalwjQKC/wBw6kZOMaiPX1jXLx2e/VDw9sQyf0eNp0HXNtWvzoZb187X583KY+ZrPBAg8lsBLOTB6LnJtXXMWdhPvVLAMp/XjUc18bfo8fSxfPz1e33S6Nn2s695d9U8CBO5V4FoWrM/7Ut3oufW19eOp/4fTxXXorK/NL1zWja7NA8/PTY+Xr5mfnz8v6+ZrPhMg8JgC78uD0fO3XBv+gGKinpssw+qla9NrlrXT4+ljfs27R+f/HNWfV3hEgMA9CbyUB6NzXqsfXR9dm3rO10/fxs4X1gE0XR9dm5pcuz49N3+sa+br0+f5nstrviZA4DEFInlwrWZ0fX3t/xYCheVjGN44AAAAAElFTkSuQmCC)

```text
<style>
    article {
        width: 100vw;
        height: 100vh;
        display: grid;
        grid-template-rows: 80px 1fr 50px;
        grid-template-columns: 80 1fr;
        grid-template-areas: "header header header"
            "nav main main"
            "footer footer footer";
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        border: solid 1px blueviolet;
        padding: 10px;
        box-sizing: border-box;
        color: white;
        font-size: 25px;
    }

    div:nth-child(1) {
        grid-area: header-start/nav-start/main-end/main-end;
    }

    div:nth-child(2) {
        grid-area: footer-start/footer-start/footer-end/footer-end;
    }
</style>
...

<article>
	<div></div>
	<div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#区域占位)区域占位

使用一个或多个 `.` 定义区域占位。

![image-20190829203245181](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    article {
        width: 100vw;
        height: 100vh;
        display: grid;
        grid-template-rows: repeat(3, 33.3%);
        grid-template-columns: repeat(3, 33.3%);
        grid-template-areas: "top . ."
            "top . ."
            "bottom bottom bottom";
    }

    .top {
        background: blueviolet;
        grid-area: top;
        font-size: 35px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
    }

    .bottom {
        background: orange;
        grid-area: bottom;
        text-align: center;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 35px;
    }
</style>
...

<article>
    <div class="top">
        houdunren.com
    </div>
    <div class="bottom">
        后盾人
    </div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#栅格流动)栅格流动

在容器中设置`grid-auto-flow` 属性可以改变单元流动方式。

| 选项   | 说明     |
| ------ | -------- |
| column | 按列排序 |
| row    | 按行排列 |

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#基本使用)基本使用

下例将单元按列排序流动

![image-20190830003134787](data:image/png;base64,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)

```text
<style>
  article {
      width: 400px;
      height: 400px;
      display: grid;
      grid-template-rows: repeat(2, 1fr);
      grid-template-columns: repeat(2, 1fr);
      border: solid 5px silver;
      grid-auto-flow: column;
  }

  div {
      background: blueviolet;
      background-clip: content-box;
      padding: 10px;
      font-size: 35px;
      color: white;
  }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#强制填充)强制填充

当元素在栅格中放不下时，将会发生换行产生留白，使用`grid-auto-flow: row dense;` 可以执行填充空白区域操作。

![image-20190830004630960](data:image/png;base64,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UAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATAHFHzN3UxMgQIBAUAHFHzR4YxMgQIBATIE5hzv2xo0bD/ddvR8BAgQIECAwIgGv+EcEb1sCBAgQIDAKAcU/CnV7EiBAgACBEQko/hHB25YAAQIECIxCYGxi8jaKje1JgAABAgQIlBfwir+8uR0JECBAgMDIBBT/yOhtTIAAAQIEygso/vLmdiRAgAABAiMTUPwjo7cxAQIECBAoL6D4y5vbkQABAgQIjExA8Y+M3sYECBAgQKC8gOIvb25HAgQIECAwMgHFPzJ6GxMgQIAAgfICir+8uR0JECBAgMDIBBT/yOhtTIAAAQIEygv8P2b8cAzdE3r3AAAAAElFTkSuQmCC)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 200px;
        padding-top: 200px;
    }

    article {
        width: 600px;
        height: 600px;
        display: grid;
        grid-template-rows: repeat(3, 200px);
        grid-template-columns: repeat(3, 200px);
        border: solid 5px silver;
        grid-auto-flow: row dense;
    }

    div {
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        font-size: 35px;
        color: white;
    }

    article div:nth-child(1) {
        grid-column: 1/span 2;
        background: #000;
    }

    article div:nth-child(2) {
        grid-column: 2/span 1;
    }
</style>
...

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#栅格对齐)栅格对齐

可以通过属性方便的定义栅格的对齐方式，可用值包括 `start | end | center | stretch | space-between | space-evenly | space-around`。

| 选项            | 说明                                             | 对象     |
| --------------- | ------------------------------------------------ | -------- |
| align-items     | 栅格内所有元素的垂直排列方式                     | 栅格容器 |
| justify-items   | 栅格内所有元素的横向排列方式                     | 栅格容器 |
| justify-content | 所有栅格在容器中的水平对齐方式，容器有额外空间时 | 栅格容器 |
| align-content   | 所有栅格在容器中的垂直对齐方式，容器有额外空间时 | 栅格容器 |
| align-self      | 元素在栅格中垂直对齐方式                         | 栅格元素 |
| justify-self    | 元素在栅格中水平对齐方式                         | 栅格元素 |

![image-20190829225727414](https://houdunren.gitee.io/note/assets/img/image-20190829225727414.7861d31b.png)

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#平均分布)平均分布

![image-20190829231259807](https://houdunren.gitee.io/note/assets/img/image-20190829231259807.2b1db179.png)

```text
border: solid 5px silver;
width: 600px;
height: 600px;
display: grid;
grid-template-columns: 200px 200px;
grid-template-rows: 200px 200px;
justify-content: space-between;
align-content: space-evenly;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#元素对齐)元素对齐

用于控制所有元素的对齐方式

![image-20190928161557891](data:image/png;base64,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)

```text
margin: 0 auto;
border: solid 1px silver;
width: 400px;
height: 100px;
display: grid;
grid-template-columns: repeat(4, 100px);
justify-items: center;
align-items: center;
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#元素独立控制)元素独立控制

控制单个元素的对齐方式

![image-20190928161449880](data:image/png;base64,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)

```text
div:first-child {
  justify-self: end;
  align-self: center;
}

div:nth-child(4) {
  justify-self: start;
  align-self: center;
}
```

### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#组合简写)组合简写

#### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#place-content)place-content

用于控制栅格的对齐方式，语法如下：

```text
place-content: <align-content> <justify-content>
```

#### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#place-items)place-items

控制所有元素的对齐方式，语法结构如下：

```text
place-items: <align-items> <justify-items>
```

#### [#](https://houdunren.gitee.io/note/css/11 栅格系统.html#place-self)place-self

控制单个元素的对齐方式

```css
place-self: <align-self> <justify-self>
```

# 变形动画

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#基础知识)基础知识

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#坐标系统)坐标系统

要使用元素变形操作需要掌握坐标轴，然后通过改变不同坐标来控制元素的变形。

![image-20190901174833435](https://houdunren.gitee.io/note/assets/img/image-20190901174833435.9b3582ae.png)

- X轴是水平轴
- Y轴是垂直轴
- Z轴是纵深轴

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#变形操作)变形操作

使用 `transform` 规则控制元素的变形操作，包括控制移动、旋转、倾斜、3D转换等，下面会详细介绍每一个知识点。

下面是CSS提供的变形动作。

| 选项                          | 说明                                  |
| ----------------------------- | ------------------------------------- |
| none                          | 定义不进行转换。                      |
| translate(*x*,*y*)            | 定义 2D 转换。                        |
| translate3d(*x*,*y*,*z*)      | 定义 3D 转换。                        |
| translateX(*x*)               | 定义转换，只是用 X 轴的值。           |
| translateY(*y*)               | 定义转换，只是用 Y 轴的值。           |
| translateZ(*z*)               | 定义 3D 转换，只是用 Z 轴的值。       |
| scale(*x*,*y*)                | 定义 2D 缩放转换。                    |
| scale3d(*x*,*y*,*z*)          | 定义 3D 缩放转换。                    |
| scaleX(*x*)                   | 通过设置 X 轴的值来定义缩放转换。     |
| scaleY(*y*)                   | 通过设置 Y 轴的值来定义缩放转换。     |
| scaleZ(*z*)                   | 通过设置 Z 轴的值来定义 3D 缩放转换。 |
| rotate(*angle*)               | 定义 2D 旋转，在参数中规定角度。      |
| rotate3d(*x*,*y*,*z*,*angle*) | 定义 3D 旋转。                        |
| rotateX(*angle*)              | 定义沿着 X 轴的 3D 旋转。             |
| rotateY(*angle*)              | 定义沿着 Y 轴的 3D 旋转。             |
| rotateZ(*angle*)              | 定义沿着 Z 轴的 3D 旋转。             |
| skew(*x-angle*,*y-angle*)     | 定义沿着 X 和 Y 轴的 2D 倾斜转换。    |
| skewX(*angle*)                | 定义沿着 X 轴的 2D 倾斜转换。         |
| skewY(*angle*)                | 定义沿着 Y 轴的 2D 倾斜转换。         |
| perspective(*n*)              | 为 3D 转换元素定义透视视图。          |

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#变形叠加)变形叠加

重复设置变形操作时只在原形态上操作。

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#默认处理)默认处理

下面设置了两次移动，并不会移动 550px 而是只移动50px。

```text
<style>
    div {
        transform: translateX(500px);
        width: 100px;
        height: 100px;
        background: #9b59b6;
    }

    div:nth-child(1) {
        transform: translateX(50px);
    }
</style>

<div></div>
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#伪类叠加)伪类叠加

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7734353.de347599.gif)

```text
<style>
    div {
        transition: 2s;
        transform: translateX(200px) translateX(50px);
        width: 100px;
        height: 100px;
        background: #9b59b6;
    }

    div:hover {
        transition: 2s;
        transform: translateX(100px);
    }
</style>

<div></div>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#行级元素)行级元素

行级元素不产生变形效果，将其转为 `inline-block` 或 `block` 以及弹性元素时都可以产生变化效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7734657.cce0a000.gif)

```text
<style>
    span {
        display: inline-block;
        transition: 2s;
        transform: translateX(100px) translateX(50px);
        width: 100px;
        height: 100px;
        background: #9b59b6;
    }

    span:hover {
        transition: 2s;
        transform: translateX(100px);
    }
</style>

<span>hdcms</span>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#伪类状态)伪类状态

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#hover):hover

鼠标移动上后发生改变。

![image-20190902133840698](data:image/png;base64,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)

```text
article div:nth-child(2):hover {
	transform: rotate(180deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#target):target

以下操作变化时间为零秒，通过掌握后面的过渡动画可以控制变化时间。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7404551.0296ff4c.gif)

```text
<style>
    article {
        width: 300px;
        height: 300px;
        display: grid;
        gap: 10px;
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(2, 1fr);
        position: relative;
        border: solid 5px silver;
        color: white;
    }

    article div a {
        color: white;
        text-decoration: none;
    }

    article div,
    article div aside {
        background: blueviolet;
        background-clip: content-box;
        padding: 5px;
        border: solid 2px blueviolet;
        box-sizing: border-box;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }

    article div aside {
        position: absolute;
        display: none;
        width: 100px;
        height: 100px;
    }

    aside:target {
        display: block;
        transform: translateY(150px);
        box-shadow: 0 0 10px #ddd;
    }
</style>

<article>
    <div>
        <a href="#hdcms">hdcms</a>
        <aside id="hdcms">
            内容管理系统
        </aside>
    </div>
    <div>
        <a href="#houdunren">houdunren</a>
        <aside id="houdunren">
            在线社区
        </aside>
    </div>
</article>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#移动元素)移动元素

- 沿X轴移动时正值向右移动、负值向左移动
- 沿Y轴移动时正值向下移动、负值向上移动
- 如果使用百分数将控制元素的原尺寸计算百分比然后移动
- 可同时设置多个值，解析器会从左向右依次执行
- 变形是在原基础上更改，即第二次设置值时不是在第一次值上变化

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#translatex)translateX

正值向右移动、负值向左移动。

![image-20190901223332605](data:image/png;base64,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)

```text
<style>
    article {
        width: 300px;
        height: 300px;
        position: relative;
        border: solid 5px silver;
    }

    article div {
        width: 100px;
        height: 100px;
        background: blueviolet;
        box-sizing: border-box;
        position: absolute;
        left: 50%;
        margin-left: -50px;
        top: 50%;
        margin-top: -50px;
    }

    article div:nth-child(1) {
        background: #e9dddd;
    }

    article div:nth-child(2) {
        transform: translateX(100px);
    }
</style>
...

<article>
    <div></div>
    <div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#translatey)translateY

正值向下移动、负值向上移动。

![image-20190901223350501](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: translateY(100px);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#translate)translate

使用 `translate` 可以控制按X、Y同时移动操作，第一个值控制X移动，第二个值控制Y移动。

![image-20190901223632200](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAT8AAAFBCAYAAAABjqgaAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAycDIwMdgycCZmFxc4BgQ4ANUwgCjUcG3a0C1QHBZF2RWvOCkr28r/r3yy/C89rZ8Lz+mehTAlZJanAyk/wBxenJBUQkDA2MKkK1cXlIAYncA2SJFQEcB2XNA7HQIewOInQRhHwGrCQlyBrJvANkCyRmJQDMYXwDZOklI4ulIbKi9IMDr464Q6hMS5Bju6eJKwL0kg5LUihIQ7ZxfUFmUmZ5RouAIDKVUBc+8ZD0dBSMDQ0sGBlCYQ1R/vgEOS0YxDoRYgRgDg8UMoOBDhFg80A/b5RgY+PsQYmpA/wp4MTAc3FeQWJQIdwDjN5biNGMjCJt7OwMD67T//z+HMzCwazIw/L3+///v7f///13GwMB8i4HhwDcAZtdiW04WgFAAAAwDSURBVHgB7dnBjV1lEIRRQE6CCCxSIAGHhciAdCYS5J13hAEWS4ZFLaalenWPdx61rv4+bX0awY9/f//zgz8ECBB4mMBPD9vXugQIEPhXQPz8QyBA4JEC4vfIs1uaAAHx82+AAIFHCojfI89uaQIExM+/AQIEHinw6b9bv729/fdH/k6AAIGXFvjy5cu79/vN7x2JHxAg8AQB8XvCle1IgMA7AfF7R+IHBAg8QUD8nnBlOxIg8E7g3f/weDfx/Qf/9x8L/2/Ozwg8UeC3X74+ce3anX/941v0Nr/5RUyGCBBYExC/tYvahwCBSED8IiZDBAisCYjf2kXtQ4BAJCB+EZMhAgTWBMRv7aL2IUAgEhC/iMkQAQJrAuK3dlH7ECAQCYhfxGSIAIE1AfFbu6h9CBCIBMQvYjJEgMCagPitXdQ+BAhEAuIXMRkiQGBNQPzWLmofAgQiAfGLmAwRILAmIH5rF7UPAQKRgPhFTIYIEFgTEL+1i9qHAIFIQPwiJkMECKwJiN/aRe1DgEAkIH4RkyECBNYExG/tovYhQCASEL+IyRABAmsC4rd2UfsQIBAJiF/EZIgAgTUB8Vu7qH0IEIgExC9iMkSAwJqA+K1d1D4ECEQC4hcxGSJAYE1A/NYuah8CBCIB8YuYDBEgsCYgfmsXtQ8BApGA+EVMhggQWBMQv7WL2ocAgUhA/CImQwQIrAmI39pF7UOAQCQgfhGTIQIE1gTEb+2i9iFAIBIQv4jJEAECawLit3ZR+xAgEAmIX8RkiACBNQHxW7uofQgQiATEL2IyRIDAmoD4rV3UPgQIRALiFzEZIkBgTUD81i5qHwIEIgHxi5gMESCwJiB+axe1DwECkYD4RUyGCBBYExC/tYvahwCBSED8IiZDBAisCYjf2kXtQ4BAJCB+EZMhAgTWBMRv7aL2IUAgEhC/iMkQAQJrAuK3dlH7ECAQCYhfxGSIAIE1AfFbu6h9CBCIBMQvYjJEgMCagPitXdQ+BAhEAuIXMRkiQGBNQPzWLmofAgQiAfGLmAwRILAmIH5rF7UPAQKRgPhFTIYIEFgTEL+1i9qHAIFIQPwiJkMECKwJiN/aRe1DgEAkIH4RkyECBNYExG/tovYhQCASEL+IyRABAmsC4rd2UfsQIBAJiF/EZIgAgTUB8Vu7qH0IEIgExC9iMkSAwJqA+K1d1D4ECEQC4hcxGSJAYE1A/NYuah8CBCIB8YuYDBEgsCYgfmsXtQ8BApGA+EVMhggQWBMQv7WL2ocAgUhA/CImQwQIrAmI39pF7UOAQCQgfhGTIQIE1gTEb+2i9iFAIBIQv4jJEAECawLit3ZR+xAgEAmIX8RkiACBNQHxW7uofQgQiATEL2IyRIDAmoD4rV3UPgQIRALiFzEZIkBgTUD81i5qHwIEIgHxi5gMESCwJiB+axe1DwECkYD4RUyGCBBYExC/tYvahwCBSED8IiZDBAisCXxaW+gJ+/z19esT1nyZHX//8/PLvPUJD317+xat6Te/iMkQAQJrAuK3dlH7ECAQCYhfxGSIAIE1AfFbu6h9CBCIBMQvYjJEgMCagPitXdQ+BAhEAuIXMRkiQGBNQPzWLmofAgQiAfGLmAwRILAmIH5rF7UPAQKRgPhFTIYIEFgTEL+1i9qHAIFIQPwiJkMECKwJiN/aRe1DgEAkIH4RkyECBNYExG/tovYhQCASEL+IyRABAmsC4rd2UfsQIBAJiF/EZIgAgTUB8Vu7qH0IEIgExC9iMkSAwJqA+K1d1D4ECEQC4hcxGSJAYE1A/NYuah8CBCIB8YuYDBEgsCYgfmsXtQ8BApGA+EVMhggQWBMQv7WL2ocAgUhA/CImQwQIrAmI39pF7UOAQCQgfhGTIQIE1gTEb+2i9iFAIBIQv4jJEAECawLit3ZR+xAgEAmIX8RkiACBNQHxW7uofQgQiATEL2IyRIDAmoD4rV3UPgQIRALiFzEZIkBgTUD81i5qHwIEIgHxi5gMESCwJiB+axe1DwECkYD4RUyGCBBYExC/tYvahwCBSED8IiZDBAisCYjf2kXtQ4BAJCB+EZMhAgTWBMRv7aL2IUAgEhC/iMkQAQJrAuK3dlH7ECAQCYhfxGSIAIE1AfFbu6h9CBCIBMQvYjJEgMCagPitXdQ+BAhEAuIXMRkiQGBNQPzWLmofAgQiAfGLmAwRILAmIH5rF7UPAQKRgPhFTIYIEFgTEL+1i9qHAIFIQPwiJkMECKwJiN/aRe1DgEAkIH4RkyECBNYExG/tovYhQCASEL+IyRABAmsC4rd2UfsQIBAJiF/EZIgAgTUB8Vu7qH0IEIgExC9iMkSAwJqA+K1d1D4ECEQC4hcxGSJAYE1A/NYuah8CBCIB8YuYDBEgsCYgfmsXtQ8BApGA+EVMhggQWBMQv7WL2ocAgUhA/CImQwQIrAmI39pF7UOAQCQgfhGTIQIE1gTEb+2i9iFAIBIQv4jJEAECawLit3ZR+xAgEAmIX8RkiACBNQHxW7uofQgQiATEL2IyRIDAmoD4rV3UPgQIRALiFzEZIkBgTUD81i5qHwIEIgHxi5gMESCwJiB+axe1DwECkYD4RUyGCBBYExC/tYvahwCBSED8IiZDBAisCYjf2kXtQ4BAJCB+EZMhAgTWBMRv7aL2IUAgEhC/iMkQAQJrAuK3dlH7ECAQCYhfxGSIAIE1gU9rCz1hn58/f37CmnYkcCrgN79TXh8nQKBVQPxaL+NdBAicCojfKa+PEyDQKiB+rZfxLgIETgXE75TXxwkQaBUQv9bLeBcBAqcC4nfK6+MECLQKiF/rZbyLAIFTAfE75fVxAgRaBcSv9TLeRYDAqYD4nfL6OAECrQLi13oZ7yJA4FRA/E55fZwAgVYB8Wu9jHcRIHAqIH6nvD5OgECrgPi1Xsa7CBA4FRC/U14fJ0CgVUD8Wi/jXQQInAqI3ymvjxMg0Cogfq2X8S4CBE4FxO+U18cJEGgVEL/Wy3gXAQKnAuJ3yuvjBAi0Cohf62W8iwCBUwHxO+X1cQIEWgXEr/Uy3kWAwKmA+J3y+jgBAq0C4td6Ge8iQOBUQPxOeX2cAIFWAfFrvYx3ESBwKiB+p7w+ToBAq4D4tV7GuwgQOBUQv1NeHydAoFVA/Fov410ECJwKiN8pr48TINAqIH6tl/EuAgROBcTvlNfHCRBoFRC/1st4FwECpwLid8rr4wQItAqIX+tlvIsAgVMB8Tvl9XECBFoFxK/1Mt5FgMCpgPid8vo4AQKtAuLXehnvIkDgVED8Tnl9nACBVgHxa72MdxEgcCogfqe8Pk6AQKuA+LVexrsIEDgVEL9TXh8nQKBVQPxaL+NdBAicCojfKa+PEyDQKiB+rZfxLgIETgXE75TXxwkQaBUQv9bLeBcBAqcC4nfK6+MECLQKiF/rZbyLAIFTAfE75fVxAgRaBcSv9TLeRYDAqYD4nfL6OAECrQLi13oZ7yJA4FRA/E55fZwAgVYB8Wu9jHcRIHAqIH6nvD5OgECrgPi1Xsa7CBA4FRC/U14fJ0CgVUD8Wi/jXQQInAqI3ymvjxMg0Cogfq2X8S4CBE4FxO+U18cJEGgVEL/Wy3gXAQKnAuJ3yuvjBAi0Cohf62W8iwCBUwHxO+X1cQIEWgXEr/Uy3kWAwKmA+J3y+jgBAq0C4td6Ge8iQOBUQPxOeX2cAIFWAfFrvYx3ESBwKiB+p7w+ToBAq4D4tV7GuwgQOBUQv1NeHydAoFVA/Fov410ECJwKiN8pr48TINAqIH6tl/EuAgROBcTvlNfHCRBoFRC/1st4FwECpwLid8rr4wQItAqIX+tlvIsAgVMB8Tvl9XECBFoFxK/1Mt5FgMCpgPid8vo4AQKtAuLXehnvIkDgVED8Tnl9nACBVgHxa72MdxEgcCogfqe8Pk6AQKuA+LVexrsIEDgVEL9TXh8nQKBVQPxaL+NdBAicCojfKa+PEyDQKvApedjb21syZoYAAQIvI+A3v5c5lYcSIPCRAuL3kZq+RYDAywiI38ucykMJEPhIAfH7SE3fIkDgZQR+/Pv7n5d5rYcSIEDggwT85vdBkD5DgMBrCYjfa93LawkQ+CAB8fsgSJ8hQOC1BP4BCJQaf8P1XdQAAAAASUVORK5CYII=)

```text
article div:nth-child(2) {
	transform: translate(100px, -100px);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#百分比移动)百分比移动

元素宽度为100px设置50%时将移动50px，即百分比是指元素的尺寸的百分比。

![image-20190902145927971](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: translateX(50%);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#元素居中)元素居中

居中可以使用多种方式，如弹性布局、定位操作，下面来看使用移动操作居中。

![image-20190904112916419](data:image/png;base64,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AgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAmI0BitgwkQIECgExChTsg+AQIECIwJiNAYrYMJECBAoBMQoU7IPgECBAiMCYjQGK2DCRAgQKATEKFOyD4BAgQIjAm8/Ozkx+Pxs217BAgQIEDgKQG/CT3F54cJECBA4BkBEXpGz88SIECAwFMCIvQUnx8mQIAAgWcEROgZPT9LgAABAk8JfPr29uepE/wwAQIECBD4oIDfhD4I58cIECBA4HkBEXre0AkECBAg8EEBEfognB8jQIAAgecF/gaE1xfrbjML7gAAAABJRU5ErkJggg==)

```text
<style>
    body {
        height: 100vh;
    }

    main {
        width: 400px;
        height: 400px;
        border: solid 5px silver;
        position: relative;
    }

    main div {
        width: 100px;
        height: 100px;
        background: blueviolet;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }
</style>

<main>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#translatez)translateZ

控制Z轴移动，正数向外、负数向里移动。因为Z轴是透视轴没有像X/Y一样的固定尺寸，所以不能使用百分数。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7827784.63fc4fc8.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        transform-style: preserve-3d;
        transition: 2s;
        transform: perspective(900px) rotateY(60deg);
    }

    body:hover main {
        transform: perspective(600px) rotateY(60deg) scaleZ(5);
    }

    div {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #f1c40f;
    }

    div.b {
        background: #8e44ad;
        transform: translateZ(-100px);
    }
</style>

<main>
    <div class="f"></div>
    <div class="b"></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#translate3d)translate3d

用于同时控制X/Y/Z轴的移动，三个值必须输入如果某个轴不需要移动时设置为零。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7824321.6a82c902.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        background: #f1c40f;
        perspective: 600px;
        transform: perspective(600px) rotateY(35deg);
        transition: 2s;
    }

    body:hover main {
        transform: perspective(600px) rotateY(35deg) translate3d(50%, 50%, 200px);
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#渐变表单)渐变表单

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7851179.821af195.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: 300px;
        height: 300px;
        border: solid 5px silver;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .field {
        position: relative;
        overflow: hidden;
        margin-bottom: 20px;
    }

    .field::before {
        content: '';
        position: absolute;
        left: 0;
        height: 2px;
        bottom: 0;
        width: 100%;
        background: linear-gradient(to right, white, #1abc9c, #f1c40f, #e74c3c, white);
        transform: translateX(-100%);
        transition: 2s;
    }

    .field:hover::before {
        transform: translateX(100%);
    }

    .field input {
        border: none;
        outline: none;
        background: #ecf0f1;
        padding: 10px;
    }
</style>

<main>
    <div class="field">
        <input type="text" placeholder="请输入后盾人帐号">
    </div>
    <div class="field">
        <input type="text" placeholder="请输入密码">
    </div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#页面切换)页面切换

下面是使用移动效果制作的页面切换效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7584912.730ab731.gif)

```text
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
<style>
    * {
        padding: 0;
        margin: 0;
    }

    a {
        text-decoration: none;
    }

    body {
        display: flex;
        width: 100vw;
        height: 100vh;
        flex-direction: column;
    }

    main {
        position: relative;
        background: #f3f3f3;
        flex: 1;
        overflow: hidden;
    }

    nav {
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: 8vh;
        text-align: center;
        background: #34495e;
    }

    nav a {
        flex: 1;
        font-size: 1.3em;
        text-transform: uppercase;
        font-weight: bold;
        opacity: .8;
        color: white;
    }

    nav a:nth-child(2) {
        border-right: solid 1px #aaa;
        border-left: solid 1px #aaa;
    }

    main>div {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        transition: all 1s;
        z-index: 1;
        background: #f3f3f3;
        opacity: 0;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transform: translate(0, -100%);
        color: white;
        font-size: 2em;
    }

    main>div:target {
        opacity: 1;
        transform: translate(0%, 0%);
    }

    main>div:nth-of-type(1):target {
        background: #3498db;
    }

    main>div:nth-of-type(2):target {
        background: #9b59b6;
    }

    main>div:nth-of-type(3):target {
        background: #16a085;
    }

    div i[class^="fa"] {
        font-size: 100px;
        color: white;
    }
</style>

<body>
    <main>
        <div id="home">
            <i class="fa fa-home" aria-hidden="true"></i>
            houdunren.com
        </div>
        <div id="video">
            <i class="fa fa-vimeo" aria-hidden="true"></i>
        </div>
        <div id="live">
            <i class="fa fa-viadeo" aria-hidden="true"></i>
        </div>
    </main>
    <nav>
        <a href="#home">home</a>
        <a href="#video">video</a>
        <a href="#live">live</a>
    </nav>
</body>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#缩放元素)缩放元素

比如数值为2时表示为原尺寸的两倍。

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#scalex)scaleX

下面是沿X轴缩放一半。

![image-20190902151123183](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY8AAAGSCAYAAAAb0k2iAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAycDEwMOgyaCcmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgscyG/7BVLP8ytjPr/X1730SJM9SiAKyW1OBlI/wHi9OSCohIGBsYUIFu5vKQAxO4AskWKgI4CsueA2OkQ9gYQOwnCPgJWExLkDGTfALIFkjMSgWYwvgCydZKQxNOR2FB7QYDXx10h1CckyDHc08WVgHtJBiWpFSUg2jm/oLIoMz2jRMERGEqpCp55yXo6CkYGhpYMDKAwh6j+fAMcloxiHAixAjEGBosZQMGHCLF4oB+2yzEw8PchxNSA/hXwYmA4uK8gsSgR7gDGbyzFacZGEDb3dgYG1mn//38OZ2Bg12Rg+Hv9///f2////7uMgYH5FgPDgW8AEPRhmJCm9HoAABE3SURBVHgB7dqxbSTmFQRgSrgmpAYucR+XqQ034dDdKFPGPpyoAbsMSXCquQcsSGBnsN+F7z9yh98cMCCkH/7468+bPwQIECBA4AGBHx/4u/4qAQIECBD4v4Dx8A+BAAECBB4WMB4Pk/kCAgQIEDAe/g0QIECAwMMCxuNhMl9AgAABAsbDvwECBAgQeFjAeDxM5gsIECBA4EsieH9/T2c3AgQIEHgxgW/fvsWf2G8ekcWRAAECBC4B43HpeCNAgACBKGA8IosjAQIECFwCxuPS8UaAAAECUcB4RBZHAgQIELgE4v9t9b0v+N5/df/e33cnQIAAgQ2BR/8vW795bPQqJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ8B4bPQkJQECBKoEjEdVHcIQIEBgQ+DLRkwpnynwv99/f9rH//avt7f//udpH/+0D/75H29vv/z7aR//9tPXr8/7cJ88IeA3j4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECXgPHo6kMaAgQITAgYj4mahCRAgECX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)

```text
article div:nth-child(2) {
	transform: scaleX(.5);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#scaley)scaleY

下面是沿Y轴缩放一半。

![image-20190902151103536](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY8AAAGPCAYAAACkmlznAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAycDEwMOgyaCcmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgscyG/7BVLP8ytjPr/X1730SJM9SiAKyW1OBlI/wHi9OSCohIGBsYUIFu5vKQAxO4AskWKgI4CsueA2OkQ9gYQOwnCPgJWExLkDGTfALIFkjMSgWYwvgCydZKQxNOR2FB7QYDXx10h1CckyDHc08WVgHtJBiWpFSUg2jm/oLIoMz2jRMERGEqpCp55yXo6CkYGhpYMDKAwh6j+fAMcloxiHAixAjEGBosZQMGHCLF4oB+2yzEw8PchxNSA/hXwYmA4uK8gsSgR7gDGbyzFacZGEDb3dgYG1mn//38OZ2Bg12Rg+Hv9///f2////7uMgYH5FgPDgW8AEPRhmJCm9HoAABEhSURBVHgB7dqxkWZnFQRQRE0SIoF1yGM9pUESmGSDhzd54CgBCENSYc9O1Rj3/d3NWXO0+l7f06rqWkk//fbHrz/5RYAAAQIEviDw5y/8Xr+VAAECBAj8T8B4+AeBAAECBL4sYDy+TOZvIECAAAHj4Z8BAgQIEPiygPH4Mpm/gQABAgTePiJ4f3//6Md+RoAAAQL/ZwLfv3//8GJ/8viQxQ8JECBA4DMB4/GZjr9GgAABAh8KGI8PWfyQAAECBD4TMB6f6fhrBAgQIPChgPH4kMUPCRAgQOAzgQ//b6sf/Q0/+q/uP/r9fk6AAAECHQJf/b9s/cmjo1cpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycpCRAgECVgPKLqEIYAAQIdAsajoycp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)

```text
article div:nth-child(2) {
	transform: scaleY(.5);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#scale)scale

使用 `scale` 可同时设置 `X/Y` 轴的缩放，如果只设置一个值时表示两轴缩放相同。

使用数值定义缩放，如 .5 表示缩小一半，2 表示放大两倍。

![image-20190902151035273](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: scale(.5, 2);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#scalez)scaleZ

沿Z轴缩放元素，需要有3D透视才可以查看到效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7905140.2e8820f0.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    body {
        width: 100vw;
        height: 100vh;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: 400px;
        height: 400px;
        border: solid 5px silver;
        transform-style: preserve-3d;
        transform: perspective(900px) rotateY(45deg);
        transition: 3s;
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -100px;
        margin-top: -100px;
        width: 200px;
        height: 200px;
    }

    div:nth-child(1) {
        background: #2ecc71;
    }

    div:nth-child(2) {
        background: #e67e22;
        transition: 1s;
        transform: translateZ(-300px);
    }

    body:hover main {

        transform: perspective(900px) rotateY(45deg) scaleZ(3);
    }
</style>

<main>
    <div></div>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#scale3d)scale3d

沿X/Y/Z三个轴绽放元素。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7828065.e355537e.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        transform-style: preserve-3d;
        transition: 2s;
        transform: perspective(900px) rotateY(60deg)
    }

    body:hover main {
        transform: perspective(600px) rotateY(60deg) scale3d(2, 2, 4);
    }

    div {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #f1c40f;
    }

    div.b {
        background: #8e44ad;
        transform: translateZ(-100px);
    }
</style>

<main>
    <div class="f"></div>
    <div class="b"></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#菜单缩放)菜单缩放

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7638319.e0db60be.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }

    ul {
        list-style: none;
        display: flex;
        justify-content: space-evenly;
        width: 200px;
    }

    ul li {
        position: relative;
    }

    ul li strong {
        background: #e67e22;
        color: #2c3e50;
        padding: 2px 20px;
        cursor: pointer;
        text-transform: uppercase;
    }

    ul li strong+div {
        border: solid 2px #e67e22;
        display: flex;
        flex-direction: column;
        padding: 10px 20px;
        position: absolute;
        transform-origin: left top;
        transform: scale(0);
        z-index: -1;
        transition: .6s;
        background: #e67e22;
    }

    ul li strong+div a {
        display: inline-block;
        padding: 5px;
        font-size: 1em;
        color: #2c3e50;
        text-decoration: none;
        text-transform: uppercase;
    }

    ul li:hover strong+div {
        transform: scale(1);
    }
</style>

<main>
    <ul>
        <li>
            <strong>VIDEO</strong>
            <div>
                <a href="">PHP</a>
                <a href="">hdcms</a>
                <a href="">laravel</a>
            </div>
        </li>
        <li>
            <strong>LIVE</strong>
            <div>
                <a href="">houdunren</a>
                <a href="">angular</a>
                <a href="">css3</a>
            </div>
        </li>
    </ul>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#相册放大)相册放大

下面是使用缩放开发相册放大效果的示例。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7641188.78385d23.gif)

```text
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: #ddd;
    }

    main {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    main div {
        height: 200px;
        width: 200px;
        background: white;
        border: solid 1px #ddd;
        transition: all .5s;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.5em;
        text-transform: uppercase;
        color: blueviolet;
        overflow: hidden;
        border: solid 3px #555;
        box-sizing: border-box;
    }

    main div img {
        height: 100%;
    }

    main:hover div {
        transform: scale(.8) translateY(-30px);
        cursor: pointer;
        filter: blur(15px);
    }

    main div:hover {
        transform: scale(1.6);
        color: white;
        filter: none;
        z-index: 2;
    }

    main div:hover::after {
        content: '';
        position: absolute;
        background: #000;
        width: 100%;
        height: 100%;
        z-index: -1;
        box-shadow: 0 0 5px rgba(0, 0, 0, .3);
    }
</style>

<main>
    <div>
        <img src="1.jpg" alt="">
    </div>
    <div> <img src="2.jpg" alt=""></div>
    <div> <img src="3.jpg" alt=""></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#旋转操作)旋转操作

使用CSS可以控制元素按照不同坐标轴进行旋转。

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#rotatex)rotateX

控制元素按照X轴进行旋转操作。

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#基本使用)基本使用

按水平轴发生旋转，如果旋转90deg 将不可见。

![image-20190902130125983](data:image/png;base64,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jQICsMap6IkAgSICArAIsyIECNQoIABrnIqeCBAoIiAAizArQoBAjQICsMap6IkAgSICArAIsyIECNQoIABrnIqeCBAoIiAAizArQoBAjQICsMap6IkAgSICArAIsyIECNQoIABrnIqeCBAoIiAAizArQoBAjQICsMap6IkAgSICArAIsyIECNQoIABrnIqeCBAoIiAAizArQoBAjQICsMap6IkAgSICArAIsyIECNQoIABrnIqeCBAoIiAAizArQoBAjQICsMap6IkAgSICArAI8+QqMv+UwbTm0rnp5IXTj9n4QO+3Zvm5s9JZrz055e/bthknTUvnvH5OmrdssO2UtPC0GU2tmSc/x4VaH/38B2bNnZZWXzInnbJm1vOf7IwpJ9D+mznlKLq74GVnz0xX/euZ6c6btqXbP7VldKG/+TenpvMvm5euOX99OnQwpXze7/3j6enkRWPB99Sj+9NNv7sx7dxyoHncohUz0pW3npFOmtcPrOFDKd196470qrcvSP/x11vStz+7rQnFd9+4Ip39C3NGa23buK+3fyDNmD2QPvmLDzb733fbGenlrxwLpvuHdqZXvnFuevTePemmd25M+Xju6S8v+OHodfI3H79vTdp4z7Ppc+/qn7P0rJnp2gvHn5P7e89nV6bTLjhp9LH79xxKt33k8XTfv+9s9l197+q09aF96YZf3TB6ztmvm9N73Ip0+ye3pDs/t210v2+6KXBi/tntptWkX1Xb3drAwEAanDXQBNvsBdOb//hzKOTAzHdo7//qGaNr//W/Wt6E34//e3f68lWb0v2372zCL58wbfpAc97bP3VqE34P3rkrffrXNqQvvX9TmrN4MOXwHNle9/uLm/Db/tj+JpS+deO2tOYNc5trtPU58tjj+frun4bfo9/b09S/42+fTMPDKf3GJ5anfGc6uvVbHv3RN1NLwB3g1Jp362rf9KfL0uDMgZSDaOTO5/b1W5oAPO/N89LFv7Uwfffm7WnZOTPTwQPD6QtXPNJc6wd3PJOuPH1VWv4zY3da562dl/buOpS++AePNuc8/oO96eYPPpbyXeHI9orenVbe/qkXopsf2Nt8f6h33Uvet6T5/qX8lUN7Re/Ob8fjB9KN73i4udT6rz+THrn32fSuz6xIr3/v4nTH3z35Ukp4bEcEDvunsCMrsowXJbDiwtnN477z5e3j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)

```text
article div:nth-child(2) {
    transform: rotateX(180deg);
}
```

下面是旋转89deg后，只会看到一条线。

![image-20190902130411118](data:image/png;base64,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)

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#父级透视)父级透视

当X旋转90度后无法看到元素，这时可以控制父级旋转从上看子元素。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7910515.b98ce26d.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -200px;
        margin-top: -200px;
        width: 400px;
        height: 400px;
        border: solid 5px silver;
        transform-style: preserve-3d;
        transform: perspective(900px) rotateX(-45deg);
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -100px;
        margin-top: -100px;
        width: 200px;
        height: 200px;
        transition: 1s;
    }

    div:nth-child(1) {
        background: #2ecc71;
    }

    main:hover div:nth-child(1) {
        transform: perspective(900px) rotateX(90deg) rotateY(25deg) rotateZ(45deg);
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#rotatey)rotateY

按垂直轴旋转，如果旋转90deg 将不可见。

![image-20190902130217250](data:image/png;base64,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)

```text
article div:nth-child(2) {
    transform: rotateY(180deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#rotatez)rotateZ

没Z轴旋转元素，效果就是沿X/Y轴的平面旋转。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7824624.322879f9.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        background: #f1c40f;
        perspective: 600px;
        transform: perspective(600px) rotateY(35deg);
        transition: 2s;
    }

    body:hover main {
        transform: perspective(600px) rotateY(35deg) rotateZ(160deg);
    }
</style>

<main>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#rotate)rotate

在X与Y轴平面旋转，效果与使用 `rotateZ` 相同。

![image-20190902130455308](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: rotate(90deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#rotate3d)rotate3d

同时设置X/Y/Z轴的旋转向量值来控制元素的旋转。

需要同时设置如下四个参数

```text
rotate3d(tx,ty,tz,angle)
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#只转x轴)只转X轴

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7825021.1b22c5f4.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        background: #f1c40f;
        perspective: 600px;
        transform: perspective(600px) rotateY(35deg);
        transition: 2s;
    }

    body:hover main {
        transform: perspective(600px) rotateY(35deg) rotate3d(1, 0, 0, -645deg);
    }
</style>

<main>
	<div></div>
</main>
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#只转y轴)只转Y轴

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7825124.3529e358.gif)

```text
body:hover main {
	transform: perspective(600px) rotateY(-645deg);
}
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#只转z轴)只转Z轴

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7825181.9bfa6d74.gif)

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#xy旋转)XY旋转

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7825275.8f4b452f.gif)

```text
body:hover main {
	transform: perspective(600px) rotateY(35deg) rotate3d(1, 1, 0, -645deg);
}
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#xz转换)XZ转换

加入适当的Z向量值，可增加元素沿Z轴旋转的力度。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7825690.7f9d943e.gif)

```text
body:hover main {
	transform: perspective(600px) rotateY(35deg) rotate3d(1, 0, .5, -245deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#参数顺序)参数顺序

可以同时设置多个旋转规则，顺序不同结果也会不同。

![image-20190902130625513](https://houdunren.gitee.io/note/assets/img/image-20190902130625513.0bba2c21.png)

```text
article div:nth-child(2) {
	transform: rotateX(30deg) rotateY(30deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#旋转文字)旋转文字

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7605104.746a27d4.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    main {
        margin: 0 auto;
        width: 400px;
        height: 50vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background: #535c68;
    }

    main div {
        color: #c7ecee;
        cursor: pointer;
    }

    main div strong {
        display: inline-block;
        width: 25px;
        height: 25px;
        margin: 0 3px;
        background: #000;
        border-radius: 50%;
        transition: 2s;
        color: white;
        text-align: center;
        box-shadow: 0 2px 10px rgba(0, 0, 0, .3);
    }

    main div strong:nth-of-type(1) {
        background: #f0932b;
    }

    main div strong:nth-of-type(2) {
        background: #6ab04c;
    }

    main div:hover strong:nth-of-type(1) {
        transform: rotate(360deg);
    }

    main div:hover strong:nth-of-type(2) {
        transform: rotate(-360deg);
    }
</style>

<main>
    <div>
        <strong>h</strong>ou<strong>d</strong>unren.com
    </div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#电子时钟)电子时钟

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7645507.b3731f7b.gif)

```text
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: #34495e;
    }

    main {
        position: relative;
        width: 400px;
        height: 400px;
        background: #34495e;
        border-radius: 50%;
        box-shadow: 0 0 10px rgba(0, 0, 0, .7);
    }

    main::before {
        position: absolute;
        left: 0;
        top: 0;
        content: '';
        width: 100%;
        height: 100%;
        border-radius: 50%;
        transform: scale(1.2);
        background: radial-gradient(at right, #27ae60, #e67e22, #e74c3c, #e67e22, #27ae60);
        z-index: -1;
    }

    main .line>div {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 10px;
        height: 95%;
        background: white;
    }

    main .line>div:nth-child(1) {
        transform: translate(-50%, -50%) rotate(0deg);
    }

    main .line>div:nth-child(2) {
        transform: translate(-50%, -50%) rotate(30deg);
    }

    main .line>div:nth-child(3) {
        transform: translate(-50%, -50%) rotate(60deg);
    }

    main .line>div:nth-child(4) {
        transform: translate(-50%, -50%) rotate(90deg);
    }

    main .line>div:nth-child(5) {
        transform: translate(-50%, -50%) rotate(120deg);
    }

    main .line>div:nth-child(6) {
        transform: translate(-50%, -50%) rotate(150deg);
    }

    main>div[class="mark"] {
        position: absolute;
        width: 100%;
        height: 100%;
        left: 0%;
        top: 0%;
        background: #34495e;
        border-radius: 50%;
        transform: scale(.8);
    }

    main>.point {
        width: 20px;
        height: 20px;
        background: #e74c3c;
        border-radius: 50%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 2;
    }

    main .hour {
        width: 15px;
        position: absolute;
        height: 25%;
        background: #95a5a6;
        left: 50%;
        bottom: 50%;
        transform: translate(-50%, 0);
    }

    main .minute {
        width: 8px;
        position: absolute;
        height: 35%;
        background: #3498db;
        left: 50%;
        bottom: 50%;
        transform-origin: left bottom;
        transform: translate(-50%, 0) rotate(60deg);
    }

    main .second {
        width: 2px;
        position: absolute;
        height: 35%;
        background: #f1c40f;
        left: 50%;
        bottom: 50%;
        transform-origin: left bottom;
        transform: translate(-50%, 0) rotate(90deg);
    }

    main:hover .second {
        transition: 10s;
        transform: rotate(260deg);
    }

    main .text {
        font-size: 1.2em;
        color: white;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, 20px);
        text-transform: uppercase;
        opacity: .5;
        text-align: center;
    }
</style>

<main>
    <section class="line">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </section>
    <div class="mark"></div>
    <div class="point"></div>
    <div class="hour"></div>
    <div class="minute"></div>
    <div class="second"></div>
    <div class="text">
        houdunren.com <br>
        向军大叔
    </div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#倾斜操作)倾斜操作

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#skewx)skewX

没X轴倾斜元素

![image-20190902151842782](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: skewX(30deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#skewy)skewY

沿Y轴倾斜元素

![image-20190902151909797](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY8AAAGPCAYAAACkmlznAAABRmlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8zAycDEwMOgyaCcmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgscyG/7BVLP8ytjPr/X1730SJM9SiAKyW1OBlI/wHi9OSCohIGBsYUIFu5vKQAxO4AskWKgI4CsueA2OkQ9gYQOwnCPgJWExLkDGTfALIFkjMSgWYwvgCydZKQxNOR2FB7QYDXx10h1CckyDHc08WVgHtJBiWpFSUg2jm/oLIoMz2jRMERGEqpCp55yXo6CkYGhpYMDKAwh6j+fAMcloxiHAixAjEGBosZQMGHCLF4oB+2yzEw8PchxNSA/hXwYmA4uK8gsSgR7gDGbyzFacZGEDb3dgYG1mn//38OZ2Bg12Rg+Hv9///f2////7uMgYH5FgPDgW8AEPRhmJCm9HoAABvnSURBVHgB7d0LvKVzuQfwB+N+ZzDDuIzSiBBSqSgqtxC5K6fbEZKoTqeOOo6je52KUEl35ZpLEkZy64KEhBAZl3Ef98u4O++aXSFjZu/Z6137//zXd30++9PYe633fZ7vb+n3WdZe78z2THMLNwIECBAgMASB2YdwX3clQIAAAQLTBJSHJwIBAgQIDFlAeQyZzAMIECBAQHl4DhAgQIDAkAWUx5DJPIAAAQIERk2PYOLEidP7tu8RIECAQJ8JbLzxxtPd2CuP6bL4JgECBAjMSEB5zEjHzwgQIEBgugLKY7osvkmAAAECMxJQHjPS8TMCBAgQmK6A8pgui28SIECAwIwEpvvbVi/2gBd71/3F7u/7BAgQIJBDYKi/ZeuVR45cTUmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxMSYAAgaIElEdRcRiGAAECOQSUR46cTEmAAIGiBJRHUXEYhgABAjkElEeOnExJgACBogSUR1FxGIYAAQI5BJRHjpxGdMrv73JzTLrwkRGdwckJEChLQHmUlUeR09z4x0fih++5OU7a9/a479YnipzRUAQI9FZAefTWO/XZLj3x/jjwrdfHud+6O/UehidAYPgCymP4hn11hGeejjjrG1PiG5tMij+f8kBf7W5ZAgSeFVAez1r40xAE7r7x8Tj+47fFEbtOjsmXTR3CI92VAIEaBJRHDSmO4A7X/fbhOHzHm+KUA+6Ih+95agQncWoCBHopoDx6qV3xuS466r5p74f8/gf3VLyl1QgQ+IeA8viHhP8dtsDjjzwdE798V3xzqxviqjMfGvbxHIAAgXIFlEe52aSd7I5rHouj97pl2tftzZ/dCBCoT0B51JdpMRt1Xn18q3kV0nk18vjDza9puREgUI2A8qgmynIX6bwPcuBG18cfmvdF3AgQqENAedSRY/FbdH4T65fNb2QdvuONcd1vHi5+XgMSIDBjAeUxYx8/7bLA5MsejSM+MDl+1nxG5O4bHu/y0R2OAIFeCSiPXkk7z/MELm8+nf6NTSfFWQdNiaefeuZ5P/MPBAiUL6A8ys+o6gnP/fbdzfshk+LSE+6vek/LEahNQHnUlmjCfe5vrtR70qdun3bl3hsucun3hBEauQ8FRvXhzlYuVKDzd4Z0vtbaZuHY4EOjY6Exnp6FRmUsAuGVhydBcQKXHN9c+r351d7zDnPp9+LCMRCBvwsoD0+FIgWeeuKZ+PWBU+LgzSbFFac+WOSMhiLQzwLKo5/TT7D7lEmPx3EfuzV+stvkuOXyRxNMbEQC/SGgPPoj5/RbXnvew/Gd7W+MUz97Zzxyn0u/pw/UAukFlEf6CPtrgQt/eu+0S7+f/6N7+2tx2xIoTEB5FBaIcWYu8NhDT8fpX7wzvv2OG+Lqs1z6feZi7kGg+wLKo/umjtgjgduueiyO2vOWOGbvW+POa136vUfsTkNgmoDy8ERIL/CXMx6MQ7e8Ic74v7viiaku/Z4+UAukEFAeKWIy5GAEfve9zqXfJ8Ufj3Hp98F4uQ+B4Qgoj+HoeWxxAg9NeTJ+sf8d8d2db4q//d6l34sLyEDVCCiPaqK0yHMFbr50avz4/ZPjhE/cFvfc9MRzf+TPBAh0QUB5dAHRIcoVuOzkB+Kgja+Psw+ZEuHK7+UGZbJ0AsojXWQGnhWBcw7tXPr9+vjTSQ/MysM9hgCBfxFQHv8C4h/rFbh38hNx4n/dFj96381x08VT613UZgR6IKA8eoDsFGUJXH/+I/G9d90UJ+93ezx455NlDWcaAkkElEeSoIzZfYGLjxu49PtvD7+n+wd3RAKVCyiPygO23owFnnzsmfjV1+6KQ7aYFFee7tLvM9byUwLPCiiPZy38qY8F7rru8Tj2I7fGkXvcErde6dLvffxUsPogBZTHIKHcrT8ErjnnoThs2xvjtM/fGVMfcOn3/kjdlrMi4C+JnhU1j6le4IIj7o1LT7w3XrVjxGqbV7/uCxYcO2HCC77nGwSeK+CVx3M1/JnAcwQea672/rvvRhz/sYgbL3rOD/yRAIFQHp4EBGYicNffIk77XMSvvhJx780zubMfE+gTAeXRJ0Fbc/gCf/tdxDF7RVx4RMRTLpc1fFBHSC2gPFLHZ/iRELj0+Igjd4u46oyROLtzEihDQHmUkYMpkgk83Hyu8NxvRvx834hb/pxseOMS6IKA8ugCokP0r8Btf4n4xX4RZx8U8eAd/etg8/4TUB79l7mNWxC45uzmP2XtHnHxMS0c3CEJFCigPAoMxUg5BZ5p/r6Qi46KOGqPiL+em3MHUxMYrIDyGKyU+xEYpMD9t0Wc9fWIU/aPuP3qQT7I3QgkE/AJ82SBGTePwOQ/RXS+Vtkkpn1Sfb5F8sxuUgIzE/DKY2ZCfk5gmAJ/OX3gV3v/dOIwD+ThBAoSUB4FhWGUegWefCzigh9FHLt3xPXn17unzfpHQHn0T9Y2LUDgnhsjzvhSxOmfj5hyfQEDGYHALAp4z2MW4TyMwHAEbvhDROdr9S0H3g+Za77hHM1jCfRewCuP3ps7I4F/Cvz55IHPh1xx6j+/5Q8EUggojxQxGbJmgUcfiPjtdyJO+HjETRfXvKndahJQHjWlaZfUAndeG3HqZyLO/GrEfbekXsXwfSCgPPogZCvmErjuNxFH7xnxh59EPP1krtlN2z8CyqN/srZpMoFLfjbwfsjVZyYb3Lh9IaA8+iJmS2YVeGhKxDmHRJz86Yhbr8i6hblrFFAeNaZqp+oEOsXRKZBzDo546K7q1rNQQgHlkTA0I/evwNW/HvhPWZcc178GNi9DQHmUkYMpCAxa4OmnmjfTf9q8qf7BiOvOG/TD3JFAVwWUR1c5HYxA7wTuu7X5td6vRfzygIg7/tq78zoTgY6Ay5N4HhBILnDzJRGdr1U3HbjUybwLJ1/I+CkEvPJIEZMhCcxc4MrTBt4PueznM7+vexAYroDyGK6gxxMoSOCJqRHn/yDiuI9ETLqwoMGMUp2A8qguUgsRiLh7UsTELzRfX2z+fAMRAt0XUB7dN3VEAsUITLqgeRWyT/Nq5IcRTzxazFgGqUBAeVQQohUIzEzgspOa90N2i+i8L+JGoBsCyqMbio5BIIHA1PsjfnNYxImfaH4769IEAxuxaAHlUXQ8hiPQfYE7rmk+G/K/Eb9uPiNyf/NZETcCsyKgPGZFzWMIVCBw7XkRRzWfUr/oyIhnnq5gISv0VEB59JTbyQiUJ3DxsQPvh1zTXDfLjcBgBZTHYKXcj0DFAg82V+o9u7li7y/+O+K2Kyte1GpdE1AeXaN0IAL5BW65POLnn8q/hw3aF1Ae7Rs7AwECBKoTUB7VRWohAgQItC+gPNo3dgYCBAhUJ6A8qovUQgQIEGhfQHm0b+wMBAgQqE5AeVQXqYUIECDQvoDyaN/YGQgQIFCdgPKoLlILESBAoH0B5dG+sTMQIECgOgHlUV2kFiJAgED7AsqjfWNnIECAQHUCyqO6SC1EgACB9gWUR/vGzkCAAIHqBJRHdZFaiAABAu0LKI/2jZ2BAAEC1Qkoj+oitRABAgTaF1Ae7Rs7AwECBKoTUB7VRWohAgQItC+gPNo3dgYCBAhUJ6A8qovUQgQIEGhfQHm0b+wMBAgQqE5AeVQXqYUIECDQvoDyaN/YGQgQIFCdgPKoLlILESBAoH0B5dG+sTMQIECgOgHlUV2kFiJAgED7AsqjfWNnIECAQHUCyqO6SC1EgACB9gWUR/vGzkCAAIHqBJRHdZFaiAABAu0LKI/2jZ2BAAEC1Qkoj+oitRABAgTaF1Ae7Rs7AwECBKoTUB7VRWohAgQItC+gPNo3dgYCBAhUJ6A8qovUQgQIEGhfQHm0b+wMBAgQqE5AeVQXqYUIECDQvoDyaN/YGQgQIFCdgPKoLlILESBAoH0B5dG+sTMQIECgOgHlUV2kFiJAgED7AsqjfWNnIECAQHUCyqO6SC1EgACB9gWUR/vGzkCAAIHqBJRHdZFaiAABAu0LKI/2jZ2BAAEC1Qkoj+oitRABAgTaF1Ae7Rs7AwECBKoTUB7VRWohAgQItC+gPNo3dgYCBAhUJ6A8qovUQgQIEGhfQHm0b5z+DG//XMQyq6VfwwIECHRRQHl0EbPWQ41dNWKLz0RssFfEgkvUuqW9CBAYioDyGIpWn993wpsjdj4sYu3t+xzC+gQIhPLwJBiSwGzNM2adnSN2+mbESusP6aHuTIBARQLKo6Iwe7nKwktHvPmjEW/7n4ilJvTyzM5FgEAJAqNKGMIMeQWWXTOi83XlaRF/PDpi6v15dzE5AQKDF/DKY/BW7jkDgVU3HXg/ZI2tZnAnPyJAoBoB5VFNlCO/yJzzRKz7nojtDowY/9qRn8cEBAi0J6A82rPt2yMvvkLExp8c+Or82Y0AgfoElEd9mRazUefVR+dVyLrvjZhz3mLGMggBAl0QUB5dQHSIGQus8fbm/ZBvR3TeF3EjQKAOAeVRR47FbzHvwhHr7Rax9Zeb385aq/hxDUiAwEwElMdMgPy4uwJLvaz5bMh+A58R6XxWxI0AgZwCyiNnbumn7nw6vfMp9XXeGdH51LobAQK5BPxrmyuv6qZde7uIdzbXy1q5uW6WGwECeQSUR56sqp10geZKvW9qrti7ZXPl3qWbK/i6ESBQvoDLk5SfUd9MuHTzd4Zs2XxdfebApU4emtI3q1uUQDoBrzzSRVb/wCu/ZeBXe9fatv5dbUggq4DyyJpc5XPP3rwmfvW7InY8NOKl61W+rPUIJBRQHglD66eRF1km4i0fi9jsvyOWXKmfNrcrgbIFvOdRdj6m+7vAcmtHdL6uOLV5P+SoiEcfREOAwEgKeOUxkvrOPWSBV2w2cOn31bcc8kM9gACBLgoojy5iOlRvBOaaL+J174vY9msRK7y6N+d0FgIEni+gPJ7v4Z8SCYxeMWKTfSM2+kTEYssnGtyoBCoQUB4VhNjvK6y4bsT2B0W89t0Ro+budw37E+iNgPLojbOz9EDglVsPvB+yyiY9OJlTEOhzAeXR50+A2tafb5GI9XeP2OqLEeNeWdt29iFQjoDyKCcLk3RRYMzKEZvvH7HhRyIWGtPFAzsUAQLTBJSHJ0LVAi9748ClTtbZqVlztqpXtRyBngooj55yO9lICay9Q3Pp9+avwp2wwUhN4LwE6hJQHnXlaZsZCCy4VMQGe0dscUDE2FVmcEc/IkBgpgIuTzJTIneoTWCZ1SM6X1edMXDp94fvqW1D+xBoX8Arj/aNnaFQgZdvNPCrvWtuU+iAxiJQsIDyKDgco7UvMMecEa/ZJWKHgyNe8vr2z+cMBGoRUB61JGmPYQksumzEWz8esemnIpZ4ybAO5cEE+kLAex59EbMlByuw/DoRna/LTxl4P+Sxhwb7SPcj0F8CyqO/8p6lbcdOmDBLj8v8oLHNyuvt+lScc8jdccER92ZexewEWhHwn61aYXXQGgTmXWiO2HTfJWO3ny0fE960QA0r2YFA1wSUR9coHahWgaVXnSd2/tYysf3Xl27eD5mr1jXtRWBIAspjSFzu3M8Cq26yYHzolPHx1o8u0Vz63bVO+vm5YPcI5eFZQGCIAm/YdbHY54wVY+3tFh7iI92dQD0CyqOeLG3SQ4EFlxwVWx4wJt7/k+VixXWbvxfXjUCfCSiPPgvcut0VWG7teePd3182tv7C2Fh0XPOJQzcCfSKgPPokaGu2K/DKrRaa9p+y3rTn4u2eyNEJFCKgPAoJwhgVCDTvoW/wodGx98QVY40tF6pgISsQeHEB5fHiNn5CYJYEFltuznjHl8bGv31vXCy75ryzdAwPIlC6gPIoPSHzpRV4yevmj38/crnYYv+lYoHRLuaQNkiDT1dAeUyXxTcJdE/gVTss0rwfMj5e//7FundQRyIwwgLKY4QDcPr+EJhz3tljo/9YIvY8eYVYZaMF+2NpW1YtoDyqjtdypQksudLcscNBS8dOhy4TY18+d2njmYfAoAWUx6Cp3JFA9wRW3nCB2P2EFWKTTy4Zcy/gX8PuyTpSrwQ8a3sl7TwEpiOw7rsXjX1+tWK85p2LTuenvkWgXAHlUW42JusTgfkWmSM2+/SS8YFjl4+V1p+/T7a2ZnYB5ZE9QfNXI7DMavPEuw4bF9t9dekYPd6l36sJttJFlEelwVorr8ArNlsw9jp1fLx5n9ExxyiXfs+bZN2TK4+687VdYoH1d1t82vsha23j0u+JY6x2dOVRbbQWq0FgoTGj4u2fHRPv/fGyMf41Lv1eQ6a17KA8aknSHlULrLDOfPGeHy4bW31uTCy8tEu/Vx12kuWUR5KgjEmgI7DmOxaedqmTN+7u0u+eESMroDxG1t/ZCQxZYPY5ZosN9x4dHz5tfKy2uUu/DxnQA7oioDy6wuggBHovsPgKc8W2Xxkbu3xnXIxbY57eD+CMfS2gPPo6fsvXIPDS9eaPXY9ePt6231Ix/2Jz1LCSHRIIKI8EIRmRwGAEXr1T59LvK8br3uvS74Pxcp/hCSiP4fl5NIGiBOaaf/bY+D+XiD1OWiFe/pYFiprNMHUJKI+68rQNgWkCYybMHTsevMy0r6WaP7sR6LaA8ui2qOMRKEig8+rjg82rkM6rkbnm8697QdGkH8WzKX2EFiAwc4HO+yCdS7+v07wv4kagGwLKoxuKjkEggUDnN7E2b34ja9ejl4uXvsGl3xNEVvSIyqPoeAxHoPsC49aYN3Y5fFxs03xGZPHlXfq9+8L9cUTl0R8525LACwRWbz6d/uHTx8eGHx4ds/l/ghf4+MaMBTxlZuzjpwSqF3jjHgOXfl9za5d+rz7sLi6oPLqI6VAEsgos0lypd6vPj5l25d7lX+XS71lz7OXco3p5MuciQKBsgc7fGeLvDSk7o1Km88qjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCyqOUJMxBgACBRALKI1FYRiVAgEApAsqjlCTMQYAAgUQCyiNRWEYlQIBAKQLKo5QkzEGAAIFEAsojUVhGJUCAQCkCo4YyyMSJE4dyd/clQIAAgUoFvPKoNFhrESBAoE0B5dGmrmMTIECgUgHlUWmw1iJAgECbAsqjTV3HJkCAQKUCyqPSYK1FgACBNgVme6a5tXkCxyZAgACB+gS88qgvUxsRIECgdQHl0TqxExAgQKA+AeVRX6Y2IkCAQOsCyqN1YicgQIBAfQLKo75MbUSAAIHWBf4fiMTAf9LNS84AAAAASUVORK5CYII=)

```text
article div:nth-child(2) {
	transform: skewY(30deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#skew)skew

同时设置X/Y轴倾斜操作，不指定第二个参数时Y轴倾斜为零。

![image-20190902152104810](data:image/png;base64,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)

```text
article div:nth-child(2) {
	transform: skew(30deg, 30deg);
}
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#按钮特效)按钮特效

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7636893.3e63a4ce.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }

    main .btn {
        display: block;
        height: 30px;
        width: 150px;
        border: solid 2px #e74c3c;
        background: none;
        color: white;
        position: relative;
        text-align: center;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        cursor: pointer;
        box-shadow: 0 3px 8px rgba(0, 0, 0, .3);
    }

    main .btn::before {
        transition: all .8s;
        align-self: center;
        content: '';
        position: absolute;
        width: 0;
        height: 100%;
        background: #e74c3c;
        z-index: -1;
        transform: skewX(-45deg);
    }

    main .btn:hover::before {
        width: 200%;
    }
</style>

<main>
    <a class="btn">
        HOUDUNREN
    </a>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#立体按钮)立体按钮

![image-20190906135344963](https://houdunren.gitee.io/note/assets/img/image-20190906135344963.f9a01bf5.png)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    body {
        background: #2c3e50;
        width: 100vw;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .btn {
        color: #ecf0f1;
        text-decoration: none;
        width: 200px;
        height: 40px;
        background: #e74c3c;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        transform: skewX(25deg) rotate(-15deg);
        letter-spacing: .5em;
        text-transform: uppercase;
        font-weight: bold;
    }

    .btn::before {
        content: '';
        width: 10px;
        height: 100%;
        left: -10px;
        background: #000;
        position: absolute;
        transform: skewY(-45deg) translate(0, 5px);
    }

    .btn::after {
        content: '';
        width: 100%;
        height: 10px;
        bottom: -10px;
        background: #000;
        position: absolute;
        transform: skewX(-45deg) translate(-5px, 0);
    }
</style>

<a href="" class="btn"> houdunren</a>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#变形基点)变形基点

使用 `transform-origin` 设置元素的X/YZ操作的基点，用于控制旋转、倾斜等操作。

- 旋转默认以元素中心进行旋转，改变基点后可控制旋转点位置
- 元素移动不受变形基点所影响

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#平面旋转)平面旋转

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7932268.f587aaa0.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -200px;
        margin-top: -200px;
        width: 400px;
        height: 400px;
        border: solid 5px silver;
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -100px;
        margin-top: -100px;
        width: 200px;
        height: 200px;
        transform-origin: right bottom;
    }

    div:nth-child(1) {
        background: #2ecc71;
    }

    div:nth-child(2) {
        background: #e67e22;
        transition: 1s;
    }

    main:hover div:nth-child(2) {
        transform: rotate(-45deg);
    }
</style>

<main>
    <div></div>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#倾斜控制)倾斜控制

参考右上角控制倾斜。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7932114.ce3ee8cd.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -200px;
        margin-top: -200px;
        width: 400px;
        height: 400px;
        border: solid 5px silver;
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -100px;
        margin-top: -100px;
        width: 200px;
        height: 200px;
        transform-origin: top left;
    }

    div:nth-child(1) {
        background: #fff;
    }

    div:nth-child(2) {
        background: #e67e22;
        transition: 1s;
    }

    main:hover div:nth-child(2) {
        transform: skew(45deg);
    }
</style>

<main>
    <div></div>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#三维旋转)三维旋转

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7932004.12f1c62a.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -200px;
        margin-top: -200px;
        width: 400px;
        height: 400px;
        border: solid 5px silver;
        transform-style: preserve-3d;
        transform: perspective(900px) rotateY(95deg);
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -100px;
        margin-top: -100px;
        width: 200px;
        height: 200px;
        transform-origin: center center 200px;
    }

    div:nth-child(1) {
        background: #2ecc71;
    }

    div:nth-child(2) {
        background: #e67e22;
        transition: 1s;
    }

    main:hover div:nth-child(2) {
        transform: rotateY(360deg);
    }
</style>

<main>
    <div></div>
    <div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#新年贺卡)新年贺卡

下面是通过设置基点来制作贺卡的效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7939019.ed7152ba.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    main {
        width: 300px;
        height: 200px;
        transform-style: preserve-3d;
        transform: perspective(600px) rotateX(35deg) rotateY(15deg);
    }

    .card {
        width: 300px;
        height: 200px;
        background: #e67e22;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 3em;
        color: whitesmoke;
        position: relative;

    }

    .card::before,
    .card::after {
        transition: 1s;
        background: #e74c3c;
        line-height: 4em;
    }

    .card::before {
        content: '新年';
        width: 150px;
        height: 100%;
        left: 0px;
        top: 0;
        text-align: right;
        position: absolute;
        transform-origin: left bottom;
    }

    .card::after {
        content: '快乐';
        width: 150px;
        height: 100%;
        left: 150px;
        top: 0;
        position: absolute;
        transform-origin: right bottom;
    }

    .card:hover::before {
        transform: rotateY(-179deg);
    }

    .card:hover::after {
        transform: rotateY(179deg);
    }
</style>

<main>
    <div class="card">houdunren</div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#动感菜单)动感菜单

为了让大家清楚理解，下面把思路给大家解析一下。

![image-20190905200803607](https://houdunren.gitee.io/note/assets/img/image-20190905200803607.95e393c8.png)

![image-20190909154507295](https://houdunren.gitee.io/note/assets/img/image-20190909154507295.cfc5d8b8.png)

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#父级有宽度)父级有宽度

设置父级ul有宽度，每层都是居中对齐。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8015150.745be0aa.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        list-style: none;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #2c3e50;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    nav {
        width: 400px;
        height: 400px;
        background: transparent;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;

    }

    nav::after {
        content: '向军老师';
        color: #ecf0f1;
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 2em;
        font-weight: bold;
        text-shadow: 3px 3px 0px #34495e;
        z-index: 1;
    }

    nav::before {
        content: '';
        width: 200px;
        height: 200px;
        background: #e74c3c;
        border-radius: 50%;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        z-index: 1;
    }

    nav:hover ul {
        transform: scale(1);
    }

    ul {
        width: 300px;
        height: 300px;
        transform: scale(0);
        transition: .5s;
    }

    ul li {
        width: 80px;
        height: 80px;
        background: #e74c3c;
        border-radius: 50%;
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 2.5em;
        color: white;
        transition: 1s;
        transform-origin: 150px 150px;
        box-shadow: 0 0 15px rgba(0, 0, 0.8);
    }

    ul li span {
        transition: 1s;
    }

    nav:hover li:nth-child(1) {
        transform: rotate(40deg);
    }

    nav:hover li:nth-child(1)>span {
        transform: rotate(1040deg);
    }

    nav:hover li:nth-child(2) {
        transform: rotate(80deg);
    }

    nav:hover li:nth-child(2)>span {
        transform: rotate(1000deg);
    }

    nav:hover li:nth-child(3) {
        transform: rotate(120deg);
    }

    nav:hover li:nth-child(3)>span {
        transform: rotate(960deg);
    }

    nav:hover li:nth-child(4) {
        transform: rotate(160deg);
    }

    nav:hover li:nth-child(4)>span {
        transform: rotate(720deg);
    }

    nav:hover li:nth-child(5) {
        transform: rotate(200deg);
    }

    nav:hover li:nth-child(5)>span {
        transform: rotate(880deg);
    }

    nav:hover li:nth-child(6) {
        transform: rotate(240deg);
    }

    nav:hover li:nth-child(6)>span {
        transform: rotate(1680deg);
    }

    nav:hover li:nth-child(7) {
        transform: rotate(280deg);
    }

    nav:hover li:nth-child(7)>span {
        transform: rotate(1920deg);
    }

    nav:hover li:nth-child(8) {
        transform: rotate(320deg);
    }

    nav:hover li:nth-child(8)>span {
        transform: rotate(2200deg);
    }

    nav:hover li:nth-child(9) {
        transform: rotate(360deg);
    }

    nav:hover li:nth-child(9)>span {
        transform: rotate(2520deg);
    }
</style>

<nav>
    <ul>
        <li><span><i class="fa fa-address-book" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-adjust" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bars" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-book" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bug" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-compress" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-ban" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-beer" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bus" aria-hidden="true"></i></span></li>
    </ul>
</nav>
```

#### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#父级无宽度)父级无宽度

下面代码父级 UL 没有设置宽度，而是使用边框撑开了空间的效果，基本原理和上面一样。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7667552.863eb27b.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        background: #34495e;
    }

    nav {
        position: absolute;
        margin: 0 auto;
        left: 50%;
        top: 50%;
        width: 180px;
        height: 180px;
        background: #34495e;
        border-radius: 50%;
        text-align: center;
        line-height: 180px;
        color: #2c3e50;
        font-weight: bold;
        font-size: 2em;
        background: #f1c40f;
        box-shadow: 0 0 15px rgba(0, 0, 0, .5);
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    nav strong {
        position: absolute;
    }

    nav:hover ul {
        transform: scale(1.3);
    }

    ul {
        transform: scale(0);
        border: 150px solid transparent;
        transition: .5s;
        cursor: pointer;
        z-index: -1;
    }

    ul li {
        position: absolute;
        top: -100px;
        left: -100px;
        width: 50px;
        height: 50px;
        background: #e67e22;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-content: center;
        line-height: 1.5em;
        transition: all 1s;
        transform-origin: 100px 100px;
        box-shadow: 0 0 15px rgba(0, 0, 0, .8);
    }

    ul li span {
        transition: all 1s;
    }

    nav:hover ul li:nth-child(1) {
        transform: rotate(40deg);
    }

    nav:hover ul li:nth-child(1) span {
        transform: rotate(1040deg);
    }

    nav:hover ul li:nth-child(2) {
        transform: rotate(80deg);
    }

    nav:hover ul li:nth-child(2) span {
        transform: rotate(1000deg);
    }

    nav:hover ul li:nth-child(3) {
        transform: rotate(120deg);
    }

    nav:hover ul li:nth-child(3) span {
        transform: rotate(1680deg);
    }

    nav:hover ul li:nth-child(4) {
        transform: rotate(160deg);
    }

    nav:hover ul li:nth-child(4) span {
        transform: rotate(560deg);
    }

    nav:hover ul li:nth-child(5) {
        transform: rotate(200deg);
    }

    nav:hover ul li:nth-child(5) span {
        transform: rotate(520deg);
    }

    nav:hover ul li:nth-child(6) {
        transform: rotate(240deg);
    }

    nav:hover ul li:nth-child(6) span {
        transform: rotate(480deg);
    }

    nav:hover ul li:nth-child(7) {
        transform: rotate(280deg);
    }

    nav:hover ul li:nth-child(7) span {
        transform: rotate(440deg);
    }

    nav:hover ul li:nth-child(8) {
        transform: rotate(320deg);
    }

    nav:hover ul li:nth-child(8) span {
        transform: rotate(400deg);
    }

    nav:hover ul li:nth-child(9) {
        transform: rotate(360deg);
    }

    nav:hover ul li:nth-child(9) span {
        transform: rotate(720deg);
    }
</style>


<nav>
    向军大叔
    <ul>
        <li><span><i class="fa fa-address-book" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-adjust" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bars" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-book" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bug" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-compress" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-ban" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-beer" aria-hidden="true"></i></span></li>
        <li><span><i class="fa fa-bus" aria-hidden="true"></i></span></li>
    </ul>
</nav>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#透视景深)透视景深

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#perspective)perspective

- 使用 `perspective` 来控制元素的透视景深
- `perspective` 规则为舞台元素控制景深， `perspective` 属性为控制单个元素

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#舞台透视)舞台透视

`perspective` 规则用于将父级整个做为透视元素，会造成里面的每个子元素的透视是不一样的。就像现实中摆一排杯子，是使用统一透视的，每个杯子的透视不一样，造成有大有小。

![image-20190902164314985](data:image/png;base64,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)

```text
<style>
    article {
        margin: 0 auto;
        margin-top: 150px;
        width: 400px;
        height: 200px;
        position: relative;
        border: solid 5px silver;
        perspective: 200px;
    }

    article div {
        width: 100px;
        height: 100px;
        background: blueviolet;
        box-sizing: border-box;
        margin-right: 80px;
        float: left;
        transform: rotateY(60deg);
    }
</style>

<article>
	<div></div>
	<div></div>
</article>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#单独透视)单独透视

`perspective` 函数用于为元素设置单独透视，下面是为元素单独设置透视参数，每个元素的透视效果是一样的。

![image-20190902164423476](data:image/png;base64,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)

```text
article div {
    width: 100px;
    height: 100px;
    background: blueviolet;
    box-sizing: border-box;
    margin-right: 80px;
    float: left;
    transform: perspective(100px) rotateY(60deg);
}
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#_3d透视)3D透视

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#transform-style)transform-style

使用 `transform-style` 用于控制3d透视。

- 应用于舞台即变形元素的父级元素
- 设置 `overflow:visible` 时 `preserve-3d` 才无效

| 选项        | 说明       |
| ----------- | ---------- |
| flat        | 2D平面舞台 |
| preserve-3d | 3D透视舞台 |

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#效果体验)效果体验

下面是设置`3D`舞台后看到的效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7770216.9f7c32fd.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    body {
        background: #34495e;

    }

    main {
        position: relative;
        width: 100vw;
        height: 100vh;
    }

    div {
        position: absolute;
        left: 50%;
        top: 50%;
        height: 200px;
        width: 200px;
        transition: 1s;
        background: #e67e22;
        transform-style: preserve-3d;

    }

    div img {
        height: 80%;
        transform: perspective(500px) translateZ(100px);
    }

    div:hover {
        transform: perspective(600px) rotateY(50deg);
    }
</style>

<main>
    <div>
        <img src="5.jpg" alt="">
    </div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#三维图集)三维图集

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7838254.e56c8d56.gif)

```text
<style>
    body {
        background: #34495e;
    }

    main {
        position: absolute;
        width: 400px;
        height: 200px;
        left: 50%;
        top: 50%;
        transform-style: preserve-3d;
        transform-origin: center center -300px;
        transform: translate(-50%, -50%) rotateX(-45deg);
        transition: 2s;
    }

    body:hover main {
        transform: translate(-50%, -50%) rotateX(-45deg) rotateY(900deg);
    }

    div {
        position: absolute;
        width: 100%;
        height: 100%;
        transform-origin: center center -300px;
        overflow: hidden;
    }

    div img {
        height: 100%;
    }

    div:nth-child(1) {
        transform: rotateY(60deg);
    }

    div:nth-child(2) {
        transform: rotateY(120deg);
    }

    div:nth-child(3) {
        transform: rotateY(180deg);
    }

    div:nth-child(4) {
        transform: rotateY(240deg);
    }

    div:nth-child(5) {
        transform: rotateY(300deg);
    }

    div:nth-child(6) {
        transform: rotateY(360deg);
    }
</style>

<main>
    <div>
        <img src="5.jpg" alt="">
    </div>
    <div>
        <img src="1.jpg" alt="">
    </div>
    <div>
        <img src="3.jpg" alt="">
    </div>
    <div>
        <img src="5.jpg" alt="">
    </div>
    <div>
        <img src="1.jpg" alt="">
    </div>
    <div>
        <img src="3.jpg" alt="">
    </div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#观看视角)观看视角

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#perspective-origin)perspective-origin

`perspective-origin`用于控制视线的落点，就像我们眼睛看物体时的聚焦点。可以理解眼镜看物体的位置，比如看一台汽车，是在看车头左边看还是车头右边看。

需要设置 `perspective` 透视后才可以看到效果。

- 一般设置在舞台元素上来控制子元素

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#位置参数)位置参数

| 取值     | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| *x-axis* | 定义该视图在 x 轴上的位置。默认值：50%。可能的值：left、center、right、length、% |
| *y-axis* | 定义该视图在 y 轴上的位置。默认值：50%。可能的值：top、center、bottom、length、% |

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#效果体验-2)效果体验

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8191457.7ad994e0.gif)

```text
<style>
    body {
        background: #2c3e50;
        display: flex;
        width: 100vw;
        height: 100vh;
        justify-content: center;
        align-items: center;
    }

    main {
        border: solid 2px silver;
        width: 400px;
        height: 200px;
        transform-style: preserve-3d;
        transform: rotateY(65deg);
        perspective-origin: right bottom;
        perspective: 900px;
        transition: 2s;
    }

    body:hover main {
        perspective-origin: 1200% bottom;
        /* transform: rotateY(-65deg); */
    }

    div {
        position: absolute;
        width: 200px;
        height: 200px;
        transform: rotateY(60deg);
        overflow: hidden;
    }

    div>img {
        height: 100%;
    }

    div:nth-child(1) {
        background: #e67e22;
    }

    div:nth-child(2) {
        background: #27ae60;
        transform: rotateY(60deg) translateZ(-200px);
    }
</style>
<main>
    <div><img src="3.jpg" alt=""></div>
    <div><img src="5.jpg" alt=""></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#立方体)立方体

![image-20190906230252608](https://houdunren.gitee.io/note/assets/img/image-20190906230252608.e4e08e3d.png)

效果如下

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-7784965.483715b7.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
        list-style: none;
    }

    body {
        background: #34495e;
    }

    main {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 200px;
        height: 200px;
        transform-style: preserve-3d;
        transform-origin: 50% 50% 50px;
        transform: translate(-50%, -50%) rotateY(0deg);
        transition: 2s;
    }

    main:hover {
        transform: translate(-50%, -50%) rotate3d(1, 1, 0, 180deg);
    }

    div {
        position: absolute;
        width: 200px;
        height: 200px;
        background: #000;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 4em;
    }

    div:nth-child(1) {
        transform-origin: right;
        background: #1abc9c;
        transform-origin: bottom;
        transform: translateY(-200px) rotateX(-90deg);
        opacity: .8;
    }

    div:nth-child(2) {
        transform-origin: right;
        background: #27ae60;
        transform-origin: top;
        transform: translateY(200px) rotateX(90deg);
        opacity: .8;
    }

    div:nth-child(3) {
        transform-origin: bottom;
        background: #e67e22;
        transform-origin: right;
        transform: translateX(-200px) rotateY(90deg);
        opacity: .8;
    }

    div:nth-child(4) {
        transform-origin: top;
        background: #8e44ad;
        transform-origin: left;
        transform: translateX(200px) rotateY(-90deg);
        opacity: .8;
    }

    div:nth-child(5) {
        transform-origin: left bottom;
        background: #ecf0f1;
        opacity: .8;
    }

    div:nth-child(6) {
        transform-origin: left bottom;
        background: #ecf0f1;
        opacity: .5;
        transform: translateZ(200px);
    }
</style>

<main>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>后盾人</div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/12 变形动画.html#隐藏背面)隐藏背面

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#backface-visibility)backface-visibility

使用 `backface-visibility` 用于控制是否可以看到元素的背面。

- 一般设置在元素上而不是舞台元素上
- 需要舞台元素（父级元素）设置 `transform-style: preserve-3d`

| 选项    | 说明     |
| ------- | -------- |
| visible | 背面可见 |
| hidden  | 背面隐藏 |

### [#](https://houdunren.gitee.io/note/css/12 变形动画.html#翻转卡片)翻转卡片

下面使用隐藏背面与透视技术制作的翻转卡片效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8212174.f8db6c8c.gif)

```html
<script src='https://code.jquery.com/jquery-3.3.1.slim.min.js'></script>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
<style>
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }

    main {
        position: absolute;
        width: 100vw;
        height: 100vh;
        transition: 2s;
        transform-style: preserve-3d;
    }

    main.login {
        transform: perspective(900px) rotateY(0deg);
    }

    main.register {
        transform: perspective(900px) rotateY(180deg);
    }

    div {
        position: absolute;
        width: 100%;
        height: 100%;
        font-size: 5em;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        backface-visibility: hidden;
        transition: 2s;
        text-transform: uppercase;
        color: white;
    }

    div span {
        text-transform: lowercase;
        letter-spacing: .2em;
        font-size: .2em;
        color: #2c3e50;
    }

    div:nth-child(1) {
        background: #2ecc71;
        transform: rotateY(0deg);
    }

    div:nth-child(2) {
        background: #e74c3c;
        transform: rotateY(180deg);
    }

    nav {
        position: absolute;
        width: 100%;
        height: 100%;
        z-index: 99;
        text-align: center;
        display: flex;
        align-items: flex-end;
        justify-content: center;
        padding-bottom: 30px;
    }

    nav a {
        padding: 10px;
        text-decoration: none;
        font-size: 1em;
        background: #000;
        color: white;
        margin-right: 10px;
        cursor: pointer;
        left: 0;
        top: 0;
    }
</style>

<main>
    <div>
        <i class="fa fa-home" aria-hidden="true"></i>
        login
        <span>houdunren.com</span>
    </div>
    <div>
        <i class="fa fa-user" aria-hidden="true"></i>
        register
        <span>houdunren.com</span>
    </div>
</main>
<nav>
    <a href="javascript:;" onclick="change('login')">登录</a>
    <a href="javascript:;" onclick="change('register')">注册</a>
</nav>
<script>
    function change(t) {
        switch (t) {
            case 'login':
                $("main").removeClass().addClass('login');
                break;
            case 'register':
                $("main").removeClass().addClass('register');
                break;
        }
    }
</script>
```



# 过度延迟

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#基础知识)基础知识

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

默认情况下CSS属性的变化是瞬间完成的（其实也有时间只是毫秒级的，人眼很难感知到），而使用本章节学习的CSS过渡可以控制让变化过程平滑。

> 有关变形动画已经讲的很丰富了，请在 [后盾人](https://www.houdunren.com/) 查看相应章节。

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#动画属性)动画属性

不是所有css属性都有过渡效果，[查看支持动画的CSS属性](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) ，一般来讲有中间值的属性都可以设置动画如宽度、透明度等。

**案例分析**

下面例子中边框的变化是没有中间值的，所以没有过渡效果。但线宽度是数值类型有中间值所以会有过渡效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8732866.e1e2adfa.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #fff;
        border: solid 20px #ddd;
        transition: 2s;
    }

    div:hover {
        border-radius: 50%;
        border: dotted 60px #ddd;
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#元素状态)元素状态

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#初始形态)初始形态

指当页面加载后的样式状态，下面是表单设置的初始样式。

![image-20190914111828873](data:image/png;base64,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)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 20px;
    }

    input {
        border: solid 5px #e67e22;
        height: 60px;
        width: 100%;
        margin-bottom: 20px;
    }

    input:checked {
        position: relative;
        width: 60px;
        height: 60;
        border: none;
    }

    input:checked::before {
        content: '⩗';
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 3em;
        position: absolute;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        box-sizing: border-box;
        background: #3498db;
    }
</style>

<input type="text">
<input type="checkbox" checked>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#变化形态)变化形态

指元素由初始状态变化后的状态，比如鼠标放上、表单获得焦点后的形态。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8529268.4caf2ee6.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
         padding: 20px;
    }

    input {
        border: solid 5px #e67e22;
        height: 60px;
        width: 100%;
        margin-bottom: 20px;
        transition: 2s;
    }

    input:hover {
        border: solid 5px #000 !important;
    }

    input:focus {
        background: #e67e22;
    }

    input:checked {
        position: relative;
        width: 60px;
        height: 60;
        border: none;
    }

    input:checked::before {
        content: '⩗';
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 3em;
        position: absolute;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        box-sizing: border-box;
        background: #3498db;
    }
</style>

<input type="text">
<input type="checkbox" checked>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transition-property)transition-property

用于设置哪些属性应用过渡效果。

- 默认值为`all` 即所有属性都发生过渡效果
- 多个属性使用逗号分隔

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#属性设置)属性设置

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8703495.c1eef020.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #e67e22;
        border-radius: 50%;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 3s;
    }

    main:hover div {
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#禁用属性)禁用属性

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8688852.61c4f1a2.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 200px;
        height: 200px;
        background: #e74c3c;
        transition-property: background, transform;
        transition-duration: 2s;
        margin-bottom: 50px;
    }

    main:hover div{
        transform: scale(1.5) rotate(180deg);
        background: #9b59b6;
    }

    div:last-child {
        transition-property: none;
    }
</style>

<main>
	<div></div>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transitionend)transitionend

用于控制过渡结束后执行的JS事件，简写属性会触发多次如 `border-radius` 会触发四次事件，不难理解因为可以为`border-bottom-left-radius` 等四个属性独立设置过渡，所以就会有四次事件。

| 属性          | 说明                          |
| ------------- | ----------------------------- |
| propertyName  | 结束过渡样式                  |
| elapsedTime   | 过渡需要的时间                |
| pseudoElement | 过渡的伪元素                  |
| isTrusted     | true:用户触发，false:脚本触发 |

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8785908.6fb16183.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        width: 100vw;
        height: 100vh;
        background: #34495e;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 200px;
        height: 200px;
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        flex-wrap: nowrap;
    }

    div::before {
        content: '后盾人';
        font-size: 3em;
        color: #2c3e50;
        background: #95a5a6;
        width: 200px;
        height: 200px;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 10%;
        transition-duration: 2s;
        cursor: pointer;
    }

    div:hover::before {
         transition-duration: 1.5s;
				 border-radius: 50%;
				 background: #f1c40f;
         transform: rotate(360deg);
    }

    div::after {
        content: 'houdunren.com';
        text-transform: uppercase;
        position: absolute;
        bottom: -60px;
        font-size: 2em;
        color: #95a5a6;
        text-align: center;
        transform: translateX(-999px) skew(45deg);
        transition-duration: 1s;
    }

    div.move::after {
        transform: translateX(0px) skew(0deg);
    }
</style>

<main>
    <div>

    </div>
</main>
<script>
    document.querySelector('div').addEventListener('transitionend', function (e) {
        console.log(e);
        document.querySelector('div').className = 'move';
    })
</script>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transition-duration)transition-duration

用于设置过渡时间，需要注意以下几点

- 可使用单位为 ms毫秒、s秒
- 默认值为0s不产生过渡效果
- 一个值时，所有属性使用同样的时间
- 二个值时，奇数属性使用第一个，偶数属性使用第二个
- 变化属性数量大于时间数量时，后面的属性再从第一个时间开始重复使用

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#统一时间)统一时间

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8698225.d8694625.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #34495e;
        border-radius: 50%;
        opacity: 0.2;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 3s;
    }

    div:hover {
        opacity: 1;
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#两个时间)两个时间

下面共有四个属性并设置了两个时间值，1,3属性使用第一个值，2,4属性使用第二个值。

```text
...
div {
  width: 150px;
  height: 150px;
  background-color: #34495e;
  border-radius: 50%;
  opacity: 0.2;
  transition-property: background-color, transform, opacity, border-radius;
  transition-duration: 200ms, 5s;
}
...
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#多个时间)多个时间

下面共有四个属性并设置了三个时间值，1,2,3属性使用1,2,3时间值，第四个属性再从新使用第一个时间值。

```text
...
div {
  width: 150px;
  height: 150px;
  background-color: #34495e;
  border-radius: 50%;
  opacity: 0.2;
  transition-property: background-color, transform, opacity, border-radius;
  transition-duration: 200ms, 5s, 2s;
}
...
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#不同时间)不同时间

可以为初始与变化状态设置不同的时间。

下面是将`hover` 设置为3s，当鼠标放上时变化时间为3s。为初始设置为1s即表示变化到初始状态需要1s。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8712618.11e93849.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #e67e22;
        border-radius: 50%;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 1s;
    }

    div:hover {
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
        transition-duration: 3s;
    }
</style>

<main>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transition-timing-function)transition-timing-function

用于设置过渡效果的速度，可在 [https://cubic-bezier.com](https://cubic-bezier.com/) 网站在线体验效果差异。

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#默认参数)默认参数

| 值                            | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| linear                        | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。 |
| ease                          | 开始慢，然后快，慢下来，结束时非常慢（cubic-bezier(0.25,0.1,0.25,1)） |
| ease-in                       | 开始慢，结束快（等于 cubic-bezier(0.42,0,1,1)）              |
| ease-out                      | 开始快，结束慢（等于 cubic-bezier(0,0,0.58,1)）              |
| ease-in-out                   | 中间快，两边慢（等于 cubic-bezier(0.42,0,0.58,1)）           |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值                           |

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #e67e22;
        border-radius: 50%;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 3s;
        transition-timing-function: ease;
    }

    div:hover {
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#贝塞尔曲线)贝塞尔曲线

需要设置四个值 `cubic-bezier(<x1>, <y1>, <x2>, <y2>)`，来控制曲线速度，可在 [https://cubic-bezier.com](https://cubic-bezier.com/) 网站在线体验效果。

![image-20190917143208598](https://houdunren.gitee.io/note/assets/img/image-20190917143208598.d3bc3aad.png)

```text
...
div {
  width: 150px;
  height: 150px;
  background-color: #e67e22;
  border-radius: 50%;
  transition-property: background-color, transform, opacity, border-radius;
  transition-duration: 3s;
  transition-timing-function: cubic-bezier(.17, .67, .86, .49);
}
...
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#步进速度)步进速度

过渡使用阶梯化呈现，有点像现实生活中的机械舞，下面是把过渡分五步完成。

| 选项           | 说明                                       |
| -------------- | ------------------------------------------ |
| steps(n,start) | 设置n个时间点，第一时间点变化状态          |
| steps(n,end)   | 设置n个时间点，第一时间点初始状态          |
| step-start     | 等于steps(1,start)，可以理解为从下一步开始 |
| step-end       | 等于steps(1,end)，可以理解为从当前步开始   |

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#steps)steps

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8995229.a0f2ad3f.gif)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #34495e;
        }

        ul {
            width: 800px;
            height: 300px;
            list-style: none;
            display: flex;
            justify-content: space-between;
            position: relative;
        }

        li {
            flex: 1;
            border: solid 1px #ddd;
            text-align: center;
            padding-top: 20px;
        }

        li::before {
            content: 'houdunren.com';
            font-size: 1.2em;
            text-align: center;
            color: white;
            opacity: .3;
        }

        ul::before,
        ul::after {
            text-align: center;
            font-size: 2em;
            line-height: 100px;
            color: white;
            z-index: 2;
        }

        ul::before {
            content: 'start';
            position: absolute;
            width: 200px;
            height: 100px;
            background: #e67e22;
            transition-duration: 2s;
            transition-timing-function: steps(4, start);
            box-sizing: border-box;
            border-left: solid 10px #fff;
        }

        ul::after {
            content: 'end';
            position: absolute;
            bottom: 0;
            width: 200px;
            height: 100px;
            background: #9b59b6;
            transition-duration: 2s;
            transition-timing-function: steps(4, end);
            box-sizing: border-box;
            border-right: solid 10px #fff;
        }

        ul:hover::before {
            transform: translateX(800px);
        }

        ul:hover::after {
            transform: translateX(800px);
        }
    </style>
</head>

<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#时钟效果)时钟效果

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8996478.cd55d120.gif)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: #34495e;
        }

        main {
            width: 400px;
            height: 400px;
            background: #ecf0f1;
            border-radius: 50%;
            position: relative;
        }

        main::before {
            content: '';
            width: 20px;
            height: 20px;
            background: #333;
            position: absolute;
            left: 50%;
            top: 50%;
            border-radius: 50%;
            transform: translate(-50%, -50%)
        }

        main::after {
            content: '';
            width: 5px;
            height: 50%;
            background: #333;
            position: absolute;
            left: 50%;
            bottom: 50%;
            transform: translateX(-50%);
            transform-origin: bottom;
            transition-duration: 60s;
            transition-timing-function: steps(60, end);
        }

        body:hover main::after {
            transform: translateX(-50%) rotate(360deg);
        }
    </style>
</head>

<body>
    <main>
    </main>
    <h3>houdunren.com</h3>
</body>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#step-start-end)step-start/end

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8995438.befa69b1.gif)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #34495e;
        }

        ul {
            width: 400px;
            height: 300px;
            list-style: none;
            display: flex;
            justify-content: space-between;
            position: relative;
        }

        li {
            flex: 1;
            border: solid 1px #ddd;
            text-align: center;
            padding-top: 20px;
        }

        li::before {
            content: 'houdunren.com';
            font-size: 1.2em;
            text-align: center;
            color: white;
            opacity: .3;
        }

        ul::before,
        ul::after {
            text-align: center;
            font-size: 2em;
            line-height: 100px;
            color: white;
            z-index: 2;
        }

        ul::before {
            content: 'start';
            position: absolute;
            width: 200px;
            height: 100px;
            background: #e67e22;
            transition-duration: 1s;
            transition-timing-function: step-start;
            box-sizing: border-box;
            border-left: solid 10px #fff;
        }

        ul::after {
            content: 'end';
            position: absolute;
            bottom: 0;
            width: 200px;
            height: 100px;
            background: #9b59b6;
            transition-duration: 1s;
            transition-timing-function: step-end;
            box-sizing: border-box;
            border-right: solid 10px #fff;
        }

        ul:hover::before {
            transform: translateX(200px);
        }

        ul:hover::after {
            transform: translateX(200px);
        }
    </style>
</head>

<body>
    <ul>
        <li></li>
        <li></li>
    </ul>
</body>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#步进形态)步进形态

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8707495.8794c9d9.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #e67e22;
        border-radius: 50%;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 3s;
        transition-timing-function: steps(5, end);
    }

    div:hover {
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#变化广告)变化广告

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9032246.afdff4ca.gif)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: #34495e;
        }

        main {
            width: 400px;
            height: 200px;
            position: relative;
            overflow: hidden;
        }

        section {
            width: 800px;
            height: 200px;
            display: flex;
            transition-duration: 1s;
            transition-timing-function: step-start;
        }

        div {
            width: 400px;
            height: 200px;
            overflow: hidden;
        }

        main:hover section {
            transform: translateX(-400px);
        }
    </style>
</head>

<body>
    <main>
        <section>
            <div><img src="3.jpg" alt=""></div>
            <div><img src="5.jpg" alt=""></div>
        </section>
    </main>
</body>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transition-delay)transition-delay

用于设置延迟过渡的时间。

- 默认为0s即立刻开始过渡
- 值可以为负数
- 变化属性数量大于时间数量时，后面的属性再从第一个时间开始重复使用

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#基本使用)基本使用

下面设置了延迟时间为1s，当鼠标放上

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8713179.daeedc2e.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #e67e22;
        border-radius: 50%;
        transition-property: background-color, transform, opacity, border-radius;
        transition-duration: 1s;
        transition-delay: 1s;
    }

    div:hover {
        border-radius: 0;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#多值延迟)多值延迟

可以设置不同属性的延迟时间。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8722061.8b59c6a7.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #fff;

        transition-property: background-color, transform, border-radius;
        transition-duration: 1s, 2s, 3s;
        transition-delay: 1s, 3s, 5s;
    }

    div:hover {
        border-radius: 50%;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#使用负值)使用负值

下例圆角属性的过渡时间为4s，设置延迟为 -4s，表示鼠标放上时直接显示在4s上的效果。如果设置为-2s显示圆角变形一半的效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8722600.360959b2.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #fff;

        transition-property: background-color, transform, border-radius;
        transition-duration: 1s, 2s, 4s;
        transition-delay: 1s, 2s, -4s;
    }

    div:hover {
        border-radius: 50%;
        transform: scale(2) rotate(180deg);
        background-color: #e67e22;
    }
</style>

<main>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#transition)transition

可以使用`transition` 指令将过渡规则统一设置，需要注意以下几点。

- 必须设置过渡时间
- 延迟时间放在逗号或结束前

```text
 transition: border-radius linear 2s 0s,
                background 2s 2s,
                width linear 2s 4s,
                height linear 2s 4s;
```

### [#](https://houdunren.gitee.io/note/css/13 过渡延迟.html#点赞案例)点赞案例

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8985345.ca1008c8.gif)

```html
 <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
<script src='https://code.jquery.com/jquery-3.3.1.slim.min.js'></script>
<style>
    body {
        width: 100vw;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #ecf0f1;
    }

    div {
        position: relative;
        width: 100px;
        height: 100px;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    div i.fa {
        font-size: 100px;
        position: absolute;
        transition: all .5s;
        color: #ddd;
    }

    div.heart i.fa {
        font-size: 400px;
        color: #e74c3c;
        opacity: 0;
    }

    div.heart i.fa:nth-child(2) {
        font-size: 80px;
        color: #e74c3c;
        opacity: 1;
    }
</style>

<body>
    <div onclick="heart()">
        <i class="fa fa-heart" aria-hidden="true"></i>
        <i class="fa fa-heart" aria-hidden="true"></i>
    </div>
    <script>
        function heart() {
            $("div").toggleClass('heart');
        }
    </script>
</body>
```

# 帧动画

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#基础知识)基础知识

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

通过定义一段动画中的关键点、关键状态来创建动画。Keyframes相比transition对动画过程和细节有更强的控制。

过渡动画是两个状态间的变化，帧动画可以处理动画过程中不同时间的细节变化，不过对过渡动画理解后再不习帧动画会非常容易，也可以把帧动画理解为多个帧之间的过渡动画。

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#关键帧)关键帧

使用`@keyframes` 规则配置动画中的各个帧

- from 表示起始点
- to表示终点
- 可以使用百分数如 20%动画运行到20%时间时

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#基本使用)基本使用

下面使用 `@keyframes` 定义了动画叫 `hd` 并配置了两个帧动作`from/to` ，然后在div元素中使用`animation-name` 引用了动画并使用`animation-duration`声明执行三秒。

- 动画命名不要使用CSS关键字如 `none`

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8872502.6b4a1a8e.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
    }

    div {
        width: 150px;
        height: 150px;
        background-color: #fff;
        border: solid 20px #ddd;
        animation-name: hd;
        animation-duration: 3s;
    }

    @keyframes hd {
        from {
            opacity: 0;
            transform: scale(.1);
        }

        to {
            opacity: 1;
        }
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#时间点)时间点

帧动画需要定义在不同时间执行的动作，开始与结束可以使用 `form/to` 或 `0%/100%` 声明。

- 必须添加百分号，25%是正确写法
- 时间点没有顺序要求，即100%写在25%前也可以
- 未设置`0%`与`100%` 时将使用元素原始状态

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#物体移动)物体移动

下面定义不同时间点来让物体元素移动一圈，下例中可以不设置`from/to` 系统将定义为元素初始状态。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8874535.c42328d7.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
        border: solid 2px white;
    }

    div {
        width: 100px;
        height: 100px;
        background-color: #e67e22;
        animation-name: hd;
        animation-duration: 3s;
    }

    @keyframes hd {
        0% {}

        25% {
            transform: translateX(300%);
        }

        50% {
            transform: translate(300%, 300%);
        }

        75% {
            transform: translate(0, 300%);
        }

        to {}
    }
</style>

<main>
	<div></div>
</main>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#同时声明)同时声明

时间点可以动画样式一样时可以一起声明，下面将25%/75%背景一起声明。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8874485.ad22fb65.gif)

```text
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        background: #2c3e50;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        width: 100vw;
        height: 100vh;
        padding: 80px;
    }

    main {
        width: 400px;
        height: 400px;
        border: solid 2px white;
    }

    div {
        width: 100px;
        height: 100px;
        background-color: #e67e22;
        animation-name: hd;
        animation-duration: 3s;
    }

    @keyframes hd {
        25% {
            transform: translateX(300%);
        }

        50% {
            transform: translate(300%, 300%);
        }

        75% {
            transform: translate(0, 300%);
        }

        25%,
        75% {
            background: #9b59b6;
            border-radius: 50%;
        }

        50%,
        100% {
            background: #e67e22;
        }
    }
</style>

<main>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#使用动画)使用动画

使用`animation-name` 规则可以在元素身上同时使用多个动画。

- 使用多个动画时用逗号分隔
- 多个动画有相同属性时，后面动画的属性优先使用

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#基本使用-2)基本使用

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8875347.e8c0d538.gif)

```text
<style>
    main {
        width: 400px;
        height: 400px;
        border: solid 5px #95a5a6;
    }

    div {
        width: 100px;
        height: 100px;
        background-color: #e67e22;
        animation-name: hd, scale;
        animation-duration: 3s;
    }

    @keyframes hd {
        25% {
            transform: translateX(300%);
        }

        50% {
            transform: translate(300%, 300%);
        }

        75% {
            transform: translate(0, 300%);
        }

        25%,
        75% {
            background: #9b59b6;
        }

        50%,
        100% {
            background: #e67e22;
        }

    }

    @keyframes scale {
        from {
            border-radius: 0;
        }

        75% {
            border-radius: 50%;
        }

        to {
            border-radius: 0;
        }
    }
</style>

<main>
	<div></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#动画时间)动画时间

使用 `animation-duration` 可以声明动画播放的时间，即把所有帧执行一遍所需要的时间。

- 可以使用m秒，ms毫秒时间单位
- 可为不同动画单独设置执行时间
- 如果动画数量大于时间数量，将重新从时间列表中计算

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#炫彩背景)炫彩背景

下面实例声明三个动画，使用 `animation-duration`为每个动画设置不同执行的时间。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8878649.86285441.gif)

```text
<style>
    main {
        background: #34495e;
        animation-name: scale, colors, rotate;
        animation-duration: 1s, 5s, 1s;
        animation-fill-mode: forwards;
    }

    @keyframes scale {
        from {
            width: 0;
            height: 0;
        }

        to {
            width: 100vw;
            height: 100vh;
        }
    }

    @keyframes colors {
        0% {
            background: #e67e22;
        }

        50% {
            background: #34495e;
        }

        100% {
            background: #16a085;
        }
    }

    @keyframes rotate {
        0% {
            transform: rotate(0deg);
        }

        50% {
            transform: rotate(-360deg);
        }

        100% {
            transform: rotate(360deg);
        }
    }
</style>

<body>
    <main></main>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#动画属性)动画属性

不是所有css属性都有过渡效果，[查看支持动画的CSS属性](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) ，一般来讲有中间值的属性都可以设置动画如宽度、透明度等。

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#属性体验)属性体验

下例中的边框变化没有中间值，所以是瞬间改变也没有产生动画效果。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9070872.31519999.gif)

```text
<head>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        h2 {
            color: #f39c12;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #34495e;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        main {
            width: 100px;
            height: 100px;
            background: white;
            animation-name: hd;
            animation-duration: 2s;
        }

        @keyframes hd {
            0% {
                background: #9b59b6;
                border: solid 10px #000;
            }

            100% {
                width: 200px;
                height: 200px;
                background: #e74c3c;
                border: double 10px #000;
            }
        }
    </style>
</head>

<body>
    <main></main>
    <h2>houdunren.com</h2>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#中间值)中间值

下面是例子尺寸没有产生动画，因为`0%`帧设置的尺寸单位与 `100%` 设置的尺寸没有中间值，解析器没有办法计算，最终效果如下：

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9070670.068e273b.gif)

正确效果应该是这样

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9070692.0371db51.gif)

```text
<head>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        h2 {
            color: #f39c12;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #34495e;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        main {
            width: 100px;
            height: 100px;
            background: white;
            animation-name: hd;
            animation-duration: 2s;
        }

        @keyframes hd {
            0% {
                width: auto;
                height: auto;
                background: #9b59b6;
            }

            100% {
                width: 200px;
                height: 200px;
                background: #e74c3c;
            }
        }
    </style>
</head>

<body>
    <main></main>
    <h2>houdunren.com</h2>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#重复动画)重复动画

使用`animation-iteration-count` 规则设置动画重复执行次数，设置值为 `infinite` 表示无限循环执行。

- 可同时设置元素的多个动画重复，使用逗号分隔
- 如果动画数量大于重复数量定义，后面的动画将重新计算重复

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#心动感觉)心动感觉

下面是画心的步骤

![image-20190919170506721](https://houdunren.gitee.io/note/assets/img/image-20190919170506721.7bd12d30.png)

使用循环动画绘制心动效果

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8894047.f0ee8861.gif)

```text
<style>
    .heart {
        width: 200px;
        height: 200px;
        background: #e74c3c;
        transform: rotate(45deg);
        position: relative;
        animation-name: heart;
        animation-duration: 1s;
        animation-iteration-count: 100;
    }

    .heart::before {
        content: '';
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: #e74c3c;
        position: absolute;
        transform: translate(-50%, 0px);
    }

    .heart::after {
        content: '';
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: #e74c3c;
        position: absolute;
        transform: translate(0%, -50%);
    }

    @keyframes heart {
        from {
            transform: scale(.3) rotate(45deg);
        }

        to {
            transform: scale(1) rotate(45deg);
        }
    }
</style>

<main>
	<div class="heart"></div>
</main>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#动画方向)动画方向

使用 `animation-direction` 控制动画运行的方向。

| 选项              | 说明                         |
| ----------------- | ---------------------------- |
| normal            | 从0%到100%运行动画           |
| reverse           | 从100%到0%运行动画           |
| alternate         | 先从0%到100%，然后从100%到0% |
| alternate-reverse | 先从100%到0%，然后从0%到100% |

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#效果比较)效果比较

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9072635.d0d86895.gif)

```text
<head>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        h2 {
            color: #f39c12;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #34495e;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        ul {
            width: 400px;
            height: 100px;
            display: flex;
        }

        li {
            list-style: none;
            text-align: center;
            display: flex;
            flex-direction: column;
            flex: 1;
            justify-content: space-between;
        }

        li span {
            font-size: 10px;
            color: #ecf0f1;
        }

        i.fa {
            font-size: 30px;
            margin: 5px;
            color: #e74c3c;
            animation-name: hd;
            animation-duration: 2s;
            animation-iteration-count: infinite;
        }

        li:nth-child(1)>i.fa {
            animation-direction: normal;
        }

        li:nth-child(2)>i.fa {
            animation-direction: reverse;
        }

        li:nth-child(3)>i.fa {
            animation-direction: alternate;
        }

        li:nth-child(4)>i.fa {
            animation-direction: alternate-reverse;
        }

        @keyframes hd {
            from {}

            to {
                opacity: 1;
                transform: scale(3);
            }
        }
    </style>
</head>

<body>
    <ul>
        <li>
            <i class="fa fa-heart" aria-hidden="true"></i>
            <span>normal</span>
        </li>
        <li>
            <i class="fa fa-heart" aria-hidden="true"></i>
            <span>reverse</span>
        </li>
        <li>
            <i class="fa fa-heart" aria-hidden="true"></i>
            <span>alternate</span>
        </li>
        <li>
            <i class="fa fa-heart" aria-hidden="true"></i>
            <span>alternate-reverse</span>
        </li>
    </ul>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#reverse)reverse

根据上面的心动例子改变方向为100%~0%

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8894427.a32e9b0f.gif)

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#alternate)alternate

根据上面的心动例子改变方向为0%~100%然后100%~0%

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8894391.a4228c9e.gif)

```text
animation-direction: alternate-reverse;
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#alternate-reverse)alternate-reverse

通过使用合适的运动方向 `alternate-reverse` 制作跳动的小球

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8895617.c0966e33.gif)

```text
<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    div {
        width: 200px;
        height: 200px;
        border-radius: 50%;
        background: #e67e22;
        animation-name: ball;
        animation-duration: 2s;
        animation-iteration-count: infinite;
        animation-direction: alternate-reverse;
    }

    @keyframes ball {
        0% {}

        100% {
            transform: translateY(-600px);
        }
    }

    section {
        width: 400px;
        height: 10px;
        border-radius: 50%;
        animation-name: shadow;
        animation-duration: 2s;
        animation-iteration-count: infinite;
        animation-direction: alternate;
    }

    @keyframes shadow {
        from {
            background: #000;
            transform: scale(1);
            filter: blur(35px);
        }

        to {
            background: #aaa;
            filter: blur(10px);
        }
    }
</style>

<main>
	<div></div>
	<section></section>
</main>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#延迟动画)延迟动画

使用 `animation-delay` 规则定义动画等待多长时间后执行。

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#微场景)微场景

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8899531.e8d14a71.gif)

```text
<style>
    body {
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    header {
        width: 100vw;
        height: 10vh;
        font-size: 2.5em;
        color: white;
        background: #e74c3c;
        text-align: center;
        line-height: 10vh;
        animation-name: hd-translate;
        animation-duration: 500ms;
    }

    main {
        flex: 1;
        width: 100vw;
        height: 300px;
        left: 0;
        bottom: 0;
        background: url("5.jpg") no-repeat right bottom;
        background-size: cover;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transform: translateX(-100vw);
        animation-name: hd-rotate;
        animation-duration: 1s;
        animation-fill-mode: forwards;
    }

    main>* {
        opacity: .8;
        font-size: 1.2em;
        line-height: 2em;
        color: #f3f3f3;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 5px rgba(0, 0, 0, .6);
    }

    main>.lesson {
        width: 80vw;
        height: 40vw;
        background: #8e44ad;
        transform: translate(-100vw, -100vh);
        animation-name: hd-rotate;
        animation-duration: 1s;
        animation-delay: 1s;
        animation-fill-mode: forwards;
    }

    main>.video {
        margin-top: 20px;
        width: 60vw;
        height: 40vw;
        background: #2980b9;
        animation-name: hd-translate;
        animation-duration: 1s;
        animation-delay: 2s;
        transform: translate(-100vw, -100vh);
        animation-fill-mode: forwards;
    }

    footer {
        width: 100vw;
        height: 10vh;
        font-size: 1.5em;
        color: white;
        background: #27ae60;
        text-align: center;
        line-height: 10vh;
        animation-name: hd-skew;
        animation-duration: 500ms;
        animation-delay: 3s;
        transform: translateX(-100vw);
        animation-fill-mode: forwards;
    }

    @keyframes hd-translate {
        from {
            transform: translate(-100vw, -100vh);
        }

        to {
            transform: translateY(0);
        }
    }

    @keyframes hd-rotate {
        from {
            transform: translate(-100%, -100%);
        }

        to {
            transform: translateX(0) rotate(360deg);
        }
    }

    @keyframes hd-skew {
        from {
            transform: translateX(-100%) skew(-45deg);
        }

        to {
            transform: skewX(0deg);
        }
    }
</style>

<body>
    <header>
        后盾人
    </header>
    <main>
        <div class="lesson">
            系统课程是多个实战课程的组合，用来全面掌握一门语言或软件的使用，尤其适合刚入门的新手系统牢固的掌握知识。
        </div>
        <div class="video hd-translate">
            系统课程是多个实战课程的组合，用来全面掌握一门语言或软件的使用，尤其适合刚入门的新手系统牢固的掌握知识。
        </div>
    </main>
    <footer>
        houdunren.com
    </footer>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#动画速率)动画速率

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#系统属性)系统属性

| 值                            | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| linear                        | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。 |
| ease                          | 开始慢，然后快，慢下来，结束时非常慢（cubic-bezier(0.25,0.1,0.25,1)） |
| ease-in                       | 开始慢，结束快（等于 cubic-bezier(0.42,0,1,1)）              |
| ease-out                      | 开始快，结束慢（等于 cubic-bezier(0,0,0.58,1)）              |
| ease-in-out                   | 中间快，两边慢（等于 cubic-bezier(0.42,0,0.58,1)）           |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值                           |

- 可以在帧中单独定义，将影响当前帧的速率

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#贝塞尔曲线)贝塞尔曲线

需要设置四个值 `cubic-bezier(<x1>, <y1>, <x2>, <y2>)`，来控制曲线速度，可在 [https://cubic-bezier.com](https://cubic-bezier.com/) 网站在线体验效果。

![image-20190917143208598](https://houdunren.gitee.io/note/assets/img/image-20190917143208598.d3bc3aad.png)

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#体验效果)体验效果

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9379048.a9342460.gif)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
            display: grid;
            grid-template-columns: 1fr;
        }

        body::before {
            content: 'houdunren.com';
            color: white;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translateX(-50%);
            opacity: .5;
        }

        ul {
            box-sizing: border-box;
            list-style: none;
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
        }

        li {
            box-sizing: border-box;
            background: #e67e22;
            animation-name: move;
            animation-duration: 3s;
            animation-iteration-count: infinite;
            color: #333333;
        }

        li:nth-child(1) {
            animation-timing-function: ease;
        }

        li:nth-child(2) {
            animation-timing-function: ease-in;
        }

        li:nth-child(3) {
            animation-timing-function: ease-out;
        }

        li:nth-child(4) {
            animation-timing-function: ease-in-out;
        }

        li:nth-child(5) {
            animation-timing-function: linear;
        }

        @keyframes move {
            to {
                transform: translateY(90vh);
            }
        }
    </style>
</head>

<body>
    <ul>
        <li>ease</li>
        <li>ease-in</li>
        <li>ease-out</li>
        <li>ease-in-out</li>
        <li>linear</li>
    </ul>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#弹跳小球)弹跳小球

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9139804.a095202a.gif)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            align-items: flex-start;
            background: #2c3e50;
        }

        div {
            position: absolute;
            width: 100px;
            height: 100px;
            left: 30%;
            top: 0px;
            transform: translate(0vw, 0);
            background: radial-gradient(at right top, #f39c12, #d35400);
            border-radius: 50%;
            animation-name: jump;
            animation-duration: 2s;
            animation-iteration-count: infinite;
            animation-timing-function: ease-in;
        }

        div:nth-child(2) {
            animation-delay: .2s;
            left: 60%;
        }

        @keyframes jump {
            0% {
                transform: translateY(0);
                animation-timing-function: ease-in;
            }

            30% {
                transform: translateY(10vh);
                animation-timing-function: ease-in;
            }

            60% {
                transform: translateY(40vh);
                animation-timing-function: ease-in;
            }

            80% {
                transform: translateY(60vh);
                animation-timing-function: ease-in;
            }

            95% {
                transform: translateY(75vh);
                animation-timing-function: ease-in;
            }

            15%,
            45%,
            70%,
            85%,
            100% {
                transform: translateY(80vh);
                animation-timing-function: ease-out;
            }
        }
    </style>
</head>

<body>
    <div></div>
    <div></div>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#魔术小球)魔术小球

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-8904065.907dbaa9.gif)

```text
<style>
    body {
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-start;
        background: #2c3e50;
    }

    div {
        position: absolute;
        width: 100px;
        height: 100px;
        transform: translate(-20vw, -300%);
        background: radial-gradient(at right top, #f39c12, #d35400);
        border-radius: 50%;
        animation-name: jump;
        animation-duration: 1.5s;
        animation-iteration-count: infinite;
        animation-timing-function: ease-in;
    }

    div:nth-child(2) {
        animation-delay: .2s;
    }

    div:nth-child(3) {
        animation-delay: 1s;
    }

    @keyframes jump {
        0% {
            transform: translate(-20vw, -300%);
        }

        10% {
            transform: scaleY(.9) translate(15vw, 0%);
        }

        20% {
            transform: translate(20vw, -200%);
        }

        30% {
            transform: scaleY(.9) translate(30vw, 0%);
        }

        40% {
            transform: translate(40vw, -120%);
        }

        50% {
            transform: scaleY(.9) translate(50vw, 0%);
        }

        60% {
            transform: translate(60vw, -70%);
        }

        70% {
            transform: scaleY(.9) translate(70vw, 0%);
        }

        80% {
            transform: translate(80vw, -50%);
        }

        90% {
            transform: scaleY(.9) translate(90vw, 0%);
        }

        95% {
            transform: translate(95vw, -30%);
        }

        100% {
            transform: scaleY(.9) translate(100vw, 0%);
        }
    }

    @keyframes move {
        0% {
            /* transform: translateY(-400%); */
        }

        100% {
            /* right: 100px; */
        }
    }
</style>

<body>
    <div></div>
    <div></div>
    <div></div>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#按钮提交)按钮提交

![Untitled](data:image/gif;base64,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l8/85jv/+dCPvvSnT/3qW//62M++9rfP/e57//vgD7/4x0/+8pv//OhPv/rXz/72u//98I8/TIIAACH5BAAGAAAALDACcwAEAAQAge6qeO+wgfvs4QAAAAIGVAKGmgcFACH5BAAGAAAALDACcwAJAAQAguZ+IvPDovjgz/vo3P///wAAAAAAAAAAAAMNKLBDHoo5AhdoL94ZEgAh+QQABQAAACw0AnMACwAEAILmfiLojkTtoGb44M/659n89e////8AAAADEDi2AlQwKOZgkcu0F6euUQIAIfkEAAYAAAAsOgJzAAYABACB5n4i7aBm+ODP////AghEhmI4erlSAQAh+QQABgAAACwtAnMAEwAEAIDmfiIAAAACB4SPqcvt7woAIfkEAAYAAAAsLQJzAAEABACA5oEpAAAAAgKEUQAh+QQABQAAACwtAnMAAQAEAIDrmFkAAAACAoRRACH5BAAGAAAALC0CcwACAAQAgO2ncfG6kQIDDIxQACH5BAAGAAAALC0CcwADAAQAgPK9mPfbyAIETGB4WQAh+QQAEgAAACwtAnMABAAEAID44M////8CBYxhgZdQACH5BAAFAAAALDACcwACAAQAgPG6kfzv5QIDDIxQACH5BAAGAAAALDACcwAFAAQAgffbx/fbyPjgzwAAAAIHFIKGoXlYAAAh+QQADAAAACwxAnMACAAEAIHmfiLtoGb44M////8CCoQ1GQao7MY6SRYAIfkEAAYAAAAsMAJzAAIABACA54c2+ufaAgMMjFAAIfkEAAUAAAAsMAJzAAUABACB7aVu8bqR+ODP/O/lAgcUEmOol5sKACH5BAAGAAAALDECcwAKAAQAguZ+IuyfZPfbyPjgz/nk1v///wAAAAAAAAMOCDrVJEEB5qCk5cXVMkwAIfkEAAwAAAAsOAJzAAgABACB5n4i7aBm+ODP////AgsMEKNiqMNOWm3CAgAh+QQABgAAACwtAnMAEwAEAIDmfiIAAAACB4SPqcvt7woAIfkEAAYAAAAsLQJzAAEABACA5oUyAAAAAgKEUQAh+QQABQAAACwtAnMAAgAEAIDmgi3tpnACAwyMUAAh+QQABgAAACwtAnMAAgAEAIDzw6IAAAACA4RvBQAh+QQABgAAACwtAnMABAAEAIDmgiz659oCBYxhgZdQACH5BAAMAAAALC0CcwAEAAQAgPjgz////wIFjGGBl1AAIfkEAAUAAAAsMAJzAAEABACA+ePUAAAAAgKEUQAh+QQABgAAACwwAnMABAAEAIH1zbD20Lb89O0AAAACBlQChpoHBQAh+QQABgAAACwwAnMABwAEAILmfiLoij743cr44M/659oAAAAAAAAAAAADCzgg1KHMwUbeoiEBACH5BAALAAAALDICcwAHAAQAgeZ+Iu2gZvjgz////wIKBDQZhso51oGhAAAh+QQABgAAACwwAnMAAwAEAIHqk0/tpnD76d4AAAACBFRgeFkAIfkEAAYAAAAsMAJzAAUABACC5n4i5oMv88Sj+ODP/PHpAAAAAAAAAAAAAwg4EELKbrXXEgAh+QQABgAAACwyAnMACwAEAILmfiLpkk3538744M/659r///8AAAAAAAADEAgw1UIwKOYgkauVF6fmVwIAIfkEAAwAAAAsOAJzAAgABACB5n4i7aBm+ODP////AgsMEKNiqMNOWm3CAgAh+QQABQAAACwtAnMAEwAEAIDmfiIAAAACB4SPqcvt7woAIfkEAAYAAAAsLQJzAAEABACA6I1CAAAAAgKEUQAh+QQABgAAACwtAnMAAgAEAIDpkUrvsIECAwyMUAAh+QQABgAAACwtAnMAAwAEAIDrmFn20LYCBExgeFkAIfkEAAYAAAAsLQJzAAQABACA8LKF/PXvAgWMYYGXUAAh+QQACwAAACwtAnMABAAEAID44M////8CBYxhgZdQACH5BAAGAAAALDACcwACAAQAgOaFMvvs4QIDDIxQACH5BAAFAAAALDACcwAEAAQAgfXNsPbQtvz07QAAAAIGVAKGmgcFACH5BAAGAAAALDACcwAIAAQAguZ+Iu2gZvfWvvjgz/z17wAAAAAAAAAAAAMMOABCHoo5Ald78dIEACH5BAAFAAAALDMCcwAGAAQAgeZ+Iu2gZvjgz////wIIhIZhOHq5UgEAIfkEAAYAAAAsMAJzAAEABACA+eHQAAAAAgKEUQAh+QQABgAAACwwAnMABAAEAIHuqnjvsIH77OEAAAACBlQChpoHBQAh+QQABgAAACwwAnMACQAEAILmfiLzw6L44M/76Nz///8AAAAAAAAAAAADDSiwQx6KOQIXaC/eGRIAIfkEAAYAAAAsNAJzAAsABACC5n4i6I5E7aBm+ODP+ufZ/PXv////AAAAAxA4tgJUMCjmYJHLtBenrlECACH5BAAFAAAALDoCcwAGAAQAgeZ+Iu2gZvjgz////wIIRIZiOHq5UgEAIfkEAAYAAAAsLQJzABMABACA5n4iAAAAAgeEj6nL7e8KACH5BAAGAAAALC0CcwABAAQAgOaBKQAAAAIChFEAIfkEAAgAAAAsLQJzAAEABACA65hZAAAAAgKEUQAh+QQABAAAACwtAnMAAgAEAIDzw6IAAAACA4RvBQAh+QQABQAAACwtAnMAAwAEAIDyvZj328gCBExgeFkAIfkEABIAAAAsLQJzAAQABACA+ODP////AgWMYYGXUAAh+QQAAQAAACwwAnMAAwAEAIHtpW7ywJv87+cAAAACBFRgeFkAOw==)

```text
<head>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #34495e;
        }

        button {
            padding: 10px 50px;
            outline: none;
            background: #e67e22;
            font-size: 2em;
            border: solid 5px white;
            color: white;
        }

        button::after {
            content: '';
            display: inline-block;
            height: 3px;
            width: 3px;
            box-shadow: 3px 0 currentColor, 9px 0 currentColor, 15px 0 currentColor;
            animation-name: point;
            animation-duration: 1s;
            animation-iteration-count: infinite;
            animation-timing-function: linear;
            margin-left: 5px;
        }

        @keyframes point {
            from {
                box-shadow: none;
            }

            30% {
                box-shadow: 3px 0 currentColor;
            }

            60% {
                box-shadow: 3px 0 currentColor, 9px 0 currentColor;
            }

            90% {
                box-shadow: 3px 0 currentColor, 9px 0 currentColor, 15px 0 currentColor;
            }
        }
    </style>
</head>

<body>
    <button>
        <i class="fa fa-code" aria-hidden="true"></i>
        提交
    </button>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#步进速度)步进速度

过渡使用阶梯化呈现，有点像现实生活中的机械舞，下面是把过渡分五步完成。

| 选项           | 说明                                       |
| -------------- | ------------------------------------------ |
| steps(n,start) | 设置n个时间点，第一时间点变化状态          |
| steps(n,end)   | 设置n个时间点，第一时间点初始状态          |
| step-start     | 等于steps(1,start)，可以理解为从下一步开始 |
| step-end       | 等于steps(1,end)，可以理解为从当前步开始   |

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#steps)steps

`steps(n,start)` 可以简单理解为从第二个开始，`steps(n,end)` 从第一个开始。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9469170.45d93747.gif)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
            display: grid;
            /* justify-content: center;
            align-content: center; */
        }

        main {
            justify-self: center;
            align-self: center;
            width: 400px;
            height: 200px;
            display: grid;
            grid-template: repeat(2, 1fr)/repeat(4, 1fr);
        }

        div {
            background: #f1c40f;
            text-align: center;
            position: relative;
            border-right: solid 1px #2c3e50;
            border-bottom: solid 1px #2c3e50;
            box-sizing: border-box;
        }

        div:nth-child(5)::before {
            content: 'END';
            position: absolute;
            width: 100px;
            height: 100px;
            background: #e67e22;
            left: 0;
            animation-name: move;
            animation-duration: 2s;
            z-index: 2;
            animation-timing-function: steps(4, end);
            animation-iteration-count: infinite;
        }

        div:nth-child(1)::after {
            content: 'START';
            position: absolute;
            width: 100px;
            height: 100px;
            background: #9b59b6;
            animation-name: move;
            animation-duration: 2s;
            animation-timing-function: steps(4, start);
            animation-iteration-count: infinite;
            z-index: 2;
            left: 0;
            top: 0;
        }

        @keyframes move {
            to {
                transform: translateX(400px);
            }
        }
    </style>
</head>

<body>
    <main>
        <div>1 <small>houdunren.com</small></div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
    </main>
</body>
```

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#step-start)step-start

`step-start` 效果等于 `steps(1,start)` ,`step-end` 效果等同于 `steps(1,end)`。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9484950.4ca2375f.gif)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #2c3e50;
            display: grid;
        }

        main {
            align-self: center;
            justify-self: center;
            width: 400px;
            height: 200px;
            display: grid;
            grid-template: repeat(2, 1fr)/repeat(4, 1fr);
        }

        div {
            text-align: center;
            background: #f1c40f;
            border: solid 1px #2c3e50;
            box-sizing: border-box;
            position: relative;
        }

        div:nth-child(1)::before,
        div:nth-child(5)::before {
            animation-name: hd;
            animation-iteration-count: infinite;
            animation-duration: .5s;
            z-index: 2;
        }

        div:nth-child(1)::before {
            content: 'START';
            width: 100px;
            height: 100px;
            background: #8e44ad;
            position: absolute;
            left: 0;
            top: 0;
            animation-timing-function: step-start;
        }

        div:nth-child(5)::before {
            content: 'END';
            width: 100px;
            height: 100px;
            background: #27ae60;
            position: absolute;
            left: 0;
            top: 0;
            animation-timing-function: step-end;
        }

        @keyframes hd {
            50% {
                transform: translateX(100px);
            }

            to {
                transform: translateX(0px);
            }
        }
    </style>
</head>

<body>
    <main>
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
    </main>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#播放状态)播放状态

使用 `animation-play-state` 可以控制动画的暂停与运行。

| 选项    | 说明 |
| ------- | ---- |
| paused  | 暂停 |
| running | 运行 |

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#幻灯片)幻灯片

下面是使用无JS脚本参与的图片轮换效果，图片切换使用`steps` 步进与`animation-play-state`播放状态技术。

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9059867.a86bf9bf.gif)

```text
<head>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    <script src='https://code.jquery.com/jquery-3.3.1.slim.min.js'></script>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #2c3e50;
        }

        main {
            width: 400px;
            border: solid 5px #ddd;
            border-width: 5px 0 5px 0;
            overflow: hidden;
            position: relative;
        }

        main:hover section {
            animation-play-state: paused;
        }

        main:hover ul::before {
            animation-play-state: paused;
        }

        section {
            width: 1600px;
            height: 200px;
            display: flex;
            flex-direction: row;
            animation-name: slide;
            animation-duration: 4s;
            animation-iteration-count: infinite;
            animation-timing-function: steps(4, end);
        }

        section div {
            width: 400px;
            height: 200px;
            overflow: hidden;
        }

        section div img {
            width: 100%;
        }

        ul {
            width: 200px;
            position: absolute;
            list-style: none;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 3;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
        }

        ul li {
            font-size: 2em;
            font-weight: bold;
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: solid 3px transparent;
            box-sizing: border-box;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2;
            background: rgba(0, 0, 0, .3);
            box-shadow: 0 0 3px rgba(0, 0, 0, 1);
        }

        ul::before {
            content: '';
            width: 50px;
            height: 50px;
            border-radius: 50%;
            position: absolute;
            background: #e74c3c;
            left: 0;
            animation-name: num;
            animation-duration: 4s;
            animation-iteration-count: infinite;
            animation-timing-function: steps(4, end);
            z-index: 1;
        }

        @keyframes slide {
            from {
                transform: translateX(0px);
            }

            to {
                transform: translateX(-100%);
            }
        }

        @keyframes num {
            100% {
                transform: translateX(200px);
            }
        }
    </style>
</head>

<body>
    <main>
        <section>
            <div>
                <img src="1.jpg" alt="">
            </div>
            <div>
                <img src="2.jpg" alt="">
            </div>
            <div>
                <img src="3.jpg" alt="">
            </div>
            <div>
                <img src="5.jpg" alt="">
            </div>
        </section>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
        </ul>
    </main>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#填充模式)填充模式

`animation-fill-mode` 用于定义动画播放结束后的处理模式，是回到原来状态还是停止在动画结束状态。

| 选项      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| none      | 需要等延迟结束，起始帧属性才应用                             |
| backwards | 动画效果在起始帧，不等延迟结束                               |
| forwards  | 结束后停留动画的最后一帧                                     |
| both      | 包含backwards与forwards规则，即动画效果在起始帧，不等延迟结束，并且在结束后停止在最后一帧 |

### [#](https://houdunren.gitee.io/note/css/14 帧动画.html#效果对比)效果对比

![Untitled](https://houdunren.gitee.io/note/assets/img/Untitled-9067254.58a8233a.gif)

```text
<head>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: #34495e;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        ul {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        li {
            list-style: none;
            width: 200px;
            height: 200px;
            background: #ecf0f1;
            border-radius: 50%;
            animation-name: hd;
            animation-delay: 2s;
            animation-duration: 2s;
            text-align: center;
            font-size: 2em;
            line-height: 200px;
            margin: 10px;
        }

        li:nth-child(1) {
            animation-fill-mode: none;
        }

        li:nth-child(2) {
            animation-fill-mode: backwards;
        }

        li:nth-child(3) {
            animation-fill-mode: forwards;
        }

        li:nth-child(4) {
            animation-fill-mode: both;
        }

        @keyframes hd {
            0% {
                border-radius: 0;
                background: #9b59b6;
            }

            100% {
                border-radius: 50%;
                background: #e74c3c;
            }
        }
    </style>
</head>

<body>
    <ul>
        <li>none</li>
        <li>backwards</li>
        <li>forwards</li>
        <li>both</li>
    </ul>
    <h2>houdunren.com</h2>
</body>
```

## [#](https://houdunren.gitee.io/note/css/14 帧动画.html#组合定义)组合定义

和CSS中的其他属性一样，可以使用`animation`组合定义帧动画。animation 属性是一个简写属性，用于设置六个动画属性：

- animation-name
- animation-duration
- animation-timing-function
- animation-delay
- animation-iteration-count
- animation-direction

必须存在 `animation-duration`属性，否则过渡时间为0没有动画效果。

# 媒体查询

## [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#媒体查询)媒体查询

> [houdunren.com](https://www.houdunren.com/) @ 向军大叔

Media Queries能在不同的条件下使用不同的样式，使页面在不同在终端设备下达到不同的渲染效果。

## [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#媒体类型)媒体类型

| 选项   | 说明                               |
| ------ | ---------------------------------- |
| all    | 所有媒体类型                       |
| screen | 用于电脑屏幕，平板电脑，智能手机等 |
| print  | 打印设备                           |
| speech | 应用于屏幕阅读器等发声设备         |

> 注：tty, tv, projection, handheld, braille, embossed, aural 设备类型已经被废弃

- 可以使用 link 与 style 中定义媒体查询
- 也可以使用 `@import url(screen.css) screen` 形式媒体使用的样式
- 可以用逗号分隔同时支持多个媒体设备
- 未指定媒体设备时等同于all

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#style)style

下面是在屏幕显示与打印设备上不同的CSS效果

![image-20190928214944282](https://houdunren.gitee.io/note/assets/img/image-20190928214944282.25c822de.png)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style media="screen">
        h1 {
            font-size: 3em;
            color: blue;
        }
    </style>
    <style media="print">
        h1 {
            font-size: 8em;
            color: red;
        }

        h2,
        hr {
            display: none;
        }
    </style>
</head>

<body>
    <h1>houdunren.com</h1>
    <hr>
    <h2>后盾人</h2>
</body>
```

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#link)link

在 `link` 标签中通过 `media` 属性可以设置样式使用的媒体设备。

- `common.css` 没有指定媒体所以全局应用
- `screen.css` 应用在屏幕设备
- `print.css` 应用在打印设备

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <link rel="stylesheet" href="common.css">
    <link rel="stylesheet" href="screen.css" media="screen">
    <link rel="stylesheet" href="print.css" media="print">
</head>

<body>
    <h1>houdunren.com</h1>
    <hr>
    <h2>后盾人</h2>
</body>
```

**common.css**

```text
h1 {
    outline: solid 5px #e74c3c;
}
```

**screen.css**

```text
h1 {
    font-size: 3em;
    color: blue;
}
```

**print.css**

```text
h1 {
    font-size: 8em;
    color: red;
}

h2,hr {
    display: none;
}
```

> 可以在 CSS 文件中使用 @media 再定义媒体样式

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#import)@import

使用`@import` 可以引入指定设备的样式规则。文件中引入一个样式文件，在这个文件中再引入其他媒体的样式文件。

```text
<link rel="stylesheet" href="style.css">
```

**style.css**

```text
@import url(screen.css) screen;
@import url(print.css) print;
```

> 具体的 screen.css 与 print.css 与上面介绍的一样，在这里就不重复罗列了

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#media)@media

可以使用 `@media` 做到更细的控制，即在一个样式表中为多个媒体设备定义样式。

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        @media screen {
            h1 {
                font-size: 3em;
                color: blue;
            }
        }

        @media print {
            h1 {
                font-size: 8em;
                color: red;
            }

            h2,
            hr {
                display: none;
            }
        }
    </style>
</head>

<body>
    <h1>houdunren.com</h1>
    <hr>
    <h2>后盾人</h2>
</body>
```

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#多媒体支持)多媒体支持

可以用逗号分隔同时支持多个媒体设备。

```text
@import url(screen.css) screen,print;

<link rel="stylesheet" href="screen.css" media="screen,print">
 
@media screen,print {...}
```

## [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#查询条件)查询条件

可以使用不同条件限制使用的样式

- 条件表达式需要放在扩号中

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#逻辑与)逻辑与

需要满足多个条件时才使用样式，多个条件使用`and` 连接。下例中满足以下要求才使用样式。

- 横屏显示
- 宽度不能超过600px

![image-20190928232757752](https://houdunren.gitee.io/note/assets/img/image-20190928232757752.510a275c.png)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        @media screen and (orientation: landscape) and (max-width: 600px) {
            body {
                background: #8e44ad;
            }

            h1 {
                font-size: 3em;
                color: white;
            }
        }
    </style>
</head>

<body>
    <h1>houdunren.com</h1>
</body>
```

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#逻辑或)逻辑或

多个`或` 条件查询使用逗号连接，不像其他程序中使用 `or` 语法。

下面的示例中如果设备是横屏显示或宽度不超600px时就使用样式规则。

![image-20190928233437941](https://houdunren.gitee.io/note/assets/img/image-20190928233437941.a5e67730.png)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        @media screen and (orientation: landscape),
        screen and (max-width: 600px) {
            body {
                background: #8e44ad;
            }

            h1 {
                font-size: 3em;
                color: white;
            }
        }
    </style>
</head>

<body>
    <h1>houdunren.com</h1>
</body>
```

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#不应用)不应用

`not` 表示不应用样式，即所有条件**都满足**时**不应用**样式。

- 必须将not写在查询的最前面

![image-20190928235224561](https://houdunren.gitee.io/note/assets/img/image-20190928235224561.5abea4d5.png)

```text
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>后盾人</title>
    <style>
        @media not screen and (orientation: landscape) and (max-width:600px) {
            body {
                background: #8e44ad;
            }

            h1 {
                font-size: 3em;
                color: white;
            }
        }
    </style>
</head>

<body>
    <h1>houdunren.com</h1>
</body>
```

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#only)only

用来排除不支持媒体查询的浏览器。

- 对支持媒体查询的设备，正常调用样式，此时就当only不存在
- 对不支持媒体查询的设备不使用样式
- only 和 not 一样只能出现在媒体查询的开始

```text
@media only screen and (orientation: landscape) and (max-width: 600px) {
	...
}
```

## [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#查询特性)查询特性

根据查询特性筛选出使用样式的设备。

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#常用特性)常用特性

下面列出常用的媒体查询特性

| 特性                               | 说明                        |
| ---------------------------------- | --------------------------- |
| orientation: landscape \| portrait | landscape横屏，portrait竖屏 |
| width                              | 设备宽度                    |
| height                             | 设备高度                    |
| min-width                          | 最小宽度                    |
| max-width                          | 最大宽度                    |
| min-height                         | 最小高度                    |
| max-height                         | 最大高度                    |

### [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#使用示例)使用示例

在设备宽度为568px时使用样式

```text
@media only screen and (width:568px) {
    ...     
}
```

在设备不小于 569px时使用样式

```text
@media only screen and (min-width:569px) {
	...
}
```

橫屏设备并且宽度大于569px时使用样式

```text
@media only screen and (orientation: landscape) and (min-width:569px) {
	...
}
```

## [#](https://houdunren.gitee.io/note/css/15 媒体查询.html#实战案例)实战案例

请在版本库查看 https://gitee.com/houdunren/code/tree/master/video/css/media/hd



# 响应尺寸

## [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#响应计算)响应计算

> [houdunren.com](https://www.houdunren.com/)@向军大叔

![xj-small](https://houdunren.gitee.io/note/assets/img/xj-small.f331d790.png)

开发中需要根据不同设备尺寸进行响应处理

### [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#设备像素)设备像素

不同设备的像素尺寸差异很大，比如2K的27寸屏幕与4K的27寸屏幕的像素数量是不一样的。如果我们编写CSS时还要判断设备的物理像素就会很麻烦。

我们希望编写CSS时还是按照以往方式编写，至于具体绘制到屏幕上使用的具体像素让浏览器或小程序等自动计算就可以，这是最佳解决方案。

使用以下代码可以轻松解决上面的问题了

```text
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

### [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#初始样式)初始样式

有些标签默认含有内外边距，且不同浏览器大小也不一样。为了统一我们可以重置标签的CSS默认样式。

最简单的方式就是使用插件[css-reset](https://meyerweb.com/eric/tools/css/reset/)完成

```text
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css" />
```

### [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#案例说明)案例说明

下面是尺寸为375x600的设计稿，绿色区域为200px红色为175px宽度

![image-20200323124619494](https://houdunren.gitee.io/note/assets/img/image-20200323124619494.161abfd4.png)

### [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#像素单位)像素单位

使用固定像素定义时在iphone6与iphon6 plus中的显示效果并不相同

![image-20200323125400666](https://houdunren.gitee.io/note/assets/img/image-20200323125400666.c6a7e86d.png)

**实例代码**

```text
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css" />
  </head>
  <body>
    <div class="left"></div>
    <div class="right"></div>
  </body>
  <style>
    div {
      height: 600px;
    }
    .left {
      width: 200px;
      background: #76ba65;
      float: left;
    }
    .right {
      width: 175px;
      background: #df0f71;
      float: left;
    }
  </style>
</html>
```

### [#](https://houdunren.gitee.io/note/css/16 响应尺寸.html#自动响应)自动响应

实际操作中不同设备只能取宽或高一个尺寸为响应处理，一般情况下我们取宽度响应，高度自动处理。小尺寸时高度产生滚动条，这并不影响什么。

**计算公式**

使用rem单位来处理响应，因为改变rem单位会影响所有使用rem的元素，这确实非常的方便。

- rem是在根元素中定义的font-size
- rem用来在多个设备响应处理时使用
- html元素也可以使用:root选择器选择

下面展示的设计稿为375px宽，下面公式表示1px所占的屏幕尺寸宽度，有以下几点需要说明

- 100vw表示100%设备宽度
- 因为使用了vw宽度系统会根据不同设备自动计算rem

```text
:root {
	font-size: calc(100vw / 375);
}
```

完整代码如下

```text
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css" />
  </head>
  <body>
    <div class="left"></div>
    <div class="right"></div>
  </body>
  <style>
    :root {
      font-size: calc(100vw / 375);
    }
    div {
      height: 600rem;
    }
    .left {
      width: 200rem;
      background: #76ba65;
      float: left;
    }
    .right {
      width: 175px;
      background: #df0f71;
      float: left;
    }
  </style>
</html>
```

现在使用不同设备时宽度已经自动可以响应设置了

# 字体图标

## [#](https://houdunren.gitee.io/note/css/17 字体图标.html#字体图标)字体图标

> [houdunren.com](https://www.houdunren.com/)@向军大叔

![xj-small](https://houdunren.gitee.io/note/assets/img/xj-small.f331d790.png)

网站开发中会使用非常多的小图标，以往使用png图来完成，但不方便设置图标颜色、大小等操作。而使用失量的图标字体可以很好的解决这个问题。

**常用失量字体**

- [阿里图标库](https://www.iconfont.cn/)
- [fontawesome](http://www.fontawesome.com.cn/faicons/#new)

## [#](https://houdunren.gitee.io/note/css/17 字体图标.html#阿里图标)阿里图标

iconfont提供了丰富的图标库，也允许个人上传分享图标，非常复合中文视觉体验。

首先登录图标库网站 https://www.iconfont.cn/

### [#](https://houdunren.gitee.io/note/css/17 字体图标.html#添加图标)添加图标

然后通过关键词搜索图标，并添加到购物车或收藏夹中

![image-20200323150017555](https://houdunren.gitee.io/note/assets/img/image-20200323150017555.bd270d25.png)

将购物车中的图标添加到项目

![image-20200323145937284](https://houdunren.gitee.io/note/assets/img/image-20200323145937284.4b333737.png)

### [#](https://houdunren.gitee.io/note/css/17 字体图标.html#使用图标)使用图标

点击顶部菜单 `图标管理>我的项目`

1. 首先生成网页css代码，然后复制到网页代码中

   ```text
   <link rel="stylesheet" href="//at.alicdn.com/t/font_3434ycaug24x9.css" />
   ```

2. 在项目中复制代码链接

   ![image-20200323150536745](https://houdunren.gitee.io/note/assets/img/image-20200323150536745.3ebec9db.png)

3. 网站中按以下格式使用

   ```text
   <i class="iconfont icongongzhonghao"></i>
   ```

## [#](https://houdunren.gitee.io/note/css/17 字体图标.html#fontawesome)fontawesome

[fontawesome](http://www.fontawesome.com.cn/faicons/#new) 图标库是使用非常多的免费图标库

- 首先推荐在编辑器中安装插件实现代码提示

在页面中引入链接

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css" />
```

html中使用方式如下

```html
<i class="fa fa-user-circle-o" aria-hidden="true"></i>
```





```html
  <script type="text/javascript">function getInfo(){ 
     var s = "";   
      s += " 网页可见区域宽："+ document.body.clientWidth+"\n";    
      s += " 网页可见区域高："+ document.body.clientHeight+"\n";    
      s += " 网页可见区域宽："+ document.body.offsetWidth + " (包括边线和滚动条的宽)"+"\n";    
      s += " 网页可见区域高："+ document.body.offsetHeight + " (包括边线的宽)"+"\n";    
      s += " 网页正文全文宽："+ document.body.scrollWidth+"\n";    
      s += " 网页正文全文高："+ document.body.scrollHeight+"\n";    
      s += " 网页被卷去的高(ff)："+ document.body.scrollTop+"\n";    
      s += " 网页被卷去的高(ie)："+ document.documentElement.scrollTop+"\n";    
      s += " 网页被卷去的左："+ document.body.scrollLeft+"\n";    
      s += " 网页正文部分上："+ window.screenTop+"\n";    
      s += " 网页正文部分左："+ window.screenLeft+"\n";    
      s += " 屏幕分辨率的高："+ window.screen.height+"\n";    
      s += " 屏幕分辨率的宽："+ window.screen.width+"\n";    
      s += " 屏幕可用工作区高度："+ window.screen.availHeight+"\n";    
      s += " 屏幕可用工作区宽度："+ window.screen.availWidth+"\n";    
      s += " 你的屏幕设置是 "+ window.screen.colorDepth +" 位彩色"+"\n";    
      s += " 你的屏幕设置 "+ window.screen.deviceXDPI +" 像素/英寸"+"\n";    
      alert (s);
    }
    getInfo();
  </script>
```

