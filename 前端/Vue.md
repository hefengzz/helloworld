# Vue

## HelloWorld

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

