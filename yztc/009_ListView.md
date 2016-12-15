## 第09讲_01_ListView的基本使用

主要内容：

1. 什么是ListView？
2. ListView的常用属性
3. ListView的基本使用

### 什么是ListView？

> ListView控件提供了一个基础结构，用于在不同布局或视图中显示一组数据。

### ListView的常用属性

* ListView属性
	* android:choiceMode 设置ListView的选择行为
	* android:divider 设置List列表的分隔条（颜色分割|Drawable分割）
	* android:dividerHeight 设置分隔条的高度
	* anndroid:entries 指定一个数组资源，Android将根据该数据资源生成ListView
	* android:footerDividersEnabled 如果设为false，则不再footerView之前绘制分割条
	* android:headerDividersEnabled 如果设置为false，则不在headerView之后绘制分割条


### ListView的基本使用

entries：可以在xml文件中设置一个string-array数据源，使用@array/citys,运行就可以显示

divider和dividerHeight 需要结合到一起使用，设置item之间的间距高度和间距颜色

headerDividersEnabled和footerDividersEnabled 并没有明显的效果


使用步骤：

1. 准备数据: String[] citys = getResources().getStringArray(R.array.citys);
2. 将数据加载到适配器中 adapter = new ArrayAdapter(this,android.R.layout.simple_list_item_1,citys);
3. 将适配器加载到ListView中 lv.setAdapter(adapter);

监听事件：

- setOnItemClickListener()
	- onItemClick(AdapterView parent,View,postion,id) : parent是listView？

获取点击数据的方式：

1. 数据源中 citys[postion]
2. 适配器中 adapter.getItem(postion)
3. 在parent中获取 parent.getItemAtPosition(position).toString();
4. 在listView中获取 lv.getItemAtPosition(position).toString();


- setOnLongClickListener()
	- onItemLongClick(AdapterView parent,View,postion,id):返回值，false表示对事件不处理（对点击和长按事件都会处理），true表示处理（只对长按处理，点击不处理了）

## 第09讲_02_ListView的常用方法

主要内容：

1. ListView的常用方法
2. SimpleAdaper的使用

### ListView的常用方法

lv.addHeadView(v):必须在setAdapter之前。同理，addFooterView(v) 也一样。


ImageView iv = new ImageView(context);
iv.setLayoutParams(xx,xx);

lv.setEmptyView(v);

View v = LayoutInflater.from(Context).inflate(R.layout.header,null);

## 第09讲_03_SimpleAdaper的使用

### SimpleAdaper的使用

ArrayAdapter的数据源是数据或者集合，当展示的内容是文本信息的时候可以使用。

SimpleAdaper的数据源是一个Map，可以为多个控件赋值信息。


	private List<Map<String,Object>> dataList = new ArrayList<Map<String,Object>>();

	//1. 准备数据源
	for(int i = 0;i<10;i++){
		Map map = new HashMap<String,Object>();
		map.put("img",image[i]);
		map.put("text","要显示的内容"+i);
		list.add(map);
	}

	// 2. 将数据源加载到适配器
	SimpleAdapter adapter = new SimpleAdapter(this,dataList,R.layout.list_item,new String[]{"img","text"},new int[]{R.id.iv,R.id.tv});



## 第09讲_04_BaseAdapter的基本使用

主要内容

1. BaseAdapter的基本使用


### BaseAdapter的基本使用

1. 子类继承BaseAdapter
2. 需要重写自定义适配器中的相应的函数
3. 创建自定义适配器对象并且使用




code：

	class MyAdapter extends BaseAdapter{
		
		getCount():加载数据的总条数
		
		getItem(int postion): 表示根据指定下标获取对应item的view。可以返回 dataList.get(postion);
	
		getItemId(int position) :表示根绝指定下标获取当前item的id 可以返回 position
	
		getView(int pos,View convertView,ViewGroup parent) : 表示根据指定下标获取适配器控件中每个item对应的view对象，得到每个用于展示数据的item视图
			- pos： 当前绘制的item的下标
			- convertView：可复用的view对象
			- ViewGroup ： 表示当前绘制的item所属的listView控件
		
	}


LayoutInflater 的几种获取方式：

LayoutInflater infalter =  (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);

View v = infalter.infalte(R.layout.item_list,null);



## 第09讲_05_ListView的优化

主要内容：

1. ListView的工作原理
2. ListView的优化


### ListView的工作原理


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161214185343.png)


Listview的缓存原理

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161214185452.png)


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161214185522.png)


code:

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161214190712.png)



如果ListView比较复杂的时候，就不便给每个view设置tag了，于是我们可以使用ViewHolder将item里面的控件进行封装使用，名字可以任意起。
![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161214191239.png)

> 主要ListView的xml布局最好指定mathc_parent,因为指定wrap_content的时候，getView会执行多次。


内存空间优化（convertview）
运行时间优化（viewholder）





