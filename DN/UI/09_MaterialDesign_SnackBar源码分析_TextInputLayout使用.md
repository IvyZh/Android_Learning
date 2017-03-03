![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.22
老师:Ricky


### SnackBar源码分析

查看源码工具：zeal

google插件： Android Resource Navigator , Android Sdk Search

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303125914.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303132145.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303132526.png)

SnackbarManager,

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303133710.png)

自定义SnakebarLayout：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303135156.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303135722.png)


	源码分析：
	do{
		//不断地查找parent,实际上就是找到最外层的FrameLayout
		view.getParent();
	}while()
	.......
	rootView.addView(view);//添加到最外层的布局容器里面



### TextInputLayout ###

> 是强大的带提示的MD风格的Edittext

> 看源码：TextInputLayout extends android.widget.LinearLayout

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303142801.png)

导入design。

	<android.support.design.widget.TextInputLayout
	        android:layout_width="fill_parent"
	        android:layout_height="wrap_content" 
	        app:hintAnimationEnabled="true"
	        >
	        <EditText
	            android:layout_width="fill_parent"
	            android:layout_height="wrap_content"
	            android:hint="请输入用户名" />
	</android.support.design.widget.TextInputLayout>
	
	app:hintAnimationEnabled="true" ： 是否获得焦点的时候hint提示问题会动画地移动上去。
	app:errorEnabled="true" 是都打开错误提示。
	要使用错误提示还得自己定义规则。
	app:counterTextAppearance="" 可以自己修改计数的文字样式。
	app:counterOverflowTextAppearance="" 超出字数范围后显示的警告的文字样式



---

第二部分。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303151232.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303151250.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303151352.png)

- 源码分析：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303152538.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303152808.png)


end.