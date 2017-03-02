![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.17
老师:Ricky


### 回顾

	作业：1.解决课上的bug：滑动删除的时候，然后再滑动页面，结果有的条目不出现了 有空白的地方。
		原因：ListView和RecyclerView都会有复用条目itemView。这样就会导致上面的问题。
		解决：很多。比如在clearView回调方法里面去恢复这些条目的状态
		@Override
		public void clearView(RecyclerView recyclerView, ViewHolder viewHolder) {
			// 恢复
			viewHolder.itemView.setBackgroundColor(Color.WHITE);
			
	 		viewHolder.itemView.setAlpha(1);//1~0
	 		viewHolder.itemView.setScaleX(1);//1~0
	 		viewHolder.itemView.setScaleY(1);//1~0
			super.clearView(recyclerView, viewHolder);
		}
	
方法2：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302153815.png)

	
	2.类似QQ的条目侧滑一半的效果
	提示：
		方法一：判断
		//判断是否超出或者达到width/2，就让其setTranslationX位一般的位置
			if(Math.abs(dX)<=viewHolder.itemView.getWidth()/2){
				viewHolder.itemView.setTranslationX(-0.5f*viewHolder.itemView.getWidth());
			}else{
				viewHolder.itemView.setTranslationX(dX);
			}
		方法二：ItemView就是一个ViewPager，上面的view可以朝反方向设置TranslationX



### MateriaDesign侧滑


以前是有民间的效果：SliddingMenu

	侧滑两种效果：1.盖在整个页面上面；2.在Toolbar下面。
	在MD提出来以后，谷歌就收录并改变了很多开源项目，放到API及support包里面。
	1.DrawerLayout 抽屉容器
		来自support-v4包里面的。（android.support.v4.widget）
		相当于一个自定义容器 extends ViewGroup ,可以看出是一个有侧滑效果的帧布局
		两个部分：1）内容布局；2）侧滑出来的菜单布局
	
	2.NavigationView


- DrawerLayout：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302162656.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302163533.png)

ToolBar:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302164653.png)

可以继承AppCompatActivity或者ActionBarActivity

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302164829.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302164914.png)


加一个菜单：

ActionBarDrawerToggle

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302170557.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302171002.png)

---

另一部分：

侧滑两种效果：1.盖在整个页面上面；2.在Toolbar下面。
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302171157.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302171226.png)


- DrawerLayout源码：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302172403.png)



右边滑动：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302173535.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302173554.png)


一个简单的特效：

Toolbar还是放里面，

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302174729.png)

效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302174744.png)

end.
