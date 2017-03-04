![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.08
老师:Ricky


### TabLayout

选项卡

1. 以前：TabHost

2. 现在：android.support.design.widget.TabLayout

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304110447.png)

TabLayout控件，切换Fragment，TabLayout+ViewPager+Fragment 

XML布局：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304111006.png)

java代码：

appcompatactivity是可以兼容v4包下面的fragment的。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304111634.png)


Fragment：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304111747.png)

tablayout：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304111919.png)


效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304112036.png)

双向关联滑动：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304112206.png)

滑动viewpage关联tablayout：ctrl+t快捷键

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304112355.png)

效果演示ok。

Tablayout源码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304113453.png)


	app:tabIndicatorColor="@color/colorPrimary_pink"//指示器的颜色
    app:tabTextColor="@color/colorPrimary_pink"//tab的文字颜色
    app:tabSelectedTextColor="@color/colorPrimary_pinkDark"//选中的tab的文字颜色
    app:tabMode="fixed"//scrollable:可滑动；fixed：不能滑动，平分tabLayout宽度
    app:tabGravity="center"// fill:tabs平均填充整个宽度;center:tab居中显示


	二、如何将TabLayout实现成底部导航的样子？
	1.就把TabLayout放在布局底部
	2.如何去掉底部的indicator，可以app:tabIndicatorHeight="0dp"
	3.实现自己的效果，比如
	微信：设置自定义的标签布局
		Tab tab = tabLayout.getTabAt(i);
		tab.setCustomView(view);

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304115308.png)

源码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304115557.png)

自定义样式：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304115848.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304115920.png)

源码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304121026.png)

tab.setIcon();



	作业：
	1.tabLayout选项卡之间使用间隔线隔开
	2.滑动变色。