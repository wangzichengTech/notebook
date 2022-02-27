# Mybatis

## 简介

### 什么是Mybatis

- Mybatis是一款优秀的持久化框架
- 它支持自定义SQL，存储过程以及高级映射。MyBatis免除了几乎所有的JDBC代码以及设置参数和获取结果集的工作。Mybatis可以通过简单的XML或注解来配置和映射原始类型，接口和java POJO

### 持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程。
- 内存：断电即失
- 数据库，io文件持久化

为什么要持久化？

- 有一些对象，不能让他丢掉
- 内存太贵

### 持久层

Dao层，Service层，Controller层

- 完成持久化工作的代码块
- 层界限十分明显

### 为什么需要MyBatis

- 帮助程序员将数据存入到数据库中
- 方便
- 传统的JDBC代码太复杂了，简化，框架，自动化
- 不用MyBatis也可以，技术没有高低之分
- 优点：
  - 简单易学
  - 灵活
  - sql和代码的分离，提供可维护性
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql

## 第一个MyBatis

思路：搭建环境--》导入MyBatis--》编写代码--》测试

新建项目：

1. 创建一个普通的maven项目
2. 删除src目录 （就可以把此工程当做父工程了，然后创建子工程）
3. 导入maven依赖

```xml
 <dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13</version>
            <scope>test</scope>
        </dependency>
</dependencies>
```

  4.创建一个Module

- 编写mybatis的核心配置文件mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>
</configuration>
```

- 编写mybatis工具类

```java
package com.kuang.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            //使用mybatis第一步：获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。
    // 你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句

    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }

}
```

- 编写代码

Dao接口

```java
public interface UserDao {
    public List<User> getUserList();
}
```

接口实现类（由原来的UserDaoImpl转变为一个Mapper配置文件）

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace=绑定一个指定的Dao/Mapper接口-->
<mapper namespace="com.kuang.dao.UserDao">
    <select id="getUserList" resultType="com.kuang.pojo.User">
    select * from USER
  </select>
</mapper>
```

实体类

```java
package com.kuang.pojo;

public class User {

    private int id;
    private String name;
    private String pwd;

    public User() {
    }

    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pwd='" + pwd + '\'' +
                '}';
    }
}

```

**注意：**别忘记核心配置文件注册mappers

org.apache.ibatis.binding.BindingException: Type interface com.kuang.dao.UserDao is not known to the MapperRegistry.

**MapperRegistry是什么?**

核心配置文件中注册mappers

- junit测试

```java
    @Test
    public void test(){

        //1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //2.执行SQL
        // 方式一：getMapper
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> userList = userDao.getUserList();
        for (User user : userList) {
            System.out.println(user);
        }
        //关闭sqlSession
        sqlSession.close();
    }

```

## CRUD

1.**namespace**

namespace中的包名要和Dao/Mapper接口的包名一致

2.select

选择，查询语句；

- id：就是对应的namespace中的方法名
- resultType:Sql语句执行的返回值
- parameterType : 参数类型；

​    1.编写接口

```java
package com.kuang.dao;

import com.kuang.pojo.User;

import java.util.List;
import java.util.Map;

public interface UserDao {
//    模糊查询
    List<User> getUserLike(String value);

    List<User> getUserList();
//    根据ID查询用户
    User getUserById(int id);
//    插入一个用户
    int addUser(User user);
//    万能的Map
    int addUser2(Map<String,Object> map);
//    修改用户
    int updateUser(User user);
//    删除一个用户
    int deleteUser(int id);
}

```

​     2.编写对应的mapper中的sql语句

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.UserDao">
    <select id="getUserList" resultType="com.kuang.pojo.User">
        select * from user
    </select>
    <select id="getUserById" parameterType="int" resultType="com.kuang.pojo.User">
        select  * from user where id = #{id}
    </select>
    <insert id="addUser" parameterType="com.kuang.pojo.User">
        insert into user (id,name,pwd) values (#{id},#{name},#{pwd})
    </insert>
    <update id="updateUser" parameterType="com.kuang.pojo.User">
        update user set name= #{name},pwd = #{pwd} where id = #{id};
    </update>
    <delete id="deleteUser" parameterType="int">
        delete from user where id = #{id}
    </delete>

    <insert id="addUser2" parameterType="map">
        insert into user (id,name,pwd) values (#{userid},#{userName},#{passWord})
    </insert>
    <select id="getUserLike" resultType="com.kuang.pojo.User">
        select * from user where name like #{value}
    </select>
</mapper>
```

​     3.测试

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import com.kuang.utils.MybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class UserDaoTest {
   @Test
    public void test(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       try{
           UserDao userDao = sqlSession.getMapper(UserDao.class);
           List<User> userList = userDao.getUserList();
           for (User user : userList) {
               System.out.println(user);
           }
       }catch (Exception e){
           e.printStackTrace();
       }finally {
//           关闭SqlSession
           sqlSession.close();
       }
   }
   @Test
    public void getUserById(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();

       UserDao userdao = sqlSession.getMapper(UserDao.class);
       User user = userdao.getUserById(1);
       System.out.println(user);

       sqlSession.close();
   }
   @Test
    public void addUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserDao userdao = sqlSession.getMapper(UserDao.class);
       userdao.addUser(new User(4,"wangzi","1234567"));
//       提交事务
       sqlSession.commit();
       sqlSession.close();
   }
    //假设我们的实体类或者数据库中的表，字段或者参数过多，我们应该考虑使用Map
   @Test
   public void addUser2(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserDao userdao = sqlSession.getMapper(UserDao.class);
       Map<String, Object> map = new HashMap<>();
       map.put("userid",6);
       map.put("userName","Hello");
       map.put("passWord","123343");
       userdao.addUser2(map);
       sqlSession.close();

   }
   @Test
    public void updateUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserDao userdao = sqlSession.getMapper(UserDao.class);
       userdao.updateUser(new User(4,"www","123123"));
       sqlSession.commit();
       sqlSession.close();
   }
    @Test
    public void deleteUser(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        UserDao userdao = sqlSession.getMapper(UserDao.class);
        userdao.deleteUser(4);
        sqlSession.commit();
        sqlSession.close();
    }
    @Test
    public void getUserLike(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        UserDao userdao = sqlSession.getMapper(UserDao.class);
        List<User> userLike = userdao.getUserLike("%kuang%");
        for (User user : userLike) {
            System.out.println(user);
        }
        sqlSession.close();
    }
}

```

在模糊查询的时候可以在sql拼接中使用通配符

```xml
select * from user where name like "%"#{value}"%"
```

## 配置解析

### 核心配置文件

- mybatis-config.xml
- Mybatis的配置文件包含了会深深影响Mybatis行为的设置和属性信息。

configuration（配置）
    properties（属性）
    settings（设置）
    typeAliases（类型别名）
    typeHandlers（类型处理器）
    objectFactory（对象工厂）
    plugins（插件）
    environments（环境配置）
    	environment（环境变量）
    		transactionManager（事务管理器）
    		dataSource（数据源）
    databaseIdProvider（数据库厂商标识）
    mappers（映射器）

### 环境配置 environment

MyBatis可以配置成适应多种环境

不过要记住：尽管可以配置多个环境，但每个SqlSessionFactory实例只能选择一种环境

学会使用配置多套运行环境

MyBatis默认的事务管理器就是JDBC，连接池：POOLED

### 属性properties

我们可以通过properties属性来实现引用配置文件

这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置。【db.poperties】

编写一个配置文件：db.properties

```properties
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?userSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC
username=root
password=root
```

在核心配置文件中引入

```xml
<!--引用外部配置文件-->
<properties resource="db.properties">
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
</properties>
```

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部配置文件的

### 类型别名 typeAliases

- 类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置.
- 意在降低冗余的全限定类名书写。

```xml
<!--可以给实体类起别名-->
<typeAliases>
    <typeAlias type="com.kuang.pojo.User" alias="User"/>
</typeAliases>
```

也可以指定一个包，每一个在包 `domain.blog` 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。 比如 `domain.blog.Author` 的别名为 `author`,；若有注解，则别名为其注解值。见下面的例子：

```xml
<typeAliases>
    <package name="com.kuang.pojo"/>
</typeAliases>
```

在实体类比较少的时候，使用第一种方式。

如果实体类十分多，建议用第二种扫描包的方式。

第一种可以DIY别名，第二种不行，如果非要改，需要在实体上增加注解。

```java
@Alias("author")
public class Author {
    ...
}
```

### 映射器 mappers

MapperRegistry：注册绑定我们的Mapper文件；

方式一：推荐使用

```xml
<!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册-->
<mappers>
    <mapper resource="com/kuang/dao/UserMapper.xml"/>
</mappers>
```

方式二：使用class文件绑定注册

```xml
<!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册-->
<mappers>
    <mapper class="com.kuang.dao.UserMapper"/>
</mappers>
```

注意点：

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

方式三：使用包扫描进行注入

```xml
<mappers>
    <package name="com.kuang.dao"/>
</mappers>
```

### 作用域和生命周期

![image-20220221213715509](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221213715509.png)

声明周期和作用域是至关重要的，因为错误的使用会导致非常严重的并发问题。

**SqlSessionFactoryBuilder:**

- 一旦创建了SqlSessionFactory，就不再需要它了
- 局部变量

**SqlSessionFactory:**

- 说白了就可以想象为：数据库连接池
- SqlSessionFactory一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建一个实例。**
- 因此SqlSessionFactory的最佳作用域是应用作用域（ApplicationContext）。
- 最简单的就是使用**单例模式**或静态单例模式。

**SqlSession：**

- 连接到连接池的一个请求
- SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是请求或方法作用域。
- 用完之后需要赶紧关闭，否则资源被占用！

![image-20220221214645022](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221214645022.png)

## 解决属性名和字段名不一致的问题

数据库的字段：

![image-20220221220124129](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221220124129.png)

新建一个项目，拷贝之前的，测试实体类字段不一致的情况：

![image-20220221220144025](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221220144025.png)

测试出现问题：

![image-20220221220205133](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221220205133.png)

```xml
// select * from user where id = #{id}
// 类型处理器
// select id,name,pwd from user where id = #{id}
```

解决方法：

- 起别名

```xml
<select id="getUserById" resultType="com.kuang.pojo.User">
    select id , name , pwd as password from USER where id = #{id}
</select>
```

### resultMap

结果集映射

id name pwd

id name password

```xml
<!--结果集映射-->
<resultMap id="UserMap" type="User">
    <!--column数据库中的字段，property实体类中的属性-->
    <result column="id" property="id"></result>
    <result column="name" property="name"></result>
    <result column="pwd" property="password"></result>
</resultMap>

<select id="getUserList" resultMap="UserMap">
    select * from USER
</select>
```

- `resultMap` 元素是 MyBatis 中最重要最强大的元素。
- ResultMap 的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了。
- `ResultMap` 的优秀之处——你完全可以不用显式地配置它们。
- 如果这个世界总是这么简单就好了。

## 日志

### 日志工厂

如果一个数据库操作，出现了异常，我们需要排错，日志就是最好的助手！

曾经：sout、debug

现在：日志工厂

- SLF4J
- LOG4J 【掌握】
- LOG4J2
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING 【掌握】
- NO_LOGGING

在MyBatis中具体使用哪一个日志实现，在设置中设定

**STDOUT_LOGGING**

```xml
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

![image-20220221221238836](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220221221238836.png)

### Log4j

什么是Log4j？

- Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件；

- 我们也可以控制每一条日志的输出格式；

- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程；

- 最令人感兴趣的就是，这些可以通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码。

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

log4j.properties:

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file
#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/rzp.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sq1.PreparedStatement=DEBUG
```

配置settings为log4j实现

测试运行

**Log4j简单使用:**

1. 在要使用Log4j的类中，导入包 import org.apache.log4j.Logger;
2.  日志对象，参数为当前类的class对象
3. 日志级别

```java
Logger logger = Logger.getLogger(UserDaoTest.class);
```

1. info
2. debug
3. error

## 分页

**思考：为什么分页？**

- 减少数据的处理量

### 使用Limit分页

接口：

```java
//    分页
    List<User> getUserByLimit(Map<String,Integer> map);
```

Mapper.xml:

LIMIT 接受一个或两个数字参数,参数必须是一个整数常量。如果给定两个参数，第一个参数指定第一个返回记录行的偏移量（索引），第二个参数指定返回记录行的最大数目（显示的个数）。初始记录行的偏移量是 0(而不是 1)

```xml
    <select id="getUserByLimit" parameterType="map" resultType="user" resultMap="UserMap">
        select * from user limit #{startIndex},#{pageSize}
    </select>
```

测试：

```java
   @Test
   public void getUserByLimit(){
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      UserDao userdao = sqlSession.getMapper(UserDao.class);
      HashMap<String, Integer> map = new HashMap<>();
      map.put("startIndex",0);
      map.put("pageSize",2);
      List<User> userList = userdao.getUserByLimit(map);

      for (User user : userList) {
         System.out.println(user);
      }
      sqlSession.close();
   }
```

![image-20220222103056475](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222103056475.png)

![image-20220222103046089](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222103046089.png)

### RowBounds分页

不再使用SQL实现分页

1.接口

```java
//    分页2
    List<User> getUserByRowBounds();
```

2.mapper.xml

```xml
    <select id="getUserByRowBounds" resultMap="UserMap">
        select * from user
    </select>
```

3.测试

```java
   @Test
   public void getUserByRowsBounds(){
      SqlSession sqlSession = MybatisUtils.getSqlSession();
//      RowBounds实现
      RowBounds rowBounds = new RowBounds(1, 2);

//      通过java代码层面实现分页
      List<User> userList = sqlSession.selectList("com.kuang.dao.UserDao.getUserByRowBounds",null,rowBounds);
      for (User user : userList) {
         System.out.println(user);
      }
      sqlSession.close();
   }
```

![image-20220222103617160](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222103617160.png)

### 分页插件

![image-20220222104255732](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222104255732.png)

## 使用注解开发

### 面向接口开发

**三个面向区别**

- 面向对象是指我们考虑问题时，以对象为单位，考虑它的属性和方法；
- 面向过程是指我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现；
- 接口设计与非接口设计是针对复用技术而言的，与面向对象（过程）不是一个问题，更多的体现就是对系统整体的架构；

### 使用注解开发

1.注解在接口上实现

```java
  @Delete("delete from user where id = #{uid}")
    int deleteUser(@Param("uid") int id);
```

2.需要在核心配置文件中绑定接口

```xml
   <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>
```

3.测试

```java
   @Test
   public void deleteUser(){
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      UserDao userdao = sqlSession.getMapper(UserDao.class);
      userdao.deleteUser(3);
      sqlSession.commit();
      sqlSession.close();
   }
```

关于@Param()注解：

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，建议都加上
- 我们在SQL中引用的就是我们这里的@Param()中设定的属性名

本质：反射机制实现

底层：动态代理

![image-20220222105926522](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222105926522.png)

MyBatis详细执行流程：

![img](https://img-blog.csdnimg.cn/20200623165030775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

## Lombok

Lombok项目是一个Java库，它会自动插入编辑器和构建工具中，Lombok提供了一组有用的注释，用来消除Java类中的大量样板代码。仅五个字符(@Data)就可以替换数百行代码从而产生干净，简洁且易于维护的Java类。

使用步骤：

- 在IDEA中安装Lombok插件

- 在项目中导入lombok的jar包

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.10</version>
    <scope>provided</scope>
</dependency>
```

- 在程序上加注解

@Getter and @Setter
@FieldNameConstants
@ToString
@EqualsAndHashCode
@AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
@Data
@Builder
@SuperBuilder
@Singular
@Delegate
@Value
@Accessors
@Wither
@With
@SneakyThrows
@val

例如：

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String password;
}
```

![image-20220222112327542](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222112327542.png)

## 多对一处理

首先测试环境搭建：

1. 导入lombok
2. 新建实体类Teacher,Student
3. 建立Mapper接口
4. 建立Mapper.xml文件
5. 在核心配置文件中绑定注册我们的Mapper接口或者文件 【方式很多，随心选】
6. 测试查询是否能够成功

按照查询嵌套处理：

```java
package com.kuang.dao;

import com.kuang.pojo.Student;

import java.util.List;

public interface StudentMapper {
//    查询所有的学生信息以及对应的老师信息
    public List<Student> getStudent();
//    按照结果嵌套处理
    public List<Student> getStudent2();
}
```

```java
package com.kuang.dao;

import com.kuang.pojo.Teacher;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.annotations.Select;

public interface TeacherMapper {
    @Select("select * from teacher where id = #{tid}")
    Teacher getTeacher(@Param("tid") int id);
}
```

```java
package com.kuang.pojo;

import lombok.Data;

@Data
public class Student {
    private int id;
    private String name;
//    学生需要关联一个老师
    private Teacher teacher;
}
```

```java
package com.kuang.pojo;

import lombok.Data;

@Data
public class Teacher {
    private int id;
    private String name;

}
```

```xml
<!--
     思路：
        1. 查询所有的学生信息
        2. 根据查询出来的学生的tid寻找特定的老师 (子查询)
    -->
<select id="getStudent" resultMap="StudentTeacher">
    select * from student
</select>
<resultMap id="StudentTeacher" type="student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <!--复杂的属性，我们需要单独出来 对象：association 集合：collection-->
    <collection property="teacher" column="tid" javaType="teacher" select="getTeacher"/>
</resultMap>
<select id="getTeacher" resultType="teacher">
    select * from teacher where id = #{tid}
</select>
```

按照就结果嵌套处理：

```xml
    <!--按照结果进行查询-->
    <select id="getStudent2" resultMap="StudentTeacher2">
        select s.id sid , s.name sname, t.name tname
        from student s,teacher t
        where s.tid=t.id
    </select>
    <!--结果封装，将查询出来的列封装到对象属性中-->
    <resultMap id="StudentTeacher2" type="student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <association property="teacher" javaType="teacher">
            <result property="name" column="tname"></result>
        </association>
    </resultMap>
```

回顾Mysql多对一查询方式:

- 子查询 （按照查询嵌套）
- 联表查询 （按照结果嵌套）

## 一对多处理

一个老师多个学生；

对于老师而言，就是一对多的关系；

实体类

```java
@Data
public class Student {
    private int id;
    private String name;
    private int tid;
}
```

```java
@Data
public class Teacher {
    private int id;
    private String name;

    //一个老师拥有多个学生
    private List<Student> students;
}
```

按照结果嵌套处理：

```xml
<!--按结果嵌套查询-->
<select id="getTeacher" resultMap="StudentTeacher">
    SELECT s.id sid, s.name sname,t.name tname,t.id tid FROM student s, teacher t
    WHERE s.tid = t.id AND tid = #{tid}
</select>
<resultMap id="StudentTeacher" type="Teacher">
    <result property="id" column="tid"/>
    <result property="name" column="tname"/>
    <!--复杂的属性，我们需要单独处理 对象：association 集合：collection
    javaType=""指定属性的类型！
    集合中的泛型信息，我们使用ofType获取
    -->
    <collection property="students" ofType="Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <result property="tid" column="tid"/>
    </collection>
</resultMap>
```

小结：

1. 关联 - association 【多对一】
2. 集合 - collection 【一对多】
3. javaType & ofType
   1. JavaType用来指定实体类中的类型
   2. ofType用来指定映射到List或者集合中的pojo类型，泛型中的约束类型

注意点：

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多和多对一，属性名和字段的问题
- 如果问题不好排查错误，可以使用日志，建议使用Log4j

面试高频

- Mysql引擎
- InnoDB底层原理
- 索引
- 索引优化

## 动态SQL

**什么是动态SQL：动态SQL就是根据不同的条件生成不同的SQL语句**

**所谓的动态SQL，本质上还是SQL语句，只是我们可以在SQL层面，去执行一个逻辑代码**

动态 SQL 是 MyBatis 的强大特性之一。如果你使用过 JDBC 或其它类似的框架，你应该能理解根据不同条件拼接 SQL 语句有多痛苦，例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL，可以彻底摆脱这种痛苦。

### 流程：

搭建环境

CREATE TABLE `mybatis`.`blog`  (
  `id` int(10) NOT NULL AUTO_INCREMENT COMMENT '博客id',
  `title` varchar(30) NOT NULL COMMENT '博客标题',
  `author` varchar(30) NOT NULL COMMENT '博客作者',
  `create_time` datetime(0) NOT NULL COMMENT '创建时间',
  `views` int(30) NOT NULL COMMENT '浏览量',
  PRIMARY KEY (`id`)
)

创建一个基础工程：

1.导包

2.编写配置文件

3.编写实体类

```java
@Data
public class Blog {
    private int id;
    private String title;
    private String author;

    private Date createTime;// 属性名和字段名不一致
    private int views;
}
```

4.编写实体类对应的Mapper接口

```java
package com.kuang.dao;

import com.kuang.pojo.Blog;

import java.util.List;
import java.util.Map;

public interface BlogMapper {
//    插入数据
    int addBlog(Blog blog);
//    查询博客
    List<Blog> queryBlogIF(Map map);
//    更新博客
    int updateBlog(Map map);
}
```

5,编写Mapper/xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.BlogMapper">
    <insert id="addBlog" parameterType="Blog">
        insert into blog(id,title,author,create_time,views)
        values (#{id},#{title},#{author},#{create_time},#{views});
    </insert>
    <sql id="if-title-author">
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </sql>
    <select id="queryBlogIF" parameterType="map" resultType="blog">
        select * from blog
        <where>
        <include refid="if-title-author"></include>
        </where>

    </select>
    <select id="queryBlogChoose" parameterType="map" resultType="blog">
select * from blog
<where>
    <choose>
        <when test="title !=null">
            title = #{title}
        </when>
        <when test="author !=null">
            and author = #{author}
        </when>
        <otherwise>
            and views = #{views}
        </otherwise>
    </choose>
</where>
    </select>
    <update id="updateBlog" parameterType="map" >
        update blog
<set>
    <if test="title !=null">
        title = #{title},
    </if>
    <if test="author !=null">
        author = #{author},
    </if>
</set>
    where id = #{id}
    </update>
</mapper>
```

### if

- 概念：sql常见的场景就是判断使用
- 方式一：通过< if >直接使用，或者< include>跳转sql使用时候，需要保证where成立，所以需要在sql语句中加上类似`where 1= 1` 或者 `where state = 'active'`等语句
  - 这里使用了SQL片段复用

![image-20220222154634528](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222154634528.png)

```java
<!--if：通过include跳转到使用,缺点是必须写上判断条件成立 where 1=1-->
<select id="queryBlogByIf" parameterType="map" resultType="Blog">
    select * from mybatis.blog where 1=1
    <include  refid="if_title_author_like" />
</select>
<sql id="if_title_author_like">
    <if test="title !=null">
        and  title like #{title}
    </if>
    <if test="author !=null">
        and author like #{author}
    </if>
</sql>
```

- 方式二：通过< where >和< if >混合使用，就不用手动加上`where 1= 1`

```xml
<!--if:通过where直接使用/直接使用if判断，但是不推荐。原理：如果test存在，就自动加上where -->
<select id="queryBlogByWhere" parameterType="map" resultType="Blog">
    select * from mybatis.blog
    <where>
        <if test="id !=null">
            id like #{id}
        </if>
        <if test="views !=null">
            and views like #{views}
        </if>
    </where>
</select>
```

- 测试：模糊查询需要封装通配符

```java
@Test
public void queryBlogByIf() {
    SqlSession sqlSession = MyBatisUtil.getSqlSession();
    BlogMapper blogMapper = sqlSession.getMapper(BlogMapper.class);
    Map<String, String> map = new HashMap<>();
    //模糊查询，使用map的好处
    map.put("title", "%my%");
    List<Blog> blogs = blogMapper.queryBlogByIf(map);
    System.out.println(blogs);
    sqlSession.close();
}

@Test
public void queryBlogByWhere() {
    SqlSession sqlSession = MyBatisUtil.getSqlSession();
    BlogMapper blogMapper = sqlSession.getMapper(BlogMapper.class);
    Map<String, Object> map = new HashMap<>();
    //map.put("id","%4%");
    map.put("views", "%2%");
    List<Blog> blogs = blogMapper.queryBlogByWhere(map);
    System.out.println(blogs);
    sqlSession.close();
}
```

### choose

- 概念：有时候，我们不想使用所有的条件，而只是想从多个条件中选择一个使用。针对这种情况，MyBatis 提供了 choose 元素，它有点像 Java 中的 switch 语句。

- 需求：传入了 “title” 就按 “title” 查找，传入了 “author” 就按 “author” 查找的情形。若两者都没有传入，就返回标记为 featured 的 BLOG

- 细节：choose只能满足其中一个when\otherwisw；使用`WHERE state = ‘ACTIVE’`等保证where成立

```xml
<!--官网案例-->
<select id="findActiveBlogLike" resultType="Blog">
  SELECT * FROM BLOG WHERE state = ‘ACTIVE’
  <choose>
    <when test="title != null">
      AND title like #{title}
    </when>
    <when test="author != null and author.name != null">
      AND author_name like #{author.name}
    </when>
    <otherwise>
      AND featured = 1
    </otherwise>
  </choose>
</select>
```

### where

- 单独使用< if > 的缺点：如果没有查询条件或者第一个条件没有满足，就会出现错误的sql语句：

```xml
<select id="findActiveBlogLike"
     resultType="Blog">
  SELECT * FROM BLOG
  WHERE
  <if test="state != null">
    state = #{state}
  </if>
  <if test="title != null">
    AND title like #{title}
  </if>
  <if test="author != null and author.name != null">
    AND author_name like #{author.name}
  </if>
</select>
```

- 出现错误sql：

```java
# 没有条件成立
SELECT * FROM BLOG
WHERE
# 第一个条件没有成立
SELECT * FROM BLOG
WHERE
AND title like ‘someTitle’
```

- 使用where
  - 优势：where元素只会在子元素返回任何内容的情况下才插入WHERE子句。而且，若子句的开头为”And“或”OR“，where元素也会将它们去除。

```java
<select id="findActiveBlogLike" resultType="Blog">
  SELECT * FROM BLOG
  <where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
</select>
```

- 使用自定义trim元素来定制where元素的功能
  - 与< where>等价的< trim>
    - prefix="WHERE"满足条件，自动添加的字段：prefixOverrides自动忽略的字段，细节：AND |OR 两者后面都包含了一个空格，这是正确sql的书写要点

```java
<trim prefix="WHERE" prefixOverrides="AND |OR ">
  ...
</trim>
```

### set

- 概念：用于动态update语句的叫做 set。set 元素可以用于动态包含需要更新的列，忽略其它不更新的列
  - 等价的trim语句，***set\* 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号（这些逗号是在使用条件语句给列赋值时引入的）= 也就是说其实mybatis自动在update中set就给你加上了逗号，但是你自己手写加上了，< set> 也会给你忽略掉**

```java
<trim prefix="SET" suffixOverrides=",">
  ...
</trim>
```

```xml
<update id="updateAuthorIfNecessary">
  update Author
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
      <if test="bio != null">bio=#{bio}</if>
    </set>
  where id=#{id}
</update>
```

### foreach

- 概念：动态 SQL 的另一个常见使用场景是对集合进行遍历（尤其是在构建 IN 条件语句的时候）
- 原生：`SELECT * FROM blog WHERE 1=1 AND (id=1 OR id=2)；`
- 细节：if < where> 多个条件成立时，就会忽略掉原生中and书写

![image-20220222160843289](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222160843289.png)

```java
<select id="queryBlogByForeach" parameterType="map" resultType="Blog">
    select * from mybatis.blog
    <where>
   		<foreach collection="ids" item="id" open="(" separator="or" close=")">
    		id=#{id}
		</foreach>
    </where>
</select>
<!--官网案例：使用in时-->
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```

### SQL片段

- 回顾：前面的< where >结合< if>，我们将公共的SQL语句抽取出来，复用.
- 使用：< sql id= > 标签和< include refid= >引用
- 细节：
  - 最好基于单表使用sql片段，多表别的表不一定支持
  - 使用sql片段复用，不要使用< where >标签，因为它内置了会忽略掉某些字段

```xml
<sql id="if_title_author_like">
    <if test="title !=null">
        and  title like #{title}
    </if>
    <if test="author !=null">
        and author like #{author}
    </if>
</sql>

<select id="queryBlogByIf" parameterType="map" resultType="Blog">
    select * from mybatis.blog where 1=1
    <include refid="if_title_author_like" />
</select>
```

### bind

- bind 元素允许你在 OGNL 表达式以外创建一个变量，并将其绑定到当前的上下文。比如：

```xml
<select id="selectBlogsLike" resultType="Blog">
  <bind name="pattern" value="'%' + _parameter.getTitle() + '%'" />
  SELECT * FROM BLOG
  WHERE title LIKE #{pattern}
</select>
```

创建一个 bind 元素标签的变量后 ，就可以在下面直接使用，使用 bind 拼接字符串不仅可以避免因更换数据库而修改 SQL，也能预防 SQL 注入。

```xml
<!-- List<Employee> getEmpsTestInnerParameter(Employee employee); -->
      <select id="getEmpsTestInnerParameter" resultType="com.hand.mybatis.bean.Employee">
          <!-- bind:可以将OGNL表达式的值绑定到一个变量中，方便后来引用这个变量的值 -->
          <bind name="bindeName" value="'%'+eName+'%'"/> eName是employee中一个属性值
          SELECT * FROM emp 
          <if test="_parameter!=null">
            where ename like #{bindeName}
          </if>
      </select>
```

测试类：

```java
            Employee emp=new Employee();
            emp.setEname("张");   为eName属性赋值为“张”
            List<Employee> list=mapper.getEmpsTestInnerParameter(emp);
            for (Employee employee : list) {
                System.out.println(employee);
            }
```

## 缓存

- 我们再次查询相同数据时候，直接走缓存，就不用再存了，解决速度问题

- 什么样的数据需要用到缓存？
  - 经常查询并且不经常改变的数据，可以使用缓存

### 缓存原理图（重要）

二级缓存工作原理：

- 一次sqlsession是一级缓存，查询操作结束后，是默认保存在一级缓存中的
- 如果开启二级缓存，必须先关闭一级缓存，这时候的缓存数据会保存到二级缓存中
- 第二次查询时候，用户操作会先去二级缓存中查找

![image-20220222162701554](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222162701554.png)

### 一级缓存

- 默认情况下，只启用了本地的会话（一级）缓存，它仅仅对一个会话中的数据进行缓存。
  - 把一级缓存想象成一个会话中的map，便于理解

 ![image-20220222163005927](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222163005927.png)

- 缓存失效
  - 增删改会把所有的sql缓存失效，下次会重写从数据库查
  - 查询不同的mapper.xml
  - 手动清除缓存:`sqlSession.clearCache();`
  - 查询不同的东西

```java
 @Test
    public void test1(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.queryUserById(1);
//        sql只执行了一次，一级缓存，查询的两次都是相同记录
        /*
        * 缓存失效的原因：
        * 1.查询不同的东西
        * 2.增删改操作可能会改变原来的数据，所以必定会刷新缓存
        * 3.查询不同的Mapper.xml
        * 4.手动清除缓存
        */
        System.out.println(user);
//        mapper.updateUser(new User(2,"hello","bbbbb"));
        sqlSession.clearCache();//手动清理缓存
        System.out.println("===========================");
        User user2 = mapper.queryUserById(1);
        System.out.println(user2);
        System.out.println(user == user2);
        sqlSession.close();
    }
```

注意：openSession方法参数为true，不需要再写sqlSession.close()

![image-20220222164003163](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222164003163.png)

### 二级缓存

- mybatis-config.xml开启全局缓存

```xml
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
    <!--开启全局缓存 默认是开启的，显示写便于可读-->
    <setting name="cacheEnabled" value="true"/>
</settings>
```

- mappper.xml开启二级缓存：

```java
<!--开启二级缓存-->
<cache/>
```

映射语句文件中的所有 select 语句的结果将会被缓存。
映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
缓存不会定时进行刷新（也就是说，没有刷新间隔）。
缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。
       读写缓存需要pojo开启序列化操作

UserMapper:

```java
public interface UserMapper {
    //    根据id查询用户
    User queryUserById(@Param("id") int id);
}
```

UserMapper.xml:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.UserMapper">
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
    <select id="queryUserById" resultType="User" useCache="true">
        select * from user where id=#{id}
    </select>
</mapper>
```

开启二级缓存自定义参数：

```java
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

- eviction:清楚算法，默认LRU
  - LRU – 最近最少使用：移除最长时间不被使用的对象。
  - FIFO – 先进先出：按对象进入缓存的顺序来移除它们。
  - SOFT – 软引用：基于垃圾回收器状态和软引用规则移除对象。
  - WEAK – 弱引用：更积极地基于垃圾收集器状态和弱引用规则移除对象。

- flushInterval：刷新缓存间隔，默认无

- size：最多缓存数量，默认1024

- readOnly：只读缓存；写操作会不走缓存，直接从数据库查询，默认是读/写缓存

测试二级缓存：

```java
//    二级缓存，作用域是mapper
    @Test
    public void test2(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        SqlSession sqlSession2 = MybatisUtils.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        UserMapper mapper2 = sqlSession2.getMapper(UserMapper.class);
        User user = mapper.queryUserById(1);
        System.out.println(user);
 //关闭上次sqlSession，如果开启二级缓存，就会把这次的一级缓存保存到二级缓存中
        sqlSession.close();
//如果开启二级缓存，下次相同mapper的查询操作会先重二级缓存中查找
        User user2 = mapper2.queryUserById(1);
        System.out.println(user2);
//        如果给实体类序列化就输出false了，序列化之后取出来就不是一个对象
//        可读写的缓存会（通过序列化）返回缓存对象的拷贝，所以不是一个对象了
        System.out.println(user == user2);
        sqlSession2.close();
    }
```

![image-20220222171334613](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222171334613.png)

![image-20220222170328905](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222170328905.png)

![image-20220222170342311](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222170342311.png)

### 自定义缓存

- 概念：ehcache是一个分布式缓存，主要面向通用缓存
- 手写或者导入第三方的ehcache缓存依赖
- 所以可以自定义ehcache.xml配置文件

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.0</version>
</dependency>
```

- 在mapper.xml中配置

```xml
 <cache type="org.mybatis.caches.encache.EhcacheCache"/>
```

- 在resource中创建ehcache.xml文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
     <!--
         diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
         user.home – 用户主目录
         user.dir  – 用户当前工作目录
         java.io.tmpdir – 默认临时文件路径
       -->
    <diskStore path="./tmpdir/Tmp_EhCache"/>
          <!--
         defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
       -->
      <!--
        name:缓存名称。
        maxElementsInMemory:缓存最大数目
        maxElementsOnDisk：硬盘最大缓存个数。
        eternal:对象是否永久有效，一但设置了，timeout将不起作用。
        overflowToDisk:是否保存到磁盘，当系统当机时
        timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
        timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
        diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
        diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
        diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
        memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
        clearOnFlush：内存数量最大时是否清除。
        memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
        FIFO，first in first out，这个是大家最熟的，先进先出。
        LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
        LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
     -->
    <defaultCache
            eternal="false"
            maxElementsInMemory="10000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="259200"
            memoryStoreEvictionPolicy="LRU"/>

    <cache
            name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"/>
</ehcache>
```

### Redis

- 另一个开始



