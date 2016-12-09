## 第05讲_01_Style和Theme的使用

主要内容：

1. 什么是Style？
2. 什么是Theme？
3. Style、Theme的使用


### 什么是Style？

> 样式是一组属性指定一个视图或窗口的外观和格式。风格可以指定属性，如宽高、填充、字体大小、背景色等等。


### 什么是Theme

> Theme主要用来指定样式风格统一的页面设置一些属性的，类似无标题或者标题栏背景统一。

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161209100048.png)

### Style、Theme的使用



#### Style

样式就是属性的集合,XML目录 res/vaules/styles.xml

布局文件中引用：style="@style/button_style"

如果style和标签都定义了相同属性，那么以属性设置为主。


* 继承已有的Style
	* `<style name="button_style2" parent="button_style">`
	* `<style name="button_style.button_style2">` 只能引用自定义样式，不能引用系统样式



#### Theme

样式和主题的异同点

- 都是定义在styles.xml文件中，都是通过style标签定义
- 引用场景不同
	- style：在控件或者布局标签中使用 view
	- theme：在activity或者application中使用


> styles.xml文件中也可以定义color标签

	<style name="my_theme" parent="android:Theme.Light">
		<item name="android:backgroud">#00ffee</item>
	</style>


在activity或者application中使用

	android:theme="@style/my_theme"