![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.08
老师:Ricky


### 回顾

- 解决position可能错位的问题。
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301104900.png)


### RecyclerView设置分割线

设置分割线方向
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301111950.png)

确定Rect
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301112044.png)

写shape
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301125234.png)

先使用系统的list_divider

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301125628.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301130647.png)

绘制所有的分割线：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301141543.png)

ViewCompat.getTranslationX(child);

mDivider.getIntrinsicHeight();

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301142039.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301142517.png)

修改代码：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301143104.png)

表格的效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301143300.png)



---

第二部分

网格的分割线

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301150758.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301151051.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301151129.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301151146.png)

水平线：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301154143.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301154202.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301154631.png)

总结：


	1.RecyclerView没有默认的分割线，需要自己绘制。
	RecyclerView.ItemDecoration
		1)线性的分割线
		2）网格的分割线
	
	1）.可以通过修改Theme.Appcompa主题样式里面的android:listSelector或者 android:listDivider属性
		达到改变间隔线的大小和颜色哦！（自己尝试下）
			    <style name="AppTheme" parent="AppBaseTheme">
				<item name="android:listDivider">@drawable/item_divider</item>
			    </style>
		2）.写一个条目装饰类，继承
		class MyItemDecoration extends RecyclerView.ItemDecoration{
		}
	
	绘制分发。
		绘制RecyclerView的时候会分发Canvas到ItemDecoration里面。
	
	作业：
		1。现在DividerGridViewItemDecoration还有不完善的吗？
		效果上面
		2。看ItemDecoration的绘制分发的过程源码粗略分析


end.




