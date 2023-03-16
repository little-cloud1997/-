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

如果我们希望实现一个计数器：

+ 点击 +1，那么数字便自增 1；
+ 点击 -1，那么数字便自减 1；





















































































































































































































































































































