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

![](http://1)

简化操作：自定义HorizontalScrollView,重写onScrollChanged方法

布局：

menu.xml & main.xml

素材：

![](http://2)


main布局：

![](http://3)


自定义SlidingMenu继承HorizontalScrollView

onMeasure：

![](http://4)

onLayout：

![](http://5)


onTouch：

![](http://6)

处理属性动画：

![](http://7)

透明度效果：

ViewHelper.setAlpha(mMenu,1-factor);


### 自定义控件-条目侧滑菜单的效果


效果：

![](http://8)

继承线性布局SlidingItemMenuLayout

布局文件：

![](http://9)

自定义布局：

![](http://10)

