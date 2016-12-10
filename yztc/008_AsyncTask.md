## 第08讲_01_UI线程模型介绍

主要内容：

1. 进程和线程介绍
2. UI线程模型
3. 什么是ANR？


### 进程和线程介绍

进程：计算机正在运行的程序实例

线程：是进程中某个单一顺序的控制流

### UI线程模型

> 唯一的UI线程全权负责UI工作的线程模型，可以把它称为“UI线程模型”

> 不要阻塞UI线程到5秒以上

> 不要让UI线程职位的其他线程去访问Android的UI工具包



违法原则一：主线程阻塞

	onCreate(){
		while(true){
			count++;
			Thread.sleep(1000);//try...catch...
			tv.setText(count+"");
		}
	}


违法原则二：非UI线程不能处理UI工具包
	onCreate(){
		 new Thread(new Runnable(){
			while(true){
				count++;
				Thread.sleep(1000);
				tv.setText(count+"");//try...catch...
			}
		}).start();
	}

### 什么是ANR？

> 应用程序无响应。Application Not Responding.

## 第08讲_02_AsyncTask的基本使用
## 第08讲_03_AsyncTask显示进度
## 第08讲_04_AsyncTask的取消