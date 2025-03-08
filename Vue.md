1. Vue的概念
2. Vue常用指令
3. Vue的生命周期


# Vue的概念
* ***Vue 是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。
 * **基于MVVM(Model-View-ViewModel)思想，实现数据的双向绑定，将编程的关注点放在数据上。**
 * **官网：https://v2.cn.vuejs.org/**
 ```
   <script src="../JS/vue.js"></script>
 <body>
   <!-- 新建HTML页面,引入Vue.js文件 -->
  <!-- 编写视图 -->
  <div id="app">
   <input type="text" v-model = "message">
   {{message}}
  </div>
  <script>
  //创建Vue对象,定义数据类型
    new Vue({
      el:"#app",//Vue接管区域
      data:{
        message:"Hello Vue"
      }
    })
  </script>
</body>
```
![[Pasted image 20240817094959.png]]

**插值表达式**
==形式{{表达式}}==
内容可以是:
* 变量
* 三元运算符
* 函数调用
* 算术运算

# Vue常用指令
==指令：HTML标签上带有v-前缀的特殊属性，不同指令具有不同含义。例如：v-if，v-for...==
1) v-bind : 为HTML标签绑定属性值，如设置href，CSS样式等
2) v-model:在表单元素上创建双向数据绑定
3) v-on:为HTML标签绑定事件
4) v-if,v-else-if,v-else:条件性的渲染某元素，判定为true时渲染，否则不渲染
5) v-show:根据条件展示某元素，区别在于切换的是display属性的值
6) v-for:列表渲染，遍历容器的元素或者对象的属性

**v-bind:为HTML标签绑定属性值，如设置href，CSS样式等**
书写格式:`<a v-bind:href = "ur1">`传智教育`</a>`
可以缩写成:<a: href ="url">传智教育`</a>`

**v-model:在表单元素上创建双向数据绑定**
书写格式:`<input type = "text"  v-model = "url">`
![[Pasted image 20240817101705.png]]
==注意:通过v-bind或者v-model绑定的变量，必须在数据模型中声明==

**v-on:为HTML标签绑定事件**
书写格式:`<input type = "button"  value="按钮" v-on click= "handle()">`
书写省略格式:`<input type = "button" value = "按钮" @click = "handle()">`
==在Vue中定义函数要用methods属性==
![[Pasted image 20240817103558.png]]

**v-if,v-else-if,v-else:条件性的渲染某元素，判定为true时渲染，否则不渲染**
![[Pasted image 20240817105649.png]]


**v-show:根据条件展示某元素，区别在于切换的是display属性的值**
![[Pasted image 20240817145812.png]]

**v-for:列表渲染，遍历容器的元素或者对象的属性**
书写格式一`:<div v-for = "addr in addrs"> {{addr}} </div>`
==addr:元素的名字-可由自己命名==
书写格式二:`<div v-for="(addr,index) in addrs">{{index + 1}}:{{addr}}</div>`
==index表示元素对应的下标==
![[Pasted image 20240817151242.png]]

# Vue的生命周期
==生命周期:指一个对象从创建到销毁的整个过程==
生命周期的八个阶段:每触发一个生命周期事件,会自动执行一个生命周期的方法(钩子)
1) ==beforeCreate==:创建前
2) ==created==:创建后
3) ==beforeMoount==:挂载前
4) ==mounted:挂载完成==-主要学习
5) ==beforeUpdate==:更新前
6) ==update==:更新后
7) ==beforeDestory==:销毁前
8) ==destroyed==:销毁后
==mounted:挂载完成,Vue初始化成功,HTML页面渲染成功。（发送请求到服务端，加载数据）==
![[Pasted image 20240817154319.png]]
![[Pasted image 20240817154819.png]]

 