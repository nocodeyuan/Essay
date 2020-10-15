# CSS

### **概念**

* Cascading Style Sheets 层叠样式表
  * 层叠：多个样式可以作用在同一个html的元素上，同时生效
* 优点：
  * 将内容展示与样式控制分离（低耦合，便于分工）

---

### CSS的使用

* 内联：在标签内指定，作用于标签中
* 内部：在head标签中用style标签包裹，作用于当前页面，也可以用`@import xx.css`来导入外部样式
* 外部：独立于html文件的css文件，使用在html中引用css文件的形式，可作用于任何HTML文件，也可以导入`@import xx.css`

---

### **语法**

* `@charset  "UTF-8";`执行编码格式

* 格式：

  选择器{

  ​		属性1：属性值；

  ​		属性2：属性值

  }

* 选择器：
  * 基本选择器
    * id选择器（建议使用唯一值），优先级最高
    * 类选择器，优先级高于元素选择器
    * 元素选择器
  * 强制优先级
    * 在元素的属性值内加上`！important`,将强制使用当前值，不受优先级影响
    * 权重叠加：标签(1)<类(10)<id(100)<行内样式(1000)<!important(10000)
  * 扩展选择器
    * *{ }：选择所有元素	
    * 并集选择器,`选择器1,选择器2{}`：表示选择1和选择2
    * 后代选择器：`选择1 选择2{}`：表示选择1下的选择2
    * 子元素（亲儿子）选择器：`选择1 > 选择2{}`：表示选择2的父选择器1
    * 属性选择器：`元素[属性="值"]{}`：表示选择元素属性为值的元素
    * 伪类选择器：选择一些元素具有的状态
      * 比如a标签的不同状态的选择
      * a:link
      * a:hover
      * a:active
      * a:visited

---

### 属性

#### 字体，文本

* font-size：字体大小
* color：文本颜色
* text-align：对齐方式
* line-height：行高
* font："[font-style font-weight] font-size/line-height font-family"
  * font-style文字样式，正常，粗体，斜体
  * font-weight 400，700
  * font-family *Micorsoft Yahei*
* ***text-align***：*left/center/right*  让盒子里的文字对齐
* ***text-decoration***：规定添加到文本的修饰，可以给文本添加下划线（*underline*），上划线（*overline*），删除线（*line-through*），消除文本装饰（*none*）

* ***text-indent***：规定段落的首行缩进，*em*相对当前字符大小的倍数
* ***text-height***：规定文字的行间距
* ***line-height***：规定行高，文本默认行内垂直居中，设置行高等于盒子高度，则文本垂直居中

#### 边框

* border：表示上下左右四个边框
* border：border width | border style | border color
* 边框影响盒子大小：盒子宽高默认不算边框

#### 尺寸（块级元素）

* height：高度
* width：宽度

#### 背景（background）

* background-image:url()：文件路径

* background-repeat:no-repeat：图片不重复显示

* background-position:x y,(left,right,top,buttom,center)：可以使用精确数值

* background-attachment:scroll | fixed :背景默认随内容滚动 

* 复合写法：透明transparent，重复repeat，路径url（），滚动效果attachment，定位position

  `background:transparent url(image.jpg) no-repeat fixed top center`

* 背景色半透明：设置`background:rgba(0,0,0,0.3)`

  red,green,blue,alpha透明度

* 背景渐变：*background:-webkit-linear-gradient(left,red,blue)*

  背景从左边红色向右渐变为蓝色

### 表格

#### 元素

* thead | tr | th
* tbody | tr | td
* tfoot | tr | td

#### 边框

* 细线边框 ：*border-collapse:collapse* 合并相邻的边框

### 列表

* list-style：none

---

### 盒子模型

1. 概念

   将元素看作盒子

2. 控制布局

   * 外边距（表示与其父元素的边距）margin
   * 内边距（表示与其子元素的边距）padding
   * 边框（表示当前元素的边框）border
     * `border-collapse：collapse`：边框塌陷，实现细线表格
   * 边框和内边距会改变盒子大小，如果盒子没有指定宽高，则不会撑开
   * 块级元素水平居中：
     * 必须设置宽度
     * 设置左右外边距为：*auto*
   * 行内元素/行内块元素水平居中：在父元素中设置*text-align：center*
   
3. box-sizing属性：

   * `content-box`：在盒子外部绘制元素的内边距和边框
   * `border-box`：在盒子内部绘制元素的内边距和边框
   * `inhert`：继承父元素的box-sizing属性值

---

### 浮动

1. 行内元素
   1. 左右排列，不可设置宽高，默认宽度为本身内容的宽度，只能容纳文本或其他行内元素
   2. *a,strong,b,em,i,del,s,ins,u,span*
   
2. 块级元素
   1. 上下排列，可设置宽高，默认宽度为父容器100%，高度为0
   2. *h1~h6,p,div,ul,ol,li，form*
   
3. 行内块元素
   1. 行内显示，中间有空格，默认宽度为内容宽度，宽高边距可以设置
   2. *img，input，td*
   
4. `float`
   1. `float:left`:将块级元素浮动到左边，形成行内元素的排列方式，优先级高于存在行内元素

   2. `clear:float`：受其他块元素浮动影响的元素使用可摆脱，因为元素使用清除会无法使用margin属性，所以一般使用空块元素清除浮动影响`clear:both`。

   3. 浮动元素具有行内块元素的特点

   4. 在标准流的父元素中声明盒子宽度然后浮动“不脱离文档”。

   5. 一般父元素不设置高以容纳不确定数量的子元素，而子盒子需要浮动，则父盒子高度因子元素浮动而归0

      * **清除浮动**

        * 额外标签法，在子元素末尾添加块级元素标签设置*clear：both* 属性

        * 父级元素添加*overflow*

        * 伪元素法

          ```css
          .father:after{
              content:'';
              display:block;
              height:0;
              clear:both;
              visibility:hidden;
          }
          
          .father{ /* IE6、7专用 */
              *zoom:1;
          }
          ```

        * 双伪元素法

           ```css
           .father:before,.father:after{
               content:"";
               display:table;
           }
           .father:after{
               clear:both;
           }
           .father{
               *zoom:1;
           }
           ```

5. display

   1. 行内元素转换成块级元素：`display:block`
   2. 行内元素既左右排列，又可设置宽高：`display:inline-block`

6. overflow
   1. 内容超出元素部分的处理方式
   2. `overflow:hidden`：隐藏超出部分
   3. `overflow:auto`：自动展示超出部分，会出现垂直滚动条

7. position（定位）
   1. static：静态，默认定位
   2. absolute:绝对定位，相对于页面左上角的定位，属性z-index：表示图层顺序，值越大显示的位置越靠前
   3. relative:相对定位，以自身原位置为原点的定位
   4. fixed:固定定位，固定位置，不随用户滚动而改变位置

### sprities

1. 概念：前端使用优化网站图片请求的技术

2. 实现方式：

   现阶段是通过CSS属性background-image组合background-repeat, background-position等来实现（题外话：为何我提现阶段，因为未来浏览器若支持content则又新增另外的实现方法）。我们的主角是，你一定猜到了，就是background-position。通过调整background-position的数值，背景图片就能以不同的面貌出现在你眼前。其实图片整体面貌没有变，由于图片位置的改变，你看到只该看到的而已。

### Emmet 语法

1. *\**

   ```Emmet
   ul>li*8
   ```

2. *$*

3. *{}*

   ```
   ul>li{Item $}*8
   ```

   

### CSS3

#### border

* 圆角边框
  * *border-radius: 半径；*
  * *border-radius：t-left t-right b-r b-l*

### box-shadow

* 盒子阴影
* *box-shadow:h-shadow v-shadow blur spread color inset*
* h-shadow:必须，水平阴影为止，允许负值
* v-shadow：必须，垂直阴影的位置，允许负值
* blur：可选，模糊距离，虚实
* spread：可选，阴影尺寸，阴影部分尺寸
* color：可选，阴影颜色
* inset：可选，将外部阴影（outset）改为内部阴影

### text-shadow

* h-shadow
* v-shadow
* blur
* color

### flex布局

* 通过给父盒子添加flex属性，来控制子盒子的位置和排列方式
* 父盒子被称为“容器”，子盒子被称为“项目”
* 父盒子属性
  * ***flex-direction***：设置主轴方向
    * row：默认值 从左向右
    * row-reverse：从右向左
    * column：从上向下
    * column-reverse：从下向上
  * ***justify-content***：设置主轴上的子元素排列方式
    * flex-start：默认值，贴着头开始，默认从左向右
    * flex-end：贴着尾部排列
    * center：在主轴居中对齐
    * space-around：平分空间
    * space-between：两边贴边，剩余平分
  * ***flex-wrap***：设置子元素是否换行
    * no-wrap：默认值，不换行
    * wrap：换行
  * ***align-content***：设置侧轴上子元素的排列方式（多行），子项目出现换行的情况使用
    * flex-start：从上到下
    * flex-end：从下到上
    * center：挤到一起，垂直居中
    * space-between
    * space-around
    * stretch
  * ***align-items***：设置侧轴子元素的排列方式（单行）
    * flex-start：从上到下
    * flex-end：从下到上
    * center：挤到一起，垂直居中
    * stretch：拉伸，默认值，子盒子不设置高度，拉伸与父元素相同高度
  * ***flex-flow***：复合属性，相当于同时设置了flex-direction和flex-wrap
* 子盒子属性
  * flex：自适应大小
  * align-self：控制子项目自己在侧轴上的排列方式
  * order：定义项目的排列顺序，默认是0，取负值向前排列，正值向后排列
* 主轴和侧轴
  * 默认主轴方向就是x轴方向，水平向右
  * 默认侧轴放行就是y轴方向，水平向下

### PS切图

* 图层切片
* 手动切片
* cutterman

### CSS3

#### 属性选择器

* E[att]
* E[att="val"]：att等于val的元素
* E[att^="val"]：att以val值开头的元素
* E[att$="val"]：att以val值结尾的元素
* E[att*="val"]：包含属性为val的元素

#### 结构伪类选择器

* E:first-child

* E:last-child

* E:nth-child(n):选择第几个，前三个会把所有子元素排序号，需要子元素相同，才能选到
  * 可选偶数even，奇数odd
  * 2n偶数，2n+1奇数
  * 5n，5的倍数
  * n+5 ,从5开始，包含5到最后
  * -n+5，从开始到5，包含5
  
* E:first-of-type

* E:last-of-type

* E:nth-of-type(n)，指定子元素加序号

* 复合写法

  如ul下8个li：

  * 选择除第一个和最后一个元素

    *ul>li:not(:first-child):not(:last-child)*

  * 选择除了后两个元素

    *ul>li:not(:nth-last-child(-n+2))*

  * 选择中间四个元素

    *ul>li:nth-child(n+3):not(:nth-last-child(-n+2))*

