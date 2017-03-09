![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.19
老师:Ricky


### SVG

> svg可以使用工具来生成。


	引导：微信引入的SVG技术。
	http://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=207863967&idx=1&sn=3d7b07d528f38e9f812e8df7df1e3322&scene=4#wechat_redirect
	1.概念
		1）SVG，即Scalable Vector Graphics 可伸缩矢量图形，这种图像格式在前端中已经使用的非常广泛了。
			SVG的W3C的解释： http://www.w3school.com.cn/svg/svg_intro.asp
			首先要解释下什么是矢量图像，什么是位图图像？ 
			1、矢量图像：SVG是W3C 推出的一种开放标准的文本式矢量图形描述语言,他是基于XML的、专门为网络而设计的图像格式，
				SVG是一种采用XML来描述二维图形的语言，所以它可以直接打开xml文件来修改和编辑。 
			2、位图图像：位图图像的存储单位是图像上每一点的像素值，因而文件会比较大，像GIF、JPEG、PNG等都是位图图像格式。
		2）Vector，在Android中指的是Vector Drawable，也就是Android中的矢量图，
				可以说Vector就是Android中的SVG实现(并不是支持全部的SVG语法,现已支持的完全足够用了)

		补充：Vector图像刚发布的时候，是只支持Android 5.0+的，自从AppCompat 23.2之后，Vector可以使用于Android 2.1以上的所有系统，
				只需要引用com.android.support:appcompat-v7:23.2.0以上的版本就可以了。（所谓的兼容也是个坑爹的兼容，即低版本非真实使用SVG,而是生成PNG图片）

	2.Vector Drawable:
		Android 5.0发布的时候，Google提供了Vector的支持，即：Vector Drawable类。
		Vector Drawable相对于普通的Drawable来说，有以下几个好处：
		（1）Vector图像可以自动进行适配，不需要通过分辨率来设置不同的图片。
		（2）Vector图像可以大幅减少图像的体积，同样一张图，用Vector来实现，可能只有PNG的几十分之一。
		（3）使用简单，很多设计工具，都可以直接导出SVG图像，从而转换成Vector图像 功能强大。
		（4）不用写很多代码就可以实现非常复杂的动画 成熟、稳定，前端已经非常广泛的进行使用了。

		1） Vector 语法简介
			通过使用它的Path标签，几乎可以实现SVG中的其它所有标签，虽然可能会复杂一点，
			但这些东西都是可以通过工具来完成的，所以，不用担心写起来会很复杂。
			(1)Path指令解析如下所示：
				M = moveto(M X,Y) ：将画笔移动到指定的坐标位置，相当于 android Path 里的moveTo()
				L = lineto(L X,Y) ：画直线到指定的坐标位置，相当于 android Path 里的lineTo()
				H = horizontal lineto(H X)：画水平线到指定的X坐标位置 
				V = vertical lineto(V Y)：画垂直线到指定的Y坐标位置 
				C = curveto(C X1,Y1,X2,Y2,ENDX,ENDY)：三次贝赛曲线 
				S = smooth curveto(S X2,Y2,ENDX,ENDY) 同样三次贝塞尔曲线，更平滑 
				Q = quadratic Belzier curve(Q X,Y,ENDX,ENDY)：二次贝赛曲线 
				T = smooth quadratic Belzier curveto(T ENDX,ENDY)：映射 同样二次贝塞尔曲线，更平滑 
				A = elliptical Arc(A RX,RY,XROTATION,FLAG1,FLAG2,X,Y)：弧线 ，相当于arcTo()
				Z = closepath()：关闭路径（会自动绘制链接起点和终点）

				注意，’M’处理时，只是移动了画笔， 没有画任何东西。

		注意：1.关于这些语法，开发者不需要全部精通，而是能够看懂即可，这些path标签及数据生成都可以交给工具来实现。
			（一般美工来帮你搞定！PS、Illustrator等等都支持导出SVG图片）

				2.程序员：没必要去学习使用这些设计工具，开发者可以利用一些工具，自己转换一些比较基础的图像，
					如：http://inloop.github.io/svg2android/ 
				3.还可以使用SVG的编辑器来进行SVG图像的编写，例如：http://editor.method.ac/
				（绝配！可以先用http://editor.method.ac/ 生成SVG图片，然后用http://inloop.github.io/svg2android/ 生成 VectorDrawable xml代码）
				4.使用AndroidStudio插件完成SVG添加（Vector Asset Studio）
					详细：http://www.jianshu.com/p/d6c39f2dd5e7
					AS会自动生成兼容性图片(高版本会生成xxx.xml的SVG图片；低版本会自动生成xxx.png图片)
				5.有些网站可以找到SVG资源
					SVG下载地址： http://www.shejidaren.com/8000-flat-icons.html
								  http://www.flaticon.com/



> 可以先用http://editor.method.ac/ 生成SVG图片，然后用http://inloop.github.io/svg2android/ 生成 VectorDrawable xml代码）


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309153046.png)



使用图片，就当普通的图片使用就可以了。

	<ImageView
		android:id="@+id/iv"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		app:src="@drawable/vector_image"/>
	或者代码设置：
		ImageView iv = (ImageView) findViewById(R.id.iv);
		iv.setImageResource(R.drawable.vector_image);
		iv.setBackgroundResource(R.drawable.vector_image)
	如果是Button，可以设置selector（写两个SVG的Drawable）
		<?xml version="1.0" encoding="utf-8"?>
		<selector xmlns:android="http://schemas.android.com/apk/res/android">
			<item android:drawable="@drawable/selector1" android:state_pressed="true"/>
			<item android:drawable="@drawable/selector2"/>
		</selector>

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309160443.png)



---

第二部分。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309162624.png)



### 动态Vector ###

> 动态Vector才是Android Vector Drawable的精髓所在

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309170950.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309171025.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309171315.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309171425.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170309171814.png)


end.