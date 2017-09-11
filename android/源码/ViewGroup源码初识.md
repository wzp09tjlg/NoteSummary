按住中一个存在的view不能都是一个单独的view，很多时候是多个view组成在一起的。这时就需要认识viewgroup。viewgroup是view的子类，可以这样理解viewgroup是存放view的一个容器，在viewgroup中有一个数组来存放加入进来的view。然后对加入进来的view做统一管理(这里管理设计到事件,焦点,绘制等)。

一：
初识viewgroup，一个继承view的子类。也可以理解成一个区域，不过是这个区域中需要画多个view。
viewgroup中几个方法:layout()  draw()方法，
layout()中调用onmeasure()方法，对viewgroup进行测量
onLayout()是一个抽象的方法，继承viewgroup的子类必须重写这个方法，对子view进行布局。
draw()方法中调用ondraw()方法，然后对自view进行绘制。

二：
viewgroup的消息机制
类似view的消息传递机制，但是在viewgroup中新加了intercepTouchEvent()方法，这个方法主要是针对这个消息是否需要自己viewgroup中自己消耗，如果自己消耗这个消息，那么在会在interceptTouchEvent()方法会返回true.
在viewgroup中有这样一个参数，是用于父viewgroup中需要这个事件，自view中年也需这个事件。有这样一个方法requestDisallowInterceptTouchEvent()用于设置这种情况，父view收到这个消息，子view也能收到这个消息。
例子：
一个viewgroup中存放了一个子view，子view监听了onTouchListener()方法，于是做一个事件的传递有如下:
dispatchTouchEvent() ----viewGroup
onInterceptTouchEvent() ---viewGroup
dispatchTouchEvent()  --view
onTouchListener()        --view
onTouchEvent()            --view
onTouchEvent()            --viewgroup

三：
因为viewgroup是一个对view存放的容器，所以很多状态和事件，都会从viewgroup这个父控件去分发下去，所以在看veiwgroup的源码时会有很多的dispatch-的方法。