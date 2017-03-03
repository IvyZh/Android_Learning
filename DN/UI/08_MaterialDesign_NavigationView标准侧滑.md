![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.20
老师:Ricky


### NavigationView

> 是谷歌在侧滑的MaterialDesign的一种规范，所以提出了一个新的控件，用来规范侧滑的基本样式。

DrawerLayout+ NavigationView结合使用

注意：使用NavigationView，需要依赖项目：Design项目(引入)。

同时还需要依赖recyclerView项目和CardView项目！！！！


menu：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302183504.png)

header_layout:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302183639.png)

navigation+drawerlayout:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302183712.png)

记得主题换成Appcompat 然后Activity要继承AppcompatActivity，这样运行

运行的时候一直报错：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303100106.png)

解决办法：使用NavigationView，需要依赖项目：Design项目。	同时还需要依赖recyclerView项目和CardView项目！！！！
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303101018.png)

NavigationMenuView

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303103020.png)
 可以设置背景 android:background

子菜单：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303103458.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170303103654.png)

end.
