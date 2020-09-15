### [MVVM模式](#MVVM模式)

### [条件渲染](#条件渲染)

### [列表渲染](#列表渲染)

### [模板语法](#模板语法)

### [计算属性](#计算属性)

### [侦听器](#侦听器)

### [Class与Style绑定](#Class与Style绑定)

### [绑定内联样式](#绑定内联样式)

### [事件处理方法](#事件处理方法)

### [事件修饰符](#事件修饰符)

### [表单输入绑定](#表单输入绑定)

### [修饰符](#修饰符)

### [过渡&动画](#过渡&动画)

### [生命周期和生命周期钩子函数](#生命周期和生命周期钩子函数)

### [组件](#组件)

### [v-model与插槽](#v-model与插槽)

### [axios与fetch实现数据请求](#axios与fetch实现数据请求)

### [过滤器](#过滤器)

### [虚拟DOM与diff算法 key的作用](#虚拟DOM与diff算法 key的作用)

### [Vue-cli的使用方法](#Vue-cli的使用方法)

### [Vue进阶](#Vue进阶)

### [Vue Router](#Vue Router)

### [Vuex](#Vuex)

### [混入](#混入)

### [自定义指令](#自定义指令)



#### Vue的基本特点：

* 数据双向绑定
* 虚拟dom
* 组件话、模块化
* 数据传值。 父子、子父、事件总线、单向数据流、ref
* 轻量级
* 指令
* 客户端路由
* 状态管理

#### MVVM模式：

* model : 负责数据库；
* view：负责页面展示
* view model：负责业务逻辑处理（Ajax请求等），对数据进行加工过后交给视图展示；
* 视图和数据通过vue进行绑定就是MVVM



#### MVC模式：

* M –>model–>模型–>数据（JS变量）
* V-->View—->视图----->用户所见界面（HTML、CSS）
* C--->control—>控制器----->事件交互---->如何根据视图与用户交互后改变数据(通过DOM对象绑定事件，将变量进行修改)



#### 关于Vue：

* 在vue中一个核心的概念就是：数据驱动，避免手动操纵DOM元素。这样的话可以让前端的程序员可以有更多的时间去关注数据的业务逻辑，而不是关注DOM是如何渲染的；                   有双向数据绑定
* Vue和React的相同点：
  * 利用虚拟的DOM实现快速渲染；
  * 轻量级
  * 响应式组件
  * 支持服务器端渲染
  * 易于集成路由工具、打包工具、以及状态管理工具；



#### 条件渲染

* v-if：指令用于条件性的渲染一块内容。这一块内容只在指令的表达式返回true的时候会被渲染，如果设置的为false的话，那么就不会显示该内容
* v-else：v-else必须紧跟在带v-if或者v-else-if的元素的后面，否则他将不会被识别，使用v-else的时候，v-if如果为true那么v-else就不显示，如果为false就显示v-else的内容；注意：v-if和v-else中间不能有其他的元素；v-else可以不写`=""`;
* v-else-if : 顾名思义，充当 `v-if` 的“else-if 块”，可以连续使用：类似于v-else，v-else-if也必须紧紧跟在带v-if或者v-else-if的元素后面；
* 这些条件渲染里面也可以些一些条件表达式;
* v-show : 另一个用于根据条件展示元素的选项，用法大致一样；注意，`v-show` 不支持 `<template>` 元素，也不支持 `v-else`。   
* 注意：v-show和v-if是不一样的，v-if不显示的时候连标签都没有，v-show是css样式中的display：none；



#### 列表渲染：

* v-for：使用v-for把一个数组对应为一组元素；
* 我们可以使用v-for指令基于一个数组来渲染一个列表。v-for指令需要使用`item in items`形式的语法特殊语法，其中`items`是源数据数组，而`item`则是被迭代的数组元素的别名；
* 在 `v-for` 块中，我们可以访问所有父作用域的 property。`v-for` 还支持一个可选的第二个参数，即当前项的索引。
* 在v-for循环的时候，要加上`:key="index"`，作为一个唯一的标识，以便于他能跟踪每一个节点的身份



#### 模板语法：

* 通过使用`v-once`指令，你也能执行一次性地插值，当数据改变的时候，插值处的内容不会更新，但请留心这会影响到该节点的其他数据绑定；
* 关于插入HTML标签，使用`v-html=""`来插入HTML标签,他会把标签的括号也一起插入



#### 计算属性

* 模板内的表达式非常便利，但是设置他们的初衷是用于简单的运算的。在模板中放入太多的逻辑会让模板过重且难以维护；对于任何复杂的逻辑，你都应当使用计算属性
* 使用计算属性的话，就要在vue实例中写入`computed : {}`这个就是`计算的`的意思；



#### 侦听器

* vue提供了一种更通用的方式来观察和响应Vue实例上的数据变动，侦听属性，当你有一些数据需要随着其他数据变动而变动，你很容易滥用`watch`----特别是如果你之前使用过AngularJS。然而，通常更好的做法是使用计算属性，而不是命令式的`watch`回调，
* `watch`是用来监听事件的，就是数据该变的时候，执行相应的函数，他会传一个值，更新的`value`值，`value`就是更新的值





#### Class与Style绑定

* 操作元素的class列表和内联样式是数据绑定的一个常见需求，因为它们都是属性，所以我们可以用`v-bind`来处理它们，只需要通过表达式计算出字符串即可，不过，字符串拼接麻烦且易错。因此，在将`v-bind`用于`class`和`style`时，vuejs做了专门的增强。表达式结果的类型除了字符串以外，还可以是对象和数组；
* 在class与style进行绑定的时候，也可以这样写`<div :class="{active:isTrue}" class="page"></div>`,这样写的话他会自动拼接在一起`class="active page`
* 这里也可以写数组：





####绑定内联样式

* `v-bind:style`的对象语法十分直观---看着非常像CSS，但是其实是一个javascript对象。CSS属性名可以用驼峰式或者短横线分隔来命名；

  ```vue
   <div id="app" :style="{color:activeColor,fontSize:fontSize + 'px'}">
              asdasd
  
  
              <!--直接绑定到一个样式对象通常会更好，这会让模板更加的清晰-->
              <div :style="styleObj">This is my life</div>
          </div>
  
  
  <script>
  //JS
      let app = new Vue({
          el : "#app",
          data : {
              activeColor : "red",
              fontSize : "30",
              styleObj : {
                  color : "red",
                  fontSize : "60px",
              },
          },
      })
  ```



#### 事件处理方法：

* 监听事件：可以使用`v-on`指令来监听DOM事件，并且在触发时运行一些javascript代码。
* 在设置点击事件函数的时候，如果想要event事件的话例如:`@click=“clickEvent(item,index,$event)`



#### 事件修饰符：

* 在事件处理程序中调用`event.preventDefault()`或者`event.stopPropagation()`是非常常见的需求。尽管我们可以在方法中轻松的实现这一点，但是更好的方式是：方法只有纯粹的数据逻辑，而不是去处理DOM事件细节‘

* 为了解决这一个问题，vuejs为`v-on`提供了事件修饰符，之前提过，修饰符是由点开头的指令后缀来表示的；
  * .stop：阻止冒泡
  * .prevent：阻止默认事件
  * .capture：事件捕获
  * .self：触发自身
  * .once：只触发一次
  * .passive：
  
* ##### 案件修饰符：

  * .enter

  * .tab

  * .delete

  * .esc

  * .space

  * .up

  * .down

  * .left

  * .right

  * 你还可以通过全局`config.keyCodes`对象自定义按键修饰符别名;

    ```vue
    //可以使用`v-on:keyup.f1`;
    Vue.config.keyCodes.f1 = 112
    ```



#### 表单输入绑定：

* 你可以使用`v-model`指令在表单`<input>`,`<textarea>`,`<select>`元素上创建双向数据绑定，它会根据控件的类型自动选取正确的方法来更新元素，尽管有些神奇，但是`v-model`本质上不过是语法糖，她负责监听用户输入事件以更新数据，并对一些极端场景进行一些特殊处理；
* 注意：`v-model`会忽略表单有元素的`value`,`checked`,`selected`特性的初始值而总是将vue实例的数据作为数据的来源，你应该通过javascipt在组件`data`选项中声明初始值；
* `v-model`在内部为不同的输入元素使用不同的属性并且抛出不同的事件；
  * text和textarea元素使用value属性和input事件；
  * checkbox和radio使用checked属性和change事件；
  * select字段将value作为prop并将change作为事件



#### 修饰符：

* .lazy: 在默认情况下，`v-model`在每次`input`事件触发后将输入框的值与数据进行同步。你可以添加`lazy`修饰符，从而转为在`change`事件之后进行同步；

  ```vue
  //在change时而非input时
  <input v-model.lazy="mas">
  ```

* .number：如果想将用户输入的值转换为数值类型，可以给`v-model`添加`number`修饰符；

  ```vue
  <input v-model.number="age" type="number">
  ```

* .trim:如果要自动过滤用户输入的首尾空白字符，可以给`v-model`添加`trim`修饰符；

  ```vue
  <input v-model.trim="msg">
  ```

* 注意：多个修饰符是可以一起使用的





#### 过渡&动画

* ##### 单元素/组件的过渡：

  * Vue提供了`transition`的封装组件，在下列情形中，可以给任何元素和组件添加`进入/离开过渡`;

    * 条件渲染（使用v-if）
    * 条件展示（使用v-show）
    * 动态组件
    * 组件根节点

  * 在使用`transition`的时候，把要使用过渡的元素包裹起来就可以了，在使用的过程中应该设置一个`name`告诉它要使用什么类型的过渡。 例如：`name="fade"`,注意属性`name`会跟框架追加的类名一致，那么就是.fade-enter-active

  * ##### 在进入/离开的过渡中，会有 6 个 class 切换，他们会在使用`transition`的时候追加上去

    1. `v-enter`：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
    2. `v-enter-active`：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
    3. `v-enter-to`：**2.1.8 版及以上**定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 `v-enter` 被移除)，在过渡/动画完成之后移除。
    4. `v-leave`：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
    5. `v-leave-active`：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
    6. `v-leave-to`：**2.1.8 版及以上**定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 `v-leave` 被删除)，在过渡/动画完成之后移除。

  * ##### 注意：对于这些在过渡中切换的类名来说，如果你使用一个没有名字的`<transition>`，那么`v-`是这些类名的默认前缀，如果你使用了`<transition name="my-transition">`，那么`v-enter`会替换为`my-transition-enter`；            `v-enter-active`和`v-leave-active`可以控制进入/离开过渡的不同的缓和曲线

  * 下面是一个典型的例子

  * ```vue
    <style>
    .fade-enter-active, .fade-leave-active {
      transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
      opacity: 0;
    }
    </style>
    
    
    <div id="demo">
      <button v-on:click="show = !show">
        Toggle
      </button>
      <transition name="fade">
        <p v-if="show">hello</p>
      </transition>
    </div>
    
    
    new Vue({
      el: '#demo',
      data: {
        show: true
      }
    })
    
    ```

* 自定义过渡的类名：

  * 我们可以通过以下属性来自定义过渡类名：
    * enter-class
    * enter-active-class
    * enter-to-class
    * leave-class
    * leave-active-class
    * leave-to-class
  * 他们的优先级高于普通的类名，这对于Vue的过渡系统和其它第三方CSS动画库，比如`Animate.css`结合十分有用；
  * **注意了：使用animated的时候是animated**
  
* 多个元素过渡：（需要设置key）

  * 当有相同标签名的元素切换时，需要通过` key` 特性设置唯一的标识符来让vue区别他们，否则Vue会为了效率只会替换相同的标签内部的内容；有一个mode属性可以设置动画的进出，in-out、out-in

* 列表过渡（设置key）

  * `<transition-group></transition-group>`不同于transition，他会以一个真实的元素来呈现，默认为一个`span`你也可以通过tag特性更换为其他的元素。   提供唯一的key属性值





#### 生命周期和生命周期钩子函数

* `beforeCreate` ： 此时数据还没有实例化出来，虽然有数据，但是还没有绑定，没有绑定到Vue实例对像上 ，这个时候输出`this`的话，会显示undefined；
* `created`：此时的数据data和方法methds已经绑定到Vue实例上了，这个时候你就可以拿到数据了，但是此时的数据还不能够显示到页面上，渲染到视图上；
* `beforeMount`：此时是数据渲染之前，根据数据生成的DOM对象是获取不到数据的，此时还没有将编译出的html渲染到页面上
* `mounted` ： 此时是渲染之后，此时编译好的html已经挂在到html页面上了，数据已经初始化，注意，mounted在整个生命周期内只能执行一次；
* `brforeUpdate` : 此时是数据已经更改了，但是内容还没有更改
* `Updated` ： 此时内容已经更改完毕，只有在更改之后才能够获取得到数据内容。一般情况想要获取内容，要在内容更改完毕才能够获取
* `beforeDestroy` ： vue实例销毁之前
* `destroyed` ： 实例销毁之后

![](https://img2018.cnblogs.com/blog/1422175/201901/1422175-20190125154237190-1916558490.png)







#### 组件

* 组件是可以复用Vue的实例，且带有一个名字：在这个例子中是<button-countr>。我们可以在一个通过new Vue创建的Vue根实例中，把这个组件作为自定义元素来使用;

  ```vue
  <div id="components-demo">
    <button-counter></button-counter>
  </div>
  
  // 定义一个名为 button-counter 的新组件
  Vue.component('button-counter', {
    data: function () {
      return {
        count: 0
      }
    },
    template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
  })
  
  new Vue({ el: '#components-demo' })
  ```

* 注意：组件里面的`data`必须是一个函数，当我们定义这个`<button-counter>`组件的时候，你可能会发现他的`data`并不是直接提供一个对象，而是一个函数；一个组件的`data`必须是一个函数，因此每一个实例可以维护一份被返回对象的独立拷贝,如果没有这一条规则的话，那么点击一个按钮就会影响到其他所有的实例;

  ```vue
  data : function () {
  	return {
  	count : 0,
  	}
  }
  ```

* template : 就是组件要在页面渲染的内容

* 要使用组件的话就要先注册到Vue实例中，在Vue实例中的`components`中注册

  ```js
  let helloCom = Vue.component("hello-com",{
    template : 	"<h1>{{laochen}}</h1>",
    data : function () {
      return {
        laochen : "hello laochen"
      }
    }
  });
  
  let app = new Vue({
    el : "#app",
    data : {},
    components : {
      "hello-com" : helloCom
    }
  })
  ```

* 注意使用template的时候，在里面添加内容必须有一个最外层的标签包裹所有的内容

* #### 组件中的传值(父元素传递给子元素)：

  * Prop是你可以在组件上注册的一些自定义attribute。当一个值传递给一个prop attribute的时候，他就会变成了那个组件实例的一个property（属性），为了给组件传递一个标题，我们可以使用`props`选项将其包含在该组件可接受的prop列表中；

    ```js
    Vue.component("blog-post",{
      props : ["title"],
      template : "<h3>{{title}}</h3>"
    })
    ```

  * 一个组件默认是可以拥有任意数量的prop，任何值都可以传递给任何prop。在上述模版中，你会发现我们能够在组件实例中访问这个值，就像访问`data`中的值一样；

  * 一个prop被注册之后，我们就可以像这样把数据作为一个自定义的属性传递进来

    ```html
    <blog-post title="My journey with Vue"></blog-post>
    <blog-post title="Blogging with Vue"></blog-post>
    <blog-post title="Why Vue is so fun"></blog-post>
    ```
    
  * ![](https://img-blog.csdnimg.cn/20181228143557186)

* #### 组件中的传值（子元素传递给父元素）

  * ```vue
    父组件可以使用 props 把数据传给子组件。2、子组件可以使用 $emit 触发父组件的自定义事件。
    
    vm.$emit( event, arg ) //触发当前实例上的事件;   定义要触发的事件名称，事件名称传递的值
    
    vm.$on( event, fn );//监听event事件后运行 fn； 
    ```
    
  * 子元素向父组件传值的时候，使用`$event`来获取参数，参数名必须为`$event`
  
  * ```vue
    <div>
    父组件
    <!--这个是子组件-->
    <j-select-user-by-dep  @changeName="changeName($event)"></j-select-user-by-dep>
    <div/>
    ```
  
* 关于`ref`和`$refs`的使用：一般来讲，获取DOM元素的时候，需要使用document.querySelectot(".input1")来获取这个DOM节点，然后再获取input1的值。但是使用ref进行绑定了之后，我们就不需要在在获取DOM节点了，直接在上面input绑定input1，然后$refs里面调用就行了，然后再javascript中`this.$refs.input1`,这样可以减少获取DOM节点的消耗了；

* **注意：ref放在标签上拿到的是原生节点，放在组件上，拿到的是组件对象；**

  ```vue
  <div id="app">
    <input type="text" ref="input1"/>
    <button @click="add">添加</button>
  </div>
  
  <script>
  new Vue({
    el: "#app",
    methods:{
    add:function(){
      this.$refs.input1.value ="22"; //this.$refs.input1 减少获取dom节点的消耗
      }
    }
  })
  </script>
  ```
  
* 组件通信：

  * 父子组件中的传值（props down、events up）
  * 属性验证；
    * props ： {name : Number}
  * 事件机制：
    1. 使用 $on(eventName，callback)监听事件
    2. 使用 $emit(eventName)触发事件
  * Ref：这个是用来给元素或者子组件注册引用信息，引用信息将会注册在父组件的`$refs`对象上；
    * <input ref="mytext" />       this.$refs.mytext.     ref放在标签山拿到的是原生节点，放在组件上，拿到的是组件对象
  * 事件总线：
    * let	bus = new Vue();
    * Mounted生命周期中进行监听
  * 动态组件：
    * <component>元素，动态的绑定多个组件到他的is属性中
    * <keep-alive>保留状态，避免重新渲染，可以保留组件的值，想要使用的话，就使用keep-alive包裹着component组件就行了
    * 所谓的动态组件就是他自己都不知道该加载谁，Vue提供了一个内置的`component`这样的组件，这个组件必须起这个名字，is写哪一个组件他就显示哪一个组件；





#### v-model与插槽

* 自定义事件也可以用于创建支持`v-model`的自定义输出组件：

  * ```vue
    <input v-model="searchText">
    ```

* 等价于

  * ```vue
    <input
      v-bind:value="searchText"
      v-on:input="searchText = $event.target.value"
    >
    ```

* 当用在组件上时，`v-model` 则会这样：

  * ```vue
    <custom-input
      v-bind:value="searchText"
      v-on:input="searchText = $event"
    ></custom-input>
    ```

* 为了让她正常工作，这个组件内的<input>必须：

  * 将`value`属性绑定到一个名叫`value`的prop上；

  * 在input事件被触发之时，将新的值通过自定义的`input`事件抛出；	

  * 写成代码之后是这样的；

    ```vue
    Vue.component('custom-input', {
      props: ['value'],
      template: `
        <input
          v-bind:value="value"
          v-on:input="$emit('input', $event.target.value)"
        >
      `
    })
    ```

  * 现在`v-model`就应该可以在这个组件上完美的工作起来了;

  * ```vue
    <custom-input v-model="searchText"></custom-input>
    ```

* 到目前为止，关于组件的自定义事件你需要了解的大概就是这些了；

* ##### 插槽：

  * 通过插槽来分发内容；

  * 和HTML元素一样，我们经常需要像组件传递内容，就像这样;

  * ```vue
    <alert-box>
    	小心熊出没
    </alert-box>
    ```

  * 但是这样会报错；

  * 幸好，Vue自定义的`<slot>`元素让这变得非常简单；

  * ```vue
    Vue.component('alert-box', {
      template: `
        <div class="demo-alert-box">
          <strong>Error!</strong>
          <slot></slot>
        </div>
      `
    })
    ```

  * 如你所见，我们只需要在需要的地方加入插槽就行了----就这么简单；

  * **slot里面的内容变量只跟父元素有关**





#### axios与fetch实现数据请求

* fetch：XMLHttpRequest是一个设计粗糙的API，配置和调用方式非常的混乱，而且基于事件的异步模型写起来非常的不友好，兼容性也不好；注意：Fetch默认是不带cookie的，需要设置fetch("url",{credentials:"include"});





#### 计算属性

* 复杂的逻辑，模版难以维护；

1. 基础例子：
2. 计算缓存 VS methods
   * 计算属性是基于他们的依赖进行缓存的；
   * 计算属性只有在他的相关的依赖发生改变时才会重新复制；
3. 计算属性 VS watch
4. 使用计算属性的话在要定义一个`computed`，为什么叫计算属性呢，定义起来像一个函数一样，使用起来像一个属性一样；
5. 计算属性的依赖改变了的话，计算属性也会重新计算一遍

* 注意：当表达式包含3个操作，并不是很清晰，所以在遇到复杂的逻辑时应该使用“计算属性”
* 关于使用filter的时候，这个方法他会创建一个新的数组，原数组中的每一个元素都是传入回掉函数中，回调函数中有`return`返回值，若是返回值为true，那么这一个元素会保存在新的数组中，若是返回值为false，则该元素不会保存在新的数组中；但是原数组不会发生改变；





#### 过滤器：

* filters(局部过滤器)，过滤器的定义和methds是一样的，要使用过滤器的话`<h3>{{price | myPrice}}</h3>`在当前的模模版字符串后面加一个管道符，后面紧接着就是过滤器的名字，这个时候模版字符串就会经过这个过滤器,要过滤完成之后才会显示数据
* 全局过滤器 Vue.filter("filterName",callback),调用的时候可以直接使用filterName，不管是全局过滤器还是局部过滤器都需要返回一个值



#### 虚拟DOM与diff算法 key的作用

* 









#### Vue-cli的使用方法

* 创建项目--vue create myapp
* npm run serve 开发环境构建
* npm run build 生产环境构建
* npm run lint 代码检测工具（会自动修正）





#### Vue进阶

* 单文件组件：

  * ```html
    <template>
    	html代码
    </template>
    
    <script>
    	js代码
    </script>
    
    <style>
    	css代码
    </style>
    ```

* 整个文件的执行流程，`index.html > main.js > app.vue > index.js > xx.vue`,如果main文件里面有钩子函数的话会先走钩子函数

* Index.html文件：主页，项目入口

* App.vue--根组件

* Main.js--入口文件, main.js文件中的`render函数`的作用就是将App那个vue组件渲染成DOM节点，`render函数`里面的形参，可以做到这一点，所以`h`这个函数，里面传进去一个组件。**注意：`h`代表的是`createElement--通过指定的名称创建一个元素`**

* 组件中会有<style scoped>后面加上scoped，意思是让样式在这个组件中私有化，就是样式只是限制在本组件中，这样可避免与外界样式出项混淆的状况

* 注意：写vue项目的时候，会有你的图片无法显示的问题，这个不是你的文件的路径的问题，而是这个是在服务器上运行的，`localhst：8080`上面没有你的图片地址，时候在你的图片地址上加上`require()`这个函数，就像导入模块一样的把你的图片导入进来就行了







### Vue Router

使用`router-link`组件来导航，通过传入`to`属性来指定链接，`router-link`会被渲染成一个a标签，它的本质也是一个a标签

注意了，一般的话我们是把一个页面的小组件放在`components`里面，大组件放在`views`

* ####  动态路由匹配：

  我们经常把某种模式匹配到所有路由，全都映射到同个组件。例如，我们有一个user组件，对于所有ID各不相同的用户，都要使用这个组件来渲染。那么我们可以在`vue-router`的路有路径中使用`动态路径参数`来达到这个效果；

  ```vue
  const User = {
  template: "<div>User</div>"
  }
  
  const router = {
  routes :[
  //动态路径参数 以冒号开头
  {path : "/user/:id",component : User}
  ]
  }
  ```

  一个“路径参数”使用冒号`:`标记。当匹配到一个路由的时候，参数值会被设置到`this.$route.params`,可以在每一个组件中使用，于是我们更新User模版，输出当前用户的ID

  ```vue
  const User = {
  template : "<div>User{{$route.params.id}}</div>"
  }
  ```

* #### 监听`$route `对象改变的时候可以使用`watch:{}`

  ```vue
  watch : {
  	"$route" : function () {}
  }
  ```

* #### 嵌套路由：

  实际生活中的应用界面，通常由多层嵌套的组件组合而成。同样的，URL中个段的动态路径也是按某种结构，对应嵌套的个层组件

  接着上节创建的app

  ```vue
  <div id="app">
    <router-view></router-view>
  </div>
  const User = {
    template: '<div>User {{ $route.params.id }}</div>'
  }
  
  const router = new VueRouter({
    routes: [
      { path: '/user/:id', component: User }
    ]
  })
  ```

  这里的`<router-view></router-view>`是最顶层的出口，渲染最高级路由匹配到的组件。同样的，一个被渲染组件同样可以包含自己的嵌套`<router-view>`。例如，在User组件的模版中添加一个`<router-view>`

  ```vue
  const User = {
    template: `
      <div class="user">
        <h2>User {{ $route.params.id }}</h2>
        <router-view></router-view>
      </div>
    `
  }
  ```

  要在嵌套的出口中渲染组件，需要在`VueRouter`的参数中使用`children`配置

  ```vue
  const router = new VueRouter({
    routes: [
      { path: '/user/:id', component: User,
        children: [
          {
            // 当 /user/:id/profile 匹配成功，
            // UserProfile 会被渲染在 User 的 <router-view> 中
            path: 'profile',
            component: UserProfile
          },
          {
            // 当 /user/:id/posts 匹配成功
            // UserPosts 会被渲染在 User 的 <router-view> 中
            path: 'posts',
            component: UserPosts
          }
        ]
      }
    ]
  })
  ```

  #### 注意，使用`children`设置子路由的`path`路径的时候是不带`/`的，记住

* #### 编程式的导航

  除了使用`<router-link>`创建a标签来定义导航链接，我们还可以借助router的实例方法，通过编写代码来实现。

  * `router.push()`

    注意，在vue实例内部，你可以通过`$router`访问路由实例，因此你是可以调用`this.$router.push`

    想要导航到不同的URL，则使用`router.push`方法，这个方法会向`history`栈添加一个新的记录，所以，当用户点击浏览器后退的按钮的时候，则会回到之前的URL。

    当你点你`<router-link>`时，这个方法会在内部调用，所以说，点击`<router-link :to="...">`等同于调用`router.push`。

    该方法的参数可以是一个字符串路径，或者一个描述地址的对象。

    ```vue
    //字符串
            router.push("home");
    
            //对象
            router.push({
                path : "home",
            })
    
            //命名的路由
            router.push({
                name : "user",
                params : {userId : "123"}
            })
    
            //带查询参数，变成/register?plan=private
            router.push({
                path : "register",
                query : {plan:"private"}
            })
    ```

    注意：如果是提供了`path`,`params`则会被忽略，上述例子中的`query`并不属于这种情况，取而代之的下面的这些做法，你需要提供路由的`name`或者手写完整的带有参数的`path`:
    
    ```js
    const userId = '123'
    router.push({ name: 'user', params: { userId }}) // -> /user/123
    router.push({ path: `/user/${userId}` }) // -> /user/123
    // 这里的 params 不生效
    router.push({ path: '/user', params: { userId }}) // -> /user
    ```
    
    ## `router.go(n)`
    
    这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 `window.history.go(n)`
    
    例子
    
    ```js
    // 在浏览器记录中前进一步，等同于 history.forward()
    router.go(1)
    
    // 后退一步记录，等同于 history.back()
    router.go(-1)
    
    // 前进 3 步记录
    router.go(3)
    
    // 如果 history 记录不够用，那就默默地失败呗
    router.go(-100)
    router.go(100)
    ```
    
    #### `命名路由`
    
    ***
    
    有时候通过一个名称来标识一个路由显得更加方便一些，特别是在链接一个路由的时候，或者是在执行一些跳转的时候。你可以在创建Roter实例的时候，在`routes`配置中给某个路由设置名称
    
    ```js
    const router = new VueRouter({
      routes: [
        {
          path: '/user/:userId',
          name: 'user',
          component: User
        }
      ]
    })
    ```
    
    要链接到一个命名路由，可以给`<router-link>`中的`to`属性传一个对象
    
    ```js
    <router-link :to="{name:'user',params:{userId:123}}"></router-link>
    ```
    
    这跟代码调用 `router.push()` 是一回事：
    
    ```js
    router.push({ name: 'user', params: { userId: 123 }})
    ```
    
  * #### 命名视图

    ***

    有时候想同时 (同级) 展示多个视图，而不是嵌套展示，例如创建一个布局，有 `sidebar` (侧导航) 和 `main` (主内容) 两个视图，这个时候命名视图就派上用场了。你可以在界面中拥有多个单独命名的视图，而不是只有一个单独的出口。如果 `router-view` 没有设置名字，那么默认为 `default`。

    ```html
    <router-view class="view one"></router-view>
    <router-view class="view two" name="a"></router-view>
    <router-view class="view three" name="b"></router-view>
    ```

    一个视图使用一个组件渲染，因此对于同个路由，多个视图就需要多个组件。确保正确使用 `components` 配置 (带上 s)：

    ```js
    const router = new VueRouter({
      routes: [
        {
          path: '/',
          components: {
            default: Foo,
            a: Bar,
            b: Baz
          }
        }
      ]
    })
    ```

  * #### 重定向和别名

    * 重定向

      重定向也是通过 `routes` 配置来完成，下面例子是从 `/a` 重定向到 `/b`：

      ```js
      const router = new VueRouter({
        routes: [
          { path: '/a', redirect: '/b' }
        ]
      })
      ```

      重定向的目标也可以是一个命名的路由：

      ```js
      const router = new VueRouter({
        routes: [
          { path: '/a', redirect: { name: 'foo' }}
        ]
      })
      ```

      甚至是一个方法，动态返回重定向目标：

      ```js
      const router = new VueRouter({
        routes: [
          { path: '/a', redirect: to => {
            // 方法接收 目标路由 作为参数
            // return 重定向的 字符串路径/路径对象
          }}
        ]
      })
      ```

    * 别名

      “重定向”的意思是，当用户访问 `/a`时，URL 将会被替换成 `/b`，然后匹配路由为 `/b`，那么“别名”又是什么呢？

      **`/a` 的别名是 `/b`，意味着，当用户访问 `/b` 时，URL 会保持为 `/b`，但是路由匹配则为 `/a`，就像用户访问 `/a` 一样。**

      上面对应的路由配置为：

      ```js
      const router = new VueRouter({
        routes: [
          { path: '/a', component: A, alias: '/b' }
        ]
      })
      ```

  * #### 路由组件传参

    ***

    在组件中使用`$route`会使之与其对应路由形成高度的耦合(耦合是指两个或两个以上的体系或两种运动形式间通过相互作用而彼此影响以至联合起来的现象)，从而使组件只能在某些特定的URL上使用，限制了其灵活性。

    使用`props`将组件和路由解耦，注意了只有动态路由才能使用路由解耦

    **取代与`$route`的耦合**

    ```js
    const User = {
      template: '<div>User {{ $route.params.id }}</div>'
    }
    const router = new VueRouter({
      routes: [
        { path: '/user/:id', component: User }
      ]
    })
    ```

    **通过 `props` 解耦**

    ```js
    const User = {
      props: ['id'],
      template: '<div>User {{ id }}</div>'
    }
    const router = new VueRouter({
      routes: [
        { path: '/user/:id', component: User, props: true },
    
        // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
        {
          path: '/user/:id',
          components: { default: User, sidebar: Sidebar },
          props: { default: true, sidebar: false }
        }
      ]
    })
    ```

    这样你便可以在任何地方使用该组件，使得该组件更加的容易重用和测试

    * ##### 布尔模式

      如果`props`被设置为`true`,`route.params`将会被设置为组件属性

    * ##### 对象模式

      如果`props`是一个对象，他会被按照原样设置为组件属性。当`props`是静态的时候游泳。

    * ##### 函数模式

      你可以创建一个函数返回`props`。这样你便可以将参数转换成另一种类型，将静态值与基于路由的值结合等等。

      ```js
      const router = new VueRouter({
        routes: [
          { path: '/search', component: SearchUser, props: (route) => ({ query: route.query.q }) }
        ]
      })
      ```

      URL `/search?q=vue` 会将 `{query: 'vue'}` 作为属性传递给 `SearchUser` 组件。

      请尽可能保持 `props` 函数为无状态的，因为它只会在路由发生变化时起作用。如果你需要状态来定义 `props`，请使用包装组件，这样 Vue 才可以对状态变化做出反应。
    
  * 配置404页面

    ```js
    {
      path : "8",
      component : 
    }
    ```

* #### `导航守卫:简单的来说就是路由拦截器`

  ***

  正如其名，`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

  记住**参数或查询的改变并不会触发进入/离开的导航守卫**。你可以通过[观察 `$route` 对象](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html#响应路由参数的变化)来应对这些变化，或使用 `beforeRouteUpdate` 的组件内守卫。

  #### 全局前置守卫

  ***

  你可以使用 `router.beforeEach` 注册一个全局前置守卫：

  ```js
  const router = new VueRouter({ ... })
  
  router.beforeEach((to, from, next) => {
    // ...
  })
  ```

  当一个导航触发时，全局前置守卫按照创建顺序调用。守卫是异步解析执行，此时导航在所有守卫 resolve 完之前一直处于 **等待中**。

  每个守卫方法接收三个参数：

  - **`to: Route`**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)
  - **`from: Route`**: 当前导航正要离开的路由
  - **`next: Function`**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
    - **`next()`**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
    - **`next(false)`**: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
    - **`next('/')` 或者 `next({ path: '/' })`**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
    - **`next(error)`**: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。

  **确保 `next` 函数在任何给定的导航守卫中都被严格调用一次。它可以出现多于一次，但是只能在所有的逻辑路径都不重叠的情况下，否则钩子永远都不会被解析或报错。**这里有一个在用户未能验证身份时重定向到 `/login` 的示例：

  ```js
  // BAD
  router.beforeEach((to, from, next) => {
    if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
    // 如果用户未能验证身份，则 `next` 会被调用两次
    next()
  })
  // GOOD
  router.beforeEach((to, from, next) => {
    if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
    else next()
  })
  ```

  #### 全局解析守卫

  ***

  在 2.5.0+ 你可以用 `router.beforeResolve` 注册一个全局守卫。这和 `router.beforeEach` 类似，区别是在导航被确认之前，**同时在所有组件内守卫和异步路由组件被解析之后**，解析守卫就被调用。

  #### 全局后置钩子

  ***

  你也可以注册全局后置钩子，然而和守卫不同的是，这些钩子不会接受 `next` 函数也不会改变导航本身：

  ```js
  router.afterEach((to, from) => {
    // ...
  })
  ```

  #### 路由独享的守卫

  你可以在路由配置上直接定义 `beforeEnter` 守卫：

  ```js
  const router = new VueRouter({
    routes: [
      {
        path: '/foo',
        component: Foo,
        beforeEnter: (to, from, next) => {
          // ...
        }
      }
    ]
  })
  ```

  这些守卫与全局前置守卫的方法参数是一样的。

  #### 组件内的守卫

  最后，你可以在路由组件内直接定义以下路由导航守卫：

  - `beforeRouteEnter`
  - `beforeRouteUpdate` (2.2 新增)
  - `beforeRouteLeave`

  ```js
  const Foo = {
    template: `...`,
    beforeRouteEnter (to, from, next) {
      // 在渲染该组件的对应路由被 confirm 前调用
      // 不！能！获取组件实例 `this`
      // 因为当守卫执行前，组件实例还没被创建
    },
    beforeRouteUpdate (to, from, next) {
      // 在当前路由改变，但是该组件被复用时调用
      // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
      // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
      // 可以访问组件实例 `this`
    },
    beforeRouteLeave (to, from, next) {
      // 导航离开该组件的对应路由时调用
      // 可以访问组件实例 `this`
    }
  }
  ```

  `beforeRouteEnter` 守卫 **不能** 访问 `this`，因为守卫在导航确认前被调用，因此即将登场的新组件还没被创建。

  不过，你可以通过传一个回调给 `next`来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。

  ```js
  beforeRouteEnter (to, from, next) {
    next(vm => {
      // 通过 `vm` 访问组件实例
    })
  }
  ```

  注意 `beforeRouteEnter` 是支持给 `next` 传递回调的唯一守卫。对于 `beforeRouteUpdate` 和 `beforeRouteLeave` 来说，`this` 已经可用了，所以**不支持**传递回调，因为没有必要了。

  ```js
  beforeRouteUpdate (to, from, next) {
    // just use `this`
    this.name = to.params.name
    next()
  }
  ```

  这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 `next(false)` 来取消。

  ```js
  beforeRouteLeave (to, from, next) {
    const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
    if (answer) {
      next()
    } else {
      next(false)
    }
  }
  ```

  #### 完整的导航解析流程

  1. 导航被触发。
  2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
  3. 调用全局的 `beforeEach` 守卫。
  4. 在重用的组件里调用 `beforeRouteUpdate` 守卫 (2.2+)。
  5. 在路由配置里调用 `beforeEnter`。
  6. 解析异步路由组件。
  7. 在被激活的组件里调用 `beforeRouteEnter`。
  8. 调用全局的 `beforeResolve` 守卫 (2.5+)。
  9. 导航被确认。
  10. 调用全局的 `afterEach` 钩子。
  11. 触发 DOM 更新。
  12. 用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数。

  #### 路由元信息

  定义路由的时候可以配置 `meta` 字段：

  ```js
  const router = new VueRouter({
    routes: [
      {
        path: '/foo',
        component: Foo,
        children: [
          {
            path: 'bar',
            component: Bar,
            // a meta field
            meta: { requiresAuth: true }
          }
        ]
      }
    ]
  })
  ```

  那么如何访问这个 `meta` 字段呢？

  首先，我们称呼 `routes` 配置中的每个路由对象为 **路由记录**。路由记录可以是嵌套的，因此，当一个路由匹配成功后，他可能匹配多个路由记录

  例如，根据上面的路由配置，`/foo/bar` 这个 URL 将会匹配父路由记录以及子路由记录。

  一个路由匹配到的所有路由记录会暴露为 `$route` 对象 (还有在导航守卫中的路由对象) 的 `$route.matched` 数组。因此，我们需要遍历 `$route.matched` 来检查路由记录中的 `meta` 字段。

  下面例子展示在全局导航守卫中检查元字段：

  ```js
  router.beforeEach((to, from, next) => {
    if (to.matched.some(record => record.meta.requiresAuth)) {
      // this route requires auth, check if logged in
      // if not, redirect to login page.
      if (!auth.loggedIn()) {
        next({
          path: '/login',
          query: { redirect: to.fullPath }
        })
      } else {
        next()
      }
    } else {
      next() // 确保一定要调用 next()
    }
  })
  ```

  #### 过渡动效

  `<router-view>` 是基本的动态组件，所以我们可以用 `<transition>` 组件给它添加一些过渡效果：

  ```html
  <transition>
    <router-view></router-view>
  </transition>
  ```

  [Transition 的所有功能](https://cn.vuejs.org/guide/transitions.html) 在这里同样适用。

  #### 单个路由的过渡

  上面的用法会给所有路由设置一样的过渡效果，如果你想让每个路由组件有各自的过渡效果，可以在各路由组件内使用 `<transition>` 并设置不同的 name。

  ```js
  const Foo = {
    template: `
      <transition name="slide">
        <div class="foo">...</div>
      </transition>
    `
  }
  
  const Bar = {
    template: `
      <transition name="fade">
        <div class="bar">...</div>
      </transition>
    `
  }
  ```

  #### 基于路由的动态过渡

  还可以基于当前路由与目标路由的变化关系，动态设置过渡效果：

  ```html
  <!-- 使用动态的 transition name -->
  <transition :name="transitionName">
    <router-view></router-view>
  </transition>
  // 接着在父组件内
  // watch $route 决定使用哪种过渡
  watch: {
    '$route' (to, from) {
      const toDepth = to.path.split('/').length
      const fromDepth = from.path.split('/').length
      this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
    }
  }
  ```

  #### 路由懒加载

  当打包构建应用时，JavaScript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

  结合 Vue 的[异步组件](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#异步组件)和 Webpack 的[代码分割功能](https://doc.webpack-china.org/guides/code-splitting-async/#require-ensure-/)，轻松实现路由组件的懒加载。

  首先，可以将异步组件定义为返回一个 Promise 的工厂函数 (该函数返回的 Promise 应该 resolve 组件本身)：

  ```js
  const Foo = () => Promise.resolve({ /* 组件定义对象 */ })
  ```

  第二，在 Webpack 2 中，我们可以使用[动态 import](https://github.com/tc39/proposal-dynamic-import)语法来定义代码分块点 (split point)：

  ```js
  import('./Foo.vue') // 返回 Promise
  ```

  ES 提出的import方法，（**------****最常用------）**

  　　　　方法如下：const HelloWorld = （）=>import('需要加载的模块地址')

  　　　　（不加 { } ，表示直接return）

  组件懒加载和这个也是一样的

  ```js
  import Vue from 'vue'
  import Router from 'vue-router'
  
  Vue.use(Router)
  
  const HelloWorld = ()=>import("@/components/HelloWorld")
  export default new Router({
    routes: [
      {
        path: '/',
        name: 'HelloWorld',
        component:HelloWorld
      }
    ]
  })
  ```

  注意

  如果您使用的是 Babel，你将需要添加 [`syntax-dynamic-import`](https://babeljs.io/docs/plugins/syntax-dynamic-import/) 插件，才能使 Babel 可以正确地解析语法。

  结合这两者，这就是如何定义一个能够被 Webpack 自动代码分割的异步组件。

  ```js
  const Foo = () => import('./Foo.vue')
  ```

  在路由配置中什么都不需要改变，只需要像往常一样使用 `Foo`：

  ```js
  const router = new VueRouter({
    routes: [
      { path: '/foo', component: Foo }
    ]
  })
  ```

  #### 把组件按组分块

  有时候我们想把某个路由下的所有组件都打包在同个异步块 (chunk) 中。只需要使用 [命名 chunk](https://webpack.js.org/guides/code-splitting-require/#chunkname)，一个特殊的注释语法来提供 chunk name (需要 Webpack > 2.4)。

  ```js
  const Foo = () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
  const Bar = () => import(/* webpackChunkName: "group-foo" */ './Bar.vue')
  const Baz = () => import(/* webpackChunkName: "group-foo" */ './Baz.vue')
  ```

  Webpack 会将任何一个异步模块与相同的块名称组合到相同的异步块中。





#### Vuex

#### Vuex 是什么？

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 [devtools extension](https://github.com/vuejs/vue-devtools)，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

#### 什么是“状态管理模式”？,就是将多个组件需要共享的数据，抽离出来，对她进行管理

让我们从一个简单的 Vue 计数应用开始：

```js
new Vue({
  // state
  data () {
    return {
      count: 0
    }
  },
  // view
  template: `
    <div>{{ count }}</div>
  `,
  // actions
  methods: {
    increment () {
      this.count++
    }
  }
})
```

这个状态自管理应用包含以下几个部分：

- **state**，驱动应用的数据源；
- **view**，以声明方式将 **state** 映射到视图；
- **actions**，响应在 **view** 上的用户输入导致的状态变化。

什么时候用VueX，就是你的组件有很多的时候，大量的数据需要共享的时候使用VueX，如果就是那么一两个页面的话，就不用使用VueX了

[安装](https://vuex.vuejs.org/zh/installation.html) Vuex 之后，让我们来创建一个 store。创建过程直截了当——仅需要提供一个初始 state 对象和一些 mutation：

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

现在，你可以通过 `store.state` 来获取状态对象，以及通过 `store.commit` 方法触发状态变更：

```js
store.commit('increment')

console.log(store.state.count) // -> 1
```

为了在 Vue 组件中访问 `this.$store` property，你需要为 Vue 实例提供创建好的 store。Vuex 提供了一个从根组件向所有子组件，以 `store` 选项的方式“注入”该 store 的机制：

```js
new Vue({
  el: '#app',
  store: store,
})
```

提示

如果使用 ES6，你也可以以 ES6 对象的 property 简写 (用在对象某个 property 的 key 和被传入的变量同名时)：

```js
new Vue({
  el: '#app',
  store
})
```

现在我们可以从组件的方法提交一个变更：

```js
methods: {
  increment() {
    this.$store.commit('increment')//使用commit来触发事件，commit还可以传递一个val参数
    console.log(this.$store.state.count)
  }
}
```

再次强调，我们通过提交 mutation 的方式，而非直接改变 `store.state.count`，是因为我们想要更明确地追踪到状态的变化。这个简单的约定能够让你的意图更加明显，这样你在阅读代码的时候能更容易地解读应用内部的状态改变。此外，这样也让我们有机会去实现一些能记录每次状态改变，保存状态快照的调试工具。有了它，我们甚至可以实现如时间穿梭般的调试体验。

由于 store 中的状态是响应式的，在组件中调用 store 中的状态简单到仅需要在计算属性中返回即可。触发变化也仅仅是在组件的 methods 中提交 mutation。

**建议：可以将想要用到的全局state数据，放置到组件的computed内部使用，v-model的内容将其获取和设置分开来**

#### mapState辅助函数

当一个组件需要获取多个状态的时候，将这些状态都声明为计算属性会有些重复和冗余。为了解决这个问题，我们可以使用`mapState`辅助函数帮我们生成计算属性，让你少按几次复制粘贴

```js
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'//但是首先要导入vuex

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

#### Getter

[在 scrimba 上尝试这节课](https://scrimba.com/p/pnyzgAP/c2Be7TB)

有时候我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数：

```js
computed: {
  doneTodosCount () {
    return this.$store.state.todos.filter(todo => todo.done).length
  }
}
```

如果有多个组件需要用到此属性，我们要么复制这个函数，或者抽取到一个共享函数然后在多处导入它——无论哪种方式都不是很理想。

Vuex 允许我们在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

Getter 接受 state 作为其第一个参数：

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

#### 通过属性访问

Getter 会暴露为 `store.getters` 对象，你可以以属性的形式访问这些值：

```js
store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]
```

Getter 也可以接受其他 getter 作为第二个参数：

```js
getters: {
  // ...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
store.getters.doneTodosCount // -> 1
```

我们可以很容易地在任何组件中使用它：

```js
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```

注意，getter 在通过属性访问时是作为 Vue 的响应式系统的一部分缓存其中的。

#### 通过方法访问

你也可以通过让 getter 返回一个函数，来实现给 getter 传参。在你对 store 里的数组进行查询时非常有用。

```js
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```

注意，getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果。

#### `mapGetters` 辅助函数

`mapGetters` 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：

```js
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```

如果你想将一个 getter 属性另取一个名字，使用对象形式：

```js
...mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```

#### Mutation：注意了Mutation是没有异步的，它只能是同步的，简单的来说就是用来修改状态的

[在 Scrimba 上尝试这节课](https://scrimba.com/p/pnyzgAP/ckMZp4HN)

更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 **事件类型 (type)** 和 一个 **回调函数 (handler)**。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数：

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
```

你不能直接调用一个 mutation handler。这个选项更像是事件注册：“当触发一个类型为 `increment` 的 mutation 时，调用此函数。”要唤醒一个 mutation handler，你需要以相应的 type 调用 **store.commit** 方法：

```js
store.commit('increment')
```

#### 提交载荷（Payload）

你可以向 `store.commit` 传入额外的参数，即 mutation 的 **载荷（payload）**：

```js
// ...
mutations: {
  increment (state, n) {
    state.count += n
  }
}
store.commit('increment', 10)
```

在大多数情况下，载荷应该是一个对象，这样可以包含多个字段并且记录的 mutation 会更易读：

```js
// ...
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
store.commit('increment', {
  amount: 10
})
```

#### 对象风格的提交方式

提交 mutation 的另一种方式是直接使用包含 `type` 属性的对象：

```js
store.commit({
  type: 'increment',
  amount: 10
})
```

当使用对象风格的提交方式，整个对象都作为载荷传给 mutation 函数，因此 handler 保持不变：

```js
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

#### Mutation 需遵守 Vue 的响应规则

既然 Vuex 的 store 中的状态是响应式的，那么当我们变更状态时，监视状态的 Vue 组件也会自动更新。这也意味着 Vuex 中的 mutation 也需要与使用 Vue 一样遵守一些注意事项，mutation就是相当于来操作state里面的数据的

1. 最好提前在你的 store 中初始化好所有所需属性。
2. 当需要在对象上添加新属性时，你应该

* 使用 `Vue.set(obj, 'newProp', 123)`, 或者

* 以新对象替换老对象。例如，利用[对象展开运算符](https://github.com/tc39/proposal-object-rest-spread)我们可以这样写：

  ```js
  state.obj = { ...state.obj, newProp: 123 }
  ```

#### 使用常量替代 Mutation 事件类型

使用常量替代 mutation 事件类型在各种 Flux 实现中是很常见的模式。这样可以使 linter 之类的工具发挥作用，同时把这些常量放在单独的文件中可以让你的代码合作者对整个 app 包含的 mutation 一目了然：

```js
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

用不用常量取决于你——在需要多人协作的大型项目中，这会很有帮助。但如果你不喜欢，你完全可以不这样做。

#### Mutation 必须是同步函数，里面不能做Ajax

一条重要的原则就是要记住 **mutation 必须是同步函数**。为什么？请参考下面的例子：

```js
mutations: {
  someMutation (state) {
    api.callAsyncMethod(() => {
      state.count++
    })
  }
}
```

现在想象，我们正在 debug 一个 app 并且观察 devtool 中的 mutation 日志。每一条 mutation 被记录，devtools 都需要捕捉到前一状态和后一状态的快照。然而，在上面的例子中 mutation 中的异步函数中的回调让这不可能完成：因为当 mutation 触发的时候，回调函数还没有被调用，devtools 不知道什么时候回调函数实际上被调用——实质上任何在回调函数中进行的状态的改变都是不可追踪的。

#### 在组件中提交 Mutation

你可以在组件中使用 `this.$store.commit('xxx')` 提交 mutation，或者使用 `mapMutations` 辅助函数将组件中的 methods 映射为 `store.commit` 调用（需要在根节点注入 `store`）。

```js
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```

#### Action

Action 类似于 mutation，不同在于：

* Action 提交的是 mutation，而不是直接变更状态。
* Action 可以包含任意异步操作。

让我们来注册一个简单的 action：

```js
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```

Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 `context.commit` 提交一个 mutation，或者通过 `context.state` 和 `context.getters` 来获取 state 和 getters。当我们在之后介绍到 [Modules](https://vuex.vuejs.org/zh/guide/modules.html) 时，你就知道 context 对象为什么不是 store 实例本身了。

实践中，我们会经常用到 ES2015 的 [参数解构](https://github.com/lukehoban/es6features#destructuring) 来简化代码（特别是我们需要调用 `commit` 很多次的时候）：

```js
actions: {
  increment ({ commit }) {
    commit('increment')
  }
}
```

#### 分发 Action

Action 通过 `store.dispatch` 方法触发：

```js
store.dispatch('increment')
```

乍一眼看上去感觉多此一举，我们直接分发 mutation 岂不更方便？实际上并非如此，还记得 **mutation 必须同步执行**这个限制么？Action 就不受约束！我们可以在 action 内部执行**异步**操作：

```js
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```

Actions 支持同样的载荷方式和对象方式进行分发：

```js
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

来看一个更加实际的购物车示例，涉及到**调用异步 API** 和**分发多重 mutation**：

```js
actions: {
  checkout ({ commit, state }, products) {
    // 把当前购物车的物品备份起来
    const savedCartItems = [...state.cart.added]
    // 发出结账请求，然后乐观地清空购物车
    commit(types.CHECKOUT_REQUEST)
    // 购物 API 接受一个成功回调和一个失败回调
    shop.buyProducts(
      products,
      // 成功操作
      () => commit(types.CHECKOUT_SUCCESS),
      // 失败操作
      () => commit(types.CHECKOUT_FAILURE, savedCartItems)
    )
  }
}
```

注意我们正在进行一系列的异步操作，并且通过提交 mutation 来记录 action 产生的副作用（即状态变更）。

#### 在组件中分发 Action

你在组件中使用 `this.$store.dispatch('xxx')` 分发 action，或者使用 `mapActions` 辅助函数将组件的 methods 映射为 `store.dispatch` 调用（需要先在根节点注入 `store`）：

```js
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

#### 组合 Action

Action 通常是异步的，那么如何知道 action 什么时候结束呢？更重要的是，我们如何才能组合多个 action，以处理更加复杂的异步流程？

首先，你需要明白 `store.dispatch` 可以处理被触发的 action 的处理函数返回的 Promise，并且 `store.dispatch` 仍旧返回 Promise：

```js
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
```

现在你可以：

```js
store.dispatch('actionA').then(() => {
  // ...
})
```

在另外一个 action 中也可以：

```js
actions: {
  // ...
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
      commit('someOtherMutation')
    })
  }
}
```

最后，如果我们利用 [async / await](https://tc39.github.io/ecmascript-asyncawait/)，我们可以如下组合 action：

```js
// 假设 getData() 和 getOtherData() 返回的是 Promise

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
```

> 一个 `store.dispatch` 在不同模块中可以触发多个 action 函数。在这种情况下，只有当所有触发函数完成后，返回的 Promise 才会执行。****

#### Module

***

由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。

为了解决以上问题，Vuex 允许我们将 store 分割成**模块（module）**。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：

```js
const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

#### 模块的局部状态

对于模块内部的 mutation 和 getter，接收的第一个参数是**模块的局部状态对象**。

```js
const moduleA = {
  state: () => ({
    count: 0
  }),
  mutations: {
    increment (state) {
      // 这里的 `state` 对象是模块的局部状态
      state.count++
    }
  },

  getters: {
    doubleCount (state) {
      return state.count * 2
    }
  }
}
```

同样，对于模块内部的 action，局部状态通过 `context.state` 暴露出来，根节点状态则为 `context.rootState`：

```js
const moduleA = {
  // ...
  actions: {
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
  }
}
```

对于模块内部的 getter，根节点状态会作为第三个参数暴露出来：

```js
const moduleA = {
  // ...
  getters: {
    sumWithRootCount (state, getters, rootState) {
      return state.count + rootState.count
    }
  }
}
```

### 命名空间

默认情况下，模块内部的 action、mutation 和 getter 是注册在**全局命名空间**的——这样使得多个模块能够对同一 mutation 或 action 作出响应。

如果希望你的模块具有更高的封装度和复用性，你可以通过添加 `namespaced: true` 的方式使其成为带命名空间的模块。当模块被注册后，它的所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名。例如：

```js
const store = new Vuex.Store({
  modules: {
    account: {
      namespaced: true,

      // 模块内容（module assets）
      state: () => ({ ... }), // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
      getters: {
        isAdmin () { ... } // -> getters['account/isAdmin']
      },
      actions: {
        login () { ... } // -> dispatch('account/login')
      },
      mutations: {
        login () { ... } // -> commit('account/login')
      },

      // 嵌套模块
      modules: {
        // 继承父模块的命名空间
        myPage: {
          state: () => ({ ... }),
          getters: {
            profile () { ... } // -> getters['account/profile']
          }
        },

        // 进一步嵌套命名空间
        posts: {
          namespaced: true,

          state: () => ({ ... }),
          getters: {
            popular () { ... } // -> getters['account/posts/popular']
          }
        }
      }
    }
  }
})
```

启用了命名空间的 getter 和 action 会收到局部化的 `getter`，`dispatch` 和 `commit`。换言之，你在使用模块内容（module assets）时不需要在同一模块内额外添加空间名前缀。更改 `namespaced` 属性后不需要修改模块内的代码。

#### 在带命名空间的模块内访问全局内容（Global Assets）

如果你希望使用全局 state 和 getter，`rootState` 和 `rootGetters` 会作为第三和第四参数传入 getter，也会通过 `context` 对象的属性传入 action。

若需要在全局命名空间内分发 action 或提交 mutation，将 `{ root: true }` 作为第三参数传给 `dispatch` 或 `commit` 即可。

```js
modules: {
  foo: {
    namespaced: true,

    getters: {
      // 在这个模块的 getter 中，`getters` 被局部化了
      // 你可以使用 getter 的第四个参数来调用 `rootGetters`
      someGetter (state, getters, rootState, rootGetters) {
        getters.someOtherGetter // -> 'foo/someOtherGetter'
        rootGetters.someOtherGetter // -> 'someOtherGetter'
      },
      someOtherGetter: state => { ... }
    },

    actions: {
      // 在这个模块中， dispatch 和 commit 也被局部化了
      // 他们可以接受 `root` 属性以访问根 dispatch 或 commit
      someAction ({ dispatch, commit, getters, rootGetters }) {
        getters.someGetter // -> 'foo/someGetter'
        rootGetters.someGetter // -> 'someGetter'

        dispatch('someOtherAction') // -> 'foo/someOtherAction'
        dispatch('someOtherAction', null, { root: true }) // -> 'someOtherAction'

        commit('someMutation') // -> 'foo/someMutation'
        commit('someMutation', null, { root: true }) // -> 'someMutation'
      },
      someOtherAction (ctx, payload) { ... }
    }
  }
}
```

#### 在带命名空间的模块注册全局 action

若需要在带命名空间的模块注册全局 action，你可添加 `root: true`，并将这个 action 的定义放在函数 `handler` 中。例如：

```js
{
  actions: {
    someOtherAction ({dispatch}) {
      dispatch('someAction')
    }
  },
  modules: {
    foo: {
      namespaced: true,

      actions: {
        someAction: {
          root: true,
          handler (namespacedContext, payload) { ... } // -> 'someAction'
        }
      }
    }
  }
}
```

#### 带命名空间的绑定函数

当使用 `mapState`, `mapGetters`, `mapActions` 和 `mapMutations` 这些函数来绑定带命名空间的模块时，写起来可能比较繁琐：

```js
computed: {
  ...mapState({
    a: state => state.some.nested.module.a,
    b: state => state.some.nested.module.b
  })
},
methods: {
  ...mapActions([
    'some/nested/module/foo', // -> this['some/nested/module/foo']()
    'some/nested/module/bar' // -> this['some/nested/module/bar']()
  ])
}
```

对于这种情况，你可以将模块的空间名称字符串作为第一个参数传递给上述函数，这样所有绑定都会自动将该模块作为上下文。于是上面的例子可以简化为：

```js
computed: {
  ...mapState('some/nested/module', {
    a: state => state.a,
    b: state => state.b
  })
},
methods: {
  ...mapActions('some/nested/module', [
    'foo', // -> this.foo()
    'bar' // -> this.bar()
  ])
}
```

而且，你可以通过使用 `createNamespacedHelpers` 创建基于某个命名空间辅助函数。它返回一个对象，对象里有新的绑定在给定命名空间值上的组件绑定辅助函数：

```js
import { createNamespacedHelpers } from 'vuex'

const { mapState, mapActions } = createNamespacedHelpers('some/nested/module')

export default {
  computed: {
    // 在 `some/nested/module` 中查找
    ...mapState({
      a: state => state.a,
      b: state => state.b
    })
  },
  methods: {
    // 在 `some/nested/module` 中查找
    ...mapActions([
      'foo',
      'bar'
    ])
  }
}
```

#### 给插件开发者的注意事项

如果你开发的[插件（Plugin）](https://vuex.vuejs.org/zh/guide/plugins.html)提供了模块并允许用户将其添加到 Vuex store，可能需要考虑模块的空间名称问题。对于这种情况，你可以通过插件的参数对象来允许用户指定空间名称：

```js
// 通过插件的参数对象得到空间名称
// 然后返回 Vuex 插件函数
export function createPlugin (options = {}) {
  return function (store) {
    // 把空间名字添加到插件模块的类型（type）中去
    const namespace = options.namespace || ''
    store.dispatch(namespace + 'pluginAction')
  }
}
```

#### 模块动态注册

在 store 创建**之后**，你可以使用 `store.registerModule` 方法注册模块：

```js
import Vuex from 'vuex'

const store = new Vuex.Store({ /* 选项 */ })

// 注册模块 `myModule`
store.registerModule('myModule', {
  // ...
})
// 注册嵌套模块 `nested/myModule`
store.registerModule(['nested', 'myModule'], {
  // ...
})
```

之后就可以通过 `store.state.myModule` 和 `store.state.nested.myModule` 访问模块的状态。

模块动态注册功能使得其他 Vue 插件可以通过在 store 中附加新模块的方式来使用 Vuex 管理状态。例如，[`vuex-router-sync`](https://github.com/vuejs/vuex-router-sync) 插件就是通过动态注册模块将 vue-router 和 vuex 结合在一起，实现应用的路由状态管理。

你也可以使用 `store.unregisterModule(moduleName)` 来动态卸载模块。注意，你不能使用此方法卸载静态模块（即创建 store 时声明的模块）。

注意，你可以通过 `store.hasModule(moduleName)` 方法检查该模块是否已经被注册到 store。

#### 保留 state

在注册一个新 module 时，你很有可能想保留过去的 state，例如从一个服务端渲染的应用保留 state。你可以通过 `preserveState` 选项将其归档：`store.registerModule('a', module, { preserveState: true })`。

当你设置 `preserveState: true` 时，该模块会被注册，action、mutation 和 getter 会被添加到 store 中，但是 state 不会。这里假设 store 的 state 已经包含了这个 module 的 state 并且你不希望将其覆写。

#### 模块重用

有时我们可能需要创建一个模块的多个实例，例如：

- 创建多个 store，他们公用同一个模块 (例如当 `runInNewContext` 选项是 `false` 或 `'once'` 时，为了[在服务端渲染中避免有状态的单例](https://ssr.vuejs.org/en/structure.html#avoid-stateful-singletons))
- 在一个 store 中多次注册同一个模块

如果我们使用一个纯对象来声明模块的状态，那么这个状态对象会通过引用被共享，导致状态对象被修改时 store 或模块间数据互相污染的问题。

实际上这和 Vue 组件内的 `data` 是同样的问题。因此解决办法也是相同的——使用一个函数来声明模块状态（仅 2.3.0+ 支持）：

```js
const MyReusableModule = {
  state: () => ({
    foo: 'bar'
  }),
  // mutation, action 和 getter 等等...
}
```









#### 混入

***

##### [基础](https://cn.vuejs.org/v2/guide/mixins.html#基础)

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

例子：

```
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// 定义一个使用混入对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

##### [选项合并](https://cn.vuejs.org/v2/guide/mixins.html#选项合并)

当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。

比如，数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。

```
var mixin = {
  data: function () {
    return {
      message: 'hello',
      foo: 'abc'
    }
  }
}

new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created: function () {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
})
```

同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子**之前**调用。

```
var mixin = {
  created: function () {
    console.log('混入对象的钩子被调用')
  }
}

new Vue({
  mixins: [mixin],
  created: function () {
    console.log('组件钩子被调用')
  }
})

// => "混入对象的钩子被调用"
// => "组件钩子被调用"
```

值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。

```
var mixin = {
  methods: {
    foo: function () {
      console.log('foo')
    },
    conflicting: function () {
      console.log('from mixin')
    }
  }
}

var vm = new Vue({
  mixins: [mixin],
  methods: {
    bar: function () {
      console.log('bar')
    },
    conflicting: function () {
      console.log('from self')
    }
  }
})

vm.foo() // => "foo"
vm.bar() // => "bar"
vm.conflicting() // => "from self"
```

注意：`Vue.extend()` 也使用同样的策略进行合并。

##### [全局混入](https://cn.vuejs.org/v2/guide/mixins.html#全局混入)

混入也可以进行全局注册。使用时格外小心！一旦使用全局混入，它将影响**每一个**之后创建的 Vue 实例。使用恰当时，这可以用来为自定义选项注入处理逻辑。

```
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
})

new Vue({
  myOption: 'hello!'
})
// => "hello!"
```

请谨慎使用全局混入，因为它会影响每个单独创建的 Vue 实例 (包括第三方组件)。大多数情况下，只应当应用于自定义选项，就像上面示例一样。推荐将其作为[插件](https://cn.vuejs.org/v2/guide/plugins.html)发布，以避免重复应用混入。

##### [自定义选项合并策略](https://cn.vuejs.org/v2/guide/mixins.html#自定义选项合并策略)

自定义选项将使用默认策略，即简单地覆盖已有值。如果想让自定义选项以自定义逻辑合并，可以向 `Vue.config.optionMergeStrategies` 添加一个函数：

```
Vue.config.optionMergeStrategies.myOption = function (toVal, fromVal) {
  // 返回合并后的值
}
```

对于多数值为对象的选项，可以使用与 `methods` 相同的合并策略：

```
var strategies = Vue.config.optionMergeStrategies
strategies.myOption = strategies.methods
```

可以在 [Vuex](https://github.com/vuejs/vuex) 1.x 的混入策略里找到一个更高级的例子：

```
const merge = Vue.config.optionMergeStrategies.computed
Vue.config.optionMergeStrategies.vuex = function (toVal, fromVal) {
  if (!toVal) return fromVal
  if (!fromVal) return toVal
  return {
    getters: merge(toVal.getters, fromVal.getters),
    state: merge(toVal.state, fromVal.state),
    actions: merge(toVal.actions, fromVal.actions)
  }
}
```







#### 自定义指令

除了核心功能默认内置的指令 (`v-model` 和 `v-show`)，Vue 也允许注册自定义指令。注意，在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。举个聚焦输入框的例子，如下：

当页面加载时，该元素将获得焦点 (注意：`autofocus` 在移动版 Safari 上不工作)。事实上，只要你在打开这个页面后还没点击过任何内容，这个输入框就应当还是处于聚焦状态。现在让我们用指令来实现这个功能：

```js
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    //el就是当前插入的DOM元素
    // 聚焦元素
    el.focus()
  }
})
```

如果想注册局部指令，组件中也接受一个 `directives` 的选项：

```js
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```

然后你可以在模板中任何元素上使用新的 `v-focus` property，如下：

```html
<input v-focus>
```

##### [钩子函数](https://cn.vuejs.org/v2/guide/custom-directive.html#钩子函数)

一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

我们会在[稍后](https://cn.vuejs.org/v2/guide/render-function.html#虚拟-DOM)讨论[渲染函数](https://cn.vuejs.org/v2/guide/render-function.html)时介绍更多 VNodes 的细节。

- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

接下来我们来看一下钩子函数的参数 (即 `el`、`binding`、`vnode` 和 `oldVnode`)。

##### [钩子函数参数](https://cn.vuejs.org/v2/guide/custom-directive.html#钩子函数参数)

指令钩子函数会被传入以下参数：

- `el`：指令所绑定的元素，可以用来直接操作 DOM。

- ```
  binding
  ```

  ：一个对象，包含以下 property：

  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。

- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

除了 `el` 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 [`dataset`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/dataset) 来进行。

这是一个使用了这些 property 的自定义钩子样例：

```
<div id="hook-arguments-example" v-demo:foo.a.b="message"></div>
Vue.directive('demo', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +
      'value: '      + s(binding.value) + '<br>' +
      'expression: ' + s(binding.expression) + '<br>' +
      'argument: '   + s(binding.arg) + '<br>' +
      'modifiers: '  + s(binding.modifiers) + '<br>' +
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})

new Vue({
  el: '#hook-arguments-example',
  data: {
    message: 'hello!'
  }
})
```

name: "demo"
value: "hello!"
expression: "message"
argument: "foo"
modifiers: {"a":true,"b":true}
vnode keys: tag, data, children, text, elm, ns, context, fnContext, fnOptions, fnScopeId, key, componentOptions, componentInstance, parent, raw, isStatic, isRootInsert, isComment, isCloned, isOnce, asyncFactory, asyncMeta, isAsyncPlaceholder

##### [动态指令参数](https://cn.vuejs.org/v2/guide/custom-directive.html#动态指令参数)

指令的参数可以是动态的。例如，在 `v-mydirective:[argument]="value"` 中，`argument` 参数可以根据组件实例数据进行更新！这使得自定义指令可以在应用中被灵活使用。

例如你想要创建一个自定义指令，用来通过固定布局将元素固定在页面上。我们可以像这样创建一个通过指令值来更新竖直位置像素值的自定义指令：

```
<div id="baseexample">
  <p>Scroll down the page</p>
  <p v-pin="200">Stick me 200px from the top of the page</p>
</div>
Vue.directive('pin', {
  bind: function (el, binding, vnode) {
    el.style.position = 'fixed'
    el.style.top = binding.value + 'px'
  }
})

new Vue({
  el: '#baseexample'
})
```

这会把该元素固定在距离页面顶部 200 像素的位置。但如果场景是我们需要把元素固定在左侧而不是顶部又该怎么办呢？这时使用动态参数就可以非常方便地根据每个组件实例来进行更新。

```
<div id="dynamicexample">
  <h3>Scroll down inside this section ↓</h3>
  <p v-pin:[direction]="200">I am pinned onto the page at 200px to the left.</p>
</div>
Vue.directive('pin', {
  bind: function (el, binding, vnode) {
    el.style.position = 'fixed'
    var s = (binding.arg == 'left' ? 'left' : 'top')
    el.style[s] = binding.value + 'px'
  }
})

new Vue({
  el: '#dynamicexample',
  data: function () {
    return {
      direction: 'left'
    }
  }
})
```

结果：

<iframe height="200" class="demo" scrolling="no" title="Dynamic Directive Arguments" src="https://codepen.io/team/Vue/embed/rgLLzb/?height=300&amp;theme-id=32763&amp;default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" style="border: 1px solid rgb(238, 238, 238); border-radius: 2px; padding: 25px 35px; margin: 1em 0px 40px; user-select: none; overflow-x: auto; color: rgb(48, 68, 85); font-family: &quot;Source Sans Pro&quot;, &quot;Helvetica Neue&quot;, Arial, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-style: initial; text-decoration-color: initial; width: 700px;"></iframe>



这样这个自定义指令现在的灵活性就足以支持一些不同的用例了。

##### [函数简写](https://cn.vuejs.org/v2/guide/custom-directive.html#函数简写)

在很多时候，你可能想在 `bind` 和 `update` 时触发相同行为，而不关心其它的钩子。比如这样写：

```
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```

##### [对象字面量](https://cn.vuejs.org/v2/guide/custom-directive.html#对象字面量)

如果指令需要多个值，可以传入一个 JavaScript 对象字面量。记住，指令函数能够接受所有合法的 JavaScript 表达式。

```
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
Vue.directive('demo', function (el, binding) {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text)  // => "hello!"
})
```







#### 插件

***

插件通常用来为 Vue 添加全局功能。插件的功能范围没有严格的限制——一般有下面几种：

1. 添加全局方法或者 property。如：[vue-custom-element](https://github.com/karol-f/vue-custom-element)
2. 添加全局资源：指令/过滤器/过渡等。如 [vue-touch](https://github.com/vuejs/vue-touch)
3. 通过全局混入来添加一些组件选项。如 [vue-router](https://github.com/vuejs/vue-router)
4. 添加 Vue 实例方法，通过把它们添加到 `Vue.prototype` 上实现。
5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

##### [使用插件](https://cn.vuejs.org/v2/guide/plugins.html#使用插件)

通过全局方法 `Vue.use()` 使用插件。它需要在你调用 `new Vue()` 启动应用之前完成：use就是使用的意思。

```
// 调用 `MyPlugin.install(Vue)`
Vue.use(MyPlugin)

new Vue({
  // ...组件选项
})
```

也可以传入一个可选的选项对象：

```
Vue.use(MyPlugin, { someOption: true })
```

`Vue.use` 会自动阻止多次注册相同插件，届时即使多次调用也只会注册一次该插件。

Vue.js 官方提供的一些插件 (例如 `vue-router`) 在检测到 `Vue` 是可访问的全局变量时会自动调用 `Vue.use()`。然而在像 CommonJS 这样的模块环境中，你应该始终显式地调用 `Vue.use()`：

```
// 用 Browserify 或 webpack 提供的 CommonJS 模块环境时
var Vue = require('vue')
var VueRouter = require('vue-router')

// 不要忘了调用此方法
Vue.use(VueRouter)
```

[awesome-vue](https://github.com/vuejs/awesome-vue#components--libraries) 集合了大量由社区贡献的插件和库。

##### [开发插件](https://cn.vuejs.org/v2/guide/plugins.html#开发插件)

Vue.js 的插件应该暴露一个 `install` 方法。这个方法的第一个参数是 `Vue` 构造器，第二个参数是一个可选的选项对象：当使用Vue.use()的时候就会调用`install`这个方法

```
MyPlugin.install = function (Vue, options) {
  // 1. 添加全局方法或 property
  Vue.myGlobalMethod = function () {
    // 逻辑...
  }

  // 2. 添加全局资源
  Vue.directive('my-directive', {
    bind (el, binding, vnode, oldVnode) {
      // 逻辑...
    }
    ...
  })

  // 3. 注入组件选项
  Vue.mixin({
    created: function () {
      // 逻辑...
    }
    ...
  })

  // 4. 添加实例方法
  Vue.prototype.$myMethod = function (methodOptions) {
    // 逻辑...
  }
}
```