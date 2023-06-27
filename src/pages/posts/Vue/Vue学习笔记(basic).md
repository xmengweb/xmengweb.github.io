---
layout: "@layouts/MarkdownPost.astro"
title: "Vue学习笔记"
pubDate: 2022-10-01
description: "笔记总结"
author: "XMeng"
cover:
  url: "https://positivethinking.tech/wp-content/uploads/2021/01/Logo-Vuejs.png"
  alt: "cover"
tags: ["Vue"]
theme: "light"
featured: true
---

# Vue 学习笔记(basic)

## 模板语法

Vue 模板语法有 2 大类：

​ 1.插值语法：

​ 功能：用于解析标签体内容。

​ 写法：{{xxx}}，xxx 是 js 表达式，且可以直接读取到 data 中的所有属性。

​ 2.指令语法：

​ 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）。

​ 举例：v-bind:href="xxx" 或 简写为 :href="xxx"，xxx 同样要写 js 表达式，

​ 且可以直接读取到 data 中的所有属性。

​ 备注：Vue 中有很多的指令，且形式都是：v-????，此处是拿 v-bind 举 de 例子。

```vue
<!-- 准备好一个容器-->
<div id="root">
			<h1>插值语法</h1>
			<h3>你好，{{name}}</h3>
			<hr/>
			<h1>指令语法</h1>
			<a v-bind:href="study.url.toUpperCase()" x="hello">点我去{{study.name}}学习1</a>
			<a :href="study.url" x="hello">点我去{{study.name}}学习2</a>
		</div>

<script type="text/javascript">
Vue.config.productionTip = false; //阻止 vue 在启动时生成生产提示。
new Vue({
  el: "#root",
  data: {
    name: "jack",
    study: {
      name: "world",
      url: "http://www.xmcug.top",
    },
  },
});
</script>
```

root 容器里的代码被称为【Vue 模板】

> 学习思考:
>
> ​ 我认为插值语法`{{ }}`,或者是指令语法`v-bind:`本质上都是用于解析表达式的,都可直接读取到 data 中的所有内容.
>
> ​ 不过插值语法用于解析标签体的内容,指令语法可以简写为`:`,用于解析解析标签（包括：标签属性、标签体内容、绑定事件.....）.

## 数据绑定

1.单向绑定(v-bind)：数据只能从 data 流向页面。

2.双向绑定(v-model)：数据不仅能从 data 流向页面，还可以从页面流向 data。

​ 备注：

​ 1.双向绑定一般都应用在表单类元素上（如：input、select 等）

​ 2.v-model:value 可以简写为 v-model，因为 v-model 默认收集的就是 value 值。

```html
<!-- 普通写法 -->
单向数据绑定：<input type="text" v-bind:value="name" /><br />
双向数据绑定：<input type="text" v-model:value="name" /><br />

<!-- 简写 -->
单向数据绑定：<input type="text" :value="name" /><br />
双向数据绑定：<input type="text" v-model="name" /><br />

注意!!
<!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上 -->
<!-- <h2 v-model:x="name">你好啊</h2> -->
```

## el 和 data 的两种写法

data 与 el 的 2 种写法

​ 1.el 有 2 种写法

​ (1).new Vue 时候配置 el 属性。

​ (2).**先创建 Vue 实例，随后再通过 vm.$mount('#root')指定 el 的值**。

```js
//el的两种写法
const v = new Vue({
  //el:'#root', //第一种写法
  data: {
    name: "尚硅谷",
  },
});
console.log(v);
v.$mount("#root"); //第二种写法
```

​ 2.data 有 2 种写法

​ (1).对象式

​ (2).函数式

​ 如何选择：目前哪种写法都可以，以后学习到组件时，data 必须使用函数式，否则会报错。

```js
new Vue({
  el: "#root",
  //data的第一种写法：对象式
  /* data:{
				name:'尚硅谷'
			} */

  //data的第二种写法：函数式
  data() {
    console.log("@@@", this); //此处的this是Vue实例对象
    return {
      name: "尚硅谷",
    };
  },
});
```

​ 3.一个重要的原则：

​ **由 Vue 管理的函数，一定不要写箭头函数**，一旦写了箭头函数，this 就不再是 Vue 实例了。

## 数据代理

- **_引入:_** `Object.defineProperty()` 方法会直接在一个对象上**定义一个新属性**，或者**修改一个对象的现有属性，并返回此对象**。注意 : 应当
  直接在 [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object) 构造器对象上调用此方法，而不是
  在任意一个 `Object` 类型的实例上调用。

```js
//Object.defineProperty(obj, prop, descriptor)
//obj：必需。目标对象
//prop：必需。需定义或修改的属性的名字
//descriptor：必需。目标属性所拥有的特性,descriptor是以对象的类型传入.

let user = {};

// 使用`Object.defineProperty()`给user添加name属性：
Object.defineProperty(user, "name", {
  value: "妙公子",
});
console.log(user);
// {name: "妙公子"}

// 使用`Object.defineProperty()`给user添加sayHi方法：
Object.defineProperty(user, "sayHi", {
  value: function () {
    console.log("Hi !");
  },
});
console.log(user);
// {name: "妙公子", sayHi: ƒn}
```

​ _descriptor_

```js
descriptor: {
  value: 默认为 undefined,
  // 该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）

  writable: 默认为 false,
  // 当且仅当该属性的 writable 键值为 true 时，属性的值，也就是上面的 value，才能被赋值运算符改变

  enumerable: 默认为 false,
  // 当且仅当该属性的 enumerable 键值为 true 时，该属性才会出现在对象的枚举属性中

  configurable: 默认为 false,
  // 当且仅当该属性的 configurable 键值为 true 时，该属性才可以被删除，以及除 value 和 writable 特性外的其他特性才能可以被修改

  get: 默认为undefined,
  // 属性的 getter 函数，如果没有 getter，则为 undefined。当访问该属性时，会调用此函数。该函数的返回值就是属性的值。

  set: 默认为undefined,
  // 属性的 setter 函数，如果没有 setter，则为 undefined。当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值）。
}
```

- **_数据代理_**

```js
<!-- 数据代理：通过一个对象代理对另一个对象中属性的操作（读/写）-->
<script>
    let obj = {x:100}
	let obj2 = {y:200}
	Object.defineProperty(obj2,'x',{
        get(){
            return obj.x
        },
        set(value){
            obj.x = value
        }
    })
</script>

```

​ 我认为就是为对象 2 添加一个属性,而这个属性每当被访问是,就是去访问对象 1 的属性值,仿佛是将对象 1 的值共享给了另一个对象,每当去修改时,就是去
修改对象 1 的值.

1.Vue 中的数据代理：

​ 通过 vm 对象来代理 data 对象中属性的操作（读/写）

2.Vue 中数据代理的好处：

​ 更加方便的操作 data 中的数据

3.基本原理：

​ 通过 Object.defineProperty()把 data 对象中所有属性添加到 vm 上。

​ 为每一个添加到 vm 上的属性，都指定一个 getter/setter。

​ 在 getter/setter 内部去操作（读/写）data 中对应的属性。

![image-20220724142036908](https://cugdemo.oss-cn-hangzhou.aliyuncs.com/image-20220724142036908.png)

## 事件处理

- 事件的基本使用：

​ 1.使用 v-on:xxx 或 @xxx 绑定事件，其中 xxx 是事件名；

​ 2.事件的回调需要配置在 methods 对象中，最终会在 vm 上；

​ 3.methods 中配置的函数，不要用箭头函数！否则 this 就不是 vm 了；

​ 4.methods 中配置的函数，都是被 Vue 所管理的函数，this 的指向是 vm 或 组件实例对象；

​ 5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；

```html
<button @click="showInfo1">点我提示信息1（不传参）</button> <button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
```

```js
methods:{
    showInfo1(event){
        // console.log(event.target.innerText)
        // console.log(this) //此处的this是vm
        alert('同学你好！')
    },
    showInfo2(event,number){
        console.log(event,number)
        // console.log(event.target.innerText)
        // console.log(this) //此处的this是vm
        alert('同学你好！！')
    }
}
```

- Vue 中的事件修饰符：

​ 1.prevent：阻止默认事件（常用）；

​ 2.stop：阻止事件冒泡（常用）；

​ 3.once：事件只触发一次（常用）；

​ 4.capture：使用事件的捕获模式；

​ 5.self：只有 event.target 是当前操作的元素时才触发事件；

​ 6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；

```html
<h2>欢迎来到{{name}}学习</h2>
<!-- 阻止默认事件（常用） -->
<a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>

<!-- 阻止事件冒泡（常用） -->
<div class="demo1" @click="showInfo">
  <button @click.stop="showInfo">点我提示信息</button>
  <!-- 修饰符可以连续写 -->
  <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a>
</div>

<!-- 事件只触发一次（常用） -->
<button @click.once="showInfo">点我提示信息</button>

<!-- 使用事件的捕获模式 -->
<div class="box1" @click.capture="showMsg(1)">
  div1
  <div class="box2" @click="showMsg(2)">div2</div>
</div>
```

1.Vue 中常用的按键别名：

​ 回车 => enter

​ 删除 => delete (捕获“删除”和“退格”键)

​ 退出 => esc

​ 空格 => space

​ 换行 => tab (特殊，必须配合 keydown 去使用)

​ 上 => up

​ 下 => down

​ 左 => left

​ 右 => right

2.Vue 未提供别名的按键，可以使用按键原始的 key 值去绑定，但注意要转为 kebab-case（短横线命名）

3.系统修饰键（用法特殊）：ctrl、alt、shift、meta

​ (1).配合 keyup 使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。

​ (2).配合 keydown 使用：正常触发事件。

4.也可以使用 keyCode 去指定具体的按键（不推荐）

5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名

```html
<input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo" />
```

## 计算属性

计算属性：

​ 1.定义：要用的属性不存在，要通过已有属性计算得来。

​ 2.原理：底层借助了 Objcet.defineproperty 方法提供的 getter 和 setter。

​ 3.get 函数什么时候执行？

​ (1).初次读取时会执行一次。

​ (2).当依赖的数据发生改变时会被再次调用。

​ 4.优势：与 methods 实现相比，内部有缓存机制（复用），效率更高，调试方便。

​ 5.备注：

​ 1.计算属性最终会出现在 vm 上，直接读取使用即可。

​ 2.如果计算属性要被修改，那必须写 set 函数去响应修改，且 set 中要引起计算时依赖的数据发生改变。

```js
computed:{
    fullName:{
        //get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
        //get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
        get(){
            console.log('get被调用了')
            // console.log(this) //此处的this是vm
            return this.firstName + '-' + this.lastName
        },
            //set什么时候调用? 当fullName被修改时。
        set(value){
            console.log('set',value)
            const arr = value.split('-')
            this.firstName = arr[0]
            this.lastName = arr[1]
        }
    }
}

//简写(只用get的话就简写)
fullName(){
    console.log('get被调用了')
    return this.firstName + '-' + this.lastName
}

//这里需要注意的是返回值就可以理解为是fullname的值
```

## 监视属性

- 监视属性 watch：

​ 1.当被监视的属性变化时, 回调函数自动调用, 进行相关操作

​ 2.监视的属性必须存在，才能进行监视！！

​ 3.监视的两种写法：

​ (1).new Vue 时传入 watch 配置

​ (2).通过 vm.$watch 监视

```js
data:{
	isHot:true,
}

watch:{
     isHot:{
         immediate:true, //初始化时让handler调用一下
         //handler什么时候调用？当isHot发生改变时。
         handler(newValue,oldValue){
         console.log('isHot被修改了',newValue,oldValue)
    }
}

//或者是
vm.$watch('isHot',{
    immediate:true, //初始化时让handler调用一下
    //handler什么时候调用？当isHot发生改变时。
    handler(newValue,oldValue){
        console.log('isHot被修改了',newValue,oldValue)
    }
})

//只用handler的话可以简写
    isHot(newValue,oldValue){
        console.log('isHot被修改了',newValue,oldValue,this)
    }
    vm.$watch('isHot',(newValue,oldValue)=>{
        console.log('isHot被修改了',newValue,oldValue,this)
    })
```

- 注意:

  深度监视：

  ​ (1).Vue 中的 watch 默认不监测对象内部值的改变（一层）。

  ​ (2).配置 deep:true 可以监测对象内部值改变（多层）。

  ​ 备注：

  ​ (1).Vue 自身可以监测对象内部值的改变，但 Vue 提供的 watch 默认不可以！

  ​ (2).使用 watch 时根据数据的具体结构，决定是否采用深度监视。

  ```js
  data:{
      isHot:true,
      numbers:{
          a:1,
          b:1,
          c:{
              d:{
                  e:100
              }
          }
      }
  }

  watch:{
      //监视多级结构中某个属性的变化
      'numbers.a':{
          handler(){
              console.log('a被改变了')
          }
      }
  	//监视多级结构中所有属性的变化
      numbers:{
          deep:true,
              handler(){
              console.log('numbers改变了')
          }
      }
  }
  ```

## 绑定样式

## 条件渲染

## 列表渲染

### 显示列表

- 遍历数组: v-for / index 保存的是内容和索引
- 遍历对象: v-for / key 保存的是 value 和 key

v-for 指令:

​ 1.用于展示列表数据

​ 2.语法：v-for="(item, index) in xxx" :key="yyy"

​ 3.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

> 一个标签里面写了一个插值语法`{{p}}`代表这个 p 来自于
>
> 1. data 里放的正常的属性
> 2. 计算属性
> 3. 形参

```html
<!-- 遍历存储对象的数组person -->
<ul>
  <li v-for="(p,index) of persons" :key="index">{{p.name}}-{{p.age}}</li>
</ul>

<!-- 遍历对象 -->
<ul>
  <li v-for="(value,k) of car" :key="k">{{k}}-{{value}}</li>
</ul>
```

让每一个`li`都有了一个唯一的标识,只要有 v-for 就得有`:key`进行标识`(ul里面的每个li不能一样)`.

### key 的作用原理

​ 当初始给定了一串的列表代码后，vue 首先会根据代码数据生成虚拟 DOM，再将虚拟 DOM 转化为真实 DOM 呈现给用户，当数据发生更改后，vue 会在根据新
生成的数据生成虚拟 DOM，接着会使用虚拟 DOM 对比算法和初始的 DOM 进行对比，对比方式就是根据 key，查看和这个 key 相同的旧的 DOM 里的`li`里面的
一不一样，发现不一样的会重新生成，一样的会直接使用原来的。

​ 所以如果将 index 作为 key 时，**如果数组里的元素顺序发生变化时**，大部分 key 与之对应的数据都会错乱，导致效率低并且一些问题。

​ 实际上所以为了防止这个问题，**可以将 key 设为和数组里每个元素一样的 id 值**，就是说将 key 和每个元素捆绑起来，显然 key 捆绑元素更好，而不
是捆绑数组的下标。

### 列表过滤

例如：模糊搜索，输入一个字，显示有这个字的列表

使用**监视属性-watch**

使用**计算属性-computed**

### 列表排序

**计算属性**

### Vue 监视数据的原理

- 想法:

> Vm 把 data 存到了自身的\_data 里边, ` data===Vm._data`, 放的过程中进行了数据劫持(监视数据以便改变时更新解析),通过数据代理将属性也存在了 Vm
> 里边,所以可以直接通过 Vm 来访问(编码更加方便).
>
> Vm 所以使用 getter setter 可以让 Vm 直接读取修改到\_data 的数据,使得操作更加方便.
>
> \_data 也使用 getter setter 可以让 Vue 实现监视数据,当修改数据会调用 set,调用了 set 代表知道了数据发生了变化,Vue 自然也就做到了监视了数据.

- 引入: Vue 必须在知道数据发生了变化之后才会去解析显示,所以为了保证每次数据更新都能被解析所有有必要去了解 Vue 是怎么知道数据发生了变化即如何
  监视数据.

Vue 监视数据的原理：

​ 1. vue 会监视 data 中所有层次的数据。

​ 2. 如何监测对象中的数据？

​ 通过 setter 实现监视，且要在 new Vue 时就传入要监测的数据。

​ (1).对象中后追加的属性，Vue 默认不做响应式处理

​ (2).如需给后添加的属性做响应式，请使用如下 API：

​ Vue.set(target，propertyName/index，value) 或

​ vm.$set(target，propertyName/index，value)

​ 3. 如何监测数组中的数据？

​ 通过包裹数组更新元素的方法实现，本质就是做了两件事：

​ (1).调用原生对应的方法对数组进行更新。

​ (2).重新解析模板，进而更新页面。

​ 4.在 Vue 修改数组中的某个元素一定要用如下方法：

​ 1.使用这些 API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()

​ 2.Vue.set() 或 vm.$set()

​ 特别注意：Vue.set() 和 vm.$set() 不能给 vm 或 vm 的根数据对象 添加属性！！！

> 所以在写代码时,如果遇到了**给某个对象追加一个属性**时,一定要注意追加进行响应式处理.
>
> 还要注意**修改数组时不要直接通过索引下标然后去修改**
>
> 要思考 Vue 能否监视到数据的变化

```js
//创建一个监视的实例对象，用于监视data中属性的变化
			const obs = new Observer(data)
			console.log(obs)

			//准备一个vm实例对象
			let vm = {}
			vm._data = data = obs

			function Observer(obj){
				//汇总对象中所有的属性形成一个数组
				const keys = Object.keys(obj)
				//遍历
				keys.forEach((k)=>{
					Object.defineProperty(this,k,{
						get(){
							return obj[k]
						},
						set(val){
							console.log(`${k}被改了，我要去解析模板，生成虚拟DOM.....我要开始忙了`)
							obj[k] = val
						}
					})
				})
```

## 使用 v-model 收集表单数据

前面学到 v-model 讲到 v-model 默认收集的就是 value 值 ,所以 v-model 还可以收集其余的表单数据.

收集表单数据：

​ 若：`<input type="text"/>`，则 v-model 收集的是 value 值，用户输入的就是 value 值。

```html
账号：<input type="text" v-model.trim="userInfo.account" />
```

​ 若：`<input type="radio"/>`，则 v-model 收集的是 value 值，且要给标签配置 value 值。

```html
男<input type="radio" name="sex" v-model="userInfo.sex" value="male" /> 女<input
  type="radio"
  name="sex"
  v-model="userInfo.sex"
  value="female" />
```

​ 若：`<input type="checkbox"/>`

​ 1.没有配置 input 的 value 属性，那么收集的就是 checked（勾选 or 未勾选，是布尔值）

```html
<input type="checkbox" v-model="userInfo.agree" />
```

​ 2.配置 input 的 value 属性:

​ (1)v-model 的初始值是非数组，那么收集的就是 checked（勾选 or 未勾选，是布尔值）

​ (2)v-model 的初始值是数组，那么收集的的就是 value 组成的数组

```html
学习<input type="checkbox" v-model="userInfo.hobby" value="study" /> 打游戏<input type="checkbox" v-model="userInfo.hobby" value="game" />
吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat" />
```

​ 备注：v-model 的三个修饰符：

​ lazy：失去焦点再收集数据

​ number：输入字符串转为有效的数字

​ trim：输入首尾空格过滤

## 过滤器

一层一层过滤,作为第一个参数传入

## 组件流程

- 创建一个组件

```html
const school = Vue.extend({ template:`
<div class="demo">
  <h2>学校名称：{{schoolName}}</h2>
  <h2>学校地址：{{address}}</h2>
  <button @click="showName">点我提示学校名</button>
</div>
`, // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。 data(){ return {
schoolName:'尚硅谷', address:'北京昌平' } }, methods: { showName(){ alert(this.schoolName) } }, })
```

```vue
<template>
  <div class="demo">
    <h2>学校名称：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <button @click="showName">点我提示学校名</button>
  </div>
</template>

<script>
export default {
  name: "School",
  data() {
    return {
      name: "尚硅谷",
      address: "北京昌平",
    };
  },
  methods: {
    showName() {
      alert(this.name);
    },
  },
};
</script>

<style>
.demo {
  background-color: orange;
}
</style>
```

- 注册组件

```vue
<template>
  <div>
    <School></School>
    <Student></Student>
  </div>
</template>

<script>
//引入组件
import School from "./School.vue";
import Student from "./Student.vue";

export default {
  name: "App",
  components: {
    School,
    Student,
  },
};
</script>
```

- 使用组件

```js
import App from "./App.vue";

new Vue({
  el: "#root",
  template: `<App></App>`,
  components: { App },
});
```
