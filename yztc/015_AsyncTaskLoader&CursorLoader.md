## 第15讲_01_AsyncTaskLoader

主要内容：

1. 什么是Loader？
2. Loader的优点
3. Loader的分类
4. Loader的用法


### 什么是Loader？

> 推土机的英文名，高效的从数据库中查询数据


### Loader的优点

* 具有异步加载数据的能力，高效
* 拥有一个数据改变的通知机制，当数据源做出改变时会及时发出通知，自动加载数据，因此并不需要再重新进行数据的查询

### Loader的分类


1. CursorLoader
2. AyncTaskLoader

### Loader的用法

1. 实现LoaderCallbacks<Cursor> 接口
2. 初始化Loader，initLoader()
3. 创建Loader对象，onCreateLoader()
4. 结束创建，onLoadFinished()
5. 重置Loader对象，onLoaderReset()



Activity继承LoaderCallBacks接口

初始化Loader 也就是添加监听
LoaderManeger loaderManager = getLoaderManager();
loaderManager.initLoader(1,bundle,callback);// 1,null,this


	Loader<Cursor> onCreateLoader(){
		
		return new MyLoader(this);
	
	}
	
	
	onLoadFinished(){
		adapter.swapCursor(cursor);	
	}
	
	onLoaderReset(){
		adapter.swapCursor(null);
	}

	static class MyLoader extends AsyncTaskLoader<Cursor>{
	
		onStartLoading(){
			// 开始加载的时候调用方法
			forceLoad();// 强制加载
		}
		
		loadInBackground(){
			// 后台线程进行数据加载的方法---耗时操作
			
			return	resolver.query(ContactsContact.RawContacts.CONTENT_URI,new String[]{"_id","displayname"},...)
			
		}
	}

加权限


## 第15讲_02_CursorLoader


	Loader<Cursor> onCreateLoader(){
		
		new CursorLoader(this,uri,...);
	}