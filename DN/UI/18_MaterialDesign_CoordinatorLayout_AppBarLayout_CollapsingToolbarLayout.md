![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.08
老师:Ricky


### CoordinatorLayout

回顾项目：materialdesign_fab_animator_behavior

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306163603.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306163741.png)

FabBehavior:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306164129.png)

Behavior(CoordinatorLayout.Behavior/FloatingActionButton.Behavior)


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306165014.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306165058.png)


bug：snackbar盖住了fab

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306165425.png)


> 谷歌有个bug在最新版的Design包里面解决了：snackbar弹出的时候会遮挡住fab.

> 解决：用CoordinatorLayout将其包裹在里面就可以解决了。


### AppBarLayout ###

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306170536.png)

演示效果ok。

scrollFlags:scroll属性

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306170714.png)


	scroll: 里面所有的子控件想要当滑出屏幕的时候view都必须设置这个flag，
		没有设置flag的view将被固定在屏幕顶部。
	enterAlways:('quick return' pattern)
	enterAlwaysCollapsed：当你的视图设置了minHeight属性的时候，那么视图只能以最小高度进入，
				只有当滚动视图到达顶部时才扩大到完整高度。
	exitUntilCollapsed：滚动退出屏幕，最后折叠在顶端。
	snap：


scroll+enterAlways


### NestedScrollView ###

来自v4包下：android.support.v4.widget.NestedScrollView; 在v4包里面，是ScrollView的升级版

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306172835.png)


NestedScrollView下面放几个CardView，记得嵌套LinearLayout

演示效果ok。


ViewPager+TabLayout+Fragment + AppBarLayout

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306174502.png)

AppBarLayout实际上是继承了LinearLayout。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306174612.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306174759.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306174856.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306175101.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306175120.png)

---

### CollapsingToolbarLayout ###

> 可以实现Toolbar折叠效果,来自design包下面


注意:1.AppBarLayout设置固定高度，并且要实现折叠效果必须比toolbar的高度要高。
	     2.CollapsingToolbarLayout最好设置成match_parent

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306181121.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306181630.png)



	
	<android.support.design.widget.CollapsingToolbarLayout
	            android:layout_width="match_parent"
	        	android:layout_height="match_parent"
	            app:layout_scrollFlags="scroll|enterAlways"
	            app1:collapsedTitleTextAppearance=""
	            app1:expandedTitleMargin="5dp"
		   		app1:contentScrim="@color/colorPrimary_pink"//内容部分的沉浸式效果：toolbar和imageview有一个渐变过渡的效果
	            app1:statusBarScrim="@color/colorPrimary_pink"//和状态栏的沉浸式效果：指定颜色。
	        	app1:title="动脑学院"
	            >

5.0效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170306182505.png)



	app:layout_collapseMode="parallax" 
		parallax:视差模式，在折叠的时候会有折叠视差效果。
			一般搭配layout_collapseParallaxMultiplier=“0.5”视差的明显程度
			 be between 0.0 and 1.0.
		none:没有任何效果，往上滑动的时候toolbar会首先被固定并推出去。
		pin:固定模式，在折叠的时候最后固定在顶端。


end.
