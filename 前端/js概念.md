# 闭包

让函数拥有私有变量 在es6 以后的版本中 let const 取代了var 定义

定义：**一个能够读取其他函数内部变量的函数**，实质是**变量的解析过程**（由内而外）

闭包是ES中一个离不开的话题，而且也是是一个难懂又必须搞明白的概念！说起闭包，就不得不提与它密切相关的变量作用域和变量的生命周期。

闭包的弊端：不释放变量，调试困难

```js
function timeCount() {
  for (var i = 1; i < 5; i++) {
      setTimeout(function(){
          console.log(i)
      },1000)
  }
}

timeCount(); 

function timeCount() {
  for (var i = 1; i < 5; i++) {
      (function(i){
          setTimeout(function(){
              console.log(i)
          },1000)
      })(i)
  }
}

timeCount(); 

function timeCount() {
  for (let i = 1; i < 5; i++) {
      setTimeout(function(){
          console.log(i)
      },1000)
  }
}

timeCount();
```

# this关键字



# function 

属性：length  返回函数参数的个数

方法：toString()  将函数声明转为字符串

​           call(作用对象，参数1，参数2)  在具体的作用实例上调用函数  后面参数是具体的参数

         ```js
let obj1={color:'red'}
let obj2={color:'blue'}
function testCall(arg1,arg2){
    console.log(this.color,arg1,arg2)
}
testCall.call(obj1,'nihao')//red nihao undefine
testCall.call(obj2,'nihao')//blue nihao undefine

         ```

​          aply(作用对象，[]或者 arguments对象) 同call 只是 在传参时不需要具体每个参数

```js
let obj1={value:'I am obj1'}
let obj2={value:'I am obj2'}
function testApply(arg1,arg2){
    console.log(this.value,arg1,arg2)
}

// function testApply2(o,arg1,arg2){
//   console.log(testApply.apply(o,arguments))
// }
// testApply2(obj1,'nihao','zhangsan')
testApply.apply(obj2,['nihao','beijing'])
```

## function声明方式

直接声明 function mingzi（）{}

变量接收 var fn= function（）{}；





# $

js 中的$是一个函数，

   $() 执行后返回的是一个对象