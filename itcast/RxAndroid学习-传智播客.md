## 01_监听回调

RxJava在Android中的应用

主要内容：

1. RxJava是什么，能解决什么问题
2. 对比其他技术理解为什么要选择RxJava
3. RxJava相关API
4. RxJava在Android中的典型使用场景
5. RxJava在Android中与其他框架的融合

### RxJava是什么，能解决什么问题
* github介绍：
	> a library for composing asynchronous and event-based programs by using observable sequences.

	> 一个运行在Java VM上的库，通过可观察的序列来组成异步的、基于时间的程序。

* 解决问题：
	> 让复杂程序逻辑回归简单、清晰


---

> 异步的介绍

ButterKnife 的配置：引入方式，（5.1.1的。。。

SystemClock.sleep(2000);//界面阻塞

开启子线程做耗时操作：异步请求获取数据（网络请求、数据库查询、文件读写等

code1:

	getResuultAsync(){
		calcService.calcAsync(10,5,this);
	}

	calcAsync(int total,int person,Activity a){
	
		new Thread(new Runnable(){
			...
			a.onSuccess(result);
			...
			a.onFailed();
		}).start();		
	}


code2:面向接口编程,通过监听回调的方式实现回调

	calcAsync(int total,int person,OnResultListener a){
	
		new Thread(new Runnable(){
			...
			a.onSuccess(result);
			...
			a.onFailed();
		}).start();		
	}

总结，一种是在调用的时候传入接口，另一种是先设置监听方法，再调用请求方法。


---



## 02_RxJava的基本实现


* RxJava四个基本概念
	* Observable（可观察者/被观察者）
	* Observer（观察者/订阅者）
	* subscribe（订阅）
	* Event（事件）


### 如何使用

* build.gradle引入依赖

		compile 'io.reactivex:rxandroid:1.2.1'
		compile 'io.reactivex:rxjava:1.1.6'

### 对比其他技术理解为什么要选择RxJava

* Observable（被观察者）和Subscribe（订阅者）可以做任何事情
	* Observable可以是一个网络请求，Subscribe来显示请求结果
	* Observable可以是一个数据库查询，Subscribe来显示查询结果
	* Observable可以是按钮点击事件，Subscribe来响应点击事件
	* Observable可以是大图片文件的加载解析，Subscribe来展示解析的结果

简单的基本使用：

Observable.create(....)

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221164310.png)


变形的使用1（被观察者变形）：

	Observable.just(T...)// 就相当于上面new 出来一个OnSubscribe对象
			.subscribe(new Observer<T>(){
				onCompleted(){}
			
				onNext(){}
	
				onError(){}
				
			});

变幻2：

	Observable.from(new String[]{"a","b"})// 接收集合或者数组
			  .subscribe(new Subscriber<String>(){// Subscriber是继承了Observer
					onStart(){}// 多出来的一个方法，表示事件开始的时候

					onCompleted(){}
				
					onNext(){}
		
					onError(){}
					
				})

	Subscriber subscriber = ...;
	subscriber.unsubscribe();//在onStop的时候可以调用

	onStop(){
		if(subscriber!=null && !subscriber.isUnsubscribed()){
			subscriber.unsubscribe();
		}
	}
	

## 03_操作符及线程调度

变换3：

	Observable.from(new String[]{"a","b"}) 
			  .subscribe(new Action1<String>(){
				prublic void call(String s){
					
				}
			});

变换4：

	Observable.from(new String[]{"a","b"}) 
			  .subscribe(new Action1<String>(){// onNext
				public void call(String s){
					
				}
			},new Action1<Throwable>(){// onError
				public void call(Throwable t){
					
				}
			},new Action0(){//onCompleted
				public void call(){
					sop("compeleted");
				}
			});


### 操作符

* 转换（Map） 将一个对象转换成另外一个对象

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221173136.png)

可能是将网络数据转成bean 也可能是cursor转成bean 或者流转成图片等等

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221173327.png)


### 线程调度器

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221164310.png)

Thread.currentThread().getName();在call 和next方法中打印线程名称发现都是**`main`**


        Observable.create(new Observable.OnSubscribe<String>() {
            @Override
            public void call(Subscriber<? super String> subscriber) {
                String name = Thread.currentThread().getName();
                Log.d("tag", "call " + name);
                subscriber.onNext("123");
                subscriber.onNext("12343");
                subscriber.onCompleted();
            }
        }).subscribe(new Observer<String>() {
            @Override
            public void onCompleted() {

            }

            @Override
            public void onError(Throwable e) {

            }

            @Override
            public void onNext(String s) {
                String name = Thread.currentThread().getName();
                Log.d("tag", "onNext " + name);
            }
        });
    }

指定线程：


![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221175033.png)

subscribeOn ： 可以执行多次

subscribe ： 只需要执行一次，指定订阅者执行的线程

        Observable.create(new Observable.OnSubscribe<String>() {
            @Override
            public void call(Subscriber<? super String> subscriber) {
                String name = Thread.currentThread().getName();
                Log.d("tag", "call " + name);
                subscriber.onNext("123");
                subscriber.onNext("12343");
                subscriber.onCompleted();
            }
        })
                .subscribeOn(Schedulers.io())//让subscribe的操作执行在异步线程
                .observeOn(AndroidSchedulers.mainThread())//让订阅者代码执行在UI线程


                .subscribe(new Observer<String>() {
                    @Override
                    public void onCompleted() {

                    }

                    @Override
                    public void onError(Throwable e) {

                    }

                    @Override
                    public void onNext(String s) {
                        String name = Thread.currentThread().getName();
                        Log.d("tag", "onNext " + name);
                    }
                });


* 小结线程调度
	- Schedulers.immediate() 默然线程
	- Schedulers.newThread() 每次都创建新的线程
	- Schedulers.io() 包含线程池的机制 个数无线 可以复用空闲线程
	- Schedulers.computation() CPU密集计算线程，线程池数和CPU数一致，一般用在图形运算
	- AndroidSchedulers.mainThread() Android更新界面的UI主线程

线程的切换案例：

![](https://github.com/IvyZh/Android_Learning/blob/master/imgs/rxandroid/QQ%E6%88%AA%E5%9B%BE20161221175807.png)


* flatMap 平铺对象 把集合中的对象取出来
* take(2) 只去前2个
* distinct() 去重
* toList() 重新打包成集合
* filter() 过滤

微信：mm7718mm
QQ:3077485083