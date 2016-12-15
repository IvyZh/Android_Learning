
(一一哥)
## 第11讲_01_OptionsMenu的使用

主要内容：

1. Menu是啥？
2. Menu现状如何？
3. Menu的分类有哪些？
4. Menu怎么使用

### Menu是啥？

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215102732.png)

### Menu现状如何？

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215105124.png)
![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215105238.png)

Menu- 3.0之前

ActionBar  3.0

ToolBar 5.0


以后菜单就没怎么使用了。

### Menu的分类有哪些？

1. OptionsMenu
2. ContextMenu
3. PopupMenu


### Menu怎么使用


* OptionsMenu ： 选项菜单
	* onCreateOptionsMenu
* ContextMenu : 上下文菜单
	* onCreateOptionsMenu
* PopupMenu
	* PopupMenu popMenu = new PopupMenu(this,v);



OptionsMenu:


	//创建选项菜单
	public boolean onCreateOptionsMenu(Menu menu){
		getMenuInflate.inflate(R.menu.main,menu);
		return true;//true 使得菜单可以被显示出来
	}


	// 处理OptionsMenu点击事件
	public boolean OptionsMenuItemSelected(MenuItem item){
		int id = item.getItemId();
		if(id = R.id.action_strings){
			return true;
		}
		return super.onOptionsItemSelected(item);
	}


main.xml(res/menu/mail.xml

	<?xml version="1.0" encoding="utf-8"?>
	
	<menu xmlns:android="http://schemas.android.com/apk/res/android">
	 
	    <item android:id="@+id/connect"
			android:orderInCategory="100"
	        android:showAsAction="never"
			android:icon="@android:drawable/ic_menu_send"
	        android:title="连接" />
	</menu>




创建选项菜单另一种方式

	public boolean onCreateOptionsMenu(Menu menu){
		getMenuInflate.inflate(R.menu.main,menu);
		menu.add(Menu.NONE,Menu.NONE,Menu.NONE,"扫描");
		return true;//true 使得菜单可以被显示出来
	}


## 第11讲_02_ContextMene的使用

	创建方式：
	
	publi void onCreateContextMenu(ContextMenu menu,View v,ContextMenuInfo menuInfo){
		getMenuInflater.inflate(R.menu.main,menu);
	}
	
	
	处理上下文菜单的点击事件
	
	onContextItemSelected(MenuItem item){
		
		
	}


注册上下文菜单：
	
registerForContextMenu(tvMesg);// 长按弹出的效果。


获取控件的宽高：v.getWidth();


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215191234.png)

通常上下文菜单是和ListView或者GridView这种适配器控件绑定在一起。

## 第11讲_03_PopupMenu

	show(View v){
		PopupMenu popMenu = new PopupMenu(this,anchor);//anchor铆点
		getMenuInflater().inflate(R.menu.main,popupMenu.getMenu());
		popMenu.show();
		popMenu.setOnMenuItemClick();
	}

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215192011.png)

## 第11讲_04_PopupWindow

主要内容：

1. PopupWindow是啥？
2. PopupWindow的分类有哪些？
3. PopupWindow的使用


### PopupWindow是啥？

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215192203.png)

### PopupWindow的分类有哪些？

一种是在某个控件下面（下拉式，微信），另一种是覆盖在控件之上，浮动的（浮动式，QQ）。



### PopupWindow的使用

* 下拉式
	* mWindow.showAsDropDown(anchor,xoff,yoff,gravity);

* 浮动式
	* mWindow.showAtLocation(contentView,Grivaty.BOTTOM,0,0);



code:
	
	PopupWindown mWindown = new PopupWindown(contentView,width,heigth);//LayoutParams.WRAP_CONTENT,MATCH_PARENT
	mWindown.setOutsideTouchable(true);//设置点击外面消失
	mWindown.setBackgroundDrawable(drawable);//设置背景
	mWindown.setTouchable(true);//设置触摸时是否会有响应




	onKeyDown(int keyCode,KeyEvent event){//处理某个按键的方法
	
		switch(keyCode){
			case KeyEvent.KEYCODE_MENU:
				if(mWindow.isShowing())
					mWindown.dismiss();
				else
					mWindow.showAtLocation(contentView,Gravity.BOTTOM,0,0);
				break;
			case KeyEvent.KEYCODE_BACK:
	
				brea;
		}
	}


	onDestory(){
		if(mWindown!=null){
			mWindown.dismiss();
			mWindown = null;
		}
	}


## 第11讲_05_AlertDialog

主要内容：

1. Dialog是啥？
2. Dialog的分类有哪些？
3. Dialog的使用


### Dialog是啥？

> 对话框

### Dialog的分类有哪些？

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161215194624.png)

### Dialog的使用

AlertDialog：

	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("title")
			.setIcon(android.R.drawble.btn_dialog)
			.setMessage("message")
			.setPositiveButton("确定",listener)
			.setNegativiButton("取消",null);
	
	AlerDialog dialog = builder.create();
	dialog.show();

方法：

- dialog.isShowing();


## 第11讲_06_CustomDialog


自定义Dialog：

1. 一种是使用布局
2. 二是继承Dialog

方法一：

AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setCustomTitle(customTitleView);//自定义头布局
builder.setView(layoutResId);//设置Dialog中间的布局，可以是通过布局填充器生成的View



shape的使用


## 第11讲_07_ListDialog

ListDialog：


	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("title")
			.setIcon(android.R.drawble.btn_dialog)
			.setMessage("message")
			.setPositiveButton("确定",listener)
			.setNegativiButton("取消",null);
	builder.setSingleChoiceItems(R.array.font_names,checkedItem,listener)//设置单选 setMultiChoiceItem设置多选,需要手动写消失
	
	AlerDialog dialog = builder.create();
	dialog.show();


int[] fontSize = getResources().getIntArray(R.array.font_size);