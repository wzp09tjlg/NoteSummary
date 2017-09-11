在安卓中，view是所有widget的基类，想要理解各种widget的实现和原理，理解view是必不可少的。
view中 会有很多种状态，使用的是十六进制的状态码来表示，针对每种状态的设置使用 | 和 & 来设置其状态和取消其状态。
view表示可以绘制的一个区域，这个区域的大小是相对view的parentView的位置来确定的，就是说这个view实在一个rectR方形区域中进行不断的绘制，不管这个view是多么的复杂还多么简单，通过不断的连续的绘制，以达到视觉效果。（这里可以提下安卓中的线程：主线程和子线程；主线程就是针对当前窗体，不断的进行绘制，主线程很忙，因为它一直在连续不断的绘制图，不能有空闲的时间去做其他的事情。所以安卓这里需要理解的是主线程是做UI绘制的，并且也只有主线程做UI绘制，其他线程不允许做UI得绘制。子线程是做其他的（耗时）操作。当然这里就牵扯到线程之间的通信，handler + message 来处理主线程和子线程之间的通信handler是（默认是在)主线程中的，handler的handlemessage()就是在主线程中进行调用。所以在子线程中需要对UI进行操作，就需要发一个消息Message，然后通过handler去传递。然后将数据或者是执行UI操作切断到主线程实现）

一：
view是一个区域，用来显示需要显示的效果所以就不断的绘制，因此这里就需要对绘制的过程做一个了解：
layout() --> draw()
layout()方法是framwork层调用的方法，在view的layout方法中，查看远吗有这样几个方法：onmeasure()和onlayout()方法，onmeasure()方法是针对view的大小进行测量，计算区域的大小是多少。这里就涉及到定义view大小的三种方式：精确，最大，未告知。设定大小之后一定需要调用setMeasureDiemens(int,int);方法来告诉系统，view大小是多少。
其次是onlayout()方法，onlayout()方法就是对view的一些属性进行设置，大小及左上右下的属性等等。

然后是draw()方法，draw()也是framwrok层调用的，在draw()方法中调用了ondraw()方法，在view中这是一个空方法，需要在子类中进行实现。类似一个TextView中每次text的设置，都会对text进行设置然后进行重绘制。这样就能显示textView的效果来了(当然这里的重新绘制肯定绘制了很多的东西padding margin等其他的效果)。

二：
关于view的消息机制，每个view都不可能是独立的存在，因为需要同其他的view及实例进行通信，所以这里就需要使用到消息机制。
view的消息机制需要理解几个方法：
dispatchTouchEvent(),进行消息的分发.
onTouchEvent()进行对事件的监听,一般需要做监听的事件有MotiveEvent.ACTION_DOWN,MotiveEvent.ACTION_MOVE,MotiveEvent.ACTION_CANCEL,MotiveEvent.ACTION_UP这样几个事件。
当然还可以注册其他的处理事件，譬如:onTouchListener,onClickListener等。
这几个事件的执行顺序是首先由dispatchTouchEvent()将消息分下下去，onTouchListener()监听消息，然后是onTouchEvent()等事件，对于onClickListener是在onTouchEvent()中ACTION_UP之后进行调用的。
消息传递的过程中只要有一个动作将消息消耗掉了，那么后来的动作就监听不到这个消息的。

整个view的东西和理解。希望以后再次深入时对上述不完善或者错误的描述做些修改。


