1. Spring的基本介绍
2. SpringBoot
3. HTTP协议
4. Web服务器-Tomcat
  

# 1.Spring基本介绍
## 1.1Spring官网
Spring官网的网址:[Spring | Home](https://spring.io/)

## 1.2Spring的发展
spring到今天形成一种开发生态圈,Spting提供了若干个子项目,每个项目用于完成特定的功能


# 2.SpringBoot

## 2.1SpringBoot快速入门
**需求:使用SpringBoot开发一个web应用,浏览器发起请求/hello后,给浏览器返回字符串"Hello World~"**
实现步骤:
1) 创建SpringBoot工程,并勾选web开发相关依赖
2) 定义HelloController类,添加方法hello,并添加注解
3) 运行测试

### 2.1.1创建SpringBoot工程,并勾选web开发相关依赖
  ![[Pasted image 20241017170728.png]]
  ![[Pasted image 20241017202220.png]]
  ![[Pasted image 20241017203216.png]]

### 2.1.2定义HelloController类,并添加方法helllo,且添加注解
==注意:==
1) 要添加注解@RestController证明类是请求处理类
2) 使用标签@RequestMapping注明浏览器需要处理的指令
![[Pasted image 20241017204202.png]]

### 2.1.3运行测试
![[Pasted image 20241017204508.png]]![[Pasted image 20241017205147.png]]
![[Pasted image 20241017205502.png]]

# 3.HTTP协议

## 3.1HTTP协议的概念

### 3.1.1HTTP的特点
1) 基于TCP协议:面向连接,安全
2) 基于请求-响应模型的:一次请求对应一次响应
3) HTTP协议是无状态的协议:对事务处理没有记忆能力,每次请求-响应都是独立的
* 缺点:==多次请求间不能共享数据==
* 优点:==速度快==
概念:Hyper Text Transfer Protocol，超文本传输协议，规定了浏览器和服务器之间数据传输的规则。
![[Pasted image 20241018101316.png]]

## 3.2HTTP-请求协议
原始数据
1) 第一行:请求行
2) 第二行起:请求头(请求头的变量名+请求头的值)
![[Pasted image 20241018104906.png]]
### 3.2.1常见的请求头
1. Host:请求的主机名
2. User-Agent;浏览器版本，例如Chrome浏览器的标识类似Mozilla/5.0...Chrome/79，IE浏览器的标识类似Mozilla/5.0（WindowsNT...) like Gecko
3. Accept:表示浏览器能接收的资源类型，如`text/*`(文本)，`image/*`((文件)或者`*/*`(所有)
4. Accept-Language:表示浏览器偏好的语言，服务器可以据此返回不同语言的网页
5. Accept-Encoding:表示浏览器可以支持的压缩类型，例如gzip,deflate等。
6. Content-Type:请求主体的数据类型。
7. Content-Length:请求主体的大小（单位：字节）

### 3.2.2请求体
==POST请求特有的==
_用于存放请求参数_

### 3.1.3请求方式
![[Pasted image 20241018114855.png]]
1) 请求方式GET:请求参数在请求行中，没有请求体,GET请求大小是有限制的。
 ![[Pasted image 20241018115414.png]]
2) 请求方式POST:请求参数在请求体中,POST请求大小是没有限制的 
![[Pasted image 20241018120104.png]]
## 3.2HTTP-响应协议
==响应协议的内容包括响应头,响应行,响应体==
1) 响应行:响应数据第一行(协议,状态码,描述状态码的状态)
2) 响应头:从第二行开始,**格式key:value**
3) 响应体:最后一部分,存放响应数据

### 3.2.1常见响应码
1) 1xx:响应中-临时状态码，表示请求已经接收，告诉客户端应该继续请求或者如果它已经完成则忽略它。
2) 2xx:成功-表示请求已经被成功接收，处理已完成。
3) 3xx:重定向-重定向到其他地方；让客户端再发起一次请求以完成整个处理。
4) 4xx:客户端错误-处理发生错误，责任在客户端。如：请求了不存在的资源、客户端未被授权、禁止访问等。
5) 5xx:服务器错误-处理发生错误，责任在服务端。如：程序抛出异常等。

1. 200-英文描述:==OK==-客户端请求成功，即处理成功，这是我们最想看到的状态码
2. 302-英文描述:==Found==-指示所请求的资源已移动到由Location响应头给定的URL，浏览器会自动重新访问到这个页面
3. 304-英文描述:==Not Modified==-告诉客户端，你请求的资源至上次取得后，服务端并未更改，你直接用你本地缓存吧。隐式重定向
4. 400-英文描述:==Bad Request==-客户端请求有语法错误，不能被服务器所理解
5. 403-英文描述:==Forbidden==-服务器收到请求，但是拒绝提供服务，比如：没有权限访问相关资源
6. 404-英文描述:==Not Found==-请求资源不存在，一般是URL输入有误，或者网站资源被册除了
7. 500-英文描述:==Internal server Error==-服务器发生不可预期的错误。服务器出异常了
响应码的网址:[HTTP - 状态 | Status - 403 Forbidden - 开发者手册 - 腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/section/1190153)
**以404状态码为例**
![[Pasted image 20241022200138.png]]
### 3.2.2常见的响应头
1) Content-Type:表示该响应内容的类型，例如text/html，application/json。
2) Content-Length:表示该响应内容的长度（字节数）。
3) Content-Encoding:表示该响应压缩算法，例如gzip。
4) Cache-Control:指示客户端应如何缓存，例如max-age=300表示可以最多缓存300秒。
5) Set-Cookie:告诉浏览器为当前页面所在的域设置cookie。

# 4.Web服务器-Tomcat
==Web服务器是一个软件程序，对HTTP协议的操作进行封装，使得程序员不必直接对协议进行操作，让Web开发更加便捷,主要功能是"提供网上信息浏览服务”。==

## 4.1Tomcat服务器的官网
==官网==:[Apache Tomcat® - Welcome!](https://tomcat.apache.org/)

![[Pasted image 20241025102739.png]]

## 4.2Tomcat的使用

### 4.2.1启动Tomcat服务器
![[Pasted image 20241025103110.png]]

**更改最初打开Tomcat服务器中文是乱码的情况**
![[Pasted image 20241025104512.png]]
![[Pasted image 20241025105034.png]]
### 4.2.2暂停Tomcat服务器
1) 直接x掉运行窗口:强制关闭
2) bin\shutdown.bat:正常关闭
3) Ctrl+C:正常关闭(一般电脑可能会加fn做信号-Ctrl+C+fn)

### 4.2.3访问Tomcat
![[Pasted image 20241025105407.png]]
**当Tomcat使用的默认端口其他程序使用的端口冲突了,可以尝试修改Tomcat使用的端口8080**
![[Pasted image 20241025110142.png]]

### 4.2.4部署项目
![[Pasted image 20241025110853.png]]


![[Pasted image 20241025113430.png]]
![[Pasted image 20241025113417.png]]


### 4.2.5起步依赖
1) spring-boot-tarter-web：包含了web应用开发所需要的常见依赖。
2) pring-boot-starter-test：包含了单元测试所需要的常见依赖。
官方提供的starter: