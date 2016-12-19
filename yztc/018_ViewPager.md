## 第18讲_01_ViewPager基本用法

主要内容：

1. 什么是ViewPager？
2. 怎么用ViewPager


### 什么是ViewPager？

![](http://static.oschina.net/uploads/space/2014/0320/150920_Y0Ck_932977.png)


### 怎么用ViewPager

1. 结合PagerAdapter使用
2. 结合FragmentPagerAdapter使用

xml:

	<android.support.v4.view.ViewPager
		...
		/>

code:


	mvp.setAdapter(new MyAdapter());



	class MyAdapter extends PagerAdapter{
		
		int getCount(){
			return mList.size(); 
		}
	
		// 判断是否需要重新生成新的子视图
		boolean isViewFromObject(View v,Object o){
			return v==o;
		}	
	
		//-----
	
		// 产生一个新的视图
		Object instantianteItem(ViewGroup container,int pos){
			ImageView iv = mList.get(pos);
			container.addView(iv);
			return iv;
		}
	
		// 移除一个视图
		void destoryItem(ViewGroup container,int pos,Object obj){
			container.removeView(mList.get(pos));// 把原来的super去掉
		}
	}

## 第18讲_02_ViewPager的界面切换

加一个Title

	mvp.setOnPagerChangeListener(new SimpleOnPageChangeListener(){
		//...
		onPageSelected(int pos){
			tvTitle.setText(titles[pos]);
		}
	});

## 第18讲_03_ViewPager结合Fragment使用

	Lits<Fragment> mList = new ArrayList<Fragment>();
	for(){
		mList.add(ContentFragment.newInstance("msg balabal.."));
	}
	

	class MyAdapter extends FragmentPagerAdapter{
	
		public MyAdapter(Fragment fm){// support v4 包的
		
		}
	
		// 返回一个Fragment对象
		Fragment getItem(int pos){ support v4 包的Fragment，
			return mList.get(pos);
		}
	
		public int getCount(){
			return mList!=null?mList.seize():0;
		}
		
	}


为了得到v4包下的FragmentManager，Activty必须继承FragmentActivity



## 第18讲_04_ViewPager添加导航栏


	<android.support.v4.view.ViewPager
			...
		
		<android.support.v4.view.PagerTabStrip
			...
		/>
	
	
	</android.support.v4.view.ViewPager>


mTabStrip 导航控件


	class MyAdapter extends FragmentPagerAdapter{
	
		public MyAdapter(Fragment fm){// support v4 包的
		
		}
	
		// 返回一个Fragment对象
		Fragment getItem(int pos){ support v4 包的Fragment，
			return mList.get(pos);
		}
	
		public int getCount(){
			return mList!=null?mList.seize():0;
		}

		public CharSequence getPageTitle(int pos){
			return titleNames[pos];
		}
		
	}


	mTabStrip.setTextColor(Color.RED);
	mTabStrip.setTextSize(TypeValue.COMPLEX_NIT_SP,20);
	mTabStrip.setTabIndicatorColor(Color.RED);