#实验一：DOL开发环境配置#
***
##DOL框架描述##
&emsp;&emsp;因为是初学者，所以说并不是很懂，只能随着后续的实验陆陆续续的研究出来的它的含义及用途。现在也就只能借用一下实验文档中的内容了。
<br>
**&emsp;&emsp;分布式操作层（DOL）是一种框架，能够使应用程序（半）自动映射到形状多处理器架构平台。其包含三个基本部分：
<br>
&emsp;&emsp;在应用接口方面：定义了一些列计算和通信的过程，使得SHAPES平台可以使用一些分布式程序和并行化应用。这为程序员提供了方便，让他们不需要知道底层应用详细的知识就能进行编程。 
<br>
&emsp;&emsp;在函数测试方面：为程序员们提供了同步测试代码的可能性。除了测试函数功能以外，这个框架还可以用于获取应用级别的性能参数。
<br> 
&emsp;&emsp;在映射最优化方面：目标是计算一个应用于SHAPES平台的最优化映射。首先，基于XML的格式是允许用户在抽象层面去描述应用和结构信息的。并且，它包含了为了精确评估表现的信息。**
<br><br>
&emsp;&emsp;借用一张图片：<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221651/1b540b94-8e7a-11e6-8a0c-b5574beef662.png">
***
##DOL安装笔记##
###1.安装一些必要的环境。###
<img src="https://cloud.githubusercontent.com/assets/22441228/19221918/0af9c68a-8e7f-11e6-83c0-9b37f88984e4.png">
<img src="https://cloud.githubusercontent.com/assets/22441228/19221925/397af178-8e7f-11e6-9add-066a19e24ed4.png"><br>
**&emsp;&emsp;上述命令使得系统中的软件同步。**
<br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221933/63fc8f74-8e7f-11e6-878e-7c7faaea9ae7.png"><br>
&emsp;&emsp;上述命令意为安装Ant工具，其为一种基于Java的build工具；<br>
&emsp;&emsp;Ant用Java的类来扩展；<br>
&emsp;&emsp;Ant本身就是这样一个流程脚本引擎，用于自动化调用程序完成项目的编译，打包，测试等。其优点有以下四点：<br>
**&emsp;&emsp;跨平台性。Ant是纯java语言编写的，所示具有很好的跨平台性。<br>
&emsp;&emsp;操作简单。Ant是由一个内置任务和可选任务组成的。Ant运行时需要一个XML文件(构建文件)。<br>
&emsp;&emsp;容易维护和书写，结构清晰。<br>
&emsp;&emsp;Ant可以集成到开发环境中。**<br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221962/facb87de-8e7f-11e6-9dc6-c9efa21835b1.png"><br>
**&emsp;&emsp;以上是安装openjdk-7-jdk工具。**<br><br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221977/67cabbfc-8e80-11e6-8882-7d56fd29daab.png"><br>
**&emsp;&emsp;以上是安装解压工具。**
***
###2.将已下载的文件压缩包dol_ethz.zip和systemc-2.3.1.tgz拷贝到虚拟机中去。###
***
###3.解压文件。###
**&emsp;&emsp;新建dol的文件夹以及将dolethz.zip解压到dol文件夹中，文件过多，没有全部截出来。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221986/d787e028-8e80-11e6-8c79-a2e51f4e0817.png">
<img src="https://cloud.githubusercontent.com/assets/22441228/19221988/f23d2ad6-8e80-11e6-9ceb-b48fb05668cc.png">
<br><br>
**&emsp;&emsp;解压systemc，同样因为文件过多，没有全部进行截图。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19221995/266442e0-8e81-11e6-8510-a6143a4f71ac.png">
<img src="https://cloud.githubusercontent.com/assets/22441228/19221997/3cd0938a-8e81-11e6-8da0-8d60fccc21c4.png">
***
###4.编译systemc。###
**&emsp;&emsp;进入systemc-2.3.1的目录下，新建一个临时文件夹objdir，进入该文件夹objdir，运行configure。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222006/6af57744-8e81-11e6-95ed-f8970549301e.png">
<br><br>
**&emsp;&emsp;下图为运行configure之后的截图。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222016/8f1048d4-8e81-11e6-8a01-96a937594609.png"><br><br>
&emsp;&emsp;安装Make工具，下为简介：<br>
**&emsp;&emsp;在Linux和Ubuntu环境中，make工具主要被用来进行工程编译和程序链接<br>
&emsp;&emsp;Makefile文件：告诉make以何种方式编译源代码和链接程序<br>
&emsp;&emsp;make通过比较对应文件（规则的目标和依赖）的最后修改时间，来决定哪些文件需要更新、那些文件不需要更新。**
<img src="https://cloud.githubusercontent.com/assets/22441228/19222040/d95e6a06-8e81-11e6-8499-bdf4d2746e86.png"><br><br>
**&emsp;&emsp;查看文件目录。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222047/fc911ae6-8e81-11e6-84fe-e4bfd93ffb6e.png"><br><br>
**&emsp;&emsp;记录当前的工作路径，有用，以下表示我当前的工作路径为/home/wuxiaojie/systemc-2.3.1**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222052/1e3a0a4a-8e82-11e6-9ea6-efa6af15d610.png">
***
###5.编译dol。###
**&emsp;&emsp;进入刚刚dol的文件夹，修改build_zip.xml文件。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222062/5b07b40e-8e82-11e6-8219-1b9db54c685a.png"><br><br>
**&emsp;&emsp;接下来就是编译了。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222073/9e81f9f6-8e82-11e6-9cda-b9eb6e8bfc05.png"><br><br>
**&emsp;&emsp;下图是编译成功的截图。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222075/be59b62e-8e82-11e6-9a65-0465ada7100c.png">
***
###6.试试运行第一个例子###
**&emsp;&emsp;进入build/bin/main路径下并运行第一个例子。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222084/e4f0211a-8e82-11e6-967d-cade87b39007.png"><br><br>
**&emsp;&emsp;下图是运行成功的截图。**<br>
<img src="https://cloud.githubusercontent.com/assets/22441228/19222090/07daf2d6-8e83-11e6-81e2-302d89709804.png">
***
##实验感想与心得##
&emsp;&emsp;本次实验（其实应该是上次实验）并没有太大的问题，毕竟只是简单的配置环境，其目的也只是为了后续实验做铺垫。不过到让我感受到了实验中一些工具的强大，比如Ant,Make之类的，然而现在还不是很会用，毕竟都是初学者。当然实验中也碰到了些许问题，比如因为不熟悉Ubuntu而导致在修改build_zip.xml文件中的内容时陷入僵局，依靠同学的帮助才解决这个问题。