1.请求响应
2.响应数据
3.三层架构

# 1.请求响应

## 1.1请求响应的概念
1) 请求(HttpServletRequest):获取请求数据
2) 响应(HttpServletResponse):设置响应数据

==BS架构==:Browser/Server，浏览器/服务器架构模式。客户端只需要浏览器，应用程序的逻辑和数据都存储在服务端(通过网站可以访问)
==CS架构==:Client/Server，客户端/服务器架构模式。(要下载App进到App操作的)

## 1.2postman插件的使用
==postman是一款功能强大的网页调试与发送网页HTTP请求的chrome插件。==
_postman的作用_:常用于进行接口测试

### 1.2.1workspace的作用
**workspace主要用于保存用户所用的操作数据,并且将数据同步到云端**
_创建workspace_
![[Pasted image 20241028104400.png]]
![[Pasted image 20241028110011.png]]
![[Pasted image 20241028110612.png]]


### 1.2.2传递简单参数
1)接收简单参数的传统方式
**在原始的web程序中，获取请求参数，需要通过HttpServletRequest对象手动获取。**

**请求简单参数的原始方式**
_由于使用postman发送请求用的是Get请求方式,可以直接在url后面加上请求的参数_
```
?+name=xx&age=xx
例:http://localhost:8080//simpleParam?name=liangmou2121&age=20
```
![[Pasted image 20241104101849.png]]
![[Pasted image 20241104102453.png]]

**简单参数:参数名与形参变量名相同,定义形参即可接受参数**
![[Pasted image 20241104105324.png]]
![[Pasted image 20241104105526.png]]

==注意==:`@RequestParam`中的required属性默认为true，代表该请求参数必须传递，如果不传递将报错。如果该参数是可选的，以将required属性设置为false(当方法参数和形参名不一致时,可以使用该注解完成传递)
![[Pasted image 20241104110332.png]]
![[Pasted image 20241104112427.png]]


### 1.2.3传递实体参数
**使用一个简单的实体对象:请求参数名与形参对象属性名相同,定义POJO接收即可**
1) 简单的实体参数
![[Pasted image 20241104113734.png]]

2) 复杂的实体参数
![[Pasted image 20241104114701.png]]

### 1.2.4数组接收参数
_数组参数:_请求参数名与形参数组名称相同且请求参数为多个，定义数组类型形参即可接收参数
**数组的名称和参数的名称要一致**
![[Pasted image 20241122105624.png]]
### 1.2.5集合接收参数
集合参数:请求参数名与形参集合名称相同且请求参数为多个，@RequestParam绑定参数关系
**集合的名称要和参数的名称一致(且要在集合前加上注解@RequestParam)**
![[Pasted image 20241122110248.png]]

### 1.2.6日期参数
_日期参数_:使用@DateTimeFormat注解完成日期参数格式转换
![[Pasted image 20241122111348.png]]

### 1.2.7Json参数
_Json参数_:Json数据==键名==与形参对象==属性名==相同，定义POJO类型形参即可接收参数，需要使用@RequestBody标识
_Json格式的参数需要用POST的请求方式并且请求参数要写在请求体当中_

1) 传递Json参数
![[Pasted image 20241122112107.png]]
2)接收Json参数并封装
![[Pasted image 20241122112842.png]]

### 1.2.8路径参数
_路径参数_:通过请求URL直接传递参数，使用{...}来标识该路径参数，需要使用@PathVariable获取路径参数
![[Pasted image 20241122113639.png]]
**接收多个路径参数**
![[Pasted image 20241122114048.png]]

# 2.响应数据

## 2.1注解@ResponseBody
1) 类型:方法注解,类注解
2) 位置:Contoller方法上/类上
3) 作用:将方法返回值直接响应，如果返回值类型是实体对象/集合，将会转换为JSON格式响应
4) 说明:@RestController=@Controller+@ResponseBody

## 2.2响应结果的格式需要统一
_把响应的数据封装在一个==Result==类里_
设置相对应的响应码,1代表成功,0代表失败
**Result类的具体展示**:
![[Pasted image 20241125110904.png]]
![[Pasted image 20241125111404.png]]
==统一的响应数据格式方法的书写例子==
![[Pasted image 20241125111443.png]]


## 2.3响应请求的案例
_加载并解析emp.xml文件中的数据,并完成数数据处理,在前端页面中展示_

1) 在pom.xml文件中引入dom4j的依赖,用于解析xml文件
![[Pasted image 20241217153718.png]]
==springboot项目的静态资源(html,css,js等前端资源)默认存放目录为类目录下的static,public,或者resources目录==
![[Pasted image 20241217154714.png]]

2) 编写Controller程序,处理请求,响应数据
![[Pasted image 20241217164108.png]]
![[Pasted image 20250103100127.png]]
![[Pasted image 20250103100302.png]]

### 2.3.1加载并解析emp.xml文件
**调用工具类的parse方法**
```
//1.加载并解析emp.xml文件  
 //调用工具类里的parse方法来解析文件  
 //参数一:需要解析的是哪一份文件,参数二:解析的xml文件要往哪个对象里封装  
 //String file = "D:\\Github\\Github代码仓\\SpringBoot-project02\\src\\main\\resources\\emp.xml"; //file参数为需要解析的文件的路径 
 String file = this.getClass().getClassLoader().getResource("emp.xml").getFile();//获取文件的动态路径
 List<Emp> empList = XmlParserUtils.parse(file, Emp.class);//补全左边的快捷键-ctrl+alt+v
```

### 2.3.2对数据进行转换处理
```
//2.对数据进行转换处理-gender,job  
//处理gender  1: 男, 2: 女  
 empList.stream().forEach(emp->{  
    String gender = emp.getGender();//获得性别的字符串  
     if("1".equals(gender)){  
         emp.setGender("男");//把1改为男  
     }else if("2".equals(gender)){  
         emp.setGender("女");//把2改成女  
     }  
     //处理job 1: 讲师, 2: 班主任 , 3: 就业指导  
     String job = emp.getJob();  
     if("1".equals(job)){  
         emp.setJob("讲师");  
     }else if("2".equals(job)){  
         emp.setJob("班主任");  
     }else if("3".equals(job)){  
         emp.setJob("就业指导");  
     }  
 });
```

### 2.3.3响应数据
```
//3.响应数据  
return Result.success(empList);//响应了一个统一的Result结果
```


# 3.三层架构
* ==controller:==控制层,接收前端发送的请求,对请求进行处理,并响应数据
* ==service:==业务逻辑层,处理具体的业务逻辑
* ==dao:==数据访问层(Data Access Object)(持久层),负责数据访问操作,包括数据的增删改查

