## 第19讲_01_Handler基本用法及原理

主要内容：

1. 什么是Handler？
2. Handler怎么用？
3. Handler原理


### 什么是Handler？

### Handler怎么用？

1. sendMessage(msg)
2. handleMessage(msg)


主线程（UI线程）+工作线程（Worker）

code:

	private Hanlder handler = new Handler(){
		
		void handleMessage(Message msg){
			switch(msg.what){
				//...
				tv.setText(msg.arg2);
			}
		}
	
	};



	public void sendMsg(View v){
	
		new Thread(){
			public void run(){
				while(count < 100){
					count++;
					Thread.sleep(500);
	
					//Message msg = new Message();
					Message msg = Message.obtain();
					msg.what = 1;// what 标记
					msg.arg1 = count;// arg2
					msg.obj = ...;
					mHandler.sendMessage(msg);
				}
			}
		}.start();
	
	}




### Handler原理

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161219180959.png)


## 第19讲_02_LooperThread


Activity内部封装了Looper（轮询器）

自定义Looper线程

	onCreate(){
		new LooperThread().start();
	}	



	class LooperThread extends Thread{
	
		publi void run(){
			Looper.prepare();//准备looper线程

			// 处理消息
			mHandler = new Handler(){
				public void handleMessage(Message msg){
					L.v(String(msg.obj));
				}
			}

			Looper.loop();//循环方法
		}
	
	} 