安卓中经常会遇到消息的传递。例如在处理点事件的时候，从ViewGroup 到View的事件的传递，首先是ViewGroup的dispatchTouchEvent()  再是 onInterceptTouchEvent（） 然后是View的onTouchEvent（） 接着是ViewGroup的OnTouchEvent() 

注意几点：
1.只要是是ViewGroup中的onInterceptTouchEvent()返回true 这就说明这消息被viewGroup处理，调用的是ViewGroup的哦你TouchEvent（）不会再想View子控件传递消息。
2.只要消息没有在ViewGroup中的OninterceptTouchEvent（）处理，效益一定会走 View的OnTouchEvent()处理，如果在消息没有被监听，返回是false，那么就当下Action而言，View不会再接受到其他的动作。直到下一次的Action的到来，这时候会调用ViewGroup的onTouchEvent（）处理，如果没监听，和View一样。如果在View中监听了这个动作，放回是true，那么就这个Action的其他动作，View还是会监听处理。这是ViewGroup的是监听不到这个消息的，因为消息已经被View处理掉了。如果View没有处理ViewGroup会执行onTouchEvent（）检查viewGroup是否监听这个事件，如果监听，处理接下来Action的动作。如果没有，接下来的action剩余动作不再做处理。
3.针对ViewGroup 和 View 都有监听事件，这是怎么处理点击事件呢:
 假设 父控件F  子空间S
  1)F 比S 面积大， a) 都监听事件 点击F 则是F处理事件
                                                    点击S 则是S处理事件
                              b)只有一个监听事件  如果是F 监听，那么无论是点击F 还是S ，会有处理。
                                                               如果是S监听，那么只有在S点击时 才会有处理，点击F时 是没有处理动作的。
   2)F和S面积一样大 a)都监听事件 那么点击的肯定是S。这时处理的是S处理，F 不会处理。
                                b)只有一个监听 那么点击之后都会有动作处理的（因为范围一样大）。

这里介绍个特别的方法：
requestDisallowInterceptTouchEvent （boolean） 
对于底层的View来说，有一种方法可以阻止父层的View截获touch事件，就是调用getParent().requestDisallowInterceptTouchEvent(true);方法。一旦底层View收到touch的action后调用这个方法那么父层View就不会再调用onInterceptTouchEvent了，也无法截获以后的action。 

（这里说的是监听的点击事件，至于OnTouchEvent()方法都是可以执行，只要View没有将消息消耗掉）

用例子总结一下onInterceptTouchEvent和onTouchEvent的调用顺序：
假设最高层View叫OuterLayout，中间层View叫InnerLayout，最底层View叫MyVIew。调用顺序是这样的（假设各个函数返回的都是false）
OuterLayout.onInterceptTouchEvent->InnerLayout.onInterceptTouchEvent->MyView.onTouchEvent->InnerLayout.onTouchEvent->OuterLayout.onTouchEvent。