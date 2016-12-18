## 第14讲_01_CallLog

主要内如：
1. ContentProvider的原理
2. ContentResolver实现对系统数据的操作
3. 自定义ContentProvider


### ContentProvider的原理

不同的应用之间。

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161217165852.png)


### ContentResolver实现对系统数据的操作

1. ContentResolver 实现系统数据的操作（联系人查询、媒体库文件、通话记录、短信记录）


通话记录的获取，
	
	ContentResolver resolver = getContentResolver();// 内容解析者，可以增删改查
	
	
	Cursor cursor = resolver.query(uri,projection,selection,selectionArgs,sortOrder);//Uri：统一资源标识符 url：统一资源定位符
	
	
	查询通话记录的uri ： `content://call_log/calls`  Uri.parse(uri);
	
	projection : 查询的列  
	
	projection = new String[]{CallLog.Calls._ID,CallLog.Calls.NUMBER,CallLog.Calls.DATE,CallLog.Calls.TYPE};

需要加上读取通话日志的权限 如果修改的话 还要加上写权限。


## 第14讲_02_Sms查询

sms_uri = "content://sms";


	class MyAdapter extends CursorAdapter {
	
		// 创建一个视图---> 引入ListView中要显示的子视图
		public View newView(Context context,Cursor cursor,ViewGroup parent){
		
			return getLayoutInflater().inflate(resId,null);
		}
	
		// 绑定数据的方法
		public void bindView(View view,Context context,Cursor cursor){
	
	
			String number = cursor.getString(cursor.getColumnIndex("address"));// body type
		}
	
	
	}
	
	cursor.close();// 查询完毕之后 记得关闭 放在Activity销毁的时候  onDestory()

注意加上权限


## 第14讲_03_自定义内容提供者


想把自己应用中的数据库内容暴露给别人使用。可以是数据库文件、可以是文件、也可以是SharedPreference


ContentProvider是四大组件之一，需要再menifest文件中注册。

	
	public class CustomProvider extends ContentProvider{
	
		// 创建URI
		private static UriMatcher sMatcher = new UriMatcher(UriMatcher.NO_MATCH);
	
		static{
			sMatcher.addURI("yiyige","person",1);// 主机名 表名 code
			...
			sMatcher.addURI("yiyige","person/#",2);//# 代表任意的数字
			sMatcher.addURI("yiyige","person/filter/*",3);// * 代表任意字符
		}
		
		
		
		onCreate(){
			helper = new DbHelper(getContex());
			db = helper.getWirtableDatabase();
			return true;
		}
			
		getType()
	
		query()
	
		insert(Uri uri){
			int match =	sMatcher.match(uri);
			switch(match){
				// ...
				long insert = db.insert(...);
				return ContentUris.with(uri,insert);// 将原有的uri和id进行拼接，从而形成一个新的uri
				
			}
			return null;
		}
		
		delete()
	
		update()
	
	}
	
	
	int parseId = ContentUris.parseId(result);// 将uri和id拆分开

CustomeProvider 在manifest文件注册的时候 需要加上这个属性： exported=true 意思是允许其他应用对这个数据库进行操作。

