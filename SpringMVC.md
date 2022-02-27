# SpringMVC

## MVC简单介绍

- Model：数据模型，提供要展示的数据，因此包含数据和行为，可以认为是领域模型或JavaBean组件（包含数据和行为），不过现在一般都分离开来：Value Object（数据Dao） 和 服务层（行为Service）。也就是模型提供了模型数据查询和模型数据的状态更新等功能，包括数据和业务。

- View:负责进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西。
  Controller（调度员）： 接收用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。也就是说控制器做了个调度员的工作。

- 最常用的MVC：（Model）Bean +（view） Jsp +（Controller） Servlet

  

关于MVC的流程：

1. 用户发请求
2. Servlet接收请求数据，并调用对应的业务逻辑方法
3. 业务处理完毕，返回更新后的数据给servlet
4. servlet转向到JSP，由JSP来渲染页面
5. 响应给前端更新后的页面

![image-20220216163348084](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220216163348084.png)

pom.xml:创建maven父工程

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.ssl</groupId>
    <artifactId>SpringMVC</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
    <!--父工程导入依赖-->
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.4.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.12</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.10.0</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.62</version>
        </dependency>

    </dependencies>

    <!--资源过滤器，防止导入资源失败问题，最好在父子pom.xml里都加入一下代码-->
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>

            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>

</project>

```

1. 创建子工程，idea右键Add Framwork Support添加web支持
2. 实现HelloServlet继承HttpServlet接口，并创建/WEB-INF/jsp/test.jsp

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        获取前端参数
        String method = req.getParameter("method");
        if (method.equals("add")){
            req.getSession().setAttribute("msg","执行add方法");
        }
        if (method.equals("delete")){
            req.getSession().setAttribute("msg","执行了delete方法");
        }
//        调用业务层

//        重定向
        req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req,HttpServletResponse resp) throws ServletException,IOException {
        doGet(req,resp);
    }
}

```

web.xml:

![image-20220216165504755](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220216165504755.png)

test.jsp:

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 10130
  Date: 2022/1/28
  Time: 14:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>test</title>
</head>
<body>
${msg}
</body>
</html>

```

form.jsp:

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>form</title>
</head>
<body>
<form action="/hello" method="post">
    <input type="text" name="method">
    <input type="submit">
</form>
</body>
</html>

```

![image-20220216165040389](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220216165040389.png)

![image-20220216165100685](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220216165100685.png)

## 介绍SpringMVC

- SpringMVC是Spring框架中的一个分支，是基于java实现MVC的轻量级Web框架
- Spring的web框架围绕**DispatcherServlet** [ 调度Servlet ] 设计的。

![image-20220216170049897](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220216170049897.png)

### 执行原理

![image-20220217114600427](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217114600427.png)

**SpringMVC底层工作原理：**

1. DispatcherServlet表示前置控制器，是整个SpringMVC的控制中心。用户发出请求，DispatcherServlet接收请求并拦截请求。
2. 假设url为 : http://localhost:8080/SpringMVC/hello
3. 服务器域名：http://localhost:8080
4. web站点：/SpringMVC
5. hello表示控制器：/hello
6. 通过分析，如url表示：请求位于服务器ST:8080上的SpringMVC站点的hello控制器
7. HandlerMapping为处理器映射。DispatcherServlet调用HandlerMapping,HandlerMapping根据请求url查找Handler。
8. HandlerExecution表示具体的Handler,其主要作用是根据url查找控制器，如上url被查找控制器为：hello。
9. HandlerExecution将解析后的信息传递给DispatcherServlet,如解析控制器映射等。
10. HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler。
11. Handler让具体的Controller执行。
12. Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView。
13. HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。
14. DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名。
15. 视图解析器将解析的逻辑视图名传给DispatcherServlet。
16. DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。
17. 最终视图呈现给用户。

### 不使用注解开发：

- 配置web.xml ：完成DispatcherServlet，关联resources配置文件


![image-20220217120208675](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217120208675.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--配置DispatcherServlet:SpringMVC核心-->
    <servlet>
        <servlet-name>Springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--关联一个SpringMvc的resource配置文件-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc_servlet.xml</param-value>
        </init-param>
        <!--启动级别-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <!--匹配所有的请求： / :只匹配请求，不包含所有的.jsp
                      /*:匹配所有的请求，包括jsp页面
    -->
    <servlet-mapping>
        <servlet-name>Springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>

```

- 配置springmvc_servlet.xml:获得视图解析器，映射器，适配器，绑定跳转url

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--处理器映射器HandlerMapping:查找访问的url控制器-->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <!--处理器适配器HandlerAdapter：controller将处理好的数据返回给HandlerAdapter-->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
     <!--视图解析器ViewResolver：将后端处理好的数据和视图传给DispatchServlet，DS再交给ViewResolver先解析一遍，确认无误再传给前端
        必须熟悉，以后还要学模版引擎Thymeleaf/Freemarker...
        1 获取ModeAndView的数据
        2 解析ModeAndView的视图名字
        3 拼接视图名字，找到对应的视图 WEB-INF/jsp/hello.jsp
    -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
     <!--BeanNameUrlHandlerMapping处理器：绑定跳转的url=页面访问的网址-->
    <bean id="/hello" class="com.kuang.controller.HelloController"/>
</beans>
```

- /WEB-INF/jsp/hello.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>hello</title>
</head>
<body>
<%--接受传递的参数--%>
${msg}
</body>
</html>

```

- HelloController实现Controller 访问：http://localhost:8080/hello

```java
package com.kuang.controller;



import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.lang.annotation.Annotation;

public class HelloController implements Controller {

    @Override
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
//       ModelAndView:模型和视图
        ModelAndView mv = new ModelAndView();
//        封装对象，放在ModelAndView中
        mv.addObject("msg","HelloSpringMVC");
//        封装要跳转的视图，放在ModelAndView
        mv.setViewName("hello");//: /WEB-INF/jsp/hello.jsp
        return mv;
    }
}

```

SpringMVC原理回顾：

- 反复观看，理解原理，结合代码分析

![image-20220217125129132](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217125129132.png)

### 使用注解开发：

- web.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

- springmvc-servlet.xml:注解省略了映射器，适配器，专注于写视图解析器；跳转的Controller也不用配置进Spring


```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
    <context:component-scan base-package="com.kuang.controller"/>
    <!--让SpringMvc不处理静态资源。让.css,.js等不进视图解析器-->
    <mvc:default-servlet-handler/>
    <!--注解加载映射器、适配器，不用之前那么麻烦配置了-->
    <mvc:annotation-driven/>
    <!--配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

![image-20220217130918833](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217130918833.png)

- WEB-INF/jsp/hello.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>hello</title>
</head>
<body>
${msg}
</body>
</html>
```

- HelloController
  - 简化了实现的接口，使用@注解配置映射器
  - 访问：http://localhost:8080/hello

![image-20220217131936611](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217131936611.png)

```java
package com.kuang.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {
    @RequestMapping("/h1")
    public String hello(Model model){
//        封装数据
        model.addAttribute("msg","hello,springmvcannotation");
        return "hello";//会被视图解析器处理
    }
}
```

### Controller：

- 配置web.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springMvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring_mvc_servlet.xml</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

   <!-- <filter>
        <filter-name>encode</filter-name>
        <filter-class>com.ssl.filter.EncodeFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>encode</filter-name>
        <url-pattern>/</url-pattern>
    </filter-mapping>-->
    <filter>
        <filter-name>encode</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encode</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>

```

- springmvc_servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!--自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
    <context:component-scan base-package="com.kuang.controller"/>
    <!--让SpringMvc不处理静态资源。让.css,.js等不进视图解析器-->
    <mvc:default-servlet-handler/>
    <!--注解加载映射器、适配器，不用之前那么麻烦配置了-->
    <mvc:annotation-driven/>
    <!--以上的是定死的代码，
        以下是配置视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--不使用注解开发的适配器：/demo1,注意点是id需要配置/-->
    <bean name="/t1" class="com.kuang.controller.ControllerTest01"/>
</beans>
```

#### Controller

- 不使用注解，非常不推荐使用，因为：
  - 配置麻烦：<bean name="/t1" class="com.kuang.controller.ControllerTest01"/>，并且需要implements Controller
  - 不够灵活，太费力气，浪费时间

```java
package com.kuang.controller;

import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
//只要实现了Controller接口的类就说明这就是一个控制器了
public class ControllerTest01 implements Controller {
    @Override
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","ControllerTest1");
        mv.setViewName("admin/test");
        return mv;
    }
}
```

![image-20220217133848147](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217133848147.png)

#### @Controller

- 使用注解开发，@Controller注册进Spring容器，如果返回值是String，并且有具体的页面可以跳转，那么就会被视图解析器解析

```java
package com.kuang.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller//代表整个类会被spring接管
public class ControllerTest02 {
    @RequestMapping("/t2")
public String test1(Model model){
    model.addAttribute("msg","ControllerTest02");
    return "admin/test";
}
}
```

#### @RequestMapping

- 可以在类和方法上url访问路径
- 访问：http://localhost:8080/controller/demo3

```java
package com.kuang.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/controller")
public class ControllerDemo3 {
    @RequestMapping("/demo3")
    public String test1(Model model) {
        model.addAttribute("demo3", "demo3");
        return "demo3";
    }
}
```
#### RestFul风格

- 优点：
  - 最大的优势是安全，看不出源代码的参数和意义
  - 实现地址复用，使得get和post访问url相同，框架会自动进行类型转换
  - 高效：支持缓存

- 缺点：
  - 不像原生的url见名知意，url理解不直观

- 实现方式：

  - url `@GetMapping("/addRest/{a}/{b}")` + 参数`@PathVariable int a, @PathVariable int b`

  - url `@PostMapping("/addRest/{a}/{b}")` + 参数不变`@PathVariable int a, @PathVariable int b`

```java
package com.kuang.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class RestFulController {
//    http://localhost:8080/springmvc_controller_war_exploded/add?a=1&b=2
//    http://localhost:8080/springmvc_controller_war_exploded/add/a/b
       /**
     * 复用相同的url
     * RestFul方式二：method=post，使用RestFul的话，请求的url和GET就一样了
     */
    @PostMapping(value="/add/{a}/{b}")
    public String test1(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果1为"+res);
        return "admin/test";
    }
      /**
     * RestFul方式一：method = get
     * RequestMapping("/addRest/{a}/{b}" method=requestMethod.GET) = @GetMapping()
     * http://localhost:8080/springmvc_controller_war_exploded/addRest/1/1
     */
    @GetMapping(value="/add/{a}/{b}")
    public String test2(@PathVariable int a, @PathVariable int b, Model model){
        int res = a+b;
        model.addAttribute("msg","结果2为"+res);
        return "admin/test";
    }
      /**
     * 原生的url：http://localhost:8080/springmvc_04/add?a=1&b=1
     */
    @RequestMapping("/add")
    public String getAdd1(int a, int b, Model model) {
        int result = a + b;
        model.addAttribute("add", "原生的url：结果为" + result);
        return "add";
    }

```

### 重定向和转发

- 可以使用原生的request转发或者response重定向
- 推荐使用SpringMvc的`return “forward:xxx”/"redirect:xxx"`

```java
@Controller
public class ModelTest1 {
    //原生的转发：返回值是void，没有经过视图解析器；原生的重定向同样如此，都不走视图解析器，直接重定向
    @RequestMapping("/test1")
    public void test1(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String id = request.getSession().getId();
        System.out.println(id);
        request.getRequestDispatcher("index.jsp").forward(request,response);
    }
    //SpringMvc转发：测试结果是不走视图解析器，url没变是转发
    @RequestMapping("/test2")
    public String test2(Model model) {
        model.addAttribute("demo1","这是test2中的Spring转发");
        return "forward:/WEB-INF/jsp/demo1.jsp";
    }
    //SpringMvc重定向：测试结果是不走视图解析器
    @RequestMapping("/test3")
    public String test3() {
        System.out.println("跳转回首页index.jsp");
        return "redirect:index.jsp";
    }
}
```

#### 接受请求参数和数据回显

- 前端提交的name和后端映射器接受的形参名一样，则直接接受
- 前端提交的name和后端映射器接受的形参名不用一样，再形参前`@RequestParam("xxx")`更改名称一致
- 后端参数封装如果成一个pojo，前端传过来的name会自动pojo中的成员属性，不匹配的属性=null/0

```java
package com.kuang.controller;

import com.kuang.pojo.User;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
@RequestMapping("/user")
public class UserController {
    @GetMapping("/t1")
//    @RequestParam指定前端接受参数
    public String test1(@RequestParam("username") String name, Model model){
//        接受前端参数
        System.out.println("接收到前端的参数为"+name);
//        将返回的结果传递给前端
        model.addAttribute("msg",name);
//        视图跳转
        return "admin/test";
    }
//    前端接受的是一个对象：id，name，age
    /*
    * 1.接受前端用户传递的参数，判断参数的名字。假设名字直接在方法上，可以直接使用
    * 2.假设传递的是一个对象User，匹配User对象中的字段名，如果名字一致则OK否则就匹配不到
    */
    @GetMapping("/t2")
    public String test2(User user){
        System.out.println(user);
        return "admin/test";
    }
    /*
    * Model只有寥寥几个方法只适合于储存数据，简化了新手对Model对象的操作和理解
    * ModelMap继承了LinkedMap除了实现自身一些方法，同样继承LinkedMap的方法和特性
    * ModelAndView可以在存储数据的同时，进行设置返回的逻辑视图，进行控制展示层的跳转
    */
    @GetMapping("/t3")
    public String test3(ModelMap map){

        return "admin/test";
    }
}

```

![image-20220217202926490](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217202926490.png)

![image-20220217203939454](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217203939454.png)

![image-20220217203801353](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217203801353.png)

#### 解决乱码问题

- 方法一：web.xml里面配置的SpringMVC自带的过滤器CharacterEncodingFilter
  - **`<url-pattern>/\*</url-pattern>`：因为要跳转到xxx.jsp页面，所以url是/\*(≠/)**

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--配置SpringMVC-->
    <servlet>
        <servlet-name>springMvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring_mvc_servlet.xml</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!--web容器解决中文乱码问题-->
    <filter>
        <filter-name>encode</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encode</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```

- 方法二：一劳永逸，但需要重启Tomcat服务器，修改Tomcat里面的server.xml配置文件：URIEncoding = "UTF-8"

```xml
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443"
           URIEncoding = "UTF-8"/>
<!-- A "Connector" using the shared thread pool-->
```

## Json

### 前端初识Json

- 前端展示两者数据，学会js和json互相转换

```jsp
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>json</title>
    <script type="text/javascript">
        //user是一个js对象
        var user = {
            name : "秦疆",
            age : 3,
            sex :"男"
        };
        //将js对象转换为json对象
        var json = JSON.stringify(user);
        console.log(json);
        console.log("===========================")
        //将JSON对象转换为javaScript对象
        var obj = JSON.parse(json);
        console.log(obj);
    </script>
</head>
<body>

</body>
</html>
```

![image-20220217205257563](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217205257563.png)

### Jackson Databing与 FastJson

- **使用 Jackson Databind可以快速生成json数据**

导入依赖：

```xml
 <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.13.1</version>
        </dependency>
```

json=一个字符串，所以会与有中文乱码问题，需要在springmvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!--自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
    <context:component-scan base-package="com.kuang.controller"/>
    <!--让SpringMvc不处理静态资源。让.css,.js等不进视图解析器-->
    <mvc:default-servlet-handler/>
     <!--注解加载映射器、适配器，解决Json数据中文乱码问题-->
    <mvc:annotation-driven>
        <mvc:message-converters register-defaults="true">
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <constructor-arg value="UTF-8"/>
            </bean>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false"/>
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <!--配置视图解析器，明确json数据不走数据解析器，直接传给前端-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

编写Controller：

- @ResponseBody：该方法不走视图解析器，返回一个json数据

- @RestControoler:该类下所有方法不走视图解析器，返回一个json数据

- 访问：http://localhost:8080/t1，页面显示一个json数据，不经过视图解析器

- 回顾日期：new SimpleDateFormat("yyyy-MM-dd:HH:mm:ss")

```java
package com.kuang.utils;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;

import java.text.SimpleDateFormat;

public class JsonUtils {
    public static String getJson(Object object){
        return getJson(object,"yyyy-MM-dd HH:mm:ss");
    }
    public static String getJson(Object object,String dateFormat){
        ObjectMapper mapper = new ObjectMapper();
        mapper.configure(SerializationFeature.WRITE_DATE_KEYS_AS_TIMESTAMPS,false);
        SimpleDateFormat sdf = new SimpleDateFormat(dateFormat);
        mapper.setDateFormat(sdf);
        try {
            return mapper.writeValueAsString(object);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        return null;
    }
}

```

上述代码是JsonUtils.java

- **FastJson是阿里巴巴官方提供的，实现Json数据的另一个工具，比JackSon Databind更方便**

导包：

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.62</version>
</dependency>
```


```java
package com.kuang.controller;

import com.alibaba.fastjson.JSON;
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.kuang.pojo.User;
import com.kuang.utils.JsonUtils;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.SimpleTimeZone;

@Controller
//@RestController
public class UserController {
    @RequestMapping("/j1")
    @ResponseBody//它就不会走视图解析器，会直接返回一个字符串
    public String json1() throws JsonProcessingException {
//        jackson,ObjectMapper
        ObjectMapper mapper = new ObjectMapper();
//        创建一个对象
        User user = new User("秦疆一号",3,"男");
        String str = mapper.writeValueAsString(user);
        return str;
    }
    @RequestMapping("/j2")
    @ResponseBody
    public String json2() throws JsonProcessingException {
//        jackson,ObjectMapper
        ObjectMapper mapper = new ObjectMapper();
        List<User> userList = new ArrayList<>();
//        创建一个对象
        User user1 = new User("秦疆一号",3,"男");
        User user2 = new User("秦疆er号",3,"男");
        User user3= new User("秦疆san号",3,"男");
        userList.add(user1);
        userList.add(user2);
        userList.add(user3);
        String str = mapper.writeValueAsString(userList);
        return str;
    }
    @RequestMapping("/j3")
    @ResponseBody
    public String json3() throws JsonProcessingException {
        Date date = new Date();
        return JsonUtils.getJson(date);
    }
    //比Jackson使用更方便
    @RequestMapping("/j4")
    @ResponseBody
    public String json4() throws JsonProcessingException {
        List<User> userList = new ArrayList<>();
//        创建一个对象
        User user1 = new User("秦疆一号",3,"男");
        User user2 = new User("秦疆er号",3,"男");
        User user3= new User("秦疆san号",3,"男");
        userList.add(user1);
        userList.add(user2);
        userList.add(user3);
        String string = JSON.toJSONString(userList);
        return string;
    }
}
```

![image-20220217211624799](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217211624799.png)

![image-20220217211751270](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217211751270.png)

![image-20220217213330103](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217213330103.png)

![image-20220217213349924](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217213349924.png)

## SSM整合

### 环境

- IDEA+Mysq5.7+Tomca5.7+Maven3.6

- 数据库

  create database `ssmbuild`;
  use `ssmbuild`;
  CREATE TABLE `books` (
    `bookId` int(10) NOT NULL AUTO_INCREMENT COMMENT '书id',
    `bookName` varchar(100) NOT NULL COMMENT '书名',
    `bookCounts` int(11) NOT NULL COMMENT '数量',
    `detail` varchar(200) NOT NULL COMMENT '描述',
    KEY `bookId` (`bookId`)
  ) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8

- pom.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
  
      <groupId>com.ssl</groupId>
      <artifactId>ssmbuild</artifactId>
      <version>1.0-SNAPSHOT</version>
      <!--依赖:junit,数据库驱动，连接池，Servlet，jsp，mybatis,mybatis-mvc,Spring,SpringMVC-->
      <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
          </dependency>
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <version>5.1.47</version>
          </dependency>
          <dependency>
              <groupId>com.mchange</groupId>
              <artifactId>c3p0</artifactId>
              <version>0.9.5.2</version>
          </dependency>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>servlet-api</artifactId>
              <version>2.5</version>
          </dependency>
          <dependency>
              <groupId>javax.servlet.jsp</groupId>
              <artifactId>jsp-api</artifactId>
              <version>2.2</version>
          </dependency>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>jstl</artifactId>
              <version>1.2</version>
          </dependency>
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis</artifactId>
              <version>3.5.2</version>
          </dependency>
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis-spring</artifactId>
              <version>2.0.2</version>
          </dependency>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-webmvc</artifactId>
              <version>5.2.4.RELEASE</version>
          </dependency>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-jdbc</artifactId>
              <version>5.0.5.RELEASE</version>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <version>1.18.12</version>
          </dependency>
      </dependencies>
  
  
      <!--Maven资源过滤设置-->
      <build>
          <resources>
              <resource>
                  <directory>src/main/resources</directory>
                  <includes>
                      <include>**/*.properties</include>
                      <include>**/*.xml</include>
                  </includes>
                  <filtering>true</filtering>
              </resource>
  
              <resource>
                  <directory>src/main/java</directory>
                  <includes>
                      <include>**/*.properties</include>
                      <include>**/*.xml</include>
                  </includes>
                  <filtering>true</filtering>
              </resource>
          </resources>
      </build>
  </project>
  
  ```

### 开发

- 需求分析+设计数据库+业务+传给前端页面

![image-20220217222105566](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220217222105566.png)

### 整合Mybatis

- mybatis-config.xml:数据库连接交给spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
     <!--配置数据源，交给Spring去做-->
    <typeAliases>
        <!--resultMap:默认类名小写为使用id-->
        <package name="com.kuang.pojo"/>
    </typeAliases>
    <mappers>
        <mapper class="com.kuang.dao.BookMapper"/>
    </mappers>
</configuration>
```

```properties
# db.properties配置文件
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/ssmbuild?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8
username=root
password=123456
```

### 整合Spring

- spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <!--1 关联数据库配置文件-->
    <context:property-placeholder location="classpath:database.properties"/>
     <!--2 连接池 这次使用c3p0的连接池.常见的数据库：
    dbcp:半自动操作，不能自动连接
    c3p0：自动化操作，并且可以配置到对象中
    druid,hikari(SpringBoot)-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="user" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="maxPoolSize" value="30"/>
        <property name="minPoolSize" value="10"/>
        <property name="autoCommitOnClose" value="false"/>
        <property name="checkoutTimeout" value="10000"/>
        <property name="acquireRetryAttempts" value="2"/>
    </bean>
    <!--3 sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--绑定数据库-->
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis的配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>
     <!--4 配置dao接口扫描包，动态的实现了dao接口可以注入到Spring容器中,不用写mapperImpl.xml-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--注入sqlSessionFactory-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
        <!--扫描要扫描的dao的包-->
        <property name="basePackage" value="com.kuang.dao"/>
    </bean>
</beans>
```

- spring-service.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <!--1 扫描service下的包-->
<context:component-scan base-package="com.kuang.service"/>
    <!--2 将我们的所有业务类，注入到Spring,这里使用bean配置，平时是使用注解-->
    <bean id="BookServiceImpl" class="com.kuang.service.BookServiceImpl">
        <property name="bookMapper" ref="bookMapper"/>
    </bean>
    <!--3  声明式事务配置-->
    <bean id="transactionMan
        <property name="dataSource" ref="dataSource"/>
    </bean>
</beans>
```

- application.xml:导入其他配置进spring主配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <import resource="classpath:spring-mvc.xml"/>
    <import resource="classpath:spring-service.xml"/>
    <import resource="classpath:spring-dao.xml"/>
</beans>
```

### 整合SpringMVC

增加web项目的支持

- web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--SpringMVC配置-->
    <!--1 DispatcherServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
      <!--2 乱码过滤-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!--3 Session过期时间-->
    <session-config>
        <session-timeout>15</session-timeout>
    </session-config>
</web-app>
```

- spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!--1 注解驱动-->
    <mvc:annotation-driven/>
    <!--2 静态资源过滤-->
    <mvc:default-servlet-handler/>
    <!--3 扫描包：Controller-->
    <context:component-scan base-package="com.ssl.controller"/>
    <!--4 视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>

```

### dao层

- BookMapper接口和BookMapperMapper.xml

```java
package com.kuang.dao;

import com.kuang.pojo.Books;
import org.apache.ibatis.annotations.Param;

import java.util.List;

public interface BookMapper {
//    CRUD
    int addBook(Books books);
    int deleteBookById(@Param("bookId") int id);
    int updateBook(Books books);
    Books queryBookById(int id);
    List<Books> queryAllBook();
}

```

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.BookMapper">
    <insert id="addBook" parameterType="Books">
        insert into books (bookName,bookCounts,detail) values (#{bookName},#{bookCounts}，#{detail});
    </insert>
    <delete id="deleteBookById" parameterType="int">
        delete from books where bookID = #{bookId}
    </delete>
    <update id="updateBook" parameterType="Books">
        update books
        set bookName = #{bookName},bookCounts = #{bookCounts},detail=#{detail}
        where bookId =#{bookId};
    </update>
    <select id="queryBookById" resultType="Books">
        select * from books where bookID = #{bookId}
    </select>
    <select id="queryAllBooks" resultType="Books">
        select * from books
    </select>
</mapper>
```

### service层

```java
package com.kuang.service;

import com.kuang.pojo.Books;
import org.apache.ibatis.annotations.Param;

import java.util.List;

public interface BookService {
    int addBook(Books books);
    int deleteBookById(int id);
    int updateBook(Books books);
    Books queryBookById(int id);
    List<Books> queryAllBook();
}
```

```java
package com.kuang.service;

import com.kuang.dao.BookMapper;
import com.kuang.pojo.Books;
import org.springframework.beans.factory.annotation.Autowired;

import java.util.List;

public class BookServiceImpl implements BookService{

//注入Dao层
    private BookMapper bookMapper;
    public void setBookMapper(BookMapper bookMapper) {
        this.bookMapper = bookMapper;
    }

    @Override
    public int addBook(Books books) {
        return bookMapper.addBook(books);
    }

    @Override
    public int deleteBookById(int id) {
        return bookMapper.deleteBookById(id);
    }

    @Override
    public int updateBook(Books books) {
        return bookMapper.updateBook(books);
    }

    @Override
    public Books queryBookById(int id) {
        return bookMapper.queryBookById(id);
    }

    @Override
    public List<Books> queryAllBook() {
        return bookMapper.queryAllBook();
    }
}

```

