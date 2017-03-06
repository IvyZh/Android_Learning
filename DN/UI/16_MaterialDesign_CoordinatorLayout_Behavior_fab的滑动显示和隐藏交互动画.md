![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.08
老师:Ricky


### FloatingActionBar源码

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306104018.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306104907.png)

### CoordinatorLayout ###

Android平行空间效果：实现滑动RecyclerView,Fab显示和隐藏。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306105708.png)

下滑的时候Toolbar和fab隐藏，上滑显示。

用shape给自定义的fab做背景，是通过layer-list来实现的

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306110035.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306110224.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306110233.png)

代码设置监听：


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306110730.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306110745.png)

执行动画：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306111509.png)

修改：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306111912.png)

Toolbar的显示与隐藏：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306111958.png)


end.


注意事项：

视频讲解到RecyclerView+自定义FloatingActionButton 滑动监听RecyclerView来控制fab和toolbar的显示隐藏就完了，后面的内容就没了，CoordinatorLayout都没有讲解。

	方法二：Behavior
	RecyclerView+FloatingActionButton+CoordinatorLayout
	
	CoordinatorLayout: 继承自ViewGroup。
		通过协调并调度里面的子控件或者布局来实现触摸（一般是指滑动）产生一些相关的动画效果。
		可以通过设置view的Behavior来实现触摸的动画调度。
	
	作业：平行空间的欢迎页面效果实现。（提示：viewpager）


