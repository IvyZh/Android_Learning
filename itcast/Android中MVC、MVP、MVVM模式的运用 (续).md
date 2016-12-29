> 这篇文章主要是来展示实际开发之中自己写的Code。



Demo是用一个简单的登陆来演示的。效果图如下：

![](http://1)



## LoginDemo

包结构：

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161202110656.png)

MainActivity.Java


	public class MainActivity extends AppCompatActivity {
	
	    private EditText etUserName, etPwd;
	    private ProgressDialog dialog;
	
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	
	        etUserName = (EditText) findViewById(R.id.editText);
	        etPwd = (EditText) findViewById(R.id.editText2);
	        dialog = new ProgressDialog(this);
	    }
	
	
	    public void login(View v) {
	        final String userName = etUserName.getText().toString().trim();
	        final String pwd = etPwd.getText().toString().trim();
	        boolean isLegal = checkIsLegal(userName, pwd);//检查输入的合法性
	        if (isLegal) {
	            dialog.show();
	            new Thread(new Runnable() {
	                @Override
	                public void run() {
	                    SystemClock.sleep(3000);
	                    if ("Ivy".equals(userName) && "123".equals(pwd)) {
	                        runOnUiThread(new Runnable() {
	                            @Override
	                            public void run() {
	                                dialog.dismiss();
	                                Toast.makeText(MainActivity.this, "登陆成功：" + userName, Toast.LENGTH_LONG).show();
	
	                            }
	                        });
	                    } else {
	                        runOnUiThread(new Runnable() {
	                            @Override
	                            public void run() {
	                                dialog.dismiss();
	                                Toast.makeText(MainActivity.this, "用户名或密码失败", Toast.LENGTH_LONG).show();
	                            }
	                        });
	                    }
	                }
	            }).start();
	        } else {
	            Toast.makeText(this, "用户名或密码不能为空", Toast.LENGTH_LONG).show();
	        }
	    }
	
	    private boolean checkIsLegal(String name, String pwd) {
	        return !TextUtils.isEmpty(name) && !TextUtils.isEmpty(pwd);//简单的判断非空判断
	    }
	}


## LoginDemo_MVC


MVC包结构：

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161202111930.png)

MainActivity.Java

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161202112049.png)

这里新增了User的业务Bean，是为了将MainActivity中用户信息进行封装，然后传递给M层即UserLoginNet这个类。

UserLoginNet.java

	public class UserLoginNet {
	
	    public boolean sendUserLogin(User user) {
	        SystemClock.sleep(3000);
	        if ("Ivy".equals(user.getUserName()) && "123".equals(user.getPwd())) {
	            return true;
	        } else {
	            return false;
	        }
	    }
	}


> 发现MVC的代码减少量还是很少，在MainActivity这个类中依然夹杂着业务层和界面层信息。


## LoginDemo_MVP

> 如果将MainActivity这个类的业务层抽取出来就是MVP模式了。


MVP包结构：

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161202114840.png)


MainActivity.Java

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/QQ%E6%88%AA%E5%9B%BE20161202115023.png)


Model层不用改变，新增了UserLoginPresenter。


	public class UserLoginPresenter {
	    private IUserLoginView view;
	
	    public UserLoginPresenter(IUserLoginView view) {
	        //作为View可以是MainActivity也可以是Fragment，所以为了通用性，这里的思路是：放置参数为通用（抽象类或接口，实际开发中接口更通用）
	        this.view = view;
	    }
	
	    public boolean checkIsLegal(User user) {
	        return !TextUtils.isEmpty(user.getUserName()) && !TextUtils.isEmpty(user.getPwd());//简单的判断非空判断
	    }
	
	    public void login(final User user) {
	        new Thread(new Runnable() {
	            @Override
	            public void run() {
	                UserLoginNet net = new UserLoginNet();
	                boolean success = net.sendUserLogin(user);
	                if (success) {
	                    view.success();
	                } else {
	                    view.failed();
	                }
	            }
	        }).start();
	    }
	}

> **作为View可以是MainActivity也可以是Fragment，所以为了通用性，这里的思路是：放置参数为通用（抽象类或接口，实际开发中接口更通用）**


接口：

	public interface IUserLoginView {
	    void success();
	
	    void failed();
	}

> 作为接口，一定要把注释写清楚


Model层代码不变，还是同样的网络请求


	public class UserLoginNet {
	
	    public boolean sendUserLogin(User user) {
	        SystemClock.sleep(3000);
	        if ("Ivy".equals(user.getUserName()) && "123".equals(user.getPwd())) {
	            return true;
	        } else {
	            return false;
	        }
	    }
	}

业务Bean的代码很简单：

	public class User {
	    private String userName;
	    private String pwd;
	
	    public User(String userName, String pwd) {
	        this.userName = userName;
	        this.pwd = pwd;
	    }
	
	    public String getUserName() {
	        return userName;
	    }
	
	    public void setUserName(String userName) {
	        this.userName = userName;
	    }
	
	    public String getPwd() {
	        return pwd;
	    }
	
	    public void setPwd(String pwd) {
	        this.pwd = pwd;
	    }
	}


## LoginDemo_MVVM

详细信息请关注[官方开发者论坛](https://developer.android.com/topic/libraries/data-binding/index.html?hl=zh-cn)，里面会随时更新：



* 在使用 DataBinding 的 Module 中，如下配置：

		android {
		    ....
		    dataBinding {
		        enabled = true
		    }
		}



* Data Binding Layout Files


		<?xml version="1.0" encoding="utf-8"?>
		<layout xmlns:android="http://schemas.android.com/apk/res/android">
		   <data>
		       <variable name="user" type="com.example.User"/>
		   </data>
		   <LinearLayout
		       android:orientation="vertical"
		       android:layout_width="match_parent"
		       android:layout_height="match_parent">
		       <TextView android:layout_width="wrap_content"
		           android:layout_height="wrap_content"
		           android:text="@{user.firstName}"/>
		       <TextView android:layout_width="wrap_content"
		           android:layout_height="wrap_content"
		           android:text="@{user.lastName}"/>
		   </LinearLayout>
		</layout>

* Data Data


		@Override
		protected void onCreate(Bundle savedInstanceState) {
		   super.onCreate(savedInstanceState);
		   MainActivityBinding binding = DataBindingUtil.setContentView(this, R.layout.main_activity);
		   User user = new User("Test", "User");
		   binding.setUser(user);
		}

* Observable Objects


		private static class User extends BaseObservable {
		   private String firstName;
		   private String lastName;
		   @Bindable
		   public String getFirstName() {
		       return this.firstName;
		   }
		   @Bindable
		   public String getLastName() {
		       return this.lastName;
		   }
		   public void setFirstName(String firstName) {
		       this.firstName = firstName;
		       notifyPropertyChanged(BR.firstName);
		   }
		   public void setLastName(String lastName) {
		       this.lastName = lastName;
		       notifyPropertyChanged(BR.lastName);
		   }
		}


* ObservableFields
		
		private static class User {
		   public final ObservableField<String> firstName =
		       new ObservableField<>();
		   public final ObservableField<String> lastName =
		       new ObservableField<>();
		   public final ObservableInt age = new ObservableInt();
		}


MainActivity：


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
		// setContentView(R.layout.activity_main);
        ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
        user = new User();
        user.userName.set("ivy123");
        user.pwd.set("123");
        binding.setUser(user);


        new Thread(new Runnable() {
            @Override
            public void run() {
                SystemClock.sleep(3000);
                user.userName.set("ivy");
            }
        }).start();

    }



----

4个Demo下载地址：

[LoginDemos](https://github.com/IvyZh/Android_Learning/blob/master/demos/login_mvc_mvp_mvvm_demos.zip)
