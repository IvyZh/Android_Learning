![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.24
老师:Ricky


### Toolbar


	导航---顶部导航
	以前：谷歌干脆规范了顶部导航---ActionBar（3.0API，也有兼容包）
	后来：ActionBar开发起来很蛋疼（1.用来比较费劲；2.扩展性太差 太死板）
		大多数人都会使用一个民间的ActonBar，叫SherlockActionBar。
		谷歌就重新定义了一个Toolbar。现在又有个MaterialDesign的APPBar
	
	作用：导航控件---显示标题、导航back、快捷操作、菜单等。而且Toolbar不一定要放在顶部，也可以放底部。
	
	android.support.v7.widget.Toolbar
	
	使用：
		1.引入support-v7包
		2.修改主题：    <style name="AppBaseTheme" parent="Theme.AppCompat.Light.NoActionBar">
			注意主题一定要使用：NoActionBar
		3.写布局，把Toolbar当做一个普通的容器使用。
		4.Activity--->AppcompatActivity
		5.使用Toolbar替换ActionBar
		setSupportActionBar(toolbar);
	
	Toolbar属性：
		android:background="?attr/colorPrimary" 设置背景颜色，使用系统属性colorPrimary主色调。--在主题里面设置了。
	
	
	让标题居中显示在toobar
	    <android.support.v7.widget.Toolbar
	        android:id="@+id/toolbar"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:background="?attr/colorPrimary"
	        app:title="网易新闻"
	        >
			<TextView 
			    android:layout_width="wrap_content"
	        	android:layout_height="wrap_content"
	        	android:layout_gravity="center"//重点
	        	android:text="textview"
	        	/>
	        
	    </android.support.v7.widget.Toolbar>
	
	//设置NavigationIcon的点击事件监听，比如返回按钮。
	// app:navigationIcon="@drawable/abc_ic_ab_back_mtrl_am_alpha"
	toolbar.setNavigationOnClickListener(new OnClickListener() {
		
		@Override
		public void onClick(View v) {
			finish();
		}
	});
	
	//将弹出的菜单泡泡窗体修改成黑底白字Dark；Light白底黑字
	app:popupTheme="@style/ThemeOverlay.AppCompat.Dark"

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303160739.png)

演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303161419.png)

并不是我们想要的效果。

因为我们要使用Appcompat.Light.NoActionBar,同时Activity--->AppcompatActivity，setSupportActionBar(toolbar);

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303161555.png)


Toolbar属性：
android:background="?attr/colorPrimary" 设置背景颜色，使用系统属性colorPrimary主色调。--在主题里面设置了。

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303161901.png)

运行效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303162108.png)


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303162623.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303162649.png)

	//将弹出的菜单泡泡窗体修改成黑底白字Dark；Light白底黑字
	app:popupTheme="@style/ThemeOverlay.AppCompat.Dark"


end.