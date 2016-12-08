## 第02讲_01_LinearLayout基本使用（一）

主要内容：

1. View视图层级结构
2. 为什么需要使用布局
3. 什么是LinearLayout
4. LinearLayout的基本使用


### View视图层级结构

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161207164748.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161207164904.png)


### 为什么需要使用布局

> 使界面中视图显示的更加美观


### 什么是LinearLayout

> LinearLayout是一个视图组预习呢所有的字视图在竖直或者水平单一方向摆放。


### LinearLayout的基本使用

LinearLayout的属性：orientation(vertical、horizontal)

xmlns: 命名空间

控件宽度和高度有3种设置方式：wrap_content（包裹内容）、match_parent（填充父控件）、指定固定的值（dp）



## 第02讲_02_LinearLayout基本使用（二）

- android:layout_gravity 用在控件上（TextView、Button），表示控件（View）相对父控件的位置 right center...

- android:gravity 用在父布局（ViewGroup）上（LinearLayout...），表示ViewGroup中View的对齐方式

- android:gravity 用在子布局（View）上（控件上TextView Button...），表示控件内容与控件的对齐方式。总结：表示内容与该View控件的对齐方式


- android:padding 并不是LinearLayout的特有的，是View的所属都有的。内填充，表示里面内容距离控件的距离
- android:layout_magin 并不是LinearLayout的特有的，是View的所属都有的。控件与控件的距离。



## 第02讲_03_layout_weight属性的使用

- android:layout_weight 表示比重的意思，它可以实现通过百分比来进行布局的目的。是LinearLayout特有的。


- 当控件宽度是wrap_content的时候，权重越大 分的空间就越大
![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161207174225.png)