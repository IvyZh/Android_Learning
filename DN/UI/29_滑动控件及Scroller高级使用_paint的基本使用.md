![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.25
老师:Ricky


### 回顾

Scroller.java

View : scrollTo(x,y)
	scrollBy(x,y)

手动实现Viewpager滑动效果
自定义ViewGroup

1.侧滑菜单的效果
自定义HorizontalScrollView
重写onScrollChanged方法



2.条目侧滑菜单的效果。
ListView


### QQ侧滑

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418135259.png)



简化操作：自定义HorizontalScrollView,重写onScrollChanged方法

布局：

menu.xml & main.xml

素材：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418135718.png)


main布局：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418135808.png)




自定义SlidingMenu继承HorizontalScrollView

onMeasure：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418160417.png)


onLayout：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418160646.png)



onTouch：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418161419.png)


处理属性动画：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418161952.png)


透明度效果：

ViewHelper.setAlpha(mMenu,1-factor);


### 自定义控件-条目侧滑菜单的效果


效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170418203451.png)


继承线性布局SlidingItemMenuLayout

布局文件：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170420113823.png)


自定义布局：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170420114350.png)

代码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426152423.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426152501.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426152637.png)


记得要加上滑动的临界判断


### 3Paint的基本使用及重点方法_recv

画笔实现的水波纹扩散效果

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426153734.png)


重点来了：

线帽StrokeCap
StrokeJoin

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426154235.png)


测试效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426154502.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426154950.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170426155010.png)


End.