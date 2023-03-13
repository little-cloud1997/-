## 楔子

要做前端开发，有三座大山是绕不开的，分别是：HTML，CSS，JavaScript。

+ HTML 负责网页的内容结构，相当于人的骨架；
+ CSS 负责网页的视觉体验，相当于人的血肉；
+ JavaScript 负责网页的动态交互，相当于让人具有动态行为；

所以对于一个面向普通用户的网页，HTML、CSS、JavaScript 三者缺一不可，而本次我们的主题就是 JavaScript，后续简称 JS。这里多提一句，JS 在前端开发中非常重要，不管你后续学 Vue 还是 React，都必须要有扎实的 JS 基础。如果 JS 基础不牢固，那么像 Vue、React 这些前端框架，用起来也很难得心应手。

至于 JavaScript 的学习成本，其实也并不高，首先它由三个部分组成：

![](pic/1.png)

JavaScript 和 Python 一样，都是一门普通的解释型语言。我们首先要学习的就是 JavaScript 的语言规范，说白了就是它的语法，也就是 ECMAScript 部分。这一块比较简单，如果有 Python 或其它语言基础的话，学起来会很轻松。然后当语法掌握了之后，我们就会学习如何操作 HTML 中的标签元素，以及浏览器，这些内容我都会一点一点地说清楚。

不仅如此，关于 V8、浏览器底层、内存管理等等，这些内容也会详细剖析。

<font color="green">**然后来思考一个问题**</font>，我们知道任何一门高级语言，最终都需要转成机器指令才能执行，JavaScript 也不例外，JS 代码也要由相应的执行引擎将其翻译成机器指令。那么问题来了，JavaScript 执行引擎在什么地方？

毫无疑问，它内嵌在浏览器内核当中，因为网页是要显示在浏览器里面的。事实上浏览器内核由两部分组成，一部分负责解析 HTML 元素、样式、渲染等相关工作；另一部分就是 JavaScript 执行引擎，负责解析执行 JS 代码。

而不同的浏览器有着不同的 JavaScript 执行引擎：

+ Chakra：微软开发，用于 IE 浏览器；
+ JavaScriptCore：WebKit 中的 JavaScript 引擎，由苹果公司开发，目前在手机端，很多浏览器用的都是它；
+ V8：Chrome 中的 JavaScript 引擎，由谷歌公司开发，该引擎也让 Chrome 在众多浏览器中鹤立鸡群；

<font color="green">**JavaScript 执行引擎我们已经知道在什么地方了，接下来是 JavaScript 代码，它应该写在什么地方呢？**</font>

~~~html
<body>
<!-- 位置一：写在某个标签内部 -->
<p onclick="alert('你好呀')">Say Hello</p>
<a href="javascript: alert('你好呀')">Say Hello</a>

<!-- 位置二：写在 script 标签里面 -->
<script>
    var name = "古明地觉"
    alert("name = " + name)
</script>
<!-- 补充：虽然 script 标签里面是 JS 代码，但它同样遵循 HTML 文档的加载顺序（自上而下） -->  
<!-- 所以 JavaScript 代码所在的 script 标签，应该位于 body 子元素的最底部 -->  

<!-- 位置三：创建一个独立的文件（后缀名为 .js），将代码写在里面，然后通过 src 属性导入进来 -->
<script src="index.js"></script>
</body>
~~~

所以我们可以将 JS 代码写在三个地方，但是位置一基本不用，因为可读性太差，编写也不方便，我们都会写在位置二和位置三当中。

以上我们就简单介绍了一下 JavaScript，下面来开始学习相关语法。

## JavaScript 的变量与数据类型

在 JavaScript 中可以使用 var 关键字定义一个变量，从 ECMAScript 6 开始还支持使用 let、const 关键字，我们后续再说。

~~~html
<body>
<script>
    // 定义一个 name 变量并赋值
    var name = "古明地觉"
    // 也可以先声明，再赋值
    var age
    age = 17
    console.log(name)
    console.log(age)
</script>
</body>
~~~

这里只展示 body 标签里的内容，我们用浏览器打开文件，然后打开控制台，点击 console。

![](pic/2.png)

此时内容就打印在控制台了，console.log 的作用就是将内容输出到浏览器控制台。或者你还以使用 alert，弹出一个窗口，将内容显示在窗口上。

> JavaScript 的注释遵循 C 语言的风格

然后声明变量的时候，也可以同时声明多个。

~~~html
<body>
<script>
    // 同时声明多个变量
    var name, age
    name = "古明地觉"
    age = 17
    
    // 声明多个变量的时候，也可以赋初始值
    var a = 1, b = 2, c = 3
    
    // 当然，也可以只给部分变量赋值
    var d = 4, e, f = 6
    e = 5
    
    // console.log 函数可以打印任意个变量
    console.log(name, age, a, b, c, d, e, f)
</script>
</body>
~~~

比较简单，这里再补充一下 JavaScript 变量的命名规范。

+ 第一个字符必须是字母、下划线或美元符号；
+ 其它字符必须是字母、下划线、数字或美元符号；
+ 不能使用关键字；

然后是命名风格，JavaScript 建议使用驼峰命名法。

<font color="green">**我们编写几个测试案例，再来熟悉一下变量。**</font>

1）测试一：定义两个变量，然后交换它们的值。

~~~html
<body>
<script>
    // 建议一行一行赋值，更加清晰
    var a = 123
    var b = 456

    // 变量定义完之后，还可以修改它，这里我们将 a 和 b 进行交换
    // 在 JS 里面不支持 a, b = b, a 这种方式
    var tmp = a  // 先将 a 的值保存起来
    // 此时 a 的值变成了 b
    a = b   
    // 将 b 的值再变成 a
    b = tmp 
    console.log(a, b)  // 456 123
</script>
</body>
~~~

对于整数类型的变量而言，还可以不借助额外的临时变量完成交换，步骤如下：

+ 执行 a = a + b，此时的 a 保存了 a + b 的值
+ 执行 b = a - b，显然 b 变成了 (a + b - b)、也就是原来的变量 a
+ 执行 a = a - b，由于 b 已经变成了 a，所以最后 a 会变成 (a + b - a)、也就是原来的变量 b

经过以上三步，a 和 b 完成交换，或者还可以使用异或操作。

+ a = a ^ b
+ b = a ^ b
+ a = a ^ b

以上三步也可以完成交换，并且效率更高，这种问题一般在面试中会偶尔出现。

2）测试二：接收用户输入的一个值，并使用变量将它保存起来。

这里的重点是如何接收用户的输入，我们可以使用 prompt 函数。

~~~html
<body>
<script>
    var words = prompt("说一段你想说的话：")
</script>
</body>
~~~

![](pic/3.png)

用户输入内容，然后点击确定，那么输入的内容就会被变量 words 保存起来。注意：在用户点击确定之前，prompt 函数会处于阻塞状态。









































































































































