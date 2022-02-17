# HTML

## 全称：HyperText Markup Language / 超文本标记语言

## 1. 基础

### 标签的书写形式

标签是用来构建页面框架的，并且有两种书写形式。

1. 封闭类型标签
    `<title></title>`开始标签和结束标签
2. 非封闭类型标签（空标签）
    `<meta>`

### 标签的属性

标签的属性用于给标签提供额外的功能，且可以拥有多个属性，用空格分隔
`<meta charset="UTF-8">`
`<div 属性1="值" 属性2="值" 属性3="值"></div>`

### WEB（网页）组成结构

结构层HTML 表现层CSS 行为层JavaScript

### W3C 万维网联盟

为解决网络应用中不同平台、技术和开发者带来的不兼容问题，保障网络信息流通得顺利完整，万维网联盟制定了一系列标准并督促网络应用开发者和内容提供者遵循这些标准。标准的内容包括使用语言的规范，开发中使用的导则和解释引擎的行为等等。W3C也制定了包括XML和CSS等的众多影响深远的标准规范。

但是，W3C制定的网络标准似乎并非强制，而只是推荐标准，因此部分网站仍然不能完全实现这些标准，特别是使用早期所见即所得网页编辑软件设计的网页往往会包含大量非标准代码。

### 文件命名规范

小写英文字母/数字/_下划线/-的组合
其中不能包含汉字，空格和特殊字符
英文字母开头

### HTML标签

#### 块级元素（标签独占一行）

1. div 容器
    `<div></div>` 常用于给页面划分板块
2. 标题元素
    标题默认自带加粗，垂直方向带有间距，一级标题最大，六级标题最小

    ```javascript
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <h5>五级标题</h5>
    <h6>六级标题</h6>
    ```

    > 页面最大的标题，只能出现一次

3. 段落元素
    `<p></p>` 垂直方向自带段落间距
4. 列表
    - 无序列表

    ```javascript
    <ol>
        <li>有序列表1</li>
        <li>有序列表2</li>
        <li>有序列表3</li>
    <ol>
    ```

    - 有序列表

    ```javascript
    <ol>
        <li>有序列表1</li>
        <li>有序列表2</li>
        <li>有序列表3</li>
    <ol>
    ```

5.水平分割线
    `<hr>`
    > 他是一个空标签

### HTML标签（行内元素）

> 行内元素之间无论敲多少个空格，只会被浏览器解析成一个空格

1. 加粗
    `<b></b>`
    `<strong></strong>`
2. 斜体
    `<i></i>`
    `<em></em>`
3. 下划线
    `<u></u>`
    `<ins></ins>`
4. 删除线
    `<s></s>`
    `<del></del>`
5. 换行
    `<br>`
6. span
一般用于更改一大段文本中个别文本的样式
7. 上标
    `<sup></sup>`
8. 下标
    `<sub></sub>`
9. 图片
    `<img src='图片路径'>`
10. 超链接
    `<a herf='链接'></a>`
    target 属性默认会覆盖页面， target=‘_blank’ 新标签页打开
    > 锚点：`herf`里面使用`id`选择器可以达到页面内跳转的效果

## 2. 表格和表单

1. 表格

    ```html
    <table>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            ...
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            ...
        </tr>
        ...
    </table>
    ```

2. table 的属性
    `border` 边框
    `width` 宽度
    `heigth` 高度
    `cellspacing` 单元格外间距
    `cellpadding` 单元格外间距
    `align` 内容水平对齐方式
    `valig` 内容垂直对齐方式
    `colspan` 向右合并单元格
    `rowspan` 向下合并单元格

3. 表格行分组
    `<caption></caption>` 表格标题
    `<thead></thead>`   表头
    `<tbody></tbody>` 表主体
    `<tfoot></tfoot>` 表尾

4. 表单域

    ```html
    <from action='提交的服务器地址' method='提交的方式 GET/POST' name='名称'>
        <input type='类型' name='这个名称用于作为内容的键，方便传给服务器' value='内容'>
    </from>
    ```

    `input`的`type`属性值包括 【文本框text，密码框password，单选按钮radio，复选框checkbox，提交submit，重置reset，普通按钮button，文件上传file，图像形式的提交按钮，隐藏域hidden】

    - 密码框的`value`是提示内容
    - 复选框的`checked`属性用于表示是否被选中，不写默认未选中

5. 下拉菜单

    ```html
        <select name=''>
            <option value='o1'>选项一</option>
            <!-- selected 属性表示默认被选中 -->
            <option value='o2' selected>选项二</option>
            <option value='o3'>选项三</option>
        </select>
    ```

6. 文本关联控件

    `<lable for=''></lable>`
    `lable`的`for`属性用于关联控件的`id`属性
