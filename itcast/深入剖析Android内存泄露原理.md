
# Android 内存泄露分析

---

## 1. 什么是内存泄露

OOM：outOfMemery dvm只有10M，如加载大图片，堆内存空间。

## 2. JVM垃圾回收机制和算法

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226154054.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226155729.png)

## 3. 常见的内存泄露场景

* 非静态内部类的错误使用

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226160528.png)

> 内部类对象对外部类对象有一个隐式的强引用

> 解决方案：不要这样使用线程，可以使用线程池，或在在Activity结束的时候，把Thread的任务给结束掉。

Java中的四种引用类型

1. 强引用 User u = new User();显示的强引用，强可及对象，GC是不会回收的。
2. 软引用 SoftReference srf = new SoftReference(u); 软可及，当内存不足的时候GC
3. 弱引用
4. 虚引用


## 4. LeakCanary的使用

> https://github.com/square/leakcanary


* In your build.gradle:

		dependencies {
		   debugCompile 'com.squareup.leakcanary:leakcanary-android:1.5'
		   releaseCompile 'com.squareup.leakcanary:leakcanary-android-no-op:1.5'
		   testCompile 'com.squareup.leakcanary:leakcanary-android-no-op:1.5'
		 }

* In your Application class:

		public class ExampleApplication extends Application {
		
		  @Override public void onCreate() {
		    super.onCreate();
		    if (LeakCanary.isInAnalyzerProcess(this)) {
		      // This process is dedicated to LeakCanary for heap analysis.
		      // You should not init your app in this process.
		      return;
		    }
		    LeakCanary.install(this);
		    // Normal app init code...
		  }
		}

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226163353.png)





### 案例二



	public class UserUtils{
	
		private static InnerClassActivity.User sUser;
	
		public static void setUser(InnerClassActivity.User user){
			sUser = user;
		}
	
	}
	
	class InnerClassActivity ...{
		onCreate(){
		
			UserUtils.setUser(new User());
		}
	
		class User{
		
		}
	}

解决方案：给User类加上static


	static class User{
		
	}



### 案例三

* Handler的错误使用

code:

Handler mHandler = new Handler();

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226165103.png)


内存泄露到75k，已经算是很大了的。

解决方案：

	onDestory(){
		mHanlder.removeCallbacksAndMessages(null);//移除当前handler发送所有的msg和handler
	}


### 案例四

> 案例：单例的Toast导致Activity内存泄露


	public class UIUtils{
		private static Toast sToast;
	
		public void showToast(Context context,String msg){
			if(sToast==null){
				sToast = Toast.makeTest(context,msg,1);
			}
			sToast.setText(msg).show();
		}
	}



	MainActivity...{
	
	
		show(){
			UIUtils.showToast(this,getTime());
		}
		
	
	}


> 已经造成了对Activity的内存泄露

解决方案：

	public class UIUtils{
		private static Toast sToast;
	
		public void showToast(Context context,String msg){
			if(sToast==null){
				sToast = Toast.makeTest(context.getApplicationContext(),msg,1);
			}
			sToast.setText(msg).show();
		}
	}

## Context介绍

> 字节码一旦被加载了，一般就不会被移除了。加载字节码是类加载器工作。

系统类加载器和自定义加载器（class myClassLoader extends...

如果是系统加载器加载的字节码文件，那么一般都不会被移除的，如果是被自定义加载器加载进去的，那么当我们自定义加载器被回收的时候，那么字节码才会被移除。



* Android上下文解析

> https://possiblemobile.com/2013/06/context/



## 使用LeakCanary检测复杂项目的泄露请情况

检测已有项目内存泄露情况

环信+LeadCloud

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226173816.png)

解决：

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161226174045.png)


view置为null，adapter置为null

