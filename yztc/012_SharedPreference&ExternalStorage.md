> Android的数据存储

## 第12讲_01_SharedPreference

主要内容：

1. 存储方式有哪些？
2. 不同存储方式使用场景
3. 不同存储方式的用法


### 存储方式有哪些？

1. SharePreference：共享参数，XML文件
2. 内部存储：
3. 外部存储：
4. 数据库存储：
5. 网络存储：


### 不同存储方式使用场景

1. SharePreference：简单的信息，非敏感的信息，不能存放文件
2. 内部存储：保存在app内部空间，非公开私有数据，可以存放文件
3. 外部存储：公开空间，可以存放文件
4. 数据库存储：结构化数据
5. 网络存储：云


### 不同存储方式的用法


	SharedPreferences sp = getSharedPreferences("configs",MODE_PRIVATE);//本质上就是一个map结构的xml文件
	
	Editor editor = sp.edit();
	
	editor.putString(key,value);//boolean int long float
	
	boolean commit = editor.commit();//提交保存
	
	if(commit){
		showToast("success");
	}
	
	String value = sp.getString(key);


存储位置： data/data/包名/shared_prefs/configs.xml


## 第12讲_02_内部存储

background：@android:drawable/editbox_background


	FileOutStream fos = openFileOutput(name,MODE_PRIVATE);//不需要添加任何权限，该文件是与当前上下文所在的包有关的
	fos.write(str.getBytes());
	fos.close();
	
	FileInputStream fis = openFileInputStream(name);
	byte[] buffer = new buffer[fis.available()];
	fis.read(buffer);
	fis.close();

- boolean b = deleteFile(fileName);//删除当前上下文中指定名称的文件


文件保存位置：data/data/包名/files/fileName

特点：内部存储的东西会随着app的卸载而被清掉。

## 第12讲_03_ExternalStorage

	public calss IOUtils{
	
		// 外部存储路径
		public static final String STORE_PATH = Environment.getExternalStorageDirectory()+File.separator+"Ivy"+File.separator+"images";
		
		// 判断sdcard是否挂载
		public static void isMounted(){
			return Environment.getExternalStorageState().equeals(Environment.MEDIA_MOUNTED);
		}
	
		// 保存图片
		public static boolean saveImg(String fileName,byte[] data){
			if(!isMounted()){
				return false;
			}
			
			File dir = new File(STORE_PATH);
			if(!dir.exists()){
				dir.mkdirs();
			}
	
			
			try{
				FileOutputStream fos = new FileOutputStream(new File(dir,fileName));
				fos.write(data);
				fos.close();
	
				return true;
			}catch(IOException e){
				return false;
			}
			
		}
		
		// 读取图片
		public static Bitmap readImg(String fileName){
			if(!isMounted()){
				return null;
			}	
			
			File imgFile = new File(STORE_PATH,fileName);
			if(imgFile.exist()){
				return BitmapFactory.decodeFile(imgFile.getAbsolutePath());
			}
			return null;
		}
	
	}


调用：

	Bitmap bitmap = BitmapFactory.decodeResource(getResources(),R.drawable.dog);
	
	ByteArrayOutputStream baos = new ByteArrayOutputStream();
	bitmap.compress(CompressFormat.JPEG,100,boas);//将图片压缩，会将图片的信息保存在baos中
	boolean isSaveSuccess = IOUtils.saveImg("dog.jpg",baos.toByteArray());
	
	if(isSaveSuccess){
		
	}

	baos.close();


权限：