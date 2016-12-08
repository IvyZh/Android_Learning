## 第03讲_01_TextView、EditText的使用

主要内容：

1. 什么是TextView？
2. TextView的使用
3. 什么是EditText？
4. EditText的使用


### 什么是TextView？

> TextView主要用来显示丰富的文本信息，也可以用来显示图文并茂的混排的页面。


### TextView的使用

* TextView常用属性
	* text：设置TextView的文本信息
		* @string/hello_world
		* 直接写文字，硬编码
	* textColor：设置TextView中文本的颜色 RGB格式
	* textSize：设置TextView中文本的大小
	* textStyle：设置TextView中文本的字体样式，多个属性可以用 | 来分隔使用
		* normal
		* bold
		* italic
	* singleLine：单行显示
	* drawableTop:在文本的上方显示图片
		* @drawable/ic_launcher
	* autoLink：表示TextView中的文本添加可点击的超链接
		* none
		* web ： 点击打开浏览器
		* email ： 点击打开邮箱
		* phone ： 拨号
		* map
		* all


### 什么是EditText

> 是TextView的一个子类，允许用具输入文本的编辑框，可以是一行或者是多行。出来文本输入还可以允许各种其他操作，例如文本选择等。


### EditView的使用

* EditView的属性
	* hint
	* maxLength:限制当前文本框输入长度
	* password：设置为true表示设置为密码框
	* inputType
		* textPassword
		* textEmailAddress
		* number
	* imeOptions：设置完成键为响应的功能键
		* actionGo
		* actionSearch 查询
		* actionDone 完成
		* actionSend 发送
		* actionNext 下一个

## 第03讲_02_Button的使用

主要内容：

1. 什么是Button？
2. Button的使用


### 什么是Button？

> Button由文字或图标（文字和图标）组成的按钮用户触摸它时做出响应。

继承了TextView

### Button的使用

Button响应用户单击事件

* 第一种方式
	* 布局文件添加onClick属性


1. layout布局文件中的Button标签添加onClick属性
2. Activity中穿件对应响应事件

注意：该方法的名称必须与onClick属性值相同


* 第二种方式
	* 绑定监听事件


绑定监听事件

0. 在xml布局文件中的button标签添加android:id 标签
1. 获取Button findViewById
2. 给Button设置点击响应事件 setOnClickListener(new OnClickListener(){//...});//匿名内部类


* 第三种方式
	* 内部类形式

	class MyObClickListener implements OnClickListener{//...}

* 第四种方式
	* Activity 继承 OnClickListener，实现onClick方法



## 第03讲_03_ImageView的使用


主要内容：

1. 什么是ImageView？
2. ImageView使用


### 什么是ImageView

> ImageView主要用来显示app中的图片的控件

### ImageView使用

* ImageView属性
	* src : @drawable/img_logo 设置ImageView
	* maxWidth : 10dp 设置控件最大宽度
	* maxHeight: 10dp 设置控件最大高度
	* adjustViewBounds: true 设置为ture 表示允许设置imageView调整自己的边界保存显示图片长宽比例


案例：图片上一张 下一张

 iv.setImageResource(resId);// 设置图片资源id


## 第03讲_04_RadioButton的使用

主要内容：

1. 什么是RadioButton？
2. RadioButton的使用


### 什么是RadioButton？

> 单选按钮允许用户在一个组中选择一个选项。同一个组中的单选按钮具有互斥效果。


### RadioButton的使用

RadioGroup:放置RadioButton的容器

- oritentation ：设置RadioButton的显示方向
- setOnCheckChangeListener() : 表示radiogroup中RadioButton状态切换时触发时的监听
- getCheckedRadioButtonId() : 获取radiogroup中选中RadioButton的资源id


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161208143229.png)


## 第03讲_05_CheckBox的使用

主要内容：

1. 什么是CheckBox？
2. CheckBox的使用


### 什么是CheckBox？

> 复选框允许用户在用一个组中选择一个或者多个选项。

### CheckBox的使用

- setOnCheckedChangeListener() :当checkbox的状态改变了，就会调用。android.widget.CompoundButton 导包

CheckBox 也是可以在XML布局设置onClick属性的。

## 第03讲_06_Toast的使用

主要内容：

1. 什么是Toast？
2. Toast使用

### 什么是Toast？

> Toast对操作提供简单的反馈在一个弹出框中。它只填充所需的空间信息，当前的仍然仍热可见和互动的。

3个特点

1. 操作仍然可见
2. 自动消失
3. 不能获得用户焦点（不能放置一个Button等等


### Toast使用

1. 创建：Toast.make(Context,String,duration);
2. 设置位置：setGravity(gravvity,xOffset,yOffset);
3. 显示 show();