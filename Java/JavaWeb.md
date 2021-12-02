# Servlet

- servlet是suin公司开发动态web的一门技术

- Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤；
	1. 编写一个类继承Servlet接口
	2. 把开发好的java类部署到web服务器中

- 把实现了Servlet接口的java程序叫做Servlet

**编写：**

1. 编写一个普通类
2. 实现servlet接口，可以直接继承HttpServlet

### JSP九大内置对象

- PageContext	存东西

- Request    存东西

- Response

- Session    存东西

- Application   【ServletContext】 存东西的

  ==Application 和 ServletContext 意思是相同的，只不过前者JSP后者是Servlet的==

- config

  ==config 和 ServletConfig 意思也是相同的==

- out

- page

- exception

## Cookie

- 一个网站Cookie只能保存一个信息
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- Cookie大小有限制4kb；
- 300个cookie浏览器上限

删除Cookie：

- 不设置有效期，关闭浏览器，自动失效；
- 设置有效期为 0；

## 文件上传

GET：有限制

POST：没有限制