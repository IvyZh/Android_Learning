> 来源：动脑学院 Jason 2016.6.6


* 为什么要做架构设计
	* 最主要是为了系统的扩展
	* 安全...


* MVC（并没有明确的规范）
* MVP：Android开发使用，相对MVC规范比较规范，在系统扩展、架构扩展上面更加的灵活
	* Model：业务逻辑
	* View：视图
	* Presenter:中间者（绑定Model和View）



### MVP

![](http://1)

* MVP需求提出
	* 数据获取由本地加载改成网络获取
	* 界面由ListView改成GridView
	* 项目就会改来改去...


* 分析
	* 展示（视图）有可能会变
	* 业务逻辑有可能会变


在Android中角色MVP分配

* View：Activity

* Model：业务逻辑类(接口)// 所在包com.xx.xx.model
	* IGrilModel
		* public interface IGirlModel


IGirlModel 是加载数据的

- 是作为一个单独的类存在的


		public interface IGirlModel{
			void loadGirl(GirlOnLoadListener listener);
			
			public interface GirlOnLoadListener{
				void onComplete(List<Girl> girls)
			}
		
		}


View层：视图 IGirlView，包名：com.xx.xx.view

		public interface IGirlView{
			void showLoading();
			void showGirls(List<Girl> girls)；
		}


Model的实现

* GirlModelImplV1

		public GirlModelImplV1 implents IGirlModel{
		
			void loadGirl(GirlOnLoadListener listener){
				//load local data...
				listener.onComplete(girls);//回调
			}
		}


* Presenter

		public GirlPresenterV1{
			IGirlView mGirlView;
			IGirlModel mGirlModel = new GirlModelImplV1();
		
			public GirlPresenterV1(IGirlView mGirlView){
				this.mGirlView = mGirlView;
			}
		
			// bind view and model
			public void fetch(){
				mGirlView.showLoading();
				if(mGirlMode!=null){
					mGirlModel.loadGirl(new IGirlModel.GirlOnLoadListener(){
						// 显示给View
						public void onComplete(List<Girl> girls){
							mGirlView.showGirl(girls);
						}
					
					});
				}
				
			}
		}

		

* GirlListActivity

		public GirlListActivity extends Activity implents IGirlView{
	
			onCreate(){
				new GirlPresenter(this).fetch();
			}		
	
			public void showLoading(){
				dialog.show();
			}
	
			public void showGirls(List<Girl> girls){
				listView.setAdapter(new MyAdapter(girls));
			}
		}


> View持有Presenter，Presenter**持有Model的接口类型**



IGirlView为什么设计成接口？
* 不同的Activity都可以实现这个方法

IGirlModel为什么设计成接口？

* Presenter**持有Model的接口类型**，是为了可以实现不同网络请求方法，可以在Presenter里面setGirlModer()方法来指定加载所使用的方式

* Model加载完数据之后，使用接口来回调给View，让它来显示数据。


COP开闭原则

* 需求1：把本地数据换成网络数据[改变Model]

	- new GirlPresenterV2(this).fetch();//GirlPresenterV2 里面的加载Model换成了另外的加载(GirlModelImplV2)，可以是网络。
	- new GirlPresenterV1(this).setModel(1).fetch()//GirlPresenterV1 里面加一个设置Model的方法，Model有两个实现(GirlModelImplV1,GirlModelImplV2);

* 需求2：ListView变成GridView[改变View]
	* GirlGridActivity extends Activity implents IGirlView{//...}


* 两个问题
	* new GirlPresenterV2(this).fetch(); 可以抽取出来
	* 内存泄露问题


- 内存泄露

![](http://2)



分析：一个Activity可能有多个网络请求，如何从架构角度来分析设计呢？


- MVPBaseActivity--->模板方法


	public abstract class MVPBaseActivity <V,T extends BasePresenter<V>> extends Activity{
	
		protected T mPresenter;
	
		onCreate(){
			mPresenter = createPresenter();
			mPresenter.attachView((V)this);//关联
		}
	
		onDestory(){
			mPresenter.detachView();//解除关联
		}
	
	}


- BasePresenter

		public class BasePresenter{
		
			protected WeakRefrence<T> mViewRef;
		
			attachView(T view){
				mViewRef = new WeakRefrence<T>(view);
			}
		
			detachView(){
				if(mViewRef!=null){
					mViewRef.clear();
					mViewRef = null;
				}
			}
		
		}


- 当内存不足的时候，优先回收Model而不是View



----

- 架构设计
- 高级UI
- 性能优化
- ndk
- react-native
