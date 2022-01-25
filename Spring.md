# Spring

## Spring简单介绍

优点：

1. spring是一个开源的免费的框架（容器）。
2. Spring是一个轻量级的，非入侵式的框架。
3. 控制反转（IOC），面向切面编程（AOP）。
4. 支持事务的处理，对框架整合的支持。

弊端：发展太久之后，违背了原来的理念，配置十分繁琐，人称“配置地狱”！

## IOC理论推导

我们之前的业务中，用户的需求可能会影响我们原来的代码，我们根据用户的需求去修改代码，如果程序的代码量十分大，修改一次的成本的代价会变得十分昂贵。

![image-20220119112856013](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220119112856013.png)

我们使用了一个Set接口实现，已经发生了革命性的变化。

之前，程序是主动创建对象，控制权在程序员手上，使用了set注入后，程序不再具有主动性，而是被动的接受对象，主动权在用户手上。这种思想，从本质上解决了问题，我们不需要再去管理对象的创建了，系统的耦合性大大降低，可以更加的专注在业务的实现上，这是IOC的原型！

![image-20220119113722829](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220119113722829.png)

所谓的IoC一句话搞定：对象由Spring来创建，管理和装配。

## 静态代理

角色分析：

- 抽象角色：一般会使用接口或抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
- 客户：访问代理对象的人

![image-20220120125650050](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220120125650050.png)

代码步骤：

接口

```java
package com.kuang.demo01;
//租房
public interface Rent {
    public void rent();
}

```



真实角色

```java
package com.kuang.demo01;
//房东
public class Host implements Rent{
    public void rent(){
        System.out.println("房东要出租房子！");
    }
}

```



代理角色

```java
package com.kuang.demo01;
//组合优于继承原则
public class Proxy implements Rent{
    private Host host;

    public Proxy() {
    }

    public Proxy(Host host) {
        this.host = host;
    }
//    看房
    public void seeHouse(){
        System.out.println("中介带你看房");
    }
//    签合同
    public void hetong(){
        System.out.println("签租赁合同");
    }
//    收中介费
    public void fare(){
        System.out.println("收中介费");
    }
    @Override
    public void rent() {
        seeHouse();
        host.rent();
        hetong();
        fare();
    }
}

```



客户端访问代理角色

```java
package com.kuang.demo01;

public class Client {
    public static void main(String[] args) {
//        房东要租房子
        Host host = new Host();
//        代理，中介帮房东租房子，但是代理角色一般会有些附属操作
        Proxy proxy = new Proxy(host);
//        你不用面对房东，直接找中介租房即可
        proxy.rent();
    }
}

```



代理模式的好处：

- 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
- 公共业务就交给代理角色，实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理

缺点：

- 一个真实角色就会产生一个代理角色：代码量会翻倍

## 动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的
- 动态代理分为两大类：基于接口的动态代理和基于类的动态代理
  - 基于接口--jdk动态代理
  - 基于类：cglib
  - java字节码 javasist

需要了解两个类：Proxy：代理；InvocationHandler：调用处理程序

InvocationHandler

一个动态代理类代理的是一个接口，一般就是对应的一类业务。

一个动态代理类可以代理多个类，只要是实现了接口就行



![image-20220121114826579](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220121114826579.png)

![image-20220121114844895](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220121114844895.png)









