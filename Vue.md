<head>
    <title>我的Vue</title>
</head>
<div class="xyc">
    <a href="https://xie-yingcheng.github.io/"><img src="./images/北极熊.png" height="35px" /> 主页</a>
    <a>返回</a>
</div>



# Vue核心

## 下载与安装

(1)Vue中文官网

```text
https://cn.vuejs.org/
```

(2)Vue.js的下载(Vue2.x版本)

- 开发版本：包含完整的警告和调试模式

```text
https://cn.vuejs.org/js/vue.js
```

- 生产版本：删除了警告信息

```text
https://cn.vuejs.org/js/vue.min.js
```

- Vue.js各个版本下载地址

```text
https://unpkg.com/browse/vue@3.2.26/dist/
https://cdn.jsdelivr.net/npm/vue@next/dist/
```

(3)引入Vue.js

```html
<script type="text/javascript" src="../js/vue.js"></script>
```

(4)安装浏览器插件Vue.js devtools，提供方是：

```text
https://vuejs.org
```

> (1)注意：安装后需要修改插件的**详情**，打开**允许访问文件网址选项**。
>
> (2)安装完成后在浏览器控制台可以看到Vue选项。

(5)关闭开发提示：Vue.js运行在浏览器上，使用开发版本会占用更多资源，因此引入的是**开发版本**控制台会有一个警告信息，在JavaScript中使用如下语句关闭该警告。

```javascript
Vue.config.productionTip = false; // 阻止Vue在启动时生成生产提示
```



## 入门案例

(1)引入Vue.js

```html
<script type="text/javascript" src="../js/vue.js"></script>
```

(2)准备一个供Vue使用的容器

```html
<div id="demo">
    Hello，{{name}}。
</div>
```

> (1)容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；
>
> (2)容器里的代码被称为**Vue模板**；
>
> (3)**{{xxx}}**中的xxx要写JavaScript**表达式**，且xxx可以自动读取到Vue实例data中的所有属性；
>
> (4)一旦data中的数据发生改变，那么页面中用到该数据的地方也会**自动更新**；

> JavaScript**表达式**和JavaScript**语句**
>
> (1)表达式：一个表达式会产生一个**值**，可以放在任何一个需要值的地方；
>
> - a
> - a + b
> - x === y ? 'a' : 'b'
>
> (2)语句：不一定会产生值；
>
> - if(){}
> - for(){}

(3)创建Vue实例，接管上面的容器

```html
<script type="text/javascript">
    // 创建Vue实例
    new Vue({
        el: '#demo', // el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。
        data: { // data中用于存储数据，数据供el所指定的容器去使用
            name: 'xyc'
        }
    });
</script>
```

> (1)想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；
>
> - el：指定当前Vue实例为哪个容器服务，值通常为**CSS选择器**字符串；
> - data：用于存储数据，数据供el所指定的容器去使用；
>
> (2)data可以使用json数据格式。
>
> (3)Vue实例和容器是**一一对应**的。

> 配置对象：
>
> (1)配置对象的内容使用**键值对**表示，如：el: '#demo'；
>
> - 配置对象中的键都可以直接写，也可以写为**字符串**的形式，如：'el': '#demo'；
>
> (2)不同的配置内容之间使用逗号(,)分隔，最后一个配置内容不写逗号(,)。



## Vue模板语法

(1)Vue模板语法有2大类：

- 插值语法
- 指令语法

(2)插值语法：

- 功能：用于解析标签体内容。

- 写法：{{xxx}}，xxx是**JavaScript表达式**，且可以直接读取到data中的所有属性。

(3)指令语法：

- 功能：用于解析标签，如：标签属性、标签体内容、绑定事件等；

- 举例：`v-bind:href="xxx"`或简写为`:href="xxx"`，xxx同样要写**JavaScript表达式**，且可以直接读取到data中的所有属性。

```html
<div id="demo">
    <div>插值语法：获取name的值，name={{name}}</div>
    <div>指令语法：点我去<a v-bind:href="url">{{name}}</a></div>
</div>
```

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            name: '百度',
            url: 'https://www.baidu.com/'
        }
    });
</script>
```



## 数据绑定

### 单向数据绑定：v-bind

(1)指令：指令用于解析html标签

- 完整写法：

```text
v-bind:属性 = "xxx"
```

- 简写：

```text
:属性 = "xxx"
```

> (1)属性：指的是html中的属性，但必须在Vue接管的容器中才能生效；
>
> (2)xxx表示的是属性的值，值可以使用**JavaScript表达式**引入。
>
> - 可以直接使用data中的数据；
> - 不需要使用插值语法{{}}。

(2)单向数据绑定的特点：数据只能从data流向页面(模板)。

### 双向数据绑定：v-model

(1)指令：双向绑定一般都应用在**表单类元素**上，如：input、select等。

- 完整写法：

```text
v-model:属性 = "xxx"
```

- 简写：`v-model:value`可以简写为`v-model`，因为v-model默认收集的就是**value**值。

```text
v-model = "xxx"
```

(2)双向数据绑定的特点：

- 数据不仅能从data流向页面，还可以从页面流向data，即：在页面上改变输入框中的值，data中对应的值也会改变。

- v-model默认收集的是**value**值。

- v-model应用在**表单类元素**上，如果应用在别的元素上，会报错。

```html
<div id="demo">
    单向数据绑定：<input type="text" :value="name"><br/>
    双向数据绑定：<input type="text" v-model="name"><br/>
</div>
```

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            name: '百度'
        }
    });
</script>
```



## data与el的2种写法

### el的2种写法

(1)创建Vue实例的时候配置el属性。

```html
<script type="text/javascript">
    new Vue({
        el: '#demo'
    });
</script>
```

> 此时Vue实例不需要变量来存放。

(2)先创建Vue实例，随后再通过`vm.$mount('#root')`指定el的值。

```html
<script type="text/javascript">
    const vm = new Vue({
        data: {
            name: "百度"
        }
    });
    vm.$mount('#demo');
</script>
```

> 此时Vue实例需要有一个变量来存放。

### data的2种写法

(1)对象式

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            name: '百度'
        }
    });
</script>
```

(2)函数式

```html
<script>
    new Vue({
        el: '#demo',
        data() {
            console.log(this); // 此处的this是Vue实例对象
            return {
                name: '百度'
            };
        }
    });
</script>
```

> 在使用组件时，data必须使用函数式，否则会报错。

> **一个重要的原则**：由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例，将是window实例。



## MVVM模型

(1)M：模型(Model) ：data中的数据

(2)V：视图(View) ：模板代码

(3)VM：视图模型(ViewModel)：Vue实例

> (1)data中**所有的属性**，最后都出现在vm实例上。
>
> (2)vm**实例所有的属性**及**Vue原型上所有属性**，在Vue模板中都可以直接使用。



## 回顾`Object.defineProperty`方法

(1)方法：

```javascript
Object.defineProperty(any, property, attributes);
```

(2)参数说明：

- any：需要添加/修改属性的对象；
- property：属性的名字，**string**类型；

- attributes：目标属性所拥有的特性，例如：修改、获取该属性的set()与get()方法等；
- 返回值：传入的对象。

```html
<script type="text/javascript">
    let number = 28;
    let person = {
        name: '张三',
        sex: '男'
    };
    Object.defineProperty(person, 'age', {
        // value: 18, // 默认值
        // enumerable: true, // 控制属性是否可以枚举，默认值是false
        // writable: true, // 控制属性是否可以被修改，默认值是false
        // configurable: true, // 控制属性是否可以被删除，默认值是false
        // 当读取person的age属性时，get函数就会被调用，返回值就是age的值
        get() {
            return number;
        },
        // 当修改person的age属性时，set函数就会被调用，且会收到修改的具体值
        set(value) {
            number = value;
        }
    });
    console.log(person);
</script>
```



## 数据代理：data

(1)**数据代理**：通过一个对象代理对另一个对象中属性的操作(读/写)。

(2)Vue中的数据代理：通过vm对象来代理data对象中属性的操作。

(3)Vue中数据代理的好处：更加方便的操作data中的数据。

(4)Vue数据代理的基本原理：

- 通过`Object.defineProperty()`把data对象中所有属性添加到vm上；

- 为每一个添加到vm上的属性，都指定一个getter/setter；

- 在getter/setter内部去操作data中对应的属性。



## 事件：methods与v-on

### 事件的基本使用

(1)事件的基本使用：

- 指令：使用`v-on:xxx`或`@xxx`绑定事件，其中xxx是事件名；
- 事件的回调需要配置Vue实例的methods中，最终会在vm上；
- methods中配置的函数，不要用箭头函数，否则this就不是vm了；

- methods中配置的函数，都是被Vue所管理的函数，this的指向是**vm**或**组件实例对象**；

- `@click="demo" `和 `@click="demo($event)"` 效果一致，但后者可以传参；

(2)案例：

```html
<div id="demo">
    <button @click="showInfo($event, 66)">按钮</button>
</div>
```

- 写法一：

```html
<script>
    new Vue({
        el: "#demo",
        data: {
            name: "百度"
        },
        methods: {
            showInfo: function (event, number) {
                console.log("hello," + this.name + "---" + number); // 可以获取data中的数据、传入的参数
                console.log(event); // 事件本身
            }
        }
    });
</script>
```

- 写法二：推荐

```html
<script>
    new Vue({
        el: "#demo",
        data: {
            name: "百度"
        },
        methods: {
            showInfo(event) {
                console.log("hello," + this.name); // this表示当前的Vue实例
            }
        }
    });
</script>
```

> 多个事件回调的方法之间使用逗号(,)分隔。

### 事件修饰符

(1)Vue中的事件修饰符：

- prevent：阻止默认事件(**常用**)；
- stop：阻止事件冒泡(**常用**)；
- once：事件只触发一次(**常用**)；
- capture：使用事件的捕获模式；
- self：只有event.target是当前操作的元素时才触发事件；
- passive：事件的默认行为立即执行，无需等待事件回调执行完毕。

(2)事件修饰符使用的位置：

- v-on:xxx**.**事件修饰符

- @xxx**.**事件修饰符

```html
<a href="http://www.baidu.com/" @click.prevent="showInfo">点我提示信息</a>
```

> 修饰符可以连续写，先写的先执行：@click**.**prevent**.**stop。

### 键盘事件

(1)Vue中常用的按键别名：

- 回车：enter

- 删除：delete，捕获**删除**和**退格**键

- 退出：esc

- 空格：space

- 换行：tab，特殊，必须配合keydown去使用

- 上：up

- 下：down

- 左：left

- 右： right

```html
<input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo">
```

(2)Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case(短横线命名)

(3)系统修饰键：ctrl、alt、shift、meta

- 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。

- 配合keydown使用：正常触发事件。

(4)也可以使用keyCode去指定具体的按键(不推荐)。

(5)`Vue.config.keyCodes.自定义键名 = 键码`，可以去定制按键别名。



## 计算属性：computed

(1)**计算属性**：要用的属性不存在，要通过已有属性计算得来。

(2)计算属性的原理：底层借助了`Objcet.defineProperty()`方法提供的getter和setter。

(3)get函数什么时候执行：

- 初次读取时会执行一次。
- 当**依赖的数据**发生改变时会被再次调用。

(4)优势：与methods实现相比，内部有缓存机制，效率更高，调试方便。

> (1)计算属性最终会出现在vm上，直接读取使用即可。
>
> (2)如果计算属性要被修改，那必须写set()函数去响应修改，且set()中要引起计算时依赖的数据发生改变。
>
> (3)setter和getter函数中的this都是Vue实例。

```html
<div id="demo">
    姓：<input type="text" v-model="firstName"> <br />
    名：<input type="text" v-model="lastName"> <br />
    全名：<span>{{fullName}}</span>
</div>
```

```html
<script type="text/javascript">
    const vm = new Vue({
        el: '#demo',
        data: {
            firstName: '张',
            lastName: '三',
        },
        computed: {
            fullName: {
                // 当读取fullName时，get()就会被调用，且返回值就作为fullName的值
                get() {
                    return this.firstName + '-' + this.lastName
                },
                // 当fullName被修改时调用set()
                set(value) {
                    const arr = value.split('-')
                    this.firstName = arr[0]
                    this.lastName = arr[1]
                }
            }
        }
    });
</script>
```

(5)当计算属性只有getter的时候，可以使用简写的形式：

```javascript
fullName() {
    return this.firstName + '-' + this.lastName
}
```



## 监视属性：watch

(1)监视属性：

- 当被监视的属性变化时，回调函数自动调用，进行相关操作；

- 监视的属性**必须存在**，才能进行监视；

(2)监视的两种写法：

- new Vue时传入watch配置

- 通过vm.$watch监视

### 监视属性：创建Vue实例时创建

```html
<div id="demo">
    <div>今天的天气是：{{info}}</div>
    <button @click="changeWeather">切换天气</button>
</div>
```

(1)完整写法：

```javascript
const vm = new Vue({
    'el': '#demo',
    'data': {
        isHot: true
    },
    computed: {
        info() {
            return this.isHot ? '晴' : '雨';
        }
    },
    methods: {
        changeWeather() {
            this.isHot = !this.isHot
        }
    },
    // 监视属性：当被监视的属性发生变化时，handler()自动执行
    watch: {
        isHot: {
            immediate: true, // 初始化时让handler调用一下
            // 当isHot发生改变时，handler()自动调用
            handler(newValue, oldValue) {
                console.log('isHot被修改了', newValue, oldValue);
            }
        }
    }
});
```

(2)简写形式：只有handler()方法

```javascript
const vm = new Vue({
    // 其他相同项省略
    // 监视属性：当被监视的属性发生变化时，handler()自动执行
    watch: {
        isHot(newValue, oldValue) {
            console.log('isHot被修改了', newValue, oldValue);
        }
    }
});
```

> newValue：监视属性变化后的值；
>
> oldValue：监视属性变化前的值。

### 使用vm.$watch创建监视属性

```html
<div id="demo">
    <div>今天的天气是：{{info}}</div>
    <button @click="changeWeather">切换天气</button>
</div>
```

(1)完整写法：

```html
<script type="text/javascript">
    const vm = new Vue({
        'el': '#demo',
        'data': {
            isHot: true
        },
        computed: {
            info() {
                return this.isHot ? '晴' : '雨'
            }
        },
        methods: {
            changeWeather() {
                this.isHot = !this.isHot
            }
        }
    });
    //  使用vm.$watch创建监视属性
    vm.$watch("isHot", {
        immediate: true,
        handler(newValue, oldValue) {
            console.log('isHot被修改了', newValue, oldValue)
        }
    });
</script>
```

(2)简写形式：只有handler()方法

```javascript
vm.$watch("isHot", (newValue, oldValue) => {
    console.log('isHot被修改了', newValue, oldValue)
});
```

### 深度监视

(1)深度监视：

- Vue中的watch默认不监测对象内部值的改变：只监视一层。

- 配置deep: true可以监测对象内部值改变：监视多层。

> (1)Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以。
>
> (2)使用watch时根据数据的具体结构，决定是否采用深度监视。

(2)案例：

```html
<div id="demo">
    <div>number中的a是：{{number.a}}</div>
    <div>number中的b是：{{number.b}}</div>
    <button @click="changeNumber">改变number</button>
</div>
```

```html
<script type="text/javascript">
    const vm = new Vue({
        'el': '#demo',
        'data': {
            number: {
                a: 1,
                b: 200
            }
        },
        methods: {
            changeNumber() {
                this.number.a++;
                this.number.b--;
            }
        },
        watch: {
            number: {
                deep: true, // 开启深度监视
                handler(newValue, oldValue) {
                    console.log(newValue.a);
                    console.log(newValue.b);
                }
            }
        }
    });
</script>
```

> (1)如果不开启深度监视，上述示例中改变a或者b的时候，监视属性不会被执行，因为监视的number，而number没有改变。
>
> (2)原因：number是对象，是引用地址，地址没有改变，那么number就没有改变。



## 计算属性与监视属性的比较

(1)computed和watch之间的区别：

- computed能完成的功能，watch都可以完成。

- watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。

(2)两个重要的小原则：

- 所有被Vue管理的函数，最好写成普通函数，这样this的指向才是**vm**或**组件实例对象**。
- 所有不被Vue所管理的函数(**定时器的回调函数**、**ajax的回调函数**等、**Promise的回调函数**)，最好写成**箭头函数**，这样this的指向才是**vm**或**组件实例对象**。



## 绑定样式

- 所需要的测试样式

```html
<style>
    .basic{
        width: 400px;
        height: 100px;
        border: 1px solid black;
    }
    .happy{
        border: 4px solid red;;
        background-color: rgba(255, 255, 0, 0.644);
        background: linear-gradient(30deg, yellow, pink, orange, yellow);
    }
    .sad{
        border: 4px dashed rgb(2, 197, 2);
        background-color: gray;
    }
    .normal{
        background-color: skyblue;
    }
</style>
```

### 绑定class样式

(1)使用固定的class值

```html
<div class="basic normal" >test</div>
```

(2)绑定class样式：字符串写法


```html
<div class="basic" :class="mood" @click="changeMood">test</div>
```

> (1)**:class**的值来源于data中的数据；
>
> (2)字符串写法适用于：样式的class值不确定，需要动态指定；
>
> (3)该div元素会被浏览器解析为下列代码：假设mood的值是happy。

```html
<div class="basic happy">test</div>
```

(3)绑定class样式：数组写法

```html
<div class="basic" :class="classArr">test</div>
```

>(1)**:class**的值(classArr)来源于data中的数据，是一个字符串数组，值来源于测试样式中的class值；
>
>(2)数组写法适用于：要绑定的样式个数不确定、名字也不确定。

(4)绑定class样式：对象写法

```html
<div class="basic" :class="classObj">test</div>
```

> (1)对象写法适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用；
>
> (2)**:class**的值(classObj)来源于data中的数据，是一个对象；
>
> (3)对象中的键是样式的class值；
>
> (4)对象中的值是true或者false：
>
> - true：该class样式被应用；
> - false：该class样式不应用。

```javascript
classObj: {
    happy: false, // 表示class值为happy对应的样式不应用
    sad: true // 表示class值为sad对应的样式需要应用
}
```

### 绑定style样式

(1)绑定style样式：对象写法

```html
<div class="basic" :style="styleObj">test</div>
```

```javascript
styleObj: {
    fontSize: '40px',
    color: 'red'
}
```

>(1)将短线写法的css样式写法驼峰写法：
>
>- font-size: 40px
>- fontSize: '40px'
>
>(2)对象中的键必须是css样式，否则会报错。

(2)绑定style样式：数组写法(**对象数组**)

```html
<div class="basic" :style="styleArr">test</div>
```

```javascript
styleArr: [styleObj1, styleObj2]  // 同时应用多个对象中的样式
```



## 条件渲染

### v-show

(1)写法：v-show="表达式"。

(2)适用场景：切换频率较高的场景。

(3)特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉。

```html
<div v-show="a === 1">test</div>
```

- 若a != 1，则该元素会被渲染为：

```html
<div style="display: none;">test</div>
```

- 若a = 1，则该元素会被渲染为：

```html
<div style="">test</div>
```

> (1)v-show="表达式"：
>
> - 表达式结果为true：展示该元素；
> - 表达式结果为false：**隐藏**该元素；
> - 表达式中的变量值来源于Vue实例中的data。
>
> (2)v-show 不支持`<template>`元素，也不支持v-else。

### v-if

(1)写法：

```text
v-if="表达式" 
v-else-if="表达式"
v-else="表达式"
```

> (1)表达式结果：
>
> - 表达式结果为true：展示该元素；
> - 表达式结果为false：**移除**该元素；
> - 表达式中的变量值来源于Vue实例中的data。
>
> (2)注意：v-if可以和v-else-if、v-else一起使用，但要求结构**不能被打断**。
>
> (3)用法与Java的if-else一样的执行逻辑。

(2)适用场景：切换频率较低的场景。

(3)特点：不展示的DOM元素直接被**移除**，条件不成立时，v-if的所有子节点不会解析。

### `<template>`

(1)因为v-if是一个指令，所以必须将它添加到一个元素上。

(2)如果想切换多个元素，此时使用`<template>`元素当做不可见的包裹元素，并在上面使用v-if。

(3)最终的渲染结果将不包含`<template>`元素。

(4)做法1：使用`<div>`元素

```html
<div v-if="n === 1">
    <p>段落1</p>
    <p>段落2</p>
</div>
```

- 当`n = 1`时，渲染结果：会多一个`<div>`标签，有时候会破坏DOM结构

```html
<div>
    <p>段落1</p>
    <p>段落2</p>
</div>
```

(5)做法2：使用`<template>`元素

```html
<template v-if="n === 1">
    <p>段落1</p>
    <p>段落2</p>
</template>
```

- 当`n = 1`时，渲染结果：不会破坏DOM结构

```html
<p>段落1</p>
<p>段落2</p>
```

> `<template>`元素只能配合v-if使用。

## 列表渲染

### v-for：遍历数组

(1)基本的数据：数组形式

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            persons: [
                { id: '001', name: '张三', age: 18 },
                { id: '002', name: '李四', age: 19 },
                { id: '003', name: '王五', age: 20 }
            ]
        }
    });
</script>
```

(2)单个参数：

```html
<div id="demo">
    <ul>
        <li v-for="p in persons" :key="p.id">
            {{p.name}}-{{p.age}}
        </li>
    </ul>
</div>
```

> (1)**:key**：指定一个唯一的标识，类似于数据库的主键，也可以使用数组的索引。
>
> (2)也可以用**of**替代**in**作为分隔符，因为它更接近JavaScript迭代器的语法。

```html
<div v-for="item of items"></div>
```

(3)两个参数：

```html
<div id="demo">
    <ul>
        <li v-for="(p, index) in persons" :key="index">
            {{index}}-{{p.name}}-{{p.age}}
        </li>
    </ul>
</div>
```

> 参数说明：
>
> - p：persons数组的某个元素；
> - index：persons数组的索引值。

### v-for：遍历对象

(1)基本的数据：对象形式

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            car: {
                name: '奥迪A8',
                price: '70万',
                color: '黑色'
            }
        }
    });
</script>
```

(2)单个参数：

```html
<div id="demo">
    <ul>
        <li v-for="value in car">
            {{value}}
        </li>
    </ul>
</div>
```

> (1)参数说明：
>
> - value：对象中每一项的value值。
>
> (2)因为value值不一定唯一，所以**:key**没有意义。

(3)两个参数：

```html
<div id="demo">
    <ul>
        <li v-for="(value, k) in car" :key="k">
            {{k}}：{{value}}
        </li>
    </ul>
</div>
```

> (1)参数说明：
>
> - value：对象中每一项的value值；
> - k：对象中每一项的key值。
>
> (2)因为对象的key值唯一，所以可以作为**:key**的值。

(4)三个参数

```html
<div id="demo">
    <ul>
        <li v-for="(value, k, index) in car" :key="index">
            {{index}}--{{k}}：{{value}}
        </li>
    </ul>
</div>
```

> (1)参数说明：
>
> - value：对象中每一项的value值；
> - k：对象中每一项的key值;
> - index：key值的索引。
>
> (2)在遍历对象时，会按`Object.keys()`的结果遍历，但是**不能**保证它的结果在不同的JavaScript引擎下都一致。

### v-for：遍历字符串

(1)基本的数据：字符串形式

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            str: "hello"
        }
    });
</script>
```

(2)遍历字符串：

```html
<div id="demo">
    <ul>
        <li v-for="(char, index) in str" :key="index">
            {{index}}--{{char}}
        </li>
    </ul>
</div>
```

> 参数说明：
>
> - char：字符串中的每个字符；
> - index：每个字符的索引位置。

### v-for：遍历数字

```html
<div id="demo">
    <ul>
        <li v-for="(number, index) in 5" :key="index">
            {{index}}-{{number}}
        </li>
    </ul>
</div>
```

### 列表过滤

```html
<div id="demo">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="keyWord">
    <ul>
        <li v-for="(p,index) of filPerons" :key="index">
            {{p.name}}-{{p.age}}-{{p.sex}}
        </li>
    </ul>
</div>
```

```html
<script type="text/javascript">
    new Vue({
        el: '#demo',
        data: {
            keyWord: '',
            persons: [
                { id: '001', name: '马冬梅', age: 19, sex: '女' },
                { id: '002', name: '周冬雨', age: 20, sex: '女' },
                { id: '003', name: '周杰伦', age: 21, sex: '男' },
                { id: '004', name: '温兆伦', age: 22, sex: '男' }
            ]
        },
        computed: {
            filPerons() {
                return this.persons.filter((p) => {
                    return p.name.indexOf(this.keyWord) !== -1;
                });
            }
        }
    });
</script>
```

### 列表排序

```html
<div id="root">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="keyWord">
    <button @click="sortType=2">年龄升序</button>
    <button @click="sortType=1">年龄降序</button>
    <button @click="sortType=0">原顺序</button>
    <ul>
        <li v-for="(p, index) of filPerons" :key="p.id">
            {{p.name}}-{{p.age}}-{{p.sex}}
        </li>
    </ul>
</div>
```

```html
<script type="text/javascript">
    Vue.config.productionTip = false

    new Vue({
        el: '#root',
        data: {
            keyWord: '',
            sortType: 0, //0原顺序 1降序 2升序
            persons: [
                { id: '001', name: '马冬梅', age: 19, sex: '女' },
                { id: '002', name: '周冬雨', age: 20, sex: '女' },
                { id: '003', name: '周杰伦', age: 21, sex: '男' },
                { id: '004', name: '温兆伦', age: 22, sex: '男' }
            ]
        },
        computed: {
            filPerons() {
                const arr = this.persons.filter((p) => {
                    return p.name.indexOf(this.keyWord) !== -1;
                });
                // 判断是否需要排序
                if (this.sortType) {
                    arr.sort((p1, p2) => {
                        return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age;
                    });
                }
                return arr; // 注意需要返回
            }
        }
    });
</script>
```





## key的作用与原理

(1)虚拟DOM中key的作用：
- key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据**新数据**生成**新的虚拟DOM**；
- 随后Vue进行**新虚拟DOM**与**旧虚拟DOM**的差异比较。

(2)比较规则：

- 旧虚拟DOM中找到了与新虚拟DOM相同的key：
    - 若虚拟DOM中内容没变，直接使用之前的真实DOM；
    - 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
- 旧虚拟DOM中未找到与新虚拟DOM相同的key：
    - 创建新的真实DOM，随后渲染到到页面。

(3)用index作为key可能会引发的问题：
- 若对数据进行：逆序添加、逆序删除等**破坏顺序**操作：
    - 会产生没有必要的真实DOM更新，此时界面效果没问题，但效率低。
- 如果结构中还包含**输入类的DOM**：
    - 会产生错误DOM更新，界面有问题。

(4)开发中如何选择key：
- 最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。
- 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。

> (1)**:key**是给Vue内部对比算法中使用。



