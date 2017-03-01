![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.13
老师:Ricky


### RecyclerView 如何添加头部和底部

	ListView.addHeadView();
	ListView.addFooterView();

	RecyclerView没有这样的方法，需要自己解决
	所以我们通过看ListView的源码学习如何解决这个问题！！
	
	ListView.addHeaderView(){
		 if (mAdapter != null) {
	            if (!(mAdapter instanceof HeaderViewListAdapter)) {
	                mAdapter = new HeaderViewListAdapter(mHeaderViewInfos, mFooterViewInfos, mAdapter);
	            }
	};
	ListView.setAdapter(){
		if (mHeaderViewInfos.size() > 0|| mFooterViewInfos.size() > 0) {
	            mAdapter = new HeaderViewListAdapter(mHeaderViewInfos, mFooterViewInfos, adapter);
	        } else {
	            mAdapter = adapter;
	        }
	}
	
	ListView.setAdapter(new SimpleAdapter(xxx))
	
	使用了中间代理模式解决的。模仿！！


![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301192324.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301192504.png)

getItemCount:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301192633.png)

getItemType():

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301193151.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301193729.png)


onBindViewHolder():

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301193831.png)
同理addFooterView:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194011.png)

MyAdapter:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194117.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194215.png)

设置：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194253.png)

记得设置LayoutManager，要不然不显示。

运行效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194414.png)

解决数组越界问题：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170301194536.png)

end.
