# JavaScritpt

## 1. 类型声明

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

## 2. 数据类型

`number`：数字 整数/小数

`NaN`: 

`string`：字符串

`boolean`：true和false

`null`：一个对象为空的占位符

`undefined`：未定义。如果一个变量没有初始化，默认赋值为undefined

1. 数据类型是在运行时确定的。
2. 数据类型是动态的， 意思是一个变量刻意随意赋值任何类型

**变量中的进制**

```javascript
// 八进制
var num1 = 010;
// 十六进制
var num2 = 0xa;
```

### 数据类型转换

##### 转为数字型

1. 整数

   ```javascript
   // 不会做四舍五入
   parseInt('3.14'); // 输出 3
   parseInt('3.99'); // 输出 3
   // 如果是数字开头会截取数字
   parseInt('120px'); // 输出 120
   parseInt('rrr120ll'); // 输出 NaN
   ```

2. 小数

   ```javascript
   parseFloat('3.14'); // 输出 3.14
   // 如果是数字开头会截取数字
   parseFloat('120px'); // 输出 120
   parseFloat('rrr120ll'); // 输出 NaN
   ```

3. 隐式转换

   ```javascript
   // 这些表达式都可以让 String 转为 number
   console.log('120' - 0); // 输出 120
   console.log('120' * 1); // 输出 120
   console.log('120' / 1); // 输出 120
   // 要注意的是 + 是连接字符串
   console.log('120' + 1); // 输出 1201
   ```

##### 转为字符串型

```javascript
// 方法 1
String(123);
// 方法 2
var num = 123;
num.toString;
// 方法 3
console.log(123 + '')
```



## 3. 正则表达式

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

## 4. 标签

`<a>`：超链接功能有两种：

>1. 可以被点击：样式
>2. 点击后跳转到href指定的url，但是通过href="javascript:void(0);"可以实现消除此功能。

## 5. 样式

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

##1. 模板字符串

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

## 2. 函数默认参数

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

## 3. 箭头函数

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

##4. 对象初始化简写

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

##5. 对象结构

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

##6. 传播操作符

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

