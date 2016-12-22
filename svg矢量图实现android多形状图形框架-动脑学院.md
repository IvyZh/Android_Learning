位图：可以看到像素点 png jpg...
矢量图：算法生成的 依据路径
SVG：SVG 是使用 XML 来描述二维图形和绘图程序的语言。


矩形：

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
	"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	
	<svg width="100%" height="100%" version="1.1"
	xmlns="http://www.w3.org/2000/svg">
	
		<rect width="300" height="100"
		style="fill:rgb(0,0,255);stroke-width:1;
		stroke:rgb(0,0,0)"/>
	
	</svg>


SVG路径Path：

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
	"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	
	<svg width="100%" height="100%" version="1.1"
	xmlns="http://www.w3.org/2000/svg">
	
	<path d="M250 150 L150 350 L350 350 Z" />
	
	</svg>


如何使用这个xml的svg呢？又该如何合成呢？

SVGParser解析XML文件。


code:得到svg的picture的bitmap

	getSvgBitmap(context,size,size,svgRawRourceId)	{
		Bitmap bitmap = Bitmap.creatBitmap(width,heigth,Config.ARGB_8888);
		Canvas canvas = new Canvas(bitmap);
		Paint paint = new Paint(Paint.ANTI_ALIAS_FLAG);
		paint.setColor(Color.BLACK);
		
		if(svgRawResourceId>0){
		
			SVG svg = SVGParser.getSVGFromInputStream(content().getResource().openRawResource(svgRawResourceId),...);
			canvas.drawPicture(svg.getPicture());
		}else{
			canvas.drawRect(new Rect(0,0,width,width),paint);
		}
		
		return bitmap;
	}
	


code：根据svg图形和原始图片合成目标图片

	public static Bitmap getSvgShapeBitmap(Context contex,Bitmap fg,int svgRawRourceId){
	
		int size = Math.min(fg.getWidth(),fg.getHeigth());
		int x = (fg.getWidth()-size)/2;
		int y = (fg.getHeigth()-size)/2;
	
		// 先加载svg图片
		Bitmap bg = getSvgBitmap(context,size,size,svgRawRourceId);
		Paint paint = new Paint(Paint.ANTI_ALIAS_FLAG);
		Bitmap bitmap = Bitmap.creatBitmap(width,heigth,Config.ARGB_8888);
		Canvas canvas = new Canvas(bitmap);
		canvas.drawBitmap(bg,new Matrix(),pain);
		// 设置交集模式SrcATop
		pain.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.SRC_ATOP));
		canvas.drawBitmap(Bitmap.createBitmap(fg,x,y,size,size),new Matri(),paint);
		return bitmap();
	}


![](http://dl.iteye.com/upload/attachment/567804/f3756216-bc69-348f-9f4f-55428a78a287.png)