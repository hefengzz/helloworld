# CSS (cascading style sheet)

## 全称：cascading style sheet / 层叠样式表

## 1. CSS样式表三种使用方法

1. 内联样式
    - 在`<head></head>`标签中引入一个`<style></style>`
    - CSS选择器由选择器和样式声明组成

    ```css
        选择器 {
            属性名: 属性值;
            属性名: 属性值;
            ...
        }
    ```

    - CSS 属性
        宽度 `width: 200px;` CSS属性值单位必不可少，值为0可以不用
        高度 `hedth: 200px;`
        背景颜色 `backgroud-color:red;`
        字体颜色 `color:red;`
        > 所有块级元素可以设置宽高，行内元素不可以。但这四个行内元素属于例外（`img`,`input`,`textrea`,`select`）

2. 外联样式
    1. 在外部创建的后缀名未`.css`的文件，一般所有CSS文件都在一个css文件夹内部。
    2. 在`<head></head>`标签中用`<link>`引用外部的CSS文件

        ```html
        <head>
            ...
            <link rel='stylesheet' herf=''>
            <!-- rel='stylesheet' 表示关联样式表 -->
            <!-- herf='xxxx.css' 引入路径-->
        </head>
        ```

    3. 在外部css样式表文件开头位置添加 `@charset "utf-8";`，可以防止CSS中存在中文，从而产生乱码的问题。（但是正常开发不会在代码中出现中文所以用的很少）。

    4. 在`<style></style>` 标签中使用 `@import url()` 引入外部的CSS文件

        ```html
        <head>
            ...
            <style>
                /*-- 注意这里引入文件不需要引号包裹 */
                @import url(css/xxx.css);
            </style>
        </head>
        ```

    >**面试** `link` 和 `@import` 的区别
    >
    >1. **引入的内容不同**`link`除了引用样式文件，还可以引用图片等资源文件，而`@import`只引用样式文件
    >2. **加载顺序不同**`link`引入CSS时在页面载入时同时加载，而`@import`需要等待页面**完全载入后**加载
    >3. **兼容性不同**`link`属于XHTML标签，无兼容性问题，而`@import`是CSS2.1提出的，低版本浏览器不支持
    >4. **对JS的支持不同**`link`支持使用JavaScript控制DOM去改变样式，而`@import`不支持

3. 行内样式
    在标签中使用`style`属性设置样式，如：
    `<div style='width: 100px; heigth: 200px; backgorund-color:red;'></div>`

## 2. 选择器

1. 元素选择器
2. **类选择器**
    在元素中使用`class`属性，如：
    `<div class="box"></div>`
    使用方法：`#box {}`
    > 类名命名规则：见名知意，可以包含小写字母，数字，_下划线，-中横杠，**小写字母开头**
    > 元素可以拥有多个类名空格隔开
3. id选择器
    在元素中使用`id`属性，如：
    `<div id="box"></div>`
    使用方法：`.box {}`
    > 一个元素只能有一个id名，一个id名只能被使用一次
    > 一般给大板块取id名，内部其他元素一般使用类名
4. 通配符选择器
    通配符是 * 星号，表示所有的意思，一般用来去除浏览器或元素的默认样式
5. 群组选择器
    多个元素应用同一个样式可以写在一起，用 , 逗号分隔
    `#box, .nav, div {}`
6. **子代选择器**
    一般用于父元素给某一类子元素统一设置样式，可以减少去类名的麻烦
    用 > 大于号来选择元素包裹的子元素
    `#box > div`
    `ul > li`
    > 子代选择器一定是**父子关系**
7. **后代选择器**
    用空格分隔
    `#box a`
    > 后代和子代的区别是，后代是**包含的所有**不一定是父子关系
8. **伪类选择器**
    > `<a></a>` 标签的伪类选择器一定要按下面的顺序引入，不然可能会有某个样式不生效

    ```css
    :link 访问前
    :visited 访问后
    :hover 鼠标移入（常用）
    :active 激活

    使用方法
    :hover{
        backgroud-color: red;
    }
    ```

## 3. 权值

选择器的权值：

- 元素选择器 1
- 类选择器 10
- id选择器 100
- 行内样式 1000
- 属性后面加`!important`**权值最高**

计算权值：

`.warp > ul > li` 权值：12
`#warp li .box` 权值：12
`.warp, li` 权值：拆分计算

## 4. 属性

### 1. 文本属性

1. 字号
    `font-size: 20px;`
    浏览器认为 12px 是文字最小的像素， 所以再低就不会生效了
    文本有多种单位，如：
    **em和rem**
    - em：父元素字体的大小倍数，如果父元素没有设置字号，就是自己字号的倍数
    - rem：根元素字体大小的倍数
2. 字体
    `font-family: '微软雅黑', Arial, 'Times New Roman';`
    - 一般很少去设置，因为不确定用户的电脑中安装了什么字体
    - 写中文用引号包裹，多个单词组用引号包裹
    - 由左向右查找字体
3. 字体颜色
    `color: #e3393c;`
    `color: rgb(255,255,255);`
4. 字体粗细
    `font-weith: normal正常/ weigth加粗/ 100-900之间的整数不带单位`
5. 字体倾斜
    `font-style: italic / oblique`
6. 字体线条
    `text-decoration: none无线条 / underline下划线 / line-through删除线 / overline上划线;`
7. 首行缩进
    `text-indent: 2em`
8. 行高
    `line-heigth: 20px`
    单行文本所占高度，常用于设置文本在容器中垂直居中，行高设置为容器高度即可
9. 字间距
    `letter-spacing: 10px;`
10. 词间距
    中文字符不常用
    `word-spacing: 10px;`
11. 文本和图片的水平对齐方式
    `text-align: left左对齐 / rigth右对齐 / center居中 / justify;`
    > img的水平居中要设置给img的容器，而不是img本身
12. 文本和图片的垂直对齐方式
    `vertical-align: top顶部 / bottom底部 / middle垂直居中 / baseline基线对齐`
    通常我们会去掉img的基线对齐，因为如果不去掉，img的下方会存在3-6px的间距
    `img {vertical-align: middle}`

### 2. 列表属性

1. 列表标识符
    `list-style-type: none无 / disc实心圆 / circle空心圆 / square实心矩形 / decimal数字`
2. 列表图片
    `list-style-image: url();`
3. 标识符位置
    `list-style-positon: inset;`

### 3. 边框属性

四个方向的边框设置
`border: 粗细 线型 颜色;`
线型：solid直线 / dashed虚线 / dotted点状线 / double双线

## 5. CSS 属性的继承

一般来说：`font- / line- / text- / color / opacity` 这些有继承性

## 6. 背景图

背景图一般仅用于装饰作用，而`<img></img>`标签通常是页面内容

1. 背景颜色
    `backgroud-color`
2. 背景图
    `backgroud-image: url();`
3. 背景重复
    `backgroud-repeat: repeat默认值，重复 / no-repeat不重复，只出现一次 / repeat-x水平重复 / repeat-y垂直重复`
4. 背景定位
    `backgroud: 背景颜色 背景图路径 是否重复 背景定位`
    `backgroud-position: 0px 0px;`
    第一个值表示水平位移，正向移动给正值
    rigth右 / left左 / center居中
    第二个值表示垂直位移，正向移动给正值
    top上 / bottom下 / center居中
5. 背景固定
    `backgroud-attachment: fixed`;

## 7. CSS Sprites / 雪碧图 / 精灵图

多个小图拼在一张大图上，通过背景属性引入进来，背景定位来调整具体详引入的背景图位置

## 8. 透明度

1. `backgroud: rgb(255, 255, 255, 0.4);`
    0.4代表 40% 透明度，数值越小越透明。最大1，最小0
2. `opacity: 0-1之间的小数` **有继承性**

## 9. 溢出属性

`overflow: visible默认值，溢出可见 / hidden溢出隐藏 / scroll滚动条 / auto自动`

## 10. 单行文本省略号效果

文本不换行：`white-space: nowrap;`
添加省略号：`text-overflow: ellipsis;`

## 11. 浮动

`float: left左浮动 / right右浮动 / none默认值，不浮动`
>浮动元素会脱离文档流
>浮动元素停止条件：
>
> 1. 碰到父元素边界
> 2. 碰到浮动元素

## 12. 清除浮动

`clear: left / right / both二者;`

## 13. 伪元素选择器

```css
/* 在元素前加一个元素 */
::befor {
    content:'想添加的文本';
}
/* 在元素后加一个元素 */
::after {
    content:'想添加的文本';
}
```

## 14. 父容器高度塌陷问题

1. 笨方法：给父容器固定高度
2. 父容器设置
    `overflow: hidden;`
    父容器设置该属性后，子元素高度参与计算
3. 万能清除浮动

    ```css
    .clear-fix::after{
        content: '';
        display: block;
        clear: both;
    }
    ```

## 15. 元素类型转换

`display: block;`将元素转为块元素
`display: inline;`将元素转为行内元素
`display: inline-block;`将元素转为行内块元素
`display: none;`删除元素

## 16. 元素隐藏的办法

`display: none;`
`opacity: 0;`透明度变为0
`visbility: hidden;` 位置还是占用

## 17. 框模型 / 盒模型

**面试：什么是盒模型** 所有HTML元素可以看作盒子，在CSS中，"box model"这一术语是用来设计和布局时使用。

CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：外边距，边框，内边距（填充），和实际内容。

盒模型允许我们在其它元素和周围元素边框之间的空间放置元素。

> 在元素中设置宽和高，实际上设置的是内容区的宽高。不包括内外边距和边框。

### 外边距 margin

外边距的样式属性：`margin`

通过外边距让元素水平居中：

```css
/* 水平居中 */
/* 方法一 */
/* margin: auto; */
/* 方法二 */
/* margin: 0 auto;  */
/* 方法三 */
/* margin-left: auto; 
margin-right: auto;  */
```

> 浮动元素/脱离文档流的元素不能使用该方法获得水平居中

**面试：使用外边距遇到的问题：**

1. 外边距传递的问题
    给子元素设置上边距会默认作用于父元素
    触发条件：

    - 内外嵌套的`div`
    - 双方都没有设置浮动（其中一个设置就会解决）
    - 父元素没有上边框
    - 子元素上方没有相邻的兄弟元素

2. 垂直外边距相遇问题
    相邻元素设置边距以值最大的为准
    触发条件：
    - 没设置浮动
    - 不能设置尺寸的行内元素，垂直边距不生效

### 内边距 padding（内填充）

内边距的样式属性：`padding`

内边距遇到的问题

1. 元素添加内边距后会撑大尺寸
2. 不能设置尺寸的行内元素，设置垂直方向内边距会撑大元素的高度，但不会改变元素在文档流中的占用高度

## 18. 定位 position

### 偏移量

什么是偏移量? 当元素==开启了定位后==,可以通过偏移量来控制元素的位置,相对的没有开启定位的元素是无法设置偏移量的.
偏移量属性: top / bottom / left / rigth
正向移动取正数，反之

#### static 静态定位

**静态定位**是默认属性,无论你是否有设置 `position:static` 都是静态定位
> 需要知道的是,静态定位是不可以设置偏移量的!

#### relative 相对定位

属性 `position: relative;`

1. 偏移参照物：元素初始位置的原点
2. 脱离文档流：false
3. 使用场景
    - 配合绝对定位使用
    - 元素位置移动，但是要保留初始位置

#### absolute 绝对定位

属性 `position: absolute;`

1. 偏移参照物：
    - 首先查找父元素是否设置**非static**定位属性
    - 如果父元素没有**非static**定位属性，则查找爷爷元素
    - 如果爷爷元素没有，则查找...
    - 知道
2. 脱离文档流：true
3. 使用场景：叠加效果

#### fixed 固定定位

属性 `position: fixed;`

1. 偏移参照物：浏览器文档区的原点
2. 脱离文档流：true
3. 使用场景：在屏幕的某一个位置固定，不随滚动条滚动

#### sticky 粘滞定位

属性 `position: sticky;`

1. 偏移参照物：浏览器文档区顶部
2. 脱离文档流：false
3. 使用场景：做吸顶效果

#### 堆叠顺序 / 层叠顺序

层叠顺序的属性`z-index`

顾名思义，设置元素层叠顺序

一般用在相邻的元素上

#### 面试 元素的居中办法

1. 方法一，中心点居中法
**此方法适用于父元素尺寸未知，子元素尺寸已知（子元素尺寸大于父元素也可用）**
    1. 给父元素设置相对定位，本身设置绝对定位
    2. 设置本身的偏移量

        ```css
        top: 50%; /* 向下移动父元素高度的一半 */
        left: 50%; /* 向右移动父元素宽度的一半 */
        /* 此时当前元素的原点，已经在父元素的中心 */
        ```

    3. 然后，设置本身的外边距

        ```css
        margin-top:   /* 向上移动自身高度的一半 （负值） */
        margin-left:  /* 向左移动自身宽度的一半 （负值） */
        ```

2. 方法二，极限偏移量
**此方法适用于父子元素尺寸都未知，且子元素尺寸小于父元素**
    1. 给父元素设置相对定位，本身设置绝对定位
    2. 设置本身的偏移量

        ```css
        top: 0; 
        bottom: 0;
        left: 0;
        right: 0;

        margin: auto;
        ```

#### 通过定位（偏移量）设置元素尺寸

1. 案例一，子元素自适应
    **此方法适用于只知道父元素内边距的情况**

    1. 给父元素设置相对定位，本身设置绝对定位
    2. 设置本身的偏移量

        ```css
        top: /*上边距*/
        bottom: /*下边距*/
        left: /*左边距*/
        right: /*右边距*/
        ```

    > 这里其实是利用了浮动的知识点

2. （**面试**）案例2， 一侧固定一侧自适应
    方法一
    1. 两侧元素设置固定布局
    2. 左侧元素固定宽高

        ```css
        width: 200px;
        heigth: 500px;
        position: fixed;
        top: 0; 
        left: 0;
        ```

    3. 另一侧根据偏移量自适应尺寸

        ```css
        position: fixed;
        top: 0; 
        left: 另一侧元素宽度;
        bottom: 0;
        ```

    方法二
    1. `html和body`的初始高度是0，需要设置为100%

        ```css
        heigh: 100%;
        ```

    2. 然后一侧固定宽高，另一侧高度100%即可

> 同理，还有其它的布局类型也可以用偏移量的方法做自适应布局
