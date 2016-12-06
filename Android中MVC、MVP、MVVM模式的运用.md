
## 浅谈MVC MVP MVVM模式

> 技能

- 设计模式
- 框架
- MVC 
- MVX（MVP、MVVM）



> 来源:itcast公开课

# 1、开篇
### 案例

* 用户登录案例，如何拆分代码使结构更加的合理。

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201152004.png)


# 2、MVC项目改造
### 分析、思路

* 登陆逻辑分析[流程]
	* 用户登陆界面展示
	* 用户输入
	* 按钮点击
	* 判断用户输入合法性
	* 显示滚动条
	* 一系列耗时操作
	* 隐藏滚动条
	* 提示用户的信息Toast

### 代码实现

- 判断用户输入合法性(是用了一个业务Bean来实现的

	public boolean checkUserInfo(User user){
	
	}

- 显示进度条
	- new ProgessBar(this)
- 开子线程，睡几秒
	- SystemClock.sleep(3000);


简单回顾下代码结构,现在所有的代码都写在了MainActivity里面了。

0：未经过任何处理的代码MainActivity.java

包结构：

	com.xx.bean
		- User
	com.xx.activity
		- MainActivity

MainActivity Code:

	public void login(View v){
		String userName = e1.getText().toString().trim();
		String pwd = e2.getText().toString().trim();
		if(checkUserInfo(new User(userName,pwd))){
			dialog.show();

			new Thread(new Runnable(){
					SystemClock.sleep(3000);
					if("ivy".equeals(userName) && "123".equeals(pwd) ){
						RunOnUIThread(new Runnable(){
							dialog.dismiss();
							Toast.show("登陆成功");
						});
					}else{
						RunOnUIThread(new Runnable(){
							dialog.dismiss();
							Toast.show("用户名或密码错误");
						});
					}
					
				});
			}).start();
			
		}else{
			Toast.show("用户名或密码输入不合法");
		}
	
	}
	
	public void boolean checkUserInfo(User u){// 合法性判断
		boolean flag;	
		//...非空判断
		return flag;
	}


> 上面的的逻辑没有按照任何模式来做，简单来说在Activity里面存放了M和C的事情，V对应于Layout（XML布局，这个没什么好说的，基本固定不变）。接下来做MVC优化就是讲Model（数据库或网络等耗时操作）抽出来作为UserLoginNet一层。


### 按照MVC模式拆分

界面   ----> V

控制层 ----> C

模型   ----> M

> 简单理解下，种草莓M，然后交给商贩C，最终卖给客户V。数据是一层一层像上面传递。


界面   ----> V ====> Layout

控制层 ----> C ====> Activity

模型   ----> M ====> 数据库、网络....




> 包结构：

	com.xx.bean
		- User
	com.xx.activity
		- MainActivity
	com.xx.net
		- UserLoginNet


UserLoginNet.java(模拟了下

	class UserLoginNet {
		public void sendUserLoginInfo(User u){
			SystemClock.sleep(3000);
			if("ivy".equeals(u.getUserName) && "123".equeals(u.getPwd())){
				return true;
			}else{
				return false;
			}
		}
	}


MainActivity.java 就变成了

	public void login(View v){
		String userName = e1.getText().toString().trim();
		String pwd = e2.getText().toString().trim();
		User u = new User(userName,pwd);
		if(checkUserInfo(u)){
			dialog.show();

			new Thread(new Runnable(){
					
					UserLoginNet net = new UserLoginNet();
					if(net.sendUserLoginInfo(u)){
						RunOnUIThread(new Runnable(){
							dialog.dismiss();
							Toast.show("登陆成功");
						});
					}else{
						RunOnUIThread(new Runnable(){
							dialog.dismiss();
							Toast.show("用户名或密码错误");
						});
					}
					
				});
			}).start();
			
		}else{
			Toast.show("用户名或密码输入不合法");
		}
	
	}
	
	public void boolean checkUserInfo(User u){// 合法性判断
		boolean flag;	
		//...非空判断
		return flag;
	}


---

以上就是MVC改造的，不过还是有些问题


存在的问题：

1. 业务相关的
2. 界面相关的

如果业务很复杂了，这个Activity会很大；如果界面复杂了，这个Activity也会很大


界面   ----> V ====> Layout----->XML

控制层 ----> C ====> Activity--->**业务+界面**

模型   ----> M ====> 数据库、网络....----->UserLoginNet


> 就会造成这个V就一个Layout的xml布局文件，相对较少，而这个Activity界面C就会越来越庞大。


看Activity的源码，发现setContenView和findViewById都是Window来实现的，封装。

	getWindow().xxxx


解决方案：

1. 如果将Activity中的业务部分拆分-----> MVP
2. 如果将Activity中的界面部分拆分-----> MVVM



# 3、MVP项目改造（将Activity中的业务部分拆分）

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201165944.png)


MVC的代码Copy一份，进行MVP改造。


> 思路就是把和界面相关的都留在Activity里面，然后将业务相关的就抽取到P中（UserLoginPresenter）。

包结构：

	com.xx.bean
		- User
	com.xx.activity
		- MainActivity
	com.xx.net
		- UserLoginNet
	com.xx.presenter
		- UserLoginPresenter



分类：


- 界面(MainActivity
	- findViewById
	- etPwd.getText().toString().trim();
	- User u = new User(xx,xx)
	- success()
	- failed()

- 业务(UserLoginPresenter
	- checkUserInfo(User u)
	- login(User u)
	- 构造函数将MainActivity的View层传递过来,方便如下调用
		- UserLoginPresenter(MainActivity view)
		- view.success();
		- veiw.failed();

作为View可以是MainActivity也可以是Fragment，所以为了通用性，这里的思路是：放置参数为通用（抽象类或接口，实际开发中**接口**更通用）



包结构：

	com.xx.bean
		- User
	com.xx.activity
		- MainActivity
	com.xx.net
		- UserLoginNet
	com.xx.presenter
		- UserLoginPresenter
		- **IUserLoginView**



IUserLoginView.java（作为接口，一定要把注释写完整

	public interface IUserLoginView{
		void success();//登陆成功
		void failed();//登陆失败
	}

然后MainActivity实现IUserLoginView接口就可以了。

到这里，一个简单的MVP就实现了，耦合度就变低了。


M---> 网络 数据库---UserLoginNet

V---> Layout----->XML

P---> UserLoginPresenter


# 4、DataBingding使用

MVVM

- Model：代表你的基本业务逻辑（数据库、网络UserLoginNet
- View：显示内容（Layout XML
- ViewModel：将前面两者联系起来

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201174808.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201175351.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201175438.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201175833.png)


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161201180419.png)

notify();
两种方式，参考Google data-binding/guide.html



> M  <------>  V


到目前为止，M层数据改变了，V会自动跟着改变，不用考虑子线程的问题。

那么，如果V改变了，怎么影响到M呢？

比如登陆的Demo。

点击登陆按钮，要获取EditText里面的内容，该如何操作呢？

> user.username.get() 是不可以的。



EditText.addTextChangedListener


步骤比较复杂。直接看**代码**。


# 5、MVVM项目改造



