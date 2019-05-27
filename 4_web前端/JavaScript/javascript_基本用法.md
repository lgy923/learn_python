## JavaScript基本用法

### javascript简介

javascript是一种轻量级的编程语言，是一种高级的，[解释性语言](https://baike.baidu.com/item/解释性语言)和编程语言，同时也是一种[脚本语言](https://baike.baidu.com/item/脚本语言/1379708)。

随着最新的HTML5和CSS3语言标准的推行，它还可以运用于游戏、桌面和移动应用程序的开发，和在服务器端网络环境运行，如[Node.js](http://www.runoob.com/nodejs/nodejs-tutorial.html)。

一般来说，完整的javascript包括以下几个部分：

-   ECMAScript，描述该语言的语法和基本对象；
-   文档对象模型（DOM），描述处理**网页内容**的方法和接口；
-   浏览器对象模型（BOM），描述与**浏览器**进行交互的方法和接口。

javascript的基本特点：

-   是一种解释性脚本语言（代码不进行[预编译](https://baike.baidu.com/item/%E9%A2%84%E7%BC%96%E8%AF%91)）；
-   主要用来向HTML页面添加**交互行为**；
-   可以直接嵌入HTML页面，但写成单独的js文件有利于结构和行为的分离。

javascript常用来完成以下任务：

-   嵌入动态文本与HTML页面；
-   对浏览器事件作出相应；
-   读写HTML元素；
-   在数据被提交到服务器之前验证数据；
-   检测访客的浏览器信息；
-   控制[cookies](https://baike.baidu.com/item/cookie/1119?fr=aladdin)，包括创建和修改等。

### javascript用法

#### 把js代码引入到html文件的方式或写法

1、把javascript代码写在<script></script>标签中(类似于CSS的内联样式)，放在<head></head>标签中。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script>
			document.write("<h1>这是一个标题</h1>");
			document.write("<p>这是一个段落</p>");
		</script>
	</head>
	<body>
	</body>
</html>
```

2、把javascript代码写在<script></script>中，放在<body></body>中，建议放在body最后面。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p>这是网页的信息</p>
		
		<script>
			document.write("<h1>这是一个标题</h1>");
			document.write("<p>这是一个段落</p>");
		</script>
	</body>
</html>
```

3、把javascript代码写在一个 **.js** 文件中，然后通过<script></script>引入到html中(类似于CSS的外部引入样式)。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p>这是网页的信息</p>
		
		<!-- 把js文件夹下的flash.js文件引入到当前html -->
		<script src="js/flash.js"></script>
	</body>
</html>
```
