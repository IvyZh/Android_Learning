## 第06讲_01_初识Activity

主要内容：

1. Activity是什么？
2. Activity有什么作用？
3. Activity的创建
4. 如何启动Activity？

### Activity是什么？

> 一个门面

### Activity有什么作用

用户和应用程序交互的接口

摆放各种控件的容器


### Activity的创建

1. 继承Activity
2. 重写onCreate()方法：是个回调方法，系统会自动执行，不需要我们来手动调用，是一个生命周期方法，表示当Activity被创建时回调的方法，又系统架构调用，Bundle：存放String字符串的Map集合。
3. 提供xml布局文件：需要再onCreate()方法中调用setContentView方法加载布局文件
4. 在清单文件中注册

清单文件中activity标签的属性

- name:需要配置包名.类名
- label：表示应用程序列表中程序图标瞎放的文字
- icon:表示应用程序的图标


### 如何启动Activity？

* Intent 意图


Intent intent= new Intent(Context,class);
startActivty(intent);

## 第06讲_02_Activity的生命周期（一）

主要内容：

1. 什么是生命周期？
2. 研究Activity生命周期有什么作用？
3. Activity生命周期执行顺序
4. 横竖屏切换时生命周期变化


### 什么是生命周期？

> Activity从创建 运行 销亡的整个过程。


### 研究Activity生命周期有什么作用？


> 可以在Activity不同的生命周期中执行对应的逻辑代码，使Activity发挥最好的效果，提升用户体验。


### Activity生命周期执行顺序

![](http://hi.csdn.net/attachment/201109/1/0_1314838777He6C.gif)



	-- 启动程序 --
	onCreate：表示Activity创建的时候被调用
	onStart：表示Activity被用户看到时被调用
	onResume：表示Activity获取用户焦点时 能与用户交互时 被调用
	
	-- 按下Home键 --
	onPause：表示失去焦点时被调用。数据的保存可以放在这里
	onStop：Activity不可见时被调用，Activity被完全遮挡的时候被调用

	-- 重新按下启动图标 -- 
	onReStart:表示Activity处于停止时在进入时调用
	onStart
	onResume

	-- 按下回退键，退出Activity --
	onPause
	onStop
	onDestory:表示Activity被销毁时被调用
	
Activity设置Dialog主题之后的生命周期




## 第06讲_03_Activity的生命周期（二）

Activity设置Dialog主题之后的生命周期

	onPause-->onResume

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161209135115.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161209135441.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161209135515.png)


### 横竖屏切换时生命周期变化

> 默认情况下Activity会关闭并且重新启动。

- android:screenOritentation="landscape"（横屏） portrait（竖屏）

- 设置android:configChanges属性:表示横竖屏切换不会调用生命周期
	- orientation
	- keyboardHidden
	- screenSize


## 第06讲_04_Activity传值（一）

主要内容：

1. Activity之间通过Intent传值
2. Activity之间通过Bundle传值
3. 使用Application全局对象传值
4. 启动Activity回传数据

### Activity之间通过Intent传值

> key-value形式传值

存：

	Intent intent = new Intent();
	intent.putExtra(kay,value);//String char int boolen double float
	startActivity(intent);

取：

	// 获取激活组件的intent对象
	Intent intent = getIntent();
	intent.getStringExtra(key);/getIntExtra(key,default);...



### Activity之间通过Bundle传值

> 其实底层就是Map传输数据


传输：

1. 新建一个Bundle类
2. Bundle类中key-value对的形式存储数据
3. 创建Intent对象，将Bundle存入Intent对象

接受：

1. 获取激活Intent对象
2. 获取传递Bundle对象
3. 根据Bundle中的key去除指定的value值

代码：

	Bundle bundle = new Bundle();
	bundle.putString(key,value);//...
	intent.putExtras(bundle);

	String value = getIntent().getBundle().getString("key");


## 第06讲_05_Activity传值（二）

### 使用Application全局对象传值

需求：C中要得到A中的数据

	A--->B--->C


使用Application存取。


	public void click(View v){
		MyApplication application = (MyApplication)getApplication();
		application.setName("zhangsan");
	}

	MyApplication application = (MyApplication)getApplication();
	application.getName();



### 启动Activity回传数据


	startActivityForResult(intent,CODE);
	
	setResult(Activity.RESULT_OK,intent);
	finish();


	onActivityResult(int requestCode,int resultCode,Intent data){
		if(requestCode==CODE&&resultCode==Activity.RESULT_OK){
		
		}
	
	}