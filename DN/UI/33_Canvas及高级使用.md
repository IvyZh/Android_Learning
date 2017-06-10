![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.08
老师:Ricky


### Canvas的使用



Canvas的使用以及高级部分

Canvas：画布、画板。
一、Canvas基本的使用

绘制直线、点、几何图形、曲线、Bitmap、圆弧等等
Path路径来绘制线条

1.Region区域


Canvas画布的正确的理解：
	1）当canvas执行drawXXX的时候就会新建一个新的画布图层
		canvas.drawRect(r, paint);
	2）虽然后面新建了一个画布图层，但是还是会沿用之前设置的平移变换。不可逆的。（save和restore来解决）
		canvas.translate(50, 50);
		//当canvas执行drawXXX的时候就会新建一个新的画布图层
		canvas.drawRect(r, paint);
		RectF r2 = new RectF(0, 0, 400, 500);
		paint.setColor(Color.RED);
		//虽然新建了一个画布图层，但是还是会沿用之前设置的平移变换。不可逆的。（save和restore来解决）
		canvas.drawRect(r2, paint);



作业：1.实现圆角的头像控件。
	方法很多，提示：Xfermode
	2.实现Reveal效果。
	3.（选做）做一个侧滑菜单动画(类似SVG动画)，提示：源码


![](http://1)

![](http://2)

path:

![](http://3)

效果：
![](http://4)

Region：

![](http://5)

效果：
![](http://6)


---


第二小节


### Canvas变换技巧

![](http://7)

![](http://8)

![](http://9)

作业：

![](http://10)


---

END.