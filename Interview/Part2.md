# 前端面试题集之JS



## 1. js的new操作符

new 操作符新建了一个空对象，这个对象原型指向构造函数的prototype，执行构造函数后返回这个对象。



## 2. 改变函数内部this的指向函数

通过apply和call改变函数的this指向，他们两个函数的第一个参数都是一样的表示要改变指向的那个对象，第二个参数，apply是数组，而call则是arg1,arg2...这种形式。

call()方法传递实参只需要在第一个参数后面依次用,(逗号)隔开

```js
var obj={num:1};
function fun(number1,number2){
    console.log(this,num+number1+number2);
}
fun.call(obj,10,20);//31
```

apply()方法需要将实参封装到一个数组中统一传递

```js
var obj={num:1};
function fun(number1,number2){
    console.log(this,num+number1+number2);
}
fun.apply(obj,[10,20]);//31
```



通过bind改变this作用域会返回一个新的函数，这个函数不会马上执行。与call()和apply()方法不同,使用了bind方法只会将复制后的函数作为返回值传递回来,并不会调用函数

```js
function Person(age){
    this.age=age;
}
Person.prototype.play=function(){
    console.log(this);
    console.log(this.age);
}

function Student(age){
    this.age=age;
}
var per=new Person(10);
var stu=new Student(20)；

var fun=per.play.bind(stu);
fun();//this指向为stu,this.age的值为20
```



```js
function f1(x,y){
console.log(x+y)；
}
var ff=f1.bind(null,10,20)//在复制的时候传入实参
ff();
Var ff=f1.bind(null);
ff(10,20);//在调用的时候传入参数
```



## 3. 闭包

**闭包的概念**:函数A中,有一个函数B,函数B中可以访问函数A中定义的变量或者数据,此时形成了闭包(这句话暂时不严谨)

**闭包的模式**:分为函数模式的闭包和对象模式的闭包(函数中有一个对象)

**闭包的作用**:缓存数据,延迟作用域链,闭包使用的父函数的变量或参数会被永久保存,直到页面关闭

**闭包的优点和缺点**:缓存数据(优点也是缺点,没有及时的释放数据) 局部变量在函数中被函数使用后会被自动的释放,而闭包后,里面的局部变量的使用作用域链就会被延长

**闭包的形成条件**: 如果满足以下两点,那么可以把内部函数称为闭包

- 函数嵌套函数

- 内部函数使用父函数的变量或参数



## 4. eval

它的功能是将对应的字符串解析成js并执行，应该避免使用js，因为非常消耗性能（2次，一次解析成js，一次执行）



## 5. Commonjs,AMD和CMD

一个模块是能实现特定功能的文件，有了模块就可以方便的使用别人的代码，想要什么功能就能加载什么模块。

### 5.1 Commonjs

我们先从CommonJS谈起，因为在网页端没有模块化编程只是页面JavaScript逻辑复杂，但也可以工作下去，在服务器端却一定要有模块，所以虽然JavaScript在web端发展这么多年，第一个流行的模块化规范却由服务器端的JavaScript应用带来，CommonJS规范是由NodeJS发扬光大，这标志着JavaScript模块化编程正式登上舞台。

1、定义模块
根据CommonJS规范，一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为global对象的属性

2、模块输出：
模块只有一个出口，module.exports对象，我们需要把模块希望输出的内容放入该对象

3、加载模块：
加载模块使用require方法，该方法读取一个文件并执行，返回文件内部的module.exports对象

看个例子

```js
//模块定义 myModel.js

var name = 'Byron';

function printName(){
    console.log(name);
}

function printFullName(firstName){
    console.log(firstName + name);
}

module.exports = {
    printName: printName,
    printFullName: printFullName
}

//加载模块

var nameModule = require('./myModel.js');

nameModule.printName();
```

不同的实现对require时的路径有不同要求，一般情况可以省略js拓展名，可以使用相对路径，也可以使用绝对路径，甚至可以省略路径直接使用模块名（前提是该模块是系统内置模块）

**尴尬的浏览器**

仔细看上面的代码，会发现require是同步的。模块系统需要同步读取模块文件内容，并编译执行以得到模块接口。

这在服务器端实现很简单，也很自然，然而， 想在浏览器端实现问题却很多。

浏览器端，加载JavaScript最佳、最容易的方式是在document中插入script 标签。但脚本标签天生异步，传统CommonJS模块在浏览器环境中无法正常加载。

解决思路之一是，开发一个服务器端组件，对模块代码作静态分析，将模块与它的依赖列表一起返回给浏览器端。 这很好使，但需要服务器安装额外的组件，并因此要调整一系列底层架构。

另一种解决思路是，用一套标准模板来封装模块定义，但是对于模块应该怎么定义和怎么加载，又产生了分歧



### 5.2 AMD

AMD 即Asynchronous Module Definition，中文名是异步模块定义的意思。它是一个在浏览器端模块化开发的规范

由于不是JavaScript原生支持，使用AMD规范进行页面开发需要用到对应的库函数，也就是大名鼎鼎RequireJS，实际上AMD 是 RequireJS 在推广过程中对模块定义的规范化的产出

requireJS主要解决两个问题

1、多个js文件可能有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
2、js加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应时间越长
看一个使用requireJS的例子

```js
// 定义模块 myModule.js
define(['dependency'], function(){
    var name = 'Byron';
    function printName(){
        console.log(name);
    }

    return {
        printName: printName
    };
});

// 加载模块
require(['myModule'], function (my){
　 my.printName();
});
```

**语法**

requireJS定义了一个函数 define，它是全局变量，用来定义模块

define(id?, dependencies?, factory);

1. id：可选参数，用来定义模块的标识，如果没有提供该参数，脚本文件名（去掉拓展名）
2. dependencies：是一个当前模块依赖的模块名称数组
3. factory：工厂方法，模块初始化要执行的函数或对象。如果为函数，它应该只被执行一次。如果是对象，此对象应该为模块的输出值
   在页面上使用require函数加载模块

require([dependencies], function(){});
require()函数接受两个参数

1. 第一个参数是一个数组，表示所依赖的模块
2. 第二个参数是一个回调函数，当前面指定的模块都加载成功后，它将被调用。加载的模块会以参数形式传入该函数，从而在回调函数内部就可以使用这些模块

require()函数在加载依赖的函数的时候是异步加载的，这样浏览器不会失去响应，它指定的回调函数，只有前面的模块都加载成功后，才会运行，解决了依赖性的问题。



### 5.3 CMD

CMD 即Common Module Definition通用模块定义，CMD规范是国内发展出来的，就像AMD有个requireJS，CMD有个浏览器的实现SeaJS，SeaJS要解决的问题和requireJS一样，只不过在模块定义方式和模块加载（可以说运行、解析）时机上有所不同
**语法**
Sea.js 推崇一个模块一个文件，遵循统一的写法
define(id?, deps?, factory)
因为CMD推崇

1. 一个文件一个模块，所以经常就用文件名作为模块id
2. CMD推崇依赖就近，所以一般不在define的参数中写依赖，在factory中写

factory是一个函数，有三个参数，function(require, exports, module)

1. require 是一个方法，接受 模块标识 作为唯一参数，用来获取其他模块提供的接口：require(id)
2. exports 是一个对象，用来向外提供模块接口
3. module 是一个对象，上面存储了与当前模块相关联的一些属性和方法

看个例子：

```js
// 定义模块  myModule.js
define(function(require, exports, module) {
  var $ = require('jquery.js')
  $('div').addClass('active');
});

// 加载模块
seajs.use(['myModule.js'], function(my){

});
```



### 5.4 AMD与CMD区别

最明显的区别就是在模块定义时对依赖的处理不同

**1、AMD推崇依赖前置，在定义模块的时候就要声明其依赖的模块**
**2、CMD推崇就近依赖，只有在用到某个模块的时候再去require**
这种区别各有优劣，只是语法上的差距，而且requireJS和SeaJS都支持对方的写法

AMD和CMD最大的区别是对依赖模块的执行时机处理不同，注意不是加载的时机或者方式不同

很多人说requireJS是异步加载模块，SeaJS是同步加载模块，这么理解实际上是不准确的，其实加载模块都是异步的，只不过AMD依赖前置，js可以方便知道依赖模块是谁，立即加载，而CMD就近依赖，需要使用把模块变为字符串解析一遍才知道依赖了那些模块，这也是很多人诟病CMD的一点，牺牲性能来带来开发的便利性，实际上解析模块用的时间短到可以忽略

为什么我们说两个的区别是依赖模块执行时机不同，为什么很多人认为ADM是异步的，CMD是同步的（除了名字的原因。。。）

同样都是异步加载模块，AMD在加载模块完成后就会执行改模块，所有模块都加载执行完后会进入require的回调函数，执行主逻辑，这样的效果就是依赖模块的执行顺序和书写顺序不一定一致，看网络速度，哪个先下载下来，哪个先执行，但是主逻辑一定在所有依赖加载完成后才执行

CMD加载完某个依赖模块后并不执行，只是下载而已，在所有依赖模块加载完成后进入主逻辑，遇到require语句的时候才执行对应的模块，这样模块的执行顺序和书写顺序是完全一致的

这也是很多人说AMD用户体验好，因为没有延迟，依赖模块提前执行了，CMD性能好，因为只有用户需要的时候才执行的原因