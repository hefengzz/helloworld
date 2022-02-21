# VUE 2

## 认识Vue

```html
<!-- HTML -->
<div id="app">
    <!-- 类似于模板字符串 -->
    {{ message }}
    <h1>obj.name: {{ obj.name }}</h1>
    <ul>
        <li>
            arr[0]: {{arr[0]}}
        </li>
        <li>
            arr[1]: {{arr[1]}}
        </li>
        <li>
            arr[2]: {{arr[2]}}
        </li>
    </ul>
</div>
<!-- Vue.JS -->
<script>
    // 创建一个对象
    var app = new Vue({
        // el: 选择元素
        el: '#app',
        // data: 数据对象
        data: {
            message: 'Hello Vue!',
            obj: {
                name: "Zephyr",
                email: "hefengzz@outlook.com",
                phone: 123456789
            },
            arr: ["苹果", "梨子", "橘子", "葡萄"]
        }
    })
</script>
```

## VUE指令

Vue指令指的是,已`v-`开头的一组特殊语法。



==v-text==

```html
<!-- HTML -->
<div id="app">
    <!-- 使用 v-text 指令时，标签内不可插入任何东西 -->
    <div v-text="message">哈哈</div>
    <div v-text="obj.name">
        <button></button>
    </div>
    <div v-text="arr[0]">哈哈</div>
    <!-- 使用模板语法，值可以被更改 -->
    <div>message: {{ message }} 哈哈</div>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue!',
            obj: {
                name: "Zephyr",
                email: "hefengzz@outlook.com",
                phone: 123456789
            },
            arr: ["苹果", "梨子", "橘子", "葡萄"]
        }
    })
</script>
```

如果需要做字符拼接可以在`属性`中添加或者在`模板语法`中添加，具体请看实例；

```html
<!-- 就和平常在代码中拼接字符串一样的语法「 + "字符"」 -->
<div v-text="message+'拼接了一串字符'"></div>
<div>{{message+'拼接了一串字符'}}</div>
```

==v-html== 此属性和`v-text`，类似于原生JS中`innerText`和`innerHTML`的区别一样

```html
<!-- HTML -->
<div id="app">
    <div v-html="msg"></div>
    <div v-text='msg'></div>
    <div v-html="msg22"></div>
    <div v-text='msg22'></div>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        data: {
            msg: '点击我',
            msg22: '<button>点击我</button>',
        }
    })
</script>
```

==v-on== 用于绑定事件

```html
<!-- HTML -->
<div id="app">
    <button v-on:click="fn">按钮1</button>
    <button v-on:dblclick='fn'>按钮2</button>
    <!-- 这是一种特殊写法，用 @ 符号代替 v-on->
    <button @click='fn'>按钮3</button>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        methods: {
            fn:function(){
                alert(123);
            }
        }
    })
</script>
```

==v-show== 布尔值控制元素，显示或隐藏

==v-if== 布尔值控制元素，显示或隐藏

> `v-show`和`v-if`的区别在于，前者是通过`style="display: none;"`样式属性操作的，而后者是通过删除和添加`dom`元素操作的。
>
> 所以`v-if`相较于`v-show`会比较消耗性能。

==v-bind== 设置元素的属性

```html
<!-- HTML -->
<div id="app">
    <img v-bing:src="src"></img>
    <!-- 这是一种特殊写法，用 : 符号代替 v-bing -->
    <img :src="src"></img>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        data: {
            src: "d:\xxx\xxx\xxx.jpg"
        }
    })
</script>
```

==v-for== 根据数据生成列表结构，通常和数组结合使用

```html
<!-- HTML -->
<div id="app">
    <ul>
        <!-- 类似于 foreach，遍历然后打印数据，只不过这里是遍历然后添加元素 -->
        <li v-for="(item,index) in src">
        	{{ item }}
        </li>
    </ul>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        data: {
            src: ["d:/xxx/xxx/xxx.jpg","d:/xxx/xxx/xxx.jpg"
                  ,"d:/xxx/xxx/xxx.jpg","d:/xxx/xxx/xxx.jpg"]
        }
    })
</script>
```

==v-model== 获取和设置元素中的值（双向数据绑定）

```HTML
<!-- HTML -->
<div id="app">
    <!-- 修改输入框的值，msg也会跟着修改 -->
    <input type="text" v-model="msg"></input>
	<h1>{{msg}}</h1> 
	<button @click="msg='123456'">修改msg的值: 123456</button>
</button>
</div>
<!-- Vue.JS -->
<script>
    var app = new Vue({
        el: '#app',
        data: {
            msg: "haha"
        }
    })
</script>
```


## 插槽

插槽不能使用`v-show` https://www.imooc.com/article/details/id/25193

## Vue响应式渲染

给引用类型新增数据页面不刷新：https://www.jianshu.com/p/71b1807b1815

根据官方文档定义：**如果在实例创建之后添加新的属性到实例上，它不会触发视图更新**。

当Vue的data里边声明或者已经赋值过的对象或者数组（数组里边的值是对象）时，向对象中添加新的属性，如果更新此属性的值，是不会更新视图的。

此坑可以通过官方约定的API`$set`解决

```vue
Vue.set(vm.userInfo,'address','beijing')
<!-- 此时就是在不改变地址引用 就可以直接改变数据  并且渲染在页面上 -->
vm.$set(vm.userInfo,'address','beijing') 也可以实现一样的效果
<!-- 对于列表 上述两种set用法都可以实现改变数据 渲染在网页上 -->
```



## Vue运行过程

template -> ast -> render -> vdom -> UI

模板解析成抽象语法编译运行渲染函数，渲染成虚拟dom然后通过diff算法更新真实dom

![img](https://img-blog.csdnimg.cn/20200101163454894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hpZGlhbjI4NTA=,size_16,color_FFFFFF,t_70)



## 生命周期钩子

Vue2.0的生命周期钩子一共有10个，同样结合官方文档作出了下表

| 生命周期钩子  | 详细                                                         |
| ------------- | ------------------------------------------------------------ |
| beforeCreate  | 在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。 |
| created       | 实例已经创建完成之后被调用。在这一步，实例已完成以下的配置：数据观测(data observer)，属性和方法的运算， watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。 |
| beforeMount   | 在挂载开始之前被调用：相关的 render 函数首次被调用。         |
| mounted       | el 被新创建的 vm.\$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.\$el 也在文档内。 |
| beforeUpdate  | 数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。 |
| updated       | 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。 |
| activated     | keep-alive 组件激活时调用。                                  |
| deactivated   | keep-alive 组件停用时调用。                                  |
| beforeDestroy | 实例销毁之前调用。在这一步，实例仍然完全可用。               |
| destroyed     | Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 |

> （除了beforeCreate和created钩子之外，其他钩子均在服务器端渲染期间不被调用。）



## 动态组件

内置组件`<component></component>`可以实现页面的切换渲染的效果

```vue
<!-- 动态组件由 vm 实例的 is 属性的值控制  -->
<component :is='componentId'></component>

<!-- 也能够渲染注册过的组建或 prop 传入的组建 -->
<component :is='￥options.components.child'></component>
```

`<keep-alive></keep-alive>`组件可以把内部组件进行缓存，而不是销毁组件

```vue
<keep-alive>
    <component :is='componentId'></component>
</keep-alive>

<!-- include 设置需要缓存的组件 -->
<!--  exclude 属性可以让组件不进入缓存 -->
<keep-alive include='componentId1, componentId2'>
    <component :is='componentId1'></component>
    <component :is='componentId2'></component>
    <component :is='componentId3'></component>
</keep-alive>

```



## VUE常用属性

原链接 https://www.cnblogs.com/mengfangui/p/8143702.html

![image-20220219230148839](C:/Users/Zephyr/Desktop/VUE2.assets/image-20220219230148839.png)



## 组件的自定义事件

组件间通讯的一种手段

使用场景：子组件想给父组件传数据，那么就要在父组件中给子组件绑定自定义事件（事件回调在父组件中）

绑定事件：

1. 方式一，在父组件中，子组件根节点自定义监听方法`<Son @传递的方法名='父组件的方法'>`，在方法中定义`父组件的方法`方法，然后在子组件定义方法，方法体中调用`this.$emit('传递的方法名', 传递的参数)`

2. 方式二：在父组件中：`<Son ref='method'>`，然后在父组件中的`mounted`中监听`this.$refs.son.$on('传递的方法名',this.接收的方法)`

   

## 路由

### hash和history

关于#的定义

https://www.cnblogs.com/yeer/archive/2013/01/21/2869827.html

1. HTTP请求不包括hash，在第一个#后面出现的任何字符，都会被浏览器解读为位置标识符。这意味着，这些字符都不会被发送到服务器端。

2. 且改变hash后面的字符不会引起页面重载
3. 改变hash会改变浏览器的访问历史

### 关于两种模式的区别：

https://www.cnblogs.com/ceceliahappycoding/p/10552620.html

简单来说区别在于，地址栏显示的区别，详情看上面的博客。

### 路由的使用

官方示例：https://router.vuejs.org/zh/guide/#html

1. 创建路由并挂载到Vue配置项

   在`src`目录下创建`router`目录，创建`index.js`

   ```js
   import Vue from 'vue'
   import VueRouter from 'vue-router'
   // 导入组件
   import Home from '../components/Home'
   import About from '../components/About'
   // 1. 全局引入VueRouter
   Vue.use(VueRouter)
   
   // 3. 创建r路由配置项，配置路由和组件中的映射关系
   // 这里有个大坑，routes不要写成routers
   const routes = [
   	{
           // 指定hash
           path: '/home',
           // 导入组件
           // 此处有坑component不要写成components
           component: Home,
       }, 
       {
           // 指定hash
           path: '/about',
           // 导入组件
           component: About,
       },
   ]
   // 2. 创建router对象
   const router = new VueRouter({
       // 传入配置项
       routes,
       // 配置模式，默认是hash模式
       mode: 'history'
   })
   
   // 4. 导出挂载到main.js
   export default router
   ```

2. 使用`<route-link>`组件，绑定路由

   ```VUE
   <template>
     <div id="app">
       <router-link to="/home">首页</router-link>
       <router-link to="/about">关于</router-link>
     </div>
   </template>
   ```

3. 使用`<router-view>`组件，渲染当路由组件的模块

   ```VUE
   <template>
     <div id="app">
       <!-- 默认会被渲染成a标签，tag属性可以设置为其它标签 -->
       <router-link to="/home"  tag='button'>首页</router-link>
        <!-- replace属性可以移除历史记录，无法后退 -->
       <router-link to="/about" replace>关于</router-link>
       <!-- 渲染当路由组件的模块 -->
       <router-view></router-view>
     </div>
   </template>
   ```

   

### 编程式导航

官方案例：https://router.vuejs.org/zh/guide/essentials/navigation.html

除了使用 `<router-link>` 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。

**注意：在 Vue 实例中，你可以通过 `$router` 访问路由实例。因此你可以调用 `this.$router.push`。**

所以说可以在自定义事件中使用内置的路由实例来实现页面跳转，就不需要使用`<router-link>`

### 动态路由/命名路由

除了`$router`以外还有一个名字非常相似的`$route`属性，这属性表示的是当前活跃的路由页面

### 路由懒加载

1. 为什么要用路由懒加载。

   在单页面开发模式下，打包文件会把所有的业务代码打包到一个JS文件里，这样会导致用户在请求的过程中出现页面白屏，等待时间过长，非常影像用户体验。

   

   如果使用懒加载的方式就会把组件分为单个JS文件打包，只有在请求的时候才会从服务器拉取资源

   ![image-20220221164759917](C:/Users/Zephyr/Desktop/VUE2.assets/image-20220221164759917.png)



### 嵌套路由

嵌套路由很简单，在一级路由内添加一个`children`属性就可以。

```js
{
    path: '/home',
        // 此处有坑component不要写成components
        component: Home,
            children: [
                {
                    path: '',
                    redirect: 'news'
                },
                {
                    path: 'news',
                    component: HomeNews,
                },
                {
                    path: 'msg',
                    component: HomeMessage
                }
            ]
}
```

### 导航守卫

#### 完整导航解析流程

1. 导航被触发。
2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫(2.2+)。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫(2.5+)。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 DOM 更新。
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。

![image-20220221184224210](C:/Users/Zephyr/Desktop/VUE2.assets/image-20220221184224210.png)
