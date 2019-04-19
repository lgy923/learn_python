<h2>CSS简介</h2>

CSS（Cascading Style Sheets）：层叠样式表

引入方式

1、内联样式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<div style="color: red">Hello world!</div>
	</body>
</html>
```

2、内部样式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <style>
            div {
                color: red;
            }
        </style>
        
	</head>
	<body>
		<div>Hello world!</div>
	</body>
</html>
```

3、外部样式

style.css文件

```css
div {
	color: red;
}
```

index.html文件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<link rel="stylesheet" href="style.css">
	</head>
	<body>
		<div>Hello world!</div>
	</body>
</html>
```

