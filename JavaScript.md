==简称JS==
1. JS的作用
2. JS的概念
3. JS的引入方式
4. JS的基础语法
5. JS函数
6. JS对象
7. JS事件


# 1.JS的作用
**负责网页的行为(交互效果)**

# 2.JS的概念
* JavaScript（简称：JS）是一门跨平台、面向对象的脚本语言。是用来控制网页行为的，它能使网页可交互。
* JavaScript和Java是完全不同的语言，不论是概念还是设计。但是基础语法类似。
* JavaScript在1995年由BrendanEich发明，并于1997年成为ECMA标准。
==ECMA==：ECMA国际（前身为欧洲计算机制造商协会），制定了标准化的脚本程序设计语言ECMAScript，这种语言得到广泛应用。而JavaScript是遵守ECMAScript的标准的
* ECMAScript6(ES6）是最新的JavaScript版本（发布于2015年)。

# 3.JS 的引入方式
## 3.1内部脚本
* JavaScript代码必须位于`<script></script>`标签之间
* 在HTML文档中,可以在任意地方,放置任意数量的`<script>`
* 一般会把脚本置于`<body>`元素的底部,可改善显示速度
![[Pasted image 20240811173257.png]]

![[Pasted image 20240811173757.png]]
==可以在任意地方,放置任意数量的`<script>`-在HTML文档中有多少个`<script>`标签,警告就会出现多少次==
![[recording 1.gif]]

## 3.2外部脚本
* 外部js文件中,只包含js代码,不能包含`<script>`标签
* `<script>`标签不能自闭合
**自闭合**
![[Pasted image 20240811173404.png]]
**正确的外部脚本代码**
![[Pasted image 20240811173415.png]]

![[Pasted image 20240811174725.png]]
# 4.JS的基础语法
## 4.1书写语法
* 区分大小写:与java一样,变量名,函数名以及其他一切东西都是区分大小写的*
* 每行结尾的分号可有可无(建议加上)
* 注释
**单行注释://注释内容
多行注释: /*注释内容*/****
* *大括号表示代码块*
### 4.1.1输出语句
* 适应 ==window.alert()== 写警告框
* 适应 ==document.write()== 写HTML输出
* 适应 ==console.log()== 写入浏览器控制输出台

**写警告框**
![[Pasted image 20240813082123.png]]

**写HTML输出**
![[Pasted image 20240813082420.png]]

**写浏览器控制输出台**
![[Pasted image 20240813082743.png]]

## 4.2变量
* JavaScript中用==var==关键字(variable的缩写)来声明变量
* JavaScript是一门弱类型的语言,变量可以存放不同类型的值
* 变量名的规则:
1) 组成字符可以是任何字母,数字,下划线(_)或美元符号($)
2) 数字不能开头
3) 建议使用驼峰命名

 ![[Pasted image 20240813083619.png]]
**变量的特点**
特点1:变量的作用域比较大,是全局变量
特点2:可以重复定义
重复定义
![[Pasted image 20240813084033.png]]
注意:
==1)ECMAScript6新增了let关键字来定义变量。它的用法类似于var，但是所声明的变量，只在let关键字所在的代码块内有效，且不允许重复声明
2)ECMAScript6新增了const关键字，用来声明一个只读的常量。一旦声明，常量的值就不能改变==
![[Pasted image 20240813084442.png]]

![[Pasted image 20240813084835.png]]
## 4.3数据类型,运算符,流程控制语句
==数据类型包括原始数据类型和引用数据类型==
### 4.3.1原始数据类型
* number:数字（整数、小数、NaN(NotaNumber))
* string：字符串，单双引皆可
* boolean:布尔。true，false
* null:对象为空
* undefined：当声明的变量未初始化时，该变量的默认值是undefined 
```
<body>
<script>
    // 原始数据类型
    // typeof运算符-用来获取数据类型
    alert(typeof 3);//number
    alert(typeof 3.14);//number
    
    alert(typeof "A");//String
    alert(typeof 'liangmou');//String

    alert(typeof true);//boolean
    alert(typeof false);boolean

    alert(typeof null);//object类型

    var a;//未初始化数据-当声明的变量未初始化时，该变量的默认值是undefined
    alert(typeof a);//undefined
</script>
</body>
```
==typeof运算符== :可以获取数据类型

### 4.3.2数据类型的转换
* ==字符串类型转为数字==
将字符串字面值转为数字。如果字面值不是数字，则转为NaN
* ==将其他类型转为boolean==
1) Number:O和NaN为false，其他均转为true。
2) String：空字符串为false，其他均转为true。
3) Null和undefined：均转为false。
![[Pasted image 20240813092718.png]]

### 4.3.3运算符
* 算术运算符：+ ,－ , * ,  / , %，++, --
* 赋值运算符：=，+=，-=，*=，/=，%=
* 比较运算符：>，<，>=，<=，!=，===
* 逻辑运算符：&&，I，！
* 三元运算符：条件表达式 ? true_value：false_value

**`==`和`===`的区别**
* `==`会进行类型转换,`===`不会进行类型转换
```
    var a = 10;
    alert(a == "10");//true
    //==号会将a从number数据类型转换成String类型再进行比较,内容相同返回true
    alert(a === "10");//false
    //===号不会进行类型转换,如果类型不同直接返回false
 ```

### 4.3.4流程控制语句
* if...elseif...else...
* switch
* for
* while
* do...while

# 5.JS函数
**定义:JavaScript函数通过==function==关键字进行定义,语法为:**
![[Pasted image 20240813093217.png]]
定义方式二:
![[Pasted image 20240813094507.png]]

注意:
1) 形式参数不需要类型。因为JavaScript是弱类型语言
2) 返回值也不需要定义类型，可以在函数内部直接使用return返回即可
3) 在JS中,函数调用可以传递任意个数的参数
**调用:** 函数名称(实际参数列表)
```
 <script>
    //  定义函数
    // 定义方式一
    function add(a,b){
      return a + b;
    }

    // 定义方式二:
    var add = function(a,b){
      return a + b;
    }
    
    //函数调用
    var result = add(10,20);
    alert(result);//30
  </script>
```


# 6.JS对象

## 6.1Array对象
==用于定义数组==
**定义方式一:
var  变量名 = new  Array(元素列表); - 例: var arr = new Array(1,2,3,4);
定义方式二:
var 变量名= [元素列表]； 例: var arr =[1,2,3,4];**

**访问Array对象
arr[索引] = 值 ;     例: arr[10] = "hello";**

### 6.1.1Array的特点
==数组的特点:长度可变,类型可变==
1) 长度可变:数组可以越界访问并赋值,赋值的同时编译器会拓展数组的长度,剩下未赋值的元素编译器默认为undefined
2) 类型可变: 数组中可以放任意类型的数据

### 6.1.2Array的属性
==length== :设置或返回数组中的元素数量
**遍历数组**
```
 // 遍历数组方式一:
    //for循环会遍历数组中所有元素
    var arr3 = [1,2,3,4,5,"A",true,"abc"];
    for (let i = 0; i < arr3.length; i++) {
      console.log(arr3[i]);      
  }
```

### 6.1.3Array方法
==forEach()== :遍历数组中的每个有值的元素，并调用一次传入的函数
==push()== :将新元素添加到数组的末尾，并返回新的长度。
==splice()== : 从数组中删除元素。

**forEach()方法**
```
 // 遍历数组方式二:
// forEach只遍历数组中有值的元素
  arr3.forEach(function (e){
    console.log(e);
  })

  //ES6 中提供的箭头函数  =>用于简化代码
  arr3.forEach((e) =>{
    console.log(e);
  })
```

**push()方法**
==可以一次添加多个元素==
![[Pasted image 20240813152520.png]]
**splice()方法**
![[Pasted image 20240813153106.png]]

## 6.2String对象
**定义方式一:
var 变量名 = new String("...")；var str = new String("Hello String");
定义方式二:
var变量名 = ".";                          var str = "Hello String";
                           var str='Hello String';**

![[Pasted image 20240813154111.png]]
### 6.2.1属性
==length== : 字符串长度
```
//length 获取字符串长度
    console.log(str2.length);//13
    //hello world1字符共11个 加上两个空格共13个
```

### 6.2.2方法
==charAt()==: 返回在指定位置的字符。
==indexOf()==: 检索字符串。
==trim()==:去除字符串两边的空格并返回一个新的字符串
==substring()==: 提取字符串中两个指定的索引号之间的字符-包头不包尾。
![[Pasted image 20240813155326.png]]

## 6.3JSON

**自定义对象的定义:**
![[Pasted image 20240813155814.png]]

**自定义对象的调用格式:**
![[Pasted image 20240813155856.png]]
```
  <script>
    //自定义对象
    var user = {
      name : "liangmou",
      age : 20,
      gender : "女",
      //成员方法 写法一:
      eat : function(){
        alert("正在吃饭");
      },
      
      // 写法二:
      sleep() {
        alert("正在睡觉");
      }
    }

    //调用对象的成员
    alert(user.name);
    user.eat();
  </script>
```

### 6.3.1JSON的概念
* 概念: JavaScript Object Notation , JavaScript对象标记法
* JSON是通过JavaScript对象标记法书写的文本
* ==由于其语法简单,层次结构鲜明,现多用于作为数据载体,在网络中进行数据传输==

**JSON的格式和自定义对象的格式类似,只是所有的变量名和变量值要加上双引号**
**在搜索引擎上搜索json格式化可以找到代码格式化程序或者其他工具来判断代码是否正确**
![[Pasted image 20240813162542.png]]


### 6.3.2JSON的基础语法
**定义:
var  变量名  =  {"key1": value1, "key2": value2}
例:var userStr =‘{"name":"Jerry","age":18，"addr":["北京","上海","西安"]}' **

**JSON是一个字符串,获取JSON里面的内容需要创建对象**
1) JSON字符串转为JS对象
==var jsobject = JsoN.parse(userStr)==
2) JS对象转为JSON字符串
==var jsonStr = JsoN.stringify(jsobject);==
```
 //定义JSON
    var str = '{"name" : "liangmou","age" : 18, "arr" : [1,2,3,4]}';
    
    //将json字符串转换成JS对象-可以获取到js字符串里面的成员变量
     var obj =  JSON.parse(str);
     console.log(obj.name);//liangmou
     
     //将JS对象转换成json字符串
     alert(JSON.stringify(obj));
```

**value的数据类型为**
* 数字(整数或浮点数)
* 字符串(在双引号中)
* 逻辑值(true 或 false)
* 数组(在中括号中)
* 对象(在大括号中)
* null

## 6.4BOM

### 6.4.1BOM的概念
**Brower Object Model 浏览器对象模型,允许JavaScript与浏览器对话,JavaScript将浏览器的各个组成部分封装成对象**

### 6.4.2BOM的组成
共有五个组成部分,此处只学习两个最重要的其中两个部分
* window : 浏览器窗口对象
* Location:地址栏对象

**window对象**
获取window对象,其中window可以省略
```
window.alert("Hello Window");
alert("Hello Window");
```

**window对象的属性**
* history: 对History对象的只读引用
* location:用于窗口或框架的Location对象
* navigator: 对Navigator对象的只读引用

**window对象的方法**
* ==alert()== : 示带有一段消息和一个确认按钮的警告框
* ==confirm()==:示带有一段消息以及确认按钮和取消按钮的对话框。
* ==setinterval()==:按照指定的周期（以毫秒计）来调用函数或计算表达式。
* ==setTimeout()==:指定的毫秒数后调用函数或计算表达式。
![[Pasted image 20240813171045.png]]

**Location对象**
==地址栏对象==
**获取:使用window.location获取,其中window.可以省略**
_window.location.属性；location.属性；_

**Location的属性**
* ==href== : 设置或返回完整的URL
URL，全称为Uniform Resource Locator，中文意思是统一资源定位符，是互联网上用来标识某一处资源的地址。它是一个字符串，用来指明网络上的资源在哪里，并且可以通过它来访问这个资源
例:
```
 location.href ="https://www.itcast.cn";
```

![[recording.gif]]


## 6.5DOM

### 6.5.1DOM的概念
**Document Object Model,文档对象模型**

**JavaScript通过DOM,就能对HTML进行操作**
* 改变HTML元素的内容
* 改变HTML元素的样式(CSS)
* 对HTML DOM事件作出反应
* 添加和删除HTML元素

### 6.5.2DOM的基本组成元素
**DOM是W3C（万维网联盟）的标准，定义了访问HTML和XML文档的标准，分为3个不同的部分：**
1) Core DOM-所有文档类型的标准模型
==Document==:整个文档对象
 ==Element== :元素对象
  ==Attribute==: 属性对象
 ==Text==:文本对象
 ==Comment==:注释对象

2) XML DOM-XML 文档的标准模型
3) HTML DOM-HTML 文档的标准模型
* image`<img>`
* Button: `<input type = 'button'>`

**用Document对戏那个获取Element元素对象**
_HTML中的Element对象可以通过Document对象获取，而Document对象是通过window对象获取的。_
Document对象中提供了以下获取Element元素对象的函数：
```
//网页代码
</head>
  <!-- 定义一个网页 -->
   <img id = "h1" src="../1.jpg" ><br></br>
    <div class="cls">广州南方学院</div>
    <div class="cls">liangmou3434</div>
    
    <input type="checkbox" name = "hobby">电影
    <input type="checkbox" name = "hobby">游戏
    <input type="checkbox" name = "hobby">旅行
```
1) 根据id属性值获取，返回单个Element对象
```
 var img = document.getElementById('h1');
    alert(img);//[object HTMLImageElement]
```
2) 根据标签名称获取，返回Element对象==数组==
```
var divs=document.getElementsByTagName('div');
  for (let i = 0; i < divs.length; i++) {
       alert(divs[i]);  
       //打印结果-[object HTMLDivElement]
       //[object HTMLDivElement]
     }
``` 
3) 根据name属性值获取，返回Element对象==数组==
```
 var ins = document.getElementsByName('hobby');
     for (let i = 0; i < ins.length; i++) {
      alert(ins[i]);
      //打印结果,获得三个[object HTMLDivElement]
     }
```
4) 根据class属性值获取，返回Element对象==数组==
```
  var divs2 = document.getElementsByClassName('cls');
     for (let i = 0; i < divs2.length; i++) {
      alert(divs2[i]);  
      //打印结果,获得两个[object HTMLDivElement]
     }
```

![[Pasted image 20240813222003.png]]
![[Pasted image 20240813223908.png]]

![[Pasted image 20240813224054.png]]

# 7.JS事件
* **事件**:HTML事件是发生在HTML元素上的事情
1) 按钮被点击
2) 鼠标移动到元素上
3) 按下键盘快键
## 7.1JS事件监听
==JavaScript可以在实践被侦测到时 执行代码==

### 7.1.1事件绑定
**方式一:通过HTML标签中的事件属性进行绑定**
![[Pasted image 20240814154933.png]]

**方式二:通过DOM元素属性进行绑定**
![[Pasted image 20240814155001.png]]
![[Pasted image 20240814155837.png]]

### 7.1.2常见事件
1) ==onclick==:鼠标单击事件
2) ==onblur==:元素是失去焦点
3) ==onfocus==:元素获得焦点
4) ==onload==:某个页面或图像被完成加载
5) ==onsubmit==:当表单提交时触发该事件
6) ==onkeydown==:某个键盘的键被按下
7) ==onmouseover==:鼠标被移到某元素上
8) ==onmouseout==:鼠标从某元素移开

1) ![[Pasted image 20240814163502.png]]
2) ![[Pasted image 20240814163627.png]]
3) ![[Pasted image 20240814163812.png]]
4) ![[Pasted image 20240814163923.png]]
5) ![[Pasted image 20240814164041.png]]
7) ![[recording.gif]]

