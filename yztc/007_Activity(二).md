## 第07讲_01_Task、Back Stack

主要内容：

1. 什么是Task？
2. 什么是Back Stack？


### 什么是Task？

> Task就是用户为了执行特定工作而与之交互的activity的集合

### 什么是Back Stack？

发生短信的意图：

	Intent intent = new Intent(Intent.ACTION_SENDTO,Uri.parse("sms://10086"));
	startActivity(intent);


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210103242.png)

## 第07讲_02_Activity的启动模式

主要内容：

1. 什么是启动模式？
2. 启动模式有什么作用？
3. Activity的启动模式


### 什么是启动模式？

> Activity启动时的策略

AndroidManifest.xml中标签的android:launchMode属性设置


### 启动模式有什么作用？

> 可以更好的根据用户需求在Back Stack中管理Activity 提高用户体验


## Activity的启动模式

* Standard
* SingleTop：顶部唯一模式 应用场景：浏览器书签
* SingleTask：站内唯一模式，应用场景：回到主页面的时候，如浏览器主页面
* SingleInstance：来电话

> Standard标准模式 默认模式 Activity会根据启动顺序压入Back Stack

除了在布局文件中设置启动模式外，还可以用java代码flag来实现，后面会讲。


## 第07讲_03_Intent的属性（一）

主要内容：

1. 什么是Intent？
2. Intent有什么作用？
3. Intent的七大属性

### 什么是Intent？

> 组件之间的消息传递，运行时绑定

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210112616.png)


### Intent有什么作用？

> 1. 用来激活其他应用程序组件

> 2. 作为传递数据和事件的桥梁



### Intent的七大属性

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210112909.png)

* ComponentName：组件名称，对目标组件的一个描述，是一个类类型的对象。
![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210113151.png)
* Action：普通字符串，表示Intent要执行动作的表示，如拨打电话、发送短信，也可以使用自定义形式，一个Intent只能设置一个Action
	* setAction()
	* getAction()
* Data：对本次操作的数据的描述

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210113459.png)

* Type：对Data这个数据类型进一步的描述，如果Data为null的时候才有效。
* Category：对执行动作的附加信息的描述，字符串，
![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210113827.png)
* Extras：一切附加信息的操作，用于多个Action之间数据交换，通过键值对进行数据存储，如发送邮件时，可以将发送地址、内容以键值对的形式存储
* flags：标记组件如何启动以及启动之后如何对待等。设置Activity的启动模式
	* setFlag();
	* FLAG_ACTIVITY_SINGLE_TOP
	* FLAG_ACTIVITY_CLEAR_TOP：类似single task效果
	* ...


案例（演示Intent属性用法）：



- 启动Activity的几种方式

		ComponenName compontent = new ComponenName(MainActivity.this.OtherActivty.class);
		Intent intent = new Intent().setCompontent(compontent);

		Intent intent = new Intent();
		intent.setClass(MainActivity.this.OtherActivty.class);//其实它的底层也是会调用 new ComponenName(MainActivity.this.OtherActivty.class); 这个方法的

		Intent intent = new Intent();
		intent.setClassName(MainActivity.this.OtherActivty.class.getName());



- 拨打电话
		
		Intent intent = new Intent();
		intent.setAction(Intent.ACTION_CALL,Uri.parse("tel://10086"));//Uri是一个抽象类，调用静态方法。指定action操作数据。
	

## 第07讲_04_Intent的属性（二）

> 拨打电话的时候需要再Manifest里面加入权限：android.permiss.CALL_PHONE


- 发送短信

		intent.setAction(Intent.ACTION_SENDTO,Uri.parse("sms://10000")); // 打开发短信界面，没有添加权限

- 打开网页

		new Intent(Intent.ACTION_VIEW,Uri.parse("http://www..baidu.com"));

- 播放音频
		Intent intent = new Intent(Intent.ACTION_VIEW);

		intent.setDataAndType(Uri.parse("file:///"+Enviroment.getExternamStorageDirectory().getAbsolutePath()+"1.mp3"),"audio/*");
		// intent.setData(Uri.parse("file:///"+Enviroment.getExternamStorageDirectory().getAbsolutePath()+"1.mp3"));
		// intent.setType("audio/*");
		


## 第07讲_05_隐式启动

主要内容：

1. 什么是隐式Intent？
2. 隐式Intent使用场景
3. 隐式Intent的使用


### 什么是隐式Intent？

显示Intent：直接指定目标组件的ComponentName

	适合启动同一个应用中其他组件

隐式Intent：比如打电话、发短信...没有明确指定组件名Intent为隐式意图

	适合启动设备中不同应用中的组件


intent-filter

IntentFilter 描述了一个组件愿意接受什么样的Intent对象，告诉Activity可以相应什么类型的Intent。

是通过action data category匹配的。


Action：

- Intent对象只能命名一个单一的Action，一个IntentFilter可以列出多个Action
- 过滤器必须包含一个<Action>，否则它将阻止所有的Intent通过


Category：

- Intent对象包含Category都能在IntentFilter中找到
- 隐式Intent加上一个默认的"android.intent.category.DEFAULT"


Data

- scheme://host:port/path
- Intent中的URI和IntentFilter的URL比较时，只比较中实际定义的部分属性


		<intent-filter>
		
			<action android:name="com.ivy.action" />
			<category android:name="android.intent.category.DEFAULT"/>//默认就会有的
		
		</intent-filter>


		intent.setAction("com.ivy.action");
		//intent.setCategory("android.intent.category.DEFAULT"); 可以不写


---


	<intent-filter>
	
		<action android:name="com.ivy.action" />
		<category android:name="android.intent.category.DEFAULT"/>//默认就会有的
		<data android:scheme="yztc" android:host="com"/>
	</intent-filter>

	intent.setAction("com.ivy.action");
	intent.setData(Uri.parse("yztc://com"))
	
---

	<intent-filter>
	
		<action android:name="com.ivy.action" />
		<category android:name="android.intent.category.DEFAULT"/>//默认就会有的
		<data android:scheme="yztc" android:host="com"/>
		<data android:port="90"/>
		<data android:path="/res"/>// yztc://com:90/res
	</intent-filter>

---

	<intent-filter>
	
		<action android:name="com.ivy.action" />
		<category android:name="android.intent.category.DEFAULT"/>//默认就会有的
		<data android:scheme="yztc" android:host="com"/>
		<data android:port="90"/>
		<data android:path="/res"/>// yztc://com:90/res
		<data android:mimeType="text/*"/>
	</intent-filter>

	intent.setDataAndType(Uri.parse("yztc://com:90/res"),"text/*")；



> 隐式启动另一个程序中的组件

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161210152417.png)

