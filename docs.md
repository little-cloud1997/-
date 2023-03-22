### 组件通信

在开发的时候，可以只创建一个 App.vue，也就是根组件，然后将所有逻辑都放到根组件中，但这样做的话代码就会变得非常臃肿。所以组件化的核心思想就是对组件进行拆分，拆分成一个个小的组件。然后在 App.vue 中将这些小的组件组合嵌套在一起，最终形成我们的应用程序。

举个例子：

![](pic/1.png)

App 组件是根组件，它是 Header、Main、Footer 的父组件，Main 是 Banner 和 ProductList 的父组件，按照这种方式拆分之后，我们开发对应的逻辑只需要去对应组件中编写即可。

而在开发过程中，我们经常会遇到组件之间相互通信的需求。

+ 比如 App 可能使用了多个 Header，每个地方的 Header 展示的内容不同，那么就需要使用者给 Header 传递一些数据，让其进行展示；
+ 又比如我们在 Main 当中一次性请求了 Banner 数据和 ProductList 数据，那么就需要传递给它们进行展示；
+ 也可能是子组件中发生了事件，但是要由父组件来完成某些操作，那么就需要子组件向父组件传递事件；

总之在一个 Vue 项目中，组件之间的通信是非常重要的环节，下面我们就来了解一下组件之间是如何进行通信的。

直接说结论：

+ 父组件传递给子组件：通过 props 属性；
+ 子组件传递给父组件：通过 $emit 触发事件；

#### 父组件传递数据给子组件

先来看看父组件将数据传递给子组件。

~~~html
<!-- components/ProductItem.vue -->
<template>
  <div class="product">
    <p>商品名称: {{ name }}</p>
    <p>商品价格: {{ price }}</p>
    <p>商品数量: {{ count }}</p>
  </div>
</template>

<script>

export default {
  // 我们一会要在父组件中使用 <product-item><product-item/>
  // 所以数据是由父组件传来的，因此这里不能用 data 属性，否则就写死了
  // 表示 {{ }} 里面的 name、proce、count 会使用父组件指定的数据
  props: ["name", "price", "count"]
}
</script>

<style scoped>
.product {
  color: cadetblue;
  margin-top: 10px;
}
</style>

<!-- App.vue -->
<template>
  <h2>商品信息</h2>
  <!-- 使用子组件的时候，同时传递数据 -->  
  <product-item name="香蕉" price="2/个" count="6"></product-item>
  <product-item name="苹果" price="5/个" count="3"></product-item>
</template>

<script>
// 导入组件对象
import ProductItem from "@/components/ProductItem";
export default {
  // 将组件注册到当前组件中，然后在 template 中就可以使用 <product-item> 了
  components: {
    "product-item": ProductItem
  }
}
</script>

<style scoped>
h2 {
  color: cadetblue;
}
</style>
~~~

我们来看一下效果：

![](pic/2.png)

此时我们就是实现了父组件往子组件传递数据。

但是这样做有一个弊端，就是我们无法验证数据是否符合类型，比如子组件的 name 必须是字符串、price 和 count 必须是数值，那么该怎么办呢？

~~~html
<!-- components/ProductItem.vue -->
<template>
  <div class="product">
    <p>商品名称: {{ name }}</p>
    <p>商品价格: {{ price }}</p>
    <p>商品数量: {{ count }}</p>
  </div>
</template>

<script>

export default {
  // 只是表示 name、price、count 三个值来自于父组件，但是类型没有做限制
  // props: ["name", "price", "count"]
  props: {
    name: {type: String, default: "我是默认的 name"},
    price: {type: Number, default: 0},
    count: {type: Number, default: 0},
  }
}
</script>

<style scoped>
.product {
  color: cadetblue;
  margin-top: 50px;
}
</style>

<!-- App.vue -->
<template>
  <h2>商品信息</h2>
  <!-- 如果是 price="2"，那么 price 就是个字符串，但是会自动转化 -->
  <!-- 如果是 :price="2"，那么会把引号里面的内容单独拿出来，此时就是数值 2 -->
  <!-- 如果是 :name="香蕉"，那么会把引号里面的内容单独拿出来，但没有名为 香蕉 这个属性-->
  <!-- 所以希望通过 :name 指定字符串，那么应该指定 :name="'香蕉'" -->
  <product-item name="香蕉" price="2" count="6"></product-item>
  <product-item name="苹果" price="5" count="3"></product-item>
</template>

<script>
// 导入组件对象
import ProductItem from "@/components/ProductItem.vue";
export default {
  components: {
    "product-item": ProductItem
  }
}
</script>

<style scoped>
h2 {
  color: cadetblue;
}
</style>
~~~

此时就对类型进行了限制，除了 type 和 default，还可以指定 required，值为布尔类型，表示是否为必传参数。











































































































































































































