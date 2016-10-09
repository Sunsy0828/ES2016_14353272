#  嵌入式实验一：DOL开发环境的配置

### Description
The distributed operation layer (DOL) is a framework that enables the (semi-) automatic mapping of applications onto the multiprocessor SHAPES architecture platform. The DOL consists of basically three parts:

 1.**DOL Application Programming Interface**
 
 2.**DOL Functional Simulation**
 
 3.**DOL Mapping Optimization**

### How to install
###### 1.安装一些必要的环境
`$ sudo apt-get update`

`$ sudo apt-get install ant`

`$ sudo apt-get install openjdk-7-jdk`

`$ sudo apt-get install unzip`

![](http://upload-images.jianshu.io/upload_images/3240217-d5766cfc70201719.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 2.下载两个文件：dol_ethz.zip和systemc-2.3.1.tgz
###### 3.解压文件
 ·新建dol文件

 `$ mkdir dol`

 ·将dolethz.zip解压到 dol文件夹中

 `$ unzip dol_ethz.zip -d dol`

 ·解压systemc

 `$ tar -zxvf systemc-2.3.1.tgz`
###### 4.编译systemc

·解压后进入systemc-2.3.1的目录下

`$ cd systemc-2.3.1`

·新建一个临时文件夹objdir，并进入

`$ mkdir objdir`

`cd objdir`

·运行configure

`$ ../configure CXX=g++ --disable-async-updates`

![](http://upload-images.jianshu.io/upload_images/3240217-fe61f67146e1e535.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

·编译，编译后目录如下图

`$ sudo make install`

![](http://upload-images.jianshu.io/upload_images/3240217-2a2b8b667fb01a84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

·记录当前的工作路径

`$ pwd`

![](http://upload-images.jianshu.io/upload_images/3240217-7465c8dba2d55993.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 5.编译dol

·进入刚刚的dol文件夹

`$ cd ../dol`

·修改build_zip.xml文件

><property name="systemc.inc" value="YYY/include"/>

><property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>

>把YYY改成上页pwd的结果

·再次编译，成功则会显示build successful

![](http://upload-images.jianshu.io/upload_images/3240217-d679e50ce42f9b10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 6.试运行example1

·进入build/bin/mian路径下

`$ cd build/bin/main`

·运行第一个例子,成功如图示。

`$ ant -f runexample.xml -Dnumber=1`

![](http://upload-images.jianshu.io/upload_images/3240217-a37f6a32be1b2469.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Experimental experience

本次实验是为之后的实验做好环境配置，基本按照文档指示即可完成。重点在于后面版本控制。git是非常方便的，我们平常写代码，尤其是调试过程中做好版本管理非常重要。Git是分布式的版本控制系统，与传统的集中式相比，具有无需联网，安全性高的优点。无需联网使我们不必收到互联网速度的限制，集中式正是因为中央服务器的限制才会逐渐显现出劣势。安全性高是说每个人的电脑上都有一个完整的版本库，一个损坏，还可以去别处复制。所以本次实验我们就从最基础的部分开始，创建自己的版本库，并上传第一份md文件。说到md文件，是用markdown语言编辑的，相比与html，更加简单，因为它的语法数量少，便于记忆，同时排版功能也毫不逊色。以后可以多加尝试用Markdown来编辑文本。
