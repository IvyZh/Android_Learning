![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.10.09
老师:Ricky


### WaveView


Path工具类：用来记录线条的轨迹路径。
canvas.draw(path,paint);

贝塞尔曲线
手机充电等等效果
现实生活当中：任何的曲线和曲面都可以用贝塞尔公式来解决。比如：iPhone 2.5D屏幕曲面；奥迪A9流线型；

1.设计贝塞尔曲线或者贝塞尔曲线效果图
2.怎么去得到贝塞尔曲线的几个要素(比如二阶贝塞尔：p0初始位置,p1拐点,p2结束点)
p1拐点如何确定，可以通过工具来确定，比如Photoshop的钢笔工具等；
3.代码里面如何来实现。
Path工具类
Path path = new Path();
//二阶贝塞尔
path.quadTo();
//三阶贝塞尔
path.cubicTo();



作业：如何做一个圆形的水波纹上涨进度控件。

![](http://1)

![](http://2)


![](http://3)


![](http://4)

![](http://5)

---

END.