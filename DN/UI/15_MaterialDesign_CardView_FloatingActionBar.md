![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.06
老师:Ricky


### CardView

兼容开发，引用v7目录下面的CardView项目
CardView： android-support-v7-cardView.jar


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305025905.png)

6.0 效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305025923.png)

4.4 效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305030555.png)


1.特性
	
	1) 边框圆角效果
		5.x 图片和布局都可以很好的呈现圆角效果，图片也变圆角了
		4.x 图不能变成圆角，如果要做成5.x一样的效果：通过加载图片的时候自己去处理成圆角
	2）阴影效果

	3）5.x上有Ripple水波纹效果（低版本需要自己做自定义的）
		android:foreground="?attr/selectableItemBackground"
		android:clickable="true"
	4）5.x实现按下的互动效果---下沉，松开弹起---Z轴位移效果 （低版本也需要自己自定义做）
		
	5）可以设置内容的内边距
	 app:contentPadding="5dp"

> 同一套布局的兼容性开发：(5.x上面不需要设置app:contentPadding="5dp"，而4.x上面不需要设置)
layout
layout-v21

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305214746.png)

- 阴影效果

		5.x上面，边距阴影比较小，需要手动添加边距16dp
		4.x上面，边距太大， 手动修改边距0dp（原因：兼容包里面设置阴影效果自动设置了margin来处理16dp）

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305215053.png)



- 5.x上有Ripple水波纹效果

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305215500.png)

- 5.x实现按下的互动效果

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305215720.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305215904.png)


### FloatingActionButton ###

在design包下面。

	FloatingActionButton :悬浮动作按钮
	特性：1.阴影效果--景深（反馈动作：按下去阴影加深elevation）
		2.水波纹效果
	
		//3.其他效果--自己做
	
	兼容性注意:
		需要写两个layout/layout-v21
		layout-v21:添加layout_margin="16dp"
		layout: 添加layout_margin="0dp"
	
		app:backgroundTint="?attr/colorPrimary"背景着色
	        app:elevation="10dp"阴影深度
	        android:layout_margin="0dp"
	        app:fabSize="mini"大小：normal，mini


作业：分析源码CardView和FloatingActionButton


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305220921.png)

- 水波纹
 		
		rippleColor
		clickable

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170305221645.png)

end.