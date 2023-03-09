### 网络字体

我们在输入文字的时候，浏览器会使用操作系统默认的字体进行显示。而其它字体也有对应的名字，通过名字即可指定字体。

但对于我们下载到本地的字体就不行了，必须先将字体文件引入到当前网页中，然后才可以使用。

~~~html
<style>
    @font-face {
        font-family: "myFont";
        src: url("字体文件路径");  /*还可以指定类型，比如 format("truetype")*/
    }
</style>
~~~

后续通过 myFont 进行引入即可。

> 还有字体图标，www.iconfont.cn ，登录进去下载即可，然后通过 i 标签使用 CSS 里面的类。

![](pic/1.png)

### 认识精灵图 CSS Sprite

什么是 CSS Sprite

+ 是一种图像合成技术，将各种小图片合并到一张图片上，然后利用 CSS 的背景定位来显示对应的图片部分；
+ 有人翻译为：CSS 雪碧，CSS 精灵；

使用 CSS Spirte 的好处

+ 减少网页的 HTTP 请求数量，加快网页的访问速度，减轻服务器压力；
+ 减少图片总大小；
+ 解决了图片命名的困扰，只需要针对一张集合的图片命名；

Spirte 图片一般由设计人员制作。

![](pic/2.png)

比如这里就是一张精灵图，然后选择指定的部分，通过指定大小和位置的方式。

### cursor：设置光标

cursor 可以设置鼠标指针（光标）在元素上面的显示形式，常见的值如下：

+ auto：浏览器根据上下文决定指针的显示样式，比如根据文本和非文本切换指针样式；
+ default：由操作系统决定，一般就是一个小箭头；
+ pointer：一只小手，鼠标指针挪动到链接上面，默认就是这个样式；
+ text：一条竖线，鼠标指针挪到文本输入框上面就是这个样式；
+ none：没有任何指针显示在元素上面；

### CSS  布局之元素定位（非常重要）

#### 标准流

默认情况下，元素都是按照 normal flow（标准流）进行排布

+ 从左到右、从上到下按顺序排放好
+ 默认情况下，兄弟元素之间不存在层叠现象

![](pic/3.png)

如果想调整元素位置，那么可以使用 margin、padding，其中 margin 还可以为负数。但它有比较明显的缺点：

+ 设置一个元素的 margin 和 padding 通常会影响标准流中其它元素的定位效果；
+ 不便于实现元素的层叠效果；

> inline 元素的上下 margin 是无效的，inline-block 和 block 的上下左右 margin 都是有效的，但 margin 0 auto 只有 block 支持。

如果我们希望一个元素可以跳出标准流，单独对某个元素进行设置，那么可以通过 position 属性。这样的话，元素就会脱离文档流，被单独拎出来了，不再受标准文档流的要求按照规则排布了。

#### position 属性

你在浏览网页的时候，发现不断滚轮怎么滑动，有一部分元素始终固定在浏览器视口的某个区域，那么它肯定是脱离了标准文档流。

所以 position 允许你从正常的文档流布局中取出元素，并使它们具备不同的行为：

+ 例如放在另一个元素的上面；
+ 或者始终保持在浏览器视窗内的同一位置；

那么position 都有哪些取值呢？

+ static：默认行为，当没有设置 position 的时候，那么position 默认为 static；
+ relative：相对定位；
+ absolute：绝对定位；
+ fixed：固定定位；
+ sticky：粘性定位；

下面分别介绍。

<font color="green">**static**</font>

+ position 属性的默认值
+ 元素按照 normal flow 布局
+ left、right、top、bottom 没有任何作用（当设置为后面四个值的时候，会被激活）

<font color="green">**relative**</font>

将 position 设置 relative 之后，元素依然是按照标准流布局的，占据相应空间。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .text {
            position: relative;
        }
    </style>
</head>
<body>

<a>你好</a>
<span class="text">古明地觉</span>
<span class="text">古明地恋</span>
<div>魔理沙</div>
</body>
</html>
~~~

![](pic/4.png)

但可以通过 left、right、top、bottom 进行定位，并且定位是相对于元素原来自己的位置。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .text {
            position: relative;
            /*距离不设置 left 时的元素位置的左侧 10px*/
            left: 20px;
        }
    </style>
</head>
<body>

<a>你好</a>
<span class="text">古明地觉</span>
<span>古明地恋</span>
<div>魔理沙</div>
</body>
</html>
~~~

![](pic/5.png)

我们看到元素重叠在一起了，想象一下 margin，如果是 margin 的话，那么会影响其它元素。而使用 left，那么它相当于脱离了标准流，直接相对原本的位置进行移动，而不影响其它元素，因此效果就是两个元素发生了重叠。

![](pic/6.png)

所以相对定位的场景就是，在不影响其它元素位置的前提下，对当前元素进行微调。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        p {
            font-size: 20px;
        }
        span {
            position: relative;
            font-size: 12px;
            bottom: 8px;
        }
    </style>
</head>
<body>
<p>
    3<span>2</span> + 4<span>2</span> = 5<span>2</span>
</p>
</body>
</html>
~~~

![](pic/7.png)

是不是很有趣呢？当然这个功能也可以通过 sup 标签实现。

<font color="green">**fixed**</font>

元素直接脱离文档流，可以通过 left、right、top、bottom 进行定位。注意它和 relative 的区别，前者参照的是元素所在位置本身，而 fixed 参考的是浏览器视窗（viewport），当画布滚动时固定不动。

并且 relative 在不设置位置的时候，还是按照标准流的方式来排的，别的元素不会主动和它重叠，除非我们改变位置。但 fixed 从设置的那一刻就已经脱离标准流了，它就仿佛不存在一样，别的元素会顶替它的位置。至于该元素究竟在哪，则取决于我们。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .text {
            position: fixed;
        }
    </style>
</head>
<body>

<a>你好</a>
<span class="text">古明地觉</span>
<span class="text">古明地恋</span>
<div>魔理沙</div>
</body>
</html>
~~~

这是刚才的例子，但将 relative 改成了 fixed。

![](pic/8.png)

我们看到两个 span 发生了重叠，如果是 relative 的话，那么元素的排列是不会重叠的，仍然按照标准文档流的方式是排列。第二个 span 会在第一个 span 的后面，除非我们手动改变第一个 span 的位置。但将第一个 span 从 relative 改成 fixed 之后，它就已经脱离标准文档流了，元素的排列不会考虑它，因此它和后一个 span 发生了重叠。

一般设置成 fixed 最常用的场景就是回到顶部，再比如右侧的一些导航栏之类的，它们的位置始终固定，且不会随着鼠标的滑动而改变位置。

![](pic/9.png)

我们实现个案例吧，在右下角写一个回到顶部和反馈的用例。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /* 包裹回到顶部和反馈的整个 div 处于 fixed */
        /* 距离右侧 50px 左侧 30px */
        .handler {
            position: fixed;
            right: 50px;
            bottom: 30px;
        }
        /* .handler 下的 .item 的宽和高分别为 80 40 */
        /* 内部的文字居中显示，设置颜色和背景色 */
        .handler .item {
            width: 80px;
            height: 40px;
            text-align: center;
            /* 对于文字而言，让行高和高度保持一致，可以实现垂直居中显示 */
            line-height: 40px;
            color: #fff;
            background-color: seagreen;
            /* 圆角显示 */
            border-radius: 8px;
            /* 设置光标 */
            cursor: pointer;
        }

        /* 鼠标悬浮的时候，改变背景颜色 */
        .handler .item:hover {
            background-color: orange;
        }

        /* 两个 div 要有一段距离 */
        .top {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
<div class="handler">
    <div class="item top">回到顶部</div>
    <div class="item top">反馈</div>
</div>
</body>
</html>
~~~

![](pic/10.png)

这个效果我们就做出来了。

<font color="green">**absolute**</font>

relative 是没有脱离标准流的，只是激活了 left、right等属性，可以在不影响其它元素的情况下改变位置。但 fixed 和 absolute 都会脱离文档流，不过 fixed 是相对于整个浏览器视窗的，而 absolute 是相对于最近的（有定位的）父元素。如果没有找到这样的元素，那么参照的是浏览器视窗，此时就和 fixed 完全等价了。

所以当我们使用 absolute 的时候，一定不是希望它相对浏览器视窗，因为那样使用固定定位 fixed 即可。当使用 absolute 的时候，一定是希望它相对某个父元素，但前提是父元素也要是有定位的。不过按照逻辑上来讲，我们是为了子元素而影响了父元素，非要让父元素设置 position。但这么做也可以，就是你不能影响父元素，所以一般父元素都会设置成 relative，不让它脱离文档流。

> 所以子绝父相就是这么来的，子元素用绝对定位，那么父元素要相对定位。其实对于子元素而言，父元素啥定位都无所谓（除了 static），但是不能影响父元素原本的逻辑。因为父元素原本就是按照标准文档流布局的，所以为了子元素，父元素可以设置 position，但是依然要满足文档流布局。所以这个时候要设置为 relative，此时会激活 left 等属性，但我们不用，那么对父元素就无影响。





















































