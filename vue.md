# Npm

npm 默认的仓库地址是在国外，速度较慢，建议大家设置到淘宝镜像，

但是切换镜像是比较麻烦的，推荐一款切换镜像的工具：nrm

`我们首先安装nrm,这里-g代表全局安装`

```cmd
npm install nrm -g   #安装nrm  -g表示任何地方都可以使用nrm
nrm ls  		#检查nrm安装好没，其实就是看具体软件用的具体镜像
nrm use taobao  #使用淘宝镜像
nrm test taobao # 测试淘宝镜像的连接。

```

# nodejs

先安装nodejs。

```cmd
npm install nodejs -g  #安装nodejs
```

安装完成后记得重启电脑。

# idea中使用

## 1.初始化

`打开项目首先初始化,在Terminal中Local窗口输入npm init -y 初始化项目` 

```cmd
npm init -y #初始化项目
```

`初始化后，项目中就会多了一个package.json文件，这个就类似我们的pom文件我们可以在这里面对前端进行配置。`

## 2.安装vue

```cmd
npm install vue --save  #安装vue --save表示只在本地安装
```

## 3.Vue实例

### 3.1.创建Vue实例

每个Vue应用都是通过用`Vue`函数创一个新的Vue实例开始的：

```js
var vm =new Vue({
    //选项
})
```

在构建函数中传入一个对象，并且在对象中申明各种Vue需要的数据和方法，包括：

- el
- data
- methods
- ...

### 3.2.模版或元素

每个Vue实例都需要关联一端Html模版，Vue会基于此模版进行视图渲染。

我们可以通过el属性来指定。

例如一端Html模版：

```html
<div id="app">

</div>
```

然后创建Vue实例，关联这个div

```js
var vm=new Vue({
	el:"#app"
})
```

这样，Vue就可以基于id为app的div元素作为模版进行渲染了。在这个div范围以外的部分是无法使用vue特性的。

### 3.3.数据

当Vue实例被创建时，他会尝试获取在data中定义的所有属性。用于视图的渲染，并且监视data中的属性变化，当data发生改变，所有相关的视图都将重新渲染，这就是“响应式”系统。

html：

```html
<div id="app">
	<input type="text" v-model="name"/>
</div>
```

js:

```js
var vm= new vue({
	el:"#app",
	data:{
		name:"刘德华"
	}
})
```

- name的变化会影响到input的值
- input中的值。也会导致vm中的name发生改变

### 3.4.方法

Vue实例中除了可以定义data属性，也可以定义方法，并且在Vue的作用返回内使用。

html:

```html
<div id="app">
	<button @click="add">点我</button>
</div>
```

js:

```js
var vm=new Vue({
	el:"#app",
	data:{
	},
	methods:{
		add:function(){
			console.log("hello!")
		},
		handleClick(){
                console.log("hello!");
        }
	}
})
```

### 3.5.生命周期

[Vue生命周期]: https://www.cnblogs.com/xiaobaibubai/p/8383952.html	"所有具体的方法描述。"

#### 3.5.1.钩子函数

例如：created代表在Vue实例创建后：

我们可以在Vue中定义一个created函数，代表这个时期的构建函数：

html:

```html
<div id="app">
	{{hello}}
<div/>
```

js:

```js
var vm= new Vue({
	el:"#app",
	data:{
		hello:""  //hello初始化为空
	}，
	created(){
		this.hello="hello word! 我出生了！"
	}
})
```

#### 3.5.2 .this

我们可以看下载Vue内部的this变量是谁，我们在created的时候，打印this

```
var vm=new Vue({
	el："#app",
	data:{
		hello:""  //hello初始化为空
	}，
	created(){
		this.hello="hello word! 我出生了！";
		console.log(this);
	}
})
```

总结：`this`就是当前的vue实例，在Vue对象内部，必须使用this才能访问到Vue中定义的data内属性，方法等。 

## 4.指令

 什么是指令？

指令[Directives]是带有`v-`前缀的特殊属性，例如我们在入门案例的v-model,代表双向绑定。

### 4.1插值表达式

#### 4.1.1.花括号

格式：

```html
{{表达式}}
```

说明：

- 该表达式支持js语法。可以调用js内置函数{必须有返回值}
-  表达着必须有返回结果。例如1+1，没有结果的表达式不允许使用，如：var a=1+1;
- 可以直接获取Vue实例中定义的数据或函数。

示例：

 Html:

```html
<div id="app">{{name}}</div>
```

js:

```js
var app=new Vue({
    el:"#app",
    data:{
        name:"jack"
    }
})
```

#### 4.1.2.插值闪烁

使用{{}}方式在网速较慢时会出现问题，在数据未加载完成时，页面会显示出原始的{{}}，加载完毕后才显示正确的数据，我们称为插值闪烁。

#### 4.1.3.v-text和v-html

使用v-text和v-html指令来替代{{}}

说明：

- v-text：将数据输入到元素内部，如果输出的数据有HTML代码，会作为普通文本输出。
- v-html：将数据输出到元素内部，如果输出的数据有HTML代码，会被渲染。

示例：

HTML:

```html
<div id="app">
	v-text:<span v-text="hello"></span><br>
    v-html:<span v-html="hello"></span>
</div>
```

JS:

```JS
var app=new Vue({
    el:"#app",
    data:{
        hello:"<h1>大家好，我是杨彬茂</h1>"
    }
})
```

并且不会出现插值闪烁，当没有数据的时，会显示空白。

### 4.2.v-model

刚才的V-text和V-html可以看做是单选绑定，数据影响了视图的渲染，但是反过来就不行，接下来学习的v-model是双向绑定，视图（View）和模型（Model）之间会互相影响。

既然是双向绑定，一定是在属兔中可以修改数据，这样就限定了视图的元素类型，目前v-model的可使用元素有：

- input
- select
- textarea
- checkbox
- radio
- components(Vue的自定义组件)

基本上除了最后一项，其他都是表达的输入项。

举例：

html:

```html
<div id="app">
    <input type="checkbox" v-model="lessons" value="java"/>java
    <input type="checkbox" v-model="lessons" value="前端"/>前端
    <input type="checkbox" v-model="lessons" value="python"/>python
    <h1>
        您已购买下列课程：<span v-text="lessons.join(',')"></span>
    </h1>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script>
    var app=new Vue({
    el:"#app",
    data:{
        lessons:[]
    }
})
</script>
```

- 多个`CheckBox`对应一个model时，model的类型是一个数组，单个checkbox值是boolean类型
- radio对应的值是input的value值
- `input`和`textarea`默认对应的model是字符串
- `select`单选对应字符串，多选对应也是数组

### 4.3.v-on

#### 4.3.1.基本用法

v-on指令用于给页面元素绑定事件。

`语法`：

```js
v-on:事件名="js片段或函数名"
```

`简写语法`：

```js
@事件名="js片段或函数名"
```

例如v-on:click=‘add’可以简写为@click=‘add’

   

```html
<div id="app">
    <!--事假中直接写js片段-->
    <button @click="num++">增加</button>
     <!--时间指定一个回调函数，必须是Vue实例中定义的函数-->
    <button @click="decrement">减少</button>
    <h1>num:<span v-text=num></span></h1>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
            num:1
        },
        methods:{
           decrement(){
               this.num--;
           } 
        }
    })
</script>
```

#### 4.3.2.事件修饰符

在事件处理程序中调用`event.preventDefault()`或`event,stopPropagation()`是非常常见的需求，尽管我们可以在方法中轻松实现这点，但更好的方式是：方法值有纯粹的数据逻辑，而不是去处理DOM事件细节。

为了解决这个问题。Vue.js为`v-on`提供了时间修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。

- `.stop`:阻止事件冒泡
- `prevent`:阻止默认事件发生
- `.capture`：使用事件捕获模式
- `.self`:只有元素自身出发事件才执行。（冒泡或捕获的都不执行）
- `.once`： 只执行一次

### 4.4.v-for

遍历数据渲染页面是非常常用的需求。Vue中通过v-for指令来实现。

#### 4.4.1.遍历数组

语法：

```js
v-for="item in items"
```

- items：要遍历的数组，需要在Vue的data中定义好。
- item：迭代得到的数组元素的别名,随便命名。

示例：

```html
<div id="app">
    <ul>
        <li v-for="user in users" v-text="user.name+','+user.gender+','+user.age">
            
        </li>
        <!--下边的效果和上边效果一样的，区别在于插值闪烁-->
         <li v-for="user in users" >
            {{user.name+','+user.gender+','+user.age}}
        </li>
    </ul>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
            users:[
                {name:'张三',gender:'男',age:21},
                {name:'李四',gender:'男',age:21},
                {name:'王五',gender:'男',age:21},
                {name:'赵六',gender:'男',age:21},
            ]
        } 
    })
</script>
```

#### 4.4.2.数组角标

在遍历的过程中，如果我们需要知道数组角标，可以指定第二个参数

语法：

```js
v-for="(item,index) in items"
```

- items：要遍历的数组，需要在Vue的data中定义好。
- item：迭代得到的数组元素的别名,随便命名。
- index：迭代到的当前元素索引，从0开始。

示例：

```html
<div id="app">
  <ul>
     <li v-for="(user,index) in users" >
    	{{index}}-{{user.name+','+user.gender+','+user.age}}
    </li>
   </ul>
</div>
```

4.4.3.遍历对象

v-for除了可以迭代数组，也可以迭代对象。语法基本类似

语法

```js
v-for="value ini object"
v-for="(value,key) ini object"
v-for="(value,key,index) ini object"
```

- 1个参数时，得到的是对象的值
- 2个参数时，第一个是值，第二个是键
- 3个参数时，第三个是索引，从0开始。

```html
<div id="app">
  <ul>
     <li v-for="(value,key,index) in users[0]" >
    	{{index}}-{{key+"："+user}}
    </li>
   </ul>
</div>
```

#### 4.4.3.遍历数字

```html
<div id="app">
  <ul>
       <li v-for="i in 5">
            {{i}}
        </li>
   </ul>
</div>
```

#### 4.4.4.key

当 用`v-for`正在更新已渲染过的元素列表时。它默认用“就地复用”策略。如果数据项的顺序被改变，Vue将不会移动DOM元素来匹配数据项的顺序，而是简单复用此处每个元素，并且确保他在特定索引下显示已被渲染过的每个元素。

这个功能可以有效的提高渲染的效率。

但是要实现这个功能，你需要给Vue一些提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一`key`属性。理想的`key`值是每项都有的且唯一的`id`。

示例：

```html
<ul>
	<li v-for="(item,index) in items" :key="index"></li>
</ul>
```

- 这里使用了一个特殊语法：`:key=""`我们后面会讲到，它可以让你读取Vue中的属性，并赋值给key属性
- 这里我们绑定的key是数组的索引，应该是唯一的。

### 4.5.v-if和v-show

#### 4.5.1.基本使用

v-if ：顾名思义，条件判断。当得到结果为true时，所在的元素才会被渲染。

语法：

```js
v-if="布尔表达式"
```

示列：

```html
<div id="app">
    <!--事件中直接写js片段-->
	<button @click="show=!show">点击切换</button>
    <h1 v-if="show">
        你好
    </h1>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
         	show:true
        } 
    })
</script>
```

#### 4.5.2.与v-for结合

当v-if和v-for出现在一起时，v-for优先级更高，也就是说会先遍历，在判断条件。

示列：

```html
<div id="app">
    <!--示列一-->
    <ul>
        <li v-for="user in users" v-text="user.name+','+user.gender+','+user.age" v-if="user.gender=='女'">           
        </li>
    </ul> 
    <!--示列二-->
      <ul>
        <li v-for="i in 5" v-if="i%2===0" v-text="i"></li>
    </ul>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
            users:[
                {name:'张三',gender:'男',age:21},
                {name:'李四',gender:'男',age:21},
                {name:'王五',gender:'男',age:21},
                {name:'赵六',gender:'男',age:21},
            ]
        } 
    })
</script>
```

#### 4.5.3.v-else

你可以使用`v-else`指令来表示`v-if`的else块：

```html
<div v-if="Math.random()>0.5">
    	Now you see me
</div>
<div v-else>
    	Now you don't
</div>
```

`v-else`元素必须要紧跟在`v-if`或者`v-else-if`的元素的后面，否则它将不会被识别。

`v-else-if`,顾名思义。充当`v-if`的else-if块。可以连续使用：

```html
<div v-if="type==='A'">
    A
</div>
<div v-else-if="type==='B'">
    B
</div>
<div v-else-if="type==='C'">
    C
</div>
<div v-else>
    Not A/B/C
</div>
```

类似`v-else`，`v-else-if`也必须紧跟在带`v-if`或`v-else-if`的元素之后。

#### 4.5.4.v-show

另一个用于根据条件展示元素的选项是`v-show`指令。用法大致一样：

```html
<h1 v-show="ok">Hello</h1>
```

和`v-if`效果一样。不同的是，在界面渲染过程中，v-if是直接重写渲染DOM元素，而v-show是在元素标签上给display效果。

### 4.6.v-bind

#### 4.6.1.属性上使用vue数据

看这样一个案例：

我们提前定义了一些CSS样式：

```css
div {
    width:100px;
    height:100px;
    color:darkgray
}
.red{
    background-color:red;
}
.blue{
    background-color:blue;
}
```

然后定义页面：

```html
<div id="app">
    <button @click="color='red'">红</button>
    <button @click="color='blue'">蓝</button>
	<div :class="color">
        点击按钮。背景会切换颜色噢
    </div>
    <!-- :class是v-bind:class的简写-->
    <div v-bind:class="color">
        点击按钮。背景会切换颜色噢
    </div>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
        	color:"red"
        } 
    })
</script>
```

解读：

- 首页有两个按钮，点击时，会改变Vue实例中的color值，这个值与前面定义的css样式一致。
- 目前div的class为空，我们希望实现点击按钮后，div的class样式会在.red和。blue之间切换

该如何实现？

​	既然color值会动态变化为不同的class名称，name我们直接把color注入到class属性就好了。于是就这样写：

```html
<div class="{{color}}"></div>
```

这样写是错误的！因为插值表达式是不能用在标签的属性中。

此时，Vue提供了一个新的指令来解决：v-bind,语法：

```js
v-bind:属性名="Vue中的变量"
```

例如，在这里，我们可以写成：

```html
<div v-bind:class="color"></div>
```

不过，v-bind太麻烦，因此可以省略，直接写成：	`:属性名="属性值"`，即：

```html
<div :class="color"></div>
```

#### 4.6.2.class属性的特殊用法

上边虽然实现了颜色切换，但是语法却比较啰嗦。

Vue对class属性进行了特殊处理，可以接受数组或对象格式

对象语法：

我们

传给`:class`一个对象，以动态地切换class:

```html
<div :class="{red:true,blue:false}"></div>
```

- 对象中，key是已经定义的class样式的名称，如本例中的：`red`和`blue`
- 对象中，value是一个布尔值，如果为true,则这个样式会生效，如果为false,则不生效。

之前的案例可以改成这样：

```html
<div id="app">
    <button @click="boo=!boo">点击切换背景</button>
	<div :class="{red:boo,blue:!boo}">
        点击按钮。背景会切换颜色噢
    </div>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
        	boo:true,//一个布尔标记，判断样式是否生效。
        } 
    })
</script>
```

- 首先class绑定的是一个对象：`{red:boo,blue:!boo}`
  - red和blue两个样式的值分别是boo和!boo，也就是说这两个样式生效标记恰好相反，一个生效，另一个失败。
  - boo默认为true,也就是说默认的red生效，blue不生效。
- 现在只需要一个按钮即可，点击时对boo取反，自然实现了样式的切换

### 4.7.计算属性

在插值表达式中使用js表达式是非常方便的，而且也经常被用到。

但是如果表达式的内容很长，就会显得不够优雅，而且后期维护起来也不方便，例如下面的场景，我们有一个日期的数据，但是是毫秒值：

```js
data:{
	birthday:1529032123201 //毫秒值
}
```

我们在页面渲染，希望得到yyyy-MM-dd的样式：

```html
<h1>您的生日是{{
    new Date(birthday).getFullYear()+"-"+new Date(birthday.getMonth()+"-"+new Date(birthday.getDay()))
    }}
</h1>
```

虽然得到结果，但是非常麻烦。

Vue中提供了计算属性，来替代复杂的表达式：

```js

<script>
    const app = new Vue({
        el:"#app" ,
        data: {
            birthday:1529032123201
        },
        computed:{//所有的计算属性，都要放在这个computed下边。
            birth(){
                const day=new Date(this.birthday);
                return day.getFullYear()+"年"+day.getMonth()+"月"+day.getDay()+'日'
            }
        }
    });
</script>

```

- 计算属性本质就是方法，但是一定要返回数据。然后页面渲染时，可以把这个方法当成一个变量来使用。

页面使用：

```html
<div id="app">
    <h1>
        您的生日是：{{birth}}
    </h1>
</div>
```

### 4.8.watch

#### 4.8.1.监控

watch可以让我们监控一个值的变化。从而做出相应的反应。

示例：

```html
<div id="app">
    <input type="text" v-model="message">
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
        	message:"",
        },
        watch:{
            message(newVal,oldVal){
                console.log(newVAL,oldVal)
            }
        }
    })
</script>
```

####  4.8.2.深度监控

如果监控的是一个对象，需要进行深度监控，才能监控对象中属性的变化，例如：

```html
<div id="app">
    姓名：<input type="text" v-model="person.name"><br>
    年龄：<input type="text" v-model="person.age">
    <button @click="person.age++">+</button>
    <h1>
        {{person.name}}今年{{person.age}}岁了
    </h1>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    var app=new Vue({
        el:"#app",
        data:{
        	message:"",
        },
        watch:{
            person:{
                deep:true,//开启深度监控，可以监控对象中属性变化
                handler(val){//定义监控到以后的处理方法，必须是handler这个名字
                    console.log(val.name+":"+val.age)
                }
            }
        }
    })
</script>
```

变化：

- 以前定义监控时，person是一个函数，现在改成了对象，并且要直到两个属性：
  - deep:代表深度监控，不仅监控person变化，也监控person中属性变化。
  - handier：就是以前监控处理函数。

##   5.组件化 

在大型应用开发的时候，页面可以划分成很多部分，往往不同的页面也会有相同的部分。例如可能会有相同的头部导航。

但是如果每个页面都独自开发，这无疑增加了我们开发的成本。所以我们会把页面的不同部分拆分成独立的组件，然后在不同页面就可以共享这些组件，避免重复开发。

### 5.1.定义全局组件

我们通过vue的component方法来定义一个全局组件。

```html
<div id="app">
    <!--使用定义好的全局组件-->
    <counter></counter>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    Vue.component("counter",{
        template:"<button v-on:click='count++'>你点了我{{count}}次，我记住了。</button>"
        data(){
        	return{
                count:6
            }
    }
    })
    var app=new Vue({
        el:"#app",
    })
</script>
```

- 组件其实也是一个Vue实例。因此他在定义时也会接收：data、methods、生命周期函数等。
- 不同的是组件不会与页面的元素绑定，否则就无法复用，因此没有el属性。
- 但是组件渲染需要html模版，所以增加了template属性，值就是html模版
- 全局组件定义完毕。任何Vue实例都可以直接在HTML中通过组件名称来使用组件了。
- data的定义方式比较特殊，必须是一个函数。

### 5.2.组件的复用

定义好的组件，可以任意复用多次：

```html
<div id="app">
    <counter></counter>
    <counter></counter>
    <counter></counter>
</div>
```

你会发现每个组件互不干扰，都有自己的count值。怎么实现的？

组件的data属性必须是函数：

当我们定义这个`<Counter>`组件时，它的data并不是像这样直接提供一个对象：

```js
data：{
	count:6
}
```

取而代之的是，一个组件的data选项必须是一个函数。因此每个实例可以维护一份呗返回对象的独立拷贝：

```js
data:funsion(){
	return {
		count:6
	}
}
//也可以下边这样写
data(){
	return {
		count:6
	}
}
```

如果Vue没有这条规则。点击一个按钮就会影响到其他所有实例！

### 5.3.局部注册

一旦全局注册，就意味着即便以后你不在使用这个组件，他依然会随着Vue的加载而加载。

因此，对于一些并不频繁使用的组件，我们会采用局部注册，

我们先在外部定义一个对象，结构与创建组件时传递的第二个参数一致：

```js
    const counter= {
        template: "<button @click='count++'>点我试试，我记住你了！点了我{{count}}次！</button>",
        data() {
            return {
                count: 0,
            }
        }
    };
```

然后在Vue中使用它：

```js
const app=new Vue({
        el:"#app",
        data:{
        },
        components:{
            counter:counter
        }
    })
```

- components就是当前Vue对象组件集合。
  - 其key就是子组件名称
  - 其值就是组件对象的属性
- 效果与刚才的全局组成是类似的，不同的是，这个counter组件只能在当前Vue实例中使用。

### 5.4.组件通信

通常一个页面应用会以一颗嵌套的组件树的形式来组织：

- 页面首先分成了顶部导航、左侧内容区，右侧边栏三部分
- 左侧内容区又分为上下两个组件
- 有侧边栏中又包含了3个子组件

每个组件之间以嵌套 的关系组合在一起，name这个手不可避免的会有主见间的通信需求。

#### 5.4.1.父向子传递props

比如我们有一个子组件：

```js
 Vue.component("introduce",{
 	//直接使用props接收到的属性来渲染页面
 	template:"<h1>{{title}}</h1>",
 	props:{title} //通过props来接收一个父组件传递的属性。
 })
```

- 这个子组件中要使用title属性渲染页面，但是自己并没有title属性
- 通过props来接收父组件属性，名为title

父主键使用子组件，同时传递title属性：

```html
<div id="app">
    <h1>打个招呼：</h1>
    <!--使用子组件，同时传递title属性-->
    <introduce :title="msg"></introduce>
    <for-component :title="lessons"></for-component>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    //第一种简单方式
    Vue.component("introduce",{
        //直接使用props接收到的属性来渲染页面
        template:"<h1>{{title}}</h1>",
        props:{"title"} //通过props来接收一个父组件传递的属性。
     })
    
    //第二种方式
     const forComponent={
         //直接使用props接收到的属性复杂写法
        template: "<ul><li v-for='item in items'>{{item}}</li></ul>",
        props:{
            items:{ 
                type:Array,
                default:['默认课程1','默认课程2']
            }
        }
    }
    
    
    var app=new Vue({
        el:"#app",
        data:{
            msg:"大家好",
            lessons:['java','c#','c++','python','php']
        },
           components:{//如果是局部注册的组件。即不是Vue.component就要在Vue对象里注册。
            forComponent  //等同于forComponent:forComponent
        }
        
    })
    
    
</script>
```

#### 5.4.2.传递复杂数据

我们定义一个子组件：

```js
const myList={
    template:`<ul>
				<li v-for='item in items' :key=item.id>{{itme.id}:{{item.name}}}</li>
			   </ul>`,
    props:{//通过props来接收父组件传递的属性
        items:{//这里定义item属性
            type:Array,//要求必须是Array类型
            default:[] //如果父组件没有穿。那么给定默认值是[]
        }
        
    }
}
```

-  这个子组件可以对items进行迭代，并输出到页面。
- 但是组件中并为定义items属性。
- 通过props来定义需要从父组件中接收的属性
  - items：是要接受的属性名称
    - type：限定父组件传递来的必须是数组，否则报错。
    - default：默认值

我们在父组件中使用它：

```html
<div id="app">
    <h2>开设的课程</h2>
    <!--使用子组件的同时，传递属性。这里使用了v-bind,指向父组件自己的属性：lessons-->
    <my-list :items="lessons"></my-list>
</div>
```

```js
Vue app=new Vue({
    el:"#app",
    components:{
        myList //当key和value一样时，可以只写一个
    },
    data:{
        lessons:[
            {id:1,name:'java'},
            {id:2,name:'php'},
            {id:3,name:'python'}
        ]
    }
})
```

#### 5.4.3.子向父的通信

来看这样的一个案例：

```html
<div id="app">
    <h2>num:{{num}}</h2>
    <counter :num="num"></counter>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script type="text/javascript">
    Vue.components('counter',{
        //子组件，定义了两个按钮，点击数字num会加或减
        template:`<div>
                        <button @click='handleAdd'>加</button>
                        <button @click='handleReduce'>减</button>
                        <h1>Num:{{num}}</h1> 
                    </div>`,
        props:['num']//count是从父组件获取的。
    })
    
    var app=new Vue({
        el:"#app",
        data:{
            count:0
        }
    })
</script>
```

- 子组件接收父组件的num属性
- 子组件定义点击按钮，点击后对num进行加或减操作

我们尝试运行：就会报错，大概错误意思就是不能直接对子组件操作。而是应该去改变父组件的值，从而影响子组件。

```js
var app=new Vue({
	el:"#app",
    data:{
        count:0
    },
    methods:{//父组件中定义操作num的方法。
     	add(){
            this.count++;
        },
        reduce(){
            this.count--;
        }
    }
})
```

但是，点击按钮是在子组件中，那就是说需要子组件来调用父组件的函数，怎么做？

我们可以通过v-on指令将父组件的函数绑定到子组件上：

```html
<div id="app">
    <h2>count:{{count}}</h2>
    <connter @incr="add" @redvce="reduce"></connter>
</div>
```

然后，当子组件中按钮被点击时，调用绑定的函数：

```js
 Vue.components('counter',{
        //子组件，定义了两个按钮，点击数字num会加或减
        template:`<div>
                        <button @click='handleAdd'>加</button>
                        <button @click='handleReduce'>减</button>
                        <h1>Num:{{num}}</h1> 
                    </div>`,
        methods:{
              handleAdd(){
                this.$emit('incr')
            },
            handleReduce(){
                this.$emit('decr')
            }
        }
    })
```

- vue提供了一个内置的this.$emit函数。用来调用父组件绑定的函数

总结：

1. 首先要正常定义一个父组件。如果想要子组件操作父组件的某个属性参数，你就在父组件中写对应属性参数的操作方法。
2.  然后在定义全局或者局部组件也就是子组件。然后在子组件里写对应的html标签也就是template参数。然后在子组件里定义方法指定这个方法在页面的html标签中（也就是上边`<connter @incr="add" @redvce="reduce"></connter>`中@后面incr或者redvce）对应的名字。
3. 最后在页面标签中（@后面incr或者redvce的等号后面）绑定对应主组件的相关方法。

子组件不能直接修改父组件传递参数的引用或者基本类型参数值，子组件可以修改父组件对象类型参数的属性。



















# ps:页面























































































`建立一个hello.html页面`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <button @click="handleClick">点我</button>
    <button @click="add">add</button>
    <input type="text" v-model="num"> <!--输入框和对象绑定-->
    <button @click="num++">+</button> <!--按钮和对象绑定-->
    <h1>
        {{name}} 非常帅
        <br>
        {{num}}位女神为其着迷！
    </h1>
</div>
<script src="node_modules/vue/dist/vue.js"></script>
<script>
    const app = new Vue({
        el:"#app" ,  //element vue作用的标签  绑定标签
        data:{   //所有的属性都放在data里面
            name:"杨彬茂",
            num:1,
        },
        methods:{ //所有的方法都放在methods里面。
            handleClick(){    //方法命名方式一
                console.log("hello!");
            },
            add:function () {   //方法命名方式二
                console.log("add")
            }
        }
    });
</script>
</body>
</html>
```

