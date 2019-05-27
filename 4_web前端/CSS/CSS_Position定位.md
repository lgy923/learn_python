CSS Position（定位）

position属性指定了元素的定位类型，共有5个属性值：

-   static
-   relative
-   fixed
-   absolute
-   sticky

元素还可以使用顶部、底部、左侧和右侧(left、bottom、left、right)的属性定位，都是基于先设定position属性，再使用。

static定位

HTML元素的默认值，即没有定位，遵循正常的文档流对象。静态定位的元素不会受到top、bottom、left、right影响。

fixed定位

元素的位置相对于浏览器窗口是固定位置，即使窗口滑动它也不会移动。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>fixed定位</title>
    
    <style>
        p.pos_fixed {
            position:fixed;
            top:30px;
            right:5px;
        }
    </style>
</head>
<body>
    <p class="pos_fixed">Some more text</p>
    <p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p><p>Some text</p>
</body>
</html>
```

注意：

i、fixed定位使元素的位置与文档流无关，因此不占据空间；

ii、fixed定位的元素和其他元素重叠。



relative定位

相对定位的定位是相对其正常位置。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>relative定位</title>
    <style>
        h2.pos_left
        {
            position:relative;
            left:-20px;
        }

        h2.pos_right
        {
            position:relative;
            left:20px;
        }
    </style>
</head>

<body>
    <h2>这是位于正常位置的标题</h2>
    <h2 class="pos_left">这个标题相对于其正常位置向左移动</h2>
    <h2 class="pos_right">这个标题相对于其正常位置向右移动</h2>
    <p>相对定位会按照元素的原始位置对该元素进行移动。</p>
    <p>样式 "left:-20px" 从元素的原始左侧位置减去 20 像素。</p>
    <p>样式 "left:20px" 向元素的原始左侧位置增加 20 像素。</p>
</body>

</html>
```

移动相对定位元素，但它原本所占的空间不变。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>relative定位</title>
    <style>
        h2.pos_top
        {
            position:relative;
            top:-50px;
        }
    </style>
</head>

<body>
    <h2>这是一个没有定位的标题</h2>
    <h2 class="pos_top">这个标题是根据其正常位置向上移动</h2>
    <p><b>注意:</b> 即使相对定位元素的内容是移动,预留空间的元素仍保存在正常流动。</p>
</body>

</html>
```

