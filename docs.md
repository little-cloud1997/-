### 认识 Vue

Vue 是一套用于构建用户前端界面的渐进式 JavaScript 框架，它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型。帮助你高效地开发用户界面，无论任务是简单还是复杂。

<font color="green">那什么是渐进式框架呢？</font>

+ 表示我们可以在项目中一点点地来引入 Vue，而不一定要全部使用 Vue 来开发整个项目；
+ 但目前来将，很少使用 Vue 来做渐进式开发，基本上用 Vue 都是开发整个项目；

<font color="green">目前 Vue 在前端开发中处于什么地位呢？</font>

目前前端最流行的三大框架：Vue、React、Angula。

+ Angular：入门门槛较高，并且国内市场占有率低，但框架本身是非常优秀的；
+ React：在国内外市场的占有率都非常高，作为前端工程师也是必学的一个框架；
+ Vue：在国内市场的占有率是最高的，几乎所有的前端岗位都会对 Vue 有要求；

总之 Vue 必须要学好的，Vue 对于前端来说非常非常重要。

<font color="green">学习 Vue2 还是 Vue3？</font>

Vue 存在两个版本，分别是 Vue2 和 Vue3，我们应该学习哪一个呢？关于这一点 Vue 的作者给出了答复，直接学习 Vue3 即可，因为 Vue3 兼容 Vue2。而在 2020 年的 9 月 19 日，万众期待的 Vue3 终于发布了正式版，命名为 One Piece，它具有以下特点：

+ 更好的性能；
+ 更小的包体积；
+ 更好的 TypeScript 集成；
+ 更优秀的 API 设计；

那么现在是学习 Vue3 的时间吗？答案是肯定的。

+ Vue3 目前已经是最稳定的版本，并且在 2022 年 2 月 7 日已经成为默认安装版本；
+ 目前社区也经过一定时间的沉淀，更加的完善了，包括 AntDesignVue、Element-Plus 都提供了对 Vue3 的支持，所以很多公司目前新的项目都采用 Vue3 来开发了；
+ 并且在面试的时候，几乎都会问到各种各样 Vue3 相关的问题；

<font color="green">Vue 要如何使用呢？</font>

Vue 的本质就是一个 JavaScript 库（一个普通的 .js 文件），刚开始我们不需要把它想的过于复杂，就把它理解成一个已经帮助我们封装好的库，在项目中引入并使用即可。因此可以把 Vue 想象成 jQuery，它就是一个普通的 JavaScript 库，我们将它下载下来，然后直接通过 script 标签引入就行。

而 Vue 的下载也很简单，我们在浏览器中输入 https://unpkg.com/vue@next 然后回车，就能看到 Vue 的源码了，并且是最新版的 Vue。然后创建一个 vue.js 文件，将源码拷贝到 vue.js 当中，就可以使用了。

~~~html
<body>
<!-- 这里的 src 也可以指定为 https://unpkg.com/vue@next 
     会通过 CDN 自动下载 Vue，另外 jQuery 也支持 CDN -->
<script src="./vue.js"></script>
<script>
    // 使用 Vue
</script>
</body>
~~~

下面我们就来体验一下 Vue。

### Vue 初体验

我们通过 Vue 来往页面中输出一个 h2 标签，内容是 Hello World。

~~~html
<body>

<p>古明地觉</p>
<div id="app"></div>
<p>古明地恋</p>

<script src="./vue.js"></script>
<script>
    // vue.js 引入进来之后有一个全局对象，也叫 Vue
    // 然后它里面有一个函数叫 createApp，该函数接收一个 Object()
    const app = Vue.createApp({
        // 这个对象里面都可以放哪些属性呢？首先是 template
        // 它的意思是模板，可以在里面编写我们的 HTML
        template: `<h2>Hello World</h2>`
    })
    // 可能有人觉得这样编写代码也太麻烦了，别着急，目前只是基础
    // 先把基础打牢，到后面才轻松

    // 目前这个 template 还无法渲染到页面上，因为我们并没有指定内容要被渲染到什么地方
    // 所以执行 app.amount("#app")，表示将内容挂载到 id="app" 的标签内部
    app.amount("#app")
</script>
</body>
~~~

![](pic/1.png)

我们看到内容成功挂载到 #app 里面了，具体做法就是：

+ 通过 Vue 创建一个 app，在内部指定 template 模板；
+ template 就是要渲染到页面上的内容；
+ 内容已经有了，但是要渲染到什么地方去呢？通过 app.mount("#app")，表示将模板内容渲染到 id 为 "app" 的标签里面（注意是标签的里面）；

所以从这里也能感受到 Vue 的渐进式体验，里面的 HTML 元素既可以手动编写，也可以通过 Vue 渲染。

然后来做几个小案例，进一步感受一下 Vue 的使用。

#### 案例一：动态展示数据

我们上面虽然输出了一个 Hello World，但这个数据是写死的，能不能动态展示数据呢？

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        // {{}} 可以理解为一个占位符
        template: `<h2>name: {{name}}, age: {{age}}</h2>`,
        // data 属性需要接收一个函数，函数返回一个对象
        // Vue 会用对象里面的 name 替换掉 template 里面的 {{name}}
        // 用对象里面的 age 替换掉对象里面的 {{age}}
        data: function () {
            return {name: "古明地觉", age: 17}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/2.png)

此时数据就动态展示了，这个功能就比较强大了。并且对于有 Python 经验的人，看到 {{ }} 会立刻反应过来，这不和 Python 的模板渲染引擎是一样的嘛。没错，它们本质都是类似的。然后 data 函数里面的数据是我们随便写的，如果是在工作中的话，我们会向后端请求数据，然后动态渲染到页面上。而在整个过程中，我们不需要手动操作 DOM，这种开发模式就是声明式，我们只负责声明某个位置要展示什么数据，至于渲染则交给框架来完成。

另外看到 {{ }}，估计会有人想到 ES6 的 \${ }，它们本质上都是对字符串做替换，不过替换的时机不一样。

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    let v1 = "姓名"
    let v2 = "年龄"

    const app = Vue.createApp({
        // 里面有两种占位符，一种是 ${ }，另一种是 {{ }}
        // 对于 ${ }，JavaScript 引擎在解析到这行字符串时，就已经把 ${ } 替换掉了
        // 所以这里的 template 实际上就是 "<h2>姓名: {{name}}, 年龄: {{age}}</h2>"
        // 至于 {{ }} 则是 Vue 在渲染的时候，才替换的
        template: `<h2>${v1}: {{name}}, ${v2}: {{age}}</h2>`,

        // data: function() {} 可以简写成 data () {}
        data() {
            return {name: "古明地觉", age: 17}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/3.png)

非常简单，然后再来思考一个问题。如果 template 模板中，{{ }} 里面的变量在 data 函数返回的对象中不存在怎么办？

~~~html
<body>
<div id="app"></div>
    
<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        template: `<h2>name: {{name}}, age: {{age}}</h2>`,
        // 返回的对象中没有 age 这个属性，但是多一个 gender 属性
        data() {
            return {name: "古明地觉", gender: "female"}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/4.png)

首先 data 函数返回的对象中的 gender 属性，template 并没有用到，但是不影响渲染。其次，如果 template 里面要替换的模板变量在 data 函数返回的对象中不存在的话，那么默认会被替换为空字符串。

所以结论很简单，data 函数返回的对象，里面可以包含任意的属性。如果在渲染 template 的时候，发现 {{ ... }} 在对象里面存在，那么就用对应的 value 替换掉；如果不存在，那么替换为空字符串。

#### 案例二：展示列表数据

在上面的案例中，要渲染的数据是一个普通的字符串，比较简单。但如果是一个数组呢？

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        template: `
          <h2>{{title}}</h2>
          <p>{{items}}</p>
        `,
        data() {
            return {title: "守望先锋", items: ["半藏", "麦克雷", "破坏球", "卢西奥"]}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/5.png)

数组的话也是可以渲染的，但很明显我们想要的效果应该不是这样的，我们应该将里面的每个元素放在 li 标签中进行展示。

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        template: `
          <h2>{{title}}</h2>
          <ul>
            <li>{{items[0]}}</li>
            <li>{{items[1]}}</li>
            <li>{{items[2]}}</li>
            <li>{{items[3]}}</li>
          </ul>
        `,
        data() {
            return {title: "守望先锋", items: ["半藏", "麦克雷", "破坏球", "卢西奥"]}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/6.png)

这才是我们真正期望的效果，但代码属于硬编码模式，如果后续数组改变了，那么程序就会出问题。

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        template: `
          <h2>{{title}}</h2>
          <ul>
              <li v-for="item in items">{{item}}</li>
          </ul>
        `,
        data() {
            return {title: "守望先锋", items: ["半藏", "麦克雷", "破坏球", "卢西奥"]}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

我们在 li 标签里面写上了 v-for="item in items"，那么 Vue 在解析的时候就知道要去遍历 items，遍历出来的元素命名为 item。

然后每遍历一次，就创建一个 \<li\>{{ item }}\</li\>，直到遍历结束。其中 {{ item }} 会被替换为遍历得到的具体的值，如果只写 item 而不加 {{ }} 的话，那么 item 就是一个普通的长度为 4 的字符串。

然后我们用浏览器打开，效果和之前是一样的。另外关于这里 v-for，后面会详细讲解。

#### 案例三：计数器

我们来实现一个计数器：

+ 点击 +1，那么数字便自增 1；
+ 点击 -1，那么数字便自减 1；

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    // 计数是不断变化的，肯定不能写死
    const app = Vue.createApp({
        template: `
          <h2>当前计数: {{counter}}</h2>
          <button>加 1</button>
          <button>减 1</button>
        `,
        data() {
            return {counter: 0}
        }
    })

    app.mount("#app")
</script>
</body>
~~~

![](pic/7.png)

因为数字就是 Vue 渲染上去的，它的值取决于 counter，所以如果我们能够改变 counter 的值，那么浏览器上的计数会自动刷新。因此现在要做的是，点击加 1 按钮，那么将 counter 自增 1，点击减 1 按钮，将 counter 自减 1，该怎么实现呢？

~~~html
<body>
<div id="app"></div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        template: `
          <h2>当前计数: {{counter}}</h2>
          <button @click="incr">加 1</button>
          <button @click="decr">减 1</button>
        `,
        data() {
            return {counter: 0}
        },
        // 属性 methods 接收的也是对象，里面是事件对应的一系列的方法
        // 在两个 button 里面我们都绑定了 click 事件
        // @click="incr" 表示的就是：当按钮被点击时，去执行 methods 里面的 incr 函数
        methods: {
            incr() {
                // 修改 counter 即可，但这里可能有人会好奇
                // 为啥通过 this 能拿到 data 函数返回的对象里的属性呢
                // 不用奇怪，这是 Vue 底层帮我们做的，通过 bind 函数将 this 绑定在了某个对象上
                // 而该对象可以操作 data 返回的对象里的属性，后面我们会分析它的原理
                this.counter++
            },
            decr() {
                this.counter--
            }
        }
    })

    app.mount("#app")
</script>
</body>
~~~

我们再来测试一下：

![](pic/8.png)

此时点击按钮，数字就会发生改变。因为点击按钮，会修改 counter 的值，而页面上的数字又是和 counter 绑定的，所以也会跟着改变。上面这个例子就是 Vue 的整个逻辑，以后使用 Vue 的时候，做的基本都是这个事情。后面会介绍 Vue 各种各样的语法，并且编写方式也会有所改变，但核心就是这些东西。

#### 案例三：计数器（重构）

计数器这个功能虽然简单，但是它将 Vue 的核心都体现了出来。不过重新审视一下编写的代码的话，会发现有一个地方让人感觉很不爽，那就是 template。因为当前是将 HTML 代码放在字符串里面的，编写起来非常的不方便，那么能不能将内容放在普通的 HTML 标签里面，然后再让 Vue 渲染呢？答案是可以的。

~~~html
<body>
<div id="app">
    <h2>当前计数: {{counter}}</h2>
    <button @click="incr">加 1</button>
    <button @click="decr">减 1</button>
</div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        data() {
            return {counter: 0}
        },
        methods: {
            incr() {
                this.counter++
            },
            decr() {
                this.counter--
            }
        }
    })

    app.mount("#app")
</script>
</body>
~~~

注意：app.mount("#app") 是将 template 里面的内容渲染之后，挂载到 id="app" 的标签里面。但如果该标签里面本身就有内容的话，那么里面的内容会被丢弃，只显示渲染之后的 template。

但如果没有 template 的话，那么 Vue 会将 id="app" 的标签里面的内容当做 template 进行渲染。因此我们可以不设置 template 属性，而是把内容直接写在要挂载的标签里面，这样做会更方便一些。

我们用浏览器打开文件，效果和之前是一样的。另外上面的案例一和案例二也可以进行重构，只需要将渲染的内容放在要挂载的标签里面，然后删除 template 属性即可。

### 命令式编程和声明式编程的区别

现在我们已经对 Vue 有了一个基本的认识，那么就要对比一下它和之前编写代码的区别。我们将上面的计数器案例使用原生的 JavaScript 实现一下，然后看看两者有什么不一样，进而对比一下命令式编程和声明式编程在思想上的差异。

~~~html
<body>
<div id="app">
    <h2>当前计数: <span>0</span></h2>
    <button id="incr">加 1</button>
    <button id="decr">减 1</button>
</div>

<script>
    // 获取按钮
    let incrBtn = document.getElementById("incr")
    let decrBtn = document.getElementById("decr")
    // 绑定事件
    incrBtn.onclick = function (event) {
        // 获取 h2 里的 span 标签
        let incrSpan = document.querySelector("#app h2 > span")
        // 将里面的值加 1，由于会被当成字符串，所以需要通过 Number 转一下
        incrSpan.innerText = Number(incrSpan.innerText) + 1
    }

    decrBtn.onclick = function (event) {
        let decrSpan = document.querySelector("#app h2 > span")
        decrSpan.innerText = Number(decrSpan.innerText) - 1
    }

</script>
</body>
~~~

最终实现的效果是一样的，如果你是刚学习 Vue 的话，那么通过原生 JavaScript 或者 jQuery 操作 DOM 的方式，会更熟悉一些。这种编程方式叫做命令式编程，而通过 Vue 编程的方式叫做声明式编程，不难发现这两种方式有着很明显的区别。

<font color="green">命令式编程</font>：如果想完成某一个功能，那么必须要思考完成该功能需要哪些步骤，然后一步步完成它。所以它关注是 how to do，how 需要我们来完成。以当前使用原生 JavaScript 编写的计数器为例，如果希望点击按钮能够修改计数器的值，那么需要以下步骤：

+ 通过操作 DOM 的方式，获取按钮对应的标签，然后给它绑定一个点击事件，并开启监听；
+ 当按钮被点击时，执行事件处理函数，在函数中依旧通过操作 DOM 的方式，获取计数器的值，并进行加 1 或减 1；
+ 用更新后的值替换掉计数器的值；

所以每一个操作，都要通过 JavaScript 编写相应的代码，给浏览器一个指令，这就是命令式编程，原生 JavaScript 和 jQuery 都是这种编程模式。

<font color="green">声明式编程</font>：关注的是 what to do，要什么样的效果提前声明好，至于 how 则由框架来完成。以当前使用 Vue 编写的计数器为例，如果希望点击按钮能够修改计数器的值，那么需要以下步骤：

+ 声明一个模板，并将后续要动态变化的数据通过 {{ }} 包起来，即 {{ counter }}。至于点击按钮所执行的函数，也通过 @click 声明好；
+ 定义一个 data 函数，模板里面需要的数据通过 data 函数返回（换句话说就是将数据声明好），然后 Vue 会渲染到页面上。至于 Vue 到底是怎么做的，我们不需要关心，框架会帮我们完成；
+ 而点击事件所执行的函数，也通过 methods 属性指定好，当事件触发时会自动自行；

所以 Vue 的开发模式就是，先声明一个模板，告诉你需要哪些数据。然后我们在其它地方将数据准备好，至于数据怎么渲染到模板上，Vue 会帮我们处理。并且后续当数据发生改变时，页面显示的内容也会自动发生改变，不需要我们手动做绑定操作。

因此这就是声明式编程，当然并不是说 Vue 就不会操作 DOM 了，Vue 底层也是要操作 DOM 的，只不过它将我们的编程方式改变了。以前是要一步一步手动操作 DOM，现在则是将数据声明好、并告诉 Vue 数据要怎么展示即可（指定 template、data、methods），至于具体的绑定过程由 Vue 去做。目前 Vue、React、Angular、小程序的编程模式，都是声明式编程。

#### MVC 和 MVVM 的架构模型

这里再补充一些概念性的东西，就是关于 MVC 和 MVVM，它们都是一种软件的体系结构。

+ MVC 是 Model - View - Controller 的简称，在早期使用非常广泛的一种架构模式，比如 IOS、前端。不过 MVC 对于后端开发人员来说，或许会更熟悉一些，概念是相似的；
+ MVVM 是 Model - View - ViewModel 的简称，是目前非常流行的架构模式；

通常情况下，我们也称 Vue 是一个 MVVM 框架。不过 Vue 官方其实有说明，Vue 虽然没有完全遵守 MVVM 模型，但整个设计是受到它的启发的。那么什么是 MVVM 呢？

![](pic/9.png)

View 可以理解为 DOM，Model 可以理解 JavaScript 的一些对象，说白了就是要展示的数据。本来使用 DOM 就是为了要操作这些数据，然后通过 innerText、innerHTML 等等，将数据放在标签里面，但在 MVVM 当中这两者却不直接沟通。

在 MVVM 中 View 只需要定义模板，比如 <font color="blue">\<h2\>当前计数: {{ counter}}\</h2\></font>，而不用去操作 DOM。然后 ViewModel 会帮我们将 Model 中的数据绑定到 View 上面，也就是 Data Bindings，这是框架帮我们做的第一件重要的事。而第二件重要的事就是事件监听，比如在定义模板的时候绑定了一些事件，那么当事件发生时，由框架帮我们完成 DOM Listeners。我们没有写类似 <font color="blue">btn.onclick = ...</font> 之类的代码，只需要在 View 中定义模板时，通过 @click 指定好要执行的函数即可，当事件发生时，ViewModel 框架会自动帮我们去做。

所以这就是 MVVM 架构，M 是 Model，V 是 View，VM 是 ViewModel，而 Vue 便是 ViewModel 的一种。数据绑定，事件处理，都由 Vue 来完成。

### 聊一聊 createApp 中的 data 属性

Vue.createApp 里面有一个 data 属性，它的值是一个函数，函数里面返回一个对象，用于 template 的渲染；

+ 在 Vue 2.x 的时候，也可以直接给 data 传递一个对象（官方推荐是函数），用于 template 的渲染；
+ 在 Vue 3.x 的时候，必须给 data 传入一个函数，否则浏览器会报错；

而在 data 函数中返回的对象，会被 Vue 的响应式系统劫持，之后对该对象的修改和访问都会在劫持中被处理：

+ 所以在 template 或者 #app 中，可以通过 {{ counter }} 访问 data 函数返回的对象里的 counter 属性；
+ 同时 Vue 还会监听对象的变化，通过 new 一个 Proxy 的方式实现。所以在修改了对象的 counter 属性的值时，Vue 会立刻感知到，将 {{ counter }} 换成修改之后的值，同时浏览器显示的内容也会发生改变；

现在先做一个了解，后面会手动实现它。事实上即便不理解也没关系，Vue 已经封装的非常好了，我们只需要按照它规定的方式编写代码即可。

### 聊一聊 createApp 中的 methods 属性

在计数器的案例中，我们给 button 标签绑定了 click 事件，事件的处理函数是 incr 和 decr。而绑定的过程也很简单，在标签里面写上 @click="incr" 和 @click="decr" 即可。然后具体的 incr 和 decr 函数，我们要写在 methods 属性里面，这是 Vue 的要求。

所以 methods 属性的值是一个对象，通常我们会在这个对象中定义很多的方法：

+ 这些方法可以被绑定到模板中；
+ 在方法中，可以通过 this 关键字来直接访问 data 返回的对象中的属性；

我们再看一下之前关于计数器的案例：

~~~html
<body>
<div id="app">
    <h2>当前计数: {{counter}}</h2>
    <button @click="incr">加 1</button>
    <button @click="decr">减 1</button>
</div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        data() {
            return {counter: 0}
        },
        methods: {
            incr() {
                this.counter++
            },
            decr() {
                this.counter--
            }
        }
    })

    app.mount("#app")
</script>
</body>
~~~

现在来看这个例子就很轻松了，但我想问的是，根据官方文档，我们在定义 incr 和 decr 的时候，不可以使用箭头函数，这是为什么呢？如果不使用箭头函数，而是普通函数，那么里面的 this 又指向谁呢？

<font color="blue">为什么不能使用箭头函数？</font>

如果把 incr 和 decr 换成箭头函数，由于箭头函数不可以绑定 this，那么会从父级作用域中寻找 this，而父级作用域是谁呢？首先肯定不是 methods，因为 methods 是一个对象，它没有自己的作用域，同理 methods 的上一层还是一个对象，也没有自己的作用域。于是再往上找，相信结论很清晰了，如果使用箭头函数，那么里面的 this 最终指向的是 window。

<font color="blue">如果使用普通函数，那么里面的 this 指向谁呢？</font>

有人说它可以访问 data 函数返回的对象的属性，那么它肯定指向这个对象，真的是这样吗？根据我们对 JavaScript 的理解，函数是谁调用的，那么函数里面的 this 就指向谁。

事实上在 Vue 的源码中有一个变量叫 publicThis，它是 data 函数返回的对象的一个代理，当然通过代理也可以修改原对象。然后 Vue 会遍历 methods 对象，取出里面的每一个函数（methodHandler），并调用 <font color="green">methodHandler.bind(publicThis)</font>。我们知道调用 bind 会返回一个新的函数，而 Vue 会用这个新的函数将原来老的函数替换掉。所以后续调用的时候，函数里面 this 的指向就改变了，它会和全局的 publicThis 一样，都指向 data 函数返回的对象的代理。

因此我们通过 this，能够直接操作 data 函数返回的对象里面的属性。

### Vue 模板语法

模板说白了就是要显示在页面上的内容，一开始我们是写在 template 属性里面的，但这样太麻烦了，于是后面又将它写在了要挂载的标签中。而我们接下来的任务就是学习 Vue 的模板语法，掌握了模板语法，我们才能更好地开发。

<font color="blue">首先是 mustache 语法，也就是 {{ }} 实现的文本插值。</font>

如果需要展示一个动态数据，比如前面提到的计数器，那么便可以使用 {{ }} 将 counter 包起来，后续会整体替换掉。并且当 data 函数返回的对象的属性发生改变时，页面内容也会自动更新。

这一点我们已经提到了，但其实 {{ }} 里面不仅仅可以是属性，还可以是一个 JavaScript 表达式。

~~~html
<body>
<div id="app">
    <h2>个人信息</h2>
    <p>姓名: {{ name }}</p>
    <p>年龄: {{ age }}</p>
    <p>年龄+1: {{ age + 1 }}</p>
    <p>兴趣: {{ hobby.join(",")}}</p>
</div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        data() {
            return {name: "古明地觉", age: 17,
                    hobby: ["洞察人心", "在地灵殿歌唱", "探戈"]}
        },
    })
    app.mount("#app")
</script>
</body>
~~~

![](pic/10.png)

注意：{{ }} 里面只能放表达式，不能放语句。因此 {{ }} 里面也可以是一个函数调用，因为函数调用最终返回的也是一个普通的值。

~~~html
<body>
<div id="app">
    <h2>个人信息</h2>
    <p>{{ Number("123") + Number("234") }}</p>
    <p>{{ Number("123") + "234" }}</p>
    <p>{{ mySum(11, 22, 33) }}</p>
    <p>{{ mySum("11", 22, 33) }}</p>
</div>

<script src="./vue.js"></script>
<script>
    const app = Vue.createApp({
        methods: {
            mySum(a, b, c) {
                return a + b + c
            }
        }
    })
    app.mount("#app")
</script>
</body>
~~~

![](pic/11.png)

结果没有问题，{{ }} 里面调用的函数可以是内置的，也可以是我们定义在 methods 对象里面的。所以 {{ }} 还是很强大的，并且也支持三元运算符，不过在实际开发中，不建议在 {{ }} 里面做太复杂的计算。

{{ }} 里面只需要传递一个属性即可，至于该属性对应的值，应该在函数里面提前处理好，而不是等到渲染的时候在 {{ }} 里面计算。

#### v-once 指令

介绍完 mustache 语法之后，再来看看 Vue 提供的一些指令，它也算是模板语法的一部分。首先 Vue 提供的指令非常多，比如 v-for、v-once、v-bind 等等，这些指令都作为标签的属性而存在，比如 <font color="blue">\<h2 v-for="..."\>\</h2\></font> 等等。

我们要学习的第一个指令就是 v-once，

































































































































































































































































































