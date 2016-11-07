#实验三：死锁分析#
***
##实验题目:##
###&emsp;&emsp;代码之Deadlock分析###
***
##实验步骤:##
###1.效果截图###
&emsp;&emsp;**1) 第169次产生死锁:<br>**
<img src="https://cloud.githubusercontent.com/assets/22441228/20047431/46b48ee0-a4ef-11e6-9515-9ad847229ec4.JPG"><br><br>
&emsp;&emsp;**2) 第249次产生死锁:<br>**
<img src="https://cloud.githubusercontent.com/assets/22441228/20047438/5af2f2d4-a4ef-11e6-9e83-9828eaca999e.JPG"><br>
***
###2.死锁产生的四个必要条件###
&emsp;&emsp;**我们清楚死锁是指两个或者多个进程，互相请求对方占用的资源而导致的。在上学期的操作系统课上，我们了解了死锁产生的四个必要条件:<br>
&emsp;&emsp;1) 互斥条件：一个资源每次只能被一个进程使用<br>
&emsp;&emsp;2) 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放<br>
&emsp;&emsp;3) 不剥夺条件：进程已获得的资源，在未使用完之前，不能强行剥夺<br>
&emsp;&emsp;4) 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系<br>**
***
###3.解释产生死锁的原因###
**&emsp;&emsp;首先我们来看一份代码：<br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/20047468/9e086c84-a4ef-11e6-8c3c-85e281ea9e44.JPG"><br>
**&emsp;&emsp;这里定义了两个类，在下面的函数运行中会用到。我们不需要管函数的内容，只需注意函数名前的修饰词：synchronized，我们可以认为这个关键字是用来给对象或是代码进行加锁的，当它锁定一个方法或是代码块时，同时最多只能有一个线程执行该方法或代码块，其他要访问该方法或是代码块的线程只能等待，即进入临界区。<br><br>**
&emsp;&emsp;<img src="https://cloud.githubusercontent.com/assets/22441228/20047483/b61a3078-a4ef-11e6-9b82-7cf7e0234e60.JPG"><br>
**&emsp;&emsp;接下来是运行的主类，首先新建两个类。然后进入主线程Deadlock，创建一个子线程t，因为优先级的原因，所以会继续运行主线程，接着设定count值为500000，然后子线程t进入就绪状态，主线程进入while循环中，受多级反馈调度机制，主线程的优先级会不断降低，直至被线程t抢占（当然，一开始是不可能的，毕竟谁也不会设一个很大的count值吧）。而在循环结束后，主线程将执行函数methodA，于是主线程获取了锁a，同时类a里的函数不能被任何线程执行，在执行完函数后，锁a被释放，这时执行子线程，获取锁b，又释放锁b。其后又创建主线程Deadlock，循环往复，而当主线程又一次被创建后，在循环结束后，其与子线程的优先级已经非常接近了，这时，很有可能在主线程Deadlock获取了锁a后，准备运行函数methodA里的内容时，优先级低于子线程的优先级，于是悲催了，子线程抢占了主线程Deadlock，同时执行类b中的函数methodB，从而获取了锁b，这时就尴尬了，子线程在执行函数methodB时，必须调用函数a.last，而其除线程Deadlock，不能被任何线程执行，被阻塞，同时，想运行的主线程想执行函数methodA，也必须调用函数b.last，同样被阻塞，满足产生死锁的四个条件，从而产生了死锁。<br><br>**