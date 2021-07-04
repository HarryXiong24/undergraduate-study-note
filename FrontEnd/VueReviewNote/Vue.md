# Vue 回顾笔记



## 模板语法中的动态参数

### 作用

可以动态修改标签中需要绑定的属性：

```vue
<template>
  <div class="home">
    <div>
      <button @[eventName]="clickMe">点击我</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      eventName: "click", // 此时就可以动态替换click，blur
    };
  },
  methods: {
    clickMe() {
      alert("你点击了我!");
    },
  }
};
</script>
```

### 注意点

#### 对动态参数的值的约束

动态参数预期会求出一个字符串，异常情况下值为 `null`。这个特殊的 `null` 值可以被显性地用于移除绑定。任何其它非字符串类型的值都将会触发一个警告。

#### 对动态参数表达式的约束

动态参数表达式有一些语法约束，因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的。例如：

```vue
<!-- 这会触发一个编译警告 -->
<a v-bind:['foo' + bar]="value"> ... </a>
```

变通的办法是使用没有空格或引号的表达式，或用计算属性替代这种复杂表达式。

在 DOM 中使用模板时 (直接在一个 HTML 文件里撰写模板)，还需要避免使用大写字符来命名键名，因为浏览器会把 attribute 名全部强制转为小写：

```vue
<!--
在 DOM 中使用模板时这段代码会被转换为 `v-bind:[someattr]`。
除非在实例中有一个名为“someattr”的 property，否则代码不会工作。
-->
<a v-bind:[someAttr]="value"> ... </a>
```



## 计算属性

### 计算属性的书写方式

只有getter时的简写：

```js
computed: {
  // 计算属性的 getter
  reversedMessage: function () {
    // `this` 指向 vm 实例
    return this.message.split('').reverse().join('')
  }
}
```

同时有getter和setter时的写法：

```js
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```

**注意：setter作用于属性本身改变值的时候，而不是作用于别的变量修改值的时候。**



### 计算属性缓存 vs 方法

你可能已经注意到我们可以通过在表达式中调用方法来达到同样的效果：

```vue
<p>Reversed message: "{{ reversedMessage() }}"</p>
// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 `Date.now()` 不是响应式依赖：

```vue
computed: {
  now: function () {
    return Date.now()
  }
}
```

相比之下，每当触发重新渲染时，调用方法将**总会**再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 **A**，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 **A**。如果没有缓存，我们将不可避免的多次执行 **A** 的 getter！如果你不希望有缓存，请用方法来替代。

用例展示：

```vue
<template>
  <div class="home">

    <div>
      {{ date }}
      {{ showDate() }}
    </div>

    <input v-model="newName" />
    <button @click="submit">submit</button>
    <div>
      {{ fullName }}
    </div>
      
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      firstName: "harry",
      lastName: "xiong",
      newName: "",
    };
  },
  methods: {
    clickMe() {
      alert("你点击了我!");
    },
    showDate() {
      return Date.now();
    },
    submit() {
      this.fullName = this.newName;
    }
  },
  computed: {
    date: {
      get: function () {
        return Date.now();
      },
    },
    fullName: {
      get: function () {
        return this.firstName + " " + this.lastName;
      },
      set: function (newName) {
        let names = newName.split(" ");
        this.firstName = names[0];
        this.lastName = names[names.length - 1];
      },
    },
  },
};
</script>
```

此时，在输入框里输入数据，就会触发DOM更新，而此时 date 没有监测到数据响应式变化，所以不会发生更新。但此时 showDate() 方法相当于重新触发了，因此就会不断调用。



## `v-for` 与 `v-if` 一同使用

注意我们**不**推荐在同一元素上使用 `v-if` 和 `v-for`。更多细节可查阅[风格指南](https://cn.vuejs.org/v2/style-guide/#避免-v-if-和-v-for-用在一起-必要)。

当它们处于同一节点，`v-for` 的优先级比 `v-if` 更高，这意味着 `v-if` 将分别重复运行于每个 `v-for` 循环中。当你只想为*部分*项渲染节点时，这种优先级的机制会十分有用，如下：

```vue
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```

上面的代码将只渲染未完成的 todo。

而如果你的目的是有条件地跳过循环的执行，那么可以将 `v-if` 置于外层元素 (或 [`) 上。如：

```vue
<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>
```



## 表单修饰符

### .lazy

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了[上述](https://cn.vuejs.org/v2/guide/forms.html#vmodel-ime-tip)输入法组合文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件_之后_进行同步：

```
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">
```

### .number

如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```
<input v-model.number="age" type="number">
```

这通常很有用，因为即使在 `type="number"` 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 `parseFloat()` 解析，则会返回原始的值。

### `.trim`

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：

```
<input v-model.trim="msg">
```

