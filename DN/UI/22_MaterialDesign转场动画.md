![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.07.18
老师:Ricky


### Activity transition（Activity转场动画效果）

> 概念：两个Activity进行跳转的时候，转场动画。


	ActivityOptions类。只支持API21以上的版本。
	版本判断会比较麻烦，谷歌很贴心 设计了一个兼容类：ActivityOptionsCompat（v4包中）
	但是此类在低版本上面并没有转场动画效果，只是解决了我们手动去判断版本的问题而已。
	
	转场动画可以分为两大类：共享元素转换和普通的转换
	
	使用转换动画前提：需要给两个Activity都设置如下，让其允许使用转场动画。
	//方法一：
	getWindow().requestFeature(Window.FEATURE_CONTENT_TRANSITIONS);
	//方法二：
	修改主题：<item name="android:windowContentTransitions">true</item>

	1）共享元素转换
		概念：可以把两个Activity当中的相同的元素关联起来做连贯的变换动画。
		前提：（1）给两个Activity当中的共享元素view都设置同一个名字---android:transitionName
				<ImageView
				android:id="@+id/iv1"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:scaleType="centerCrop"
				android:transitionName="iv_meinv3"
				android:src="@drawable/meinv3" />

			
		
		按返回键的时候自动实现了返回的共享元素转场动画，原因看源码：
		public void onBackPressed() {
			finishAfterTransition();
		}
		public void finishAfterTransition() {
			if (!mActivityTransitionState.startExitBackTransition(this)) {
			    finish();
			}
		}

		//单个元素共享
		ActivityOptionsCompat optionsCompat = ActivityOptionsCompat.makeSceneTransitionAnimation(this, iv1, "iv_meinv3");
		Intent intent = new Intent(this, SecondActivity.class);
		startActivity(intent, optionsCompat.toBundle());
		//多个共享元素
		ActivityOptionsCompat optionsCompat = ActivityOptionsCompat
				.makeSceneTransitionAnimation(this, Pair.create((View)iv1, "iv1"),Pair.create((View)bt, "bt"));
		Intent intent = new Intent(this, SecondActivity.class);
		startActivity(intent, optionsCompat.toBundle());


	2）普通的转换动画
		（只有API 21才有下面自带效果）
		三种系统带的：滑动效果(Slide)、展开效果Explode、渐变显示隐藏效果Fade
			

之前的动画：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308175336.png)



实现转场动画：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308180510.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308181520.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308182525.png)

---

第二部分。



- 普通的转换动画（只有API 21才有下面自带效果）
	- 三种系统带的：滑动效果(Slide)、展开效果Explode、渐变显示隐藏效果Fade

Slide:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308183158.png)

进场动画：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308183406.png)

Explode：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170308183621.png)

同样也要设置进场动画。

Fade效果也是同样的设置。

作业：
	1.实现揭露效果的低版本兼容！

作业：
	1.使用RecyclerView实现共享元素转场动画。
	2.如何实现普通的转换动画滑动效果(Slide)，兼容低版本实现。
		手动撸。提示：各种属性动画组合实现。

	view.setTranslationX(xxx)
	objectClass.setCurrentRadius(xxx)


InstagramDemo2

end.