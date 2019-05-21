1、打印九九乘法表：

```javascript
<script>
	for (var i = 1; i <= 9; i++){
		var str = ""
		for (var j = 1; j <= i; j++){
			var tmp = j + "*" + i + "=" + j * i + "\t";
			str += tmp;
		}
		console.log(str)
	}
</script>
```

2、打印下面图形：

```
    *
   ***
  *****
 *******
*********
```

```

```

