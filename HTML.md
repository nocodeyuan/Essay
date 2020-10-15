# HTML

### 概念：

* Hyper Text Markup Language超文本标记语言，最基础的网页开发语言
* 超文本：超文本是用超链接的方式，将各种不同空间的文字信息组织在一起的网状文本
* 标记语言：由标签构成的语言，html，xml

### 标签

#### 标签分类
##### 行级标签
特点：可以和其他元素保持在同一行，不可以自动换行，但不能设置宽高
常见的行级标签：a，span，strong，u（下划线），em(强调)，i(斜体)，sub(下标),sup(上标)

##### 块级标签
特点：不可以和其他元素保持在同一行（独占一行），可以自动换行，能设置宽高
常见的块级标签：div，p，h1-h6，ul，li，dl（定义列表，跟ul…li类似），dt（定义了定义列表中的项目），dd（定义描述项目的内容，跟dt一起搭配）

##### 行内块级标签
特点：可以和其他元素保持在在一行，还能能设置宽高
常见标签：textarea，input，img，button

##### 总结
这些标签很多，这里列举的是一部分，更多的标签需要不断练习才能记得牢。
所谓的行级标签，块级标签，其实可以根据需要，在开发中通过css样式互相转换。即通过设置displiay属性，它的属性值中，inline（元素以行内标签进行展示），block（元素以块级标签进行展示），inline-block（元素以行内块级标签进行展示）

---

#### 文件标签

1. `<!DOCTYPE html>`定义文档的类型
2. html：文档的根标签
3. head：头标签，用于指定htm文档的属性
4. body：体标签

#### 文本标签

* 标题h1-h6/段落p/换行br/水平线hr/加粗b/斜体i/字体font/居中center

#### 图片标签

   * `<img />`

#### 列表标签
   * 有序列表：`<ol> <li></li> </ol>`
   * 无序列表：`<ul> <li></li> </ul>`
   * 自定义列表：`<dl><dt>描述</dt><dd>内容1</dd><dd>内容2</dd></dl>`

#### 超链接标签
   * `<a href="xxx" target="_blank"></a>`
   * "_blank"打开新空白页面
   * "_self"本页面打开
   * 设置点击不跳转：`<a href="javascript=void(0);">`

#### 表格标签

   * `<table><tr><td></td></tr></table>`
   * table定义一个表格区域
   * tr定义行。td定义列，**th**包裹在tr内定义表第一行作为表头
   * border属性：边框宽度
   * caption:定义标题
   * td中：rowspan占两行。colspan占两列
   * *thead*表头，*tbody*表格体，*tfoot*表格脚部

#### 表单标签
概念：收集用户数据

##### form标签
用于定义表单区域的，区域代表采集用户数据的范围
     * action属性：指定提交用户数据的URL
          * method属性：指定提交方式
       * get/post
       * 区别：
         * get：请参数会再地址栏显示，参数大小有限制，不安全
         * post：参数不会在地址栏显示，会被封装在请求体中，比较安全

   ##### input标签

  		表单项（label标签的for属性对应一个表单项的id属性）
  		* **type属性**：
              
       * 默认text，文本属性，list属性指定数据列
         
         * `<datalist id="list"></datalist>`指定id属性，可供文本标签访问
       * password：密码
       * radio：单选，name属性需要是一致的，value提供单选的值，check=checked默认选择
       * checkbox：复选框，name属性需要是一致的，value提供选择的值，check=checked默认选择
       * file：上传文件
       * hidden：用于提交用户验证
       * 按钮：
         * img：图片作为按钮点击则提交表单
         * button
         * sumit：提交
           * value属性：定义提交按钮的意思
       * 取色器：color
       * date：日期
       * email：邮箱正则校验
       * number：数字
       * url：填写网址
          * range：范围取值
          
          * **name属性**：表单中的数据要想被提交，须指定name属性
          
          * **required**：必填项
          
          * **placeholder**：指定输入框的提示信息，当值变更时会就消失
          
          * **autofocus**：自动获取焦点
          
            * **form**：input可以不放在表单域中，通过form属性关联form标签的id提交数据
            
              `<form id ="frm"><form/> <input form="frm"/>`
   ##### select标签
   * name属性：定义下拉菜单的值信息
       * option标签select子元素：下拉菜单的选择项（第一个默认请选择，值为空）
       * value属性定义选项的值
       * optgroup标签包裹option标签，可以用label属性赋值

**textarea**：文本域：定义一个文本输入区

* cols：指定文本列数，也就是每行显示字数
* rows：指定文本行数
* name：指定文本的复制变量

---

#### 语义化标签

   * HTML5中为了提高程序可读性，提供的标签
* header：头标签
* nav：导航
* aside：侧边栏
* footer
* section：章节，定义文档某个区域
* article:文章，内容标签

