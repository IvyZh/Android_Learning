![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.08
老师:Ricky


### 回顾

v7可以最低兼容到3.0版本

	CoordinatorLayout
		--RecylerView（app:kayout_behavior="@string/appbar_scrolling_view_behavior"）
		--AppBarLayout(extends LinearLayout,scroll_flags:enterAlways)实际上appbar已经配置了behavior，只要配置这个flags就可以了。
			--Toolbar
		--FloatingActionButton


AppBarLayout源码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307124105.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307124622.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307124641.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307125059.png)

ViewOffsetBehavior-onLayoutChild

自己写的Behavior：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307125641.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307125755.png)


CollapsingToolbarLayout：


	CoordinatorLayout
		--RecylerView（app:kayout_behavior="@string/appbar_scrolling_view_behavior"）
		--AppBarLayout(extends LinearLayout,scroll_flags:enterAlways)实际上appbar已经配置了behavior，只要配置这个flags就可以了。
			--CollapsingToolbarLayout
				--ImageView
				--Toolbar
		--FloatingActionButton


Behavior

> 所有的Behavior都继承CoordinatorLayout.Behavior，桥梁，监听者。包裹在里面的所有子控件或者容器产生的联动效果。

Behavior可以做到下面两种情况：

某个View需要监听另外一个View的状态（比如：位置、大小、显示状态）；
某个View需要监听CoordinatorLayout里面所有控件的滑动状态。




- 某个View需要监听另外一个View的状态（比如：位置、大小、显示状态）
	- 需要重新方法layoutDependsOn/onDependtentViewChanged


### 自定义Behavior ###

实现B控件监听A控件的状态；

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307144528.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307145542.png)

ViewCompat:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307151742.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307152010.png)


效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307152129.png)

---

第二部分：


- 某个View需要监听CoordinatorLayout里面所有控件的滑动状态
	- 需要重写方法：onStartNestedScroll,onNestedScroll,或者onNestedPreScroll
	- 能被CoordinatorLayout捕获到滑动状态的控件只有：RecyclerView、NestedScrollView、ViewPager

案例：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307154731.png)

记得用线性布局嵌套这些TextView

效果是左右两个NestedScrollView，滑动一个 另一个也跟随滑动。

给观察者添加Behavior

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307155401.png)

滑动效果ok：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307155438.png)

问题：快速滑动的时候，右边没有跟上。

解决：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170307160001.png)


想一下这些方法到底是怎么触发的？

了解CoordinatorLayout是如何做到监听里面子控件的状态改变，并执行回调（onStartNestedScroll，onNestedScroll...）过程？


end.










