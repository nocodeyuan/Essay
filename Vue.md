## `Vue`学习笔记

### `MVVM`

*  `Model View ViewModel`

* `Vue-MVVM`
  * 视图：`VIEW: DOM`
  * 模型：`MODEL: Javascript Objects`
  * 视图模型`VIEWMODEL: VUEAPPLICATION(DOM Listeners&Data Bindings)`

### `OPTIONS`

* `el`: 字符串或节点对象。

* `data`：对象或函数。

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
        	.up、.down、.left、.right
        ```

  * `v-model`： 双向数据。

  * `v-for`： 列表渲染。

    * :key绑定唯一，优化diff算法性能。

  * `v-once`：仅渲染一次。

  * `v-show`：显示隐藏。

  * `v-if`：条件渲染，比较消耗性能，建议经常操作使用`v-show`。

  * `v-html`: 用于展示节点字符串。

  * `v-text`: 代替插值语法。

  * `v-pre`：不解析插值语句。

  * `v-cloak`：用于延迟解析，绑定到根元素，在等待渲染过程中使用`css`设置元素不显示。



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
reduce()和 reduceRight() （ES5新增）：归并，参数接收回调（参数为数组前后项），返回 值。
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

