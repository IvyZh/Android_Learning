## 第17讲_01_静态Fragment的创建

1. 什么是Fragment？
2. 为什么要设计出Fragment？
3. Fragment怎么用？
4. Fragment生命周期
5. Fragment间传值


### 什么是Fragment？

> 1. "碎片"---> Sub Activity ,Fragment的宿主就是Activity

![](http://img3.imgtn.bdimg.com/it/u=3427184727,524098667&fm=214&gp=0.jpg)


### 为什么要设计出Fragment？

Android3.0之后才出来的。3.0是适用于平板的，到了4.0之后又合并了。

为了合理的利用空间

### Fragment怎么用？

1. 静态添加，XML控件来使用
2. 动态添加


静态添加

	<fragment
		android:id="+id/ft_left"
		...
		/>
	
	<fragment
		android:id="+id/ft_right"
		...
		/>


	class LeftFragment extends Fragment{
	
		public View onCreateView(){
			return inflater.inflate(R.layout.left,null);
		}
	
	}

	<fragment
		android:id="+id/ft_left"
		class="com.ivy.LeftFragment"
		...
		/>
	
	<fragment
		android:id="+id/ft_right"
		android:name="com.ivy.RightFragment"
		...
		/>

运行就可以了。这种方式很少用。

## 第17讲_02_动态创建Fragment

放帧布局作为容器

	<FrameLayout
		android:id="@+id/fl_left"
		...
		/>
	
	<FrameLayout
		android:id="@+id/fl_right"
		...
		/>


LeftFragment和RightFragment和上面的一样


使用：

	FragmentManager manager = getFragmentManager();//Actiivty内部用来与Fragment进行交互的接口
	FragmentTransaction transaction = manager.beginTransaction();//开启一个事务
	Fragment lFragment = new LeftFragment();
	Fragment rFragment = new RightFragment();
	transaction.add(R.id.fl_left,lFragment);
	transaction.add(R.id.fl_right,rFragment);
	
	transaction.commit();

## 第17讲_03_Fragment生命周期简介

Fragment:11
Activity:7

![](http://1)

onAttach()//挂载Fragment到Activity中

onCreate()

onCreateView()// 创建Fragment的视图

onActivityCreated() // 当Activity的onCreate方法执行完毕之后，告诉Fragment自己创建完毕。这个方法用来接收Activity传递过来的信息

onStrat()

onResume

onPause

onStop()

onDesoryView()

onDestory()

onDetach() // 解除挂载


## 第17讲_04_Fragment传值（一）

1. setArguments(bundle)
2. 接口回调



	FragmentTransition transaction = manager.beginTransaction();
	
	ContentFragment fragment = new ContentFragment();
	fragment.setArguments(bundle);
	transaction.add(R.id.fl_container,fragment);
	transaction.commit();


	class ContentFragment extends Fragment{
	
		onCreateView(){
		
			Bundle bundle = getArguments();
		
			if(bundle!=null){
				String value = bundle.getString("key","");
				// ...
			}
		}
	}



## 第17讲_05_Fragment传值（二）

接口:

	ContentFragment fragment = (ContentFragment)manager.findFragmentByTag("content");
