# 4.前端框架及其相关、JS高阶

> # jQuery

#### JQuery的源码看过吗？能不能简单概况一下它的实现原理？

```
原理就是对常用操作的封装，顺便解决了兼容性问题
```

#### jQuery 库中的 $\(\) 是什么？

```
$() 函数是 jQuery() 函数的别称。$() 函数用于将任何对象包裹成 jQuery 对象，接着你就被允许调用定义在 jQuery 对象上的多个不同方法。你可以将一个选择器字符串传入 $() 函数，它会返回一个包含所有匹配的 DOM 元素数组的 jQuery 对象。
```

#### jQuery 遍历

```
parent() 方法返回被选元素的直接父元素。

parents() 方法返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)     .parents("标签")的那个父

parentsUntil() 方法返回介于两个给定元素之间的所有祖先元素。
```

#### jQuery.fn的init方法返回的this指的是什么对象？为什么要返回this？

```
答案一：https://segmentfault.com/q/1010000003700711
答案二：https://stackoverflow.com/questions/4754560/help-understanding-jquerys-jquery-fn-init-why-is-init-in-fn
```

#### jquery中如何将数组转化为json字符串，然后再转化回来？

```
jQuery 中没有提供这个功能，所以需要先编写两个 jQuery 的扩展：
$.fn.stringifyArray = function(array) {
    return JSON.stringify(array)
}
$.fn.parseArray = function(array) {
    return JSON.parse(array)
}
//
然后调用:
$("").stringifyArray(array)
```

#### jQuery 的属性拷贝（extend）的实现原理是什么？如何实现深拷贝？

```
答案一：https://www.cnblogs.com/yuqingfamily/p/5813650.html
```

#### jquery.extend 与 jquery.fn.extend的区别？

```
答案一:http://www.jb51.net/article/69369.htm
```

#### 谈一下Jquery事件委托方法中的bind\(\),live\(\),delegate\(\),on\(\)的区别？

```
bind() 方法为被选元素添加一个或多个事件处理程序，并规定事件发生时运行的函数。
on() 方法事件处理程序到当前选定的jQuery对象中的元素。
delegate() 方法为指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。
live() 方法为被选元素附加一个或多个事件处理程序，并规定当这些事件发生时运行的函数

(1)、bind 【jQuery 1.3之前】

定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

语法：bind(type,[data],function(eventObject))；

特点：

　　(1)、适用于页面元素静态绑定。只能给调用它的时候已经存在的元素绑定事件，不能给未来新增的元素绑定事件。

　　(2)、当页面加载完的时候，你才可以进行bind()，所以可能产生效率问题。

实例如下：$( "#members li a" ).bind( "click", function( e ) {} );

(2)、live 【jQuery 1.3之后】

定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

语法：live(type, [data], fn);

特点：

　　(1)、live方法并没有将监听器绑定到自己(this)身上，而是绑定到了this.context上了。

　　(2)、live正是利用了事件委托机制来完成事件的监听处理，把节点的处理委托给了document，新添加的元素不必再绑定一次监听器。

　　(3)、使用live（）方法但却只能放在直接选择的元素后面，不能在层级比较深，连缀的DOM遍历方法后面使用，即$(“ul”").live...可以，但$("body").find("ul").live...不行； 

实例如下：$( document ).on( "click", "#members li a", function( e ) {} );

(3)、delegate 【jQuery 1.4.2中引入】

定义和用法：将监听事件绑定在就近的父级元素上

语法：delegate(selector,type,[data],fn)

特点：

　　(1)、选择就近的父级元素，因为事件可以更快的冒泡上去，能够在第一时间进行处理。

　　(2)、更精确的小范围使用事件代理，性能优于.live()。可以用在动态添加的元素上。

实例如下：

$("#info_table").delegate("td","click",function(){/*显示更多信息*/});

$("table").find("#info").delegate("td","click",function(){/*显示更多信息*/});

(4)、on 【1.7版本整合了之前的三种方式的新事件绑定机制】

定义和用法：将监听事件绑定到指定元素上。

语法：on(type,[selector],[data],fn)

实例如下：$("#info_table").on("click","td",function(){/*显示更多信息*/});参数的位置写法与delegate不一样。

说明：on方法是当前JQuery推荐使用的事件绑定方法，附加只运行一次就删除函数的方法是one()。

总结：.bind(), .live(), .delegate(),.on()分别对应的相反事件为：.unbind(),.die(), .undelegate(),.off()


http://www.jb51.net/article/120018.htm
```

#### JQuery一个对象可以同时绑定多个事件,这是如何实现的?

```
(未解决)
```

#### 是否了解针对 jQuery 性能的优化方法？

```
基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。
//
频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好。
 比如：var str=$("a").attr("href");
 //
for (var i = size; i < arr.length; i++) {}
for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：
for (var i = size, length = arr.length; i < length; i++) {}
```

#### jQuery 与 jQuery UI 有何区别？

    `jQuery`是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。
    `jQuery UI`则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等

#### jQuery UI 如何自定义组件？

```
答案一：https://yq.aliyun.com/ziliao/138127
```

#### 如何找到所有 HTML select 标签的选中项？

```
$('[name=selectname] :selected')
```

#### $\(this\) 和 this 关键字在 jQuery 中有何不同？

```
$(this) 返回一个 jQuery 对象，你可以对它调用多个 jQuery 方法，比如用 text() 获取文本，用val() 获取值等等。

而 this 代表当前元素，它是 JavaScript 关键词中的一个，表示上下文中的当前 DOM 元素。你不能对它调用 jQuery 方法，直到它被 $() 函数包裹，例如 $(this)
```

#### jquery怎么移除标签onclick属性？

```js
获得a标签的onclick属性: $("a").attr("onclick")

删除onclick属性：$("a").removeAttr("onclick");

设置onclick属性：$("a").attr("onclick","test();");
```

#### jquery中addClass,removeClass,toggleClass的使用

```js
$(selector).addClass(class)：为每个匹配的元素添加指定的类名

$(selector).removeClass(class)：从所有匹配的元素中删除全部或者指定的类，删除class中某个值；

$(selector).toggleClass(class)：如果存在（不存在）就删除（添加）一个类

$(selector).removeAttr(class);删除class这个属性；
```

#### JQuery有几种选择器?

```js
(2)、层次选择器：parent > child，prev + next ，prev ~ siblings

(3)、基本过滤器选择器：:first，:last ，:not ，:even ，:odd ，:eq ，:gt ，:lt

(4)、内容过滤器选择器： :contains ，:empty ，:has ，:parent

(5)、可见性过滤器选择器：:hidden ，:visible

(6)、属性过滤器选择器：[attribute] ，[attribute=value] ，[attribute!=value] ，[attribute^=value] ，[attribute$=value] ，[attribute*=value]

(7)、子元素过滤器选择器：:nth-child ，:first-child ，:last-child ，:only-child

(8)、表单选择器： :input ，:text ，:password ，:radio ，:checkbox ，:submit 等；

(9)、表单过滤器选择器：:enabled ，:disabled ，:checked ，:selected
```

#### jQuery中的Delegate\(\)函数有什么作用？

```
delegate()会在以下两个情况下使用到：

1、如果你有一个父元素，需要给其下的子元素添加事件，这时你可以使用delegate()了，代码如下：

$("ul").delegate("li", "click", function(){ $(this).hide(); });

2、当元素在当前页面中不可用时，可以使用delegate()
```

#### $\(document\).ready\(\)方法和window.onload有什么区别？

```
(1)、window.onload方法是在网页中所有的元素(包括元素的所有关联文件)完全加载到浏览器后才执行的。

(2)、$(document).ready() 方法可以在DOM载入就绪时就对其进行操纵，并调用执行绑定的函数。
```

#### 如何用jQuery禁用浏览器的前进后退按钮？

```js
实现代码如下：

<script type="text/javascript" language="javascript">
　　$(document).ready(function() {
　　　　window.history.forward(1);
  　　　　//OR window.history.forward(-1);
　　});
</script>
```

#### jquery中$.get\(\)提交和$.post\(\)提交有区别吗？

```
相同点：都是异步请求的方式来获取服务端的数据；

异同点：

1、请求方式不同：$.get() 方法使用GET方法来进行异步请求的。$.post() 方法使用POST方法来进行异步请求的。
2、参数传递方式不同：get请求会将参数跟在URL后进行传递，而POST请求则是作为HTTP消息的实体内容发送给Web服务器的，这种传递是对用户不可见的。
3、数据传输大小不同：get方式传输的数据大小不能超过2KB 而POST要大的多
4、安全问题： GET 方式请求的数据会被浏览器缓存起来，因此有安全问题。
```

#### 写出一个简单的$.ajax\(\)的请求方式？

```js
$.ajax({
    url:'http://www.baidu.com',
    type:'POST',
    data:data,
    cache:true,
    headers:{},
    beforeSend：function(){},
    success:function(){},
    error:function(){},
    complete:function(){}
});
```

#### css3动画和jquery动画的差别

```
css3中的过渡和animation动画都是基于css实现机制的，属于css范畴之内，并没有涉及到任何语言操作。效率略高与jQuery中的animate()函数，但兼容性很差。

jQuery中的animate()函数可以简单的理解为css样式的“逐帧动画”，是css样式不同状态的快速切换的结果。效率略低于css3动画执行效率，但是兼容性好。‍
```

> # ECMAScript6

#### Object.is\(\) 与原来的比较操作符“ ===”、“ ==”的区别？

```
两等号判等，会在比较时进行类型转换；
三等号判等(判断严格)，比较时不进行隐式类型转换,（类型不同则会返回false）； 

Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，
但 Object.is(NaN, NaN) 会返回 true.

Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。
```

#### 谈一谈你对ECMAScript6的了解？

```
详解：http://wiki.jikexueyuan.com/project/es-six-deeply/an-introduction.html
```

#### ECMAScript6 怎么写class么，为什么会出现class这种东西?

```
详解：https://www.zhihu.com/question/29789315/answer/45624154
```

#### promise方法的理解和使用

```
https://www.jianshu.com/p/063f7e490e9a
```

#### JavaScript中var、let、const区别？

```
使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象；
使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；
使用const声明的是常量，在后面出现的代码中不能再修改该常量的值。

http://www.infoq.com/cn/articles/es6-in-depth-let-and-const
```

#### 平时用了es6的哪些特性，体验如何 和es5有什么不同

```
let const关键字 箭头函数 字符串模板 class类 模块化 promise

es5 require react.createclass
```

> # React

#### 简单介绍

```
React是Facebook开发的一款JS库
Facebook认为MVC无法满足他们的扩展需求，由于他们非常巨大的代码库和庞大的组织，使得MVC很快变得非常复复杂，每当需要添加一项新的功能或特性时，系统的复杂度就成级数增长，致使代码变得脆弱和不可预测，结果导致他们的MVC正在土崩瓦解。认为MVC不适合大规模应用，当系统中有很多的模型和相应的视图时，其复杂度就会迅速扩大，非常难以理解和调试，特别是模型和视图间可能存在的双向数据流动。

解决这个问题需要“以某种方式组织代码，使其更加可预测”，这通过他们(Facebook)提出的Flux和React已经完成。

Flux是一个系统架构，用于推进应用中的数据单向流动。React是一个JavaScript框架，用于构建“可预期的”和“声明式的”Web用户界面，它已经使Facebook更快地开发Web应用

构建那些数据会随时间改变的大型应用，做这些，React有两个主要的特点：

简单：

简单的表述任意时间点你的应用应该是什么样子的，React将会自动的管理UI界面更新当数据发生变化的时候。

声明式：

在数据发生变化的时候，React从概念上讲与点击了F5一样，实际上它仅仅是更新了变化的一部分而已。
React是关于构造可重用组件的，实际上，使用React你做的仅仅是构建组建。通过封装，使得组件代码复用、测试以及关注点分离更加容易。

比较分析：和其他一些js框架相比，React怎样，比如Backbone、Angular等。

React不是一个MVC框架，它是构建易于可重复调用的web组件，侧重于UI, 也就是view层
其次React是单向的从数据到视图的渲染，非双向数据绑定
不直接操作DOM对象，而是通过虚拟DOM通过diff算法以最小的步骤作用到真实的DOM上。
不便于直接操作DOM，大多数时间只是对 virtual DOM 进行编程

详解：https://www.jianshu.com/p/ae482813b791
```

#### React 生命周期

```
组件会随着组件的props和state改变而发生变化，它的DOM也会有相应的变化。

一个组件就是一个状态机：对于特定的输入，它总会返回一致的输出。
React组件提供了生命周期的钩子函数去响应组件不同时刻的状态，组件的生命周期如下：实例化、存在期、销毁期

详解：https://segmentfault.com/a/1190000006792687
```

#### React实现组件有哪些方式？

```
React创建组件的三种方式及其区别

React推出后，出于不同的原因先后出现三种定义react组件的方式，殊途同归；具体的三种方式：

函数式定义的无状态组件
es5原生方式React.createClass定义的组件
es6形式的extends React.Component定义的组件

详解：https://www.cnblogs.com/wonyun/p/5930333.html
```

#### React 生命周期AJAX 的问题

```js
在项目中是把数据请求单独定义一个函数，在进入页面是didMount中加载这个函数，如果有数据更新（也就是你说的刷新列表触发事件）时，再执行这个行数即可

componentDidMount(){
    this.loadlists()
}
loadlists(){
    ajax请求……
}
refreshdata(){
    this.loadlists()
}
```

#### React系列——shouldComponentUpdate避免组件无意义渲染

```
详解：https://segmentfault.com/a/1190000008656863
```

#### 调用 setState 之后发生了什么?

```
（未完成）在代码中调用setState函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程(Reconciliation)。经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个UI界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。
```

#### React之key详解

```
https://blog.csdn.net/hzxonlineok/article/details/78735557
```

#### react-router的实现原理

```
https://segmentfault.com/a/1190000004527878
```

#### Weex和React Native框架对比与选择

```
https://www.cnblogs.com/valenhua/p/7346682.html
```

#### ControlledComponent与UncontrolledComponent之间的区别是什么

```
React 的核心组成之一就是能够维持内部状态的自治组件，不过当我们引入原生的HTML表单元素时（input,select,textarea 等），我们是否应该将所有的数据托管到 React 组件中还是将其仍然保留在 DOM 元素中呢？这个问题的答案就是受控组件与非受控组件的定义分割。受控组件（Controlled Component）代指那些交由 React 控制并且所有的表单数据统一存放的组件。譬如下面这段代码中username变量值并没有存放到DOM元素中，而是存放在组件状态数据中。任何时候我们需要改变username变量值时，我们应当调用setState函数进行修改。
```

#### 高阶组件 Higher-order Components（HOC）

```
https://www.jianshu.com/p/d36f5d9211eb
```

#### React数据流和组件间的通信总结

```
https://www.cnblogs.com/tim100/p/6050514.html
```

#### 深入React技术栈：React数据流和生命周期

```js
数据流

在React中，数据是单向流动的，是从上向下的方向，即从父组件到子组件的方向。
state和props是其中重要的概念，如果顶层组件初始化props，那么React会向下遍历整颗组件树，重新渲染相关的子组件。其中state表示的是每个组件中内部的的状态，这些状态只在组件内部改变。
把组件看成是一个函数，那么他接受props作为参数，内部由state作为函数的内部参数，返回一个虚拟dom的实现。

state
上面说过，state是组件内部的状态，当组件内部使用内置的setState方法，该组件会重新进行渲染。
注意一下，setState方法是一个异步的方法，在一个生命周期中的所有setState方法会合并操作。

props
props是React中用来让组件之间相互联系的一种机制，props的传递过程对React是非常直观的，React的单向数据流主要的流动管道就是props，props本身是不可变的，当我们试图改变props的原始值，React会报类型错误的警告。组件的props一定是来源于默认指定的属性或者是从父组件传入的。
React为props提供了默认配置，通过defaultProps静态变量的方式来定义，当组件被调用的时候，默认值保证渲染后始终有值。
在React中有一个内置的props--children，代表的是子组件的集合，根据子组件的数量，this.props.children的数据类型而且不一致，当没有子组件的时候为undefined，当有一个的时候为object，当有多个的时候为array。

propTypes
propTypes是用来规范props的类型和必须的状态，如果组件定义了propTypes，那么在开发环境下会对props进行检查，在生产环境下是不会进行检查的。

生命周期

了解React的生命周期对React的使用会有更好的理解，可以让自己的代码写的更加合理。
广义的可以将React分为挂载，渲染，卸载这几个阶段，当渲染后的组件需要更新，我们会重新去渲染组件，直至卸载。

import React , {Component, PropTypes} from 'react'

class App extends Component {
    static propTypes = {

    }

    static defaultProps = {

    }

    constructor(props) {
        super(props)
        this.state = {

        }
    }

    componentWillMount() {

    }
    componentDidMount() {

    }
    render() {

    }

}
首先我们看下上面的代码结构，propTypes和defaultProps分别代表的是props的类型检查和默认类型值。这两个属性声明为组件的静态属性，所以可以通过类对其进行访问。如： App. defaultProps。

然后可以看到componentWillMount这个方法，会在render方法之前执行，componentDidMount方法会在render方法之后执行，分别代表了渲染前和渲染后的阶段。

以上的过程都只会在组件初始化的时候执行一次，如果是在componentWillMount中执行了setState方法是无意义的，因为组件只渲染一次。在componentDidMount中执行setState方法组件会再次更新，这样初始化的时候就渲染了两次。在必要的情况下可以在componentDidMount执行setState方法。

关于数据的更新
在React的数据是单向的，数据的更新要么来自父组件的props或者是自身state的改变。
import React, {Component, PropTypes} from 'react'

class App extends Component {
    componentWillReceiveProps(nextProps){
        // this.setState
    }

    shouldComponentUpdate(nextProps, nextState){
        //return true
    }

    componentWillUpdate(nextProps, nextState){

    }

    componentDidUpdate(preProps, preState){

    }

    render() {

    }
}

如上关于组件更新的生命周期需要使用到的方法。
如果是组件自身的state发生改变，那么依次会执行shouldComponentUpdate，componentWillUpdate，render, componentDidUpdate。

shouldComponentUpdate方法，该方法接受需要更新的props和state，方法返回FALSE的时候表示不进行更新，接下来的生命周期方法不会再执行下去，默认返回的是TRUE表示确定进行更新。

注意我们不可以在componentWillUpdate中执行setState方法。

在shouldComponentUpdate方法之前，还有一个componentWillReceiveProps方法，该方法在数据是有父组件的props更新的时候会触发，在此方法中执行setState方法是不会进行二次渲染的。
```

#### 在React中使用Redux

```
详细：https://www.jianshu.com/p/06f5285e2620
```

#### React与Vue，，它们有哪些区别？​

```
各自的组件更新进行对比：https://www.cnblogs.com/heyuqing/p/7526738.html


答案一：http://caibaojian.com/vue-vs-react.html

答案二：
        都用了virtual dom的方式, 性能都很好

        ui上都是组件化的写法，开发效率很高

        vue是双向数据绑定，react是单项数据绑定，当工程规模比较大时双向数据绑定会很难维护

        vue适合不会持续的  小型的web应用，使用vue.js能带来短期内较高的开发效率. 否则采用react
```

> # Vue.js

#### 简要介绍

```
渐进式 JavaScript 框架

易用：已经会了 HTML、CSS、JavaScript？即刻阅读指南开始构建应用！

灵活：不断繁荣的生态系统，可以在一个库和一套完整框架之间自如伸缩。


高效：20kB min+gzip 运行大小
     超快虚拟 DOM 
     最省心的优化
```

#### Vue双向数据绑定的实现

```
vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者（文本节点则是作为订阅者），在收到消息后执行相应的更新操作。

compile主要做的事情是解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

AngularJS 采用“脏值检测”的方式，数据发生变更后，对于所有的数据和视图的绑定关系进行一次检测，识别是否有数据发生了改变。
```

> # webpack&grunt/gulp

#### 工具区分

```
1.webpack
官网：http://webpack.github.io/docs/

中文文档：http://www.css88.com/doc/webpack2/

Webpack 是一个模块打包工具。它将一堆文件中的每个文件都作为一个模块，找出他们的依赖关系，将它们打包为可部署的静态资源。



2.Grunt/gulp
a)构建工具是什么，有什么用

知乎回答https://www.zhihu.com/question/35595198

自动化构建工具，就是用来代替手工执行机械重复的事情，解放我们的双手的。

例如，项目使用 CoffeeScript/ES6代替Javascript，但浏览器对这些语言是不支持或者支持得不完整的，要让它在浏览器里运行起来就要执行以下操作：

（1）执行编译命令：xx.coffee->xx.js

（2）执行压缩丑化命令：xx.js->xx.min.js

如果文件代码被修改，那么上面两条命令就要再执行一遍。同样的，也会有用Less写CSS，用Jade写HTML，用webpack/Browserify模块化、为非覆盖式部署的资源加MD5戳等等。自动化构建工具就是用来帮助我们完成这些重复而机械的工作的。

b)gulp VS grunt
gulp VS grunt知乎专栏https://zhuanlan.zhihu.com/p/20309820

3.webpack与grunt/gulp
a)不同职能的工具，可以配合使用
官方对webpack的定位是模块打包器，而gulp/grunt属于构建工具。虽然webpack可以代替gulp的一些功能，但是很明显webpack和gulp/grunt不是一个职能的工具。webpack官方中给出了webpack with gulp/grunt的说明，两者可以配合共同服务于一个项目的。

b)构建gulp/grunt与webpack相配合的前端工作流
gulp与webpack的迷思https://segmentfault.com/a/1190000004249679

要构建这样一个工作流,首先要理清几个问题

（1）什么工作应该交给gulp，什么工作应该交给webpack

（2）webpack貌似支持增量更新，gulp是否支持增量更新

（3）如何实现live reload

具体配置方法参考官网

Webpack与grunt官网http://webpack.github.io/docs/usage-with-grunt.html

Webpack与gulp官网http://webpack.github.io/docs/usage-with-gulp.html
```

> #### Git

#### 简要介绍

```
廖雪峰：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/
```

> # 其他

#### 谈谈你对模块化的理解？

```
什么是模块化？

模块化就是为了减少系统耦合度，提高高内聚，减少资源循环依赖，增强系统框架设计。
让开发者便于维护,同时也让逻辑相同的部分可复用
模块化开发：针对js、css，以功能或业务为单元组织代码。js方面解决独立作用域、依赖管理、api暴露、按需加载与执行、安全合并等问题，css方面解决依赖管理、组件内部样式管理等问题。

模块化的过程就是：
1、拆分

将整个系统按功能,格式,加载顺序,继承关系分割为一个一个单独的部分.
注意:拆分的粒度问题,可复用问题,效率问题.如何这些问题处理的不好，就有可能出现不想要的后果。

将功能或特征相似的部分组合在一起,组成一个资源块.
将每个资源块按找需求,功能场景以及目录约束放到固定的地方以供调用.

模块的历程
模块化的发展也是从草根一步一步走过来的。从最开始到现在成熟方案：
1.namespace
2.sass,less
3.AMD&CMD
4.html模版
5.grunt,gulp,webpack
6.FIS,YUI,KISSY
```



