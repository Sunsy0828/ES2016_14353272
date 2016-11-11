##安装ROS
####配置Ubuntu的软件源
配置Ubuntu要求允许接受restricted,universe和multiverse的软件源，这一步需要在Software&Update下配置，一般来说这一步都是默认的，效果如图：

![](http://upload-images.jianshu.io/upload_images/3240217-27e76b53cf0aaead.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####添加软件源到sources.list

`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`

一旦添加了正确的软件源，操作系统就可以前往正确的地址下载程序并安装软件
####设置密钥

`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`

####安装
首先确认安装的软件包是最新的

`sudo apt-get update`

完成效果如下：

![](http://upload-images.jianshu.io/upload_images/3240217-dfe44ee603ebe724.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

更新完成后开始正式安装，因为ROS中有许多工具和库函数，所以我们选择完全安装

`sudo apt-get install ros-jade-desktop-full`

完成后效果如图：

![](http://upload-images.jianshu.io/upload_images/3240217-aaa4964e625125fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

为了找到可利用的包，执行下面这条指令，效果如图：

`apt-cache search ros-jade`

![](http://upload-images.jianshu.io/upload_images/3240217-7d2faa8c71868458.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####初始化rosdep
rosdep不仅能够使你更方便的安装一些系统依赖程序包，而且ROS的一些主要部件的运行也需要rosdep。

`sudo rosdep init`

`rosdep update`

![](http://upload-images.jianshu.io/upload_images/3240217-4b6e873bd8e72a7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3240217-d68b13b67b034a9c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####设置环境
添加ROS的环境变量

`echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

####安装rosinstall
rosinstall命令是一个使用的非常频繁的命令，使用这个命令可以轻松的下载许多ROS软件包。

`sudo apt-get install python-rosinstall`

当以上这些都做完后，我们就基本完成了ROS的安装，效果最终如下：

![](http://upload-images.jianshu.io/upload_images/3240217-6ef0937ca5b65592.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

但是我们怎么知道自己的ROS到底安装成功没有，在没有进一步安装cartographer的时候需要用其他方法来验证一下：

`$ roscore`

![](http://upload-images.jianshu.io/upload_images/3240217-3585bc2d0c880af1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

出现started core service [/rosout]表示启动正常