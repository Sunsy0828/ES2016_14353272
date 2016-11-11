###实验效果
####example2
#####修改前
实现的功能是从0到19输入20个数，分别执行三次平方操作，最终输出结果如下：

![](http://upload-images.jianshu.io/upload_images/3240217-84519fd227cffbc0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

dot截图如下,可以看出在生产者和消费者这两个模块之间一共有三个平方模块，相互之间用连接线相连，每个connection上标注了通道名称:

![](http://upload-images.jianshu.io/upload_images/3240217-d75586b527629c51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####修改后

![](http://upload-images.jianshu.io/upload_images/3240217-cb49f4976d4d465a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

dot图中平方模块变成了两个，和上面的输出结果相对应。

![](http://upload-images.jianshu.io/upload_images/3240217-b4b6bfadbd478be2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####example1
使原来输出平方的功能变成输出三次方，效果如下：

![](http://upload-images.jianshu.io/upload_images/3240217-9102073c8d0a1c7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

dot图无实质变化，但实际的功能已经改变

![](http://upload-images.jianshu.io/upload_images/3240217-77c8164ecf475cbf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###修改说明
####example2
修改xml文件中的迭代次数，使原来的3次平方迭代变为2次

![](http://upload-images.jianshu.io/upload_images/3240217-ba5d0e09d923feff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样会迭代生成两个平方模块和三个sw_channel

![](http://upload-images.jianshu.io/upload_images/3240217-ff7fae005f850cb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3240217-9be7ee5d3a204da9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

并且以迭代的方式生成connection，因为每条线要有2个connection，所以我们看到在迭代部分是下图这样的

![](http://upload-images.jianshu.io/upload_images/3240217-29e17da0927f0128.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样就解释清楚了example2的修改思路和方法
####example1
直接修改square.c文件，把原来的i = i × i,改为i = i × i ×i 即可实现立方运算，关于各模块的功能分析和连线同example2.

![](http://upload-images.jianshu.io/upload_images/3240217-e554b3301d47a44b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###实验感想
学习了有关DOL实例的分析，学会了以下内容：
在每个example的src文件夹下是各进程，每个进程由一个.c文件和.h文件对应，每个进程要对应两个接口，以及两个函数分别是init和fire，代表初始化的内容和运行时实现的功能。.xml文件中定义了模块之间的连接方式，其中包含了process,sw_channel,connection。Process即为进程内容，sw_channel是每个进程的通道线，connection定义了进程间的连接方式。
我们这次分析的是包含生产者和消费者两个进程的实例，生产者负责执行一个功能，其中会设定一个生产长度，只有程序执行次数达到生产长度才会停止。消费者是将执行结果打印到输出端，也是有一个对应的长度。程序要实现的功能部分就写在Square.c这个功能模块里，在example1里，我们一开始定义的是一个平方进程。
以上是模块部分，比较好理解。
而在xml文件中就涉及具体的如何连接这些模块。首先是进程定义，需要包含进程名称（与模块名称对应），端口设置以及对应的文件源，每个端口都要有对应的类型和一个具体的名称。一般来说，端口名称会定义在对应模块的.h文件里。然后是通道设置，每个通道一定会连接一个输入端口和一个输出端口，我们还可以为通道定义缓冲区大小。最后是定义模块之间的连接，用一条连线表示，每条连线会对应两个connection。这里需要注意一下，在我们的实例中，每条连接线并不是直接连通两个模块，而是先从模块连接到了定义好的sw_channel的某一个端口，再从channel的其他端口连接到其他模块。
通过这次对DOL实例分析和对程序做出的简单修改，对整个机制有了更清晰的了解，对今后实现自己的想法有了一定基础。