1. Element的概念
2. Element入门
3. Element的常见组件


# 1.Element的概念
**Element是饿了么团队研发的,一套为开发者,设计师和产品经理准备的基于Vue2.0的桌面端组件库组件:组成网页的部件,例如:超链接,按钮,图片,表格,表单,分页条等等**
官网:`https://element.eleme.cn/#/zh-CNListener`

# 2.Element入门
1) 安装ElementUI组件库（在当前工程的目录下），在命令行执行指令：
```
npm install element-ui@2.15.3
```
![[Pasted image 20240819172215.png]]

2) 引l入ElementUI组件库
![[Pasted image 20240819172625.png]]
![[Pasted image 20240819172850.png]]

3) 访问官网，复制组件代码，作出调整
![[Pasted image 20240819173551.png]]
![[Pasted image 20240819174014.png]]
![[Pasted image 20240819174955.png]]


# 3.Element中的常见组件

## 3.1常见组件-Table表格
**Table表格:用于展示多条结构类似的数据,可对数据进行排序,筛选,比对或其他自定义操作**
![[Pasted image 20240819180008.png]]
![[Pasted image 20240819180246.png]]
![[Pasted image 20240819180505.png]]

## 3.2常见组件-分页
**Pagination分页：当数据量过多时，使用分页分解数据。**
![[Pasted image 20240819181241.png]]

**分页中的layout属性**
![[Pasted image 20240819182109.png]]

**分页中的两个事件**
1) size-change :   pageSize -改变时会触发(每页记录数发生变化)-回调参数:每页条数
2) current-change  :currentPage 改变时会触发(当前页码发生变化)-回调参数:当前页
![[Pasted image 20240819182649.png]]
![[Pasted image 20240819183412.png]]

**事件加上后效果**
![[recording.gif]]

## 3.3常见组件-对话框
**Dialog对话框：在保留当前页面状态的情况下，告知用户并承载相关操作。**
![[Pasted image 20240819184223.png]]

**设置两个相应的数据模型**
![[Pasted image 20240819184528.png]]


**控制对话框的显示或者隐藏**
![[Pasted image 20240819185309.png]]

## 3.4常见组件-表单
**Form表单：由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据。**
![[Pasted image 20240819191113.png]]
![[Pasted image 20240819191244.png]]

![[Pasted image 20240819192544.png]]

![[Pasted image 20240819193245.png]]

**呈现效果**
![[Pasted image 20240819193446.png]]
**展示form对象内的属性值**
form是js对象,想要展示对象内的属性值,要把js对象转换成json字符串
使用JSON.stringfy():
![[Pasted image 20240819194000.png]]



