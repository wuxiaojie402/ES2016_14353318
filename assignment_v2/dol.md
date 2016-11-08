#实验二：DOL实例分析#
***
##实验题目：##
###&emsp;&emsp;DOL实例分析&编程###
***
##实验任务：##
**&emsp;&emsp;1.修改example1，使其输出3次方数。**
<br>
**&emsp;&emsp;2.修改example2，让3个square模块变成2个。**
***
##实验步骤:##
###1.效果截图###
&emsp;&emsp;**1) example1.dot：<br>**
<img src="https://cloud.githubusercontent.com/assets/22441228/19841312/a1808e7e-9f44-11e6-949a-f2e5fcaeee5e.png"><br><br>
&emsp;&emsp;**2) example2.dot：<br>**
<img src="https://cloud.githubusercontent.com/assets/22441228/19841332/1ab75d68-9f45-11e6-9a41-1a141fc72008.png"><br>
***
###2.修改过程###
**example1：<br>&emsp;&emsp;依据实验文档，我们来分析一下这一部分代码，我们查看dot图，发现其中包含生产者、立方模块、消费者、通道C1与C2。<br>**
**&emsp;&emsp;生产者代码：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841373/b3c01f04-9f45-11e6-9009-7c83c07a2109.JPG"><br>
**&emsp;&emsp;定义生产者进程。<br>**
**&emsp;&emsp;初始化进程，设定当前位置为0，并设置生产者长度，此处local指针指向.h文件的local states结构，如下：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841388/fc327610-9f45-11e6-8e47-10aafc1c33ba.JPG"><br>
**&emsp;&emsp;函数generator.fire是信号产生函数，此处代码意为若当前位置小于生产长度，则将x（当前下标）写到generator的端口"PORT OUT"上（即输出端），否则销毁进程。所以，就是让这个程序执行length次后停下来。<br><br>**
**&emsp;&emsp;消费者代码：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841410/6bc5d2f6-9f46-11e6-84a7-23d97664f6b5.JPG"><br>
**&emsp;&emsp;定义消费者进程。<br>**
**&emsp;&emsp;与生产者类似，也是初始化进程。<br>**
**&emsp;&emsp;信号消费函数consumer_fire，类似于信号生产函数，如果当前位置小于设定长度，则读出输入端信号，并且打印（将结构输出到命令行），否则销毁进程。<br><br>**
**&emsp;&emsp;cubic.c文件：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841432/b341b082-9f46-11e6-911b-657f9293b8b7.JPG"><br>
**&emsp;&emsp;定义立方进程。<br>**
**&emsp;&emsp;初始化进程，与上述类似。<br>**
**&emsp;&emsp;信号处理函数，读入输入端信号i，将其立方后写出到输出端，同样，重复length次之后进程停止。<br><br>**
**&emsp;&emsp;example1.xml文件：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841473/307b2844-9f47-11e6-81d6-f18f5f2fb093.JPG"><br>
**&emsp;&emsp;很容易理解，生产者只需要一个输出端口，端口名字为1，消费者只需要一个输入端口，端口名字为1，立方模块需要输入、输出各一个端口，名字分别为1，2。<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841484/54128e64-9f47-11e6-8fb9-a07538087092.JPG"><br>
**&emsp;&emsp;通道C1、C2，方式为FIFO（先进先出），缓冲区大小都为10，通道C1的输入端口名字为0，输出端口名字为1，通道C2一样。<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841491/78289708-9f47-11e6-8c9c-9585a89167bb.JPG"><br>
**&emsp;&emsp;将两个通道与三个模块连接起来，这里仅以一条连线为例，查看dot图，很明显通道C1的输入端口与生产者的输出端口（仅有输出端口）连接起来，所以是生产者模块的"1"端口与通道C1的"0"端口连接起来。而其他三条连线类似，通道C1的输出端口（"1"端口）与立方模块的输入端口（"1"端口）连接起来，通道C2的输入端口（"0"端口）和立方模块的输出端口（"2"端口）连接起来，通道C2的输出端口（"1"端口）和消费者模块的输入端口（"1"端口连接起来）。<br><br>**
**&emsp;&emsp;经过这么多分析，想必大家也看到了修改之前我们所定义的是平方进程，而现如今所需的是立方进程，很明显只需将平/立方进程定义的地方稍作修改即可。<br>**
<img src="https://cloud.githubusercontent.com/assets/22441228/19841503/9df341d6-9f47-11e6-9f54-0b389afa794c.JPG"><br><br>
**example2：<br>&emsp;&emsp;这个实例中生产者、消费者、平方模块和未修改的example1是一样的，区别就在于布局文件example2.xml，此处我们需要2个square模块，所以我们需要迭代2次。<br>**
**&emsp;&emsp;首先定义一个变量N，设定值为2.<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841509/d8cd7b00-9f47-11e6-8c50-04ecff5c6596.JPG"><br>
**&emsp;&emsp;接下来就是定义模块及通道端口了，首先是生产者、消费者，前者定义输出端口"10"，后者定义输入端口"100"，因为需要两个平方模块，所以利用迭代函数，定义两个模块、四个端口。虽说名字有差别，但输入端口、输出端口都是"0"、"1"端口。定义3条通道，同样设定输入端口及输出端口。查看dot图，我们需要6条连线，如下：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/19841523/07115842-9f48-11e6-8735-18c28427c111.JPG"><br>
**&emsp;&emsp;此处只列举两条连线，分别是第一条通道的输出端口（"1"端口）和第一个平方模块的输入端口（"0"端口）的连线和第二条通道的输出端口（"1"端口）和第二个平方模块的输入端口（"0"端口）的连线。另外四条不外乎就是第二条通道的输入端口（"0"端口）和第一个平方模块的输出端口（"1"端口）的连线、第三条通道的输入端口（"0"端口）和第二个平方模块的输出端口（"1"端口）的连线、第一条通道的输入端口（"0"端口）和生产者的输出端口（"10"端口）、第三条通道的输出端口（"1"端口）和消费者的输入端口（"100"端口）。<br><br>**
**&emsp;&emsp;想必大家也知道了在修改之前的example2是迭代3次，所以所设的N值是3，那是定义了3个平方模块，4条通道，而应实验要求，N值修改为2。**
***
##实验感想:##
&emsp;&emsp;本次实验相对来说比较简单，其一在于实验任务中已经指明了在哪里修改，我们所需要做的无非就是运行一下修改后的代码及简单写一下实验报告罢了，其二在于TA在上课的时候已经将所有的代码帮我们分析了一遍，更遑论实验文档中叙写的明明白白。当然，再简单的实验题也是会遇到问题的，大部分人的问题就是明明修改了，但结果却没有变，这就是TA上课所提到的了，在每一次编译得到结果后都要把/build文件夹中编译之后的文件删掉再去修改/src中的实例。在TA说完若是能自己加点变化有加分后，我就尝试着把代码中的square修改成cubic，于是要不就是这里漏改了，要不就是那里漏改了，简直要崩溃了。
在做完这次实验后，我们会发现代码的运行与大二的操作系统是类似的，但正如第一次实验所述，分布式操作系统是由三个基本组成部分的：应用接口部分（这里是在.xml文件中定义的），函数方面（例如实验的三个模块：生产者、消费者、平方模块），映射方面（本次实验就是.xml文件中的connection部分），比我们原先学的操作系统更特殊了一点。