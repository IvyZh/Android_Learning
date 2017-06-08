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


2. 文字绘制

![](http://1)

![](http://2)



			//获得字符行间距
	//		mPaint.getFontSpacing();
			//获得字符之间的间距
	//		mPaint.getLetterSpacing();
	//		mPaint.setLetterSpacing(letterSpacing)//设置
			//设置文本删除线
	//		mPaint.setStrikeThruText(true);
			//是否设置下划线
	//		mPaint.setUnderlineText(true);
			//设置文本大小
	//		mPaint.setTextSize(textSize);
	//		mPaint.getTextSize();
	//		mPaint.setTypeface(Typeface.BOLD);//设置字体类型
	//		Typeface.ITALIC
	//		Typeface.create(familyName, style)//加载自定义字体
			//文字倾斜 默认0，官方推荐的-0.25f是斜体
	//		mPaint.setTextSkewX(-0.25f);
			//文本对齐方式
	//		mPaint.setTextAlign(Align.LEFT);
	//		mPaint.setTextAlign(Align.CENTER);
	//		mPaint.setTextAlign(Align.RIGHT);
			//计算制定长度的字符串（字符长度、字符个数、显示的时候真实的长度）
	//		int breadText = mPaint.breakText(text, measureForwards, maxWidth, measuredWidth)
			
			mPaint.setTextSize(50);
	//		float[] measuredWidth = new float[1];
	//		int breakText = mPaint.breakText(str, true, 200, measuredWidth);
	//		Log.i("RICKY", "breakText="+breakText+", str.length()="+str.length()+", measredWidth:"+measuredWidth[0]);
			
			// Rect bounds获取文本的矩形区域（宽高）
	//		mPaint.getTextBounds(text, index, count, bounds)
	//		mPaint.getTextBounds(text, start, end, bounds)
			
			//获取文本的宽度，和上面类似，但是是一个比较粗略的结果
			float measureText = mPaint.measureText(str);
			//获取文本的宽度，和上面类似，但是是比较精准的。
			float[] measuredWidth = new float[10];
			
			//measuredWidth得到每一个字符的宽度；textWidths字符数
			int textWidths = mPaint.getTextWidths(str, measuredWidth);
	//		mPaint.getTextWidths(text, start, end, widths)
			Log.i("RICKY", "measureText:"+measureText+", textWidths:"+textWidths);
		



3. 基线的问题

![](http://3)


![](http://4)


![](http://5)


		FontMetrics fontMetrics = mPaint.getFontMetrics();
		fontMetrics.top;
		fontMetrics.ascent;
		fontMetrics.descent;
		fontMetrics.bottom;
		所有的四个值都是以基线baseLine为基准来计算的。baseline以上的就是负的；以下的是正的。

		在做自定义控件的时候canvas.drawText(x,y) 这个y并不是text的左上角，而是以baseline为基准的。

		1）实例：指定左上角的顶点坐标 绘制文本
		公式： float baselineY = Y - fontMetrics.top;

		
		2）实例：指定中间位置，绘制文本
		公式： float baselineY = centerY + (fontMetrics.bottom-fontMetrics.top)/2 - fontMetrics.bottom
		

作业:1.实现自定义进度条
	2.实现价格标签自定义控件。

----

案例：自定义进度条


定义参数：


![](http://6)

![](http://7)


![](http://8)

![](http://9)


![](http://10)

效果：

![](http://11)


End.