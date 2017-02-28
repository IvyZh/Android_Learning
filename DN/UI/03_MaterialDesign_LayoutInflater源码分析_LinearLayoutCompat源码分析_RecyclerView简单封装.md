![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.06
老师:Ricky


### 回顾

1. 修复bug

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228152606.png)

	
- 解决本次课的瀑布流效果的bug

		报错：NullPointException----LayoutParams为空
		
		View.inflate(viewGroup.getContext(), android.R.layout.simple_list_item_1, null)
		最终都会调用该方法：
		inflate(resource, root, root != null);
		inflate(resource, null, false);
		
		经过修改：
		MyViewHolder holder = new MyViewHolder(View.inflate(viewGroup.getContext(), android.R.layout.simple_list_item_1, viewGroup));
		还是报错：
		java.lang.IllegalStateException: 
		The specified child already has a parent. You must call removeView() on the child's parent first.
		默认还是调用的：
		inflate(resource, root, root != null);
		inflate(resource, root, true);
		看源码就知道：多做了一个事情就是
		 if (root != null && attachToRoot) {
		                        root.addView(temp, params);
		                    }
		
		由于RecyclerView/ListView会自动将child添加到它里面去
		
		为何Fragment的onCreateView又可以呢？
		
		
		最终结局办法：
		首先，root不为null, boolean(attachToRoot)必须为false。
		inflate(resource, root, false);

还有一种方式，simple_list_item_1.xml中的textview加一个父布局，这样就可以直接偷懒使用View.inflate(context,resId,null)这个方法了。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228154640.png)

关联LinearLayoutCompat源码

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228155042.png)

* 看源码LinearLayoutCompat ，分析实现的原理:是如何做到给里面的所有的child之间添加间隔线的？
	
		View的绘制会经过三个方法：onMearsue（测量自身和里面的所有子控件）,onLayout（摆放里面所有的子控件）,onDraw（绘制）
		猜想：
		1）mearsuredWidth,mearsuredHeight会变大（加上间隔线）；
		2）摆放子控件位置会有一定的体现（childView: left/top/right/bottom）；
		3)onDraw绘制的时候也会有体现（childView: left/top/right/bottom）；

- 切换布局
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228164911.png)

- 添加、删除条目

adapter.setItemAnimator();

- RecyclerView没有条目点击事件，需要自己写。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228170209.png)

这里有点不太懂，讲到位置问题。`解决position可能错位的问题`

holder.getLayoutPosition();