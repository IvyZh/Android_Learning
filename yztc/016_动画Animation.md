## 第16讲_01_FrameAnimation的使用

主要内容：

1. 动画的分类
2. 动画的用法


### 动画的分类

1. 帧动画
2. 补间动画：透明、旋转、缩放、平移
3. 属性动画：改变控件本身的属性


### 动画的用法

帧动画：

1. 素材是一系列的连续帧动画

2. 在drawable文件夹下 创建girl.xml文件

		<animation-list>
		
			<item android:drawable="@drawable/girl_1"
				android:duration="200">
			
		</animation-list>


3. 使用

		<ImageView
			...
			android:background="@drawable/girl"
			/>


4. 代码中

		AnimationDrawable animation = (AnimationDrawable)iv.getBackground();//用来创建帧动画的对象
		animation.start();//stop();
	

## 第16讲_02_补间动画的用法


透明：

	AlpaAnimation aa = new AlphaAnimation(0.1f,1.0f);
	aa.setDuration(2000);
	aa.setRepeatCount(2);// 会执行3次
	aa.setRepeatMode(Animation.RESTART);// 重复模式 REVERSE（反转）
	aa.setFillAfter(true);// 保持结束时候的状态
	iv.startAnimation(aa);

平移：
	
	// fromXDelta,toXDelta,fromYDelta,toYSDelta : x的起点和终点 y的起点和终点。以像素为单位
	TranslateAnimation ta = new TranslateAnimation(fromXDelta,toXDelta,fromYDelta,toYSDelta);
	...
	iv.startAnimation(ta);

	
	//fromXType:在x轴上进行变化时的类型 Animation.ABSOLUTE， RELATIVE_TO_PARENT ，RELATIVE_TO_SELF，

	// RELATIVE_TO_SELF+0.0f: 表示控件现在所在的坐标+0*控件本身的宽度 
	// RELATIVE_TO_SELF+0.5f: 表示控件现在所在的坐标+0.5*控件本身的宽度 

	// RELATIVE_TO_PARENT+0.5f：表示控件现在所在的坐标+0.5*控件的父控件的宽度 

	new TranslateAnimation(fromXType,fromXValue,toXType,toXValue,fromYType,fromYValue,toYType,toYValue);


旋转：
	
	new RotateAnimation(fromDegress,toDegress);// 0,45
	new RotateAnimation(fromDegress,toDegress,...)

缩放：
	
	new ScaleAnimation(fromX,toX,fromY,toY);// 0,2,0,2
	new ScaleAnimation(fromX,toX,fromY,toY,pivatXType,pivotXvalue...)



	AnimationSet as = new AnimationSet(true);// 表示使用同一个插值器
	as.addAnimation(aa);
	...
	iv.startAnimation(as);

## 第16讲_03_属性动画的用法

透明：

<ImageView 这个控件有个属性alpha


	ObjectAnimator anim = ObjectAnimator.ofFloat(target,propertyName,values);// iv,"alpha",0,0.5f
	// anim.set....
	anim.start();


平移：

	ObjectAnimator anim = ObjectAnimator.ofFloat(iv,"translation",0,200);

旋转：

	ObjectAnimator anim = ObjectAnimator.ofFloat(iv,"rotationX",0,180);


缩放：

	ObjectAnimator anim = ObjectAnimator.ofFloat(iv,"scaleX",0,4);

集合：


	AnimatorSet set = new AnimatorSet();
	List<Animator> items = new ArrayList<Animator>();
	// ...
	// set.play(anim);
	set.playSequentially(items);
	set.start();