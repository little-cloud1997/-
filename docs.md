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

## JavaScript 的变量声明

在 JavaScript 中可以使用 var 关键字声明一个变量，从 ECMAScript 6（简称 ES6）开始还支持使用 let、const 关键字，我们后续再说，目前先来学习 ES5。

~~~html
<body>
<script>
    // 声明一个 name 变量并赋值
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

<font color="green">**然后是使用变量时的一些注意事项：**</font>

1）如果一个变量没有声明就直接使用，那么会报错；

~~~html
<body>
<script>
    console.log(age)
</script>
</body>
~~~

浏览器在执行这段代码时会报错：Uncaught ReferenceError: age is not defined。再比如执行 var newAge = age，在没有声明 age 的情况下同样会报错，总之不可以使用一个没有声明的变量。

但如果你打印的是 name，不是 age，那么会发现正常执行。

~~~html
<body>
<script>
    console.log(name)
</script>
</body>
~~~

这并不是我们的结论出错了，而是因为默认有一个全局的 name，它位于 window 里面，我们打印一下 window。

![](pic/4.png)

这个 window 是浏览器提供给我们的，当变量不存在时，会从 window 里面查找。关于 window 我们后续会详细说，总之变量必须在声明之后才可以使用。

2）如果一个变量声明了，但是没有赋值，那么会有一个默认值 undefined；

~~~html
<body>
<script>
    var xxx
    console.log(xxx)  // undefined
    console.log(xxx === undefined)  // true
</script>
</body>
~~~

3）变量不声明直接赋值也是可以的，但不推荐，如果不声明直接赋值，那么表示创建一个全局变量（会被添加到 window 对象上）；

~~~html
<body>
<script>
    // 定义一个函数，关于函数后面说
    function func() {
        // 这里没有使用 var 关键字，表示在不声明的情况下直接赋值
        // 此时相当于创建了一个全局变量
        name = "古明地觉"
    }
    func()
    // 函数执行完之后，全局变量就创建好了
    console.log(name)  // 古明地觉
</script>
</body>
~~~

如果在函数里面的 name 前面加上了 var 关键字，那么创建的就是局部变量，只能在函数里面生效。

所以这就是 JavaScript 的变量声明，在声明的时候如果使用了 var 关键字，那么创建的变量只能在当前作用域内使用；如果不使用 var 关键字，那么创建的就是全局变量，在任何地方都可以用。除非你明确自己就是要创建一个全局变量，否则不要省略 var 关键字。

## JavaScript 的数据类型

在 JavaScript 中，每一个值都拥有特定的类型，那么总共都有哪些类型呢？

+ number
+ string
+ boolean
+ undefined
+ null
+ object
+ bigint（ES 6 新增）
+ symbol（ES 6 新增）

可以看到总共八种类型，7 种原始类型，一种复杂类型。

提到数据类型，这里必须要提一个操作符 typeof，它用于检测变量值的类型。因为 JavaScript 是动态语言，我们给一个变量赋值为一个字符串，然后再给它赋值为一个整数，这是允许的。

~~~html
<body>
<script>
    var words = "你好"
    console.log(typeof words)  // string
    words = 123
    console.log(typeof words)  // number
</script>
</body>
~~~

对于动态语言来说，在声明变量的时候无法显式地指定类型，只能根据赋的值去推断。当赋值为 "你好" 时，那么 words 就是 string 类型；后续给 words 重新赋值，不要求类型一定为 string，也可以赋值为别的类型，比如 number。

~~~html
<body>
<script>
    var words
    // 只声明不赋值，值为 undefined，类型也为 undefined
    console.log(typeof words)  // undefined
    // 重新赋值为字符串
    words = "哈哈"
    console.log(typeof words)  // string
    // 重新赋值为整数
    words = 123
    console.log(typeof words)  // number
</script>
</body>
~~~

所以对一个变量或值使用 typeof 时，会返回一个字符串，总共如下几种：

+ "undefined"：表示变量或值未定义；
+ "boolean"：表示变量或值为布尔类型；
+ "string"：表示变量或值为字符串；
+ "number"：表示变量或值为整数或浮点数；
+ "object"：表示变量或值为对象（不是函数）或 null；
+ "function"：表示变量或值为函数；
+ "symbol"：表示变量或值为符号；

下面来分别介绍这些类型。

### number 类型 

number 类型代表整数或浮点数。

~~~html
<body>
<script>
    var age = 17
    var height = 155.5
    console.log(typeof age)  // number
    console.log(typeof height)  // number
</script>
</body>
~~~

number 类型的值可以进行加减乘除、取余等数学运算，还可以进行左移、右移、按位与等位运算。这些运算符和其它语言都是类似的，因此就不赘述了。

除了常规数值，还有一些特殊数值也属于 number 类型。

~~~html
<body>
<script>
    // 代表正无穷
    var a = Infinity
    // 代表负无穷
    var b = -Infinity
    // 代表一个错误，NaN 的意思是 not a number
    var c = NaN
</script>
</body>
~~~

然后是进制，不同进制的整数要怎么表示呢？

~~~html
<body>
<script>
    // 二进制
    var bin = 0b101101
    // 八进制
    var oct = 0o173
    // 十六进制
    var hex = 0xFF
</script>
</body>
~~~

我们也可以获取 JavaScript 所能表示的最大整数和最小整数。

~~~html
<body>
<script>
    var max = Number.MAX_VALUE
    var min = Number.MIN_VALUE
</script>
</body>
~~~

然后 Number 还提供了很多的 API，用来操作一个数值，这些等到后面单独说。

### string 类型

在开发中，我们经常会有一些文本需要表示，这时候我们会使用字符串来保存。

~~~html
<body>
<script>
    // 可以使用双引号，也可以使用单引号
    var name = "古明地觉"
    var where = '地灵殿'
    // 在 ES6 里面还新增了反引号，它实现了 Python 的 f-string 功能
    var info = `name: ${name}，where: ${where}`
</script>
</body>
~~~

字符串很简单，然后是字符串的一些方法和属性，比如字符串的替换、查找等等，这些也留到后面单独说。

### boolean 类型和 undefined 类型

用于表示真假，有两个值：true 和 false。

~~~html
<body>
<script>
    var flag = false
    var flag2 = 2 > 1
    var flag3 = (typeof true) === "boolean"
    console.log(flag)  // false
    console.log(flag2) // true
    console.log(flag3) // true
</script>
</body>
~~~

然后是 undefined 类型，比较简单，就和布尔类型放在一起说了。当一个变量只声明没有赋值的时候，类型和值都为 undefined。

~~~html
<body>
<script>
    var x
    console.log(x)  // undefined
    console.log(typeof x)  // undefined
    // 或者手动赋值给 undefined
    var y = undefined
    // 但判断类型的时候，要写成 "undefined"，不要写成了 undefined
    console.log((typeof y) == "undefined")  // true
</script>
</body>
~~~

注意：在声明变量的时候最好赋一个初始值，并且不要显式地声明为 undefined。

### object 类型和 null 类型

object 类型是一个特殊的类型，我们通常把它们称之为引用类型或复杂类型。

+ 其它的数据类型通常称之为原始类型，因为只能保存单个具体的值；
+ 而 object 类型可以保存非常多的值；

~~~html
<body>
<script>
    // 类似 Python 的字典，但在 JavaScript 里面叫做对象
    // key 可以加引号、也可以不加，如果 key 不符合变量的命名规则，那么必须加引号
    var girl = {
        name: "古明地觉",
        age: 17,
        "public address": "地灵殿"
    }
    // 可以通过 . 的方式来获取，也可以通过 [] 来获取
    console.log(girl.name)
    console.log(girl["age"])
    console.log(girl["public address"])
</script>
</body>
~~~

然后每个类型都有对应的零值，比如 number 类型的零值为 0 或 0.0，string 类型的零值为 ""，那么 object 类型的零值是什么呢？答案是 null。

~~~js
console.log(typeof null)  // object
~~~

所以 null 通常用来表示一个对象为空，在给一个对象初始化时，会赋值为 null。

这里有人分不清 undefined 和 null 的关系，我们总结一下：

+ undefined 通常只有在一个变量已声明、但未初始化的时候才会用到，它的值默认为 undefined；
+ 并且我们不推荐直接给变量赋值给 undefined，所以很少主动来用；
+ null 值非常常用，当变量准备保存一个对象时，但对象不确定，这时候可以先赋值为 null，它就是为 object 类型准备的；

关于类型先说到这里，symbol 和 bigint 后续再聊。

### 数据类型的转换

在开发中，我们会经常对数据进行类型转换。

+ 大多数情况下，运算符和函数会自动将赋予它们的值转成正确的类型，这是隐式转换；
+ 我们也可以通过显式的方式，来对数据进行转换；

下面来看一下数据类型之间的转换，转换主要发生 number、string、boolean 之间。

#### 字符串 string 的转换

其它类型需要经常转成 string 类型，比如和字符串拼接在一起，或者使用字符串中的方法。

转换方式一：隐式转换。

+ 执行 + 操作，如果 + 运算符两边有一个是字符串，那么另一个也会自动转成字符串进行拼接；
+ 某些函数执行时，也会自动将参数转成字符串类型，比如 console.log；

~~~html
<body>
<script>
    // 会以字符串的形式相加
    console.log(123 + "456")  // 123456
    // 如果和空字符串相加，那么等价于将类型转成字符串
    var num = 123
    var numStr = num + ""
    console.log(numStr === "123")  // true
    var flag = true
    var flagStr = flag + ""
    console.log(flagStr === "true")  // true
</script>
</body>
~~~

转换方式二：显式转换。

~~~html
<body>
<script>
    var num = 123
    // 通过 String 函数，将整数转成字符串
    var numStr = String(num)
</script>
</body>
~~~

#### 数值 number 的转换

其它类型也可以转成 number 类型，并且转换方式同样有两种。

方式一：隐式转换。

+ 在非加法算数运算中，会将符号两边的值转成 number 类型进行运算；
+ 但如果是加法，除非 + 号两边都是数值，只有一个是字符串，那么两边都会转成字符串运算；

~~~html
<body>
<script>
    console.log("6" / "2")  // 3
</script>
</body>
~~~

方式二：显式转换

~~~html
<body>
<script>
    // 这里的 62 是字符串
    console.log("6" + "2")  // 62
    // 调用 Number 函数显示转换
    // 这里的 8 是整数
    console.log(Number("6") + Number("2"))  // 8
</script>
</body>
~~~

这里是字符串转整数，如果是其它类型的值：

+ Number(undefined) 返回 NaN
+ Number(null) 返回 0
+ Number(true) 返回 1、Number(false) 返回 0
+ Number(字符串)，当字符串去掉首尾空格后，如果是空字符串，那么返回 0。否则字符必须全部是数字，否则返回 NaN

#### 布尔类型的转换

这个是最简单的，它发生在逻辑运算中，但也可以通过 Boolean 显式地进行转换。

+ 0、空字符串、null、undefined、NaN 都为 false；
+ 其它值为 true

不管显式还是隐式，都符合这个规则。

## JavaScript 的运算符

任何语言都有各种各样的运算符，比如：

+ 算数运算符
+ 赋值运算符
+ 自增和自减
+ 比较运算符
+ 逻辑运算符

像我们生活中使用的 + - * / 便属于运算符，而运算符应用的对象叫做运算元。比如 5 + 2，加号应用在两个对象上，那么它就有两个运算元，因为属于二元运算符。再比如取反操作 ~，它显然就是一元运算符。

### 算数运算符

算数运算符用在数学表达式中，它的使用方式和数学中是一样的。

![](pic/5.png)

比较简单，这里需要说一下幂运算，在 ES7 之前需要通过 Math.pow 计算，但从 ES7 开始变成了一个操作符。当然 Math 里面还有很多其它的函数，比如正余弦，对数等等。

### 赋值运算符

前面使用的 = 也是一个运算符，被称为赋值运算符。

比如 var x = 123，var name = "古明地觉"。

另外 JavaScript 还支持链式赋值，举个例子：

~~~html
<body>
<script>
    var x = 1
    var y = 1
    var z = 1
    
    var x1 = 1, y1 = 1, z1 = 1
    // 当赋的值都相同时，可以采用链式赋值
    var x2 = y2 = z2 = 1
</script>
</body>
~~~

比较简单，没什么好说的。但从代码可读性的角度，不推荐链式赋值。

然后赋值还有一种简写。

+ num = num + 10 等价于 num += 10

所有算数运算符和位运算符都支持这种形式。

说到赋值，自增和自减就一起说了，如果某个变量要增加 1，那么可以写成 num++，减少 1，可以写成 num--。

+ num++ 等价于 num += 1
+ num-- 等价于 num -= 1

### 比较运算符

在数学中，有很多用于大小比较的运算符，这些在 JavaScript 里面也是支持的。

+ a > b, a < b
+ a >= b, a <= b
+ a == b, a != b

比较运算符的结果都是布尔类型。

![](pic/6.png)

这些都是其它语言中出现的，就不详细说说明了。但在 JS 中除了 == 之外，还有 ===。

+ ==，如果两边值的类型不同，那么会统一转成 number 类型的值进行比较；
+ ===，如果两边值的类型不同，那么直接返回 false；

~~~html
<body>
<script>
    var x = ""
    var y = 0
    // x 和 y 转成布尔值之后都是 0
    console.log(x == y)  // true
    console.log(x === y)  // fale
</script>
</body>
~~~

同样的还有 != 和 !==，建议在工作中一律使用 === 和 !==。

## JavaScript 的控制流

任何语言都包含控制流，比如分支、循环，JavaScript 也是如此。

在程序开发中，程序有三种不同的执行方式：

+ 顺序：从上到下，顺序执行代码，这也是 JavaScript 代码的默认执行流程；
+ 分支：根据条件判断，决定执行代码的分支；
+ 循环：让特定代码重复执行

### 分支

说一下 JavaScript 里面的分支，首先是 if 语句。

~~~html
<body>
<script>
    var age = 18
    if (age > 60) {
        console.log("old")
    } else if (age > 18) {
        console.log("adult")
    } else {
        console.log("young")
    }
</script>
</body>
~~~

JavaScript 分支条件必须使用括号包起来，然后具体代码写在大括号里面。注意：JavaScript 的大括号只是为了将代码组合在一起，它并没有定义一个独立的作用域，换句话说里面的声明的变量在外部也是可以生效的。

~~~html
<body>
<script>
    var age = 18
    if (age > 60) {
        console.log("old")
    } else if (age > 18) {
        console.log("adult")
    } else {
        var xx = "aaaa"
        console.log("young")
    }
    console.log(xx)
</script>
</body>
~~~

当 age 小于 18 时，会执行 else 分支，会定义变量 xx，因此可以打印。虽然 xx 是在大括号里面定义的，不过不要紧，它没有单独定义作用域。另外如果某个分支的代码只有一行，那么可以省略大括号。

> 分支的条件也可以跟一个普通的值，会自动调用 Boolean，判断是否为假，这一点和 Python 一样。

来看一下三元运算符，有时我们会根据一个条件去赋值一个变量，比如：

~~~html
<body>
<script>
    var age = 18
    var desc
    if (age >= 18) {
        desc = "已成年"
    } else {
        desc = "未成年"
    }
</script>
</body>
~~~

像这种判断非常常见，而每次都要写 if 语句会很麻烦，于是便有了三元运算符。

var desc = age > 18 ? "已成年" : "未成年"，所以比较简单，规律如下：

+ condition ? val1 : val2，翻译过来就是 condition 满足吗？满足的话就是 val1，否则是 val2

再来补充一下逻辑运算符，&&、||、!

+ && 连接两个布尔值，都为真才为真；
+ || 连接两个布尔值，一个为真就为真；
+ ! 对一个布尔值取反；

然后 JavaScript 还提供了 switch 语句，首先 if 语句里面的分支可以做各种各样的判断，但 switch 语句只能做等值判断，并且是 ===，来看一下。

~~~html
<body>
<script>
    var grade = "D"
    if (grade === "A") {
        console.log("best")
    } else if (grade === "B") {
        console.log("good")
    } else if (grade === "C") {
        console.log("normal")
    } else {
        console.log("bad")
    }
    
    // 如果换成 switch 语句
    switch (grade) {
        case "A": {
            console.log("best")
            break
        }
        case "B": {
            console.log("good")
            break
        }
        case "C": {
            console.log("normal")
            break
        }
        default: {
            console.log("bad")
            break
        }
    }
</script>
</body>
~~~

因为 case 有穿透效果，所以结尾处要加上 break。

### 循环









































































































