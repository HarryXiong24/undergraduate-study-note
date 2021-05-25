# Vue





![logo](./img/logo.png)





Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。



Vue.js 是世界上主流的渐近式 JavaScript 框架。其生态比较繁荣，且很多组件都由官方进行维护、同步更新。相比 React 虽然第三方组件及支持少一些，但是其各模块之间兼容性良好，不会发生冲突。



## 1. Vue简介



### 1.1 Vue的特性

**Vue是一套用于构建用户界面的渐进式框架,与其它大型框架不同的是,Vue 被设计为可以自底向上逐层应用,Vue拥有以下特性:**

- 组件化思想
- 模板的使用和数据渲染非常灵活，层次结构鲜明
- 简单的语法并能够简单快速构建一个项目
- 轻量级，体积小渲染速度更快
- Vue采用的脚手架工具为vue-cli
- 初期是尤雨溪维护，现在有加入的团队组织个人提供技术一同维护迭代更新
- Vue中指令和组件分得更清晰。指令只封装     DOM 操作,而组件代表一个自给自足的独立单元,都拥有有自己的视图样式和数据逻辑



### 1.2 Vue知识框架

![1](./img/1.png)



### 1.3 开发准备



#### 1.3.1 下载Node.js

 

去Node.js的官网下载最新版的node,需要用到其包管理工具npm ([Node.js官网](https://nodejs.org/en/))



#### 1.3.2 配置淘宝镜像

 

因为npm是国外的,在国内用会特别慢,所以需要先用淘宝的cnpm代替npm

 

在命令行窗口输入  npm install -g cnpm --registry=https://registry.npm.taobao.org  配置淘宝镜像



#### 1.3.3 vue-cli脚手架

 

vue-cli是一个基于vue的构建工具,用于搭建vue项目的环境,有着兼容,方便,快速的优点,能够完全遵循前后端分离的原则,用vue开发单网页项目(SPA)的能力尤其的好

 

**注:**可以不用脚手架(vue-cli)就可以基于 webpack 打包工具 ,webpack最终会把整个项目打包成一个js文件但需要自己进行配置各个版本兼容问题,正因为这样,前端有一个专门的配置工程师





#### 1.3.4 使用vue-cli

 

在命令行窗口输入 cnpm i -g vue-cli **全局安装vue-cli脚手架**

Vue-cli要全局安装

 

**注:**安装完成后可以使用 vue -V 查看是否安装成功



**安装项目文件**

 

先到项目文件夹,打开命令行窗口输入vue init webpack 项目文件夹名(不输入则就是在该文件夹里创建)



**运行项目文件**

 

在项目文件中使用npm run dev运行项目文件



**打包项目**

 

在项目文件夹中运行 npm run build 将项目打包 ,打包后的文件将会保存在该文件的list文件夹中

 

 npm run build --report 生成打包视图，可视化显示所有包在项目中占的大小



 生产环境打包发布

​    npm run build

​    npm install -g serve

​    serve dist

​    

#### 1.3.5 ESLint



说明：

1. ESLint     是一个代码规范检查工具 

2. 它定义了很多特定的规则,     一旦你的代码违背了某一规则,eslint会作出非常有用的提示 

3. 官网:http://eslint.org/ 

4. 基本已替代以前的 JSLint



 ESLint 提供以下支持：

1. ES 

2. JSX 

3. style 检查

4. 自定义错误和提示



ESLint 提供以下几种校验：

1) 语法错误校验 

2) 不重要或丢失的标点符号，如分号

3) 没法运行到的代码块（使用过 WebStorm 的童鞋应该了解） 

4) 未被使用的参数提醒 

5) 确保样式的统一规则，如 sass 或者 less 

6) 检查变量的命名



规则的错误等级有三种：

1) 0：关闭规则。 

2) 1：打开规则，并且作为一个警告（信息打印黄色字体） 

3) 2：打开规则，并且作为一个错误（信息打印红色字体）



相关配置文件

1) eslintrc.js: 全局规则配置文件 'rules':{ 'no-new':1 }

2) 在 js/vue 文件中修改局部规则 /*eslint-disableno-new*/ newVue({ el:'body', components:{App} })

3) eslintignore: 指令检查忽略的文件 *.js *.vue



## 2. Vue实例对象



### 2.1 创建并绑定Vue对象

 

**Vue也是一个构造函数,通过new Vue()可以创建一个Vue对象,通过Vue对象进行对DOM元素以及内部的子孙元素的操作**

```vue
<div id="div">
    {{msg}}<!--显示123-->
</div>
<script>
new Vue({
    el:"#div",
    /*
    在Vue中通过el属性来绑定一个DOM元素,从而让该DOM元素以及内部都绑定Vue的相关操作,一般是通过ID进行查找,因为这样才能够精确绑定
    */
    data:{//data属性中包含着在el中使用的使用的变量或属性
        msg:123
    }
    //也可以使用函数形式的
    data(){
    return{
        msg:123
    };
    //methods属性包含着需要使用的方法
    methods:{
        show(){
            console.log(this.msg);
        }
    }
}
})
</script>

```

**注:在实例内部使用定义的属性或方法时不能直接使用,必须通过this来指定需要用的属性**



### 2.2 vue实例中的参数与选项

 

**el:"#id", //DOM成员（1/3）**

提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。

**template:"`<tag></tag>`", //DOM成员（2/3）**

一个字符串模板作为 Vue 实例的标识使用。模板将会 替换 挂载的元素。挂载元素的内容都将被忽略，除非模板的内容有分发 slot

**render: (h)=>{h(App)}, //DOM成员（3/3）**

字符串模板的代替方案，允许你发挥 JavaScript 最大的编程能力。

```vue
// 原理
render: (h) => {

  return <APP></APP>

}
// 可以代替components和template 
```

**data //数据成员（1/6）**

data():{ return{ } },

Vue实例的数据对象。Vue 将会递归将 data 的属性转换为 getter/setter，从而让 data 的属性能够响应数据变化

**methods //数据成员（2/6）**

methods:{ func(){ } }

methods将被混入到 Vue 实例中，可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用

方法中的 this自动绑定为 Vue 实例

**watch //数据成员（3/6）**

watch:{ key:value $route:function (newValue, oldValue) { //监控路由 } }

整个为一个对象，键是需要观察的表达式，值是对应回调函数

**computed //数据成员（4/6）**

computed:{ getTotalCount(){ const totalCount=0; return totalCount; } },

vue的计算属性，将被混入到 Vue 实例中。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例

**props //数据成员（5/6）**

props:['counts','ids'],

用于父子组件的eventbus传值，是数组或对象，props的成员是子组件接收的来自父组件的数据

**propsData //数据成员（6/6）**

创建实例时传递 props。主要作用是方便测试。基本不使用。

 

**filters //资源（1/3）**

filters('filterName',(input,function(){ return newvalue }))

包含 Vue 实例可用过滤器的哈希表。

**directives //资源（2/3）**

包含 Vue 实例可用指令的哈希表。

**components //资源（3/3）**

（即该组件的子实例）这里是包含 Vue 实例可用组件的哈希表。

 

**name //杂项（1/6）**

允许组件模板递归地调用自身。注意，组件在全局用 Vue.component() 注册时，全局 ID 自动作为组件的 name。

**parent //杂项（2/6）**

指定已创建的实例之父实例，在两者之间建立父子关系。子实例可以用 this.$parent 访问父实例，子实例被推入父实例的 $children 数组中。

**mixins //杂项（3/6）**

mixins 选项接受一个混合对象的数组。Mixin钩子按照传入顺序依次调用,并在调用组件自身的钩子之前被调用。

**extends //杂项（4/6）**

允许声明扩展另一个组件。这主要是为了便于扩展单文件组件。这和 mixins 类似，区别在于，组件自身的选项会比要扩展的源组件具有更高的优先级。

**delimiters //杂项（5/6）**

改变纯文本插入分隔符。

**functional //杂项（6/6）**

使组件无状态（没有 data ）和无实例（没有 this 上下文）。他们用一个简单的 render 函数返回虚拟节点使他们更容易渲染。



### 2.3 常用指令实例

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>startVue</title>
</head>
<body>
    <div id="app">
        <!-- {{}}双大括号表达式，里面是js代码 -->
        <p>{{msg}}</p>
        <!-- 相当于innerText -->
        <p v-text="str"></p>
        <!-- 相当于innerHTML -->
        <p v-html="str"></p>
        <!-- 强制绑定事件, 一般用于用于响应式地更新HTML attribute, 简写方式:
            从 2.6.0 开始，可以用方括号括起来的 JavaScript 表达式作为一个指令的参数
            <a v-bind:[attributeName]="url"> ... </a>
            这里的 attributeName 会被作为一个 JavaScript 表达式进行动态求值,求得的值将会作为最终的参数来使用。
            例如，如果你的 Vue 实例有一个 data 属性 attributeName，其值为 "href"
            那么这个绑定将等价于 v-bind:href
        -->
        <a v-bind:href="url">Baidu</a>
        <!-- 绑定事件监听,监听 DOM 事件, 简写方式@ -->
        <button v-on:click="test">Submit</button>
        <!-- 双向绑定事件,动态实时更新里面的内容 -->
        <div> 
            <input type="text" v-model="input" placeholder="Please input">
            <p>{{input}}</p>
        </div>
    </div>
</body>
<script text="javascript" src="./vue.js"></script>
<script text="javascript">
    const app = new Vue({
        //要挂载的位置  
        //在Vue中通过el属性来绑定一个DOM元素,从而让该DOM元素以及内部都绑定Vue的相关操作
        //一般是通过ID进行查找,因为这样才能够精确绑定
        el: "#app",
        // data属性中包含着在el中使用的使用的变量或属性
        data:{
            msg: 'xhw',
            str: '<a href="#">XHW</a>',
            url: 'https://www.baidu.com',
            input: '',
        },
        /**
         * 也可以写成(以组件形式里必须写成这个)
         * data() {
         *     return {
         *         
         * }
         * },
        */
        
        // methods属性包含着需要使用的方法
        methods: {
            test () {
                alert("!!!");
            }
        }
    });
</script>
</html>

```





### 2.4 vm.$mount



如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用 vm.$mount() 手动地挂载一个未挂载的实例

 

**注意:**这个方法返回实例自身,因而可以链式调用其它实例方法

 

```vue
var MyComponent = Vue.extend({
  template: '<div>Hello!</div>'
 })

// 创建并挂载到 #app (会替换 #app)
 new MyComponent().$mount('#app')

// 同上
 new MyComponent({ el: '#app' })

// 或者，在文档之外渲染并且随后挂载
 var component = new MyComponent().$mount()
 document.getElementById('app').appendChild(component.$el)
```



## 3. 基本指令 



### 3.1 v-text



**v-text,**该指令的用法同原生JS中的innerText,更新绑定元素内部的文本内容



```vue
<div id="div">
<span v-text="msg"></span><!--不会有闪烁问题-->
<!-- 和下面的一样 -->
<span>{{msg}}</span>
</div>
```



### 3.2 v-html



**v-html,**该指令用法同原生JS的innerHTML,可以解析内部的HTML标签



### 3.3 v-cloak



**v-cloak**,该指令CSS一起使用,用于隐藏还没有开始编译的{{}}(插值表达式)直到编译完成,解决其闪烁问题



```vue
[v-cloak] {
  display: none;/*如果没有起作用可能是由于优先级不够导致的,可以加上!important提高优先级*/
}
```



```vue
<div v-cloak>
  {{ message }}
</div>
```



### 3.4 v-show



**v-show,**该指令用于显示和隐藏DOM元素,根据表达式之真假值,切换元素的display属性值



**注意:**



- 当条件变化时该指令触发过渡效果

- v-show指令不支持在< template>< /template>标签上写,也不支持v-else,一般来说,v-if 有更高的切换开销,而 v-show 有更高的初始渲染开销。因此,如果需要非常频繁地切换,则使用 v-show 较好,如果在运行时条件很少改变,则使用 v-if 较好



### 3.5 v-if,v-else与v-else-if



- **v-if,**该指令用于是否渲染DOM元素,传入一个布尔值,通过该布尔值的条件改变实现对于DOM元素的删除和重建,该指令不同于v-show,而是会完全销毁这个DOM元素
  **注意:**当条件变化时该指令触发过渡效果

- v-else,

  该指令用于

  不需要任何表达式

  ,但是在该指令的前一个兄弟元素必须有v-if或者v-else-if指令,该指令的用处是为v-if 或者 v-else-if添加else的选项

  ```vue
  <div v-if="Math.random() > 0.5">
    Now you see me
  </div>
  <div v-else>
    Now you don't
  </div
  ```

  

- v-else-if,

  该指令用于用于v-if的else if选项,前一个兄弟元素必须要v-if指令,并且该指令可以链式调用,也就是说可以调用多次v-else-if指令

  ```vue
  <div v-if="type === 'A'">
    A
  </div>
  <div v-else-if="type === 'B'">
    B
  </div>
  <div v-else-if="type === 'C'">
    C
  </div>
  <div v-else>
    Not A/B/C
  </div>
  ```



### 3.6 v-for



**v-for,**该指令可以基于源数据多次渲染元素或模板块,用于循环遍历某个数组或对象,如果只用一个变量代表得到是数组或对象的value值



**注意:**在内部必须使用固定的i**tem in/of items**形式的特殊语法(下面的in都可以用of代替,并且更符合实际)



```vue
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }} <!--Foo Bar-->
  </li>
</ul>
<script>
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
</script>
```



- 遍历数组时其实还支持第二个变量,代表的是遍历数组的索引值

  ```vue
  <ul id="example-2">
    <li v-for="(item, index) in items">
      {{ parentMessage }} - {{ index }} - {{ item.message }}
      <!--
          Parent-0-Foo
          Parent-1-Bar
      -->
    </li>
  </ul>
  <script>
  var example2 = new Vue({
    el: '#example-2',
    data: {
      parentMessage: 'Parent',
      items: [
        { message: 'Foo' },
        { message: 'Bar' }
      ]
    }
  })
  </script>
  ```

- 遍历对象时还可以接受第二三两个变量,分别代表了键名和索引值

  ```vue
  <ul id="v-for-object" class="demo">
   <div v-for="(value, key, index) in object">
    {{ index }}. {{ key }}: {{ value }}
    <!--
      0. firstName: John
      1. lastName: Doe
      2. age: 30
     -->
  </div>
  </ul>
  <script>
      new Vue({
          el: '#v-for-object',
          data: {
              object: {
                  firstName: 'John',
                  lastName: 'Doe',
                  age: 30
              }
          }
  })
  </script>
  ```

- 该指令还可以遍历一个整数,遍历的量会分别从1开始得到赋值直到到这个整数的值

  ```vue
  <p v-for="count in 10">{{count}}</p>
  //1 2 3 4 5 6 7 8 9 10
  ```



**注意:**当v-for和v-if处于同一节点时,v-for 的优先级比 v-if更高，这意味着 v-if将分别重复运行于每个 v-for循环中,当想为仅有的一些项渲染节点时,这种优先级的机制会十分有用



```vue
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
<!--
官方并不建议v-for和v-if指令一起使用,如果要使用这种方式,就进行条件渲染
-->

<!--
如果想有条件才继续v-for指令,则可以将v-if置于外层元素(或<template>)上
-->
<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>
<!--
条件渲染
v-if如果想只写一个而同时切换多个元素,可以在最外成包裹一层<template></template>标签,在这个标签上面
使用v-if,在渲染的时候并不会将<template>标签渲染出来
-->
```



### 3.7 v-bind



**v-bind**,该指令用于动态绑定一个或多个特性,该方法绑定的特性与普通的属性效果一致,只是其内部会被解析为JS表达式,而不是普通特性一样会是一个字符串



**修辞符:**



- **.prop** - 被用于绑定 DOM 属性(property)

- **.camel** -  将短横线命名法特性名转换为驼峰命名法

- **.sync** - 会扩展成一个更新父组件绑定值的 v-on 侦听器



**注意:**



- 该指令有其简写写法,通过:来代替v-bind:

- 该指令可以动态对绑定的参数进行改变,参数用[]括起来



```vue
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">

<!-- 动态特性名 (2.6.0+) -->
<button v-bind:[key]="value"></button>

<!-- 缩写 -->
<img :src="imageSrc">

<!-- 动态特性名缩写 (2.6.0+) -->
<button :[key]="value"></button>

<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName">

<!-- class 绑定 -->
<div :class="{ red: isRed }"></div><!--对象通过布尔值确定是否传入class中-->
<div :class="[classA, classB]"></div><!--数组会直接将类名传入到class中-->
<div :class="[classA, { classB: isB, classC: isC }]"><!--对象和数组可以混用-->

<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div><!--通过对象写入每个属性-->
<div :style="[styleObjectA, styleObjectB]"></div><!--数组的成员中实际是一个个对象-->

<!-- 绑定一个有属性的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- 通过 prop 修饰符绑定 DOM 属性 -->
<div v-bind:text-content.prop="text"></div>

<!-- prop 绑定。“prop”必须在 my-component 中声明。-->
<my-component :prop="someThing"></my-component>

<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
```



### 3.8 v-on



**v-on**,该指令用于绑定监听事件,表达式可以是一个方法的名字或一个内联语句(也就是说在传入事件的时候可以选择加()可以选择不加(),推荐在传入参数的时候添加,在不传参的时候写事件名)



**参数:**该指令的参数为原生JS中的事件名,只不过没有on



**修饰符**



- **.stop** - 调用 event.stopPropagation(),会阻止本元素上的事件进行冒泡传播

- **.prevent** - 调用 event.preventDefault(),不能和.passive一起使用

- **.capture** - 添加事件侦听器时使用 capture 模式,父元素会执行在子元素上进行的同名事件

- **.self** - 只当事件是从侦听器绑定的元素本身触发时才触发回调,只会真正自己触发的事件才会进行,和.stop是有区别的,这个只会阻止自己的冒泡,但不会阻止该元素的父元素事件的冒泡进行

- **.{keyCode | keyAlias}** - 只当事件是从特定键触发时才触发回调,可以是表示键盘字符的数字或者表示特效事件的按键修饰符

- **.native** - 监听组件根元素的原生事件,一个Vue实例内部通过只能v-on只能绑定自己内部的方法,不能绑定原生DOM事件的方法,通过该修饰符就可以使用原生JS的事件方法了

- **.once** - 只触发一次回调

- .**left** -  只当点击鼠标左键时触发

- **.right** -  只当点击鼠标右键时触发

- **.middle** - 只当点击鼠标中键时触发

- **.passive** - 不用查找是否阻止默认事件的请求直接进行操作。如在滚动页面时的onscroll事件,每次触发事件时浏览器都会查看是否有阻止默认滚动事件的操作,但是如果本来就没有进行这个操作,在滚动的时候就会出现卡的的情况,因为在触发滚动条滚动时总会先查找请求,这个修饰符就是告诉浏览器不用进行查找直接进行滚动操作。因为作用的冲突,所以不能和.prevent一起使用



**注意:**



- 该指令有简写形式,通过@来代替v-on:

- 该指令可以动态对绑定的参数进行改变,参数用[]括起来



```vue
<!-- 方法处理器 -->
<button v-on:click="doThis"></button>

<!-- 动态事件 (2.6.0+) -->
<button v-on:[event]="doThis"></button>

<!-- 内联语句 -->
<button v-on:click="doThat('hello', $event)"></button>

<!-- 缩写 -->
<button @click="doThis"></button>

<!-- 动态事件缩写 (2.6.0+) -->
<button @[event]="doThis"></button>

<!-- 停止冒泡 -->
<button @click.stop="doThis"></button>

<!-- 阻止默认行为 -->
<button @click.prevent="doThis"></button>

<!-- 阻止默认行为，没有表达式 -->
<form @submit.prevent></form>

<!--  串联修饰符 -->
<button @click.stop.prevent="doThis"></button>

<!-- 键修饰符，键别名 -->
<input @keyup.enter="onEnter">

<!-- 键修饰符，键代码 -->
<input @keyup.13="onEnter">

<!-- 点击回调只会触发一次 -->
<button v-on:click.once="doThis"></button>

<!-- 对象语法 (2.4.0+) -->
<button v-on="{ mousedown: doThis, mouseup: doThat }"></button>

<!-- 组件中的自定义事件 -->
<my-component @my-event="handleThis"></my-component>

<!-- 内联语句 -->
<my-component @my-event="handleThis(123, $event)"></my-component>

<!-- 组件中的原生事件 -->
<my-component @click.native="onClick"></my-component>
```



### 3.9 v-model



**v-model**,该指令用于表单内的标签进行双向的数据绑定



**注意:**v-model只能绑定给input,textarea,select等表单元素和自定义的组件中,除此之外不能在其他标签上绑定



**修辞符:**



- **.lazy** - 取代 input监听 change 事件,默认在用户写入值时是使用的input事件,也就是当值输入完成后才会触发事件,而change是一些有输入法的语言在值还没有输入时就时刻监听改变

- **.number**- 输入字符串转为有效的数字

- **.trim** - 输入首尾空格过滤



**用法:**



- **如果是对input文本框和textarea绑定的**,绑定的值会根据输入的内容,就是将内部的变量的值改为value中的值

- **如果是对复选框绑定的**

- - **如果绑定的变量不是数组**,会根据复选框是否被选中而改变为false或true,即使原来不是布尔值也会被强制转换为布尔值,这是因为双向的数据绑定,如果是有多个复选框,那么则会一起被选中或不选中

- - **如果变量是数组**则会将value属性中的值(没有写value属性会传入null)传入该数组作为其中的一个成员,Vue会根据数组内部的值来判断是否选中该复选框(内部其实就是这样运作的),如果value值一样会有多个复选框被选中,再次点击就会将该值删去然后取消复选框的选中

```vue
<div id='example'>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Checked names: {{ checkedNames }}</span>
</div>

<!--也可以在被选中和没被选择直接设置不同的值-->
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no"
>
<!--
 当选中时
vm.toggle === 'yes'
 当没有选中时
vm.toggle === 'no'
注意:点击了才会改变值,如果没有点击过而变量本身有值的话就不会是fasle-value的值
-->
```

- **如果是对单选按钮进行绑定的**,变量值会随着选中单选框的value值而变化,如果变量的值刚开始就是一个单选框的value值,那么就会自动选中这个单选框
  **注意:**

- - 单选框和复选框即使不写相同的name而只绑定了相同的modle也会认做是一类单选框的,但是最好还是将name写上

- - 单选框和复选框都可以通过v-bind:value绑定的value值来设置值自身的value值

- 如果是对选择框select进行绑定的

  ,绑定的变量的值会随着选中的option选项内部的内容而发生变化,如果option没有写value属性,该变量会变成< option>< /option>内部的值,如果有value属性,变量会变成value值而不是option的内容

  ```vue
  <div id="example">
    <select v-model="selected">
      <option disabled value="">请选择</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
  <script>
  new Vue({
    el: '#example',
    data: {
      selected: ''
    }
  })
  </script>
  ```

  注意:

  在s多选时要绑定一个数组,将上方的selected:[]，这样在选入的时候就能将每个选择的选项的值加到变量中去,还可以是一个对象,但是要通过v-bind:value绑定

  ```vue
  <select v-model="selected">
      <!-- 内联对象字面量 -->
    <option v-bind:value="{ number: 123 }">123</option>
  </select>
  ```



### 3.10 v-pre



**该指令不接受任何表达式,使用了该指令的元素Vue在编译时跳过这个元素和它的子元素的编译过程,可以用来显示原始的模板{{}}标签,跳过大量没有指令的节点会加快编译**



### 3.11 v-once



**该指令不需要表达式,只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能**



### 3.12 ref



```vue
// 和react里的ref用法基本一致
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>ref</title>
  <style>
     
  </style>
</head>
<body>
 
  <div id="app">
    <!-- 给需要获取的标签去一个ref属性的别名 -->
    <p ref="content">Hello ref!</p>
    <button @click="get">Get</button>
  </div>
  <script type="text/javascript" src="./vue.js"></script>
  <script type="text/javascript">
    new Vue({
        el: "#app",
        data() {
           return {
           }
        },
        
        methods: {
            get() {
                // 调用this.$refs.xxx获取到相应的标签
                alert(this.$refs.content.innerHTML);
            }
        },
    })
  </script>
</body>
</html>
```



## 4. 计算属性与监视



### 4.1 computed

 

**计算属性computed是用于定义一些可以动态改变的属性的,模板内的表达式非常便利,但是设计它们的初衷是用于简单运算的。**

在模板中放入太多的逻辑会让模板过重且难以维护,所以尽量不要在模板{{}}中使用计算表达式,这时就可以用Vue实例中的computed属性,computed里面的属性的值为一个函数,可以在该函数中间一系列的计算,然后将需要的结果返回

 

```vue
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen'
      },
      methods: {},
      computed: { 
    /*
    计算属性； 特点：当计算属性中所以来的任何一个 data 属性改变之后，都会重新触发 本计算属性 的重新计    算，从而更新 fullName 的值
    */
        fullName() {
          return this.firstName + ' - ' + this.lastName;
        }
      }
    });
  </script>

```

**计算属性默认只有getter,不过在需要时也可以提供一个setter,这时最外层的属性会是一个对象,内部分别有get()方法和set()方法**

```vue
<div id="app">
    <input type="text" v-model="firstName">
    <input type="text" v-model="lastName">
    <!-- 点击按钮重新为 计算属性 fullName 赋值 -->
    <input type="button" value="修改fullName" @click="changeName">
<span>{{fullName}}</span>
</div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
        el: '#app',
        data: {
            firstName: 'jack',
            lastName: 'chen'
        },
        methods: {
            changeName() {
                this.fullName = 'TOM - chen2';
            }
        },
        computed: {
            fullName: {
                get: function () {
                    return this.firstName + ' - ' + this.lastName;
                },
                set: function (newVal) {
                    var parts = newVal.split(' - ');
                    this.firstName = parts[0];
                    this.lastName = parts[1];
                }
            }
        }
    });
</script>


```

**注意:**

- 计算属性本质上就是一个方法,不过只需要将其当做一个属性来用,**在使用这些属性的时候是直接使用它们的名称**,而不是将其当做方法来用,所以**在引用的时候不要在后面加上()**
- **只要计算属性的函数内部所用到的data中的数据发生了变化就会立刻调用该函数,计算属性的值会重新被计算**
- **与方法不同的是computed是有缓存的,意味着只要内部的响应式依赖变量没有发生改变访问的该函数的结果依然不会发生改变**,而如果是方法,每当再次访问方法时都会重新执行一次函数,所以不会有缓存,如果不相同要有缓存,computed就用方法methods来代替



### 4.2 watch

 

**watch属性为Vue实例或组件中的一个自定义的侦听器,通过该属性可以在实例或组件的数据发生变化时进行相应的操作,对于路由这些虚拟DOM的监听是非常好用的**

 

**watch的属性方法里有两个参数**

```
xxx（new, old）{

//第一个参数是新数据，第二个参数是旧数据
//只写一个的时候代表新数据**

}
```

 

- 类型：{ [key: string]: string | Function | Object | Array }
- 详细：
            一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。
- 示例：

```vue
var vm = new Vue({
  data: {
    a: 1,
    b: 2,
    c: 3,
    d: 4,
    e: {
      f: {
        g: 5
      }
    }
  },
  watch: {
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    // 方法名
    b: 'someMethod',
    // 该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
    c: {
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    },
    // 该回调将会在侦听开始之后被立即调用
    d: {
      handler: 'someMethod',
      immediate: true
    },
    e: [
      'handle1',
      function handle2 (val, oldVal) { /* ... */ },
      {
        handler: function handle3 (val, oldVal) { /* ... */ },
        /* ... */
      }
    ],
    // watch vm.e.f's value: {g: 5}
    'e.f': function (val, oldVal) { /* ... */ }
  }
})
vm.a = 2 // => new: 2, old: 1

```

**注意:**

不应该使用箭头函数来定义 watcher 函数 (例如 searchQuery: newValue => this.updateAutocomplete(newValue))。理由是箭头函数绑定了父级作用域的上下文，所以 this 将不会按照期望指向 Vue 实例，this.updateAutocomplete 将是 undefined。



**监听data数据变化** 

```vue
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen',
        fullName: 'jack - chen'
      },
      methods: {},
      watch: {
        'firstName': function (newVal, oldVal) { // 第一个参数是新数据，第二个参数是旧数据
          this.fullName = newVal + ' - ' + this.lastName;
        },
        'lastName': function (newVal, oldVal) {
          this.fullName = this.firstName + ' - ' + newVal;
        }
      }
    });
  </script>
 


```

**监听路由的变化**

```vue
<div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>

	<router-view></router-view>
</div>

<script>
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });

var router = new VueRouter({
      routes: [
        { path: "/login", component: login },
        { path: "/register", component: register }
      ]
    });

// 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router: router,
      watch: {
        '$route': function (newVal, oldVal) {
          if (newVal.path === '/login') {
            console.log('这是登录组件');
          }
        }
      }
    });
  </script>
```





### 4.3 wath,computed与methods的区别

- **computed属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。主要当作属性来使用**
- **methods方法表示一个具体的操作，主要书写业务逻辑**
- **watch一个对象，键是需要观察的表达式，值是对应回调函数。主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作,可以看作是computed和methods的结合体**



### 4.4 实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>startVue</title>
</head>
<body>
    <div id="app">
    
        <div>
            FirstName<input type="text" v-model="firstName" placeholder="Please input">
            LastName<input type="text" v-model="lastName" placeholder="Please input">
            <br>
            FullNameComputed<input type="text" v-model="fullName1">
            <br>
            FullName2Watch<input type="text" v-model="fullName2">
            <br>
            FullNameSet<input type="text" v-model="fullName3">
        </div>
    </div>
</body>
<script text="javascript" src="./vue.js"></script>
<script text="javascript">
    const app = new Vue({
        el: "#app",
        data:{
            firstName: '',
            lastName: '',
            fullName2: '',
        },
        
        // computed当做属性来使用,里面的属性名一般不用写到data中，属性值是一个方法
        computed: {
            fullName1: function() {
                // this就是指app这个Vue的实例对象
                return this.firstName + " " + this.lastName;
            },
            fullName3: {
                // 接受
				// 需要读取当前属性值的时候进行回调
                get() {
                    return this.firstName + " " + this.lastName;
                },
				// 当属性值发生改变的时候进行回调，更新相关数据
                // 更新数据时输出
                set(newValue) {
                    var names = newValue.split(' ')
                    this.firstName = names[0]
                    this.lastName = names[names.length - 1]
                }
            }
        },
        //watch是一个对象,对象里的属性写到data中
        watch: {
            firstName: function(value) {
                this.fullName2 = value + " " + this.lastName;
            },
            lastName: function(value) {
                this.fullName2 = this.firstName + " " + value;
            }
        }
    });
</script>
</html>

```



## 5. 绑定class和style



### 5.1 绑定class



- 通过数组的书写传入

  :class

  形式绑定的类名

  ```vue
  <h1 :class="['red','big']">Vue</h1>
  ```

- 通过对象书写的形式绑定类名,对象中的属性名就是要传入的class名,而属性名对应的属性值为一个布尔值,可以是变量,如果是真就作为一个类名传入class中,如果是假的就不计入class中

  ```vue
  <h1 :class="{red:true,big:true}">Vue</h1>
  ```

  注意:

  传入一个对象的时候完全可以在Vue的实例创建的时候传入变量,直接在class中写入变量名

- 传入三目表达式进行切换是否用该类名的判断

  ```vue
  <h1 :class="['red',isActive?'big':'small']">Vue</h1>
  ```

- 在数组中使用对象,可以使用该方法代替繁琐的三目表达式

  ```vue
  <h1 :class="['red',{big:isActive}]">Vue</h1>
  ```



### 5.2 绑定style



**绑定的style样式可以通过驼峰命名法会短横线分割法进行命名(短横线命名需要在外层用单引号包住)**



- 直接在元素上同过

  :style

  的形式,通过对象的形式书写

  ```vue
  <h1 :style="{color:'red','font-size':'40px'}">Vue</h1>
  ```

- 将样式定义在data中,再引用到

  :style中

  ```vue
  <h1 :style="foo">Vue</h1>
  ```

  ```vue
  data:{
      foo:{color:'red','font-size':'40px'}
  }
  ```

- 在:style中通过数组引用多个data中的样式对象,其实每个对象就相当于一个class,只是需要在data中设置

  ```vue
  <h1 :style="[foo,foo2]">Vue</h1>
  ```

  ```vue
  data:{
      foo:{color:'red','font-size':'40px'},
      foo2:{fontWight:200}//驼峰命名法也可以
  }
  ```



### 5.3 实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>classAndstyle</title>
    <style type="text/css">
        .red {
            color: red;
        }
        .blue {
            color: blue;
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- 一下都是需要动态操作css所采用的方法,如果只是普通的绑定css,则直接原生法绑定即可 -->
        <h2>class绑定</h2>
        <!-- 参数绑定 -->
        <p :class="color">111111</p>
        <!-- 对象绑定,后面的参数为布尔值 -->
        <p :class="{red: isred, blue: isblue}">222222</p>
        <!-- 数组绑定,可接若干个,用''括起 -->
        <p :class="['red']">333333</p>
        <button @click="update(color)">更新</button>

        <h2>style绑定</h2>
        <!-- 对于属性:属性值,可以只有属性,然后再data里写属性值;也可以写好属性:属性值,然后在data里写属性值;
            记住要用驼峰命名法,否则则要用""标注,比如"background-color"
        -->
        <p :style="{color:activeColor, fontSize, backgroundColor: value}">aaaaaa</p>
        <!-- 也可以用数组的形式 -->
        <p :style="[foo,foo2]">bbbbbb</p>
    </div>
</body>
<script text="javascript" src="./vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            color: "red",
            isred: true,
            isblue: false,
            activeColor: "green",
            fontSize: "30px",
            //backgroundColor: "blue",
            value: "blue",
            foo:{color:'red','font-size':'40px'},
            foo2:{fontWight:200},
        },
        methods: {
            update(color) {
                if(color === "blue"){
                    this.color = "red";
                    this.isred = true;
                    this.isblue = false;
                }
                else if(color === "red"){
                    this.color = "blue";
                    this.isred = false;
                    this.isblue = true;
                }
            }
        },
    })
</script>
</html>
```



## 6. Vue基本操作



### 6.1 条件渲染实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ifAndshow</title>
</head>
<body>
    <div id="app">
        <h2>Is a number?</h2>
        <input type="text" placeholder="Input" v-model="value">
        <button @click="check">Check</button>
        <!-- 条件渲染里面可以写表达式 -->
        <p v-if="res === true">True</p>
        <p v-else>False</p>
        <!-- v-show相当于display的切换 -->
        <p v-show="ok">v-show</p>
        <button @click="change">Change</button>
    </div>
</body>
<script text="javascript" src="./vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            value: "",
            res: false,
            ok: "true",
        },
        methods: {
            check() {
                if( isNaN(Number(this.value)) === false) {
                    this.res = true;
                }
                else {
                    this.res = false;
                }
            },
            change() {
                if(this.ok === true){
                    this.ok = false;
                }
                else{
                    this.ok = true;
                }
            }
        },
    })
</script>
</html>

```



### 6.2 列表渲染的实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>for</title>
</head>
<body>
    <div id="app">
       <h2>搜索</h2>
       姓名搜索: <input type="text" placeholder="Please input name" v-model="value">
       <ul>
           <!-- v-for的使用方法，filterPeople是一个计算属性 -->
           <li v-for="(person, index) in filterPeople" :key="index">
                {{index}}---{{person.name}}---{{person.age}}
           </li>
       </ul>
       <button @click="sort(1)">年龄升序</button>
       <button @click="sort(2)">年龄降序</button>
       <button @click="sort(0)">原本顺序</button>
    </div>
</body>
<script text="javascript" src="./vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
           value: "",
           people: [
               {name: 'jack', age:18},
               {name: 'jackson', age:19},
               {name: 'pete', age:20},
               {name: 'peter', age:22},
               {name: 'john', age:20},
               {name: 'james', age:45},
               {name: 'frack', age:6},
               {name: 'susan', age:46},
           ],
           sortWay: 0,
        },
        computed: {
            filterPeople: function() {
                var newArr = [...this.people];
                if( this.value.trim() ) {
                    newArr = this.people.filter(
                        (item) => {
                            return item.name.indexOf(this.value) !== -1;
                        }
                    )
                }
                // 0代表不排序
                if(this.sortWay) {
                    newArr.sort(
                        function(p1, p2) {
                            if(this.sortWay === 1) {
                                return p1.age - p2.age;
                            }
                            else {
                                return p2.age - p1.age;
                            }
                        } 
                    )
                    console.log(this.sortWay);
                }
                return newArr;
            }
        },
        methods: {
            sort(res) {
                this.sortWay = res;
            }
        },
    })
</script>
</html>

```



### 6.3 事件绑定的实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>事件处理</title>
</head>
<body>
    <!--
        1. 绑定监听:
            v-on:xxx="fun"
            @xxx="fun"
            @xxx="fun(参数)"
            当没有参数时@xxx="fun"时，默认@xxx="fun($event)"，绑定了该事件
            当带有参数时@xxx="fun(参数)"，如果需要绑定该事件，则要自己加上@xxx="fun(参数, $event)
        
        2. 事件修饰符:
        .prevent : 阻止事件的默认行为 event.preventDefault()
        .stop : 停止事件冒泡 event.stopPropagation()
        3. 按键修饰符
        .keycode : 操作的是某个keycode值的健
        .enter : 操作的是enter键
    -->
  <div id="example">
    <h2>1. 绑定监听</h2>
    <button @click="test1">test1</button>
    <button @click="test2('abc')">test2</button>
    <button @click="test3('abcd', $event)">test3</button>
    <h2>2. 事件修饰符</h2>
    <a href="http://www.baidu.com" @click.prevent="test4">百度一下</a>
    <div style="width: 200px;height: 200px;background: red" @click="test5">
      <div style="width: 100px;height: 100px;background: blue" @click.stop="test6"></div>
    </div>

    <!-- 可以用来做回车符提交密码操作 -->
    <h2>3. 按键修饰符</h2>
    <input type="text" @keyup.13="test7">
    <input type="text" @keyup.enter="test7">
  </div>
  <script type="text/javascript" src="./vue.js"></script>
  <script type="text/javascript">
    new Vue({
      el: '#example',
      data: {
      },
      methods: {
        test1(event) {
          alert(event.target.innerHTML);
        },
        test2(msg) {
          alert(msg)
        },
        test3(msg, event) {
          alert(msg + '---' + event.target.textContent)
        },
        test4() {
          alert('点击了链接')
        },
        test5() {
          alert('out')
        },
        test6() {
          alert('inner')
        },
        test7(event) {
          // 可以用来显示键盘操作对应的数值码
          console.log(event.keyCode)
          alert(event.target.value)
        }
      }
    })
  </script>
</body>
</html>

```



### 6.4 表单的制作实例

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>表单输入绑定</title>
</head>
<body>
<!--
1. 使用v-model(双向数据绑定)自动收集数据
  text/textarea
  checkbox
  radio
  select
-->
<div id="demo">
  <form action="/xxx" @submit.prevent="handleSubmit">
    <span>用户名: </span>
    <input type="text" v-model="username"><br>
    <span>密码: </span>
    <input type="password" v-model="pwd"><br>
    <span>性别: </span>
    <input type="radio" id="female" value="女" v-model="sex">
    <label for="female">女</label>
    <input type="radio" id="male" value="男" v-model="sex">
    <label for="male">男</label><br>
    <span>爱好: </span>
    <input type="checkbox" id="basket" value="basket" v-model="likes">
    <label for="basket">篮球</label>
    <input type="checkbox" id="foot" value="foot" v-model="likes">
    <label for="foot">足球</label>
    <input type="checkbox" id="pingpang" value="pingpang" v-model="likes">
    <label for="pingpang">乒乓</label><br>
    <span>城市: </span>
    <select v-model="cityId">
      <option value="">未选择</option>
      <option :value="city.id" v-for="(city, index) in allCitys" :key="city.id">{{city.name}}</option>
    </select><br>
    <span>介绍: </span>
    <textarea rows="10" v-model="info"></textarea><br><br>
    <input type="submit" value="注册">
  </form>
</div>
<script type="text/javascript" src="./vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#demo',
    data: {
      username: '',
      pwd: '',
      sex: '男',
      likes: ['foot'],
      allCitys: [{id: 1, name: 'BJ'}, {id: 2, name: 'SS'}, {id: 3, name: 'SZ'}],
      cityId: '2',
      info: ''
    },
    methods: {
      handleSubmit () {
        console.log(this.username, this.pwd, this.sex, this.likes, this.cityId, this.info)
        alert('提交注册的ajax请求')
      }
    }
  })
</script>
</body>
</html>

```



## 7. 按键修饰符 



**在绑定了键盘或鼠标的点击事件后,可以通过按下的按键触发要进行的事件,这时需要在后方添加表示按键的修辞符**



### 7.1 按键码



- 可以通过keyCode的值来绑定需要触发的按键

  ```html
  <input v-on:keyup.13="submit">
  ```

- **部分特殊的按键码可以使用别名**

- - **.enter**

- - **.tab**

- - **.delete**(捕获“删除”和“退格”键)

- - **.esc**

- - **.space**

- - **.up**

- - **.down**

- - **.left**

- - **.right**

- 也可以自定义按键修饰符的别名

  ```vue
  Vue.config.keyCodes.f1 = 112;//使用Vue对象上的全局属性config.keyCodes来定义别名
  // 在绑定时就可以使用v-on:keyup.f1直接对f1按键进行操作了
  ```



### 7.2 系统修饰符



**系统修辞符监听仅在同时按下了绑定键盘或鼠标按钮时才会触发事件**



- **键盘**

- - **.ctrl**

- - **.alt**

- - **.shift**

- - **.meta**


**注意:**在 Mac 系统键盘上，meta 对应 command 键 (⌘)。在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。

```html
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

- **鼠标**

- - **.left**

- - **.right**

- - **.middle**



**注:**修饰键与常规按键不同，在和 `keyup` 事件一起用时，事件触发时修饰键必须处于按下状态。换句话说，只有在按住 `ctrl` 的情况下释放其它按键，才能触发 `keyup.ctrl`。而单单释放 `ctrl` 也不会触发事件。如果只想要单独触发,则需要使用keycode编码或**.exact**修饰符



- .exact

  .exact 修饰符允许用户控制由精确的系统修饰符组合触发的事件

  ```html
  <!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
  <button @click.ctrl="onClick">A</button>
  
  <!-- 有且只有 Ctrl 被按下的时候才触发 -->
  <button @click.ctrl.exact="onCtrlClick">A</button>
  
  <!-- 没有任何系统修饰符被按下的时候才触发 -->
  <button @click.exact="onClick">A</button>
  ```



## 8. Vue的生命周期



### 8.1 生命周期



![2](./img/2.png)



### 8.2 Vue实例创建阶段

- var vm=new  Vue(),创建出一个Vue实例对象

- **beforeCreat**，当Vue实例被完全创建出来之前,就会执行该函数，这是表示刚初始化了一个空的Vue对象,这时候这个对象身上只有一些     
            **注意:**在beforeCreat生命周期函数执行的时候,data和methods等中的数据还没有初始化,所以在这里面调用这些data或methods等中的属性和方法会报错

- **created**,在该函数中,data和methods等数据已经被初始化好了,如果要调用methods中的方法或者data中的数据,最早只能在created中进行操作     
            **注:**如果要发Ajax请求尽量在这个阶段发送

- 在这两个生命周期函数之间进行Vue的编译模板,把Vue代码中的那些指令进行执行,最终在内存中生成一个编译好的最终模板字符串,然后把这个字符串渲染为内存中的DOM,但是此时只是在内存中渲染DOM,还没有将其挂载到页面中去

- **beforeMount**,在该函数中模板已经在内存中了,但是还没有把模板渲染到页面中,也就是说{{}}中的内容还没有被解析,页面中的元素还没有真正被替换,只是写了一些模板字符串

- 将内存中的DOM挂载到页面中去

- **mounted,**表示内存中的DOM已经挂载到页面中了,用户已经可以看到渲染好的页面了    

   **注意:**

  mounted是实例创建期间执行的最后一个生命周期函数,当执行完mounted就表示实例已经完全被创建好了

  如果要通过某些插件操作页面上的DOM节点,最早要在mounted中进行



### 8.3 Vue实例运行阶段

 

**下面两个生命周期必须要数据发生改变时才会进行,会根据data数据的改变触发0次或多次**

- **beforeUpdate,**这个函数表明Vue实例在运行时数据已经被更新,而页面还没有被更新的时间节点,当执行该函数时,页面中显示的数据还是没有更新前的数据,而data中的数据是最新的,页面还没有和数据实现同步
- 在这两个函数之间,会根据data中的最新数据,重新渲染出一份最新的内存DOM树,当最新的内存DOM树被更新之后,会把最新的内存DOM树重新渲染到真实的页面中去,完成数据从data到页面视图的更新
- **updated,**当这个函数执行时证明data中的数据已经和页面中的数据保存同步更新了



### 8.4 Vue实例销毁阶段

- **beforeDestroy,**     当执行该函数时,Vue实例就已经从运行阶段进入到了销毁阶段,实例上的所以属性如data,methods等都还是处于可用状态,还没有真正的执行销毁
- **destroyed,**当执行到该函数时,Vue实例已经被完全销毁,此时所有实例中的属性都不可用了



### 8.5 生命周期演示实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>09_Vue实例_生命周期</title>
</head>
<body>
<!--
    1. vue对象的生命周期
    1). 初始化显示
        * beforeCreate()
        * created()
        * beforeMount()
        * mounted()
    2). 更新状态
        * beforeUpdate()
        * updated()
    3). 销毁vue实例: vm.$destory()
        * beforeDestory()
        * destoryed()
    2. 常用的生命周期方法
    created()/mounted(): 发送ajax请求, 启动定时器等异步任务
    beforeDestory(): 做收尾工作, 如: 清除定时器
-->
<div id="test">
  <button @click="destroyVue">destory vue</button>
  <p v-if="isShow">尚硅谷IT教育</p>
</div>
<script type="text/javascript" src="./vue.js"></script>
<script type="text/javascript">
  new Vue({
    el: '#test',
    data: {
      isShow: true
    },
    beforeCreate() {
      console.log('beforeCreate()')
    },
    created() {
      console.log('created()')
    },
    beforeMount() {
      console.log('beforeMount()')
    },
    mounted () {
      console.log('mounted()')
      // 执行异步任务
      this.intervalId = setInterval(() => {
        console.log('-----')
        this.isShow = !this.isShow
      }, 1000)
    },

    beforeUpdate() {
      console.log('beforeUpdate()')
    },
    updated () {
      console.log('updated()')
    },

    beforeDestroy() {
      console.log('beforeDestroy()')
      // 执行收尾的工作
      clearInterval(this.intervalId)
    },
    destroyed() {
      console.log('destroyed()')
    },
    methods: {
      destroyVue () {
        this.$destroy()
      }
    }
  })

</script>
</body>
</html>

```



### 8.6 总结

![3](./img/3.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>vue生命周期学习</title>
  <script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>
</head>
<body>
  <div id="app">
    <h1>{{message}}</h1>
  </div>
</body>
<script>
  var vm = new Vue({
    el: '#app',
    data: {
      message: 'Vue的生命周期'
    },
    beforeCreate: function() {
      console.group('------beforeCreate创建前状态------');
      console.log("%c%s", "color:red" , "el     : " + this.$el); //undefined
      console.log("%c%s", "color:red","data   : " + this.$data); //undefined 
      console.log("%c%s", "color:red","message: " + this.message) 
    },
    created: function() {
      console.group('------created创建完毕状态------');
      console.log("%c%s", "color:red","el     : " + this.$el); //undefined
      console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化 
      console.log("%c%s", "color:red","message: " + this.message); //已被初始化
    },
    beforeMount: function() {
      console.group('------beforeMount挂载前状态------');
      console.log("%c%s", "color:red","el     : " + (this.$el)); //已被初始化
      console.log(this.$el);
      console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化  
      console.log("%c%s", "color:red","message: " + this.message); //已被初始化  
    },
    mounted: function() {
      console.group('------mounted 挂载结束状态------');
      console.log("%c%s", "color:red","el     : " + this.$el); //已被初始化
      console.log(this.$el);    
      console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化
      console.log("%c%s", "color:red","message: " + this.message); //已被初始化 
    },
    beforeUpdate: function () {
      console.group('beforeUpdate 更新前状态===============》');
      console.log("%c%s", "color:red","el     : " + this.$el);
      console.log(this.$el);   
      console.log("%c%s", "color:red","data   : " + this.$data); 
      console.log("%c%s", "color:red","message: " + this.message); 
    },
    updated: function () {
      console.group('updated 更新完成状态===============》');
      console.log("%c%s", "color:red","el     : " + this.$el);
      console.log(this.$el); 
      console.log("%c%s", "color:red","data   : " + this.$data); 
      console.log("%c%s", "color:red","message: " + this.message); 
    },
    beforeDestroy: function () {
      console.group('beforeDestroy 销毁前状态===============》');
      console.log("%c%s", "color:red","el     : " + this.$el);
      console.log(this.$el);    
      console.log("%c%s", "color:red","data   : " + this.$data); 
      console.log("%c%s", "color:red","message: " + this.message); 
    },
    destroyed: function () {
      console.group('destroyed 销毁完成状态===============》');
      console.log("%c%s", "color:red","el     : " + this.$el);
      console.log(this.$el);  
      console.log("%c%s", "color:red","data   : " + this.$data); 
      console.log("%c%s", "color:red","message: " + this.message)
    }
  })
</script>
</html>
```



![4](./img/4.png)



## 9. 过渡与动画



**Vue中可以通过`transition`组件来实现过渡效果Vue 在插入,更新或者移除 DOM 时,提供多种不同方式的应用过渡效果**



- 在 CSS 过渡和动画中自动应用 class

- 可以配合使用第三方 CSS 动画库，如 Animate.css

- 在过渡钩子函数中使用 JavaScript 直接操作 DOM

- 可以配合使用第三方 JavaScript 动画库，如 Velocity.js



### 9.1 过渡的类名



#### 9.1.1 自身实现的类名



**这些类名是transition组件中自定好的,在使用的时候只需要在CSS中写入特定的类名和样式就可以了**



- **v-enter**：定义进入过渡的开始状态。在元素被插入之前生效，此时元素还没有进入过渡，在元素被插入之后的下一帧移除

- **v-enter-active**：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数

- **v-enter-to**: 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 **v-enter** 被移除)，在过渡/动画完成之后移除

- **v-leave**: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除

- **v-leave-active**：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数

- **v-leave-to**:定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 **v-leave** 被删除)，在过渡/动画完成之后移除



**注:**



- **一般都是使用v-enter,v-leave-to与v-enter-active和v-leave-active的组合**

- **对于这些在过渡中切换的类名来说,如果使用一个没有名字的 `<transition>`,则 `v-` 是这些类名的默认前缀,如果使用了 `<transition name="my-transition">`,那么 `v-enter` 会替换为 `my-transition-enter**`,通过这个可以绑定:name实现动态过渡的效果



```html
<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
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

<script>
new Vue({
  el: '#demo',
  data: {
    show: true
  }
})
</script>
```



- 动画效果同过渡效果,只是在动画中v-enter这个类名在插入DOM中后不会立刻被删除,

  而是在

  animationend

  事件触发时才会被删除

  注:

  动画可以实现多个阶段的样式

  ```html
  <style>
  .bounce-enter-active {
    animation: bounce-in .5s;
  }
  .bounce-leave-active {
    animation: bounce-in .5s reverse;
  }
  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }
  }
  </style>
  
  <div id="example">
    <button @click="show = !show">Toggle show</button>
    <transition name="bounce">
      <p v-if="show">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris facilisis enim libero, at lacinia diam fermentum id. Pellentesque habitant morbi tristique senectus et netus.</p>
    </transition>
  </div>
  
  <script>
  new Vue({
    el: '#example-2',
    data: {
      show: true
    }
  })
  </script>
  ```



#### 9.1.2  自定义过渡的类名



**可以通过引入第三方库实现过渡效果,这时需要使用自定义过渡的类名来加第三方库的过渡效果使用**



可以通过以下特性来自定义过渡类名,这些类名分别也对应着上方的执行时期,它们的优先级高于普通的类名



- **enter-class**

- **enter-active-class**

- **enter-to-class**

- **leave-class**

- **leave-active-class**

- **leave-to-class**



**在这些自定义的属性中可以写入要引入的第三方库的CSS样式就能实现效果**



```html
<link href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1" rel="stylesheet" type="text/css">

<div id="example">
  <button @click="show = !show">
    Toggle render
  </button>
  <transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
  >
    <p v-if="show">hello</p>
  </transition>
</div>

<script>
new Vue({
  el: '#example',
  data: {
    show: true
  }
})
</script>
```



#### 9.1.3 实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>过渡与动画</title>
  <style>
      .fade1-enter, .fade1-leave-to {
          opacity: 0;
      }
      .fade1-enter-active, .fade1-leave-active {
          transition: opacity 1s;
      }
      .fade2-enter {
          opacity: 0;
          transform: translateX(-20px);
      }
      .fade2-leave-to {
        opacity: 0;
        transform: translateX(20px);
      }
      .fade2-enter-active, .fade2-leave-active {
          transition: all 3s;
      }
  </style>
</head>
<body>
    <!--
        1. vue动画的理解
            操作css的transition或animation
            vue会给目标元素添加/移除特定的class
        2. 基本过渡动画的编码
            1). 在目标元素外包裹<transition name="xxx">
            2). 定义class样式
                1>. 指定过渡样式: transition
                2>. 指定隐藏时的样式: opacity/其它
        3. 过渡的类名
            xxx-enter-active: 指定显示的transition
            xxx-leave-active: 指定隐藏的transition
            xxx-enter: 指定隐藏时的样式
    -->
  <div id="app1">
    <button @click="isShow = !isShow">Destroy</button>
    <transition name="fade1">
        <p v-if="isShow">Hello</p>
    </transition>
  </div>
  <div id="app2">
    <button @click="isShow = !isShow">Destroy</button>
    <transition name="fade2">
        <p v-if="isShow">Hello</p>
    </transition>
  </div>
  <script type="text/javascript" src="./vue.js"></script>
  <script type="text/javascript">
    new Vue({
        el: "#app1",
        data() {
            return {
                isShow: "false",
            }
        },
    })
    new Vue({
        el: "#app2",
        data() {
            return {
                isShow: "false",
            }
        },
    })
  </script>
</body>
</html>

```





### 9.2 初始渲染过渡



**为`transition`组件添加一个简单的属性appear就能够实现在刚开始渲染的时候就使用一次`enter-active-class`来实现开始渲染列表的过渡效果**



**初始渲染时也可以使用自定义的CSS类名进行初始渲染**



- **appear-class**

- **appear-active-class**

- **appear-to-class**



**注意:**使用自定义类名进行渲染时也需要添加appear属性



```html
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class"
  appear-active-class="custom-appear-active-class"
>
  <!-- ... -->
</transition>

<!--当然也可以使用JS的钩子函数-->
<transition
  appear
  v-on:before-appear="customBeforeAppearHook"
  v-on:appear="customAppearHook"
  v-on:after-appear="customAfterAppearHook"
  v-on:appear-cancelled="customAppearCancelledHook"
>
  <!-- ... -->
</transition>
```



### 9.3 显性定义过渡时间



**默认情况下，Vue 会等待其在过渡效果的根元素的第一个 `transitionend` 或 `animationend` 事件。**然而也可以不这样设定——比如，我们可以拥有一个精心编排的一系列过渡效果，其中一些嵌套的内部元素相比于过渡效果的根元素有延迟的或更长的过渡效果。在这种情况下,**可以用 `<transition>` 组件上的绑定的 `duration` 属性定制一个显性的过渡持续时间 (以毫秒为单位)**



```html
<transition :duration="1000">...</transition>
```



**可以传入一个对象分别对移入和移除的时间进行设置**



```html
<transition :duration="{ enter: 500, leave: 800 }">...</transition>
```



### 9.4 JS钩子



**除了通过CSS实现过渡效果,还可以用JS中的钩子函数实现过渡效果**,这些钩子可以结合CSS使用,也可以全部单独使用



```html
<transition
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"

  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>
```



```html
// ...
methods: {
  // --------
  // 进入中
  // --------

  beforeEnter: function (el) {
    // ...
  },
  // 当与 CSS 结合使用时
  // 回调函数 done 是可选的
  enter: function (el, done) {
    // ...
    el.offsetWidth;
     //玄学操作,不加这个设置全JS样式时,动画不会有过渡效果出现,可以认为是这个操作会强制动画刷新
    done()
     //done()所代表的函数就是下一个结束afterEnter的函数,只有调用了这个回调函数才会执行下面的方法
  },
  afterEnter: function (el) {
    // ...
  },
  enterCancelled: function (el) {
    // ...
  },

  // --------
  // 离开时
  // --------

  beforeLeave: function (el) {
    // ...
  },
  // 当与 CSS 结合使用时
  // 回调函数 done 是可选的
  leave: function (el, done) {
    // ...
    done()
  },
  afterLeave: function (el) {
    // ...
  },
  // leaveCancelled 只用于 v-show 中
  leaveCancelled: function (el) {
    // ...
  }
}
```



**注意:**



- 推荐对于仅使用 JavaScript 过渡的元素添加 `v-bind:css="false"`，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响

- 当只用 JavaScript 过渡的时候，**在 enter 和 leave 中必须使用 done 进行回调**。否则，它们将被同步调用，过渡会立即完成。



### 9.5 多个元素过渡



对于原生标签可以使用 `v-if`和`v-else` 来实现多标签过渡效果



**注意:**当有相同标签名的元素切换时，需要通过 `key` 特性设置唯一的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容



```html
<transition>
  <button v-if="isEditing" key="save">
    Save
  </button>
  <button v-else key="edit">
    Edit
  </button>
</transition>
<!--也可以也可以通过给同一个元素的 key 特性设置不同的状态来代替 v-if 和 v-else-->
<transition>
  <button v-bind:key="isEditing">
    {{ isEditing ? 'Save' : 'Edit' }}
  </button>
</transition>
```



**过渡模式**



**通过mode属性来定义多个元素过渡时的过渡模式**



- **in-out**：新元素先进行过渡，完成之后当前元素过渡离开

- **out-in**：当前元素先进行过渡，完成之后新元素过渡进入



```html
<transition  mode="out-in"></transition>
```



### 9.6 列表过渡



**渲染一整个列表时,如用v-for来渲染,就需要使用< transition-group> 组件**、



**注意:**



- 不同于 < transition>组件，< transition-group>组件会以一个真实元素呈现,默认为一个 `<span>`标签,可以通过 tag 特性更换为其他元素
  **如:**内部是li列表,那么可以用`<transition-grounp tag="ul">`来让该组件被渲染时表现为ul

- 过渡模式不可用，因为不再相互切换特有的元素

- 内部元素必须要有提供唯一的 key 属性值



#### 9.6.1 添加与删除列表



**通过对一个`transiton-grounp`用过渡的类名和实现当个成员在过渡时的效果**



```html
<style>
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to
/* .list-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>

<div id="list-demo" class="demo">
  <button v-on:click="add">Add</button>
  <button v-on:click="remove">Remove</button>
  <transition-group name="list" tag="p">
    <span v-for="item in items" v-bind:key="item" class="list-item">
      {{ item }}
    </span>
  </transition-group>
</div>

<script>
new Vue({
  el: '#list-demo',
  data: {
    items: [1,2,3,4,5,6,7,8,9],
    nextNum: 10
  },
  methods: {
    randomIndex: function () {
      return Math.floor(Math.random() * this.items.length)
    },
    add: function () {
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    remove: function () {
      this.items.splice(this.randomIndex(), 1)
    },
  }
})
</script>
```



#### 9.6.2 排序过渡列表



**上方的添加与删除列表只会对进行操作的成员自身产生过渡效果,对组件中的其他成员没有过渡效果,如果要想通过过渡效果进行添加,需要使用v-move的类名写入CSS样式**,该效果会在组件的成员改变其定位的时候起作用,所以要想起过渡效果还需要在过渡时将元素的定位改变为绝对定位.也可以通过 `name` 属性来自定义前缀,也能通过 `move-class` 属性CSS效果



```html
<style>
.flip-list-move {
  transition: transform 1s;
}
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.14.1/lodash.min.js"></script>

<div id="flip-list-demo" class="demo">
  <button v-on:click="shuffle">Shuffle</button>
  <transition-group name="flip-list" tag="ul">
    <li v-for="item in items" v-bind:key="item">
      {{ item }}
    </li>
  </transition-group>
</div>

<script>
new Vue({
  el: '#flip-list-demo',
  data: {
    items: [1,2,3,4,5,6,7,8,9]
  },
  methods: {
    shuffle: function () {
      this.items = _.shuffle(this.items)
    }
  }
})
</script>
```



#### 9.6.3 交错过渡列表



**通过JS钩子来实现列表的过渡效果,使data属性与JS进行数据通信,就可以实现列表的交错过渡效果**



```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/velocity/1.2.3/velocity.min.js"></script>

<div id="staggered-list-demo">
  <input v-model="query">
  <transition-group
    name="staggered-fade"
    tag="ul"
    v-bind:css="false"
    v-on:before-enter="beforeEnter"
    v-on:enter="enter"
    v-on:leave="leave"
  >
    <li
      v-for="(item, index) in computedList"
      v-bind:key="item.msg"
      v-bind:data-index="index"
    >{{ item.msg }}</li>
  </transition-group>
</div>

<script>
new Vue({
  el: '#staggered-list-demo',
  data: {
    query: '',
    list: [
      { msg: 'Bruce Lee' },
      { msg: 'Jackie Chan' },
      { msg: 'Chuck Norris' },
      { msg: 'Jet Li' },
      { msg: 'Kung Fury' }
    ]
  },
  computed: {
    computedList: function () {
      var vm = this
      return this.list.filter(function (item) {
        return item.msg.toLowerCase().indexOf(vm.query.toLowerCase()) !== -1
      })
    }
  },
  methods: {
    beforeEnter: function (el) {
      el.style.opacity = 0
      el.style.height = 0
    },
    enter: function (el, done) {
      var delay = el.dataset.index * 150
      setTimeout(function () {
        Velocity(
          el,
          { opacity: 1, height: '1.6em' },
          { complete: done }
        )
      }, delay)
    },
    leave: function (el, done) {
      var delay = el.dataset.index * 150
      setTimeout(function () {
        Velocity(
          el,
          { opacity: 0, height: 0 },
          { complete: done }
        )
      }, delay)
    }
  }
})
</script>
```



## 10. 过滤器



**Vue可以通过自定义过滤器,将需要的文本格式化输出**



**注意:**



- 过滤器只能写在插值表达式或者v-bind表达式中,并且过滤器需要添加到要添加的JS表达式的后方并用管道符|分割

  ```html
  <!-- 在双花括号中 -->
  {{ message | capitalize }}
  
  <!-- 在 `v-bind` 中 -->
  <div v-bind:id="rawId | formatId"></div>
  
  <!-- 管道符后方的都是声明的过滤器函数 -->
  ```

- 每个过滤器函数会将接收到的表达式作为函数内部的第一个参数,如果在使用时传入参数,那么传入的参数会依次成为第二个第三个等参数

  ```vue
  {{ message | filterA('arg1', arg2) }}
  ```

- 多个过滤器可以进行串联操作,将传入的表达式依次进行过滤

  ```vue
  {{ message | filterA | filterB }}
  ```



### 10.1 全局过滤器



**全局的过滤器可以在任意的Vue实例中使用**



```js
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})

new Vue({
  // ...
})
```



### 10.2 私有过滤器



**私有的过滤器只能在自身的本地实例中使用**



```js
new Vue({
    data:{},
    methods{},
    filters: {
        capitalize: function (value) {
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
        }
    }  
})
```



## 11. 自定义指令



**自定义指令可以通过全局或局部的方式创建,在使用时需要在前面加上v-的标识符表示时一个指令**



### 11.1 全局指令



**通过全局的Vue的Vue.directive()可以创建一个能用在整个Vue实例内的指令**



```js
// 注册一个全局自定义指令 v-focus
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时聚焦
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```



### 11.2 局部指令 



**通过局部创建的directives属性可以创建多个内部的指令,该指令只能用在自身的Vue实例中**



```js
new Vue({
    data:{},
    methods{},  
        directives: {
        focus: {
            // 指令的定义
            inserted: function (el) {
             el.focus()
            }
        }
    }
}
```



### 11.3 钩子函数



**在定义的一个指令对象中可以绑定多个可选的钩子函数,这些钩子函数会在特定的时刻自动调用**



#### 11.3.1 函数



- **bind**: 只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置

- **inserted**: 被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)

- **update**: 所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新

- **componentUpdate**: 指令所在组件的 VNode 及其子 VNode全部更新后调用

- **unbind**: 只调用一次，指令与元素解绑时调用



**函数简写**



当只想要对bind与update设置相同行为而不设置其他的钩子函数时,可以直接写成一个函数,不用写一个包含了钩子函数的对象



```js
//全局
Vue.directive('focus', function(el){
    el.focus();
})
//局部
new Vue({
    data:{},
    methods{},  
        directives: {
        function (el) {
             el.focus()
        }           
    }
}
```



#### 11.3.2 钩子函数的参数



- **el**：指令所绑定的元素,可以用来直接操作DOM

- **binding**：一个对象，还包含以下属性

- - `name`：指令名，不包括 `v-` 前缀

- - ```
    value
    ```

    ：指令的绑定值，会将参数的表达式进行解析,如果内部绑定的参数为1+1,那么绑定后的值就为2

    注意:

    如果想要传递多个值,可以传入一个对象,通过对象进行获取多个值

    ```html
    <div v-demo="{ color: 'white', text: 'hello!' }"></div>
    <script>
        Vue.directive('demo', function (el, binding) {
          console.log(binding.value.color) // => "white"
          console.log(binding.value.text)  // => "hello!"
        })
    </script>
    ```

- - `oldValue`：指令绑定的前一个值，仅在 **update** 和 **componentUpdated** 钩子函数中中可以使用,无论值是否改变都可用

- - `expression`：字符串形式的指令表达式,不会对表达式进行解析,如果参数为1+1那么值还为 "1 + 1"

- - `arg`：传给指令的参数,可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。

- - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`

- **vnode**：Vue 编译生成的虚拟节点

- **oldVnode**：上一个虚拟节点，仅在 **update** 和 **componentUpdated** 钩子函数中可以使用



```html
<div id="hook-arguments-example" v-demo:foo.a.b="message"></div>
```



```js
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
/*
name: "demo"
value: "hello!"
expression: "message"
argument: "foo"
modifiers: {"a":true,"b":true}
vnode keys: tag, data, children, text, elm, ns, context, fnContext, fnOptions, fnScopeId, key, componentOptions, componentInstance, parent, raw, isStatic, isRootInsert, isComment, isCloned, isOnce, asyncFactory, asyncMeta, isAsyncPlaceholder
*/
```



### 11.4 实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>自定义指令</title>
</head>
<body>
<!--
    1. 注册全局指令
    Vue.directive('my-directive', function(el, binding){
        el.innerHTML = binding.value.toUpperCase()
    })
    2. 注册局部指令
    directives : {
        'my-directive' : {
            bind (el, binding) {
            el.innerHTML = binding.value.toUpperCase()
            }
        }
    }
    3. 使用指令
    v-my-directive='xxx'
-->
<!--
    需求: 自定义2个指令
    1. 功能类型于v-text, 但转换为全大写
    2. 功能类型于v-text, 但转换为全小写
-->
<div id="test">
  <p v-upper-text="msg"></p>
  <p v-lower-text="msg"></p>
</div>
<div id="test2">
  <p v-upper-text="msg"></p>
  <p v-lower-text="msg"></p>
</div>
<script type="text/javascript" src="./vue.js"></script>
<script type="text/javascript">
  // 注册一个全局指令
  // el: 指令所在的标签对象
  // binding: 包含指令相关数据的容器对象
  Vue.directive('upper-text', function(el, binding) {
    console.log(el, binding)
    el.textContent = binding.value.toUpperCase()
  })
  new Vue({
    el: '#test',
    data: {
      msg: "I Like You"
    },
    // 注册局部指令
    directives: {
      'lower-text': function(el, binding) {
        console.log(el, binding)
        el.textContent = binding.value.toLowerCase()
      }
    }
  })
  new Vue({
    el: '#test2',
    data: {
      msg: "I Like You Too"
    }
  })
</script>
</body>
</html>

```



## 12. 组件



### 12.1 **组件的定义**



**组件的出现是为了拆分Vue实例的代码量,能够让我们以不同的组件来划分不同的功能模板,将来需要什么样的功能,只需要调用对应的组件就可以了**



**组件化与模块化的区别**



- 模块化是从代码逻辑的角度进行划分的;方便代码分层开发,保证每个功能模块的职能单一

- 组件化是从UI界面的角度进行划分的,前端的组件化是为了方便UI组件的重用



### 12.2 创建组件



**组件的注意事项:**



- **每个组件必须只有一个根元素,**可以将模板的内容包裹在一个父元素内来解决这个问题

- 组件中可以有自己的data数据,使用方式同Vue实例中一样,**但是组件的data只能是一个方法,而且必须要返回一个包含了数据的对象,**因为需要每个组件之间相互独立,如果不是一个函数,那么每个组件就会影响其他的组件
  **如果要想同时影响其他数据,可以创建一个外部的镀锡,每次data返回这个对象**



#### 12.2.1 组件名



**在创建一个组件时,我们始终需要给该组件一个名字用作标识**,组件名的有多种写法



- **短横线命名法**,使用短横线命名法来命名组件在使用的时候也是直接将引用的组件名作为标签名来使用

- **驼峰命名法,**使用驼峰命名法命名的组件在引用这个组件时可以通过两种命名的方式来引用
  **注意:**当用作标签时只能使用短横线命名法,所以最好都使用短横线命名法来命名



#### 12.2.2 全局组件



**创建全局组件有三种方式,都是基于Vue.component()方法来创建的**



- 通过

  ```js
  Vue.extend()
  ```

  的方式,创建一个含有template属性的子类,引用子类到

  ```js
  Vue.component()
  ```

  创建的组件中去

  ```js
  var tem1 = Vue.extend({
      template:'<h3>这是使用 Vue.extend 创建的组件</h3>'
  });
  Vue.component('myTem1',tem1);
  
  <!--可以通过组合的形式引用-->
  Vue.component('myTem1',Vue.extend({
      template :'<h3>这是使用 Vue.extend 创建的组件</h3>'
  }));
  ```

- 直接使用

  ```js
  Vue.component()
  ```

  方法传入一个对象

  ```js
  Vue.component('my-component-name', {
    template:'<h3>这是直接使用Vue.component创建的组件</h3>'
  });
  ```

- 在一个 `<script>` 标签中，并为其带上 `text/x-template`的类型，然后通过ID引用模板(这种方式有代码提示)

  ```js
  <script type="text/x-template" id="hello-world-template">
    <p>Hello hello hello</p>
  </script>
  
  <script>
  Vue.component('hello-world', {
    template: '#hello-world-template'
  })
  </script>
  ```



#### 12.2.3 私有组件



**通过在一个Vue实例中向components对象中添加属性可以在局部注册只能在该Vue实例内部使用的私有组件**



**对于 components对象中的每个属性来说，其属性名就是自定义元素的名字，其属性值就是这个组件的选项对象**



```js
new Vue({
  el: '#app',
  components: {
      'component-a': {
          template:""
      },
      'component-b': {
          template:""
      },
  }
})
/*
    也可以通过一个普通的变量来定义组件
*/
var ComponentA = { /* ... */ }
var ComponentB = { /* ... */ }
var ComponentC = { /* ... */ }

new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```



**注意:**局部注册的组件在其子组件中不可以使用,如果要使用需要嵌套创建组件或通过webpack等导出



```js
//嵌套组件
var ComponentA = { /* ... */ }

var ComponentB = {
  components: {
    'component-a': ComponentA
  },
  // ...
}
```





### 12.3 Props



**子组件是无法直接使用父组件的data中的数据的,需要通过props属性才能够使用父组件传入过来的值**



#### 12.3.1 向子组件传入数据



**在父组件的引用中填入属性名与对应的属性值,然后在子组件的props值填入与引用子组件的属性名一致的属性名,就可以在子组件中引用父组件的数据了，就如访问data中的值一样**



```html
<blog-post title="My journey with Vue"></blog-post>
<blog-post title="Blogging with Vue"></blog-post>
<blog-post title="Why Vue is so fun"></blog-post>
<script>
Vue.component('blog-post', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})
</script>
```



**注意:**



- **-一个组件默认可以拥有任意数量的 prop,**任何值都可以传递给任何 prop,但是为了方便可以传入一个对象,调用对象的属性来使用传入的数据

- 组件中的所有props中的数据都是通过父组件传递给子组件**的,不要试图去修改props中传入的数据,**一般都是只读的,如果修改Vue会抛出报错信息

- **可以通过v-bind动态传递给prop一个值**

- 子组件的data数据并不是通过父组件传递过来的,而是子组件自身私有的,比如子组件通过Ajax请求回来的数据都可以放在data身上,**子组件的data上的数据都是可读可写的**



#### 12.3.2 Prop的大小写



**HTML中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当使用 DOM 中的模板时，驼峰命名法的prop名需要使用其等价的短横线分隔命名**



```js
<blog-post post-title="hello!"></blog-post>

<script>
Vue.component('blog-post', {
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
</script>
```



#### 12.3.3 Prop类型



**如果希望传入的prop都有指令的值类型,可以用对象的方式来,可以以对象形式列出 prop，这些属性的名称和值分别是 prop 各自的名称和类型。除此之外,还可以用于配置其他高级选项**



```js
//数组形式
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']
//对象形式
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object
}
```



```js
// 简单语法
Vue.component('props-demo-simple', {
  props: ['size', 'myMessage']
})

// 对象语法，提供校验
Vue.component('props-demo-advanced', {
  props: {
    // 检测类型
    height: Number,
    // 检测类型 + 其他验证
    age: {
      type: Number,
      default: 0,//设置默认值
      required: true,//是否必须
      validator: function (value) {//对值进行验证
        return value >= 0
      }
    }
  }
})
```



#### 12.3.4 动态传递Prop



**可以通过v-bind的方式动态传递一个变量值给一个prop**



- 传入一个数字

  ```html
  <!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post v-bind:likes="42"></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:likes="post.likes"></blog-post>
  ```

- 传入一个布尔值

  ```html
  <!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
  <blog-post is-published></blog-post>
  
  <!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post v-bind:is-published="false"></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:is-published="post.isPublished"></blog-post>
  ```

- 传入一个数组

  ```html
  <!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:comment-ids="post.commentIds"></blog-post>
  ```

- 传入一个对象

  ```html
  <!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post
    v-bind:author="{
      name: 'Veronica',
      company: 'Veridian Dynamics'
    }"
  ></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:author="post.author"></blog-post>
  ```

- 传入一个对象的所有属性

  如果想要将一个对象的所有属性都作为 prop 传入，你可以使用不带参数的 `v-bind`

  (取代 `v-bind:prop-name`)

  ```js
  post: {
    id: 1,
    title: 'My Journey with Vue'
  }
  ```

  ```js
  <blog-post v-bind="post"></blog-post>
  <!--与下面的方法等价-->
  <blog-post v-bind:id="post.id"  v-bind:title="post.title"></blog-post>
  ```



### 12.4 $ref



**可以使用ref属性为一个组件或是子元素赋予一个引用的ID,通过这个引用的ID,父组件可以直接通过`this.$refs`访问这个组件或子元素**



```html
<div id="app">
    <div>
      <input type="button" value="获取元素内容" @click="getElement" />
      <!-- 使用 ref 获取元素 -->
      <h1 ref="myh1">这是一个大大的H1</h1>

      <hr>
      <!-- 使用 ref 获取子组件 -->
      <my-com ref="mycom"></my-com>
    </div>
  </div>

  <script>
    Vue.component('my-com', {
      template: '<h5>这是一个子组件</h5>',
      data() {
        return {
          name: '子组件'
        }
      }
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        getElement() {
          // 通过 this.$refs 来获取元素
          console.log(this.$refs.myh1.innerText);
          // 通过 this.$refs 来获取组件
          console.log(this.$refs.mycom.name);
        }
      }
    });
  </script>
```



### 12.5 组件切换



#### 12.5.1 通过v-if切换组件



**通过一个标识可以进行两个组件之间的切换**



```js
<div id="app">
    <a href="#" @click.prevent="flag=true">登录</a>
    <a href="#" @click.prevent="flag=false">注册</a>
    <login v-if="flag"></login>
    <register v-else></register>
</div>

<script>
    Vue.component("login",{
        template:"<h2>登录<h2>"
    })
     Vue.component("register",{
        template:"<h2>注册<h2>"
    })
    new Vue({
        el:"#app",
        data:{
            flag:true
        }
    })
</script>
```



#### 12.5.2 通过component切换组件



**通过Vue中自带的component标签的:is特性来实现多个组件之间的切换**



```js
<div id="app">
    <a href="#" @click.prevent="clickName='login'">登录</a>
    <a href="#" @click.prevent="clickName='register'">注册</a>
    <component :is="clickName"></component>
</div>

<script>
    Vue.component("login",{
        template:"<h2>登录<h2>"
    })
     Vue.component("register",{
        template:"<h2>注册<h2>"
    })
    new Vue({
        el:"#app",
        data:{
            clickName:"login"
        }
    })
</script>
```



#### 12.5.3 过渡切换



**组件的切换比其他的东西容易很多,只需要使用过渡模式就能完成切换**



```js
<style>
    .component-fade-enter-active, .component-fade-leave-active {
        transition: opacity .3s ease;
    }
    .component-fade-enter, .component-fade-leave-to{
        opacity: 0;
    }
</style>

<div id="app">
    <a href="#" @click.prevent="clickName='login'">登录</a>
    <a href="#" @click.prevent="clickName='register'">注册</a>
    <transition mode="out-in">
    <component :is="clickName" name="component-fade"></component>
    </transition>
</div>

<script>
    Vue.component("login",{
        template:"<h2>登录<h2>"
    })
     Vue.component("register",{
        template:"<h2>注册<h2>"
    })
    new Vue({
        el:"#app",
        data:{
            clickName:"login"
        }
    })
</script>
```



## 13. 组件之间的通信方式



### 13.1 props



父子组件间通信的基本方式

属性值的2大类型: 

​      一般: 父组件-->子组件

​      函数: 子组件-->父组件

隔层组件间传递: 必须逐层传递(麻烦)

兄弟组件间: 必须借助父组件(麻烦)



#### 13.1.1 声明

在组件内声明所有的 props

1. 方式一: 只指定名称 `props:['name','age','setName'] `

2. 方式二: 指定名称和类型

   ```js
   props:{
   	name:String,
   	age:Number,
   	setName:Function 
   }
   ```

3. 方式三: 指定名称/类型/必要性/默认值 

   ```js
   props:{ 
       name:{
           type:String,
           required:true,
           default:xxx
       },
   }
   ```

   

 #### 13.1.2 优缺点

1) 此方式用于父组件向子组件传递数据 

2) 所有标签属性都会成为组件对象的属性, 模板页面可以直接引用 

3) 问题: 

a. 如果需要向非子后代传递数据必须多层逐层传递

b. 兄弟组件间也不能直接 props 通信, 必须借助父组件才可以



### 13.2 自定义事件



**子组件也无法使用组件的事件,要想传递给父组件事件,需要通过内置的$emit方法并传入事件的名字,来向父级组件触发一个事件**



#### 13.2.1 $emit()向子组件传递事件

 

**在子组件的引用中绑定事件的自定义名字,然后绑定父组件的事件,在子组件中通过抛出事件$emit来使用父组件的事件**



```html
<!--引用子组件-->
<blog-post v-on:enlarge-text="doSomething"></blog-post>
<!--子组件-->
<script>
Vue.component("enlarge-text",{
    template:"<button v-on:click="$emit('enlarge-text')">Enlarge text</button>"
})
</script>

```



#### 13.2.2 $emit()向父组件抛出值

 

**子父组件的函数中写入参数,那么当子组件使用$emit的时候可以传入后面多个参数来将值传递给父组件的参数,从而实现子组件向父组件传值**

 

```html
<div id="app">
    <blog-post
     v-on:enlarge-text="onEnlargeText"
     ></blog-post>
</div>
<script>
    Vue.component("blog-post",{
        template:"<button v-on:click="$emit('enlarge-text',0.1)">Enlarge text</button>"
    })
    new Vue({
        el="#app",
        data:{
            postFontSize:1
        }
        methods: {
            onEnlargeText: function (enlargeAmount) {
                this.postFontSize += enlargeAmount
        }
       }  
    })
</script>

```

**注意:**虽然子组件能触发父组件的方法或值,但是这些方法中的this指向依然是父组件,子组件只是使用的这些方法,同时传递了一些参数



#### 13.2.3 实例

```html
<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <!-- 需要自定义一个事件，事件名最好与对应方法名一致 -->
         <!-- 在子组件调用的地方使用，即可调用
          this.$emit('addItem', this.value)
          参数格式：自定义事件名，后面是要跟参数 -->
      <myHeader @addItem="addItem"></myHeader>
    </div>
   </div>
</template>
<script>
  import myHeader from './myHeader'
  export default {
    data () {
      return {
        // 读取localStorage保存的数据
        items: JSON.parse(localStorage.getItem('todos_key') || '[]')
      }
    },
    components: {
      myHeader
    },
    methods: {
      addItem (newValue) {
        const newItem = {name: newValue, complete: false}
        this.items.push(newItem)
      }
    },
    watch: {
      items: {
        deep: true,
        handler: function (val) {
          // 将数据(json)保存到localStorage
          localStorage.setItem('todos_key', JSON.stringify(val))
        }
      }
    }
  }
</script>
<style>
</style>
```



#### 13.2.4 \$on与\$once



- **\$on属性用于监听在当前实例上的自定义事件,事件可以由vm.$emit触发。回调函数会接收所有传入事件触发函数的额外参数**
- **\$once属性与$on一致,只不过只会触发一次,触发一次后移除该事件**

```js
vm.$on('test', function (msg) {
  console.log(msg)
})
vm.$once('test', function (msg) {
  console.log(msg)
})
vm.$emit('test', 'hi')
// => "hi"

```

**注意:**在组件化中通过创建一个中间的Vue实例可以进行中转完成父子组件的事件传值



#### 13.2.5 $on()实例



```html
<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <!-- 要给组件一个ref，在接下来进行绑定 -->
      <myHeader ref="myhead"></myHeader>
    </div>
   </div>
</template>
<script>
  import myHeader from './myHeader'
  export default {
    data () {
      return {
        // 读取localStorage保存的数据
        items: JSON.parse(localStorage.getItem('todos_key') || '[]')
      }
    },
    components: {
      myHeader
    },
    // 需要在mouunted()中使用$on,理由是要在程序还没有开始的时候就挂载该事件
    // 确保其总能被触发
    mounted () {
      // 哪个子组件要，就给谁$on
      // 不能写成this.$on('addItem', this.addItem)
      // 参数为自定义事件名，要使用的方法
      this.$refs.head.$on('addItem', this.addItem)
    },
    methods: {
      addItem (newValue) {
        const newItem = {name: newValue, complete: false}
        this.items.push(newItem)
      }
    },
    watch: {
      items: {
        deep: true,
        handler: function (val) {
          // 将数据(json)保存到localStorage
          localStorage.setItem('todos_key', JSON.stringify(val))
        }
      }
    }
  }
</script>
<style>
</style>

```



#### 13.2.6 总结



1. 方式一: 

   通过 `v-on `绑定`` @delete_todo="deleteTodo"``

   触发事件(只能在父组件中接收) `this.$emit(eventName,data)`

2. 方式二: 

   通过

   ```JS
   $on() this.$refs.xxx.$on('delete_todo',
   		function(todo){ 
   		this.deleteTodo(todo) 
   	})
   )
   
   ```

1) 此方式只用于子组件向父组件发送消息(数据)，用来取代function props(用来取代方法)

2) 问题: 隔代组件或兄弟组件间通信此种方式不合适



### 13.3 发布-订阅通信机制



#### 13.3.1 pubsub-js的下载引入



使用消息订阅(subscribe)-发布(publish)机制: 自定义事件机制

**工具库** : PubSubJS

**下载**: npm install pubsub-js --S --D

 

使用:

```JS
import PubSub from 'pubsub-js' //引入
PubSub.subscribe('delete', function(msg, data){ }); //订阅
PubSub.publish('delete', data) //发布消息

```

 

优点: 可以支持任意关系组件之间的通信



#### 13.3.2 发布消息



发布------触发事件监听

 

```JS
PubSub.publish('msg',data)

msg：给本次发布-订阅取的名字

data：需要传递的参数
```



#### 13.3.3 订阅消息



订阅------绑定事件监听

 

```JS
PubSub.subscribe('msg',
	(msg,data) => {

 
})
```



msg: 对应发布时的名字

data: 发布时传递过来的参数

回调函数: 处理的方法，再此建议用箭头函数，避免使用this的时候指向错误



#### 13.3.4 实例

```HTML
// 父组件
<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <!-- 需要给它的子组件(也就是这个组件的父组件)绑定一个remove(index)方法 -->
      <myMain :items="items"></myMain>
    </div>
   </div>
</template>
<script>
  import myMain from './myMain'
  import Pubsub from 'pubsub-js'
  export default {
    data () {
      return {
        // 读取localStorage保存的数据
        items: JSON.parse(localStorage.getItem('todos_key') || '[]')
      }
    },
    components: {
      myMain
    },
    mounted () {
      // 在此进行发布，理由是要在程序还没有开始的时候就挂载该事件，确保其总能被触发
      // 取名为delItems，msg不可省略，指代delItems，index为参数
      Pubsub.subscribe('delItems', (msg, index) => {
        // 用箭头函数使得this指向该实例
        this.remove(index)
      })
    },
    methods: {
      remove (index) {
        this.items.splice(index, 1)
      }
    }
  }
</script>
<style>
</style>

```



### 13.4 Slot传递标签



#### 13.4.1 理解

此方式用于父组件向子组件传递标签数据



#### 13.4.2 用法



子组件Child.vue

```HTML
<template> 
	<div>
		<slotname="xxx">不确定的标签结构 1</slot> 
		<div>组件确定的标签结构</div> 
		<slotname="yyy">不确定的标签结构 2</slot> 
	</div> 
</template>
```



父组件Parent.vue

```HTML
<child> 
	<div slot="xxx">xxx 对应的标签结构</div>
	<div slot="yyy">yyyy 对应的标签结构</div> 
</child>
```



## 14. Vue-Router



### 14.1 路由的定义



- **后端路由：**对于普通的网站，所有的超链接都是URL地址，所有的url地址都对应服务器上对应的资源

  **后端路由是处理请求的回调函数**

- **前端路由：**对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容；所以，单页面程序中的页面跳转主要用hash实现,在单页面应用中这就叫做前端路由

  **前端路由让构建单页面应用变得易如反掌**



### 14.2 VueRouter的安装



```bash
法一：
https://unpkg.com/vue-router/dist/vue-router.js
也可以像 https://unpkg.com/vue-router@2.0.0/dist/vue-router.js 这样指定 版本号 或者 Tag。
在 Vue 后面加载 vue-router，它会自动安装的：
<script src="/path/to/vue.js"></script>
<script src="/path/to/vue-router.js"></script>

法二：
NPM
npm install vue-router
如果在一个模块化工程中使用它，必须要通过 Vue.use() 明确地安装路由功能：
import Vue from 'vue'
import VueRouter from 'vue-router'
Vue.use(VueRouter)
如果使用全局的 script 标签，则无须如此 (手动安装)。

tip：
构建开发版
如果你想使用最新的开发版，就得从 GitHub 上直接 clone，然后自己 build 一个 vue-router。
git clone https://github.com/vuejs/vue-router.git node_modules/vue-router
cd node_modules/vue-router
npm install
npm run build

```



### 14.3 Vue-router基本操作



**1.导入 vue-router 组件类库**



```html
<!-- 1. 导入 vue-router 组件类库 -->
  <script src="./lib/vue-router-2.7.0.js"></script>
```



**2.使用 router-link 组件来导航**



```html
<!-- 
2. 使用 router-link 组件来导航
router-link组件默认渲染为一个a标签,可以使用tag属性来转换标签,但是无论转换为什么标签都可以进行跳转 
-->
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
<!--链接的跳转可以使用a标签,但是官方不推荐使用,因为a链接使用的时候需要在前面加上#,会很麻烦-->
```



**3.使用 router-view 组件来显示匹配到的组件**



```html
<!-- 
3. 使用 router-view 组件来显示匹配到的组件 
这是Vue-router提供的组件元素,专门用来当做占位符,当路由规则到了路径,就会把对应的组件展示到其中
可以使用多个router-view,这是会根据path属性的目录渲染多个组件
-->
<!--
    最外层也可以使用transition组件将 router-view 组件包裹实行过渡效果
-->
<router-view></router-view>
```



**4.创建使用`Vue.extend`创建组件**



```js
// 4.1 使用 Vue.extend 来创建登录组件
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    // 4.2 使用 Vue.extend 来创建注册组件
    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });
```



**5.创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则**



```js
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
    var router = new VueRouter({
      /*
      route这个配置对象中的route表示路由器匹配规则的意思
      每个路由规则都是一个规则对象,身上有两个必须的属性:
      第一个属性为path,表示监听哪个路由链接地址
      第二个属性为component,表示如果路由前面匹配到了path路径,则展示component属性对于的组件
      */  
      routes: [//路由器匹配规则
        
        {path:'/',redirect:'/login'},
        //通过redirect属性设置路由重定向,当访问根目录的时候自动跳转到/login目录
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]
    });
```



**6.使用 router 属性来使用路由规则**



```js
// 6. 创建 Vue 实例，得到 ViewMode
    var vm = new Vue({
      el: '#app',
      router: router // 使用 router 属性来使用路由规则
    });
```



### 14.4 修改路由的CSS样式



**当点击了`router-link`组件时,会默认为该路由设置一个`router-link-active`的CSS类名,在通过给该类名设置样式可以达到修改路由样式的能力,如果要修改这个默认的类名选用自己需要的类名,可以通过在VueRouter的构造函数中添加`linkActiveClass`来改变一个新值**



```js
var router = new VueRouter({
    routes: [//路由器匹配规则    
        {path:'/',redirect:'/login'},
        //通过redirect属性设置路由重定向,当访问根目录的时候自动跳转到/login目录
        { path: '/login', component: login },
        { path: '/register', component: register }
    ],
    linkActiveClass:"myClass"
});
```



### 14.5 向路由里传入参数



**一个Vue组件内置的$route属性可以代表着正在进行跳转的路由**



#### 14.5.1 query



**当在路由器中链接中使用查询字符串(url后面的?后的一系列值),不用修改路由规则中的path属性的路径,在路由视图的组件中可用通过this.$route获取该路由实例,通过该实例的query属性获取传入的参数的属性和值**



传入

```html
<router-link to="/login?id=123">登录</router-link>
<router-link to="/register?id=456">注册</router-link>
```



获取

```js
var login = Vue.extend({
    template: '<h1>登录组件</h1>',
    created(){
        console.log(this.$route.query.id);
    }
});

var register = Vue.extend({
    template: '<h1>注册组件</h1>'
    created(){
    console.log(this.$route.query.id);
    }
});
```



#### 11.4.2 params



**使用params来获取参数需要在路由规则中定义参数,然后在路由器链接中需要在后面跟上对应数量的/+值传给参数实现传参,通过该实例的params属性获取传入的参数的属性和值**



```html
<router-link to="/login/123/zhangsan">登录</router-link>
<router-link to="/register/456/lisi">注册</router-link>
```



```js
var login = Vue.extend({
    template: '<h1>登录组件</h1>',
    created(){
        console.log(this.$route.params.id);
    }
});

var register = Vue.extend({
    template: '<h1>注册组件</h1>'
    created(){
    console.log(this.$route.params.id);
    }
});
```



```js
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
    var router = new VueRouter({
      /*
      route这个配置对象中的route表示路由器匹配规则的意思
      每个路由规则都是一个规则对象,身上有两个必须的属性:
      第一个属性为path,表示监听哪个路由链接地址
      第二个属性为component,表示如果路由前面匹配到了path路径,则展示component属性对于的组件
      */  
      routes: [//路由器匹配规则
        
        {path:'/',redirect:'/login'},
        //通过redirect属性设置路由重定向,当访问根目录的时候自动跳转到/login目录
        { path: '/login/:id/:name', component: login },
        { path: '/register/:id/:name', component: register }
      ]
    });
```



#### 14.5.3 通过router-view



```js
<router-view :message="message"></router-view>

在router-view中传入参数，然后再路由里像props一样使用
```





### 14.6 路由嵌套



**如果想要在一层路由组件下面开启第二层组件,不能够直接通过二级的路由链接得到二级的路由组件,因为这样一级的链接组件就会消失,需要通过`routes`路由器匹配规则中相应规则的children属性,在该属性构成的数组中写入子路由来实现路由嵌套的功能**



```js
<div id="app">
    <router-link to="/account">Account</router-link>

    <router-view></router-view>
  </div>

  <script>
    // 父路由中的组件
    const account = Vue.extend({
      template: `<div>
        这是account组件
        <router-link to="/account/login">login</router-link> | 
        <router-link to="/account/register">register</router-link>
        <router-view></router-view>
      </div>`
    });

    // 子路由中的 login 组件
    const login = Vue.extend({
      template: '<div>登录组件</div>'
    });

    // 子路由中的 register 组件
    const register = Vue.extend({
      template: '<div>注册组件</div>'
    });

    // 路由实例
    var router = new VueRouter({
      routes: [
        { path: '/', redirect: '/account/login' }, // 使用 redirect 实现路由重定向
        {
          path: '/account',
          component: account,
          children: [ // 通过 children 数组属性，来实现路由的嵌套
            { path: 'login', component: login }, // 注意，子路由的开头位置，不要加 / 路径符
            { path: 'register', component: register }
          ]
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      components: {
        account
      },
      router: router
    });
  </script>
```



### 14.7 命名路由



**通过在`<router-link></router-link>`的组件中to指向一个带有name属性的对象,而在路由规则中也添加一个对应的name属性实现路由跳转,该方法能让我们更加轻松的进行路由规则的匹配**



```js
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
<script>
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})
</script>
```



### 14.8 命名视图



**在Vue的路由实例中,一个路由路径可以对应多个路由组件,所以可以设置多个路由的视图,在一个路径中就可以,通过命名的视图在一个路径中使用多个路由组件,从而实现经典的布局效果**



```js
<!--CSS-->  
<style>
    .header {
      border: 1px solid red;
    }

    .content{
      display: flex;
    }
    .sidebar {
      flex: 2;
      border: 1px solid green;
      height: 500px;
    }
    .mainbox{
      flex: 8;
      border: 1px solid blue;
      height: 500px;
    }
  </style>
<!--HTML-->  
<div id="app">
    <router-view></router-view>
    <div class="content">
      <router-view name="a"></router-view>
<!--通过name属性可以只参与对应组件的渲染,没有name属性代表是default,会渲染属性名为defalut的组件-->
      <router-view name="b"></router-view>
    </div>
  </div>
<!--JS-->  
<script>
    var header = Vue.component('header', {
      template: '<div class="header">header</div>'
    });

    var sidebar = Vue.component('sidebar', {
      template: '<div class="sidebar">sidebar</div>'
    });

    var mainbox = Vue.component('mainbox', {
      template: '<div class="mainbox">mainbox</div>'
    });

    // 创建路由对象
    var router = new VueRouter({
      routes: [
        {
          path: '/', components: {
            default: header,//定义一个name为efalut的组件,即使视图不写name属性也能渲染该组件
            a: sidebar,
            b: mainbox
          }
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router
    });
  </script>
```



### 14.9 route与router



- this.$route是路由的参数对象,所有的路由参数如pararms和query都属于该属性的参数

- this.$router是一个路由导航对象,用它可以方便的使用JS代码,实现路由器的前进,后退,跳转到新的url地址

- 有**push(), replace(), back()**三个常用方法

  ```js
  // 字符串
  this.$router.push('home')
  
  // 对象
  this.$router.push({ path: 'home' })
  
  // 命名的路由
  this.$router.push({ name: 'user', params: { userId: '123' }})
  
  // 带查询参数，变成 /register?plan=private
  this.$router.push({ path: 'register', query: { plan: 'private' }})
  ```

  注意:

- - 如果提供了 path，params 会被忽略，上述例子中的 query 并不属于这种情况

- - 该属性的API`this.$router.push`、 `this.$router.replace` 和 `this.$router.go` 跟 `window.history.pushState`、 `window.history.replaceState` 和 `window.history.go`类似



### 14.10 重定向和别名



#### 14.10.1 重定向

 “重定向”的意思是，当用户访问 /a时，URL 将会被替换成 /b，然后匹配路由为 /b。



重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b：

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



#### 14.10.2 别名



别名的意思是：

**/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。**

 

上面对应的路由配置为：

```js
const router = new VueRouter({
  routes: [
   { path: '/a', component: A, alias: '/b' }
  ]
 })
```



### 14.11  导航守卫(全局前置守卫)



“导航”表示路由正在发生改变。

正如其名，`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

记住**参数或查询的改变并不会触发进入/离开的导航守卫**。你可以通过观察 `$route` 对象来应对这些变化，或使用 `beforeRouteUpdate` 的组件内守卫。



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



**确保 `next` 函数在任何给定的导航守卫中都被严格调用一次。它可以出现多于一次，但是只能在所有的逻辑路径都不重叠的情况下，否则钩子永远都不会被解析或报错。**

这里有一个在用户未能验证身份时重定向到 `/login` 的示例：

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



### 14.12 实例



#### 14.12.1 项目中路由放置规则

1. 路由组件一般放置在views/pages的文件夹下，而不是放置在components文件夹下，一般components文件夹放置非路由组件

2. 路由器组件一般放置在router文件夹下，入口文件为index.js，里面是路由的配置



#### 14.12.2 main.js配置路由器

```js
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import router from './router/index' // 导入路由器
import App from './views/路由/App.vue'
Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>',
  // 也可以简写成router(ES6语法)
  router: router
})
```



#### 14.12.3 index.js配置

```js
/**
 * 路由器模块
 * 配置所有的路由
 */
import Vue from 'vue'
import VueRouter from 'vue-router'
import About from '../views/路由/About.vue'
import Home from '../views/路由/Home.vue'
import News from '../views/路由/News.vue'
import Message from '../views/路由/Message.vue'
import MsgDetail from '../views/路由/MsgDetail.vue'
// 如果在一个模块化工程中使用它,必须要通过Vue.use()明确地安装路由功能
Vue.use(VueRouter)
export default new VueRouter({
  // routes为一个数组对象
  routes: [
    {
      // 指定其跳转的位置
      path: '/About',
      // 指定其对应绑定的路由
      component: About
    },
    {
      path: '/Home',
      component: Home,
      // 子路由的定义方式
      children: [
        {
          // /在开头永远代表根路径
          path: '/Home/News',
          component: News,
		  // meta用来配置标识属性, 用于v-show等进行显示时的标识
	      meta: {
	        showFooter: true
	      }
			
        },
        {
          // ''代表当前路径，所以'Message'为简写
          path: 'Message',
          component: Message,
          children: [
            {
              // :表示占位，一般用于params参数的使用
              path: '/Home/Message/MsgDetail/:id',
              component: MsgDetail
            }
          ]
        },
        {
          path: '',
          redirect: 'News'
        }
      ]
    },
    /**
     * 路由的重定向
     */
    {
      path: '/',
      redirect: '/About'
    }
  ]
})

```



### 14.13 路由懒加载



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



**把组件按组分块**

有时候我们想把某个路由下的所有组件都打包在同个异步块 (chunk) 中。只需要使用 [命名 chunk](https://webpack.js.org/guides/code-splitting-require/#chunkname)，一个特殊的注释语法来提供 chunk name (需要 Webpack > 2.4)。

```js
const Foo = () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
const Bar = () => import(/* webpackChunkName: "group-foo" */ './Bar.vue')
const Baz = () => import(/* webpackChunkName: "group-foo" */ './Baz.vue')
```

Webpack 会将任何一个异步模块与相同的块名称组合到相同的异步块中。



## 15 Vuex



### 15.1 Vuex理解



**Vuex是一个全局的共享存储区域,相当于是一个数据仓库**

 

Vuex是为了保存组件之间的共享数据而诞生的,如果组件之间要有共享数据,可以直接挂载到Vuex中,而不必通过父子组件直接的传值了,而私有的数据则不需要挂载到Vuex中,**只有需要共享的数据才放在Vuex中,私有的数据只需要放在组件的data中即可**

 

**多组件共享状态的问题**

1) 多个视图依赖于同一状态 

2) 来自不同视图的行为需要变更同一状态

3) 以前的解决办法：

  a. 将数据以及操作数据的行为都定义在父组件 

  b. 将数据以及操作数据的行为传递给需要的各个子组件(有可能需要多级传递)

 4) vuex 就是用来解决这个问题的

 

**状态自管理应用** 

这个状态自管理应用包含以下几个部分：

1) state: 驱动应用的数据源 

2) view: 以声明方式将 state 映射到视图 

3) actions: 响应在 view 上的用户输入导致的状态变化(包含 n 个更新状态的方法) 

以下是一个表示“单向数据流”理念的简单示意：

![img](./img/5.png)

 

 

**Vuex的结构模型**

![vuex](./img/6.png)

### 15.2 核心概念



#### 15.2.1 state

1) vuex 管理的状态**对象**

2) 它应该是唯一的` const state = { xxx: initValue }`



#### 15.2.2 mutations

1) 包含多个直接更新 state 的方法(回调函数)的对象 

2) 谁来触发: action 中的 commit('mutation 名称') 

3) 只能包含同步的代码, 不能写异步代码

 

```js
 const mutations = { 
	方法名 (state, {data1}) { 
		xxxxx                      // 更新 state 某个属性的操作
	} 
} 
参数：
可选：{
  state,      // 等同于 `store.state`，若在模块中则为局部状态
  rootState,  // 等同于 `store.state`，只存在于模块中
  commit,     // 等同于 `store.commit`
  dispatch,   // 等同于 `store.dispatch`
  getters,    // 等同于 `store.getters`
  rootGetters // 等同于 `store.getters`，只存在于模块中
}
{data1}： 参数，可以为任意类型，但最后都会包装成一个对象
```



#### 15.2.3 actions



1) 包含多个事件回调函数的对象 

2) 通过执行: commit()来触发 mutation 的调用, 间接更新 state 

3) 谁来触发: 

组件中: this.$store.dispatch('action 名称', data) 

data为参数

4) 可以包含异步代码(定时器, ajax) 



```js
const actions = { 
	action 名称 ({commit, state}, data) { 
		commit('对应mutations的名字', {data}) 
	}
 }
第一个参数：
可选：{
  state,      // 等同于 `store.state`，若在模块中则为局部状态
  rootState,  // 等同于 `store.state`，只存在于模块中
  commit,     // 等同于 `store.commit`
  dispatch,   // 等同于 `store.dispatch`
  getters,    // 等同于 `store.getters`
  rootGetters // 等同于 `store.getters`，只存在于模块中
}
第二个参数： 可以为任意类型，但最后都会包装成一个对象


```



#### 15.2.4 getters 

1) 包含多个计算属性(get)的**对象** 

2) 谁来读取: 组件中: $store.getters.xxx 

3) 使用

```js
const getters = { 
	mmm (state) {
		return 
	} 
}

```

 

注意：

只能写相等于get()的方法，不能写set()的功能

所以如果需要set的功能，必须到组件中写



#### 15.2.5 modules

1) 包含多个 module 

2) 一个 module 是一个 store 的配置对象 

3) 与一个组件(包含有共享数据)对应



```js

const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}
const moduleB = {
  state: { ... },
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

 

**模块的局部状态**

对于模块内部的 mutation 和 getter，接收的第一个参数是模块的局部状态对象。



```js
const moduleA = {
  state: { count: 0 },
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



同样，对于模块内部的 action，局部状态通过 context.state 暴露出来，根节点状态则为 context.rootState：

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



### 15.3 项目结构

Vuex 并不限制你的代码结构。但是，它规定了一些需要遵守的规则：

1. 应用层级的状态应该集中到单个 store 对象中。
2. 提交 **mutation** 是更改状态的唯一方法，并且这个过程是同步的。
3. 异步逻辑都应该封装到 **action** 里面。

只要你遵守以上规则，如何组织代码随你便。如果你的 store 文件太大，只需将 action、mutation 和 getter 分割到单独的文件。

对于大型应用，我们会希望把 Vuex 相关代码分割到模块中。下面是项目结构示例：

```bash
├── index.html
├── main.js
├── api
│   └── ... # 抽取出API请求
├── components
│   ├── App.vue
│   └── ...
└── store
    ├── index.js          # 我们组装模块并导出 store 的地方
    ├── actions.js        # 根级别的 action
    ├── mutations.js      # 根级别的 mutation
    └── modules
        ├── cart.js       # 购物车模块
        └── products.js   # 产品模块
```



### 15.4 表单处理



当在严格模式中使用 Vuex 时，在属于 Vuex 的 state 上使用 `v-model` 会比较棘手：

```html
<input v-model="obj.message">
```

假设这里的 `obj` 是在计算属性中返回的一个属于 Vuex store 的对象，在用户输入时，`v-model` 会试图直接修改 `obj.message`。在严格模式中，由于这个修改不是在 mutation 函数中执行的, 这里会抛出一个错误。

用“Vuex 的思维”去解决这个问题的方法是：给 `<input>` 中绑定 value，然后侦听 `input` 或者 `change` 事件，在事件回调中调用一个方法:

```html
<input :value="message" @input="updateMessage">
// ...
computed: {
  ...mapState({
    message: state => state.obj.message
  })
},
methods: {
  updateMessage (e) {
    this.$store.commit('updateMessage', e.target.value)
  }
}
```

下面是 mutation 函数：

```js
// ...
mutations: {
  updateMessage (state, message) {
    state.obj.message = message
  }
}
```



**双向绑定的计算属性**

必须承认，这样做比简单地使用“`v-model` + 局部状态”要啰嗦得多，并且也损失了一些 `v-model` 中很有用的特性。另一个方法是使用带有 setter 的双向绑定计算属性：

```html
<input v-model="message">
// ...
computed: {
  message: {
    get () {
      return this.$store.state.obj.message
    },
    set (value) {
      this.$store.commit('updateMessage', value)
    }
  }
}
```



### 15.5 实例



#### 15.2.1 主要功能对象

```js
import Vue from 'vue'
import Vuex from 'vuex'
// 在一个模块化的打包系统中,必须显式地通过 Vue.use() 来安装 Vuex：
Vue.use(Vuex)
// 使用Vue.Store
export default new Vuex.Store({
  // 状态对象
  state: {
    count: 0
  },
  // 包含多个更新state函数的对象,mutations对象里的方法可以直接操作state对象
  mutations: {
    // 工程中一般这些模块都是分开文件写,所以传入state参数的写法比较好
    // 如果有其他参数则可以往后写
    INCREMENT (state) {
      state.count++
    },
    DECREMENT (state) {
      state.count--
    }
  },
  // 包含多个对应事件回调函数的对象,actions对象里的方法用来接收组件信息,同时传递给mutations
  actions: {
    // 如果有其他参数则可以往对象后面写,称作载荷(payload)
    increment ({commit}) {
      commit('INCREMENT')
    },
    decrement ({commit}) {
      commit('DECREMENT')
    },
    incrementIfOdd ({commit, state}) {
      if (state.count % 2 !== 0) {
        commit('INCREMENT')
      }
    },
    incrementAsync ({commit}) {
      // 在action里直接可以写异步代码
      setInterval(() => {
        commit('INCREMENT')
      }, 1000)
    }
  },
  // 包含多个getter计算属性的函数对象
  getters: {
    evenOrOdd: function (state) {
      if (state.count % 2 !== 0) {
        return 'Odd'
      } else {
        return 'Even'
      }
    }
  }
})

```



#### 15.2.2 组件绑定

```vue
<template>
  <div>
    <!-- 任何一个组件里都会有一个$store对象,里面有state,getters属性 -->
    <p>Count {{$store.state.count}} & count is {{evenOrOdd}}</p>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementIfOdd">increment if odd</button>
    <button @click="incrementAsync">increment async</button>
  </div>
</template>
<script>
export default {
  computed: {
    evenOrOdd: function () {
      return this.$store.getters.evenOrOdd
    }
  },
  methods: {
    increment () {
      // dispatch()去找到对应actions里面的方法
      // 参数为('对应的方法名',载荷)
      this.$store.dispatch('increment')
    },
    decrement () {
      this.$store.dispatch('decrement')
    },
    incrementIfOdd () {
      this.$store.dispatch('incrementIfOdd')
    },
    incrementAsync () {
      this.$store.dispatch('incrementAsync')
    }
  }
}
</script>
<style>
</style>

```



#### 15.2.3 辅助函数

```vue
<template>
  <div>
    <!-- 任何一个组件里都会有一个$store对象,里面有state,getters属性 -->
    <p>Count {{count}} & count is {{evenOrOdd}}</p>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementIfOdd">increment if odd</button>
    <button @click="incrementAsync">increment async</button>
  </div>
</template>
<script>
// 这些分别为常用的组件绑定的辅助函数
import {mapGetters, mapActions, mapState} from 'vuex'
export default {
  computed: {
    // 等价于mapGetters()返回值为{evenOrOdd(){return this.$store.getters['evenOrOdd']}}
    ...mapGetters(['evenOrOdd']),
    // 等价于mapState()返回值{count(){return this.$store['count']}}
    ...mapState(['count'])
  },
  methods: {
    // 其中这三个方法也可以传入一个对象而非数组,例如：
    // mapActions({Increment: 'increment'})
    // 把 `this.Increment` 映射为 `this.$store.getters.increment`
    // 意思就是给getters里的属性取一个不同于increment的名字
    ...mapActions(['increment', 'decrement', 'incrementIfOdd', 'incrementAsync'])
  }
}
</script>
<style>
</style>

```



### 15.6 总结

![image-20200617155816787](./img/7.png)

## 16. 对象数组更新



### 16.1 Vue.set

```js
Vue.set( target, propertyName/index, value )

参数：

{Object | Array} target
{string | number} propertyName/index
{any} value
返回值：设置的值。

用法：

向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性
 (比如 this.myObject.newProperty = 'hi')

注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。
```



### 16.2vm.$set

```js
vm.$set( target, propertyName/index, value )
参数：

{Object | Array} target
{string | number} propertyName/index
{any} value
返回值：设置的值。

用法：

这是全局 Vue.set 的别名。
```



### 16.3 Vue.set与vm.$set



**向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性**



- **数组添加**
  Vue中的data中的数组可以通过Vue返回后的实例进行改变,所拥有的方法同原生JS,变异方法会直接改变数组,重新渲染页面,但**如果不是变异方法也可以通过重新赋值来使用,Vue不会直接重新渲染,**而是由其内部高效的机制
  **注意:**如果直接通过赋值改变数组中成员的值或者length的长度,并不能够渲染页面,这是由JS内部的机制决定的
  **解决方案:**

- - `Vue.set(vm.items, indexOfItem, newValue)`**(第一个参数为素组名,第二个为数组索引,第三个为成员值)**

- - `vm.items.splice(indexOfItem, 1, newValue)`

- - `vm.$set(vm.items, indexOfItem, newValue)`**(其实vm.$set()就是Vue.set()方法的别名)**

- - **如果要解决改变length属性的问题,**使用`vm.items.splice(newLength)`

- **对象添加**
  如果要更新对象的属性,在已有属性的情况下改变原来的值是可以进行动态更新的,但是**如果是添加一个新的属性或为一个对象添加新的属性不能做到响应式的更新,**这也是由于JS的内部机制决定的
  **解决方案:**

- - `Vue.set(vm.userProfile, 'age', 27`)**(第一个参数为对象名,第二个为键名,第三个为键值)**

- - `vm.$set(vm.userProfile, 'age', 27)`

- - 如果要同时给多个属性使用下面这种方式

    ```
    vm.userProfile = Object.assign({}, vm.userProfile, {
        age: 27,
        favoriteColor: 'Vue Green'
    })
    //不好的方式:
    Object.assign(vm.userProfile, {
        age: 27,
        favoriteColor: 'Vue Green'
    })
    ```



## 17. Mixins



### 17.1 使用场合

**混入 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项**



Mixins是一种分发Vue组件中可复用功能的非常灵活的一种方式。页面的风格不用，但是执行的方法和需要的数据类似就可以选择使用混入



混合对于封装一小段想要复用的代码来讲是有用的。它们当然不是唯一可行的。混合很好，它不需要传递状态，但是这种模式当然也可能会被滥用。



### 17.2 基础实例

​	我们有一对不同的组件，它们的作用是切换一个状态布尔值，一个模态框和一个提示框。这些提示框和模态框除了在功能上，没有其他共同点：它们看起来不一样，用法不一样，但是逻辑一样。

```js
// 模态框
const Modal = {
  template: '#modal',
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  },
  components: {
    appChild: Child
  }
}
// 提示框
const Tooltip = {
  template: '#tooltip',
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  },
  components: {
    appChild: Child
  }
}
	解决办法如下：
const toggle = {
    data () {
        isshowing: false
    },
    methods: {
        toggleShow() {
            this.isshowing = !this.isshowing
        }
    }
}
// 下面即可使用了
// mixins: [变量名]
const Modal = {
  template: '#modal',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};
const Tooltip = {
  template: '#tooltip',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};
如果你是以vue-cli创建的项目来写，可以这样
// mixin.js
export const toggle = {
    data () {
        isshowing: false
    },
    methods: {
        toggleShow() {
            this.isshowing = !this.isshowing
        }
    }
}
// modal.vue
// 将mixin引入该组件，就可以直接使用 toggleShow() 了
import {mixin} from '../mixin.js'
export default {
    mixins: [mixin],
    mounted () {
        
    }
}
// tooltip组件同上

```



### 17.3 合并规则

当组件和混入对象含有同名选项时，这些选项将以恰当的方式混合。



**数据对象内**

mixin的数据对象和组件的数据发生冲突时以组件数据优先。

```js
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



**钩子函数**

同名钩子函数将会混合为一个数组，都将被调用到，但是混入对象的钩子将在组件自身钩子之前调用。

```js
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



**值为对象的选项**

值为对象的选项，例如 methods, components 和 directives，将被混合为同一个对象。两个对象键名冲突时，取组件对象的键值对。

```js
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



### 17.4 全局混入



全局混合被注册到了每个单一组件上。因此，它们的使用场景极其有限并且要非常的小心。一个我能想到的用途就是它像一个插件，你需要赋予它访问所有东西的权限。但即使在这种情况下，我也对你正在做的保持警惕，尤其是你在应用中扩展的函数，可能对你来说是不可知的。

```js
Vue.mixin({
    mounted() {
        console.log("我是mixin");
    }
})
new Vue({
    ...
})

```



再次提醒，小心使用它！那个 console.log将会出现在每个组件上。这种情况还不算坏（除了控制台上有多余的输出），但如果它被错误的使用，你将能看到它会多么的有害。

一个使用合理的例子

```js
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

 

**注意:** 一旦使用全局混入对象，将会影响到**所有**之后创建的 Vue 实例。使用恰当时，可以为自定义对象注入处理逻辑

```js
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



## 18. Vue原码分析

 

### 18.1 准备知识

1) [].slice.call(lis): 将伪数组转换为真数组 

2) node.nodeType: 得到节点类型  

3) Object.defineProperty(obj, propName, {}): 给对象添加/修改属性(指定描述符) configurable: true/false 是否可以重新 define 

enumerable: true/false 是否可以枚举(for..in / keys()) 

value: 指定初始值 writable: true/false value 是否可以修改 

get: 回调函数, 用来得到当前属性值 

set: 回调函数, 用来监视当前属性值的变化 

4) Object.keys(obj): 得到对象自身可枚举的属性名的数组 

5) DocumentFragment: 文档碎片(高效批量更新多个节点) 

6) obj.hasOwnProperty(prop): 判断 prop 是否是 obj 自身的属性



### 18.2 数据代理

1) 数据代理: 通过一个对象代理对另一个对象(在前一个对象内部)中属性的操作(读/写)

2) vue 数据代理: 通过 vm 对象来代理 data 对象中所有属性的操作

3) 好处: 更方便的操作 data 中的数据

4) 基本实现流程

a. 通过 Object.defineProperty()给 vm 添加与 data 对象的属性对应的属性描述符

b. 所有添加的属性都包含 getter/setter

c. getter/setter 内部去操作 data 



### 18.3 模板解析



#### 18.3.1 模板解析的基本流程 

1) 将 el 的所有子节点取出, 添加到一个新建的文档 fragment 对象中 

2) 对 fragment 中的所有层次子节点递归进行编译解析处理 

\* 对大括号表达式文本节点进行解析 

\* 对元素节点的指令属性进行解析 

\* 事件指令解析 

\* 一般指令解析

3) 将解析后的 fragment 添加到 el 中显示



#### 18.3.2 大括号表达式解析 

1) 根据正则对象得到匹配出的表达式字符串: 子匹配/RegExp.$1 name

2) 从 data 中取出表达式对应的属性值 

3) 将属性值设置为文本节点的 textContent 



####18.3.3 事件指令解析 

1) 从指令名中取出事件名 

2) 根据指令的值(表达式)从 methods 中得到对应的事件处理函数对象 

3) 给当前元素节点绑定指定事件名和回调函数的 dom 事件监听 

4) 指令解析完后, 移除此指令属性



#### 18.3.4 一般指令解析 

1) 得到指令名和指令值(表达式) text/html/class msg/myClass 

2) 从 data 中根据表达式得到对应的值 

3) 根据指令名确定需要操作元素节点的什么属性 * v-text---textContent 属性 * v-html---innerHTML 属性 * v-class--className 属性 

4) 将得到的表达式的值设置到对应的属性上 

5) 移除元素的指令属性



### 18.4 数据绑定



#### 18.4.1 数据绑定效果

一旦更新了 data 中的某个属性数据, 所有界面上直接使用或间接使用了此属性的节点都会 更新 



####18.4.2 数据劫持 

1) 数据劫持是 vue 中用来实现数据绑定的一种技术 

2) 基本思想: 通过 defineProperty()来监视 data 中所有属性(任意层次)数据的变化, 一旦变 化就去更新界面



#### 18.4.3四个重要对象

 

**1) Observer**

a. 用来对 data 所有属性数据进行劫持的构造函数

b. 给 data 中所有属性重新定义属性描述(get/set)

c. 为 data 中的每个属性创建对应的 dep 对象

 

**2) Dep(Depend)**

a. **data 中的每个属性(所有层次)都对应一个 dep 对象**

b. 创建的时机: 

\* 在初始化 define data 中各个属性时创建对应的 dep 对象

\* 在 data 中的某个属性值被设置为新的对象时

c. 对象的结构

{

  id, // 每个 dep 都有一个唯一的 id

  subs //包含 n 个对应 watcher 的数组(subscribes 的简写)

}

d. subs 属性说明

\* 当 watcher 被创建时, 内部将当前 watcher 对象添加到对应的 dep 对象的 subs 中

\* 当此 data 属性的值发生改变时, subs 中所有的 watcher 都会收到更新的通知,从而最终更新对应的界面

 

**3) Compiler**

a. 用来解析模板页面的对象的构造函数(一个实例)

b. 利用 compile 对象解析模板页面

c. 每解析一个表达式(非事件指令)都会创建一个对应的 watcher 对象, 并建立 watcher

与 dep 的关系

d. complie 与 watcher 关系: 一对多的关系

 

**4) Watcher**

a. **模板中每个非事件指令或表达式都对应一个 watcher 对象**

b. 监视当前表达式数据的变化

c. 创建的时机: 在初始化编译模板时

d. 对象的组成

{

vm, //vm 对象

exp, //对应指令的表达式

cb, //当表达式所对应的数据发生改变的回调函数

value, //表达式当前的值

depIds //表达式中各级属性所对应的 dep 对象的集合对象

//属性名为 dep 的 id, 属性值为 dep

}

 

**5) 总结: dep 与 watcher 的关系: 多对多**

a. data 中的一个属性对应一个 dep, 一个 dep 中可能包含多个 watcher(模板中有几个

表达式使用到了同一个属性)

b. 模板中一个非事件表达式对应一个 watcher, 一个 watcher 中可能包含多个 dep(表

达式是多层: a.b)

c. 数据绑定使用到 2 个核心技术

`defineProperty() ` 消息订阅与发布

 

#### 18.4.4 双向数据绑定

1) 双向数据绑定是建立在单向数据绑定(model==>View)的基础之上的 

2) 双向数据绑定的实现流程: 

a. 在解析 v-model 指令时, 给当前元素添加 input 监听 

b. 当 input 的 value 发生改变时, 将最新的值赋值给当前表达式所对应的 data 属性



### 18.5 数据驱动





#### 18.5.1 Vue与模板



**使用步骤:**



1. 编写页面模板

1. 1. 直接在 HTML 标签中写 标签

1. 1. 使用 template

1. 1. 使用 单文件 ( `<template />` )

1. 创建 Vue 的实例

1. 1. 在 Vue 的构造函数中提供: data, methods, computed, watcher, props等

1. 将 Vue 挂载到 页面中 ( mount )





#### 18.5.2 数据驱动模型



**Vue 的执行流程：**



1. 获得模板: 模板中有 "坑"

1. 利用 Vue 构造函数中所提供的数据来 "填坑", 得到可以在页面中显示的 "标签了"

1. 将标签替换页面中原来有坑的标签



**所以，Vue 利用我们提供的数据和页面中模板生成了一个新的 HTML 标签 ( node 元素 )，替换到了页面中放置模板的位置。**



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <script src="./node_modules/vue/dist/vue.min.js"></script>
  </head>
  <body>
    <!-- 第一步、写模板 -->
    <div id="root">
      <p>{{name}}</p>
      <p>{{message}}</p>
    </div>
    <script>
      // 第一个打印的root鼠标放上去页面是不会有高亮的
      console.log(root)
      // 第二步，创建实例
      const app = new Vue({
        el: '#root',
        data: {
          name: '张三',
          message: '是人'
        }
      })
      // 第三步，挂载，Vue已经帮我们实现
      // 第二个打印的root鼠标放上去页面才会有高亮的，因为Vue是替换模板，而不是在模板基础上进行修改
      console.log(root)
    </script>
  </body>
</html>
```





#### 18.5.3 简单的模板渲染



**步骤分析：**



- 拿到模板

- 拿到数据（data）

- 将数据与模板结合，得到的是HTML元素（DOM元素）

- 放到页面中





##### 18.5.3.1 简单渲染



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">
      <div>
        <p>{{name}}-{{message}}</p>
      </div>
      <p>{{name}}</p>
      <p>{{message}}</p>
    </div>
    <script>
      /*
            步骤分析：
            1.拿到模板
            2.拿到数据（data）
            3.将数据与模板结合，得到的是HTML元素（DOM元素）
            4.放到页面中
        */
      // 1.模版
      const tmpNode = document.querySelector('#root')
      // 2.数据
      const data = {
        name: '一个名字',
        message: '一个消息'
      }
      // 3.将数据放到模板中（一般使用递归）
      // {{}}语法正则
      const Mustache = /\{\{(.+?)\}\}/g
      /*
        注意的是，在这个案例中我们的template是一个DOM元素，但是真正的Vue源码中是 DOM元素 -> 字符串模板 -> 抽象语法树（AST）-> VNode -> 真正的DOM
      */
      function compiler(template, data) {
        const childNodes = template.childNodes // 取出子元素
        for (let i = 0; i < childNodes.length; i++) {
          const type = childNodes[i].nodeType //1.元素 3.文本节点
          if (type === 3) {
            // 文本节点，判断里面是否有 {{}} 插值
            let txt = childNodes[i].nodeValue // 该属性只有文本节点才有意义
            // 有没有 {{}}
            txt = txt.replace(Mustache, (_, g) => {
              // replace使用正则匹配一次，函数就会调用一次，函数第一个参数表示匹配到的内容，第二个参数表示匹配到的正则中的第一组，以此类推
              const key = g.trim() // 写在{{}}中的东西
              // 将{{xxx}}用这个值替换
              const value = data[key]
              return value
            })
            // 注意：txt现在和DOM元素没有关系
            childNodes[i].nodeValue = txt
          } else if (type === 1) {
            // 元素节点，考虑它有没有子元素，是否将其子元素进行判断是否要插值
            compiler(childNodes[i], data)
          }
        }
      }

      // 两次打印结果一致，因为我们没有生成新的template，是直接在页面更新数据，这样做模板就没有了
      /*
      console.log(tmpNode)
      compiler(tmpNode, data)
      console.log(tmpNode)
      */
      const generateNode = tmpNode.cloneNode(true) //不传true不克隆子节点，同时因为是DOM元素才这样克隆，虚拟DOM不会这样克隆
      console.log(tmpNode)
      compiler(generateNode, data)
      console.log(generateNode)
      // 4.将渲染好的html放到页面中
      tmpNode.parentNode.replaceChild(generateNode, tmpNode)

      /*
        注意：上面的代码只是个极其简陋的模板，还存在很大的问题
        1.Vue使用的是虚拟DOM
        2.只考虑了单属性 {{name}}，而Vue中大量的使用层级 {{child.name.firstName}}
        3.代码没有整合
      */
    </script>
  </body>
</html>
```



**注意：**上面的代码只是个极其简陋的模板，还存在很大的问题：



- Vue使用的是虚拟DOM

- 只考虑了单属性 {{name}}，而Vue中大量的使用层级 {{child.name.firstName}}

- 代码没有整合成面向对象形式，需要最后变成构造函数





##### 18.5.3.2 整合代码





**构造函数化**



我们将上面的简单模板进行一些整理，做成构造函数的形式，面向对象处理。



- ES5函数形式

  ```js
  // {{}}语法正则
  const Mustache = /\{\{(.+?)\}\}/g
  function compiler(template, data) {
      const childNodes = template.childNodes // 取出子元素
      for (let i = 0; i < childNodes.length; i++) {
          const type = childNodes[i].nodeType //1.元素 3.文本节点
          if (type === 3) {
              // 文本节点，判断里面是否有 {{}} 插值
              let txt = childNodes[i].nodeValue // 该属性只有文本节点才有意义
              // 有没有 {{}}
              txt = txt.replace(Mustache, (_, g) => {
                  // replace使用正则匹配一次，函数就会调用一次，函数第一个参数表示匹配到的内容，第二个参数表示匹配到的正则中的第一组，以此类推
                  const key = g.trim() // 写在{{}}中的东西
                  // 将{{xxx}}用这个值替换
                  const value = data[key]
                  return value
              })
              // 注意：txt现在和DOM元素没有关系
              childNodes[i].nodeValue = txt
          } else if (type === 1) {
              // 元素节点，考虑它有没有子元素，是否将其子元素进行判断是否要插值
              compiler(childNodes[i], data)
          }
      }
  }
  // 将我们之前的简单模板进行构造函数化
  function myVue(options) {
      // 习惯：内部数据以下划线开头，只读数据以$开头
      this._data = options.data
      this._el = options.el
      // 准备模板
      this._templateDOM = document.querySelector(this._el)
      this._parent = this._templateDOM.parentNode
      // 渲染工作
      this.render()
  }
  // 将模板结合数据，得到HTML加入到页面中
  myVue.prototype.render = function() {
      this.compiler()
  }
  // 编译，将模板与数据结合，得到真正的DOM元素
  myVue.prototype.compiler = function() {
      // 用模板得到一个准DOM
      const realHTML = this._templateDOM.cloneNode(true)
      compiler(realHTML, this._data)
      this.update(realHTML)
  }
  // 将DOM元素放到页面中，更新
  myVue.prototype.update = function(real) {
      // 注意：在真正的Vue中不是直接用的replaceChild进行更新，而是diff算法与虚拟DOM结合，这只是一个极简的版本
      this._parent.replaceChild(real, document.querySelector(this._el))
  }
  
  const app = new myVue({
      el: '#root',
      data: {
          name: '一个名字',
          message: '一个消息'
      }
  })
  ```

- ES6类的形式

  ```js
  // {{}}语法正则
  const Mustache = /\{\{(.+?)\}\}/g
  function compiler(template, data) {
      const childNodes = template.childNodes // 取出子元素
      for (let i = 0; i < childNodes.length; i++) {
          const type = childNodes[i].nodeType //1.元素 3.文本节点
          if (type === 3) {
              // 文本节点，判断里面是否有 {{}} 插值
              let txt = childNodes[i].nodeValue // 该属性只有文本节点才有意义
              // 有没有 {{}}
              txt = txt.replace(Mustache, (_, g) => {
                  // replace使用正则匹配一次，函数就会调用一次，函数第一个参数表示匹配到的内容，第二个参数表示匹配到的正则中的第一组，以此类推
                  const key = g.trim() // 写在{{}}中的东西
                  // 将{{xxx}}用这个值替换
                  const value = data[key]
                  return value
              })
              // 注意：txt现在和DOM元素没有关系
              childNodes[i].nodeValue = txt
          } else if (type === 1) {
              // 元素节点，考虑它有没有子元素，是否将其子元素进行判断是否要插值
              compiler(childNodes[i], data)
          }
      }
  }
  // 将我们之前的简单模板进行构造函数化
  class myVue {
      constructor(options) {
          // 习惯：内部数据以下划线开头，只读数据以$开头
          this._data = options.data
          this._el = options.el
          // 准备模板
          this._templateDOM = document.querySelector(this._el)
          this._parent = this._templateDOM.parentNode
          // 渲染工作
          this.render()
      }
      // 将模板结合数据，得到HTML加入到页面中
      render() {
          this.compiler()
      }
      // 编译，将模板与数据结合，得到真正的DOM元素
      compiler() {
          // 用模板得到一个准DOM
          const realHTML = this._templateDOM.cloneNode(true)
          compiler(realHTML, this._data)
          this.update(realHTML)
      }
      // 将DOM元素放到页面中，更新
      update(real) {
          // 注意：在真正的Vue中不是直接用的replaceChild进行更新，而是diff算法与虚拟DOM结合，这只是一个极简的版本
          this._parent.replaceChild(real, document.querySelector(this._el))
      }
  }
  
  const app = new myVue({
      el: '#root',
      data: {
          name: '一个名字',
          message: '一个消息'
      }
  })
  ```





**层级属性**



**解决问题：**使用`a.b.c`的方式访问对象时如何解决，其实就是使用字符串路径来访问对象的成员。



```js
// 通过分割字符串来实现
function getValueByPath(obj, path) {
    const paths = path.split('.') // a.b.c
    // 先取到a.b，再取到a.b.c
    let res = obj
    let prop = ''
    // 如果没有值最后为undefined
    while ((prop = paths.shift())) {
        res = res[prop]
    }
    return res
}
```



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">
      <p>{{name.firstName}}</p>
    </div>
    <script>
      // 将我们之前的简单模板进行构造函数化
      class myVue {
        constructor(options) {
          // 习惯：内部数据以下划线开头，只读数据以$开头
          this._data = options.data
          this._el = options.el
          // 准备模板
          this._templateDOM = document.querySelector(this._el)
          this._parent = this._templateDOM.parentNode
          // 渲染工作
          this.render()
        }
        // 将模板结合数据，得到HTML加入到页面中
        render() {
          this.compiler()
        }
        // 编译，将模板与数据结合，得到真正的DOM元素
        compiler() {
          // 用模板得到一个准DOM
          const realHTML = this._templateDOM.cloneNode(true)
          compiler(realHTML, this._data)
          this.update(realHTML)
        }
        // 将DOM元素放到页面中，更新
        update(real) {
          // 注意：在真正的Vue中不是直接用的replaceChild进行更新，而是diff算法与虚拟DOM结合，这只是一个极简的版本
          this._parent.replaceChild(real, document.querySelector(this._el))
        }
      }

      // {{}}语法正则
      const Mustache = /\{\{(.+?)\}\}/g
      function compiler(template, data) {
        const childNodes = template.childNodes // 取出子元素
        for (let i = 0; i < childNodes.length; i++) {
          const type = childNodes[i].nodeType //1.元素 3.文本节点
          if (type === 3) {
            // 文本节点，判断里面是否有 {{}} 插值
            let txt = childNodes[i].nodeValue // 该属性只有文本节点才有意义
            // 有没有 {{}}
            txt = txt.replace(Mustache, (_, g) => {
              // replace使用正则匹配一次，函数就会调用一次，函数第一个参数表示匹配到的内容，第二个参数表示匹配到的正则中的第一组，以此类推
              const path = g.trim() // 写在{{}}中的东西
              // 将{{xxx}}用这个值替换
              const value = getValueByPath(data, path)
              return value
            })
            // 注意：txt现在和DOM元素没有关系
            childNodes[i].nodeValue = txt
          } else if (type === 1) {
            // 元素节点，考虑它有没有子元素，是否将其子元素进行判断是否要插值
            compiler(childNodes[i], data)
          }
        }
      }

      /* 
      解决问题：
      使用a.b.c的方式访问对象时如何解决，其实就是使用字符串路径来访问对象的成员
      */
      function getValueByPath(obj, path) {
        const paths = path.split('.') // a.b.c
        // 先取到a.b，再取到a.b.c
        let res = obj
        let prop = ''
        // 如果没有值最后为undefined
        while ((prop = paths.shift())) {
          res = res[prop]
        }
        return res
      }
      const app = new myVue({
        el: '#root',
        data: {
          name: {
            firstName: '张',
            lastName: '三'
          }
        }
      })
    </script>
  </body>
</html>
```





#### 18.5.4 虚拟DOM



**虚拟DOM能够极大的提高页面渲染的性能，减少页面的缓存等因素的影响。**



```js
// 虚拟DOM类似下面这样
class VNode {
    constructor(tag, data, value, type) {
        this.tag = tag && tag.toLowerCase()
        this.data = data
        this.value = value
        this.type = type
        this.children = []
    }
    appendChild(vnode) {
        this.children.push(vnode)
    }
}
```



在Vue中，要将模板和数据相结合其实需要经历两个过程，这其中也涉及到了两种算法（思路与深拷贝类似）：



- 怎么将真正的 DOM 转换为 虚拟 DOM

  ```js
  // 将真正的DOM转换为VNode
  function getVNode(node) {
      const nodeType = node.nodeType
      let _vnode = null
      if (nodeType === 1) {
          const nodeName = node.nodeName
          const attrs = node.attributes
          let _attrObj = {}
          for (let i = 0; i < attrs.length; i++) {
              _attrObj[attrs[i].nodeName] = attrs[i].nodeValue
          }
          _vnode = new VNode(nodeName, _attrObj, undefined, nodeType)
  
          // 考虑node的子元素
          const childNodes = node.childNodes
          for (let i = 0; i < childNodes.length; i++) {
              _vnode.appendChild(getVNode(childNodes[i]))
          }
      } else if (nodeType === 3) {
          _vnode = new VNode(undefined, undefined, node.nodeValue, nodeType)
      }
      return _vnode
  }
  ```

- 怎么将虚拟 DOM 转换为 真正的 DOM

  ```js
  // 将VNode转换为真正的DOM
  function parseVNode(vnode) {
      // 创建真实的DOM节点
      const type = vnode.type
      let _node = null
      if (type === 3) {
          // 创建文本节点
          return document.createTextNode(vnode.value)
      } else if (type === 1) {
          _node = document.createElement(vnode.tag)
          // 属性
          const data = vnode.data // 现在这个data是键值对
          Object.keys(data).forEach(key => {
              const attrName = key
              const attrValue = data[key]
              _node.setAttribute(attrName, attrValue)
          })
  
          // 创建子元素
          const children = vnode.children
          children.forEach(subvnode => {
              _node.appendChild(parseVNode(subvnode))
          })
          return _node
      }
  }
  ```



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">
      <p>11</p>
    </div>
    <script>
      // 将真正的DOM转换为VNode
      function getVNode(node) {
        const nodeType = node.nodeType
        let _vnode = null
        if (nodeType === 1) {
          const nodeName = node.nodeName
          const attrs = node.attributes
          let _attrObj = {}
          for (let i = 0; i < attrs.length; i++) {
            _attrObj[attrs[i].nodeName] = attrs[i].nodeValue
          }
          _vnode = new VNode(nodeName, _attrObj, undefined, nodeType)

          // 考虑node的子元素
          const childNodes = node.childNodes
          for (let i = 0; i < childNodes.length; i++) {
            _vnode.appendChild(getVNode(childNodes[i]))
          }
        } else if (nodeType === 3) {
          _vnode = new VNode(undefined, undefined, node.nodeValue, nodeType)
        }
        return _vnode
      }
      // 将VNode转换为真正的DOM
      function parseVNode(vnode) {
        // 创建真实的DOM节点
        const type = vnode.type
        let _node = null
        if (type === 3) {
          // 创建文本节点
          return document.createTextNode(vnode.value)
        } else if (type === 1) {
          _node = document.createElement(vnode.tag)
          // 属性
          const data = vnode.data // 现在这个data是键值对
          Object.keys(data).forEach(key => {
            const attrName = key
            const attrValue = data[key]
            _node.setAttribute(attrName, attrValue)
          })

          // 创建子元素
          const children = vnode.children
          children.forEach(subvnode => {
            _node.appendChild(parseVNode(subvnode))
          })
          return _node
        }
      }
      class VNode {
        constructor(tag, data, value, type) {
          this.tag = tag && tag.toLowerCase()
          this.data = data
          this.value = value
          this.type = type
          this.children = []
        }
        appendChild(vnode) {
          this.children.push(vnode)
        }
      }
      const root = document.querySelector('#root')
      const vRoot = getVNode(root)
      console.log(vRoot)
      const realRoot = parseVNode(vRoot)
      // 要验证是否转换，只需要将DOM打印出来是否和原来的DOM一致
      console.log(realRoot)
    </script>
  </body>
</html>
```





### 18.6 函数科里化和渲染模型





#### 18.6.1 函数科里化





**什么是函数科里化？**



- [函数式编程](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/)

- [维基百科](https://zh.wikipedia.org/wiki/柯里化)





#### 18.6.2 基本概念



- **科里化：** 一个函数原本有多个参数, 只传入**一个**参数, 生成一个新函数, 由新函数接收剩下的参数来运行得到结构。

- **偏函数：** 一个函数原本有多个参数, 只传入**一部分**参数, 生成一个新函数, 由新函数接收剩下的参数来运行得到结构。

- **高阶函数：**一个函数**参数是一个函数**, 该函数对参数这个函数进行加工, 得到一个函数, 这个加工用的函数就是高阶函数。





#### 18.6..3 Vue中的函数科里化



**Vue 中使用函数科里化的直接受益就是能够提升性能，使用科里化能够缓存函数的一部分能力。**



Vue 本质上是使用 HTML 的字符串作为模板的, 将字符串的 模板 转换为 AST, 再转换为 VNode。



- 模板 -> AST

- AST -> VNode

- VNode -> DOM



在这三个阶段中，第一个阶段 模板 ->  AST 是最消耗性能的，因为在这里面进行了字符串的解析。在前面我们进行简单的模板渲染时并没有说明这个问题，其实 Vue 在真正的转换的时候不是那样直接转换的。



**以Vue的例子来说，在 Vue 中每一个标签可以是真正的 HTML 标签, 也可以是自定义组件, 那么怎么区分？**



其实，观察Vue的源码我们可以知道，Vue已经内部事先将可以用的 HTML 标签都保存起来了。



```js
const tags = 'html,body,base,head,link,meta,style,title,' +
      'address,article,aside,footer,header,h1,h2,h3,h4,h5,h6,hgroup,nav,section,' +
      'div,dd,dl,dt,figcaption,figure,picture,hr,img,li,main,ol,p,pre,ul,' +
      'a,b,abbr,bdi,bdo,br,cite,code,data,dfn,em,i,kbd,mark,q,rp,rt,rtc,ruby,' +
      's,samp,small,span,strong,sub,sup,time,u,var,wbr,area,audio,map,track,video,' +
      'embed,object,param,source,canvas,script,noscript,del,ins,' +
      'caption,col,colgroup,table,thead,tbody,td,th,tr,' +
      'button,datalist,fieldset,form,input,label,legend,meter,optgroup,option,' +
      'output,progress,select,textarea,' +
      'details,dialog,menu,menuitem,summary,' +
      'content,element,shadow,template,blockquote,iframe,tfoot'
```



但是，如果我们每次在进行判断的时候都要循环一次判断，这样做是非常消耗性能的。而使用科里化能够将指数次的时间复杂度降为O(1)。



```js
const tags =
      'html,body,base,head,link,meta,style,title,' +
      'address,article,aside,footer,header,h1,h2,h3,h4,h5,h6,hgroup,nav,section,' +
      'div,dd,dl,dt,figcaption,figure,picture,hr,img,li,main,ol,p,pre,ul,' +
      'a,b,abbr,bdi,bdo,br,cite,code,data,dfn,em,i,kbd,mark,q,rp,rt,rtc,ruby,' +
      's,samp,small,span,strong,sub,sup,time,u,var,wbr,area,audio,map,track,video,' +
      'embed,object,param,source,canvas,script,noscript,del,ins,' +
      'caption,col,colgroup,table,thead,tbody,td,th,tr,' +
      'button,datalist,fieldset,form,input,label,legend,meter,optgroup,option,' +
      'output,progress,select,textarea,' +
      'details,dialog,menu,menuitem,summary,' +
      'content,element,shadow,template,blockquote,iframe,tfoot'
function makeMap(tags) {
    const keys = tags.split(',')
    const set = {}
    keys.forEach(key => (set[key] = true))
    // 我们只需要通过函数是否有该属性来判断
    return function(tagName) {
        return !!set[tagName.toLowerCase()]
    }
}

// 得到这个函数来进行HTML标签和组件的判断
const isHTMLTag = makeMap(tags)
```



**那么，为什么不将`set`定义为全局对象，这样一样能够实现效果？**



因为使用`makeMap`获取各种判断的函数并不止会用一次，在Vue中不止是处理了HTML的标签，还有很多其他的标签，类似`svg`这样。所以，为了区分开以及代码的复用性，我们更倾向将其进行科里化处理。





#### 18.6.4 Vue的渲染模型（极简）



**Vue在获取到渲染函数的时候也是通过函数科里化实现的，目的在于将抽象语法树保存在内存中，增加性能。**



我们在这里不直接将抽象语法树转换为VNode，写一个极简的渲染模型，使用空的VNode模板进行渲染。



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">
      <p>{{name}}</p>
      <p>{{age}}</p>
      <p>{{gender}}</p>
      <div class="box">
        <p>box</p>
      </div>
    </div>
    <script>
      // 将真正的DOM转换为VNode
      function getVNode(node) {
        const nodeType = node.nodeType
        let _vnode = null
        if (nodeType === 1) {
          const nodeName = node.nodeName
          const attrs = node.attributes
          let _attrObj = {}
          for (let i = 0; i < attrs.length; i++) {
            _attrObj[attrs[i].nodeName] = attrs[i].nodeValue
          }
          _vnode = new VNode(nodeName, _attrObj, undefined, nodeType)

          // 考虑node的子元素
          const childNodes = node.childNodes
          for (let i = 0; i < childNodes.length; i++) {
            _vnode.appendChild(getVNode(childNodes[i]))
          }
        } else if (nodeType === 3) {
          _vnode = new VNode(undefined, undefined, node.nodeValue, nodeType)
        }
        return _vnode
      }
      // 将VNode转换为真正的DOM
      function parseVNode(vnode) {
        // 创建真实的DOM节点
        const type = vnode.type
        let _node = null
        if (type === 3) {
          // 创建文本节点
          return document.createTextNode(vnode.value)
        } else if (type === 1) {
          _node = document.createElement(vnode.tag)
          // 属性
          const data = vnode.data // 现在这个data是键值对
          Object.keys(data).forEach(key => {
            const attrName = key
            const attrValue = data[key]
            _node.setAttribute(attrName, attrValue)
          })

          // 创建子元素
          const children = vnode.children
          children.forEach(subvnode => {
            _node.appendChild(parseVNode(subvnode))
          })
          return _node
        }
      }
      const Mustache = /\{\{(.+?)\}\}/g
      // 根据路径访问对象成员
      function getValueByPath(obj, path) {
        const paths = path.split('.') // a.b.c
        // 先取到a.b，再取到a.b.c
        let res = obj
        let prop = ''
        // 如果没有值最后为undefined
        while ((prop = paths.shift())) {
          res = res[prop]
        }
        return res
      }
      // 让模板与数据结合
      function combine(vnode, data) {
        const _type = vnode.type
        const _data = vnode.data
        const _value = vnode.value
        const _tag = vnode.tag
        const _children = vnode.children

        let _vnode = null
        // 对文本节点的处理
        if (_type === 3) {
          _parsedValue = _value.replace(Mustache, (_, g) =>
            getValueByPath(data, g.trim())
          )
          _vnode = new VNode(_tag, _data, _parsedValue, _type)
        } else if (_type === 1) {
          // 元素节点
          _vnode = new VNode(_tag, _data, _value, _type)
          _children.forEach(_subvnode =>
            _vnode.appendChild(combine(_subvnode, data))
          )
        }
        return _vnode
      }
        
      class VNode {
        constructor(tag, data, value, type) {
          this.tag = tag && tag.toLowerCase()
          this.data = data
          this.value = value
          this.type = type
          this.children = []
        }
        appendChild(vnode) {
          this.children.push(vnode)
        }
      }

      class MyVue {
        constructor(options) {
          this._options = options
          this._data = options.data
          this._el = options.el
          const elm = document.querySelector(options.el) // 在Vue中这里是字符串，我们这里简化为DOM
          this._template = elm
          this._parent = elm.parentNode
          this.mount() // 挂载
        }
        mount() {
          // 需要提供一个render方法来生成虚拟DOM,引入Vue是可以传入自定义render方法的，该方法让用户提供自定义的VNode
          if (typeof this._options.render !== 'function') {
            this.render = this.createRenderFn() // 带有缓存
          }
          this.mountComponent()
        }
        mountComponent() {
          // 执行 mountComponent函数
          const mount = function() {
            this.update(this.render())
          }
          // 在Vue中其实是交给 watcher 来调用，现在就这样写
          mount.call(this)
        }
        /*
          在真正的 Vue中使用了二次提交的设计结构
          1.在页面中的DOM和虚拟DOM是一一对应的关系
          2.先由 AST 和数据生成VNode（这个是新产生的VNode）
          3.将原来的旧的VNode与新的VNode进行比较（使用diff算法），再更新（update）
        */
        // 这里是生成render函数，目的是缓存抽象语法树（现在这里我们先使用虚拟DOM来进行模拟）
        createRenderFn() {
          const ast = getVNode(this._template)
          // 在Vue中是直接：AST + DATA -> VNode

          // 我们这里做简化，将模板转换的直接的空的VNode转换为由数据的VNode
          return function() { // 带有缓存
            const _tmp = combine(ast, this._data)
            return _tmp
          }
        }

        // 将虚拟DOM渲染到页面中，diff算法就在这个地方
        update(vnode) {
          const realDOM = parseVNode(vnode)
          // 对这个过程简化，直接生成 DOM 通过替换的方式到页面中去，真实情况不是这样全部替换，而是通过diff算法一级一级比较然后改变原来的对象
          this._parent.replaceChild(realDOM, document.querySelector(this._el))
        }
      }

      const app = new MyVue({
        el: '#root',
        data: {
          name: '张三',
          age: 18,
          gender: '男'
        }
      })
    </script>
  </body>
</html>
```





### 18.7 响应式原理



**Vue的响应式基本有着下面几点：**



- 在使用 Vue 时候, 赋值属性获得属性都是直接使用的 Vue 实例（通过`this.xxx`获取，而不是`this._data.xxx`）。

- 在涉及属性值的时候, 页面的数据更新。





#### 18.7.1 属性描述符



在ES5之前，JavaScript 没有内置的机制来指定或者检查对象某个属性(property)的特性(characteristics)，比如某个属性是只读(readonly)的或者不能被枚举(enumerable)的。但是在 ES5之后，JavaScript 被赋予了这个能力，所有的对象属性都可以通过属性描述符(Property Descriptor)来指定。



```js
let myObject = {}

Object.defineProperty(myObject, 'a', {
  value: 2,
  writable: true, // 可写
  configurable: true, // 可配置
  enumerable: true // 可遍历
})
// 上面的定义等同于 myObject.a = 2;
// 所以如果不需要修改这三个特性，我们一般不会用 `Object.defineProperty`

console.log(myObject.a) // 2
```



**属性描述符的六个属性**



- value：属性值

- writable：是否允许赋值，

  true

   表示允许，否则该属性不允许赋值

  ```
  let myObject = {}
  
  Object.defineProperty(myObject, 'a', {
    value: 2,
    writable: false, // 不可写
    configurable: true,
    enumerable: true
  })
  
  myObject.a = 3 // 写入的值将会被忽略
  console.log(myObject.a) // 2
  ```

- get：返回属性值的函数。如果为 **undefined** 则直接返回描述符中定义的 **value** 值

- set：属性的赋值函数。如果为 **undefined** 则直接将赋值运算符右侧的值保存为属性值
  **注：**

- - 一旦同时使用了`get`和`set`，需要一个中间变量存储真正的值。

- - `set`和`writable:false`是不能共存的。

- configurable：如果为 

  true

  ，则表示该属性可以重新使用（

  ```js
  Object.defineProperty(...)
  ```

   ）定义描述符，或者从属性的宿主删除。缺省为 

  ```js
  true
  ```

  ```js
  let myObject = {
    a: 2
  }
  
  Object.defineProperty(myObject, 'a', {
    value: 4,
    writable: true,
    configurable: false, // 不可配置!
    enumerable: true
  })
  
  console.log(myObject.a) // 4
  myObject.a = 5
  // 因为最开始writable时true，所以不会影响到赋值
  console.log(myObject.a) // 5
  
  Object.defineProperty(myObject, 'a', {
    value: 6,
    writable: true,
    configurable: true,
    enumerable: true
  }) // TypeError
  ```

  注：

  一旦某个属性被指定为 

  ```
  configurable: false
  ```

  ，那么就不能从新指定为

  ```
  configurable: true
  ```

   了，这个操作是单向，不可逆的

  这个特性还会影响`delete` 操作的行为

  ```js
  let myObject = {
    a: 2
  }
  
  Object.defineProperty(myObject, 'a', {
    value: 4,
    writable: true,
    configurable: false, // 不可配置!
    enumerable: true
  })
  delete myObject.a
  console.log(myObject.a) // 4
  ```

- enumerable：如果为 

  true

  ，则表示遍历宿主对象时，该属性可以被遍历到（比如 

  ```
  for..in
  ```

   循环中）。缺省为 

  ```
  true
  ```

  ```js
  let myObject = {}
  
  Object.defineProperty(
    myObject,
    'a',
    // make `a` enumerable, as normal
    { enumerable: true, value: 2 }
  )
  
  Object.defineProperty(
    myObject,
    'b',
    // make `b` NON-enumerable
    { enumerable: false, value: 3 }
  )
  console.log(myObject.b) // 3
  console.log('b' in myObject) // true
  myObject.hasOwnProperty('b') // true
  
  // .......
  // 无法被遍历到
  for (let k in myObject) {
    console.log(k, myObject[k])
  }
  // "a" 2
  
  myObject.propertyIsEnumerable('a') // true
  myObject.propertyIsEnumerable('b') // false
  Object.keys(myObject) // ["a"]
  Object.getOwnPropertyNames(myObject) // ["a", "b"]
  ```

  可以看出，

  ```
  enumerable: false
  ```

   使得该属性从对象属性枚举操作中被隐藏，但

  ```
  Object.hasOwnProperty(...)
  ```

   仍然可以检测到属性的存在。另外，

  ```
  Object.propertyIsEnumerable(..)
  ```

   可以用来检测某个属性是否可枚举,

  ```
  Object.keys(...)
  ```

   仅仅返回可枚举的属性，而

  ```
  Object.getOwnPropertyNames(...)
  ```

   则返回该对象上的所有属性，包括不可枚举的



**注：**Object有专门操作属性的方法，在这里就不再多讲了





#### 18.7.2 Vue中使用属性描述符



在Vue中因为全部依赖的是响应式，所以直接使用会有命名冲突的问题，我们使用闭包来解决这个问题。



```js
const o = {
    name: '张三',
    age: '18',
    gender: '男'
}
// 简化后的版本
function defineRective(target, key, value, enumerable) {
    // 函数内部形成一个局部作用域，value只在内部使用（闭包，避免污染全局）
    Object.defineProperty(target, key, {
        configurable: true,
        enumerable: !!enumerable,
        get() {
            console.log(`读取 o 的 ${key} 属性`) // 额外
            return value
        },
        set(newValue) {
            console.log(`设置 o 的 ${key} 属性为: ${newValue}`) // 额外
            value = newValue
        }
    })
}

console.log(o) // {name: "张三", age: "18", gender: "男"}
// 将对象转换为响应式的，会将原来的键值覆盖掉
Object.keys(o).forEach(key => {
    defineRective(o, key, o[key], true)
})
console.log(o) // {}
```



但是，上面的只能对基本类型的数据进行响应式化，所以我们需要进行递归修改。



```js
const o = {
    name: '张三',
    age: '18',
    gender: '男',
    courses: [
        {
            name: '语文'
        },
        {
            name: '数学'
        }
    ]
}
// 简化后的版本
function defineRective(target, key, value, enumerable) {
    // 函数内部形成一个局部作用域，value只在内部使用（闭包，避免污染全局）
    if (
        typeof value === 'object' &&
        value !== null &&
        !Array.isArray(value)
    ) {
        // 非数组引用类型
        reactify(value)
    }

    Object.defineProperty(target, key, {
        configurable: true,
        enumerable: !!enumerable,
        get() {
            console.log(`获取${key}属性`)
            return value
        },
        set(newValue) {
            console.log(`设置${key}属性`)
            value = newValue
        }
    })
}
function reactify(o) {
    Object.keys(o).forEach(key => {
        // 将对象转换为响应式的，会将原来的键值覆盖掉
        /*
          1.判断这个属性是否为引用类型，是否是数组
          2.
          （1）如果是引用类型就递归，如果不是就不需要
          （2）如果是数组，需要循环数组，然后将数组里面的元素进行响应式话
        */
        // 数组
        if (Array.isArray(o[key])) {
            o[key].forEach(value => reactify(value))
        } else {
            // 对象或值类型
            defineRective(o, key, o[key], true)
        }
    })
}
reactify(o)
console.log(o)
```





#### 18.7.3 Vue中对数组方法的扩展



对于对象和数组添加新的属性时也需要做到响应式，在Vue官方文档中可以通过`$set`方法进行设置，都是使用递归来进行响应式化，但是数组的的一些改变原数组的方法在调用时也需要有响应式化，如：



- push

- pop

- shift

- unshift

- reverse

- sort

- splice



**我们需要在改变数组的数据的时候, 发出通知，将新加入的元素变成响应式的。**



**注意：**在 Vue 2.x 中，因为使用的是 Object 的`defineProperty`方法, 数组发生变化, 设置 length 没法通知 ( Vue 3 中使用 Proxy 语法 ES6 的语法解决了这个问题 )。





##### 18.7.3.1 扩展函数功能



**如果一个函数已经定义了, 但是我们需要扩展其功能, 我们一般的处理办法:**



1. 使用一个临时的函数名存储函数

1. 重新定义原来的函数

1. 定义扩展的功能

1. 调用临时的那个函数





##### 18.7.3.2 Vue中的拦截数组



如果要修改数组的方法，我们不能通过直接修改数组的`prototype`，因为这样会将所有的数组方法都改了，而是**修改要进行响应式化的数组的原型 ( `__proto__` )。**



```js
const ARRAY_METHOD = [
    'push',
    'pop',
    'shift',
    'unshift',
    'reverse',
    'sort',
    'splice'
]
// 原型式继承：修改原型链的结构
let arr = []
let array_method = Object.create(Array.prototype)
ARRAY_METHOD.forEach(method => {
    array_method[method] = function() {
        //调用原来的方法
        console.log(`调用拦截的${method}方法`)
        // 将数据进行响应式化
        const res = Array.prototype[method].apply(this, arguments)
        return res
    }
})
arr.__proto__ = array_method
/*
        Vue的源码中也做了这样的办法：
        1.如果浏览器支持__proto__就放原型上
        2.如果不支持Vue使用的混入的方法，Vue会挂载到当前对象上
*/
```



这样，在使用数组方法的时候就能够触发`console.log`了。





##### 18.7.3.3 Vue数组的响应式化



所以，在数组中要响应式需要再修改一下上面的`reactify`函数。同时，如果是直接用对象或者数组进行赋值，也需要响应式化，需要修改一下`defineRective`函数定义属性时候的`set`方法



**注意：**下面的代码在，直接赋值的响应式化只能够原来的值不是数组或者对象才行，数组和对象在一开始赋值的时候本身就不是一个响应式数据，而是它的成员或属性才是，所以直接赋值的时候并不会触发`set`方法，在之后会单独再进行修改。



```js
function defineRective(target, key, value, enumerable) {
    // 函数内部形成一个局部作用域，value只在内部使用（闭包，避免污染全局）
    if (
        typeof value === 'object' &&
        value !== null &&
        !Array.isArray(value)
    ) {
        // 非数组引用类型
        reactify(value)
    }

    Object.defineProperty(target, key, {
        configurable: true,
        enumerable: !!enumerable,
        get() {
            console.log(`获取${key}属性`)
            return value
        },
        set(newValue) {
            console.log(`设置${key}属性`)
            // 如果是数组等直接赋值，也需要响应式化
            value = newValue
            reactify(value)
        }
    })
}
function reactify(o) {
    Object.keys(o).forEach(key => {
        // 将对象转换为响应式的，会将原来的键值覆盖掉
        /*
          1.判断这个属性是否为引用类型，是否是数组
          2.
          （1）如果是引用类型就递归，如果不是就不需要
          （2）如果是数组，需要循环数组，然后将数组里面的元素进行响应式话
        */
        // 数组
        if (Array.isArray(o[key])) {
            // 现在的数组就是响应式
            o[key].__proto__ = array_method
            o[key].forEach(value => reactify(value))
        } else {
            // 对象或值类型
            defineRective(o, key, o[key], true)
        }
    })
}
```





##### 18.7.3.4 响应式刷新页面



将响应式读取数据与前面的模板页面相结合，就能够做到响应式刷新页面了。



**下面是集成上面代码的一个简易框架：**



```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="root">
      <p>{{name}}</p>
      <p>{{age}}</p>
      <p>{{gender}}</p>
      <div class="box">
        <p>box</p>
      </div>
    </div>
    <script>
      const ARRAY_METHOD = [
        'push',
        'pop',
        'shift',
        'unshift',
        'reverse',
        'sort',
        'splice'
      ]

      // 原型式继承：修改原型链的结构
      const array_method = Object.create(Array.prototype)

      ARRAY_METHOD.forEach(method => {
        array_method[method] = function() {
          // 将数据进行响应式化
          for (let i = 0; i < arguments.length; i++) {
            // 因为缺陷，这里无法传入vm
            reactify(arguments[i])
          }

          //调用原来的方法
          const res = Array.prototype[method].apply(this, arguments)
          return res
        }
      })

      // 简化后的版本
      function defineRective(target, key, value, enumerable) {
        // 函数内部形成一个局部作用域，value只在内部使用（闭包，避免污染全局）
        // 折中处理后的Vue实例
        const _this = this

        if (
          typeof value === 'object' &&
          value !== null &&
          !Array.isArray(value)
        ) {
          // 非数组引用类型
          reactify(value)
        }

        Object.defineProperty(target, key, {
          configurable: true,
          enumerable: !!enumerable,
          get() {
            console.log(`获取${key}属性`)
            return value
          },
          set(newValue) {
            console.log(`设置${key}属性`)
            value = newValue
            if (typeof value === 'object' && value !== null) {
              reactify(value)
            }
            // 进行模板刷新，因为要获取Vue实例，这里就通过传入参数的形式获取，真实的Vue是通过watcher来获取的，以后会有修改
            _this.mountComponent()
          }
        })
      }
      function reactify(o, vm) {
        Object.keys(o).forEach(key => {
          // 将对象转换为响应式的，会将原来的键值覆盖掉
          /*
          1.判断这个属性是否为引用类型，是否是数组
          2.
          （1）如果是引用类型就递归，如果不是就不需要
          （2）如果是数组，需要循环数组，然后将数组里面的元素进行响应式话
        */
          // 数组
          if (Array.isArray(o[key])) {
            // 现在的数组就是响应式
            o[key].__proto__ = array_method
            o[key].forEach(value => reactify(value, vm))
          } else {
            // 对象或值类型
            defineRective.call(vm, o, key, o[key], true)
          }
        })
      }
      // 将真正的DOM转换为VNode
      function getVNode(node) {
        const nodeType = node.nodeType
        let _vnode = null
        if (nodeType === 1) {
          const nodeName = node.nodeName
          const attrs = node.attributes
          let _attrObj = {}
          for (let i = 0; i < attrs.length; i++) {
            _attrObj[attrs[i].nodeName] = attrs[i].nodeValue
          }
          _vnode = new VNode(nodeName, _attrObj, undefined, nodeType)

          // 考虑node的子元素
          const childNodes = node.childNodes
          for (let i = 0; i < childNodes.length; i++) {
            _vnode.appendChild(getVNode(childNodes[i]))
          }
        } else if (nodeType === 3) {
          _vnode = new VNode(undefined, undefined, node.nodeValue, nodeType)
        }
        return _vnode
      }
      // 将VNode转换为真正的DOM
      function parseVNode(vnode) {
        // 创建真实的DOM节点
        const type = vnode.type
        let _node = null
        if (type === 3) {
          // 创建文本节点
          return document.createTextNode(vnode.value)
        } else if (type === 1) {
          _node = document.createElement(vnode.tag)
          // 属性
          const data = vnode.data // 现在这个data是键值对
          Object.keys(data).forEach(key => {
            const attrName = key
            const attrValue = data[key]
            _node.setAttribute(attrName, attrValue)
          })

          // 创建子元素
          const children = vnode.children
          children.forEach(subvnode => {
            _node.appendChild(parseVNode(subvnode))
          })
          return _node
        }
      }
      const Mustache = /\{\{(.+?)\}\}/g
      // 根据路径访问对象成员
      function getValueByPath(obj, path) {
        const paths = path.split('.') // a.b.c
        // 先取到a.b，再取到a.b.c
        let res = obj
        let prop = ''
        // 如果没有值最后为undefined
        while ((prop = paths.shift())) {
          res = res[prop]
        }
        return res
      }
      // 让模板与数据结合
      function combine(vnode, data) {
        const _type = vnode.type
        const _data = vnode.data
        const _value = vnode.value
        const _tag = vnode.tag
        const _children = vnode.children

        let _vnode = null
        // 对文本节点的处理
        if (_type === 3) {
          _parsedValue = _value.replace(Mustache, (_, g) =>
            getValueByPath(data, g.trim())
          )
          _vnode = new VNode(_tag, _data, _parsedValue, _type)
        } else if (_type === 1) {
          // 元素节点
          _vnode = new VNode(_tag, _data, _value, _type)
          _children.forEach(_subvnode =>
            _vnode.appendChild(combine(_subvnode, data))
          )
        }
        return _vnode
      }
      class VNode {
        constructor(tag, data, value, type) {
          this.tag = tag && tag.toLowerCase()
          this.data = data
          this.value = value
          this.type = type
          this.children = []
        }
        appendChild(vnode) {
          this.children.push(vnode)
        }
      }

      class MyVue {
        constructor(options) {
          this._options = options
          this._data = options.data
          reactify(this._data, this) // 先传入实例
          this._el = options.el
          const elm = document.querySelector(options.el) // 在Vue中这里是字符串，我们这里简化为DOM
          this._template = elm
          this._parent = elm.parentNode
          this.mount() // 挂载
        }
        mount() {
          // 需要提供一个render方法来生成虚拟DOM,引入Vue是可以传入自定义render方法的，该方法让用户提供自定义的VNode
          if (typeof this._options.render !== 'function') {
            this.render = this.createRenderFn() // 带有缓存
          }
          this.mountComponent()
        }
        mountComponent() {
          // 执行 mountComponent函数
          const mount = function() {
            this.update(this.render())
          }
          // 在Vue中其实是交给 watcher 来调用，现在就这样写
          mount.call(this)
        }
        /*
          在真正的 Vue中使用了二次提交的设计结构
          1.在页面中的DOM和虚拟DOM是一一对应的关系
          2.先由 AST 和数据生成VNode（这个是新产生的VNode）
          3.将原来的旧的VNode与新的VNode进行比较（使用diff算法），再更新（update）
        */
        // 这里是生成render函数，目的是缓存抽象语法树（现在这里我们先使用虚拟DOM来进行模拟）
        createRenderFn() {
          const ast = getVNode(this._template)
          // 在Vue中是直接：AST + DATA -> VNode

          // 我们这里做简化，将模板转换的直接的空的VNode转换为由数据的VNode
          return function() {
            const _tmp = combine(ast, this._data)
            return _tmp
          }
        }

        // 将虚拟DOM渲染到页面中，diff算法就在这个地方
        update(vnode) {
          const realDOM = parseVNode(vnode)
          // 对这个过程简化，直接生成 DOM 通过替换的方式到页面中去，真实情况不是这样全部替换，而是通过diff算法一级一级比较然后改变原来的对象
          this._parent.replaceChild(realDOM, document.querySelector(this._el))
        }
      }

      const app = new MyVue({
        el: '#root',
        data: {
          name: '张三',
          age: 18,
          gender: '男',
          datas: {
            info: '11'
          }
        }
      })
    </script>
  </body>
</html>
```





##### 18.7.3.5 代理方法



代理方法的实现就是将Vue上的`this._data`上的成员映射到`this`上。由于需要在更新数据的时候，更新页面的内容，所有`this._data`访问的成员与`this`访问的成员应该是同一个成员。



**我们现在对我们自己的简易框架做一点修改：**



```js
class MyVue {
    constructor(options) {
        this._options = options
        this._data = options.data
        this._el = options.el
        const elm = document.querySelector(options.el) // 在Vue中这里是字符串，我们这里简化为DOM
        this._template = elm
        this._parent = elm.parentNode
        // <------------------------------>
        this.initData() // 将data进行响应式转换，代理
        // <------------------------------>
        this.mount() // 挂载
    }
    mount() {
        // 需要提供一个render方法来生成虚拟DOM,引入Vue是可以传入自定义render方法的，该方法让用户提供自定义的VNode
        if (typeof this._options.render !== 'function') {
            this.render = this.createRenderFn() // 带有缓存
        }
        this.mountComponent()
    }
    mountComponent() {
        // 执行 mountComponent函数
        const mount = function() {
            this.update(this.render())
        }
        // 在Vue中其实是交给 watcher 来调用，现在就这样写
        mount.call(this)
    }
    /*
          在真正的 Vue中使用了二次提交的设计结构
          1.在页面中的DOM和虚拟DOM是一一对应的关系
          2.先由 AST 和数据生成VNode（这个是新产生的VNode）
          3.将原来的旧的VNode与新的VNode进行比较（使用diff算法），再更新（update）
        */
    // 这里是生成render函数，目的是缓存抽象语法树（现在这里我们先使用虚拟DOM来进行模拟）
    createRenderFn() {
        const ast = getVNode(this._template)
        // 在Vue中是直接：AST + DATA -> VNode

        // 我们这里做简化，将模板转换的直接的空的VNode转换为由数据的VNode
        return function() {
            const _tmp = combine(ast, this._data)
            return _tmp
        }
    }

    // 将虚拟DOM渲染到页面中，diff算法就在这个地方
    update(vnode) {
        const realDOM = parseVNode(vnode)
        // 对这个过程简化，直接生成 DOM 通过替换的方式到页面中去，真实情况不是这样全部替换，而是通过diff算法一级一级比较然后改变原来的对象
        this._parent.replaceChild(realDOM, document.querySelector(this._el))
    }
    // <------------------------------------------->
    initData() {
        // 遍历this._data的成员，将属性转换为响应式，同时代理到实例上
        Object.keys(this._data).forEach(key => {
            // 响应式化
            reactify(this._data, this)
            // 代理
            /*
              将this._data[key]映射到this[key]上，就是提供代理，在访问this[key]的时候相当于是在访问this._data[key]
            */
            proxy(this, '_data', key)
        })
    }
    // <------------------------------------------->
}
// <------------------------------------------->
function proxy(target, prop, key) {
    Object.defineProperty(target, key, {
        enumerable: true,
        configurable: true,
        get() {
            return target[prop][key]
        },
        set(newValue) {
            target[prop][key] = newValue
        }
    })
}
// <------------------------------------------->
```





### 18.8 发布订阅模式



**发布订阅模式的目标是通过解耦, 让各个模块之间没有紧密的联系。**



在之前我们的简单模板中的处理办法是属性在更新的 时候调用`mountComponent`方法。但是这种方法目前还存在着问题，



现在调用该方法更新的是全部的页面，也就是当前虚拟 DOM 对应的页面 DOM。



**但是，在 Vue 中, 整个的更新是按照组件为单位进行断, 已节点为单位进行更新：**



- 如果代码中没有自定义组件，那么在比较算法的时候，会将全部的模板对应的虚拟 DOM 进行比较。

- 如果代码中含有自定义组件，那么在比较算法的时候，就会判断更新的是哪一些组件中的属性，只会判断更新数据的组件，其他组件不会更新。



**所以，我们的目标是如果修改了什么属性，就尽可能只更新这些属性对应的页面 DOM。**



**发布订阅模式 ( 形式不局限于函数, 形式可以是对象等 ) ：**



1. 中间的**全局的容器**，用来**存储**可以被触发的东西（函数, 对象）。

1. 需要一个方法，可以往容器中**传入**东西（函数, 对象）。

1. 需要一个方法，可以将容器中的东西取出来**使用**（函数调用, 对象的方法调用）。





#### 18.8.1 事件模型



**总的来说发布订阅模式的一种事件就是创立一个事件模型，当需要更新的时候触发对应的事件实现更新。**



该事件模型需要做到以下几点：



- 有一个`event`对象。

- 有`on`，`off`，`emit`等绑定、取消、触发事件的方法。

- 通过`event.on('事件名', 处理函数)`订阅事件，可以同时对同一个事件订阅多个处理函数。

- 通过`event.off()`方法传入0、1、2个参数可以分别移除所有处理函数、对应事件名的所有处理函数和对应事件名的对应处理函数。

- 通过`event.emit('事件名', 参数)`, 先前注册的事件处理函数就会依次调用。



```js
const event = (function() {
    const eventObjs = {}
    return {
        /*
            注册事件：可以连续注册，可以注册多个事件
          */
        on(type, handler) {
            ;(eventObjs[type] || (eventObjs[type] = [])).push(handler)
        },
        /*
            移除事件：
            1.如果没有参数，移除所有事件
            2.如果只带有事件名参数，就移除这个事件名下的所有事件
            3.如果带有两个参数，那么就移除某一个事件的具体函数
          */
        off(type, handler) {
            if (arguments.length === 0) {
                // 没有参数，移除所有事件
                eventObjs = {}
            } else if (arguments.length === 1) {
                eventObjs[type] = []

                //只有事件类型，移除该事件的所有处理函数
            } else if (arguments.length === 2) {
                // 移除type事件的handler处理函数
                // 使用循环移除所有的改函数对应的type事件
                const _events = eventObjs[type]
                if (!events) {
                    return
                }
                // 循环数组，倒着防止序号影响
                for (let i = _events.length - 1; i >= 0; i--) {
                    if (_events[i] === handler) {
                        _events.splice(i, 1)
                    }
                }
            }
        },
        /*
            发射事件：触发事件，包装事件，传递给事件处理函数
          */
        emit(type) {
            const _events = eventObjs[type]
            const args = Array.prototype.slice.call(arguments, 1) // 获得arguments从1开始后的所有参数，返回数组
            if (!_events) {
                return
            }
            for (let i = 0; i < _events.length; i++) {
                _events[i].apply(null, args)
            }
        }
    }
})()

/*
    测试
*/

//注册事件
event.on('click', () => {
    console.log('click event')
})
setTimeout(() => {
    event.emit('click')
}, 2000)
```





#### 18.8.2 Vue中的模型



**页面中的变更（diff）是以组件为单位的：**



- 如果页面中只有一个组件 ( Vue 实例 ), 不会有性能损失

- 但是如果页面中有多个组件（多 watcher 的一种情况），第一次会有多个组件的 watcher 存入到全局watcher容器中。如果修改了局部的数据（例如其中一个组件的数据），表示只会对该组件进行 diff 算法, 也就是说只会重新生成该组件的抽象语法树，只会访问该组件的 watcher，然后调用完改 watcher 后，再次往全局存储的该组件的新的 watcher ，页面更新的时候也就只需要更新一部分。





### 18.9 Flow



Flow是一个静态的检测工具，语法与TypeScript类似，在 Vue 2.x 中是使用它来进行编码的，具体的用法可查看[官方文档](https://flow.org/en/docs/getting-started/)





### 18.10 Vue的MVVM 模式



![image-20200617161846845](./img/8.png)