
文件名：##
小标题：###


## 第01讲_01_初识Android

内容要点：

1. 什么是Android
2. Android的发展史
3. Android系统架构


### 什么是Android？

> Android是一个Linux内核为基础的半开源的移动设备操作系统。


### Android发展史 
![](http://1)


### Android系统架构

![](http://2)

![](http://3)

- Linux内核层
	- Android是在Linux内核的基础上构建的
	- C语言编写
- 本地库和Android运行时环境层
	- Libraries和Android RunTime

- 应用程序框架层
	- 活动管理器
	- 窗口管理器
	- ...

![](http://4)

- 应用层

## 第01讲_02_Android开发环境搭建

内容要点：

1. Android环境搭建


### Android环境搭建

1. 安装JDK1.5+
2. 安装Eclipse
3. 安装Android SDK
4. 安装Eclipse插件ADT（Android Developement Tools）
5. 重启Eclipse 配置android sdk路径


> 推荐使用一次性打包下载Android开发工具 ADT


## 第01讲_03_Android项目创建

主要内容：

1. Android项目创建
2. Android应用程序框架


### Android项目创建

Application Name：应用市场上的名称
Project Name：
Package Name：

### Android应用程序框架

avd：Android virtual devies

> 初期可以选择一个分辨率小的模拟器

ram:内存

internal storage：内部存储

sdcard:占有PC端的大小，设置多大就会占用pc多大的硬盘空间


* 应用程序框架
	* src：java代码
	* gen：自动生成
	* assets：资源
	* bin：
	* libs：三方库