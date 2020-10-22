## CSS

### 选择器

#### 属性值筛选选择器

```css
/*选择值包含字符串的元素*/
el[attr*="val"] 

/*选择值包含独立字符串单词val的元素*/
el[attr~='val']

/*选择值以val开头或者val-的元素*/
el[attr|='val']
el[attr|='val1-val2']
```

#### 伪类选择器

* 点击事件伪类选择器

  ```css
  /*link初始状态，hover鼠标关注，active鼠标点击，visited点击后，focus元素获取焦点*/
  el:link{}
  el:hover{}
  el:active{}
  el:visited{}
  el:focus{}
  ```

* 锚点触发选择器

  ```css
  /*锚点触发到该元素改变样式*/
  el:target{}
  ```

* 根元素与空元素伪类选择器

  ```css
  /*根元素*/
  :root{}
  /*空元素*/
  el:empty{}
  ```

* 子元素伪类

  ```css
  /*
   	:first-child :last-child
   	:first-of-type-of :last-of-type
   */
  
  /*el元素所有后代子元素中的首位*/
  el :first-child{}
  
  /*el元素直接子元素的首位*/
  el>first-child{}
  
  /*
       目标子元素，参数为固定值或奇数偶数,2n/2n-1/-n+2。。。表示 
       :nth-child(index){}
       :nth-of-type(index){}
  	 :nth-last-child(){}
  	 :nth-last-of-type(){}
  
  	唯一子元素伪类
  	el :only-child{}
  	el :only-of-type{}
  
  	排除元素选择器
  	el :not(){}
  */
  
  ```

* 其他元素选择器

  ```css
  /*
  	disable 不可用元素
  	enable	可用元素
  	checked	已选择元素
  	required 必填项
  	valid 邮箱网址等表单填写有效时
  	invalid 无效时
  */
  ```

* 文本伪元素

  ```css
  /*
  	::first-letter 第一个字符
  	::first-line 第一行
  */
  ```

#### 伪元素

```css
/*
	::before
	::after
*/
el::before{
    content: ''; //伪元素内容
}
```

#### 选择器权重

* ！important（9999）> 行内样式（1000）> id选择器（100）> class/属性选择器（10）> 标签/伪元素（1）> 通配符（0） > 继承（NULL） > 浏览器默认

### 文本

#### 定义字体

```css
@font-face{
    font-family: 'xxx',
    src: url('xxx.otf') format('opentype')
}
```

#### 组合写法

font: [font-weight] [font-style] font-size[/line-height] font-family;

#### 文本大小写转换

```css
/*小型大写*/
font-variant: small-caps;
/*大小写转换*/
text-transform: lowercase;
text-transform: uppercase;
/*首字母大写*/
text-transform: capitalize;
```

#### 文本线

```css
text-decoration: underline | overline | line-through | none;
```

#### 文本阴影

```css
text-shadow: 颜色 水平偏移px 垂直偏移px 模糊程度px;
```

#### 文本空白与换行

```css
white-space: pre保留空白与换行 | pre-wrap保留空白与换行 | pre-line合并保留换行 | nowrap不换行;

/*文本不换行 溢出隐藏 隐藏处理*/
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

#### 文本缩进与对齐

```css
/*文本缩进,按文字大小缩进固定单位*/
text-indent: 2em;

/*文本水平对齐方式*/
text-align: left | center | right;	

/*文本垂直对齐*/
vertical-align: top | middle | bottom;
```

#### 排版

* 文本字间距

  ```css
  /*单个字符间距*/
  letter-spacing: ?px;
  
  /*单词间距*/
  word-spacing: ?px;
  ```

* 排版方向

  ```css
  writing-mode: vertical-lr纵向从左到右 | vertical-rl纵向从右到左 | horizontal-tb横向从上到下 | horizontal-bt横向从下到上
  ```

### 盒子模型

#### 固定模型

```css
/*元素大小固定，不受边距及边框影响。*/
border-sizing： border-box;
```

#### 排列方式

```css
/*
	边距排列
	上右下左
	上下 左右
	上下 左 右
	负值溢出
*/
```

#### 边距合并

* 上下元素重叠边距会自动合并取最大值。

#### 盒子圆角

```css
border-radius: ?px;
```

#### 盒子阴影

```css
box-shadow: 水平偏移px 垂直偏移px 模糊程度px 阴影颜色rgba;
```

#### 元素轮廓线

```css
/*轮廓线显示不占用空间*/
outline: solid 1px #000;

/*取消input轮廓线*/
input{
	outline: none;
}
```

### 元素隐藏

#### display

```css
display: none; 元素消失，不保留原始空间。
```

#### visibility

```css
visibility: hidden; 元素隐藏，保留原始空间，相当于opacity: 0;设置透明度为0。
```

#### overflow

```css
overflow: scroll | hidden | auto; 溢出滚动 隐藏 自动
```

#### 尺寸控制

```css
/*控制显示最大最小尺寸*/
min-width: ?px;
max-width: ?px;
```

#### 自动填充

```css
/*自动填充*/
width | height: fill-available;
```

#### 自动获取内容尺寸

```css
/*适应块元素文本宽度*/
width: fit-content;

/*自适应最大最小文本内容的尺寸*/
width: max-content;
width: min-content;
```

### 背景

```css
/*透明背景*/
background-color: transparent;
/*背景图*/
background-img: url(),url();
/*背景重复*/
background-repeat: repeat-x | repeat-y | no-repeat | space平均显示;
/*背景固定*/
background-attachment: scroll滚动 | fixed固定;
/*背景位置*/
background-position: top | top left | center | 50% 50%;
/*背景比例*/
background-size: 100% 100% | cover显示部分 | contain完全显示空留白;
/*背景裁切*/
background-clip: content-box只内容区 | padding-box包含内边距 | border-box包含边框;

/* 
background-origin 规定了指定背景图片background-image 属性的原点位置的背景相对区域.
注意：当使用 background-attachment 为fixed时，该属性将被忽略不起作用。
*/

/*组合写法*/
background: [background-color] [background-image] [background-repeat] [background-attachment] [background-position] / [ background-size] [background-origin] [background-clip];
```

### 渐变

```css
/*背景线性渐变*/
background: linear-gradient(角度, color1, color2);

/*径向渐变*/
background: radial-gradient(at|to 原点位置, color1, color2);

/*径向渐变标志位 控制渐变的位置 范围*/
linear-gradient(90deg, color1, color2);

/*渐变颜色中间点 ?%*/
linear-gradient(90deg, color1, ?%, color2);

/*重复的渐变*/
repeating-linear-gradient(deg, color1, midVal, color2);
repeating-radial-gradient(position, color1, color2);

/*旧进度条*/
background: repeating-linear-gradient(45deg, blue, 25px, yellow 25px, 25px, red 50px);
```

### 浮动

#### 清除浮动

```css
/*浮动后元素会影响周围的元素的空间 在浮动元素后的元素可以通过设置清除浮动 还原浮动对空间的影响*/
clear:both; //清除所有浮动

/*伪元素清除浮动*/
el::after{
    content: '';
    display: block;
    clear: both;
}

/*overflow触发BFC清除浮动 父元素尺寸计算子元素浮动*/
overflow: hidden;
```

 #### 内容环绕

```css
/*控制浮动元素与内容的距离 加在浮动元素上的样式*/
shape-outside: border-box | margin-box | padding-box | content-box;

/*控制元素形状*/
clip-path: circle(弧度 at 原点坐标)圆形 | ellipse(水平弧度 垂直弧度)椭圆 | polygon(点1坐标, 点2坐标,..)绘制点连接多边形;

shape-outside: circle() | ellipse() | polygon(); //控制内容按形状环绕
shape-outside： url() //控制图片环绕，需要png类型图片
```

### 定位

#### 位置参考

* 绝对定位或相对定位参考的是离自己最近的设置定位的父元素。
* 固定定位参考的是文档根元素。

#### 粘性定位

* 设置元素位置触发时，固定元素。

```css
position: sticky;
```

* 同级粘性元素会叠加，不同级的会替代。

  

```css
{
    
/* 	声明flex*/
	display: flex | inline-flex;

/* 	主轴方向，项目的排列方向,主轴默认水平，交叉轴默认垂直*/
	flex-direction: row | row-reverse | column | column-reverse;

/* 	声明一条轴线排不下如何换行*/
	flex-wrap: nowrap | wrap | wrap-reverse;

/* 	flex-flow，是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。*/
	flex-flow: column wrap-reverse;

/* 	justify-content，定义主轴的对齐方式*/
	justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
/*
    flex-start（默认值）：左对齐
    flex-end：右对齐
    center： 居中
    space-between：两端对齐，项目之间的间隔都相等。
    space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
    space-evenly：轴上每个项目平均分布。
*/    

/* 	align-items，定义交叉轴的排列方式*/
	align-items: flex-start | flex-end | center | baseline | stretch;
/*
    flex-start：交叉轴的起点对齐。
    flex-end：交叉轴的终点对齐。
    center：交叉轴的中点对齐。
    baseline: 项目的第一行文字的基线对齐。
    stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。    
*/
    
/*	align-content，定义多行交叉轴方向的排列方式*/  
	align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    
/*	
    align-self，对单个元素交叉轴位置控制 设置stretch填充时元素未设置高度或设为auto,可覆盖align-items属性*/
	align-self: flex-start | flex-end | center | stretch;
    
/*	order属性，数值越小越靠前*/
	order: <integer>;/*默认0*/
    
/*	flex-grow，放大比例，属性，定义flex容器内元素占用剩余空间的放大比例，默认0原始大小，*/
    flex-grow: <number>;/*default 0*/
    
/*	flex-shrink，缩小比例，控制flex容器内元素的缩小比例*/
    flex-shrink: <number>; /* default 1 */
 
/*	flex-basis，定义了主轴尺寸。在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。*/    
    flex-basis: <length> | auto; /* default auto */
    /*	优先级max/min尺寸 > flex-basis基准尺寸 > width/height	*/

/*	flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。*/ 
    flex: flex-grow [flex-shrink] [flex-basis];
    
/*	flex可作用于文本*/    
/*	flex边距自动*/
    margin: auto;
}
```

### grid栅格布局

```css
{
    /*
    	绘制栅格，grid-template-rows grid-template-columns 绘制行列repeat绘制次数与绘制占比或尺寸
    */
    grid-template-rows: repeat(times, percent);
    grid-template-columns: repeat(2, 100px 20px);
    /*绘制占100和20像素尺寸的列 绘制两次*/
    
    /*	自动填充，auto-fill,自动填充内容绘制次数, 按照父元素的高度绘制20尺寸的栅格n行	*/
    grid-template-rows: repeat(auto-fill, 20px);
    
    /*	按比例填充，fr单位*/
    grid-template-rows: repeat(2，1fr);/*等比例绘制两行*/
    grid-template-columns:1fr 2fr 1fr;/*绘制三列占比1：2：1*/
    
    /* 栅格尺寸范围，minmax*/
    grid-template-rows: repeat(2，minmax(50px, 100px));/*绘制两行垂直方向上的尺寸最大100最小50*/
    
    /* 栅格间隙留白，row-gap column-gap gap，作用于容器，定义在父元素内*/
    row-gap: 5px;column-gap: 10px;/*设置行间距为5，列间距为10*/
    gap：<row-gap> <column-gap>;/*简写*/
 
   	
}
```

#### 放置元素

* grid-row-start，元素行开始栅格线位置。 
* grid-row-end，元素行结束栅格线位置。 
* grid-column-start，元素列开始栅格线位置。 
* grid-column-end，元素列结束栅格线位置。

<img src="C:\Users\yuan\AppData\Roaming\Typora\typora-user-images\image-20201022205659630.png" alt="image-20201022205659630" style="zoom:50%;" />

```html
<section>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
</section>
```

```css
section{
display: grid;
width: 60%;
margin: 100px auto;
border: 1px solid #000;
    /* 3*3布局 */
grid-template-rows: repeat(3, 1fr);
grid-template-columns: repeat(3, 1fr);
    /* 栅格间隔5像素*/
gap: 5px;
padding: 5px;
}

section div{
box-sizing: border-box;
border: 1px solid #3adf7b;
color: #fff;
font-weight: 700;
background-color: #3aef;
background-clip: content-box;
text-align: center;
line-height: 100px;
}

div:first-child{
grid-column-start: 1;
grid-column-end: 3;
}
div:nth-of-type(3){
grid-row-start: 2;
grid-row-end: 4;
}
div:nth-of-type(6){
grid-column-start: 2;
grid-column-end: 4;
} 
```

##### 固定命名放置

* 固定尺寸栅格命名，可以按照命名放置元素

```css
{	
    /* 绘制3*3栅格并为栅格线命名命名，可以使用栅格线名字放置元素 */
    dispaly: grid;
    grid-template-rows: [r1-start] 100px [r1-end r2-start] 100px [r2-end r3-start] 100px [r3-end];
    grid-template-columns: [c1-start] 100px [c1-end c2-start] 100px [c2-end c3-start] 100px [c3-end];
}
{
    /* 元素放置到2号位置 */
    grid-row-start:  r1-start;
    grid-row-end: r1-end;
    grid-column-start: r1-end | r2-start;/*同一条栅格线有两个名字都可以使用*/
    grid-column-end: r2-end | r3-start;
}
```

##### 重复命名

* repeat绘制栅格，可以按照栅格线命名加编号放置元素。

  ```css
  {
      /* 绘制3*3*/
      display: grid;
      grid-template-rows: repeat(3, [r-start] 1fr [r-end]);
      grid-template-column: repeat(3,[c-start] 1fr [c-end]);
  }
  
  {
      /* 同样放置在2号*/
      grid-row-start: r-start 1;
      grid-row-end: r-end 1;
      grid-column-start: c-start 2;
      grid-column-end: c-end 2;
  }
  ```

* 块元素水平垂直居中

  ```html
  <main>
  	<div>1</div>
  </main>
  ```

  ```css
  main{
      box-sizing: border-box;
      height: 100vh;
      display: grid;
      grid-template-columns: repeat(3, [c-s] 1fr [c-e]);
      grid-template-rows: repeat(3, [r-s] 1fr [r-e]);
      gap: 5px;
      border: 1px solid #000;
  }
  
  main>div{
      width: 300px;
      height: 300px;
      background-color: pink;
      background-clip: content-box;
      font-weight: 700;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
  }
  
  div:first-child{
      grid-row-start: r-s 2;
      grid-row-end: r-e 2;
      grid-column-start: c-s 2;
      grid-column-end: c-e 2;
      margin: 0 auto;
  }
  ```

##### 设置偏移量放置元素

* span

```css
/* 偏移设置在end上 */
{
    grid-row-start: 1;
    grid-row-end: span 2;/*偏移两行*/
    grid-column-start: 2;
    grid-column-end: span 1;/*偏移一行*/
}
```

##### 元素定位简写

* `grid-row: [row-start]/[row-end];`
* `grid-column: [column-start]/[column-end];`

* 偏移
  * `grid-row: [row-start]]/span 2;`
  * `grid-column: [column-start]]/span3;`

```css
{
    /*绘制3*3*/
    display: grid;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repear(3, 1fr);
}

{
    /*子元素占满第二行*/
    grid-row: 2/3;
    grid-column: 1/4;
}
```



**可以用栅格布局开发类似bootstrap的栅格系统**



#### 区域定位元素

* `grid-area: [row-start] [column-start] [row-end] [column-end]`，确定元素四条栅格线的位置绘制元素。同时可以为栅格线命名。

```css
/* 定位元素显示的区域，grid-area */
{
    /* 3*3 */
    display: grid;
    grid-template-rows: repeat(3,[r] 1fr);
    grid-template-columns: repear(3, [c] 1fr);
}

{
    /* 定位到中心 */
    grid-area: r 2/c 2/r 3/c 3;
}
```

#### 划分区域

* `grid-template-area: "r1-c1 r1-c2" "r2-c1 r2-c2" "r3-c1 r3-c2"`，为栅格命名，划分区域。

* `grid-area: xxx`，使用命名的区域。

* **命名按行，每行的栅格命名在一起。每行多个栅格名称相同则独占一行。**

* **上面栅格不命名区域的话可以使用 \. 占位。**

  `grid-template-area: ". ." ". . " "same same";`

  <img src="C:\Users\yuan\Desktop\Snipaste_2020-10-22_22-50-32.png" alt="Snipaste_2020-10-22_22-50-32" style="zoom:50%;" />

  ```html
  <main>
      <header>1</header>
      <nav>2</nav>
      <article>3</article>
      <footer>4</footer>
  </main>
  ```

  ```css
  main{
      height: 100vh;
      width: 100vw;
      display: grid;
      grid-template-rows: 60px 1fr 60px;
      grid-template-columns: 60px 1fr;
      grid-template-areas: "header header" "nav article" "footer footer";
      gap: 5px;
  }
  header, nav, article, footer{
      background-color:pink;
      background-clip: content-box;
  }
  
  header{
      grid-area: header;
  }
  
  nav{
      grid-area:nav;
  }
  article{
      grid-area: article;
  }
  footer{
      grid-area: footer;
  }
  ```

#### 元素流动

* `grid-auto-flow`，控制元素的流动方向，默认从左到右先行后列。
  * `row`
  * `column`
  * `dense`，当前面元素定位到后面时，后面的元素自动流动到前面。

#### 对齐方式

* 水平 垂直

##### 栅格对齐

* 当容器的空间大于栅格的空间，设置栅格的对齐方式，默认在开始位置。	

```css
{
    justify-content: start | end | center | space-between | space-evenly | space-around;
	align-content: start | end | center | stretch | space-around | space-between | space-evenly;
} 
```

* 简写，`place-content`属性是`align-content`属性和`justify-content`属性的合并简写形式。

```css
{
    place-content: <align-content> <justify-content>;
}
```

##### 内容对齐

* 当栅格内容小于栅格，设置内容的对齐方式，默认拉伸占满。

  ```css
  {
      justify-items: start | end | center | stretch;
    	align-items: start | end | center | stretch;
  }
  ```

* 简写，`place-items`

* 单个内容设置对齐

  ```css
  {
      justify-self：start | end | center | stretch;
      align-self: start | end | center | stretch;
  }
  
  /*简写*/
  {
      place-self: start | end | center | stretch;
  }
  ```

#### 意外多出

* grid-auto-rows
* grid-auto-columns

#### 其他简写

**一般不建议使用**

* `grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

* `grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。

