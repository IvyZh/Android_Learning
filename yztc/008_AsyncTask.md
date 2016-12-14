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

主要内容

1. 什么是AsyncTask？
2. AsyncTask的使用


### 什么是AsyncTask？

> Android提供了一个叫做AsyncTask的类，专门用于完成非UI线程更新UI的任务，AsyncTask是个抽象类

### AsyncTask的使用

1. 首先子类化AsyncTask
2. 重写响应方法
3. 在UI线程中启动AsyncTask


> 演示点击按钮下载图片




AsyncTask类的三个泛型：

1. params：表示当前的AsyncTask操作时需要的参数类型
2. progress：表示当前AsyncTask耗时操作的进度类型
3. Result：表示当前AsyncTask耗时操作结果的数据类型


code:

	class MyAsyncTask extends AsyncTask<String ,Void ,byte[]>{
		//运行在UI线程中，可以做初始化操作
		protected void onPreExecute(){
			
		}
	
		// 当onPreExecute执行完毕之后立即执行，该方法运行在工作线程中，主要执行耗时操作
		// 可变参数类型和类中泛型第一个参数类型一致
		// 返回值与类中泛型第三个参数一致
		protected byte[] doInBackground(String... params){
			byte[] image = null;
			ByteArrayOutStream baos = new ByteArrayOutputStream();
			URL url = new URL(params[0]);
			HttpURLConnection conn = (HttpURLConnection)url.openConnection();
			conn.setDoInput(true);	
			conn.setRequestMethod("GET");
			conn.connect();
			int code = conn.getResponseCode();
			if(code ==200){
				InputStream is = conn.getInputStream();
				byte[] data = new byte[1024];
				int tem= = 0;
				while((temp=is.read(data))!=-1){
					baos.write(data,0,temp);
				}
			}
			image = baos.toByteArray();
			return image;
			
		}
	
		// 当doInBackground()方法执行完毕结束之后，讲耗时操作的结果返回给该方法，该方法复制将数据结果展示到ui界面
		protected void onPostExecute(byte[] result){
			if(result!=null&&result.length!=0){
				Bitmap bitmap = BitmapFactory.decodeByteArray(result,0,result.length);
				iv.setImageBitmap(bitmap);
			}
		}
	
	}


启动任务：

	new MyAsyncTask().excute(imageUrl);

网络权限：
	
	INTERNET

## 第08讲_03_AsyncTask显示进度

主要内容：

1. AsyncTask显示进度的使用
2. AsyncTask的取消


### AsyncTask显示进度的使用

publishProgress + onProgressUpdate


code:

	class MyAsyncTask extends AsyncTask<String ,Integer ,byte[]>{
		private Progress pd;
		//运行在UI线程中，可以做初始化操作
		protected void onPreExecute(){
			pd = new ProgressDialog(MainActivty.this);
			pd.setTitle("下载进度");
			pd.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
			pd.show();
		}
	
		// 当onPreExecute执行完毕之后立即执行，该方法运行在工作线程中，主要执行耗时操作
		// 可变参数类型和类中泛型第一个参数类型一致
		// 返回值与类中泛型第三个参数一致
		protected byte[] doInBackground(String... params){
			byte[] image = null;
			ByteArrayOutStream baos = new ByteArrayOutputStream();
			URL url = new URL(params[0]);
			HttpURLConnection conn = (HttpURLConnection)url.openConnection();
			conn.setDoInput(true);	
			conn.setRequestMethod("GET");
			conn.connect();
			int code = conn.getResponseCode();
			if(code ==200){
				InputStream is = conn.getInputStream();
				long total = conn.getContentLength();
				long currentLength = 0;
				byte[] data = new byte[1024];
				int tem= = 0;
				while((temp=is.read(data))!=-1){
					currentLength+=temp;
					int progress = (int)(currentLength/(float)total*100);
					publishProgress(progess);
					baos.write(data,0,temp);
					baos.flush();
				}
			}
			image = baos.toByteArray();
			return image;
			
		}
		
		// 表示允许在主线程中用来更新进度的回调方法
		// 如果doInbackground()方法中调用publicProgress()方法想主线程发布进度，由该方法获取进度后更新ui界面
		protected void onProgressUpdata(Integer...values){
			pd.setProgress(values[0]);
		}
	
		// 当doInBackground()方法执行完毕结束之后，讲耗时操作的结果返回给该方法，该方法复制将数据结果展示到ui界面
		protected void onPostExecute(byte[] result){
			if(result!=null&&result.length!=0){
				Bitmap bitmap = BitmapFactory.decodeByteArray(result,0,result.length);
				iv.setImageBitmap(bitmap);
			}
		}
	
	}


## 第08讲_04_AsyncTask的取消


### AsyncTask的取消

1. 如果AsyncTask已经执行完毕不能被取消
2. 如果AsyncTask调用cancel()取消
3. 如果AsyncTask已经启动并且正在运行 取消会中断操作



pd.setButton(ProgressDialog.BUTTON_NEGATIVE,"cancel",listener)


AsyncTask

- cancel(boolean)
- onCancelled()：表示UI线程调用cancel方法取消异步任务成功回调的方法.不会在执行onPostExecut方法
- isCancelled()