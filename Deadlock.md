####产生死锁的效果图

![](http://upload-images.jianshu.io/upload_images/3240217-710f2ac3f74e350c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

154次时产生死锁
####产生死锁的四个必要条件
1.互斥条件：一个资源每次只能被一个进程使用

2.请求与保持：一个资源因请求资源而阻塞时，对已获得的资源保持不放

3.不剥夺条件：进程已获得的资源，在未使用完之前，不能强行剥夺

4.循环等待：若干进程之间形成一种头尾相接的循环等待资源关系

####实验分析
分析Java程序中的死锁现象就需要先理解synchronized：
·当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。
·当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。
也就是说该关键字相当于标记了一把锁。
接下来看程序

![](http://upload-images.jianshu.io/upload_images/3240217-16c6b709ef9e06ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3240217-0ebb5317531f17b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

class A中有用关键字synchronized修饰的methodA和打印语句“Inside A.last()”的函数，同样的class B中有关键字synchronized修饰的methodB和打印语句“Inside B.last()”的函数。接着定义了一个Deadlock类，如下：

![](http://upload-images.jianshu.io/upload_images/3240217-77f1ddeb61ff6e79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

该类中分别定义了class A和class B的对象，并在构造函数中，定义了新线程t,当t.start()之后，它就被插入到调度队列，当调度到它就在执行run()里面的代码。
当main函数启动后，主线程运行→t线程运行，t线程实际上执行对象b的方法methodB，由于这个方法被关键字标记，所以相当于t线程拿到了b对象的锁，但是在methodB中是对象a执行last方法，由于该方法也被关键字标记，所以t线程也要申请a对象的锁，并打印输出语句：Inside A.last()。t线程执行完之后，回到主线程，主线程在while循环中执行对象a的方法methodA，该方法会让主线程尝试去拿a对象的锁，但是a对象的锁刚刚被t线程拿着，如果t线程结束了释放了锁，那么主线程可以拿到锁，继续执行又去尝试获取b对象的锁，如果t线程没有释放锁，那么主线程将不得不等待线程t释放它需要的两个对象的锁才能接着执行。反过来，当主线程持这两个对象的锁时，线程t自然也要等待。
因为我们的系统中不可能只有这两个线程，所以在多次执行该文件的过程中，很可能在t线程刚拿了b对象的锁后，资源就给到了主线程，主线程首先申请拿a对象的锁，很好，拿到了，此时资源又给到了t，t申请对象a的锁，由于主线程自己也只走了一半，他不可能放掉手中已获得的a对象的锁，同理他也申请不到b对象的锁，因此死锁就这么产生了。
所以对于死锁产生的关键点就在于要明确锁的对象是某个类的实例，而不是某个方法，其次持锁的是线程，不同线程竞争同一对象的锁时，很可能就会发生死锁。