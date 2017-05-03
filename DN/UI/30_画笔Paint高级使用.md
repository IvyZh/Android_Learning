![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.08.21[怎么变成8月21了
老师:Ricky


### 基本使用

1. 负责图形绘制
2. 负责文字绘制


负责图形绘制


	//重置
	mPaint.reset();
	mPaint.setColor(Color.RED);
	mPaint.setAlpha(255);
	//设置画笔的样式
	//		mPaint.setStyle(Paint.Style.FILL);//填充内容
	//		mPaint.setStyle(Paint.Style.FILL_AND_STROKE);
		mPaint.setStyle(Paint.Style.STROKE);//描边
	//画笔的宽度
		mPaint.setStrokeWidth(50);
	//线帽
	//		mPaint.setStrokeCap(Paint.Cap.BUTT);//没有
		mPaint.setStrokeCap(Paint.Cap.ROUND);//圆形
	//		mPaint.setStrokeCap(Paint.Cap.SQUARE);//方形
		
	//		mPaint.setStrokeJoin(Paint.Join.MITER);//锐角
	//		mPaint.setStrokeJoin(Paint.Join.ROUND);//圆弧
	//		mPaint.setStrokeJoin(Paint.Join.BEVEL);//直线
	//线段的连接处的样式
	//		mPaint.setStrokeJoin(Paint.Join.MITER);//锐角
	//		mPaint.setStrokeJoin(Paint.Join.ROUND);//圆弧
	//		mPaint.setStrokeJoin(Paint.Join.BEVEL);//直线

	//防锯齿，会损失一定的性能
		mPaint.setAntiAlias(true);