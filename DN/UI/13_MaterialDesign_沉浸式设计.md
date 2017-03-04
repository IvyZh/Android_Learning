![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.01
老师:Ricky


### 沉浸式设计

> 官方的沉浸式Translucent：就是让整个APP沉浸(充斥了整个屏幕)在屏幕里面，没有显示状态栏，甚至没有显示底部导航栏。

> 平时大家所讨论的沉浸式：比如QQ的顶部Toolbar和状态栏程一体的颜色。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304225819.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304230103.png)


兼容开发：

1. 5.x+ api
2. 4.4 api（低于4.4API，不可以做到）
用到一些特殊手段！----4.4(KitKat)新出的API，可以设置状态栏为透明的。

默认情况下是不会实现沉浸式的

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304232652.png)

把样式换成appcompat，把colorprimary和colorprimarydark修改下，运行：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304232824.png)

> 结论：5.0+自动实现了沉浸式效果，状态栏的颜色跟随你的主题里面的`colorPrimaryDark`属性。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304233630.png)


	5.0+自动实现了沉浸式效果，状态栏的颜色跟随你的主题里面的colorPrimaryDark属性。
	  
	1）通过设置主题达到
	<!-- Application theme. -->
	    <style name="AppTheme" parent="AppBaseTheme">
		<!-- All customizations that are NOT specific to a particular API-level can go here. -->
		<item name="android:textColor">@color/mytextcolor</item>
		<item name="colorPrimary">@color/colorPrimary_pink</item>
		<item name="colorPrimaryDark">@color/colorPrimary_pinkDark</item>
	<!--         <item name="android:windowBackground">@color/background</item> -->
	<!--         <item name="colorAccent">#906292</item> -->
	    </style>
	2）通过设置样式属性解决
		<item name="android:statusBarColor">@color/system_bottom_nav_color</item>
	3）通过代码设置
		//5.0+可以直接用API来修改状态栏的颜色。
		getWindow().setStatusBarColor(getResources().getColor(R.color.material_blue_grey_800));

values-21，navigationbarcolor

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304234215.png)

代码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304234401.png)


### 4.4版本的沉浸式实现 ###
- 4.4(KitKat)新出的API，可以设置状态栏为透明的。

方法一：

	在属性样式里面解决（不推荐使用，因为兼容不好）
	<item name="android:windowTranslucentStatus">true</item>
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304234614.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304234736.png)

方法二：

	在代码里面解决
		getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
		setContentView(R.layout.activity_main);
	出现副作用：
		APP的内容顶到最上面去了，即状态栏会遮挡一部分界面。很坑
	解决办法（有几种）：
		1）给Toolbar设置android:fitsSystemWindows="true"
		该属性的作用：设置布局时，是否考虑当前系统窗口的布局，如果为true就会调整整个系统窗口
				布局(包括状态栏的view)以适应你的布局。

		但是：又出现了一个bug,当里面有ScrollView并且ScrollView里面有Edittext的时候，就会出现软键盘一弹起就会把toolbar拉下来，很难看
		这种办法有什么价值呢？如果里面没有ScrollView就可以用。
		
		2）推荐
			灵感：发现给布局最外层容器设置android:fitsSystemWindows="true" 可以达到状态栏透明，并且露出底色---android:windowBackground颜色。
			巧妙地解决：步骤：
				1.在最外层容器设置android:fitsSystemWindows="true"
				2.直接将最外层容器(也可以修改-android:windowBackground颜色)设置成状态栏想要的颜色
				3.下面剩下的布局再包裹一层正常的背景颜色。

		3）修改Toolbar的高度
			1.不要给Toolbar设置android:fitsSystemWindows="true"
			2.
			需要知道状态栏的高度是多少？去源码里面找找
			    <!-- Height of the status bar -->
			    <dimen name="status_bar_height">24dp</dimen>
			    <!-- Height of the bottom navigation / system bar. -->
			    <dimen name="navigation_bar_height">48dp</dimen>
			    反射手机运行的类：android.R.dimen.status_bar_height.

			3.修改Toolbar的PaddingTop（因为纯粹增加toolbar的高度会遮挡toobar里面的一些内容）
				toolbar.setPadding(
					toolbar.getPaddingLeft(),
					toolbar.getPaddingTop()+getStatusBarHeight(this), 
					toolbar.getPaddingRight(),
					toolbar.getPaddingBottom());


在代码里面解决getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304235240.png)

问题：APP的内容顶到最上面去了，即状态栏会遮挡一部分界面。很坑。

解决方法一：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304235431.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304235500.png)

> 1）给Toolbar设置android:fitsSystemWindows="true"
		该属性的作用：设置布局时，是否考虑当前系统窗口的布局，如果为true就会调整整个系统窗口,布局(包括状态栏的view)以适应你的布局。


> 但是：又出现了一个bug,当里面有ScrollView并且ScrollView里面有Edittext的时候，就会出现软键盘一弹起就会把toolbar拉下来，很难看,这种办法有什么价值呢？如果里面没有ScrollView就可以用。

> 而且toolbar的位置上移到了状态栏的位置。
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305000125.png)

如何解决上面的问题呢？就是scrollview嵌套edittext的时候遇到的问题。

> 如果里面没有ScrollView就可以用。


解决方法二：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305000900.png)

效果:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305000943.png)


	2）推荐
		灵感：发现给布局最外层容器设置android:fitsSystemWindows="true" 可以达到状态栏透明，并且露出底色---android:windowBackground颜色。
		巧妙地解决：步骤：
			1.在最外层容器设置android:fitsSystemWindows="true"
			2.直接将最外层容器(也可以修改-android:windowBackground颜色)设置成状态栏(background)想要的颜色
			3.下面剩下的布局再包裹一层正常的背景颜色。


解决方案三：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305002015.png)

效果:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305002056.png)


源码找navigationbar高度：(后面修正的是stata_bar

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305002754.png)

代码-反射：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305002959.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305003223.png)

运行效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305003302.png)

修改：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305003422.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305003443.png)

解决方案四：

> 修改Toolbar的PaddingTop（因为纯粹增加toolbar的高度会遮挡toobar里面的一些内容）

	toolbar.setPadding(
		toolbar.getPaddingLeft(),
		toolbar.getPaddingTop()+getStatusBarHeight(this), 
		toolbar.getPaddingRight(),
		toolbar.getPaddingBottom());

两个一起用，才是最终的解决方案

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305003834.png)

> 第三个方案和第三个方案是要一起结合使用的！


第三方的沉浸式解决方案：SystemTint。



	作业：尝试自己封装；
	思考：如何让虚拟导航也做出沉浸式效果。
		提示：5.0+ 可以用API解决  <item name="android:navigationBarColor">@color/system_bottom_nav_color</item>

end.