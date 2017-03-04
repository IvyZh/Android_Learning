![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.22
老师:Ricky


### 实现微博的Toolbar滑动半透明效果

xml布局文件：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303175816.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182045.png)

加个padding。


演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182219.png)

设置透明度：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182601.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182637.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182704.png)


如何让ScrollView绘制不考虑那个padding呢？

加上两个属性：

	android:clipToPadding="false" 该控件的绘制范围是否不在Padding里面。false：绘制的时候范围会考虑padding即会往里面缩进。
	android:clipChildren="false"  子控件是否能不超出padding的区域（比如ScrollView上滑动的时候，child可以滑出该区域）

演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303182955.png)


### Palette调色板 ###


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304093828.png)

palette 在v7包里面

> 可以在一张图片里面分析出一些色彩特性：主色调、鲜艳的颜色、柔和颜色等等……

是个单独的项目：引入v7里面的一个单独项目Palette，android.support.v7.graphics.Palette;
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304101746.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304101809.png)

异步：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304102044.png)


---

第二部分：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304102319.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304102408.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304102911.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304102952.png)

做个透明度：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304103406.png)

效果：

int alpha = rgb>>>24;//防止溢出

int blue = Color.blue(rgb);

int alpha = Color.alpha(rgb);

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170304103549.png)

end.