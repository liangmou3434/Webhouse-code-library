1. Ajax的概念
2. Ajax的作用
3. 原生Ajax
4. Axios


# 1.Ajax的概念
**AsynchronousJavaScriptAndXML，异步的JavaScript和XML**

# 2.Ajax 的作用
1) 数据交换:过Ajax可以给服务器发送请求，并获取服务器响应的数据。
2) 异步交互:可以在不重新加载整个页面的情况下，与服务器交换数据并更新部分网页的技术，如：搜索联想、用户名是否可用的校验等等
**同步交互和异步交互的区别**
![[Pasted image 20240817155750.png]]

# 3.原生Ajax
1) 准备数据地址
2) 创建XMLHttpRequest对象:用于和服务器交换数据
3) 向服务器发送请求
4) 获取服务器响应数据
![[Pasted image 20240817160729.png]]
![[Pasted image 20240817161256.png]]

![[Pasted image 20240817161848.png]]

# 4.Axios

## 4.1Axios的概念
**Axios对原生的Ajax进行了封装,简化书写,快速开发**
官网:`https://www.axios-http.cn/`

## 4.2Axios入门
1) 引入Axios的js文件
`<script src ="js/axios-0.18.0.js"></script>`
3) 使用Axios发送请求,并获取响应结果

![[Pasted image 20240817164929.png]]