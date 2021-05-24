# 前端面试题集之HTML&CSS



## 1. 高度塌陷问题



### 1.1 文档流

文档流处在网页的最底层，它表示的是一个页面中的位置，我们所创建的元素默认都处在文档流中

元素在文档流中的特点：

**块元素**

1. 块元素在文档流中会独占一行，块元素会自上向下排列。
2. 块元素在文档流中默认宽度是父元素的100%
3. 块元素在文档流中的高度默认被内容撑开

**内联元素**

1. 内联元素在文档流中只占自身的大小，会默认从左向右排列，如果一行中不足以容纳所有的内联元素，则换到下一行，继续自左向右。

2. 在文档流中，内联元素的宽度和高度默认都被内容撑开

   

### 1.2 浮动解释

块元素在文档流中默认垂直排列，所以这个三个div自上至下依次排开，如果希望块元素在页面中水平排列，可以使块元素脱离文档流

**使用float来使元素浮动，从而脱离文档流**

可选值： none，默认值，元素默认在文档流中排列 left，元素会立即脱离文档流，向页面的左侧浮动 right，元素会立即脱离文档流，向页面的右侧浮动

注意：

1. 当为一个元素设置浮动以后（float属性是一个非none的值），元素会立即脱离文档流，元素脱离文档流以后，它下边的元素会立即向上移动
2. 元素浮动以后，会尽量向页面的左上或这是右上漂浮，**直到遇到父元素的边框或者其他的浮动元素**
3. **如果浮动元素上边是一个没有浮动的块元素，则浮动元素不会超过块元素**
4. **浮动的元素不会超过他上边的兄弟元素**，最多最多一边齐
5. **浮动的元素不会盖住文字**，文字会自动环绕在浮动元素的周围，所以我们可以通过浮动来设置文字环绕图片的效果
6. 在文档流中，子元素的宽度默认占父元素的全部
7. 当元素设置浮动以后，会完全脱离文档流，**块元素脱离文档流以后，高度和宽度都被内容撑开**
8. 开启span的浮动，**内联元素脱离文档流以后会变成块元素**（内联元素本身设置宽高没有意义）



### 1.3 高度塌陷问题来由

在文档流中，父元素的高度默认是被子元素撑开的，也就是子元素多高，父元素就多高。

但是当为子元素设置浮动以后，子元素会完全脱离文档流，此时将会导致子元素无法撑起父元素的高度，导致父元素的高度塌陷。

由于父元素的高度塌陷了，则父元素下的所有元素都会向上移动，这样将会导致页面布局混乱。



### 1.4 解决高度塌陷

#### 1.4.1 直接法

​	我们可以将**父元素的高度写死**，以避免塌陷的问题出现，但是一旦高度写死，父元素的高度将不能自动适应子元素的高度，所以这种方案是**不推荐使用**的。

#### 1.4.2 BFC

根据W3C的标准，在页面中元素都一个隐含的属性叫做Block Formatting Context，简称**BFC**，该属性可以设置打开或者关闭，默认是关闭的。

**块级格式化上下文，用于清楚浮动，防止margin重叠等**

当开启元素的BFC以后，元素将会具有如下的特性：

1. 父元素的垂直外边距不会和子元素重叠
2. 开启BFC的元素不会被浮动元素所覆盖
3. 开启BFC的元素可以包含浮动的子元素

**如何开启元素的BFC**

1. 设置元素浮动，使用这种方式开启，虽然可以撑开父元素，但是会导致父元素的宽度丢失，而且使用这种方式也会导致下边的元素上移，不能解决问题
2. 设置元素绝对定位
3. 设置元素的display为inline-block，able-cell，table-caption，flex，inline-flex，可以解决问题，但是比如inline-block会导致宽度丢失，不推荐使用这种方式
4. **将元素的overflow设置为一个非visible的值**，此为推荐方式：将overflow设置为hidden是副作用最小的开启BFC的方式。

但是在IE6及以下的浏览器中并不支持BFC，所以使用这种方式不能兼容IE6。在IE6中虽然没有BFC，但是具有另一个隐含的属性叫做hasLayout，该属性的作用和BFC类似，所在IE6浏览器可以通过开hasLayout来解决该问题

开启方式很多，我们直接使用一种副作用最小的：

直接将元素的zoom设置为1即可

zoom表示放大的意思，后边跟着一个数值，写几就将元素放大几倍 zoom:1 表示不放大元素，但是通过该样式可以开启hasLayout zoom这个样式，只在IE中支持，其他浏览器都不支持

#### 1.4.3 清楚浮动

##### 清楚浮动介绍

我们有时希望清除掉其他元素浮动对当前元素产生的影响，这时可以使用clear来完成功能

clear可以用来清除其他浮动元素对当前元素的影响

可选值：

none，默认值，不清除浮动

left，清除左侧浮动元素对当前元素的影响

right，清除右侧浮动元素对当前元素的影响

both，清除两侧浮动元素对当前元素的影响

##### 解法

可以直接在高度塌陷的父元素的最后，添加一个空白的div

由于这个div并没有浮动，所以他是可以撑开父元素的高度的，然后在对其进行清除浮动，这样可以通过这个空白的div来撑开父元素的高度，

基本没有副作用，使用这种方式虽然可以解决问题，但是会在页面中添加多余的结构。

```css
/*通过after伪类，选中box1的后边*/
/*
* 可以通过after伪类向元素的最后添加一个空白的块元素，然后对其清除浮动，
* 	这样做和添加一个div的原理一样，可以达到一个相同的效果，
* 	而且不会在页面中添加多余的div，这是我们最推荐使用的方式，几乎没有副作用
*/

.clearfix::after{
    /*添加一个内容*/
    content: "";
    /*转换为一个块元素*/
    display: table;
    /*清除两侧的浮动*/
    clear: both;
}


/*
* 在IE6中不支持after伪类,
* 	所以在IE6中还需要使用hasLayout来处理
*/
.clearfix{
	zoom:1;
}
```





## 2. 定位

### 2.1 Position

**定位指的就是将指定的元素摆放到页面的任意位置**，通过定位可以任意的摆放元素

通过position属性来设置元素的定位

可选值：


 1. `static`：默认值，元素没有开启定位
 2. `relative`：开启元素的相对定位
 3. `absolute`：开启元素的绝对定位
 4. `fixed`：开启元素的固定定位（也是绝对定位的一种）



当开启了元素的定位（position属性值是一个非static的值）时，可以通过left right top bottom四个属性来设置元素的偏移量

`left`：元素相对于其定位位置的左侧偏移量

`right`：元素相对于其定位位置的右侧偏移量

`top`：元素相对于其定位位置的上边的偏移量

`bottom`：元素相对于其定位位置下边的偏移量

通常偏移量只需要使用两个就可以对一个元素进行定位，一般选择水平方向的一个偏移量和垂直方向的偏移量来为一个元素进行定位

### 2.2 相对定位

当元素的position属性设置为relative时，则开启了元素的相对定位

1. 当开启了元素的相对定位以后，而不设置偏移量时，元素不会发生任何变化
2. **相对定位是相对于元素在文档流中原来自身的位置进行定位**
3. **相对定位的元素不会脱离文档流**
4. **相对定位会使元素提升一个层级**
5. **相对定位不会改变元素的性质，块还是块，内联还是内联**

### 2.3 绝对定位

当position属性值设置为absolute时，则开启了元素的绝对定位

绝对定位：

1. **开启绝对定位，会使元素脱离文档流**
2. 开启绝对定位以后，如果不设置偏移量，则元素的位置不会发生变化
3. 绝对定位是**相对于离他最近的开启了定位的祖先元素进行定位**的（一般情况，开启了子元素的绝对定位都会同时开启父元素的相对定位），**如果所有的祖先元素都没有开启定位，则会相对于浏览器窗口进行定位**
4. **绝对定位会使元素提升一个层级**
5. 绝对定位会改变元素的性质，**内联元素变成块元素，块元素的宽度和高度默认都会被内容撑开**

### 2.4 固定定位

当元素的position属性设置fixed时，则开启了元素的固定定位

固定定位也是一种绝对定位，它的大部分特点都和绝对定位一样

不同的是：

1. 固定定位永远都会相对于浏览器窗口进行定位
2. 固定定位会固定在浏览器窗口某个位置，不会随滚动条滚动
3. IE6不支持固定定位



## 3. Flex布局

### 3.1 基本用法

**弹性盒子由display申明,通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器**

弹性容器内包含了一个或多个弹性子元素

**设置弹性盒子时需要用到的属性:**

| 属性            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| display         | 指定 HTML  元素盒子类型。                                    |
| flex-direction  | 指定了弹性容器中子元素的排列方式                             |
| justify-content | 设置弹性盒子元素在主轴（横轴）方向上的对齐方式。             |
| align-items     | 设置弹性盒子元素在侧轴（纵轴）方向上的对齐方式。             |
| flex-wrap       | 设置弹性盒子的子元素超出父容器时是否换行。                   |
| align-content   | 修改  flex-wrap 属性的行为，类似align-items, 但不是设置子元素对齐，而是设置行对齐 |
| flex-flow       | flex-direction  和 flex-wrap 的简写                          |
| order           | 设置弹性盒子的子元素排列顺序。                               |
| align-self      | 在弹性子元素上使用。覆盖容器的  align-items 属性。           |
| flex            | 设置弹性盒子的子元素如何分配空间,下面三个属性的简写。        |
| flex-grow       | 定义项目的放大比例                                           |
| flex-shrink     | 定义项目的缩小比例                                           |
| flex-basis      | 定义项目对空间的分配行为                                     |

### 3.2 父元素设置项

#### 3.2.1 flex-direction

**flex-direction属性定义弹性盒子中项目的主轴方向**,弹性盒模型将盒子中的内容通过主轴和侧轴进行显示

主轴默认是水平从左向右的,侧轴默认垂直从上到下

| 值             | 描述                                           |
| -------------- | ---------------------------------------------- |
| row            | 默认值。灵活的项目将水平显示，正如一个行一样。 |
| row-reverse    | 与 row  相同，但是以相反的顺序。               |
| column         | 灵活的项目将垂直显示，正如一个列一样。         |
| column-reverse | 与 column  相同，但是以相反的顺序。            |
| initial        | 设置该属性为它的默认值。                       |
| inherit        | 从父元素继承该属性。                           |

####  3.2.2 justify-content

**justify-content 用于设置或检索弹性盒子元素在主轴方向上的对齐方式**

默认值是flex-start,让项目位于弹性盒子的开头

| 值            | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| flex-start    | 默认值。项目位于容器的开头                                   |
| flex-end      | 项目位于容器的结尾。                                         |
| center        | 项目位于容器的中心。                                         |
| space-between | 项目位于各行之间留有空白的容器内。先将盒子的一行的两端占据,再将剩下的空间平分 |
| space-around  | 项目位于各行之前、之间、之后都留有空白的容器内。将盒子的一行完全平分 |
| initial       | 设置该属性为它的默认值                                       |
| inherit       | 从父元素继承该属性                                           |

#### 3.2.3 align-items

**align-items属性定义了项目在侧轴上的对齐方式(aligin-items主要支持单行项目)**

默认值是stretch,当子元素没有在侧轴方向定义宽或高的具体长度或者长度为auto时拉伸子元素的宽度或高度到整个侧轴的长度

| 值         | 描述                                           |
| ---------- | ---------------------------------------------- |
| stretch    | 默认。  拉伸元件以适应容器。                   |
| center     | 中心元素在容器内。                             |
| flex-start | 位置元素在容器的开头。                         |
| flex-end   | 位置元素在容器的末端。                         |
| baseline   | 位置元素在容器的文本基线。将子元素类的文字对齐 |
| initial    | 设置为默认值。                                 |
| inherit    | 从其父元素继承此属性。                         |

**注意:如果align-items的值表示默认值stretch而且子元素又没有给具体的宽高,它的大小由里面的内容撑开**

#### 3.2.4 flex-wrap

**flex-wrap属性规定了flex盒子在主轴上单行超出是否换行**

默认值是nowrap不换行

| 值           | 描述                                                     |
| ------------ | -------------------------------------------------------- |
| nowrap       | 默认值。规定灵活的项目不拆行或不拆列。                   |
| wrap         | 规定灵活的项目在必要的时候拆行或拆列。                   |
| wrap-reverse | 规定灵活的项目在必要的时候拆行或拆列，但是以相反的顺序。 |
| initial      | 设置该属性为它的默认值。                                 |
| initial      | 设置该属性为它的默认值。                                 |

**注意:**

在弹性盒子中因为flex-wrap的默认值是nowrap

如果设置了子元素的宽高超出了弹性盒子的总范围的时候会对子元素的大小进行弹性压缩,让超出的子元素等比例缩小到一行

**但是如果子元素里面有文字的时候**,最多子元素只能被压缩到文字的大小,因为文字不能被弹性压缩,只能通过font-size来设置,被压缩到文字大小后就会超出弹性盒子

**注:上面两个属性用flex-flow代替的时候flex-direction写在前面,flex-wrap写在后面**

#### 3.2.5 align-content

**align-content定义了多行子元素在侧轴上的对齐方式**

默认值是stretch,效果和align-items的相同,只不过是多行子元素进行平分整个侧轴长度

| 值            | 描述                                             |
| ------------- | ------------------------------------------------ |
| stretch       | 默认值。项目被拉伸以适应容器。                   |
| center        | 项目位于容器的中心。                             |
| flex-start    | 项目位于容器的开头。                             |
| flex-end      | 项目位于容器的结尾。                             |
| space-between | 项目位于各行之间留有空白的容器内。               |
| space-around  | 项目位于各行之前、之间、之后都留有空白的容器内。 |
| initial       | 设置该属性为它的默认值                           |
| inherit       | 从父元素继承该属性。                             |

**align-items和align-content的异同**：

- align-items和align-content有相同的功能，不过不同点是align-items是用来让每一个单行的容器居中而不是让整个容器居中
- 所以对于只有一行的flex元素，align-content是没有效果的，只有用align-items才能达到预期的效果
- 如果是多行flex元素,至于使用align-content才能让所有的flex元素在侧轴方向上面有类似justify-content在主     轴上的居中效果,而使用align-items时两个flex元素间总是有间隙

**上面是针对于整个容器的属性,现在是针对项目上的属性**



### 3.3 子元素设置项

#### 3.3.1 order

**order属性设置项目中的子元素在它那一行中主轴的排列顺序**

默认是每一个子元素都是0,数值越小排序越靠前

**注:该属性接受负值,且接受的值是整数**

#### 3.3.2 flex-grow

**flex-grow属性设置项目中的子元素在主轴上还有剩余的空间的时候通过设置一个数字来获取对于剩余空间的占比**

默认值是0

**具体用法**:会将所有子元素的flex-grow属性的数字加起来然后用各自的flex-grow的数字除以这个数就是每个子元素再分配得剩余空间大小的量

**公式: 该元素分得剩余空间 = 该元素的flex-grow值 / 所有flex-grow值之和剩余空间大小**

**注:该属性不接受负值,允许接受浮点数**

#### 3.3.3 flex-shrink

flex-shrink属性设置项目中的子元素在主轴上空间不足(这里flex-wrap没有设置为wrap)的时候,通过设置一个数字

进行对自身比例的缩小从而使得flex-shrink为0的子元素保持其本身设置的大小,该属性的默认值也是0

**具体用法**:会将所有子元素的flex-shrink属性的数字加起来然后用各自的flex-shrink的数字除以这个数就是每个子元素对于超出弹性盒子容积空间占比要缩小的量

**公式:该元素缩小空间=该元素的flex-shrink值/所有flex-shrink值之和超出弹性盒子空间大小**

**注:该属性不接受负值,允许接受浮点数**

#### 3.3.4 flex-basis

flex-basis属性定义项目对空间分配行为时,项目的实际大小(这个属性会和width和height等属性起冲突,在弹性盒子中有这个属性width或height将会无效),同时只要用这个属性设置了固定的大小,该元素就不会受到扩大或者收缩的影响

**合法值："auto"、"inherit" 或一个后跟 "%"、"px"、"em" 或任何其他长度单位的数字**

**注意:**

- **如果该元素占据的那一行占满了弹性盒子长度,那么后面的元素会自动到下一行**
- **有这个属性的元素的最大长度不能超过弹性盒子长度**

**注意:上面三个属性用flex代替的时候用flex-grow flex-shrink flex-basis 的顺序,默认值为0 1 auto**

#### 3.3.5 align-self

**align-self 属性定义flex子项单独在侧轴方向上的对齐方式**,默认值是auto，继承父元素的align-items属性的值

| 值         | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| auto       | 默认值。元素继承了它的父容器的  align-items 属性。如果没有父容器则为 "stretch"。 |
| stretch    | 元素被拉伸以适应容器。                                       |
| center     | 元素位于容器的中心。                                         |
| flex-start | 元素位于容器的开头。                                         |
| flex-end   | 元素位于容器的结尾。                                         |
| baseline   | 元素位于容器的基线上。                                       |
| initial    | 设置该属性为它的默认值                                       |
| inherit    | 从父元素继承该属性                                           |



## 4. CSS画三角形

首先了解一下盒模型：

先看一段代码：

```css
#div1{
            height: 100px;
            border-style: solid;
            border-width: 100px 100px 100px 100px;
            border-color: red forestgreen blue cyan;
            width: 100px;
        }
```

根据代码渲染，显示效果如下（边框颜色border-color四个值默认的加载方向，top right bottom left）：

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218150741552-768989036.png)

根据css代码，边框的宽度都是100px，div高度和宽度也是100px，但是这个和三角形有什么关联吗？

不急再看一个图，我们把div宽度和高度设置为0。

css代码：

```css
  #div1{
            border-style: solid;
            border-width: 100px 100px 100px 100px;
            border-color: red forestgreen blue cyan;
            width: 0px;
            height: 0px;
        }
```

浏览器就渲染出如下图片：

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218153011677-133635045.png)

咦，每个边都是三角形？ （可以试试只把div高宽其中一个设置为0，另一个100px）

既然有三角形了，下面就好办了。比如我要蓝色的三角形，把其它三个边颜色都去掉不就可以了嘛：

```
#div1{
            border-style: solid;
            border-width: 100px 100px 100px 100px;
            border-color: transparent transparent blue transparent;
            width: 0px;
            height: 0px;
        }
```

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218160013662-1855352489.png)蓝色三角形不就得到了。

审查元素一看，问题就出来了：

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218160206240-286447178.png)

虽然其它三个边都隐藏了，位置还在，怎么把多余的位置去掉呢？

试着修改下边框的宽度（宽度值对应：top right bottom left）：

先把border-width第一个值改为50px试试：

```css
#div1{
            border-style: solid;
            border-width: 50px 100px 100px 100px;
            border-color: transparent transparent blue transparent;
            width: 0px;
            height: 0px;
        }
```

修改前：![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218160206240-286447178.png)修改后：![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218161233771-81839886.png)

发现上面多余的地方少了一半，设置border-width第一个值为0px试试：

```css
        #div1{
            border-style: solid;
            border-width: 0px 100px 100px 100px;
            border-color: transparent transparent blue transparent;
            width: 0px;
            height: 0px;
        }
```

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218161630427-1580764592.png)查看元素已经完全是三角形的高度了

至此三角形就完成了。

那想其它三角形，应该怎么办？

再看下上面的图：

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218153011677-133635045.png)

就以蓝色的三角形为例，它的高度，就是css中设置的100px。那它的底边的长度和其它两个边的长度怎么来的呢？

哈哈，问的跟个小学生题一样。

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218164606052-386476893.jpg)

蓝色三角形（bottom）其实从它的顶点垂直下来一条线为准，将蓝色三角形分为左右两个小三角形，左边小三角形底边受left值影响，右边小三角形底边受right值影响。

其它一样：

top最长边=left值+right值=200px

left最长边=top值+bottom值=200px

明白以上关系，就能随便绘制什么三角形了，如将蓝色三角形渲染为直角三角形（还是以上面代码为例）：

```css
#div1{
            border-style: solid;
            border-width: 0px 0px 100px 100px;
            border-color: transparent transparent blue transparent;
            width: 0px;
            height: 0px;
}
```

![img](https://images2015.cnblogs.com/blog/802779/201512/802779-20151218165855990-704594034.png)

## 5. CSS画扇形

通过CSS画扇形：

```html
<html>
<head>
<style type="text/css">
div{
 border-radius:80px 0 0;
  width: 80px;
  height: 80px;
  background: #666;
}
</style>
</head>

<body>
<div></div>

</body>

</html>
```

效果图：

![1.jpg](https://img.php.cn/upload/image/481/399/579/1569043875455894.jpg)

**实现原理：左上角是圆角，其余三个角都是直角：左上角的值为宽和高一样的值，其他三个角的值不变（等于0）。**

border-radius 属性是一个最多可指定四个 border -*- radius 属性的复合属性

语法：

```css
border-radius: 1-4 length|% / 1-4 length|%;
```

每个半径的四个值的顺序是：左上角，右上角，右下角，左下角。如果省略左下角，右上角是相同的。如果省略右下角，左上角是相同的。如果省略右上角，左上角是相同的。

属性值：

- length 定义弯道的形状。
- % 使用%定义角落的形状。



## 6. 垂直居中的方法

### 6.1 margin:auto法

```
css:
div{
    width: 400px;
    height: 400px;
    position: relative;
    border: 1px solid #465468;
}
img{
    position: absolute;
    margin: auto;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

html:
<div>
<img src="mm.jpg">
</div>
```

定位为上下左右为0，margin：0可以实现脱离文档流的居中.

### 6.2 margin负值法

```css
.container{
    width: 500px;
    height: 400px;
    border: 2px solid #379;
    position: relative;
}
.inner{
    width: 480px;
    height: 380px;
    background-color: #746;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -190px; /*height的一半*/
	margin-left: -240px; /*width的一半*/
}
```

补充：其实这里也可以将marin-top和margin-left负值替换成，transform：translateX(-50%)和transform：translateY(-50%)

###6.3 table-cell（未脱离文档流的）

设置父元素的display:table-cell,并且vertical-align:middle，这样子元素可以实现垂直居中。

```css
div{
    width: 300px;
    height: 300px;
    border: 3px solid #555;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
img{
	vertical-align: middle;
}
```

###6.4 利用flex

将父元素设置为display:flex，并且设置align-items:center; justify-content:center;

```css
.container{
    width: 300px;
    height: 200px;
    border: 3px solid #546461;
    display: -webkit-flex;
    display: flex;
    -webkit-align-items: center;
    align-items: center;
    -webkit-justify-content: center;
    justify-content: center;
}
.inner{
    border: 3px solid #458761;
    padding: 20px;
}
```



## 7. 关于js动画和css3动画的差异性

渲染线程分为main thread和compositor thread

如果css动画只改变transform和opacity，这时整个CSS动画得以在compositor trhead完成

而js动画则会在main thread执行，然后出发compositor thread进行下一步操作

特别注意的是如果改变transform和opacity是不会重排或者重绘的。

**区别：**

1. 功能涵盖面，js比css大

2. 实现/重构难度不一，CSS3比js更加简单，性能跳优方向固定

4. 对帧速表现不好的低版本浏览器，css3可以做到自然降级

5. css动画有天然事件支持

6. css3有兼容性问题



## 8. 块元素和行内元素区别

**块元素**

1. 块元素在文档流中会独占一行，块元素会自上向下排列。
2. 可以设置margin和padding以及高度和宽度
3. 块元素在文档流中默认宽度是父元素的100%
4. 块元素在文档流中的高度默认被内容撑开

**内联元素**

1. 内联元素在文档流中只占自身的大小，会默认从左向右排列，如果一行中不足以容纳所有的内联元素，则换到下一行，继续自左向右。
2. 不会独占一行，width和height会失效，并且在垂直方向的padding和margin会失
   效。
3. 在文档流中，内联元素的宽度和高度默认都被内容撑开



## 9. 使元素消失的方法

1. opacity：0

   该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的

2. visibility：hidden

   该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件

3. display：none

   把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉。



## 10. CSS选择器优先级

1. 同一元素引用了多个样式时，排在后面的样式属性的优先级高

2. 样式选择器的类型不同时，优先级顺序为：**id 选择器 > class 选择器 = 伪类选择器 > 标签选择器 > 通配符**

3. 标签之间存在层级包含关系时，后代元素会继承祖先元素的样式。

   如果后代元素定义了与祖先元素相同的样式，则祖先元素的相同的样式属性会被覆盖。

   继承的样式的优先级比较低，至少比标签选择器的优先级低

4. 带有!important 标记的样式属性的优先级最高

5. 样式表的来源不同时，优先级顺序为：**内联样式> 内部样式 > 外部样式 > 浏览器用户自定义样式 > 浏览器默认样式**