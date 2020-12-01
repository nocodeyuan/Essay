## `Vue`学习笔记

### `MVVM`

*  `Model View ViewModel`

* `Vue-MVVM`
  * 视图：`VIEW: DOM`
  * 模型：`MODEL: Javascript Objects`
  * 视图模型`VIEWMODEL: VUEAPPLICATION(DOM Listeners&Data Bindings)`

### `OPTIONS`

* `el`: 字符串或节点对象。

* `data`：函数。

* props：接收父组件传值。

  * 可以接收对象或数组。

  * 对象

    * type
    * default
    * required

    ```
    props:{
    	//基础类型检查
    	propA: Number,
    	//多个可能的类型
    	propB: [String, number],
    	//必须的字符串
    	propC: {
    		type: String,
    		required: true
    	},
    	//默认值数字
    	propD: {
    		type: Number,
    		default: 100
    	},
    	//带有默认的对象
    	propE: {
    		type: Object,
    		default: function(){
    			return {
    				message: 'hello'
    			}
    		}
    	},
    	//自定义验证函数
    	propF: {
    		validator: function(value){
    			return ['success', 'warning', 'danger'].indexOf(value) !== -1;
    		}
    	}，
    	//通过新建类自定义类型
    }
    ```

* `watch`: 监听数据的改变，以需要监听的属性为键名，值为自定义函数接收新值和旧值为参数。

* `methods`：`[key: string]: function`

* `compted`：计算属性，对需要展示数据的计算处理，作为属性调用，调用有缓存。

  * 对象，set和get方法。
    * set方法直接更改data的值。
    * get方法直接获取并计算data的值。
  * 函数，只读，get方法。

* filters：过滤属性，在模板属性值后使用，在`|`之后的声明函数引用。

* 指令

  * `v-bind`：变量绑定到元素属性。

    * 动态绑定class/style。

  * `v-on`： 事件绑定。

    * **添加参数，如果需要event，则在调用中传入$event**。

    * 修饰符：

      * ```
        * .stop：阻止事件冒泡。
        
        * .prevent：阻止默认事件。
        
        * .native：如果要监听根元素的原生事件，可以使用。
        
        * .capture：添加事件监听器时使用事件捕获模式，即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 。
        
        * .self：只当在 event.target 是当前元素自身时触发处理函数，即事件不是从内部元素触发。
        
        * .once：仅触发一次。
        
        * .passive：<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
        			<!-- 而不会等待 `onScroll` 完成  -->
        			<!-- 这其中包含 `event.preventDefault()` 的情况 -->
        	
        * 按键监听
        	.enter、.tab、.delete、.esc、.space
        
        * .exact：修饰符允许你控制由精确的系统修饰符组合触发的事件，ctrl只有ctrl，alt+shift不再触发。	
        
        * 鼠标监听
        ```
      
    
    	.up、.down、.left、.right
    
    
  
* `v-model`： 表单的双向数据。
  
  * v-model用于单选框，v-model绑定的属性和name属性功能相似。v-model可以获取表单的值。
  
  * 表单类型：
  
    text、radio单选框、checkbox复选框、select下拉单选/select multiple下拉多选。
  
  * 修饰符
  
    	.lazy文本框防抖策略、.number文本框内容转换number类型、.trim去除空格
  
* `v-for`： 列表渲染。
  
  * :key绑定唯一，优化diff算法性能。
  
* `v-once`：仅渲染一次。
  
* `v-show`：显示隐藏。
  
* `v-if`：条件渲染，比较消耗性能，建议经常操作使用`v-show`。
  
* `v-html`: 用于展示节点字符串。

* `v-text`: 代替插值语法。

* `v-pre`：不解析插值语句。

* `v-cloak`：用于延迟解析，绑定到根元素，在等待渲染过程中使用`css`设置元素不显示。



### 组件化

#### 使用组件

* 创建组件构造器，Vue.extend({配置对象})
* 注册组件，Vue.component(组件标签名，组件变量/组件构造器对象)**全局注册**，**局部注册**是在componets的属性中写键值对，键名为标签名，值为注册组件的构造器实例名。
* 使用组件，标签形式。
* **子组件注册名不可出现大写，子组件传值自定义事件名不可出现大写。**
* 组件模板分离
  * 写到script标签中，type设置为text/x-template，用id标识。
  * 写到template标签中，类似。
* 组件网络请求，网络请求在父组件进行。




#### 父子组件传值

* 父传子，props

```js
//props验证
props: {
	//基础类型验证（null匹配任意类型）
	propA: Number,
	//多个可能的类型
	propB: [String, Number],
	//必填字符串
	propC: {
		type: String,
		required: true
	},
	//带有默认值的数字
	propD: {
		type: Number,
		default: 10
	},
	//带有默认值的对象
	propE: {
		type: Object,
		default: function(){
			return {
				message: 'aa',
				num: 100
			}
		}
	},
	//自定义验证函数
	propF: {
		validator: function(value){
			return ['success','warning', 'danger'].indexOf(value) !== -1;
		}
	}
}
```

* 子传父，$emit events自定义事件。

```js
//在子组件的事件中自定义事件将参数传给父组件，父组件通过绑定该事件触发执行。
childClick(item){
    this.$emit('item-click', item)
}
//v-on:'item-click(item)'
parentClick(item){
    console.log(item)
}
```

* 案例

```html
<div id="app">
    <div>
        <childcomponent :list="newPro" @add-item="addItem"></childcomponent>
    </div>
</div>
<template id="cpn">
    <div>
        <h1>{{msg}}</h1>
        <ul>
            <li v-for="item in list" :key="item">{{item}}</li>
        </ul>
        <input type="text" v-model="productItem" />
        <button @click="sendItem">ADD</button>
    </div>
</template>
```

```js
// 子组件声明
const childcomponent = {
    //子组件模板声明
    template: "#cpn",
    props: {
        //父传子属性验证
        list: {
            type: Array,
            default: [],
            required: true,
        },
    },
    data() {
        return {
            msg: "Hello VUE",
            productItem: "",
        };
    },
    methods: {
        //子组件触发事件，自定义传值给父组件
        sendItem() {
            const item = this.productItem.trim();

            if (item) {
                console.log(item);
                this.$emit("add-item", item);
                this.productItem = "";
            }
        },
    },
};

//父组件
const app = new Vue({
    el: "#app",
    data() {
        return {
            newPro: ["衣服", "鞋子", "帽子"],
        };
    },
    methods: {
        //父元素绑定子元素自定义事件，触发获取传递参数进行操作
        addItem(item) {
            this.newPro.push(item);
        },
    },
    //注册子组件
    components: {
        childcomponent,
    },
});
```

#### 父子组件的访问方式

* 父组件访问子组件$children/$refs。
  * $children通过访问数组下标获取组件对象。
  * **$refs**通过在组件上设置ref属性，在通过this.refs.attrubite的值获取该组件。
* 子组件访问父组件$parent。
* 子组件访问根组件$root。



#### slot插槽

* **插槽的使用组件封装**：在组件封装时，模板预留slot标签（可在slot标签体中写标签默认值模板），在使用组件时，将自定义内容插入到组件标签内，使用插槽预留的位置。
* **具名插槽**：设置插槽时，给定slot标签name属性，使用插槽时将需要替换到插槽位置的模板使用slot属性声明该插槽的name属性值，替换到相应的插槽位置。

* **作用域插槽**：父组件使用slot结构，访问子组件的数据进行展示。

  * 定义插槽在slot标签定义属性时使用v-bind绑定需要的数据。
  * 父组件使用v-slot获取插槽传递的内容。支持结构语法`v-slot:default="{ user }"`。default可替换为插槽名。
  * 缩写：`#`代替`v-slot:`，以上可写为`#default="{ user }"`。




### Vue-Webpack

* 配置vue文件加载`vue-loader`

* 配置vue文件编译`vue-template-compiler`

* 在`webpack.config.js`文件中配置vue文件路径和扩展名简写

  ```js
  module.exports = {
      resolve: {
          //文件扩展名简写，扩展名解析
          extensions: ['.js', '/css', '.vue']，
          //.vue文件预编译为.js文件
   		alias: {
          	"vue$": 'vue/lib/vue.esm.js'
      	}
      }
  }
  ```

* 配置loader和plugins将js文件和模板文件压缩到生产目录下。

#### 配置文件分离

* webpack-merge，模块合并。



### attrubite和property的区别

* property是 DOM 对象中的属性，这里的 DOM 对象就是我们在 JavaScript 里常常提到的对象；
* attribute 是HTML标签上的特性，它的值只能够是字符串；



### 数组方法回顾

```
join()：拼接数组元素，返回字符串，参数接收字符串连接符。
push()和pop()：在尾部压入和取出元素，pop返回移除的元素，push返回数组长度。
shift() 和 unshift()：在头部取出和加入元素，shift返回移除的元素，unshift返回数组长度。
sort()：参数接收排序规则回调函数，返回排序完的数组。
reverse()：反转，和sort类似。
concat()：数组连接，参数接收一个数组或参数列表，返回新数组。
slice()
splice()
indexOf()和 lastIndexOf() （ES5新增）
forEach() （ES5新增）：遍历数组，无返回。
map() （ES5新增）：参数接收回调，对数组每一项操作，返回新数组。
filter() （ES5新增）：参数接收条件回调，返回新数组。
every() （ES5新增）：参数接收条件回调，返回布尔值。
some() （ES5新增）：参数接收条件回调，返回布尔值。
reduce()和 reduceRight() （ES5新增）：归并，参数接收回调（默认参数为数组初始前后项）和初始值，返回归并值。
```



### 生命周期

| 钩子            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| `beforeCreate`  | 组件实例刚刚被创建，组件属性计算之前。                       |
| `created`       | 用来在实例创建之后执行代码，组件实例创建完成，属性已绑定，DOM未生成，`$el`属性不存在。 |
| `beforeMount`   | 模板编译或挂载之前                                           |
| `mounted`       | 模板编译或挂载之后，此时并不能保证组件已在document中。       |
| `beforeUpdate`  | 组件更新之前                                                 |
| `updated`       | 组件更新之后                                                 |
| `beforeDestroy` | 组件销毁前调用                                               |
| `destroyed`     | 组件销毁后调用                                               |

#### `beforeCreate`

```
- 组件创建会执行生命周期函数`beforeCreate`，可在当前生命周期中创建一个Loading，当页面加载完成后再移除Loading。
- `beforeCreate`在当前生命周期函数中是访问不到其他生命周期函数以及data属性的。

Vue实例化后会创建一个Vue类的对象用来处理DOM元素，这个对象的生命周期可以通过`beforeCreate`钩子函数来访问。

Vue实例刚从内存中被创建出来，此时还没有初始化好`data`和`methods`属性。

在Vue实例初始化之后，数据观测`data observer`和`event/watcher`事件配置之前被调用。

`beforeCreate`实例创建前会遍历`data`对象下所有属性并将其转化为`setter/getter`，也就是为其添加一个被观察者，后续添加新属性时视图不用更新即可使用，后续添加的属性并不会放到观察者对象中，此时数据并没有和模板建立联系，因此不能操作该属性。如果要在实例挂在完成后使添加的属性触发视图的更新，可使用`$set`方法，`$set`方法会向被观察者对象中新增自定义的属性。
```



#### `created`

```
- 当created生命周期函数执行时会将data和methods身上的属性和方法添加到vm实例上
- created执行时会遍历data的属性并为属性添加setter和getter方法
- 可以在created生命周期函数中发起AJAX数据请求

在`created`阶段，对象及其事件已经完全初始化，  `created`是访问此阶段并编写代码的钩子，简单来说，此阶段是具有默认特性的对象。

Vue实例已经创建完成后被调用，在这一步Vue实例已经完成配置：数据观测（data observer）、属性和方法的运算（`computed`）、`watch/event`事件回调。然而，挂载阶段还没开始，`$el`属性目前尚不可见。

在模板渲染成HTML前调用，即通常初始化某些属性值，然后再渲染成视图。

Vue实例已经在内存中创建完成，此时`data`和`methods`已经创建完成，此时还未开始编译模板。

`created`阶段Vue实例已经被创建完毕，属性已经绑定，属性是可以操作的。但DOM还不存在，`$el`属性也还不可以操作。此时也可以使用axios请求，但页面还未被渲染出来，若请求时间过长则会出现长时间的白屏的现象，因此推荐添加Loading界面。
```



####  `beforeMount`

```
- 生命周期函数`beforeMount`可以对`data`中的数据做最后修改
- 在`beforeMount`生命周期函数中添加的属性没有`setter`和`getter`方法，若需要则需使用`$set`方法。
- `beforeMount`生命周期函数中模板和数据未进行结合

`beforeMount`钩子调用阶段会检查是否具有模板用于要在DOM中呈现的对象，若没有模板则将定义元素的外部HTML视为模板。

`beforeMount`在挂载开始之前被调用，相关的`render`函数首次被调用。`beforeMount`阶段已经完成了模板的编译但还未挂在到页面中。
```



#### `mounted`

```
- mounted挂载后数据和模板会进行结合并生成真正的DOM结构
- mounted函数中可访问到真实的DOM结构
- mounted函数中可用于插件实例化

一旦模板准备就绪，就会将数据放入模板并创建可呈现元素。使用新数据填充元素替换DOM元素。`mounted`钩子表示DOM已准备就绪并放置到页面中。

`el`被新创建的`vm.$el`替换，并挂载到实例上去之后调用该钩子。

在模板渲染成HTML后调用，通常是初始化页面完成后，再对HTML的DOM节点进行一些需要的操作。

`mounted`阶段此时已经将编译好的模板挂载到了页面指定的容器中显示。
```



#### `beforeUpdate`

```
- beforeUpdate会多次执行，当数据更新前会执行。
- beforeUpdate更新前数据还未和模板结合，可在此函数中做更新数据的最后修改。

当外部事件或用户输入时，`beforeUpdate`钩子在反映原始DOM元素的更改之前被触发，此阶段表示更改已经完成，但尚未准备好更新DOM。

数据更新时调用，发生在虚拟DOM重新渲染和打补丁之前。可以在狗子中进一步地更改状态，这不会出发附加的重渲染过程。

状态更新之前执行`beforeUpdate`钩子函数，此时`data`中的状态值是最新的，但界面上显示的数据还是旧的，因为此时还没有开始重新渲染DOM节点。
```



#### `updated`

```
- updated函数是更新的数据和模板进行组合的位置
- 可在updated函数中获取到数据更新后最新的DOM结构
- 可在updated函数中做插件的实例化，但需添加判断条件否则会非常消耗性能。

`updated`钩子表示在DOM中程序的更改，通过实际更新DOM对象并触发`updated`方法，屏幕上的变化才得以呈现。

由于数据更改导致的虚拟DOM重新渲染和打补丁，在这之后会调用该钩子。

当这个钩子被调用时，组件DOM已经更新，所以现在可以执行依赖于DOM的操作。然而大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。

`updated`函数在Vue实例更新完毕后调用，此时`data`中的状态值和界面上显示的数据都已经完成了更新，界面已经被重新渲染好了。
```



#### `beforeDestroy`

```
- beforeDestroy函数中可访问到真实的DOM结构，可在当前生命周期函数中做事件的解绑、监听移除等操作。

当Vue对象被破坏并从内存中释放之前`beforeDestroy`钩子被触发

Vue实例销毁之前调用，在这一步中Vue实例仍然完全可用。

`beforeDestroy`钩子函数在Vue实力销毁之前调用，此时Vue实力仍然完全可用。
```



#### `destroyed`

```
- destroyed函数执行时会将vm和模板之间的关联断开
- destroyed函数中无法通过`ref`访问到真实DOM结构

`destroyed`钩子被成功运行销毁对象上调用，对象停止并从内存中删除。

Vue实例销毁后调用，调用后Vue实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不会被调用。

`destroyed`钩子函数在Vue实例销毁后调用，调用后Vue实例指向会解除绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。
```



#### created 与 mounted

```
- `beforeCreated`时`el`和`data`并未初始化
- `created`阶段完成`data`数据的初始化，此时`el`还不存在。
- `beforeMount`阶段完成了`el`和`data`的初始化
- `mounted`阶段完成挂载。

`created`在模板渲染成HTML前调用，即通常初始化某些属性值，然后再渲染成视图。

`mounted`在模板渲染成HTML后调用，通常是初始化页面完成后再对HTML的DOM节点进行一些需要的操作。

通常`created`使用的次数多，而`mounted`通常是在一些插件的使用或组件的使用中进行操作。
```



#### `Vue`内置方法

| 运行顺序 | 属性方法 |
| -------- | -------- |
| 1        | props    |
| 2        | methods  |
| 3        | data     |
| 4        | computed |
| 5        | watch    |

