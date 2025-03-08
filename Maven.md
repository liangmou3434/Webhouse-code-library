==Maven是apache旗下的一个开源项目，是一款用于管理和构建java项目的工具。==
1. Maven的作用
2. Maven的安装
3. 在idea中配置maven环境
4. 创建maven项目
5. maven坐标
6. 用IDEA导入maven项目
7. maven的依赖配置
8. maven的依赖传递
9. maven的依赖范围
10. maven的生命周期
# 1.Maven的作用
1) 依赖管理-方便快捷管理项目依赖的资源(jar包),避免版本冲突的问题
2) 统一项目结构-提供标准,统一的项目结构
![[Pasted image 20241012111046.png]]
3) 项目构建-标准跨平台(Linux,Windows,MacOS)的自动化项目构建方式

# 2.Maven的安装

## 2.1解压apache-maven-3.6.1-bin.zip

## 2.2配置本地仓库：修改conf/settings.xml中的`<localRepository>`为一个指定目录。
![[Pasted image 20241011104413.png]]
![[Pasted image 20241011104705.png]]
## 2.3配置阿里云私服：修改conf/settings.xml中的`<mirrors>`标签，为其添加如下子标签：
```
<mirror>  
	<id>alimaven</id>  
	<name>aliyun maven</name>  
	<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	<mirrorOf>central</mirrorOf>          
</mirror>
```
![[Pasted image 20241011105128.png]]
## 2.4配置环境变量:MAVEN_HOME为maven的解压目录，并将其bin目录加入PATH环境变量
![[Pasted image 20241011105636.png]]
![[Pasted image 20241011110151.png]]
## 2.5测试maven是否安装成功
win+r打开命令提示符
输入指令
```
mvn -v
```
**出现如下界面表示安装成功**
![[Pasted image 20241011110337.png]]
==注意:maven主要使用Jdk11的版本==

# 3.配置maven环境

## 3.1在idea中配置maven环境
![[Pasted image 20241011113110.png]]

![[Pasted image 20241011113714.png]]

![[Pasted image 20241011113958.png]]
![[Pasted image 20241011114226.png]]

## 3.2配置maven环境(全局)
![[Pasted image 20241011114723.png]]


# 4.用Idea创建maven项目
**在idea中创建一个空项目,在空项目里创建一个新模块**
![[Pasted image 20241012110824.png]]

![[Pasted image 20241012111421.png]]
![[Pasted image 20241012113454.png]]
# 5.maven坐标
==maven坐标是自愿中唯一的标识,可以通过该坐标唯一定位资源位置==
**使用坐标来定义项目或引入项目中的依赖**

## 5.2maven坐标的组成
1) groupid:定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima）
2) artifactld：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）
3) version：定义当前项目版本号


# 6.用IDEA导入maven项目
## 6.1导入maven项目方式一:
![[Pasted image 20241012114844.png]]
## 6.2导入maven项目方式二:
![[Pasted image 20241013211654.png]]
## 6.3删除maven项目
![[Pasted image 20241012115045.png]]

# 7.maven的依赖配置
==依赖:指当前项目运行所需要的jar包,一个项目中可以引入多个依赖==
配置:
1. 在pom.xml中编写`<dependencies>`标签
2. 在`<dependencies>`标签中使用`<dependency>`引入坐标
3. .定义坐标的==groupld，artifactld，version==
4. 点击刷新按钮，引入最新加入的坐标
maven的仓库:[Maven Repository: ch.qos.logback » logback-classic » 1.5.6 (mvnrepository.com)](https://mvnrepository.com/artifact/ch.qos.logback/logback-classic/1.5.6)

## 7.1在maven仓库中导入依赖
![[Pasted image 20241014084710.png]]
## 7.2检查依赖是添加成功
![[Pasted image 20241014091528.png]]

# 8.maven的依赖传递
1) 直接依赖:在当前项目中通过依赖配置建立的依赖关系
2) 间接依赖:被依赖的资源如果依赖其他资源,当前项目间接依赖其他资源

## 8.1排除依赖
==排除依赖指主动断开依赖的资源,被排除的资源无需指定版本==
通过`<exclusions>`标签排除依赖-该标签可以一次性排除多个依赖
![[Pasted image 20241014100851.png]]

**排除junit依赖后,junit依赖从依赖项消失**
![[recording.gif]]

# 9.maven的依赖范围
依赖的jar包,默认情况下可以在任何地方使用,可以通过`<scope>...</scope>`设置其作用范围
作用范围:
1) 主程序范围有效(main文件夹范围内)
2) 测试程序范围有效(test文件夹范围内)
3) 是否参与打包运行(package指令范围内)

## 9.1scope值
1) compile:在主程序,测试程序,打包(运行内)均有效
2) test:只在运行程序有效
3) provided:只在主程序和测试程序有效
4) runtime:只在测试程序和打包(运行有效)

## 9.2查看依赖是否在作用范围有效
以compile默认值,logback依赖为例

### 9.2.1在主程序内
![[Pasted image 20241014102506.png]]
### 9.2.2在测试程序内
![[Pasted image 20241014102653.png]]

### 9.2.3在打包(运行内)
![[Pasted image 20241014104810.png]]
![[Pasted image 20241014105418.png]]

# 10.maven的生命周期
==1.maven的生命周期就是为了对所有的maven项目构建进行抽象和统一
2.每套生命周期包含一些阶段,阶段是有顺序的,后面的阶段依赖于前面的阶段
3.在同一套生命周期中,后面的阶段运行前面的阶段都会运行==
maven中有三套相互独立的生命周期
1) clean:清理工作
2) default:核心工作,如:编译,测试,打包,安装,部署等
3) site:生成报告,发布站点等

## 10.1生命周期的阶段
1) clean:移除上一次构建生成的文件
2) compile:编译项目源代码
3) test:使用合适的单元测试框架进行测试
4) package:将编译后的文件打包
5) install:安装项目到本地仓库
![[Pasted image 20241014110711.png]]

## 10.2执行生命周期的两种方式
1) 方式一:RUN Maven Build或者双击生命周期
![[Pasted image 20241014110818.png]]
2) 方式二:通过命令行,mvn+生命周期 ![[Pasted image 20241014111818.png]]
例:
```
mvn clean
```
