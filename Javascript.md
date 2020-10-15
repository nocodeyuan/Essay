## Javascript

1. *input>autocomplete*：显示输入历史，默认*on*，设置*off*关闭。

2. window.onload与DOMContentLoaded区别：

   1、当 `onload` 事件触发时，页面上所有的DOM，样式表，脚本，图片，flash都已经加载完成了。

   2、当 `DOMContentLoaded` 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash。

3. JavaScript为事件驱动，所有相关操作需定义在回调参数内部。

4. 文本节点内容可使用正则替换。

5. 模板字符串\`\`，引用变量\`${}\`。

6. `noscript`标签，内部可解析html文档标签，当浏览器不支持或关闭支持脚本语言时显示，支持则不显示。

7. **let与var的区别**：

   1. **let是块级作用域，var是函数作用域。**

   2. **let声明的变量不会在作用域中被提升（暂时性死区），var会提升，如果用var声明的变量在作用域最后赋值，则作用域内无法使用这个值，变量保存undefined。**

   3. **let在全局作用域中声明的变量不会成为window对象的属性，var则会。**

      var重复声明的变量会被提升。

      ```javascript
      if(typeof(name) === 'undefined'){
          let name;
      }
      //全局赋值，与作用域内的let声明name无关
      name = 'yuan';
      ```

   4. let与var与setTimeout与for

      ```javascript
      //i每次循环开启一个定时器，由于var变量提升，定时器执行时，循环完成，所以输出的值为5。
      for(var i = 0; i < 5; i++){
      	setTimeout(() => console.log(i),0)
      }
      
      //用let声明，每次循环完成将j的值赋值给新的变量，所以执行结果为0，1，2，3，4。
      for(let j = 0; j < 5; j++){
          setTimeout(() => console.log(j),0)
      }
      ```

### 简单数据类型

1. 6种简单数据类型

   Undefined，Null，Boolean，Number，String，Symbol。引用数据类型（object，function，array）

2. **typeof**

   判断变量类型

   返回值：undefined,boolean,string,number,object,function,symbol.

3. **instanceof**

   判断对象类型

4. **null**，空对象的引用。

   ```javascript
   //object
   typeof null
   
   //false
   null instanceof object
   
   //true
   !null
   
   //false
   null === false
   ```

5. **boolean**

   将其他类型的值在转换成boolean，用Boolean。

   ```
   let a = 1;
   //true
   Boolean(a);
   ```

   true：true，非空字符串，非零数值，任意对象

   false：false，空字符串，0，NaN，null，undefined。

6. **number**

   * 十进制与八进制与十六进制

     ```javascript
     //十进制
     let a = 8;
     //二进制以0b开头
     let d = 0b1000;
     //八进制以0开头
     let b = 010;
     //十六进制以0x开头
     let c = 0x8;
     ```

     数学运算默认转为十进制

     * Number数值转换

     * parseInt

       接受两个参数，第一个是带数值字符串，第二个是进制底数（介于2~36，不写或为0默认十进制），否则返回NaN。

       解析字符串头空格忽略，

       第一个字符是非数值、+、-则返回NaN，

       数值加字符则返回数值忽略字符，

       数值中间空格，则只返回空格前面数值。

     * parseFloat

       无第二个参数，

       只解析十进制数值，

       不解析其他进制数，

       只解析第一个小数点，遇到第二个小数点则中断。

7. **string**

   * 定义：0或多个16位Unicode字符序列。

     * 字符字面量：\n换行,\t制表,\b退格,\r回车,\f换页，表示一个字符，占一个字符长度。

   * 字符串长度，length。

   * toString方法，数字，字符串，对象，布尔值，可以调用。可以接受一个参数作为表示底数。

     ```javascript
     let a = 16;
     a.toString(16) //==> 0x10
     a.toString(8) //==> 020
     a.toString(2) //==> 0b10000
     ```

   * String()

     * 如果值有toString方法，默认调用，不传参数。
     * 值为null，undefined返回自身的字符串。

   * 模板字符串，可以换行书写。

     ```javascript
     let a = `bbb
     		aaa`;
     /*
     	bbb
     	aaa
     */
     ```

   * 模板字符串插值

     表达式插值，会调用toString()方法。

     ```javascript
     let a = 'hello';
     console.log(`${a} world`)//hello world
     //--------------------------------------
     let fn = {toString: () => 'hello'}
     console.log(`${fn} world`)//hello world
     ```

   * 标签函数

     获取插值中间的字符串作为数组参数(除去插值以外的字符串包含空格，最后一个插值最后默认加空格，所以字符串数组长度永远比插值数组大1)，

     获取模板字符串中的插值作为函数参数。

     ```javascript
     let a = 1;
     let b = 2;
     let c = `count ${a} + ${b} = ${a + b}`;
     //标签函数
     function repeat(strs, ...args) {
     	return strs[0] + args.map((e, i) => `${e}${strs[i + 1]}`).join("");
     }
     let d = repeat`count ${a} + ${b} = ${a + b}`;
     console.log(d);//count 1 + 2 = 3
     ```

   * 模板字符串可以解析原始字符串字面量转义的值，特殊符号会被转换，不想被转换可以使用String.raw。

     ```javascript
     `\u00a9` //@那种版本号
     String.raw`\u00a9` //"\u00a9"
     ```

   * 可通过下标访问字符串对应的字符。

8. **symbol**

   * 定义一个符号

     `let a = Symbol()`

     保存一个字符串

     `let a = Symbol('a')`

     获取描述

     `a.description`

     全局注册符号

     `let a =  Symbol.for('a')`

     访问全局符号key

     `Symbol.keyFor(a) //'a'`

     作为对象属性

     `let a = {}  a[Symbol('a')] = 'a'`

     对象访问符号

     `Object.getOwnPropertySymbols(a)`

     `Reflect.ownKeys(a)`

     使用场景

     ```javascript
     //用户名相同时作为对象唯一符号
     let user1 = {name: 'lisi', key: Symbol()}
     let user2 = {name: 'lisi', key: Symbol()}
     let classScore = {
         [user1.key]: {id: 1, score: 11},
         [user2.key]: {id: 2, score: 22}
     }
     ```

     ```javascript
     //保存 获取数据
     class martData {
     	static data = {};
     	static setData(name, value) {
     		this.data[name] = value;
     	}
     	static getData(name) {
     		return this.data[name];
     	}
     }
     
     let guestDate = {
     	name: "apple",
     	desc: "guest_data",
     	key: Symbol("guest"),
     };
     
     let carData = {
     	name: "apple",
     	desc: "car_Data",
     	key: Symbol("car"),
     };
     
     martData.setData(guestDate.key, guestDate);
     martData.setData(carData.key, carData);
     console.log(martData.getData(guestDate.key));
     console.log(martData.getData(carData.key));
     ```

     ```javascript
     //作为私有变量
     let site = Symbol();
     
     class FullName {
     	constructor(name) {
     		this.name = name;
     		this[site] = "nocodeyuan.com";
     	}
     
     	getData() {
     		return `${this[site]} ${this.name}`;
     	}
     }
     
     let man = new FullName("yuan");
     console.log(man.getData());
     ```

### 引用数据类型

#### object

* 引用数据类型：Object（Array，Function）

* 创建对象

  `new Object()`

* 属性

  * constructor

  * hasOwnProperty(propertyName)

  * isPrototypeof()：检查一个对象是否存在于另一个对象的原型链上。

  * propertyIsEnumerable(propertyName)，判断属性是否可迭代。

  * toLocaleString()

  * toString()

  * valueOf()

    | **对象** | **返回值**                                               |
    | :------- | :------------------------------------------------------- |
    | Array    | 返回数组对象本身。                                       |
    | Boolean  | 布尔值。                                                 |
    | Date     | 存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。 |
    | Function | 函数本身。                                               |
    | Number   | 数字值。                                                 |
    | Object   | 对象本身。这是默认情况。                                 |
    | String   | 字符串值。                                               |
    |          | Math 和 Error 对象没有 valueOf 方法。                    |

#### Date

1. 初始化：`new Date()`
2. 格式化：toDateString(),toTimeString(),toLocaleDateString(),toLocaleTimeString(),toUTCString()
3. 组件方法：getTime，getFullYear...

#### RegExp

1. 定义：`// new RegExp()`
2. 方法：exec()匹配，test()测试
3. exec：匹配字符串第一个符合正则目标的值
   * index：匹配到的索引
   * `let re = /a/g`，全局匹配，执行一次匹配一次，结束返回null。
4. string.match(正则表达式)，匹配字符串符合正则规则的字符。

### 原始值与引用值

1. 原始值为字面量，不可赋予属性。原始值声明变量对应的是一个实际值，相同的值可以通过声明变量独立使用，互不干扰。

   ````javascript
   let a = 1, b = a; b += 1; a//a 1 b 2
   let o1 = new Object(),o2 = o1;o1.name = 'lisi';o2.name === 'lisi';
   ````

2. 引用值为对象的引用，声明变量对应对象的引用，指向相同对象的引用改变对象的属性，则其他引用属性也会随之改变。

3. 函数传参（原始值或者对象）都是通过值传递，而非引用传递。

### 操作符

1. 一元操作符

   * ++/--

     自增/自减

      对于数值做加减，字符数值、布尔类型、调用Number()转换类型再作加减，对象类型获取valueOf/toString转换为字符再进行计算。

   * 位运算符

     * 位运算将64位数值转为32位二进制数，操作完成再转换为64位数值存储。
     * 补数：二进制数反转。
     * 取反数：正数取反为二进制取补数加一。

   * ~按位非，取32位二进制的补数

     ```javascript
     let a = 10; //0b1010
     ~a; //-11 -0b1011
     //1111 1111 1111 1111 1111 1111 1111 0101
     ```

   * &按位与，32位二进制数相与运算

     2 & 3

     原二进制按位相与运算，返回二进制再进行计算。

   * |按位或，32位二进制相或运算。

   * ^按位异或，32位二进制异或运算，负负或正正皆为0。

   * <<左移,>>右移，将指定位数左右移动指定位数做运算。

     ```javascript
     let a = 2;	//10
     let b = a << 5; //0b1000000 b===64
     let c = b >> 5; //0b10 c===2
     ```

   * \>>>无符号右移，所有32位右移，对负数影响大，对整数与有符号右移一样。

   * 逻辑与或非

     与或操作有中断执行情况，即满足第一个条件则不会继续执行第二个条件。

     null返回null，undefined返回undefined，NaN返回NaN，对象操作返回对象。

   * 乘除取模

   * 指数运算

     `3 ** 2 === Math.pow(3,2)`

   * 加减性运算符

     数字加字符得字符

     减操作会自动转换

   * 关系运算符

     大于小于等于不等于

     * 任一布尔值，则转换为数值比较
     * 任意字符串和数值，转换为数值。都是字符串，则逐个比较每一位的字符编码。
     * 对象取valueOf/toString比较。
     * 对象判断相等，比较两个对象的地址是否相等。

   * 全等与不全等

     全等不转换数值类型

   * 三元运算符

   * 逗号操作符

     `let a = (1,2,3,4,5); //5`

2. 逻辑非
   * ！对象，返回false。
   * ！空字符串，返回true。
   * ！0，返回true。
   * ！null，返回true。
   * ！NaN，返回true。
   * ！undefined，返回true。

### 语句

1. 条件

   if……else

2. 循环

   while

   do……while

   for

   for……in 对象元素遍历

   for……of 可迭代对象遍历

   break……continue

   ```javascript
   //标签语句
   let num = 0;
   outFor:
   for(let i = 0; i < 10; i++){
       for(let j = 0; j < 10; j++){
           if(i === 5 && j === 5){
               break outFor; //中止最外层循环
           }
       }
       num++；
   }
   ```

3. *with语句(不推荐使用)*

   用于连接对象

   ```javascript
   //原本
   let qs = location.search.substring(1);
   let hostname = location.hostname;
   let url = location.href;
   //with
   with(location){
       let qs = search.substring(1);
       let hostName = hostname;
       let url = href;
   }
   ```

4. switch

### 变量声明

1. var声明的变量会被提升到当前作用域的前端（函数作用域或全局作用域），对一个变量声明并赋值，声明的语句会被提升，赋值语句不会。
2. let块级作用域，即花括号包裹的语句块，不可重复声明。严格来说会被提升，但由于暂时性死区，所以会报错。
3. const声明的常量同样拥有块级作用域，变量不可以重新赋值，但可以给对象变量属性赋值。如果不想改变对象属性使用`const a = Object.freeze()`，会使变量的属性赋值无效。

### 作用域

* 标识符查找

  当作用域引用变量的时候，会确定变量的值，如果当前作用域无法获取变量的值，则会访问上一级作用域继续搜索，当获取到值的时候搜索结束。也就产生了局部变量与全局变量的关系，当他们相同，则优先搜索到局部变量使搜索结束。搜索发生在当前作用域或当前作用域链上，同时会搜索对象以及对象的原型链所以并不会获得全局变量的值。

### 垃圾回收

* 浏览器史上用过的垃圾标记策略。

1. 标记清理

   垃圾回收程序运行时，会去掉在上下文中的变量及其应用的变量，其他添加标记待删除。随后运行一次清理，回收内存。

2. 引用计数

   保留变量被引用的次数，当被替换引用时减1直到归零，垃圾回收程序运行时清理所有计数为零的变量内存。

   缺点是当两个对象分别以属性的方式引用对方，那么他们的计数永远为2，无法清除。

* 性能

  垃圾回收的事件调度会影响js的性能。ie6是固定分配空间来进行垃圾回收，ie7按回收空间占比进行了改进。

* 内存管理

  1. 全局作用域的对象，在数据不再必要的时候将它设置为null，解除引用。

  2. 通过es6，let，const声明块级作用域的变量，不接受window全局，在某些情况下块级作用域先于函数作用域关闭，优先被垃圾回收。

  3. 隐藏类和删除操作优化：

     * 隐藏类存在于类的声明中，当类的两个实例对象同时声明时，他们存在相同的隐藏类，垃圾回收可以方便地回收。

     1. 在声明类的时候，将需要的参数全部放到构造函数中，防止私自添加改变实例的隐藏类。
     2. 如不需要类的属性，不是将属性删除，而是将属性设置为null。

  4. 内存泄漏，通过程序改变内存占用的时间和空间。

     1. 声明全局变量。
     2. 定时器占用外部变量。
     3. 闭包占用变量。

  5. 静态分配与对象池
     * 频繁的对象创建，更新与删除会更快地占用内存从而触发垃圾回收程序。
     * 避免动态创建对象和其他对象（数组会自己动态改变自身长度弃用原数组，提前分配长度有效避免）实例化。
     * 静态分配就是使用对象池静态方法按需获取对象，使用，归还。

### Array

#### 定义数组

1. new Array([length])
2. []

#### Array.from()

* 参数1：类数组对象，可迭代的结构，有length属性或可索引的结构。
* 参数2：增强数组元素的函数。
* 参数3：指定参数二函数对象引用的this对象。

#### Array.of()

* 将一组参数转换为数组。

#### 数组索引

* 通过数组索引访问，增加及删除元素。

  ```javascript
  let arr = [];
  arr[0] = 1;	//add
  arr.length === 1; //true
  arr[arr.length] = 2; //add
  arr.length = 1; //delete
  arr[5] = 6; //add
  arr.length; //6
  ```

#### 检测数组

* 判断一个对象是不是数组

  `Array.isArray(arr)`

  `arr instanceof Array`：在多框架结构中可能被重写而导致不适用。

#### 迭代器方法

Array原型上暴露的方法，keys(),values(),entries()，返回可迭代的数据结构，可通过Array.from获取。

```js
let a = [1,2,3];
Array.from(a.keys());
Array.from(a.values());
Array.from(a.entries());
```

* keys返回键数组。
* values返回值数组。
* entries返回元素键值对数组的二维数组。

#### 填充与复制

* fill()：将参数1的值填充到数组参数二位置与参数三位置之间，左闭右开，填充不影响数组长度。
* copyWithin：
  * 一个参数，代表从0开始复制原数组插入到数组参数位置。
  * 二个参数，代表从第二个参数位置开始复制，插入到原数组第一个参数位置。
  * 三个参数，代表复制从第二个参数位置到第三个参数位置，插入到第一个参数位置。

#### 数组元素

* null和undefined在操作时会以空字符串的形式表示。

#### 转换方法

* toString：返回数组元素以逗号相连接的字符串。
* valueOf：返回数组本身。
* toLocaleString：在调用时会调用每个元素的toLocaleString方法，无特殊跟toString相同。

#### 栈方法

* 后进先出。
* **push**末尾压入**返回数组新长度**,**pop**取出返回**最后一项**。
* 改变原数组。

#### 队列

* 先进先出，shift和push方法。
* **shift取出数组第一项并返回值**。
* **unshift将元素推入数组开头，返回新长度**。

#### 排序

* **sort排序，reverse反转会改变原数组**，**返回新数组**。

* sort会调用String()转型为字符串比较。

  稳妥的比较方法时在sort方法内传入一个比较函数作为参数。

  `sort((v1,v2) => v1-v2)`正序

  `sort((v1,v2) => v2-v1)`倒序

#### 操作

* **slice：截取原数组，不改变原数组大小**。

* **splice：可以进行删除，插入，更新操作，直接操作原数组。**

  splice(开始位置索引，改变元素数量，新元素...)

#### 搜索

* **indexOf，lastIndexOf，includes**。

* **includes，返回布尔值**。

* 断言函数

  find，findIndex

  接受一个函数，参数为元素，元素索引和数组本身。

  **find返回第一个匹配的值**。

  **findIndex返回第一个匹配的值的索引**。

#### 迭代方法

* every：返回所有元素经函数的判断是否全都满足，返回布尔类型。**判断**
* some：对数组每一项都运行函数传入的函数，有一个结果为true，则返回true。**判断**
* filter：返回经函数返回true的元素数组，不改变原数组。**过滤**
* foreach：对数组每一项都运行函数传入的函数，不返回。**遍历**
* map：对数组每一项都运行函数传入的函数，返回每一项的处理结果组成的数组，不改变原数组。**遍历及操作**

#### 归并方法

* reduce：**接受一个回调函数和一个初始值作为参数**，回调函数四个参数：上一次归并值，当前项，当前项的索引，数组本身。第一次进行时，第一个参数取数组第一个元素。第二个参数取数组第二个元素。
* reduceRight：从数组最后一位向前归并。

### Map

1. 定义：new Map()
2. 设置值：set('id','1010')
3. 判断：has(key)
4. 获取：get(key)
5. 删除：map.delete(key)
6. 清空：map.clear()
7. 迭代：for...of，foreach
8. 迭代器：keys，values，entries和本身相同。

### Set

* 基本和map相同，添加元素用add方法。
* 迭代器entries返回的都是值。

### 默认迭代对象

都可以使用解构和for……of

* Array
* 定型数组
* Map
* Set

### 迭代器与生成器

### Object

1. **定义对象**，可以定义对象的属性和行为。可以通过Object.defineProperty()方法设置属性及属性的可执行操作。

   ```javascript
   let obj = {}
   Object.defineProperty(obj,'name',{
       writable: true, //默认true表示值可以改变
       value: 'lisi', //属性值
   	configurable: true //默认true表示属性可以使用delete obj.name删除。
   })
   ```

2. **访问器属性**：给属性添加get和set方法，在对象调用访问器属性时，对对象进行一些操作，不作为迭代属性。

   访问器具有configurable，enumerable属性。其get，set函数，默认值为undefined。

   ```js
   //版本对象
   let versionNum = {
       year_: 2017,
       edition: 1
   }
   //定义新的年份属性
   Object.defineProperty(versionNum, 'year', {
       get(){
           return this.year_;
       },
       set(newYear){
       	if(newYear > 2017){
               this.year_ = newYear;
               this.edition += newYear - 2017;
           }
   	}
   })
   //调用属性的set方法
   versionNum.year = 2020;
   //调用get方法
   versionNum.year
   ```

3. 同时定义多个属性：同时定义的属性writable，cofigurable，enumerable属性不定义的话都为false。

   ```js
   let book = {};
   Object.defineProperties(book, {
   	year_: {
   		writable: true,
   		enumerable: true,
   		value: 2017,
   	},
   	edition: {
   		writable: true,
   		enumerable: true,
   		value: 1,
   	},
   	year: {
   		get() {
   			return this.year_;
   		},
   		set(newValue) {
   			if (newValue > 2017) {
   				this.year_ = newValue;
   				this.edition += newValue - 2017;
   			}
   		},
   	},
   });
   ```

4. 读取属性特性

   `Object.getOwnPropertyDescriptor(obj,'prop')`，返回一个prop属性对象，具有value，configurable，writable，enumerable属性。访问器属性对象还有get，set函数属性。

   es2017定义了新的Object静态方法，Object.getOwnPropertyDescriptors()，会在对象的属性上调用Object.defineProperties()方法返回一个描述对象的新对象。

5. 当前对象方法及Object方法

   * **hasOwnProperty(propertyName)**：确定实例上是否存在该属性。

   * **isPrototypeof()**：检查一个对象是否存在于另一个对象的原型链上。

   * propertyIsEnumerable(propertyName)，判断属性是否可枚举。

   * toLocaleString()

   * toString()

   * valueOf()

   * Object.keys(obj)

   * Object.values(obj)

   * Object.entries(obj)

   * Object.fromEntries(Map)：把键值对列表转换成对象。

   * **Object.create(obj[,{}])**：依赖目标对象创建对象，obj即为新建对象的原型，可接受第二个参数，效果相当于Object.defineProperties()的第二个参数，给新实例添加属性和配置。

   * **Object.assign(o1,o2)**：用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

   * Object.freeze(obj)：冻结对象，一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改。`freeze()` 返回和传入的参数相同的对象。

   * **Object.getPrototypeOf(obj)**：获取obj的原型对象。

   * `Object.defineProperty()`

   * `Object.defineProperties()`：定义属性集对象。

   * `Object.getOwnPropertyDescriptor()`：传递两个参数，对象和对象的键，获取对象属性的描述。

   * `Object.getOwnPropertyDescriptors()`：获取对象的属性键值对描述。

   * `Object.getOwnPropertyNames()`：在给定对象上找到的自身属性对应的字符串数组，不包括只为Symbol的属性。

   * ```js
     Object.getOwnPropertySymbols(obj)//在给定对象自身上找到的所有 Symbol 属性的数组。
     ```

6. **合并对象**

   Object.assign()方法将接受一个或多个对象可枚举（enumerable为true）的属性和自身hasOwnProperty()返回true的属性复制到目标对象。以字符串和符号为建的属性会被复制，通过源对象get取得属性的值，通过本对象set设置到键上。

7. 对象标识及相等判定

   es6的Object.is()，`Object.is(NaN,NaN)//true`

8. 对象增强

   * 属性简写：当属性名和属性值的引用变量同名时属性值可以省略。
   * 计算属性：属性键可以通过[]引用变量或函数作为键值。

   * 方法名简写：`getName: function(){}` `getName(){}`，和计算属性兼容`[](){}`。
   * 对象解构：同名解构或解构不存在的属性时赋初始值。
     * 嵌套解构：{a:{b}} = obj。
     * 函数参数解构不影响arguments对象。

#### 对象实例化

* 传参数使用new Object()或不传参数new Object。

#### 构造函数

* constructor

#### 原型

* 构造函数，原型对象和实例是三个不同的对象。
* 实例和构造函数没有直接连接，和原型对象有直接来连接。
  * 实例对象通过`_proto_`连接到原型。
  * 构造函数通过`prototype`连接到原型。

* 同一个构造函数创建的两个实例共享一个原型对象。

* 目标对象属性访问不存在时，会沿着指针访问对象的原型获取属性。

* 目标对象设置属性会遮蔽原型对象的同属性，目标对象设置为null也会，除用delete操作实例属性才会继续访问原型。

* in操作符，判断对象或原型上是否才能在该属性。

  ```javascript
  //确定属性在原型上
  !object.hasOwnProperty(proName) && (proName in object)
  ```

* hasPrototypeProperty(obj,'name')确定name属性是否只存在obj原型上。

* for……in循环返回对象及原型所有可枚举属性，遮蔽原型不可枚举enumerable为false的实例属性也会被返回。

* Object.keys()返回实例可枚举属性，Object.getOwnPropertyNames()返回所有属性无论是否可枚举。

* Object.values()和Object.entries()返回对象属性值的数组和对象属性和值的键值对数组，非字符串属性会转化为字符串，不返回符号属性。

* 通过对象字面量的方法重写原型，原型的构造函数就不会指向Person而是Object，所以要将Person复制给Person.prototype对象并保证构造函数属性不可枚举，值指向Person。

  **创建实例须在重写原型之后进行。**

  ```js
  function Person(){}
  Person.prototype = {
      name: 'lisi',
      age: 12,
      sayName(){
          console.log(this.name)
      }
  }
  Object.defineProperty(Person.prototype,'constructor',{
      enumerable: false,
      value: Person
  })
  ```

#### 原型链

* 实例对象通过内部指针指向原型，原型的constructor属性指向构造函数，如果原型是另一个构造函数的实例，则存在内部指针指向其原型，套娃的原型链。

```js
function Father(){
	this.property =  true;
}
Father.prototype.getFlag = function(){
    return this.property;
}
function Son(){
    this.sonProperty = false;
}
//继承
Son.prototype = new Father();
Son.prototype.getSonFlag = function(){
    return this.sonProperty;
}
console.log(new Son().getFlag())
```

* Father.prototype.isPrototypeOf(new Son())，判断Father的原型是否在Son实例的原型链上。

  * 用对象字面量的重写子对象的原型会覆盖之前继承的原型，是Object的实例而不是父类构造函数的实例。

* 原型链的问题

  父构造函数属性存在引用值时，两个子实例中改变引用值会作用到另一个实例上。

* 组合继承

  通过实例化父对象的 构造赋值给新对象的原型传递方法，通过父构造.call或apply绑定新对象构造传递引用属性。（p244）

* 原型式继承

  既继承原始值属性也继承引用属性。

  ```js
  function object(o){
      function F(){}
      F.prototype = o;
      return new F();
  }
  ```

  es5规范`Object.create(o,{})`

* **寄生式组合继承：**使用组合继承会调用两次父类的构造，因此使用**寄生式组合继承**。将父类构造的引用副本引入子类构造，通过增强将子类原型的构造指向子类构造，减少父类构造的引用也同时避免子类实例属性直接操作父类构造的引用。（p247）

  ```js
  function inheritProperty(Father, Son) {
  	let obj = Object.create(Father.prototype);
  	//父类实例指向子类原型
  	obj.constructor = Son;
  	Son.prototype = obj;
  }
  
  function Father(name) {
  	this.name = name;
  	this.colors = ["red", "grey"];
  }
  
  function Son(name, age) {
  	Father.call(this, name);
  	this.age = age;
  }
  
  Father.prototype.sayName = function () {
  	console.log(this.name);
  };
  Son.prototype.sayAge = function () {
  	console.log(this.age);
  };
  
  inheritProperty(Father, Son);
  
  new Son("lisi").sayName();//"lisi"
  ```

### 类

#### 类定义

* class Person{}
* const Person = class{}
* 类的声明无法提升，类是块级作用域。
* 类的构成
  * 构造函数
  * 实例方法
  * 获取与设置函数
  * 静态函数

#### 类构造

* 实例化过程：
  * 在内存中创建新对象。
  * 新对象内部的[[Prototype]]指针被赋值为构造函数的prototype属性。
  * 构造函数内部的this被赋值为这个新对象。
  * 执行构造函数内部的代码（给新对象添加属性）。
  * 如果构造函数返回非空对象，则返回该对象（构造函数的原型不作为新对象的原型）；否则返回新创建的对象。

```js
class Person{
    constructor(flag){
        this.foo = 'foo';
        if(flag){
            return {
                bar: 'bar';
            }
        }
    }
}
let p1 = new Person(true);
p1 instanceof Person;// false,返回的不是构造函数的this对象。
```

* 类构造函数与普通构造函数的区别：
  * 普通构造函数实例化时不使用new操作符，this指向全局对象即（window）。类构造函数实例化必须使用new操作符。
* 类存在prototype属性，`Person === Person.prototype.constructor;//true`
* `typeof Person //function`
* p1 instanceof Person，使用instanceof操作符确认p1是不是Person构造的实例。
* 类中定义的constructor不会被当成构造函数，`p1 instanceof Person.constructor;//false`
* 与立即执行函数类似，类也可以在定义之后立即实例化。
* 类也可以像其他对象一样作为参数传递。

#### 实例，原型与类成员

* 实例成员：每个类的实例对象都对应着唯一的成员对象，这意味着所有成员都不会在原型上共享。

* 原型方法：在类块中定义的所有方法都会定义在类的原型上。

* 访问器：类定义支持获取和设置访问器。

* 静态方法：每个类只能有一个静态成员，this引用类自身。

  ```js
  class Person{
      constructor(){
          //存在与不同实例上
          this.locate = () => {
              console.log('instance',this);
          }
          //定义在类的原型对象上
          locate(){
              console.log('prototype',this);
          }
          //静态成员定义在类本身
          static locate(){
              console.log('class',this);
          }
      }
  }
  ```

* 非函数原型和类成员：可在类块外部定义类的引用，可在类原型添加类的引用。

* 类块支持定义生成器和迭代器。

  ```js
  class Person{
      constructor(){
          this.colors = ['red','blue','green'];
      }
      *[Symbol.iterator](){
          yield *this.colors.entries();
      }
  }
  
  //直接返回迭代器实例
  class Person{
      constructor(){
          this.colors = ['red','blue','green'];
      }
      [Symbol.iterator](){
          return this.colors.values();
      }
  }
  ```

#### 继承

* extends

#### 代理与反射

* 代理：Proxy，通过反射api实现对象的增强。

* 反射：Reflex，反射api可以设置代理或直接使用。
  * get()
  * set()
  * has()
  * defineProperty()
  * deleteProperty()
  * getOwnPropertyDescriptor()
  * ownKeys()
  * getPrototypeOf()
  * setPrototypeOf()
  * isExtensible()
  * preventExtensible()
  * apply()
  * construct()
* 代理模式
  * 跟踪属性访问
  * 隐藏属性
  * 属性验证
  * 函数与构造函数参数验证
  * 数据绑定与可观察对象

### 函数

#### 函数声明

* function声明
* 变量接受匿名函数
* 变量接受箭头函数

#### caller和callee

* caller，func.caller返回调用该func函数的函数。

* callee，arguments.callee返回参数所定义的函数本身。

  ```js
  //递归,严格模式下无法使用
  function factorial(num){
      if(num <= 1){
          return 1;
      }else{
          //使用arguments.callee返回factorial本身
          return num * arguments.callee(num - 1);
      }
  }
  
  //严格改进，使用命名函数表达式
  const factorial = (function f(num){
      if(num <= 1){
          return 1;
      }else{
          return num * f(num - 1);
      }
  })
  ```

#### this

* 谁调用就指向谁。

#### new.target

* 构造函数通过new关键词调用返回本身，不使用new返回undefined。

#### 函数的属性和方法

* length，返回函数参数列表的长度。
* call和apply方法
  * call和apply会绑定传入对象的this指向，返回该函数指向该对象的结果。`func.call/apply(obj,...)`
  * bind方法，会创建返回一个新的函数实例，其this值会被绑定到传给bind的对象。
  * 函数.apply(this,[arg1,arg2])
  * 函数.call(this,arg1,arg2)

#### 尾调用函数

* 函数返回函数返回结果。

* 满足条件可用其优化

  1. 代码在严格模式下执行。
  2. 外部函数的返回值是对尾调函数的调用。
  3. 尾调用函数返回后不需要 执行额外的逻辑，即尾调函数返回主函数也立即返回。
  4. 尾调函数不是引用外部函数作用域中自由变量的闭包。

  ```js
  function outerFunc(a,b){
      return function innerFunc(a,b){return a+b}
  }
  ```

  ```js
  //0,1,2,3,5,8,13,21
  //完美尾调优化递归斐波那契数列
  
  function fb(num) {
  	return fbFunc(0, 1, num);
  }
  
  function fbFunc(a, b, n) {
  	if (n === 0) {
  		return a;
  	} else {
  		return fbFunc(b, a + b, n - 1);
  	}
  }
  ```

#### this

* 在全局函数中调用，指向window，严格模式为undefined。
* 作为对象方法调用，指向这个对象。
* 匿名函数不会绑定对象，所以指向window。

#### 闭包内存泄漏

* 将外部函数作用域被内部函数引用的变量赋值给另一个变量，当内部函数完成后，释放该变量内存。

#### 立即执行函数

//

#### 模块私有与模块增强

* **私有/模块**：函数定义私有变量和方法，返回一个含有可访问私有对象的属性的对象。
* **增强**：函数模块中定义私有内容并实例化其他模块的实例，返回带有特定属性的对象。

### BOM

#### window对象

* 全局作用域对象，在全局定义的引用时以下对象的属性。

  * ECMAScript中的Global对象。
  * 浏览器的window对象。

* BOM（brower object model）

  * window.open(url,target,features)，导航到指定URL，例如：`window.open('https://www.baidu.com','_blank','fullscreen=yes')`
  * 第三个参数设置浏览器特性（工具栏，地址栏，状态栏），不设置即默认。

* 定时器

  //

* **系统对话框属性**

  * alert，警告，带默认确定按钮，无返回。
  * comfirm，确认，带确认及取消按钮，返回布尔值。
  * promet，对话框，带文本输入框及一个确认按钮，返回输入的值。

#### location对象

地址栏对象

* 既是window的属性，又是document的属性。

* location.hash，URL散列值（#号后面跟零或多个字符），如果没有返回空字符串。

* location.host，服务器名及端口名。

* location.hostname，服务器名（域名）

* location.href，完整URL

* location.pathname，URL中的路径或文件名

* location.port，端口

* location.protocol，页面使用的协议，一般为http或https

* location.search，URL的查询字符串，以？号 开头。

* location.origin，URL的源地址，只读。

* URLSearchParams，操作location.search的类。

  ```js
  //将URL的参数整合为键值对对象，直接操作这个对象。
  let q = location.search;//?
  let url = new URLSearchParams(q);
  url.get(key);//value
  url.set(key,value);
  url.delete(key);
  ```

* location.assign(url)，立即启动导航到新的地址。

* location.replace(url)，重新加载到地址，不能返回上一级。

#### navigator

浏览器产品对象

* API
* 检测插件
* navigator.registerProtocolHandler(处理协议ftp/mailto,url,应用名称)，注册处理程序。

#### screen

客户端显示器对象

#### history

历史记录对象

* 表示用户当前窗口首次使用以来用户的导航历史记录。
* history.go()，-1后退一页，1前进一页，2前进两页，url导航到历史最近的目标页面。
* history.back()，history.forward()，go的简写。
* history.length，历史记录条目个数。
* hashchange事件，改变浏览器url不会加载新页面。
* history.pushState(state对象，新状态标题，相对url)
* popState(),processState(),replaceState().

### DOM



### 事件处理与表单操作

### 错误处理与调试

### Promise与异步

#### promise

* 解决异步加载与异步事件循环依赖

#### 宏任务与微任务

* 事件循环：同步>微任务>宏任务
* 事件占用主线程一定是事件完成再开启其他任务。

#### 状态

* pending待定状态
* fulfilled兑现，resolved解决状态
* rejected拒绝状态

#### 使用

* 创建

  new Promise(executor)，executor执行函数。

* 实例方法

  promise.then([fulfillment],[rejection])，用于promise状态注册处理函数。

  promise.catch([rejection])，用于处理reject状态。

  promise.finally([handler])

* API

  Promise.resolve([value|promise])

  Promise.reject([reason])

  Promise.all(iterable)，接收所有已解决状态的promise。

  Promise.race(iterable)，接受所最先改变状态的promise。

  Promise.allSettled(iterable)，接受所有promise。

* then方法返回一个 [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/API/Promise)。它最多需要有两个参数：Promise 的成功和失败情况的回调函数。

  ```js
  // function doubleNum(value, func) {
  // 	setTimeout(func(2 * value), 1000);
  // }
  
  // const func = (value) => {
  // 	doubleNum(value, (x) => console.log(x));
  // };
  
  // doubleNum(1, func);
  
  function doubleComp(x) {
  	return new Promise((resolve) => {
  		console.log(x);
  		setTimeout(resolve(2 * x), 1000);
  	});
  }
  doubleComp(1)
  	.then((x) => doubleComp(x))
  	.then((x) => console.log(2 * x));
  ```

#### promise队列

* 任务队列，promise的then方法返回新的promise，让前一个promise完成后再执行下一个。

  ```js
  //数组map
  function queue(arr) {
  	let promise = Promise.resolve();
  	arr.map((item) => {
  		promise = promise.then(() => {
  			return new Promise((resolve) => {
  				setTimeout(() => {
  					console.log(item);
  					resolve();
  				}, 1000);
  			});
  		});
  	});
  }
  
  //数组reduce
  function reduceLog(arr) {
  	arr.reduce((promise, n) => {
  		return promise.then(() => {
  			return new Promise((resolve) => {
  				setTimeout(() => {
  					console.log(n);
  					resolve();
  				}, 1000);
  			});
  		});
  	}, Promise.resolve());
  }
  
  let arr = [1, 2, 3, 4, 5];
  
  reduceLog(arr);//每间隔一秒输出元素 1，2，3，4，5
  
  queue(arr);//每间隔一秒输出元素 1，2，3，4，5
  ```

#### async与await

* async与await相互依赖，async定义为函数关键字，await相当于promise的then方法。

  ```js
  function sleep(delay = 2000) {
  	return new Promise((resolve) => {
  		setTimeout(() => {
  			resolve();
  		}, delay);
  	});
  }
  
  async function show(arr) {
  	for (const v of arr) {
  		await sleep();
  		console.log(v);
  	}
  }
  
  show(arr);
  ```

* 并行执行

  ```js
  let p1 = new Promise((resolve) => {
  	setTimeout(() => {
  		console.log("p1");
  	}, 1000);
  });
  
  let p2 = new Promise((resolve) => {
  	setTimeout(() => {
  		console.log("p2");
  	}, 1000);
  });
  
  async function progress(arr) {
  	return await Promise.all([arr]);
  }
  
  progress([p1, p2]);
  ```

### JSON与客户端存储

 ### XMLHttpRequest

* new XMLHttpRequest() 

* open方法，接收三个参数，准备发送请求。

  * 请求类型
  * 请求url
  * 是否异步，布尔类型

* send方法，发送请求。接收一个参数作为请求体内容。

  * 返回值
    * responseText，响应体。
    * responseXML，如果响应类型为xml类型，返回包含数据的xml文档。
    * status，响应http的状态。
    * statusText，响应http的状态描述。

* readyState

  * 0，未初始化Uninitialized，尚未调用open方法。
  * 1，已打开Open，已调用open方法，未调用send方法。
  * 2，已发送Sent，已调用send方法，尚未收到响应。
  * 3，接收中Receiving，已经收到部分响应。
  * 4，完成Complete，已经收到所有响应，可以使用了。

  ```js
  let xhr = new XMLHttpRequest();
  //每次readyState的值变化时，调用onreadystatechange事件。
  xhr.onreadystatechange = function(){
      if(xhr.readyState == 4){
          if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
              alert(xhr.reponseText)
          }else{
              alert(xhr.status)
          }
      }
  }
  
  xhr.open('get',url,true);
  xhr.send(null);
  //取消异步，xhr对象会停止触发事件，并阻止访问这个对象上任何与响应相关的属性。
  xhr.abort();
  ```

* **setRequestHeader**，设置请求头信息，setRequestHeader('MyHeader','MyValue')

  请求头：

  ```http
  GET /home.html HTTP/1.1
  Host: developer.mozilla.org
  User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
  Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
  Accept-Language: en-US,en;q=0.5
  Accept-Encoding: gzip, deflate, br
  Referer: https://developer.mozilla.org/testpage.html
  Connection: keep-alive
  Upgrade-Insecure-Requests: 1
  If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT
  If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a"
  Cache-Control: max-age=0
  ```

  * Accept，浏览器可以处理的内容类型。
  * Accept-Charset，浏览器可以显示的字符集。
  * Accept-Encoding，浏览器可以处理的压缩编码类型。
  * Accept-Language，浏览器使用的语言。
  * Connection，浏览器与服务器的连接类型。
  * Cookie，页面中设置的cookie。
  * Host，发送请求的页面所在的域。
  * Referer，发送请求的页面URI。
  * User-Agent，浏览器用户代理字符串。

* http状态码

  | 1**  | 信息，服务器收到请求，需要请求者继续执行操作   |
  | ---- | ---------------------------------------------- |
  | 2**  | 成功，操作被成功接收并处理                     |
  | 3**  | 重定向，需要进一步的操作以完成请求             |
  | 4**  | 客户端错误，请求包含语法错误或无法完成请求     |
  | 5**  | 服务器错误，服务器在处理请求的过程中发生了错误 |

  | 状态码 | 状态码英文名称                  | 中文描述                                                     |
  | :----- | :------------------------------ | ------------------------------------------------------------ |
  | 100    | Continue                        | 继续。[客户端](http://www.dreamdu.com/webbuild/client_vs_server/)应继续其请求 |
  | 101    | Switching Protocols             | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议 |
  |        |                                 |                                                              |
  | 200    | OK                              | 请求成功。一般用于GET与POST请求                              |
  | 201    | Created                         | 已创建。成功请求并创建了新的资源                             |
  | 202    | Accepted                        | 已接受。已经接受请求，但未处理完成                           |
  | 203    | Non-Authoritative Information   | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本 |
  | 204    | No Content                      | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档 |
  | 205    | Reset Content                   | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域 |
  | 206    | Partial Content                 | 部分内容。服务器成功处理了部分GET请求                        |
  |        |                                 |                                                              |
  | 300    | Multiple Choices                | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择 |
  | 301    | Moved Permanently               | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
  | 302    | Found                           | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
  | 303    | See Other                       | 查看其它地址。与301类似。使用GET和POST请求查看               |
  | 304    | Not Modified                    | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源 |
  | 305    | Use Proxy                       | 使用代理。所请求的资源必须通过代理访问                       |
  | 306    | Unused                          | 已经被废弃的HTTP状态码                                       |
  | 307    | Temporary Redirect              | 临时重定向。与302类似。使用GET请求重定向                     |
  |        |                                 |                                                              |
  | 400    | Bad Request                     | 客户端请求的语法错误，服务器无法理解                         |
  | 401    | Unauthorized                    | 请求要求用户的身份认证                                       |
  | 402    | Payment Required                | 保留，将来使用                                               |
  | 403    | Forbidden                       | 服务器理解请求客户端的请求，但是拒绝执行此请求               |
  | 404    | Not Found                       | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面 |
  | 405    | Method Not Allowed              | 客户端请求中的方法被禁止                                     |
  | 406    | Not Acceptable                  | 服务器无法根据客户端请求的内容特性完成请求                   |
  | 407    | Proxy Authentication Required   | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权 |
  | 408    | Request Time-out                | 服务器等待客户端发送的请求时间过长，超时                     |
  | 409    | Conflict                        | 服务器完成客户端的 PUT 请求时可能返回此代码，服务器处理请求时发生了冲突 |
  | 410    | Gone                            | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置 |
  | 411    | Length Required                 | 服务器无法处理客户端发送的不带Content-Length的请求信息       |
  | 412    | Precondition Failed             | 客户端请求信息的先决条件错误                                 |
  | 413    | Request Entity Too Large        | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息 |
  | 414    | Request-URI Too Large           | 请求的URI过长（URI通常为网址），服务器无法处理               |
  | 415    | Unsupported Media Type          | 服务器无法处理请求附带的媒体格式                             |
  | 416    | Requested range not satisfiable | 客户端请求的范围无效                                         |
  | 417    | Expectation Failed              | 服务器无法满足Expect的请求头信息                             |
  |        |                                 |                                                              |
  | 500    | Internal Server Error           | 服务器内部错误，无法完成请求                                 |
  | 501    | Not Implemented                 | 服务器不支持请求的功能，无法完成请求                         |
  | 502    | Bad Gateway                     | 作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应 |
  | 503    | Service Unavailable             | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中 |
  | 504    | Gateway Time-out                | 充当网关或代理的服务器，未及时从远端服务器获取请求           |
  | 505    | HTTP Version not supported      | 服务器不支持请求的HTTP协议的版本，无法完成处理               |

* 请求类型

  | 序号 | 方法    | 描述                                                         |
  | :--- | :------ | :----------------------------------------------------------- |
  | 1    | GET     | 请求指定的页面信息，并返回实体主体。请求资源。               |
  | 2    | HEAD    | 类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头 |
  | 3    | POST    | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。提交数据。 |
  | 4    | PUT     | 从客户端向服务器传送的数据取代指定的文档的内容。             |
  | 5    | DELETE  | 请求服务器删除指定的页面。                                   |
  | 6    | CONNECT | HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。    |
  | 7    | OPTIONS | 允许客户端查看服务器的性能。                                 |
  | 8    | TRACE   | 回显服务器收到的请求，主要用于测试或诊断。                   |
  | 9    | PATCH   | 是对 PUT 方法的补充，用来对已知资源进行局部更新 。           |

* getResponeseHeader(key)，获取指定响应头信息。

* getAllResponseHeaders()，获取响应头所有信息。

* get请求

  get请求查询字符串的键值都需要使用encodeURIComponent()编码，所有键值对使用&连接。

  ```js
  //拼接请求url函数
  function addURLParam(url,name,value){
      //如果路径中不含参，则以？号拼接，否则用&号拼接
      url += (url.indexOf('?') == -1 ? '?' : '&');
      //添加转码后的键值
      url += `${encodeURIComponent(name)}=${encodeURIComponent(value)}`;
      return url;
  }
  let url = '/registerAccount';
  url = addURIParam(url,'id',1);//url '/registerAccont?id=1'
  url = addURIParam(url,'name','_this');//url '/registerAccont?id=1&name=_this'
  ```

* post请求

  post请求用于向服务器发送需要保存的数据。

  * serialize方法，将form表单中的数据转化为字符串。
  * 需要设置请求头的Content-Type为`application/x-www-formurlencoded`

  ```js
  function submitData(){
      let xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function(){
          if(xhr.readyState == 4){
              if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                  alert(xhr.responseText);
              }else{
                   alert(xhr.status);
              }
          }
      }
      xhr.open('post',url,true);
      //设置Content-Type
      xhr.setRequsetHeader('Content-Type','application/x-www-formurlencoded');
      let form = document.getElementById('user-info');
      //发送数据
      xhr.send(serialize(form));
  }
  ```

* 使用FormData，对表单数据序列化。

  不需要设置任何请求头部信息。

  `xhr.send(new FormData(form))`

* 超时timeout属性，ie8后所有浏览器给XHR对象添加timeout属性，表示发送请求后等待多时毫秒，如果请求不成功就中断请求。

* ontimeout事件，在超时时间后仍未收到响应时调用。

  ```js
  let xhr = new XMLHttpRequest();
  xhr.onreadystatechange = function(){
      try{
          if(xhr.readyState == 4){
              if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                  alert(xhr.responseText);
              }else{
                  alert(xhr.status);
              }
      	}
      }catch(e){
          
      }
  }
  xhr.open('get',url,true);
  //设置超时时间
  xhr.timeout = 1000;
  //超时后调用ontimeout函数，并设置xhr对象的readyState为4，仍然会触发执行onreadystatechange方法，由于是中断响应所以xhr.status不存在。
  xhr.ontimeout = function(){
      alert('Request did not return in a second...');
  }
  xhr.send(null);
  ```

* **进度事件**

  * loadstart，在接受到响应的第一个字符时触发。
  * progress，在接收响应期间反复触发。
  * error，在请求出错时触发。
  * abort，在调用abort()终止连接时触发会终止所有与响应相关的事件触发。
  * load，在成功接收完响应时触发。
  * loadend，在通信完成时，且在error，abort或load之后触发。

  每次请求都会首先触发loadstart，之后时一个或多个progress事件，之后是error，abort或load中的一个，最后以loadend结束。

  * 进度事件接收一个event对象，他的target属性为XHR对象。

  * **onload事件**代替onreadystatechange事件，直接在完成响应时触发。只要从服务器收到响应，无论什么状态码都会触发load事件。

  * **onprogress事件**接收一个event对象，target属性为XHR对象，额外三个属性：

    * lengthComputable，布尔值，表示进度信息是否可用。
    * position，接收到的字节数。
    * totalSize，**响应**的Content-Length头部定义的总字节数。

    ```js
    let xhr = new XMLHttpRequest();
    //onload事件完成响应执行
    xhr.onload = function(){
        if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            alert(xhr.responseText);
        }else{
            alert(xhr.status);
        }
    }
    //在响应期间反复执行，制作响应进度百分比
    xhr.onprogress = function(event){
        let progressStatus = document.getElementById(id);
        if(event.lengthComputable){
            progressStatus.innerHTML = event.position/event.totalSize*100 + '%';
        }
    }
    xhr.open('get',url,true);
    xhr.send(null);
    ```

#### 原生封装axios

```js
(function (window) {
	//参数为配置对象,默认get请求,queryParams和data都为空对象
	function axios({ url, method = "GET", params = {}, data = {} }) {
		//返回一个Promise
		return new Promise((resolve, reject) => {
			//处理method的大小写
			method = method.toUpperCase();

			//处理params, 拼接成queryString
			if (params) {
				let queryString = "";
				Object.keys(params).forEach((key) => {
					queryString += `${key}=${params[key]}&`;
				});
				//去掉最后一个&
				queryString = queryString.substring(0, queryString.length - 1);
				//把queryString拼到url上
				url += "?" + queryString;
			}

			//创建xhr对象
			const request = new XMLHttpRequest();
			//打开连接(还没有请求)
			request.open(method, url);
			//发送请求
			if (method === "GET" || method === "DELETE") {
				request.send();
			} else if (method === "POST" || method === "PUT") {
				//设置请求头类型
				request.setRequestHeader(
					"ContentType",
					"application/json;charset=utf-8"
				);
				//将data从js对象转成json string
				request.send(JSON.stringify(data));
			}

			//绑定状态改变监听
			request.onreadystatechange = () => {
				//请求没有完成
				if (request.readyState !== 4) return;
				//只有status在[200,300)之间才代表成功
				const { status, statusText } = request;
				//axios的源码中也是这样的简单粗暴
				if ((status >= 200) & (status < 300)) {
					//response对象
					const response = {
						data: JSON.parse(request.response),
						status,
						statusText,
					};
					//resolve promise
					resolve(response);
				} else {
					//其他状态都表示失败, reject promise, 给予一个友好的提示
					reject(new Error("request failed! response code = " + status));
				}
			};
		});
	}

	window.axios = axios;
})(window);

```

### Fetch

#### fetch方法

* 全局作用域方法，返回promise，fetch(url,option)，参数url，option配置对象。

#### 基本用法

* 在then方法中使用response对象。

##### 分派请求

##### 读取响应

* 读取资源完整内容。

  ```js
  fetch(url).then(response=>response.text()).then(data=>console.log(data))
  ```

##### 处理状态码和请求失败

* response的ok属性，测试在状态码为非200~299时响应的状态。

  ```js
  fetch(url).then(
      			response=>{console.log(response.status,response.ok)},
                  error=>console.log(error)
                 );
  ```

##### 自定义选项

* 参数二，初始化请求配置。
* body，请求体。
* cache，缓存设置。
* headers，请求头信息。
* method，请求方法。
* redirect，重定向设置。

#### 请求模式

* 发送json数据
* 在请求体中设置发送参数
* 发送文件
* 加载Blob文件
* 发送跨源请求
* 中断请求

### 模块化





