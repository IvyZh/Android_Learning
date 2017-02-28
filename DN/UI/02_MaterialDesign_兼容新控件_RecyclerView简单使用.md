![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.03
老师:Ricky


### 回顾

	版本：1.compileSDK 编译版本；
		2.minSDK 兼容到最低版本是多少
		3.targetSDK;

1.自动导入的appcompat-v7项目自身就是报错的，什么原因？
	build的版本太低了,要么是SDK很新但是兼容包没有更新。
	还有的有其他的原因：1.没有将依赖的项目作为library，而且也没有将自己的项目加入该依赖项目。

2.multiple dex files。。。。appcompat/res/com.android.v7.R$anim 
有文件冲突--一般是代表jar包冲突。
如何解决？删掉重复的jar 


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170227230943.png)

> 关于Eclipse项目如何导入到AndroidStudio。百度。

	1.直接导入没问题；
	2.有问题，导出项目的时候应该选择gradle模式导出, 再导入到as。（这种情况下都有可能还是报错，可能是gradle版本太低了 需要升级！）
	3.直接在as里面建个项目，然后把所有的资源和代码拷贝过去 就欧了！！


为什么要用appcompat项目，因为里面是谷歌精心准备的---解决android碎片化开发蛋疼的问题，让我们app编译出来在各种高低版本之间、不同的厂商生产的ROM之间显示出来的效果UI控件等有一较一致的体验。

> SDK更新的历史上几个特别重要的版本：14（4.0）、19（4.4）、21（5.0）


修改针对5.0系统的显示样式，修改values-v21文件夹下面的xml文件

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170227232333.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170227232756.png)


	 <!-- 设置虚拟导航栏背景颜色 5.x的新特性 -->
    <item name="android:navigationBarColor">@color/colorPrimary_pink</item>

4.4版本对比

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170227233449.png)


### MaterialDesign兼容性控件的使用

> 尤其是在appcompat-V7里面有很多为兼容而生的控件
> 
> 这样就可以做到高低版本和不同的ROM之间体验一致！还可以配合appcompat的主题使用达到体验一致性

- android.support.v7.app.AlertDialog

先用原生的AlertDialog演示：

6.x模拟器和4.x模拟器效果对比：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228101741.png)

使用v7下面的AlertDialog演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228101911.png)

保证按钮在4.x模拟器显示效果也是一样，可以使用v7下面的appcompatbutton

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228102122.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228102234.png)

看下其他控件效果：

- EditText:AppCompatEditText

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228104122.png)

- 原生的 CheckBox RadioButton ProgresBar 在4.x和6.x模拟器上演示效果展示：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228104502.png)

进度条样式设置使用 style="@style/Widget.AppCompat.ProgressBar.Horizontal"


- 在v4下面有个SwipeRefreshLayout下拉刷新

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228104923.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228105213.png)

在SwipeRefreshLayout内部再套一个ScrollerView，演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228105615.png)

- 在v7包下面有一个ListPopupWindow：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228110125.png)

4.x演示效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228110140.png)

- PopupMenu


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228130502.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228130544.png)

- android.support.v7.widget.LinearLayoutCompat 
	- 给包裹在里面的所有子控件添加间隔线


	        <android.support.v7.widget.LinearLayoutCompat
	            android:layout_width="match_parent"
	            android:layout_height="match_parent"
	            app:divider="@drawable/abc_list_divider_mtrl_alpha"
	            app:showDividers="beginning|middle"
	            android:orientation="vertical" >

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228131004.png)
> 看LinearLayoutCompat源码

### V7 RecyclerView

	特点：
	1.谷歌在高级版本提出一个新的替代ListView、GridView的控件。
	2.高度解耦。
	3.自带了性能优化。ViewHolder。
	软件：低耦合高内聚。
	
	RecyclerView没有条目点击事件，需要自己写。

使用eclipse的话，需要引入RecyclerView包

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228132236.png)

设置Adapter

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228133259.png)

设置LayoutManager



![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228133617.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228134258.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170228134347.png)

end.

