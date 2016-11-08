#实验四:安装ROS#
***
##ROS的描述##
**&emsp;&emsp;ROS(Robot operation system，机器人操作系统)是一个开放的标准平台，它提供了一系列的软件框架和工具以帮助软件开发者创建机器人应用软件。底层提供硬件驱动，软件层面支持通用的文件格式。**
<br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097322/bd0181c6-a5e8-11e6-8f8e-62b226f46e6b.JPG"><br><br>
**&emsp;&emsp;当然，我们不可能接触到这么高深的东西，正如这次实验，我们仅仅是安装一下ROS，却没有去学习如何使用它，毕竟这是一款很吊的框架。**
***
##安装流程##
###Step 1:配置Ubuntu的软件中心###
**&emsp;&emsp;配置Ubuntu要求允许接受"restricted," "universe," and "multiverse."的软件源，这一步我们可以不管。**
***
###Step 2:设置你的sources.list(软件源)###
**&emsp;&emsp;保证电脑能够接收到软件安装包。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097395/27de344e-a5e9-11e6-925f-5aa0213d8f2d.png">
***
###Step 3:设置你的密钥###
<img src="https://cloud.githubusercontent.com/assets/22441228/20097408/3aa7bc94-a5e9-11e6-9fdc-14e4a700e5f5.png">
**&emsp;&emsp;此处有问题，但不清楚是何原因，上一张截图命令执行后报错，这张截图显示命令执行成功。**
***
###Step 4:安装###
**&emsp;&emsp;首先确认你的Debian的软件包索引是最新的(Debian计划是一个致力于创建一个自由操作系统的合作组织。我们所创建的这个操作系统名为Debian。Debian系统目前采用Linux内核或者FreeBSD内核)。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097431/6017633a-a5e9-11e6-8e46-f7ea7ecf6810.png"><br>
**&emsp;&emsp;此为开始。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097448/71fe29bc-a5e9-11e6-83c0-9911e920977c.png"><br>
**&emsp;&emsp;此为结束。**<br><br>
**&emsp;&emsp;在ROS中有许多不同的函数库和工具，建议是完全安装，也可以根据自己的要求分别安装。完全安装时的工具包括ROS,rqt,rviz,robot-generic libraries,2D/3D simulators,navigation and 2D/3D,perception。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097465/882bb948-a5e9-11e6-889b-7968c0f83d3f.png"><br>
**&emsp;&emsp;此处因为内容太多，所以开始安装忘记截图。**<br><br>
**&emsp;&emsp;寻找可用的包(不需要去管)。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097482/a441896e-a5e9-11e6-85bc-37c3843d6d2f.png">
***
###Step 5:初始化rosdep###
**&emsp;&emsp;在使用ROS之前，需要初始化rosdep。它可以使你轻松的安装你想要编译及运行的模块。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097503/b976fb5c-a5e9-11e6-94d2-588a53957d94.png"><br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097505/badc2ad0-a5e9-11e6-89ff-f08c71dc0998.JPG"><br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097507/bc452ca0-a5e9-11e6-8fee-d03e864088b6.JPG"><br>
**&emsp;&emsp;又是这种情况，第一次执行命令失败，第二次执行才成功。**<br>
***
###Step 6:设置环境###
**&emsp;&emsp;添加ROS的环境变量，这样，当你打开你新的shell时，你的bash会话中会自动添加环境变量。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/20097544/ed23dfce-a5e9-11e6-87ad-c1f65f2efd9d.JPG">
***
###Step 7:安装rosinstall###
<img src="https://cloud.githubusercontent.com/assets/22441228/20097570/0c9ef564-a5ea-11e6-93c5-e08bc704aa6b.JPG"><br>
**&emsp;&emsp;rosinstall命令是一个使用的非常频繁的命令，使用这个命令可以轻松的下载许多ROS软件包。**<br>
***
##实验感想与心得##
&emsp;&emsp;本次实验与第一次安装DOL的感觉差不多，甚至还不堪，因为之后我们对DOL实例进行了分析，而这次却完全不懂。至于安装的时候则是按部就班的照着网站上的命令敲得，而原因、结果正确与否都不是很清楚，想必很多人和我都有着一样的感觉吧。所以在我看来，我们都有必要去熟悉一下这套框架的具体用途以及一些简单的使用方法，不求半懂，只求略懂。