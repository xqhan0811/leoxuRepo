# 1.Vue实例与数据绑定

## 1.1实例与数据

```js
let app = new Vue({
    //选项
});
```

app代表了这个Vue实例



```js
let app = new Vue({
    el:'#app'	//	el:document.getElementById('app')
    data:{
    	name:'hello vue'
	}
});
```

`el`是必不可少的选项. `el`指定一个页面中已存在的DOM来挂载Vue实例.它可以是HTMLElement,也可以是CSS选择器

我们可以通过 `app.$el `来访问该元素(`app.$data` ...)

处理显示的声明数据外,也可以指向一个已有的变量

```js
let myData={
    name:'hello vue'
}

let app = new Vue({
    el:'#app'
    data:{
    	name:myData
	}
});
```

## 1.2 插值与表达式

使用双大括号(Mustache 语法)`{{}}` 最基本的插值方法



# 2. 指令与事件

指令(Directives) 是Vue.js模板中最常用的一项功能,它带有前缀v-

指令的主要职责就是当其表达式的值改变时,相应地将某些行为应用到DOM上,入v-if

`v-bind`: 的基本用途是动态更新HTML元素上的属性,比如id,class等

```html
<div id="app">
    <a :href="url"></a>
    <img :src="imgUrl" alt="picture">
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            url:'https://www.github.com',
            imgUrl:'http://xxx.xxx.xx/img.png'
        }
    });
</script>
```



`v-on`: 用来绑定事件监听器

```html
<div id="app">
    <button @click="handleClose">点我</button>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        methods:{
            handleClose : function (){
                console.log('hello vue');
            }
        }
    });
</script>
```



在普通元素上,v-on可以监听原生的DOM事件,除了click外,还有dbclick,keyup,mousemove等



## 2.1 语法糖

语法糖是指在不影响功能的情况下,添加某种方法实现同样的效果,从而方便程序的开发

`v-bind:src` 可以缩写成 `:src`

`v-on:click` 可以缩写成 `@click`



## 2.2 内置指令

### 2.2.1 基本指令

- v-cloak 配合css使用

  ```css
  [v-cloak]{
      display: none;
  }
  ```

- v-once



### 2.2.2 条件渲染指令

- v-if v-else-if v-else

  ```html
  <div id="app">
      <p v-if="status===1">status=1</p>
      <p v-else-if="status===2">status=2</p>
      <p v-else>other</p>
  </div>
  <script src="vue.js"></script>
  <script>
      let app = new Vue({
          el:'#app',
          data:{
              status:1
          }
      });
  </script>
  ```

  如果判断包含多个元素,可以在Vue.js内置的<template>上使用

  ```html
  <div id="app">
  	<template v-if="status===1">
      	<p>aaa</p>
          <p>bbb</p>
          <p>ccc</p>
      </template>
  </div>
  ```

  Vue在渲染元素时,出于效率考虑,会尽可能复用已有的元素而非重新渲染.如果你不希望这样做可以使用Vue.js提供的key属性



- v-show

  不能再<template>上使用

  v-show 的用法与v-if基本一致，只不过 v-show是改变元素的 css属性 display。当 v-show 表 达式的值为 false时， 元素会隐藏，查看 DOM 结构会看到元素上加载了内联样式 display:none;

  v-if 和v-show 具有类似的功能，不过 v-if 才是真正的条件渲染，它会根据表达式适当地销毁 

  或重建元素及绑定的事件或子组件。若表达式初始值为 false ，则一开始元素／组件并不会渲染，只 有当条件第一次变为真时才开始编译。



### 2.2.3 列表渲染指令 

- v-for 当需要将一个数组遍历或枚举一个对象循环显示时，就会用到列表渲染指令 v-for。它的表达 式需结合in来使用，类似 item in items 的形式

  ```html
  <div id= ” app ” > 
      <ul> 
      	<li v-for ＝”book in books ” >{ { book.name } }</li>
      </ul> 
  </div>
  <script src="vue.js"></script>
  <script>
      let app = new Vue({
          el:'#app',
          data:{
              books: [ 
  				{name:' <Vue . js实战》’｝ ，
                  {name:’《JavaScript语言精粹》’｝，
                  {name:’《JavaScript 高级程序设计》’｝
               ]
          }
      });
  </script>
  ```

  v-for的表达式支持一个可选参数作为当前项的索引

  ```html
  <li v-for= ”( book , index) in books ” >{{ index}} -{{book .name })</li>
  ```

  与 v-if 一样， v-for 也可 以用 在 内 置标签＜template＞上，将多个元素进行渲染.

  除了数组外，对象的属性也是可以遍历的,遍历对象属性时，有两个可选参数，分别是键名和索引

  v-for还可以迭代整数

  ```html
  <span v-for="n in 10">{{n}}</span>
  ```

  

## 2.3 方法与事件

Vue 提供了一个特殊变量`$event`,用于访问原生DOM事件

```html
<div id="app">
	<a href="http://www.apple.com" @click="handleClick('禁止打开',$event)">			打开链接
    </a>
</div>
<script>
	let app = new Vue({
        el:'#app',            
        methods:{
            handleClick:function(message,event){
                event.preventDefault();
                window.alert(message);
            }
        }
    });
</script>
```





# 3. 计算属性

最终要返回一个结果

计算属性中,只要有一个属性发生变化,计算属性就会自动重新执行,视图中的数据也会变化

```html
<script>
	let app = new Vue({
        el:'#app';
        data:{
        	num1:1,
        	num2:2,
    	},
        computed:{
        	sum : function(){
        		return num1 + num2;
    		}	              
        }
    });
</script>
```



每个计算属性都包含一个getter和setter ,上面的示例都是计算属性的默认用法,只是利用了getter来读取.在你需要的时,也可以提供一个setter函数,当手动秀海计算属性的值就像修改一个普通数据那样时,就会触发setter函数,执行一些自定义的操作

```html
<script>
	let app = new Vue({
        el:'#app';
        data:{
        	firstName:'Jack',
        	lastName:'Green',
    	},
        computed:{
        	fullName:{
        		//getter,用于获取
                get:function(){
        			return this,firstName+' '+this.lastName;
    			},
                //setter //写入时触发
                set:function(newValue){
                    let names = newValue.split(' ');
                    this.firstName = names[0];
                    this.lastName = names[names.length-1];
                }
    		}	              
        }
    });
</script>
```



计算属性除了上述的简单的文本插值外,还经常用于动态地设置元素的样式名称class 和内联样式style.当时用组件时,计算属性也经常用来动态的传递props



计算属性还有两个很实用的小技巧容易被忽略:

1.计算属性可以依赖其他计算属性

2.计算属性不仅可以依赖当前Vue实例的数据,还可以依赖其他实例的数据



# 4. v-bind及class与style绑定

## 4.1 绑定class的几种方式

### 4.1.1 对象语法

给v-bind:class设置一个对象,可以动态的切换class

```html
<div id="app">
    <div :class="{'active':isActivve}"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            isActive:true
        }
    });
</script>
```

类名active依赖于数据isActive,当其为true时,div会拥有类名active,为false时则没有,所以最终渲染完后是:<div class="active"></div>

对象中可以传入多个属性,来动态切换class. :class可以和普通的class共存

当:class的表达式过长或逻辑复杂时,可以绑定一个计算属性.一般当条件多余2个,都可以使用data或computed

```html
<div id="app">
    <div :class="classes"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            isActive:true,
            error:null
        },
        computed:{
            classes:function (){
                return {
                    active:this.active && !this.error,
                    'text-fail':this.error && this.error.type === 'fail'
                }
            }
        }
    });
</script>
```





### 4.1.2 数组语法

当需要多个class时,可以使用数组语法,给:class绑定一个数组,应用一个class列表

```html
<div id="app">
    <div :class="[activeCls,errorCls]"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            activeCls:'active',
            errorCls:'error'
        }
    });
</script>
```

渲染后的结果:<div class="active error"></div>

也可以使用三元表达式来根据条件切换class

```html
<div id="app">
    <div :class="[isActive ? activeCls : '',errorCls]"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            isActive:true,
            activeCls:'active',
            errorCls:'error'
        }
    });
</script>
```

样式error会始终应用,当isActive为真时,样式active才会被应用

class有多个条件时,这样写会比较繁琐,可以在数组语法中使用对象语法

```html
<div id="app">
    <div :class="[{'active': isActive},errorCls]"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            isActive:true,
            errorCls:'error'
        }
    });
</script>
```

与对象语法一样,也可以使用data,computed和methods 三种方法,以计算属性为例

```html
<div id="app">
    <div :class="clssses"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            size:'large',
            disabled:true
        },
        computed:{
            classes:function (){
                return [
                    'btn',
                    {
                        ['btn-' + this.size]: this.size !== '',
                        ['btn-disabled'] : this.disabled
                    }
                ]
            }
        }
    });
</script>
```

btn的样式会始终应用,当数据size不为空时,会应用样式前缀btn-, 后加size的值:当数据为disabled为真的时候,会应用样式btn-disabled,所以该示例最终会渲染的结果为:

```html
<div class="btn btn-large btn-disabled"></div>
```



### 4.1.3 在组件上使用

如果直接在自定义组件上使用class或:class,样式规则会直接应用到这个组件的根元素上,例如声明一个简单的组件

```html
Vue.component('my-component',{
	template:'<p class="article">一些文本</p>'
});
```

调用组件

```html
<div id="app">
    <my-component :class="{'active':isActive}"></my-component>
</div>
<script>
	let app = new Vue({
        el:'#app',
        data:{
            isActive:true
        }
    });
</script>
```

最终组件渲染后的结果:<p class="article active">一些文本</p>

这样的用法仅适用于自定义组件的最外层是一个根元素,否则会无效,当不满足这种条件或需要给具体的子元素设置类名时,应当适用组件的props来传递.这些用法同样适用绑定内联样式style的内容



## 4.2 绑定内联样式

使用v-bind:style(:style)可以给元素绑定内联样式,与:class类似

```html
<div id="app">
    <div :style="{'color' : color,'fontSize' : fontSize + 'px'}"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            color:'red',
            fontSize:14
        }
    });
</script>
```

渲染后:<div style="color:red;font-size:14px;">文本</div>

直接写一长串的样式不便于阅读和维护,所以一般写在data或者computed里,以data为例

```html
<div id="app">
    <div :style="styles"></div>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            styles:{
                color:'red',
            	fontSize:14+'px'
            }
        }
    });
</script>
```



应用多个样式对象时,可以使用数组语法:

```html
<div :style="[styleA,styleB]">文本</div>
```

在实际业务中,:style的数组语法并不常用,因为往往可以写在一个对象里面;而较为常用的应当是计算属性.此外,在使用:style时,Vue.js会自动给特殊的CSS属性名称增加前缀,比如transform



# 过滤器

Vue.js支持在{{}}插值的尾部添加一个管道符`|`对数据进行过滤,经常用于格式化文本

```html
<div id="app">
    {{data | formatDate}}
</div>
```



```js
let app = new Vue({
    el:'#app',
    data:{
        name:'hello vue',
        date:new Date()
    },
    filters:{
        formatDate:function (value){
            let  date=  new  Date(value);
            return date.toLocaleDateString() + ' ' + date.toLocaleTimeString();
        }
    }
});
```



过滤器可以串联,而且可以接收参数,例如:

```html
<!-- 串联 -->
{{ message | filterA | filterB }}
<!-- 接收参数 -->
{{ message | filterA('arg1','arg2') }}
```

这里的字符串arg1和arg2讲分别传给过滤器的第二个和第三个参数,因为第一个是数据本身.

如果要实现更为复杂的数据变换,应该使用计算属性



# 5 . 表单与 v-model

```html
<div id="app">
    <input type="text" v-model="message" placeholder="输入..."/>
    <p>输入的内容是:{{message}}</p>
</div>
<script>
	let app = new Vue({
        el:'#app',
        data:{
            message:''
        }
    });
</script>
```



单选按钮:

在单独使用时,不需要v-model,直接使用v-bind绑定一个布尔类型的值,为真时选中,为否时不选

```html
<div id="app">
    <input type="radio" :checked="picked"/>
    <label>单选按钮</label>
</div>
<script>
	let app = new Vue({
        el:'#app',
        data:{
            picked:true
        }
    });
</script>
```

 如果是组合使用来实现互斥选择的效果,就需要v-model配合value来使用:

```html
<div id="app">
    <input type="radio" v-model="picked" value="html" id="html"/>
    <label for="html">html</label>
    <br>
    <input type="radio" v-model="picked" value="js" id="js"/>
    <label for="js">js</label>
    <br>
    <input type="radio" v-modeld="picked" value="css" id="css"/>
    <label for="css">css</label>
    <br>
    <p>选择的项是:{{picked}}</p>
</div>
<script>
	let app = new Vue({
        el:'#app',
        data:{
            picked:'js'
        }
    });
</script>
```

复选框:

单独使用时和单选框不同,使用v-model绑定布尔类型的值

组合使用时,也是v-model和value一起,多个勾选框都绑定到同一个数组类型的数据,value的值在数组当中,就会选中这一项.这一过程也是双向的,在勾选时,value的值也会自动push到这个数组中

```html
<div id="app">
    <input type="checkbox" v-model="picked" value="html" id="html"/>
    <label for="html">html</label>
    <br>
    <input type="checkbox" v-model="picked" value="js" id="js"/>
    <label for="js">js</label>
    <br>
    <input type="checkbox" v-model="picked" value="css" id="css"/>
    <label for="css">css</label>
    <br>
    <p>选择的项是:{{picked}}</p>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            picked:['js','css']
        }
    });
</script>
```



选择列表

```html
<div id="app">
    <select v-model="selected">
        <option>html</option>
        <option value="js">JavaScript</option>
        <option>css</option>
    </select>
    <p>选择的项是:{{selected}}</p>
</div>
<script src="vue.js"></script>
<script>
    let app = new Vue({
        el:'#app',
        data:{
            selected:'html'
        }
    });
</script>
```



<option>是备选项,如果含有value属性,v-model就会优先匹配value;如果没有,就会直接匹配<option>的text,比如第二个选中时,selected的值是js,而不是JavaScript



给<selected> 添加 multiple 就可以多选了,此时v-model绑定的是一个数组

```html
<script>
    let app = new Vue({
        el:'#app',
        data:{
            selected:['html','css']
        }
    });
</script>
```



在业务中,<option>经常用v-for动态输出,value和text也是用v-bind来动态输出的



## 5.1 修饰符

- .lazy
- .number
- .trim



# 6. 组件

## 6.1 全局组件



```html
<div id="app">
    <my-component></my-component>
</div>
<script src="vue.js"></script>
<script>
    Vue.component('my-component',{
        template:'<div>这里是组件的内容</div>'
    });
    let app = new Vue({
        el:'#app'
    });
</script>
```



## 6.2 局部组件

```html
<div id="app">
    <my-component></my-component>
</div>
<script src="vue.js"></script>
<script>
    let Child = {
        template:'<div>局部组件</div>'
    };
    let app = new Vue({
        el:'#app',
        components:{
            'my-component':Child
        }
    });
</script>
```



Vue组件模板在某些情况下回受到HTML的限制,比如<table>内规定只允许<tr>,<td>等,所以在<table>内直接使用组件时无效的.在这样的情况下,可以使用特殊的is属性来挂载组件:

```html
<div id="app">
    <table>
        <tbody is="my-component"></tbody>
    </table>

</div>
<script src="vue.js"></script>
<script>
    let Child = {
        template:'<div>局部组件...</div>'
    };
    let app = new Vue({
        el:'#app',
        components:{
            'my-component':Child
        }
    });
</script>
```



## 6.3 组件传值

###  6.3.1 父传子

子组件使用 props 选项来声明需要从父级接收的数据

props的值可以是2种

- 数组
- 对象 (当props需要验证时,就需要对象的写法了)



# 生命周期

每个Vue实例创建时,都会经历一系列的初始化过程,同事也会调用相应的生命周期钩子,我们可以利用这些钩子,在合适的时机执行我们的业务逻辑.比如jQuery的ready()方法,比如以下示例

```js
$(document).ready(function(){
    //DOM加载完后,会执行这里的代码
});
```



Vue生命周期钩子比较常用的有

`created`: 实例创建完后调用,此阶段完成了数据的观测等,但是尚未挂载,$el还不可以使用.需要初始化处理一些数据时会比较有用.

`mounted`: el挂载到实例后调用,一般我们的第一个业务逻辑会在这里开始.

`beforeDestroy`: 实例销毁前调用.主要解绑一些使用addEventListener监听的事件.



# 数组更新

Vue 的核心是数据与视图的双向绑定，当我们修改数组时， Vue 会检测到数据变化，所以用 v-for 渲染的视图也会立即更新。Vue包含了 一组观察数组变异的方法，使用它们改变数组也会触 发视图更新：

- push()

- pop()

- shift()

- unshif()

- splice()

- sort()
- reverse()

使用以上方法会改变被这些方法调用的原始数组，有些方法不会改变原数组，例如：

- filter()
- concat()
- slice()

它们返回的是一个新数组，在使用这些非变异方法时，可以用新数组来替换原数组