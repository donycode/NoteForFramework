# NoteForFramework
Study notes of the Framework
#Struts2-day01

一、框架概述
什么是框架，为什么使用框架，框架优点
框架（framework）是一个基本概念上的结构，用于去解决或者处理复杂的问题
框架，即framework。其实就是某种应用的半成品，就是一组组件，供你选用完成你自己的系统。简单说就是使用别人搭好的舞台，你来做表演。
框架是在特定的领域内解决问题。
优点
重用代码大大增加，软件生产效率和质量也得到了提高
使用框架开发，它提供统一的标准，大大降低了我们的后期维护。
学习框架重点:了解框架做了什么，我们要在这个基础上在做什么事情。


二、java开发中常用框架
SSH   (SSM  SSI)
SSH  struts2  spring  hibernate
SSM(SSI) springmvc spring mybatis(ibatis)

SSH 它是企业开发中比较主流的一套架构。
SSH框架在开发中所处的位置:

三、 Struts2框架介绍
什么是struts2框架，学习struts2框架的核心。
Struts2是一个基于MVC设计模式的Web应用框架，它本质上相当于一个servlet，在MVC设计模式中，Struts2作为控制器(Controller)来建立模型与视图的数据交互
Struts2=struts1+webwork

问题:struts2是一个mvc框架，它的mvc是什么?

javaweb开发中的mvc,是在jsp的model2模式中提过
Model------javabean
View--------jsp
Controller----servlet

核心点:
1.拦截器 interceptor
2.Action
3.ognl与valueStack

在现在开发中与struts2比较类似的框架有哪些?
Struts1  webwork  springmvc  jsf

Struts2框架流程


四、今天内容介绍与重点

今天内容：
一个简单的登录案例


在这个案例中，我们要使用struts2框架怎样解决

重点:
1.struts2框架如何完成原来由servlet完成的工作。
2.Struts2框架如何完成请求参数的封装处理
3.Struts2框架如何完成页面跳转。




五、简单登录案例原型
需要三个jsp页面  login.jsp   success.jsp  failer.jsp
还需要一个servlet   LoginServlet 主要完成的是业务逻辑操作。

login.jsp

LoginServlet



六、Struts2框架来完成登录操作
1．问题:为什么使用struts2框架？
Struts2框架它是一个在web中应用的mvc框架。
我们使用strtus2框架来完成web开发有什么优势？


2．问题：怎样使用strtuts2框架
首先要上网下载它的jar包。
步骤:
1.导入相关的jar文件
2.需要在web.xml文件中配置一个Filter（只有配置了它才可以使用struts2框架）
3.struts.xml配置
4.创建Action来完成逻辑操作

3．快速入门
我们使用的是struts2 2.3.24版本
我们使用strtus2框架不是直接将它的lib包下的所有的jar文件copy到项目中，而是使用其中的一部分。
我们可以参考它的示例代码：

1.导入13个jar包
2.需要在web.xml文件中配置StrutsPrepareAndExecuteFilter--前端控制器
3.创建一个struts.xml文件,它的位置是可以放置在src下。

3.1．代码实现
jsp页面

Action

struts.xml文件配置

3.2．流程分析


4．使用struts2完成简单登录操作
1.login.jsp页面不变动
2.创建一个LoginAction来完成逻辑操作
3.在struts.xml文件中完成配置操作

问题1:在LoginAction中如何得到username与password
可以直接在Action类中提供成员属性，并为其提供get/set方法。
就可以得到请求参数

问题2:如果实现路径跳转？
1.我们可以给action中的方法添加一个String返回值
2.在struts.xml配置文件中，在其对应的action配置上通过<result>来确定跳转的路径。


七、Struts2框架执行流程
1．Struts2源码导入

对于struts2框架它的源代码我们主要使用三部分
1.struts2核心部分源代码  org.apache.struts2xx
src\core\src\main\java
2.struts2的xwork核心部分源代码
src\xwork-core\src\main\java\com\opensymphony\xwork2
3.struts2的插件的源代码
src\plugins
2．关于struts.xml配置文件中提示问题
第一步
在eclipse的window下首选面中查找xml catalog
第二步
Location:配置本地的dtd文件路径
key type:选择URI
Key: http://struts.apache.org/dtds/struts-2.3.dtd
注意版本要对应，如果你可以上网，那么会自动缓存dtd,具有提示功能。


3．执行流程介绍
1.当通过浏览器发送一个请求
2.会被StrutsPrepareAndExecuteFilter拦截
3.会调用strtus2框架默认的拦截器(interceptor)完成部分功能
4.在执行Action中操作
5.根据Action中方法的执行结果来选择来跳转页面Resutl视图

一般管StrutsPrepareAndExecuteFilter 叫做前端控制器(核心控制器)，只有配置了这个filter我们的strtus2框架才能使用。
Strtus2的默认拦截器(interceptor)它们是在struts-default.xml文件中配置
注意:这上xml文件是在strtus-core.jar包中。
默认的拦截器是在defaultStack中定义的。

八、Struts2配置详解
1．Struts2配置文件加载顺序

第一个加载的是default.properties文件
位置:strtus2-core.jar包   org.apache.struts2包下
作用:主要是声明了struts2框架的常量 
第二个加载的是一批配置文件
Strtus-default.xml
位置:struts2-corl.jar 
作用:声明了interceptor  result  bean
Strtus-plugin.xml
位置:在strtus2的插件包中
作用:主要用于插件的配置声明
Strtus.xml
位置:在我们自己的工程中
作用:用于我们自己工程使用strtus2框架的配置
第三个加载的是自定义的strtus.properties
位置:都是在自己工程的src下
作用:定制常量
第四自定义配置提供
第五加载的是web.xml配置文件
主要是加载strtus2框架在web.xml文件中的相关配置.
第六 bean相关配置

重点掌握:
1.Default.properties
2.Struts-default.xml
3.Struts-plugin.xml
4.Strtus.xml
5.web.xml


2．struts.xml文件配置介绍
2.1．package配置
1.name属性  作用:定义一个包的名称，它必须唯一。
2.namespace属性 作用:主要是与action标签的name属性联合使用来确定一个action	的访问路径
3.extends属性 作用:指定继承自哪个包。一般值是strtus-default
		strtus-default包是在strtus-default.xml文件中声明的。
4.abstruct属性 它代表当前包是一个抽象的，主要是用于被继承 
2.2．action配置
1.name属性 作用:主要是与package的namespace联合使用来确定一个action的访问路	径
2.class属性  作用:用于指示当前的action类
3.method属性  作用:用于指示当前的action类中的哪个方法执行
2.3．result配置
它主要是用于指示结果视图
1.name属性 作用是与action类的method方法的返回值进行匹配，来确定跳转路径
2.type属性 作用是用于指定跳转方式(默认是转发forward)
2.4．扩展
关于action配置中的class与method的默认值以及result中的name与type 默认值问题

原因:strtus-default.xml文件中配置

它的作用就是当一个请求来时，如果查找不到指定的class及对应的method就会执行
ActionSupport类中的execute方法。
在这个类的execute方法中默认返回的是”success”
也就是说，result的name属性默认值是success,默认的跳转方式是请求转发 dispatcher

3．常量配置
default.properties文件中定义了struts2框架常用常量 .
问题:我们怎样可以定义常量 
1.可以在src下创建一个strtus.properties配置文件
2.可以在web.xml文件中配置
3.可以直接在strtus.xml文件中定义常量 (推荐)


注意:后加载的配置文件中的常量会将先加载的常量覆盖

九、Struts2的Action详解
Struts2中的action，主要是完成业务逻辑操作。Action替代在servlet中完成的作用。
Action的学习主要有两点
1.如何创建一个struts2的action
2.如果访问一个struts2的action

1．Action类创建方式(三种)
1.创建一个pojo类
Pojo(plani Ordinary java object)简单的java对象
Pojo类就是没有实现任何接口没有继承任何类
优点:无耦合
缺点:所有的功能都要自己完成

2.创建一个类实现一个Action接口
com.opensymphony.xwork2.Action

在Action接口中定义了五个常量，一个execute方法
五个常量:它们是默认的五个结果视图<result name=””>:
ERROR : 错误视图
INPUT: 它是struts2框架中interceptor中发现问题后会访问的一个视图
LOGIN:它是一个登录视图，可以在权限操作中使用
NONE:它代表的是null,什么都不做（也不会做跳转操作）
SUCCESS:这是一个成功视图
优点：耦合度低
缺点:还是需要自己来完成功能

3.创建一个类继承ActionSupport类
com.opensymphony.xwork2.ActionSupport
ActionSupport类也实现了Action接口。
我们在开发中一般会使用这种方案:
优点:具有丰富的功能，例如  表单校验 错误信息设置  国际化
缺点:耦合度高
2．action的访问方式
1.直接通过<action>标签来配置，通过method来指定访问的方法，如果method没有，默认访问的是execute方法。
2.简化的action访问方式，可以使用*通配符来访问。
这种方式的缺点:不建议使用过多的*号，它带来程序阅读障碍，不便于理解
使用*来简化操作方案，它对名称规范必须进行一个统一。




3．扩展--动态方法调用

这是strtus2提供的动态方法调用。

注意:对于strtus2的动态方法调用，要想使用我们必须配置一个常量来开启动态方法调用

这代表动态方法调用没有开启

个人不建议使用动态方法调用
十、Struts2框架封装数据
主要解决的问题:是在action中如果获取请求参数

主要有两种方式:
1.属性驱动
a.直接在action类中提供与请求参数匹配属性，提供get/set方法
b.在action类中创始一个javaBean,对其提供get/set ，在请求时页面上要进行修改，  	例如 user.username  user.password ,要使用ognl表达式
以上两种方式的优缺点:
第一种比较简单，在实际操作我们需要将action的属性在赋值给模型(javaBean)	去操作
	第二种:不需要在直接将值给javaBean过程，因为直接将数据封装到了javaBean	中。它要求在页面上必须使用ognl表达式，就存在页面不通用问题。

2.模型驱动
步骤:
1.让Action类要实现一个指定接口ModelDriven
2.实例化模型对象(就是要new出来javaBean)
3.重写getModel方法将实例化的模型返回。


对于模型驱动它与属性驱动对比，在实际开发中使用比较多，模型驱动缺点，它只能对	一个模型数据进行封装。

 

十一、总结
 
今天主要内容是围绕着简单的登录案例来讲解:
1.关于strtus2框架的环境搭建
2.关于strtus2框架配置
3.关于strtus2框架请求参数封装
4.关于strtus2框架的路径跳转



关于action访问的配置
<package name=””  namespace=””  extends=””>
<action  name=””  class=””  method=””>

<result name=”” type=””>路径</result>
</action>

</package>

关于路径跳转问题:
是通过<result>来配置跳转的路径.
它的name属性是与action中的方法的返回值进行对比的。
它的type属性可以取哪些值?

默认值是dispatcher 它代表的是请求转发。针对于jsp页面
redirect  它代表的是重定向   针对于jsp页面 
chain  它类似于请示转发，只不过它是针对于action跳转.
redirectAction 它类似于重定向  针对于action
关于路径跳转的配置
可以直接在<package>下创建全局的result



