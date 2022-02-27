# javascript

## 操作BOM对象

javascript和浏览器关系？
BOM：浏览器对象模型

### window

window代表 浏览器窗口

window.alert(1)

window.innerHeight

window.innerwidth

window.outerHeight

window.outerwidth

![image-20220222202144291](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222202144291.png)

### navigator

Navigator封装了浏览器的信息

大多数时候，我们不会使用navigator对象，因为会被认为修改!

![image-20220222202338286](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222202338286.png)

### screen

screen代表屏幕尺寸

![image-20220222202423131](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222202423131.png)

### location（重要）

location代表当前页面的URL信息

![image-20220222202732598](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222202732598.png)

跳转到csdn网站：

location.assign('https://blog.csdn.net/')

### document（内容DOM）

document代表当前的页面，HTML DOM文档树

![image-20220222203251642](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222203251642.png)

![image-20220222204658671](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222204658671.png)

title发生变化了：

![image-20220222204723338](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222204723338.png)

获取具体的文档树节点：

![image-20220222205813023](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222205813023.png)

获取cookie：

![image-20220222205736988](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222205736988.png)

### history

![image-20220222210245764](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222210245764.png)

## 操作DOM对象

DOM：文档对象模型

浏览器网页就是一个Dom树形结构！

- 更新：更新Dom节点
- 遍历Dom节点：得到Dom节点
- 删除：删除一个Dom节点
- 添加：添加一个新的节点

要操作一个Dom节点，就必须要先获得这个Dom节点

### 获得DOM节点

![image-20220222211110082](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211110082.png)

![image-20220222211120190](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211120190.png)

这种都是原生代码，往后尽量用jQuery();

![image-20220222211350954](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211350954.png)

### 删除节点

![image-20220222211602894](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211602894.png)

注意：删除多个节点的时刻，children是在时刻变化的，删除节点的时候一定要注意。

### 插入节点

获得了某个DOM节点，假设这个DOM节点是空的，通过innerHTML就可以增加一个元素了，但是这个DOM节点已经存在元素了，就会产生覆盖。

![image-20220222211752466](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211752466.png)

效果：

![image-20220222211807408](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222211807408.png)

创建一个新标签，实现插入

![image-20220222212105300](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222212105300.png)

![image-20220222212332068](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220222212332068.png)



















