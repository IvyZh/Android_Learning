![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE.png)

录制时间：2016.06.15
老师:Ricky

> 视频把wmv转换成avi就有画面了

### RecyclerView交互动画

- ItemTouchHelper

演示效果：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302104643.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302104705.png)

ItemTouchHelper:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302131211.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302133011.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302133152.png)

isLongPressDragEnabled:

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302133235.png)

运行效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302133257.png)

如何做到按住头像就可以拖拽了呐？

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302133723.png)

设计接口：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302134102.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302134148.png)

回调：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302134309.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302134337.png)

---

第二部分：

NotifyItemMoved(from,to)

接口：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302135053.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302135326.png)

Adapter：
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302135534.png)

效果：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302135628.png)


侧滑删除：

继续在接口中添加方法，
![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140145.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140211.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140259.png)

演示效果是ok的。

做个效果：拖拽的时候条目颜色设个背景

onSelectedChanged(ViewHolder holder,int actionState)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140807.png)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140830.png)

复原状态：
clearView(ViewHolder holder,int actionState)

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302140936.png)

做个效果：侧滑的时候透明度改变，给条目做特性

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302141737.png)

演示效果ok，还可以设缩放等效果。

Bug：

![](https://github.com/IvyZh/Android_Learning/blob/master/DN/UI/imgs/QQ%E6%88%AA%E5%9B%BE20170302142012.png)

是因为划出去之后，就会出现了一个空行。


作业：
1.解决课上的bug：滑动删除的时候，然后再滑动页面，结果有的条目不出现了 有空白的地方。
2.类似QQ的条目侧滑一半的效果,右侧出现删除的按钮。

end.



