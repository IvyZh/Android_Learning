## 第04讲_01_Spinner的使用


主要内容：

1. 什么是Spinner？
2. ArrayAdapter的使用
3. Spinner的使用


### 什么是Spinner？

> Spinner表现为一种列表，它的主要是让用户进行选择。

![](http://www.jcodecraeer.com/uploads/20150105/1420392233199796.png)


### ArrayAdapter的使用

> 起到了数据源和适配器控件的桥梁作用

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/yztc/QQ%E6%88%AA%E5%9B%BE20161208170430.png)

使用方法：

- 1. XML文件中定义加载的数据资源，通过ArrayAdapter.createFromResource()方法加载资源
- 2. Java代码中使用Adapter对象，把List<T>中的数据资源加载到Spinner中


### Spinner的使用

1. 准备数据
2. 加载数据到适配器中
3. 将适配器设置给Spinner中


在strings.xml资源文件中设置资源数组

	<string-array name="plantes_array">
		<item>Earth</item>
		<item>Mars</item>
		<item>Venus</item>
	</string-array>

String[] plantes = getResources().getStringArray(R.array.plantes_array);


ArrayAdapter<String> adapter = new ArrayAdapter<String>(context,resource,objects);

	context:上下文。
	resource：表示列表item布局资源id，可以使用android提供的布局android.R.layout.simple_spinner_item
	objects:数据源，plantes

- Spinner的监听事件：
	- setOnItemSelectedListener
		- OnItemSelectedListener中有两个方法
			- onItemSelected(AdapterView parent,View view,int pos,long id)AdapterView:表示当前触发事件的适配器控件对象 spinner；view：表示当前被选中item的对象
			- onNothingSelected：当没有东西选中的时候

获取选中的数据

1. 根据下标在数据源中获取 
2. 根据下标在适配器中获取 adapter.getItem(position)
3. 根据下标在spinner在控件中获取 spinner.getItemAtPosition(position).toString();


## 第04讲_02_AutoCompleteTextView

主要内容：

1. 什么是AutoCompleteTextView？

2. AutoCompleteTextView的使用


### 什么是AutoCompleteTextView？


> 当用户输入它会自动提供建议，建议列表显示在下拉菜单，从中用户可以选择一个项目，以取代编辑框的内容。

![](http://images.cnitblog.com/blog/446475/201409/131644517621390.jpg)


### AutoCompleteTextView的使用

1. 准备数据
2. 将数据源数据加载到适配器中
3. 将适配器数据加载到控件中



在strings.xml资源文件中设置资源数组

	<string-array name="plantes_array">
		<item>Earth</item>
		<item>Mars</item>
		<item>Venus</item>
	</string-array>

String[] plantes = getResources().getStringArray(R.array.plantes_array);


ArrayAdapter<String> adapter = new ArrayAdapter<String>(context,resource,objects);

	context:上下文。
	resource：表示列表item布局资源id，可以使用android提供的布局android.R.layout.simple_spinner_item
	objects:数据源，plantes

autoTextView.setAdapter(adapter);


AutoCompleteTextView属性：

- completetionThreshold="1": 设置自动提示最少输入字符
- completetionHint : 提示信息


列表中某个item被点击的事件

autoTextView.setOnItemClickListener(new OnItemClickListener{//...})

可以在数据源中获取 可以在Adapter中获取 可以在AutoCompleteTextView中获取。