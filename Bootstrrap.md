# Bootstrap

## 响应式布局

* 同一套页面可以兼容不同分辨率的设备
* 实现：依赖于栅格系统：将一行平均分为12个格子，可以指定元素占几个格子
* 步骤：
  1. 定义容器，相当于table
     1. 容器分类
        1. container:两边有留白，不同适配留白面积不同
        2. container-fluid:每一种适配都是百分百的宽度
  2. 定义行：样式row，相当于tr
  3. **定义元素**。指定该元素在不同设备上，所占的格子数目。样式：col-设备代号-格子数目
     * 设备代号
       * xs:手机 <768px,col-xs-12
       * sm:平板>=768px,col-sm-12
       * md:桌面显示器 >=992px
       * lg:大桌面显示器>=1200px
* 注意事项：
  1. 一行如果格子超出12个，则超出部分自动换行
  2. 栅格属性向上兼容。栅格类适用于与屏幕宽度大于或等于分界点大小的设备
  3. 如果真是宽度小于设置的栅格类属性的设备代码的最小值，一个元素会占一整行

---

## CSS样式与Js插件

1. 按钮
   * class=" .btn btn-default"
2. 图片
   * class="img-responsive":图片在任意尺寸都占100%
   * 图片形状
     * class="img-rounded"：方形
     * class="img-circle"：圆形
     * class="thumbnail"：相框
3. 表格
   * class=".table"：bootstrap表格
   * .table-bordered:边框
   * .table-hover:悬停效果
4. 表单
   * .form-control
   * .form-group
5. 导航条
6. 分页条
7. 轮播图