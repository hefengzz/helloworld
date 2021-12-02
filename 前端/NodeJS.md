# Node.js

`Node.js`是一个基于`Chrome V8`引擎的`JavaScript`运行时的语言

用白话说就是类似于`Java`的`JDK`环境，在操作系统中`JVM`虚拟机会将Java代码转为机器码，`node.js`就是负责这个，所以，它让`JavaScript`在后端也能使用了。

通过上述简介，也应该猜到了，`Node.js`也一定提供了很多内置`API`，不过在`Java`中叫做包，这里叫做模块

| 命令    | 含义                                  | 实例                                              |
| ------- | ------------------------------------- | ------------------------------------------------- |
| require | 导入包(同java import差不多，但有差别) | var mysql = require("mysql"); //导入了一个mysql包 |

## nmp


>npm （node package manage）
>通过inpm`下载的包会存记录在``package.json`
>这个文件中，类似于`maven。
```js
//安装模块
npm install 模块名
//安装模块,并在package.json中添加描述
npm install 模块名 --save
npm install 模块名 -S
//从淘宝镜像下载模块
npm install 模块名 --registry=https://registry.npm.taobao.org
//安装具体版本号模块
npm install 模块名@版本号
//全局安装模块
npm install -g 模块名
//卸载模块
npm uninstall 模块名
//卸载模块，并删除依赖项
npm uninstall 模块名 --save
npm uninstall 模块名 -S

// 查看npm配置信息
npm config list
```
查看具体包版本号:
[https://www.npmjs.com/packge/模块名]()
>Babel

`ES6`中有部分高级语法在浏览器和`Node.js’中
都无法运行，`Babel的作用就是转换器。

yarn仓库：

registry: 'https://registry.yarnpkg.com'

## package.json

`package.json`是模块的配置文件，当其中的`main`就表示当前模块的入口文件；

```JS
{
    // 如果package.json中main有值，则其他包引入此模块时会去找到main指定的模块，如果main没有值则会去找index.js
    // 若main既没有值，当前模块下也没有index.js文件，则会一直往上级目录找同名模块直到磁盘根目录找不到，则报错 not find module xxx；
    main: 'index.js'
}
```







## 常用实例/常见问题

**连接数据库**

```javascript
// require导包
var mysql = require("mysql");
// 创建连接对象,配置连接信息
var connection = mysql.createConnection({
    host:"127.0.0.1",
    port:"3306",
    user:"root",
    password:"root",
    database:"smbms"

});
// 开辟连接
connection.connect();
// 执行sql
connection.query("select * from smbms_user", function(error,result,fields) {
    if(error) throw error;

    console.log("result = ", result)
});
```

**可能会遇到的坑**

```javascript
// 连接数据库报错信息
code: 'ER_NOT_SUPPORTED_AUTH_MODE',
errno: 1251,
sqlMessage: 'Client does not support authentication protocol requested by server; consider upgrading MySQL client',
sqlState: '08004',
fatal: true
```

**如何处理**

因为5.0和8.0的mysql密码加密不一样，所以在连接8.0版本的`mysql`会报错，此时需要去`CMD`中修改密码`mysql`加密的方式。

```powershell
# 首先登录数据库
mysql -u root -p
# 更改mysql加密方式
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;
# 修改新密码
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
# 刷新
FLUSH PRIVILEGES;
```



## 模块的加载和导出

`NodeJS`中关于模块有两个关键字，「require」和「export」

|           |                                                              |
| --------- | ------------------------------------------------------------ |
| `require` | 1. 加载文件模块并执行里面的代码<br />2. 拿到被加载文件模块导出的接口对象 |
| `export`  | 1. 每个文件模块中都默认提供了一个对象export<br />2. 默认对象是一个空对象，也就是 {} |

==demo1.js==

```JS
// 导入一个模块，并赋予给变量 a
var a = require("./demo2.js")
// 调用 demo1.js 中的对象 obj
console.log(a.obj);
```

==demo2.js==

```js
var obj = "abc";

// 将对象挂载到模块对象
exports.obj = "hello";

// 对象必须挂载到 export，否则在被引入时其他模块是无法访问到的。
var obj2 = "im obj2";

// 如果一个模块需要直接导出某个成员，则要用以下方式,如果写了多个表达式，则后者会覆盖前者
// module.exports = "123";
// module.exports = "789";
```

