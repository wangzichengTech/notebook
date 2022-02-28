# Vue

Vue的核心库只关注视图层，方便与第三方库或既有项目整合。

HTML+CSS+JS ：视图：给用户看，刷新后台给的数据

网络通信：axios

页面跳转：vue-router

状态管理：vuex

Vue-UI：ICE，ElementUI

## 前端核心分析

### VUE 概述

Vue (读音/vju/, 类似于view)是一套用于构建用户界面的渐进式框架，发布于2014年2月。与其它大型框架不同的是，Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层，不仅易于上手，还便于与第三方库(如: vue-router: 跳转，vue-resource: 通信，vuex:管理)或既有项目整合

### 前端三要素

- HTML (结构) :超文本标记语言(Hyper Text Markup Language) ，决定网页的结构和内容
- CSS (表现) :层叠样式表(Cascading Style sheets) ，设定网页的表现样式
- JavaScript (行为) :是一种弱类型脚本语言，其源代码不需经过编译，而是由浏览器解释运行,用于控制网页的行为
  

### JavaScript框架

- jQuery: 大家熟知的JavaScript框架，优点是简化了DOM操作，缺点是DOM操作太频繁,影响前端性能;在前端眼里使用它仅仅是为了兼容IE6、7、8;

- Angular: Google收购的前端框架，由一群Java程序员开发，其特点是将后台的MVC模式搬到了前端并增加了模块化开发的理念，与微软合作，采用TypeScript语法开发;对后台程序员友好，对前端程序员不太友好;最大的缺点是版本迭代不合理(如: 1代-> 2代，除了名字，基本就是两个东西;截止发表博客时已推出了Angular6)

- React: Facebook出品，一款高性能的JS前端框架;特点是提出了新概念[虚拟DOM]用于减少真实DOM操作，在内存中模拟DOM操作，有效的提升了前端渲染效率;缺点是使用复杂，因为需要额外学习一门[JSX] 语言;

- Vue:一款渐进式JavaScript框架，所谓渐进式就是逐步实现新特性的意思，如实现模块化开发、路由、状态管理等新特性。其特点是综合了Angular (模块化)和React (虚拟DOM)的优点;

- Axios :前端通信框架;因为Vue 的边界很明确，就是为了处理DOM,所以并不具备通信能力，此时就需要额外使用一个通信框架与服务器交互;当然也可以直接选择使用jQuery提供的AJAX通信功能;
  **前端三大框架：Angular、React、Vue**

## 第一个Vue程序

### 什么是MVVM

MVVM (Model-View-ViewModel) 是一种软件架构设计模式，由微软WPF (用于替代WinForm，以前就是用这个技术开发桌面应用程序的)和Silverlight (类似于Java Applet,简单点说就是在浏览器上运行的WPF)的架构师Ken Cooper和Ted Peters 开发，是一种简化用户界面的事件驱动编程方式。由John Gossman (同样也是WPF和Silverlight的架构师)于2005年在他的博客上发表。
MVVM 源自于经典的MVC (ModeI-View-Controller) 模式。MVVM的核心是ViewModel层，负责转换Model中的[数据](https://so.csdn.net/so/search?q=数据&spm=1001.2101.3001.7020)对象来让数据变得更容易管理和使用，其作用如下:

- 该层向上与视图层进行双向数据绑定
- 向下与Model层通过接口请求进行数据交互

![image-20220228154135649](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220228154135649.png)

### 为什么要使用MVVM

MVVM模式和MVC模式一样，主要目的是分离视图(View)和模型(Model),有几大好处：

- 低耦合：视图可以独立于Model变化和修改，一个viewModel可以绑定到不同的View上，当View变化时Model可以不变，当Model变化时View也可以不变。
- 可复用：你可以把一些视图逻辑放在一个ViewModel里面，让很多View重用这段视图逻辑。
- 独立开发：开发人员可以专注于业务逻辑和数据的开发，设计人员可以专注于页面设计。
- 可测试：界面素来时比较难以测试的，而现在测试可以针对ViewModel来写。

### Vue是MVVM模式的实现者

![image-20220228154830134](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220228154830134.png)

- Model：模型层，在这里表示JavaScript对象。
- View：视图层，在这里表示DOM（HTML操作的元素）。
- ViewModel:连接视图和数据的中间件，Vue.js就是MVVM中的ViewModel层的实现者在MVVM架构中，是不允许数据和视图直接通信的，只能通过ViewModel来通信，而ViewModel就是定义一个Observer观察者。
- ViewModel能够观察到数据的变化并对视图对应的内容进行更新。
- ViewModel能够监听到视图的变化，并能够通知数据发生改变

至此，我们就明白了，Vue.js 就是一个MVVM的实现者，他的核心就是实现了**DOM监听**与**数据绑定**

Vue在线cdn:

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
```

## Vue基本语法

### v-bind

现在数据和DOM已经被建立了关联，所有的东西都是响应式的。我们在控制台操作对象的属性，界面可以实时更新

我们可以使用v-bind来绑定元素属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<p>狂神说Java</p>

<!--view层 模板-->
<div id="app">
    <span v-bind:title="message">鼠标悬停几秒钟查看此处动态绑定的提示信息！</span>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "hello,vue"
        }
    })
</script>
</html>
```

### v-if v-else

```html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Title</title>
</head>
<body>
<p>狂神说Java</p>

<!--view层 模板-->
<div id="app">
   <h1 v-if="type==='A'">A</h1>
   <h1 v-else-if="type==='B'">B</h1>
   <h1 v-else>C</h1>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
   var vm = new Vue({
       el: "#app",
       data: {
           type: "A"
       }
   })
</script>
</html>
```

### v-for

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<p>狂神说Java</p>

<!--view层 模板-->
<div id="app">
    <li v-for="item in items">
        姓名：{{item.name}}，年龄：{{item.age}}
    </li>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            items: [
                {name: "zhangsan", age: 12},
                {name: "lisi", age: 10},
                {name: "wangwu", age: 16}
            ]
        }
    })
</script>
</html>
```

### v-on 事件绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<p>狂神说Java</p>

<!--view层 模板-->
<div id="app">
    <button v-on:click="sayHi">Click Me</button>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "你点我干嘛？"
        },
        methods: {
            //方法必须绑定在Vue的Methods对象中，v-on:事件
            sayHi: (function (event) {
                alert(this.message)
            })
        }
    })
</script>
</html>
```

## Vue双向绑定v-model

### 什么是双向绑定

 Vue.js是一个MVVM框架，即数据双向绑定,即当数据发生变化的时候,视图也就发生变化，当视图发生变化的时候，数据也会跟着同步变化。这也算是Vue.js的精髓之处了。

 值得注意的是，我们所说的数据双向绑定，一定是对于UI控件来说的，非UI控件不会涉及到数据双向绑定。单向数据绑定是使用状态管理工具的前提。如果我们使用vuex，那么数据流也是单项的，这时就会和双向数据绑定有冲突。

### 为什么要实现数据的双向绑定

在Vue.js 中，如果使用vuex ，实际上数据还是单向的，之所以说是数据双向绑定，这是用的UI控件来说，对于我们处理表单，Vue.js的双向数据绑定用起来就特别舒服了。即两者并不互斥，在全局性数据流使用单项,方便跟踪;局部性数据流使用双向，简单易操作。

### 在表单中使用双向数据绑定

你可以用`v-model`指令在表单 `<input>`、`<textarea>` 及`<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但`v-model`本质上不过是语法糖。它负责监听户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

**注意：v-model会忽略所有元素的value、checked、selected特性的初始值而总是将Vue实例的数据作为数据来源，你应该通过JavaScript在组件的data选项中声明。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!--view层 模板-->
<div id="app">
    下拉框：
    <select v-model="selected">
        <!--        disabled表示不可选择-->
        <option value="" disabled>-请选择-</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>
    <p>value:{{selected}}</p>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            selected: ""
        }
    })
</script>
</html>
```

## Vue组件

 组件是可复用的`Vue`实例，说白了就是一组可以重复使用的模板，跟JSTL的自定义标签、Thymeleaf的`th:fragment` 等框架有着异曲同工之妙。通常一个应用会以一棵嵌套的组件树的形式来组织：

![image-20220228170930511](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220228170930511.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!--view层 模板-->
<div id="app">
    <qinjiang v-for="item in items" v-bind:qin="item"></qinjiang>
</div>
</body>

<!--导入js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    Vue.component("qinjiang",{
        props: ['qin'],
        template: '<li>{{qin}}</li>'
    })

    var vm = new Vue({
        el: "#app",
        data: {
            items: ['Java','Python','Php']
        }
    })
</script>
</html>
```

## Axios通信

 Axios是一个开源的可以用在浏览器端和`NodeJS` 的异步通信框架，她的主要作用就是实现AJAX异步通信，其功能特点如下:

- 从浏览器中创建`XMLHttpRequests`
- 从node.js创建http请求
- 支持Promise API [JS中链式编程]
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF (跨站请求伪造)

### 为什么要使用Axios

由于Vue.js是一个视图层框架且作者(尤雨溪) 严格准守SoC (关注度分离原则)，所以Vue.js并不包含Ajax的通信功能，为了解决通信问题，作者单独开发了一个名为vue-resource的插件，不过在进入2.0 版本以后停止了对该插件的维护并推荐了Axios 框架。少用jQuery，因为它操作Dom太频繁 !
模拟Json数据：

```json
{
  "name": "weg",
  "age": "18",
  "sex": "男",
  "url":"https://www.baidu.com",
  "address": {
    "street": "文苑路",
    "city": "南京",
    "country": "中国"
  },
  "links": [
    {
      "name": "bilibili",
      "url": "https://www.bilibili.com"
    },
    {
      "name": "baidu",
      "url": "https://www.baidu.com"
    },
    {
      "name": "cqh video",
      "url": "https://www.4399.com"
    }
  ]
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    v-clock解决闪烁问题-->
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>
<div id="vue" v-clock>
    <div>{{info.name}}</div>
    <div>{{info.address.city}}</div>
    <a v-bind:href="info.url">点我</a>
</div>
<!--1.导入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<!--导入axios-->
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.min.js"></script>
<script type="text/javascript">
    var vm = new Vue({
        el:'#vue',
        data:{
            //请求的返回参数合适，必须和json字符串一样
            info:{

            }
        },
        //钩子函数就是页面渲染完成后需要执行的函数，这个时候传数据最合适
        mounted(){//钩子函数 链式编程 ES6新特性
            axios.get('../data.json').then(response=>(this.info=response.data));
        }
    });
</script>
</body>
</html>
```

### Vue计算属性

计算属性的重点突出在`属性`两个字上(属性是名词)，首先它是个`属性`其次这个属性有`计算`的能力(计算是动词)，这里的计算就是个函数;简单点说，它就是一个能够将计算结果缓存起来的属性(将行为转化成了静态的属性)，仅此而已;可以想象为**缓存**！

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue</title>
</head>
<body>
<div id="app">
<!--    methods:定义方法，调用方法使用currentTime()，需要带括号-->
    <p>currentTime1 {{currentTime1()}}</p>
<!--    computed:定义计算属性，调用属性使用currentTime2,不需要带括号-->
    <p>currentTime2 {{currentTime2}}</p>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            message:"hello,kuangshen"
        },
        methods: {
            currentTime1:function (){
                return Date.now();//返回一个时间戳
            }
        },
        //计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销
        computed:{//计算属性
            currentTime2:function (){
                this.message;//如果方法中的值发生变化，则缓存就会刷新
                return Date.now();
            }
        }
    });
</script>
</body>
</html>
```

**结论:**
 调用方法时，每次都需要进行计算，既然有计算过程则必定产生系统开销，那如果这个结果是不经常变化的呢?此时就可以考虑将这个结果缓存起来，采用计算属性可以很方便的做到这一点,**计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销;**

## 内容分发slot

在Vue.js中我们使用元素作为承载分发内容的出口，作者称其为插槽，可以应用在组合组件的场景中；

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue</title>
</head>
<body>
<!--view层 模板-->
<div id="app">
    <todo>
        <todo-title slot="todo-title" :title="title"></todo-title>
        <todo-items slot="todo-items" v-for="item in todoItems" :item="item"></todo-items>
    </todo>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script>
    //slot:插槽
    Vue.component("todo",{
        template:
            '<div>\
            <slot name="todo-title"></slot>\
            <ul>\
            <slot name="todo-items"></slot>\
            </ul>\
            </div>'
    });
    Vue.component("todo-title",{
        props:['title'],
        template: '<div>{{title}}</div>'
    })
    Vue.component("todo-items",{
        props:['item'],
        template: '<li>{{item}}</li>'
    })
    var vm = new Vue({
        el:"#app",
        data:{
            title:"需要学习的东西",
            todoItems:['Java','前端','Linux']
        }
    });
</script>
</body>
</html>
```























