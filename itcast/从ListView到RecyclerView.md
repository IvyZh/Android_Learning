Android5.0 之后推出的。集合了ListView和GridView的功能，还自带了瀑布流效果。


Menu:

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161228140903.png)


RecyclerView:

1. 布局填充器LayoutManager
2. 适配器Adapter


mRecyclerView.setLayoutManager(LayoutManager layout)


- LayoutManager
	- LinearLayoutManager
	- StaggeredGridLayoutManager

// 设置布局管理器

mRecyclerView.setLayoutManager(new LinearLayoutManager(this))


> ctrl + p： 参数提示


// 设置Adapter

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161228142226.png)


onCreateViewHolder

onBindViewHolder


### ListView垂直反转

- layoutManager.setReverseLayout(true);//设置是否反向


### 设置方向

- layoutManager.setOritation(HORIZONTAL VERTICAL)


### 添加CardView的依赖

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/itcast/QQ%E6%88%AA%E5%9B%BE20161228164619.png)

- 属性
	- cardelevation 海拔



### 瀑布流


new StaggeredGridLayoutManager(2,oritation);

