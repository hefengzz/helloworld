#JavaScritpt

### 类型声明

```javascript
// 局部变量
let i = 0;
// 全局变量
var i = 0;
// 常量
const i = 0;
```

**注意**

在实际开发和生产中，如果是小程序，uniapp活着一些脚手架中的，可以大胆使用`let`和`const`

但是如果你是在`web`开发中，建议还是使用`var`，因为很多低版本的浏览器不支持`ES6`的特性

### 数据类型

`number`：数组	整数/小数/NaN(不是数字的数字类型)

`string`：字符串

`boolean`：true和false

`null`：一个对象为空的占位符

`undefined`：未定义。如果一个变量没有初始化，默认赋值为undefined

### 正则表达式

1. 单个字符:[ ]

   如 `[a] [ab] [a-zA-Z0-9_]`

   * 特殊符号代表特殊含义的单个字符

     ​	`\d`: 单个数字字符 `[0-9]`

     ​	`\w`: 单个单词字符`[a-zA-Z0-9_]`

2. 量词符号

   `?`: 表示出0次或1次

   `*`: 表示出现0次或多次

   `+`: 出现1次或多次
   `{m, n}`: 表示 m <= 数量 => n

   * m 如果缺省:  { ,n} 最多n次
   * n 如果缺省: {m, } 最少m次

### 标签

`<a>`：超链接功能有两种：

>1. 可以被点击：样式
>2. 点击后跳转到href指定的url，但是通过href="javascript:void(0);"可以实现消除此功能。

### 样式

通过document调用属性style时，如果样式属性有「`-`」则可以将横杠后的首字母大写。

使用名称「className」而不是「class」作为属性名,是因为「class」在JavaScript中是个保留字。

所以在使用 JS 设置元素属性是需要非常注意！！！

**案例**

> CSS的写法：`font-size`
>
> JS的写法：`document.getElementById("div1").style.fontSize`



# jQuery

jQuery是JS的库，可以理解为java中的util包，也就是封装类，工具类。

它并不是框架。

帮助文档：https://jquery.cuishifeng.cn/

**语法**

```javascript
/*牢记这个语法：$(选择器).事件(事件函数) */
$('selector').fn()

/*JS: 
	1.获取标签的纯文本
	2.获取标签
	3.往标签写入纯文本
	4.写入标签*/
document.getElementById('selector').innerText
document.getElementById('selector').innerHTML
document.getElementById('selector').innerText = "123"
document.getElementById('selector').innerHTML = "<li>123</li>"

/*jQuery方式：可以使用CSS选择器
	1.获取标签的纯文本
	2.获取标签
	3.往标签写入纯文本
	4.写入标签*/
$('.selector').text(); // 类选择器
$('#selector li[name=js]').html(); //属性选择器 层次选择
$('#selector').text("123");
$('#selector li[name=js]').html("<li>123</li>");

/*设置CSS样式*/
$('#selector').css({"color":"red"});
/*显示和隐藏*/
$('#selector').show();
$('#selector').hide();
```



# ES6

###模板字符串

```javascript
var person = {
    name: 'zephyr',
    address: '广东深圳'
};
let age = '18';

// 传统方式字符串拼接
let str1 = "我叫"+ person.name +"，来自" + person.address + "," + age + "岁";
// ES6新特性
let str2 = `我叫${person.name}${person.address} ${age}岁`;

console.log(str1);
console.log(str2);
```

### 函数默认参数

```javascript
function sum1(a, b) {
    return a + b;
}
sum1(1, 2);
// ES6新特性，给参数默认赋值
function sum2(a, b=5) {
    return a + b;
}
sum2(100);
```

### 箭头函数

箭头函数很重要，在`uniapp`，`小程序`和`脚手架`中经常会使用到

```javascript
var sum1 = function(a, b) {
    return a + b;
}

// 箭头函数 - 改进1,省去了「funciton」关键字
var sum2 = (a, b) => {
    return a + b;
}

// 箭头函数 - 改进2,如果代码块中仅有一行返回逻辑，则可以省去return和大括号，反之不能省去！
var sum2 = (a, b) => a + b;
```

### 对象初始化简写

```javascript
var info = {
    name: 'zephyr',
    address: '广东深圳'，
    go:function() {
        console.log("骑着我心爱小摩托");
    }
}
// ES6
var address = '广东深圳';
var info = {
    name: 'zephyr',
    address，// key和value相同的情况下
    go() {
        console.log("骑着我心爱小摩托");
    }
}
```

### 对象结构

```javascript
var info = {
    name: 'zephyr',
    address: '广东深圳'，
    go:function() {
        console.log("骑着我心爱小摩托");
    }
}
// 通过「.」的方式
console.log(info.name);
console.log(info.address);
info.go();

// 通过「[]」的方式
console.log(info["name"]);
console.log(info["address"]);
info["go"]();

// ES6
var {name, address, go} = info;
console.log(name);
console.log(address);
console.log(go);
```

### 传播操作符

```javascript
var info = {
    name: 'zephyr',
    address: '广东深圳'，
    go:function() {
        console.log("骑着我心爱小摩托");
    }
}

// ES6 ,取走其中一个值，剩下的值会被一个对象打包取走
var {address, ...obj} = info;
console.log(address);
console.log(obj);
```

