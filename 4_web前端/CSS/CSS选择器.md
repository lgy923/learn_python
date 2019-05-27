<h2>CSS选择器</h2>

<h3>概述</h3>

在CSS中，选择器（Selector）是一种模式，用于选择需要添加样式的元素。

<h3>CSS基础选择器</h3>

<h4>1、标签选择器</h4>

一个完整的HTML页面是有很多不同的标签组成，而标签选择器，则是决定哪些标签采用相应的CSS样式，如下：

```html
<!-- index.html -->
<div>Hello world!</div>
<span>Hello Asia!</span>
<div>Hello China!</div>
<!-- 三个div标签 -->
```

```css
/* style.css */
div {
    width: 300px;
    height: 300px;
    background-color: red;
}
/* 表示选中所有div标签 */
```

<h4>2、类选择器</h4>

通过class属性给元素自定义命名（参考变量命名规则）。在CSS中，定义选择器应该以 **.** 作为开头，否则浏览器无法识别这是一个类选择器，如下：

```html
<div class="header_list">Hello world!</div>
<div class="header_list">Hello Asia!</div>
<div>Hello China!</div>
```

```css
.header_list {
    width: 100%;
    height: 300px;
}
/* 选中所有类名为header_list的标签 */
```

类，顾名思义，种类，表示一些拥有相同相似性质的事物。所以，**类名可以重复**（我们每个人的名字都可以是马化腾）。

<h4>3、ID选择器</h4>

通过ID属性给元素自定义命名。在CSS中，定义选择器应该从以 **#** 开头，如下：

```html
<!-- index.html -->
<div>Hello world!</div>
<div>Hello Asia!</div>
<div id="national_name">Hello China!</div>
<div id="personal_name">Linda</div>
```

```css
/* style.css */
# national_name {
    font-size: 30px;
    color: red;
}
/* 选中所有id名为national_name的标签 */
```

ID，顾名思义，类似于我们的身份证号，在全国，每个公民拥有唯一的ID号来标识自己的身份。所以，**ID名不可以重复**。

<h4>4、通用选择器</h4>

通用选择器使用 ***** 标识，它的作用是选择页面中的所有元素。该选择器一旦使用后父选择器与后代选择器的搭配容易出现浏览器不能解析的情况，所以平时不推荐大家使用。

```css
/* style.css */
* {
    margin: 0;
    padding: 0;
}
/* 选中所有标签元素 */
```

<h4>5、后代选择器</h4>

是对某元素所嵌套的指定元素进行选择，每个选择符之间 **空格** 进行分割，多个嵌套层次应该以多个空格进行分割。如下：

```html
<!-- index.html -->
<div class="container">
    <article>
        <h1>Napoléon Bonaparte</h1>
        <p>Adversity is the midwife of genius.</p>
    </article>
</div>
```

```css
/* style.css */
.container article {
    text-align: center;
}
.container h1 {
    color: #000000;
}
.container p {
    color: rgb(125,125,0);
}
```

<h4>6、子类选择器</h4>

子类选择器区别于后代选择器的地方就是，后代选择器可以选择嵌套内部任意层级的标签元素，而子选择器只能选择当前标签往内一层的元素，即直接子元素。每个选择符之间用 **>** 进行分割，如下：

```html
<!-- index.html -->
<header>
	<img src="images/logo.png" alt="logo">
	<nav>
		<ul class="menu_list">
			<li><a href="javascript:;">首页</a></li>
			<li><a href="javascript:;">新闻</a></li>
			<li><a href="javascript:;">科技</a></li>
			<li><a href="javascript:;">社会</a></li>
		</ul>
	</nav>
</header>
```

```css
/* style.css */
header > img {
    width: 80px;
    height: 30px;
}
header > nav > ul.menu_list {
    list-style-type: none;
}
```

<h4>7、伪类选择器</h4>

| 选择符              | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| a:link              | 设置超链接a在未被访问之前的样式。                            |
| a:visited           | 设置超链接a在其链接地址已被访过时的样式。                    |
| a:hover             | 设置元素在其鼠标悬停时的样式。                               |
| a:active            | 设置元素在被用户激活（在鼠标点击与释放之间发生的事件）时的样式。 |
| E:focus             | 设置元素在成为输入焦点（该元素的onfocus事件发生）时的样式。  |
| E:root              | 匹配E元素在文档的根元素。                                    |
| E:lang(fr)          | 匹配使用特殊语言的E元素。                                    |
| E:not(s)            | 匹配不含有S选择符的E元素。                                   |
| E:first-child       | 匹配父元素的第一个子元素E。                                  |
| E:last-child        | 匹配父元素的最后一个子元素E。                                |
| E:only-child        | 匹配父元素仅有的一个子元素E。                                |
| E:nth-child(n)      | 匹配父元素的第n个子元素E。                                   |
| E:nth-last-child(n) | 匹配父元素的倒数n个子元素E。                                 |
| E:first-of-type     | 匹配父元素第一个类型为E的子元素。                            |
| E:last-of-type      | 匹配父元素最后一个类型为E的子元素。                          |
| E:empty             | 匹配没有任何子元素（包括text节点）的元素E。                  |
| E:checked           | 匹配用户界面上处于选中状态的元素E。（用于input type为radio与checkbox时） |
| E:enable            | 匹配用户界面上处于可用状态的元素E。                          |
| E:disable           | 匹配用户界面上处于不可用状态的元素E。                        |
| E:target            | 设置页面相关URL指向的E元素。                                 |
| @page:first         | 设置页面容器第一页使用的样式。仅用于@page规则。              |
| @page:left          | 设置页面容器位于装订线左边的所有页面使用的样式。仅用于@page规则。 |
| @page:right         | 设置页面容器位于装订线右边的所有页面使用的样式。仅用于@page规则。 |

注意：

1.  a:hover必须被置于a:link和a:visited之后，才是有效的。
2.  a:active必须被置于a:hover之后，才是有效的。
3.  伪类选择器的名称不区分大小写。

```html
<!-- index.css -->
<ul>
	<li>
		<a href="https://www.baidu.com">Baidu</a>
	</li>
</ul>
```

```css
/* style.css */
a:focus {
    color:red;
}
a:link {
    color:yellow;
}
a:visited {
    color:blue;
}
a:hover {
    color:green;
}
a:active {
    color:pink;
}
```