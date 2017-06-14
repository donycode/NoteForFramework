# Note For Framework
Study notes of the Framework
# Struts2
## day01 了解struts的执行流程
### keywords: struts.xml文件配置介绍
1. **package name**="whatever1"
2. 方式一  **action name**="whatever2"
   方式二  **action name**="whatever_*"   *前面的随便是什么英文字符,*是通配符 表示Action类里面的方法名称,出现在method="{1}"中1的位置
3. **result name**="Action类中*方法的返回值" 根据此返回值配置路径

***package配置***
1.name属性  作用:定义一个包的名称，它必须唯一。
2.namespace属性 作用:主要是与action标签的name属性联合使用来确定一个action的访问路径
3.extends属性 作用:指定继承自哪个包。一般值是strtus-default
		strtus-default包是在strtus-default.xml文件中声明的。
4.abstruct属性 它代表当前包是一个抽象的，主要是用于被继承 
***action配置***
1.name属性 作用:主要是与package的namespace联合使用来确定一个action的访问路径
2.class属性  作用:用于指示当前的action类
3.method属性  作用:用于指示当前的action类中的哪个方法执行
***result配置***
它主要是用于指示结果视图
1.name属性 作用是与action类的method方法的返回值进行匹配，来确定跳转路径
2.type属性 作用是用于指定跳转方式(默认是转发forward)



### Examples
action类中:
```
package cn.itheima.action;

import com.opensymphony.xwork2.ActionSupport;

public class Struts2Action extends ActionSupport {
    public String add() {

        System.out.println("add");
        return NONE;

    }

    public String execute() {//execute是默认方法名,如果访问localhost:8080/st_ 即可访问此action方法    
          System.out.println("execute");
        return "rrr";
    }

    public String del() {

        System.out.println("del");
        return "aaa";

    }


}
```
struts.xml 文件中:
```
    <package name="default" namespace="/" extends="struts-default">
    <!--第二种方式访问action 通配符*  注意这里的{1} 里面的1表示第1个*的值  --> 
          <action name="st_*" class="cn.itheima.action.Struts2Action" method="{1}">   
          <result name="aaa">/index.jsp</result>
            <result name="rrr">/index.jsp</result>
           </action>
      </package>
      
    <package name="default" namespace="/" extends="struts-default">
    <!--第一种方式访问action 通配符* -->
           <!--  1 没有配置result, method匹配可以访问-->
        <action name="addAction" class="cn.itheima.action.Struts2Action" method="add">
            </action>
        <!--  2 resule name匹配,没有method执行默认方法execute-->
        <action name="exe" class="cn.itheima.action.Struts2Action">
            <result name="rrr">/index.jsp</result>
            </action>
        <!--  3 method匹配,result name也匹配,可以访问-->
        <action name="delAction" class="cn.itheima.action.Struts2Action" method="del">
            <result name="aaa">/index.jsp</result>
           </action>
    </package>
    ```
<!--第三种动态访问不推荐-->

tips:IDEA中报错找不类先看看包的导入是否正确

## day02 
### keywords:

### Examples
