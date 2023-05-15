1、VUE是什么

~~~
Vue.js（/vjuː/，或简称为Vue）是一个用于创建用户界面的开源JavaScript框架，也是一个创建单页应用的Web应用框架
~~~

2、VUE的核心特性

~~~
数据驱动（MVVM)
MVVM表示的是 Model-View-ViewModel

Model：模型层，负责处理业务逻辑以及和服务器端进行交互
View：视图层：负责将数据模型转化为UI展示出来，可以简单的理解为HTML页面
ViewModel：视图模型层，用来连接Model和View，是Model和View之间的通信桥梁

组件化
组件化一句话来说就是把图形、非图形的各种逻辑均抽象为一个统一的概念（组件）来实现开发的模式，在Vue中每一个.vue文件都可以视为一个组件

指令系统
解释：指令 (Directives) 是带有 v- 前缀的特殊属性作用：当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM
~~~

3、Vue和React对比

~~~
相同点
都有组件化思想
都支持服务器端渲染
都有Virtual DOM（虚拟dom）
数据驱动视图
都有支持native的方案：Vue的weex、React的React native
都有自己的构建工具：Vue的vue-cli、React的Create React App

区别
数据流向的不同。react从诞生开始就推崇单向数据流，而Vue是双向数据流
数据变化的实现原理不同。react使用的是不可变数据，而Vue使用的是可变的数据
组件化通信的不同。react中我们通过使用回调函数来进行通信的，而Vue中子组件向父组件传递消息有两种方式：事件和回调函数
diff算法不同。react主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。Vue 使用双向指针，边对比，边更新DOM
~~~

4、什么是SPA

~~~
单页面应用
只有一个WEB主页面的应用，公共资源(js、css等)仅需加载一次，所有的内容都包含在主页面，对每一个功能模块组件化。单页应用跳转，就是切换相关组件，仅刷新局部资源

单页面应用用户体验好、快，内容的改变不需要重新加载整个页面，维护成本低，但不利于搜索引擎的抓取，可使用ssr进行优化，首次渲染速度相对较慢

多页面应用切换加载资源，速度慢，用户体验差，但利于seo的爬取
~~~

5、v-show和v-if有什么区别

~~~
v-show隐藏则是为该元素添加css--display:none，dom元素依旧还在。v-if显示隐藏是将dom元素整个添加或删除

v-if 相比 v-show 开销更大的（直接操作dom节点增加与删除）
如果需要非常频繁地切换，则使用 v-show 较好
~~~

6、Vue实例挂载的过程

~~~
new Vue的时候调用会调用_init方法

定义 $set、$get 、$delete、$watch 等方法
定义 $on、$off、$emit、$off等事件
定义 _update、$forceUpdate、$destroy生命周期
调用$mount进行页面的挂载

挂载的时候主要是通过mountComponent方法

定义updateComponent更新函数

执行render生成虚拟DOM

_update将虚拟DOM生成真实DOM结构，并且渲染到页面中
~~~

7、Vue生命周期

~~~
beforeCreate
初始化vue实例
（执行时组件实例还未创建，通常用于插件开发中执行一些初始化任务）

created
可调用methods中的方法，访问和修改data数据触发响应式渲染dom，可通过computed和watch完成数据计算
此时vm.$el 并没有被创建
(组件初始化完毕，各种数据可以使用，常用于异步数据获取)

beforeMount
在此阶段可获取到vm.el
此阶段vm.el虽已完成DOM初始化，但并未挂载在el选项上

mounted
vm.el已完成DOM的挂载与渲染
(初始化结束，dom已创建，可用于获取访问数据和dom元素)

beforeUpdate
此时view层还未更新

updated
完成view层的更新

beforeDestroy
实例被销毁前调用，此时实例属性与方法仍可访问
(销毁前，可用于一些定时器或订阅的取消)

destroyed
完全销毁一个实例。可清理它与其它实例的连接，解绑它的全部指令及事件监听器
并不能清除DOM，仅仅销毁实例

vue3生命周期
setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
onBeforeMount() : 组件挂载到节点上之前执行的函数。
onMounted() : 组件挂载完成后执行的函数。
onBeforeUpdate(): 组件更新之前执行的函数。
onUpdated(): 组件更新完成之后执行的函数。
onBeforeUnmount(): 组件卸载之前执行的函数。
onUnmounted(): 组件卸载完成后执行的函数
onActivated(): 被包含在中的组件，会多出两个生命周期钩子函数。被激活时执行。
onDeactivated(): 比如从 A 组件，切换到 B 组件，A 组件消失时执行。
~~~

8、v-if和v-for为什么不能一起用

~~~
v-for优先级比v-if高
v-if 和 v-for 同时用在同一个元素上，带来性能方面的浪费（每次渲染都会先循环再进行条件判断）
如果避免出现这种情况，则在外层嵌套template（页面渲染不生成dom节点），在这一层进行v-if判断，然后在内部进行v-for循环
~~~

9、为什么data属性是一个函数而不是一个对象？

~~~
根实例对象data可以是对象也可以是函数（根实例是单例），不会产生数据污染情况
组件实例对象data必须为函数，目的是为了防止多个组件实例对象之间共用一个data，产生数据污染。采用函数的形式，initData时会将其作为工厂函数都会返回全新data对象
~~~

 10、Vue组件之间的通信方式都有哪些？

~~~
父组件传递数据给子组件
子组件设置props属性，定义接收父组件传递过来的参数
父组件在使用子组件标签中通过字面量来传递值

子组件传递数据给父组件
子组件通过$emit触发自定义事件，$emit第二个参数为传递的数值
父组件绑定监听器获取到子组件传递过来的参数

父组件在使用子组件的时候设置ref
父组件通过设置子组件ref来获取数据

兄弟组件传值
创建一个中央事件总线EventBus
兄弟组件通过$emit触发自定义事件，$emit第二个参数为传递的数值
另一个兄弟组件通过$on监听自定义事件

在祖先组件定义provide属性，返回传递的值
在后代组件通过inject接收组件传递过来的值

Vuex作用相当于一个用来存储共享变量的容器
~~~

11、双向数据绑定是什么

~~~
Vue 数据双向绑定原理是通过 数据劫持 + 发布者-订阅者模式 的方式来实现的，首先是通过 ES5 提供的 Object.defineProperty() 方法来劫持（监听）各属性的 getter、setter，每个data中有自己的key每个key对应一个Dep实例，初始化视图时读取某个key，例如name1，创建⼀个watcher1，由于触发name1的getter方法，便将watcher1添加到name1对应的Dep中，当name1更新，setter触发时，便可通过对应Dep通知其管理所有Watcher更新
~~~

12、说说你对vue的mixin的理解，有什么应用场景？

~~~
mixin（混入），提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。
本质其实就是一个js对象，它可以包含我们组件中任意功能选项，如data、components、methods、created、computed等等
我们只要将共用的功能以对象的方式传入 mixins选项中，当组件使用 mixins对象时所有mixins对象的选项都将被混入该组件本身的选项中来

当组件存在与mixin对象相同的选项的时候，进行递归合并的时候组件的选项会覆盖mixin的选项
但是如果相同选项为生命周期钩子的时候，会合并成一个数组，先执行mixin的钩子，再执行组件的钩子

在日常的开发中，我们经常会遇到在不同的组件中经常会需要用到一些相同或者相似的代码，这些代码的功能相对独立
这时，可以通过Vue的mixin功能将相同或者相似的代码提出来
~~~

13、说说你对keep-alive的理解是什么？

~~~
keep-alive是vue中的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM
keep-alive 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们
keep-alive可以设置以下props属性：
include - 字符串或正则表达式。只有名称匹配的组件会被缓存
exclude - 字符串或正则表达式。任何名称匹配的组件都不会被缓存
max - 数字。最多可以缓存多少组件实例

beforeRouteEnter

可以在actived和beforeRouteEnter中对数据进行更新
~~~

14、你有写过自定义指令吗？

~~~
在vue中提供了一套为数据驱动视图更为方便的操作，这些操作被称为指令系统
我们看到的v-开头的行内属性，都是指令，不同的指令可以完成或实现不同的功能

// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()  // 页面加载完成之后自动让输入框获取到焦点的小功能
  }
})

局部注册通过在组件options选项中设置directive属性

bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置

inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)

update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新

componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用

unbind：只调用一次，指令与元素解绑时调用
~~~

15、Vue项目中有封装过axios吗？

~~~
axios 是一个轻量的 HTTP客户端 基于 XMLHttpRequest 服务来执行 HTTP 请求

设置接口请求前缀
利用node环境变量来作判断，用来区分开发、测试、生产环境

在本地调试的时候，还需要在vue.config.js文件中配置devServer实现代理转发，从而实现跨域
devServer: {
    proxy: {
      '/proxyApi': {
        target: 'http://dev.xxx.com',
        changeOrigin: true,
        pathRewrite: {
          '/proxyApi': ''
        }
      }
    }
  }
 设置请求头与超时时间
当需要特殊请求头时，将特殊请求头作为参数传入，覆盖基础配置

封装请求方法
先引入封装好的方法，在要调用的接口重新封装成一个方法暴露出去 
把封装的方法放在一个api.js文件中

请求拦截器
请求拦截器可以在每个请求里加上token，做了统一处理后维护起来也方便

响应拦截器
响应拦截器可以在接收到响应后先做一层操作，如根据状态码判断登录状态、授权
~~~

16、Vue项目中你是如何解决跨域的呢？

~~~
跨域本质是浏览器基于同源策略的一种安全手段
协议相同（protocol）
主机相同（host）
端口相同（port）

JSONP
CORS
Proxy

CORS （Cross-Origin Resource Sharing，跨域资源共享）是一个系统，它由一系列传输的HTTP头组成，这些HTTP头决定浏览器是否阻止前端 JavaScript 代码获取跨域请求的响应
CORS 实现起来非常方便，只需要增加一些 HTTP 头，让服务器能声明允许的访问来源
只要后端实现了 CORS，就实现了跨域

代理（Proxy）也称网络代理，是一种特殊的网络服务，允许一个（一般为客户端）通过这个服务与另一个网络终端（一般为服务器）进行非直接的连接。一些网关、路由器等网络设备具备网络代理功能。一般认为代理服务有利于保障网络终端的隐私或安全，防止攻击
~~~

17、父子组件的生命周期

~~~
加载渲染阶段：父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted
更新阶段：父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated
销毁阶段：父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
~~~

18、computed 和 watch 的区别？

~~~
computed计算属性，依赖其它属性计算值，内部任一依赖项的变化都会重新执行该函数，计算属性有缓存，多次重复使用计算属性时会从缓存中获取返回值，计算属性必须要有return关键词。
watch侦听到某一数据的变化从而触发函数。当数据为对象类型时，对象中的属性值变化时需要使用深度侦听deep属性，也可在页面第一次加载时使用立即侦听immdiate属性。

运用场景：
计算属性一般用在模板渲染中，某个值是依赖其它响应对象甚至是计算属性而来；而侦听属性适用于观测某个值的变化去完成一段复杂的业务逻辑。
~~~

19、什么是slot

~~~
slot插槽，一般在组件内部使用，封装组件时，在组件内部不确定该位置是以何种形式的元素展示时，可以通过slot占据这个位置，该位置的元素需要父组件以内容形式传递过来。slot分为：

默认插槽：子组件用<slot>标签来确定渲染的位置，标签里面可以放DOM结构作为后备内容，当父组件在使用的时候，可以直接在子组件的标签内写入内容，该部分内容将插入子组件的<slot>标签位置。如果父组件使用的时候没有往插槽传入内容，后备内容就会显示在页面。
具名插槽：子组件用name属性来表示插槽的名字，没有指定name的插槽，会有隐含的名称叫做 default。父组件中在使用时在默认插槽的基础上通过v-slot指令指定元素需要放在哪个插槽中，v-slot值为子组件插槽name属性值。使用v-slot指令指定元素放在哪个插槽中，必须配合<template>元素，且一个<template>元素只能对应一个预留的插槽，即不能多个<template> 元素都使用v-slot指令指定相同的插槽。v-slot的简写是#，例如v-slot:header可以简写为#header。
作用域插槽：子组件在<slot>标签上绑定props数据，以将子组件数据传给父组件使用。父组件获取插槽绑定 props 数据的方法：

scope="接收的变量名"：<template scope="接收的变量名">
slot-scope="接收的变量名"：<template slot-scope="接收的变量名">
v-slot:插槽名="接收的变量名"：<template v-slot:插槽名="接收的变量名">
~~~

