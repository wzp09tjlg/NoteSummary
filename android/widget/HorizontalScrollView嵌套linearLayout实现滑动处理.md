安卓中使用ListView或者使用GridView时 不能保证滑动之后都是按照自己想要的方式进行滑动。针对特殊的要求，这里实现对滑动之后控制Item微调的处理：
一：明确几个属性
  getX() ;针对触摸点到父控件的X的距离
  getY(); 针对触摸点到父控件的Y的距离
  getRawX();触摸点相对整个窗口的X的距离
  getRawY();触摸点相对整个窗口的Y的距离
  getLeft();  触发事件的控件相对父布局的左边的距离
  getTop();  触发事件的控件相对父控件的右边的距离
 针对HorizontalScrollView控件，有这样几个方法
  horizontalScrollerView.getScrollX();  控件内部的布局X轴上滑动的距离
  horizontalScrollerView.getScrollY();  控件内部的布局Y轴上滑动的距离
  horizontalScrollerView.scrollTo(x,y); 控件内部的布局向X轴滑动x距离，向Y轴滑动y距离。

二：关于实现horizontalScrollview中嵌套布局，左右滑动时item微调处理
A                                 【                                                            】
B                   [____________________________________________________________]
C                               [--左--]        .....................................           [---右--]

其中A是HorizontalScrollView B是嵌套的LinearLayout布局   C是布局中的Item
针对C中的右边Item情况分析 
   int[] posView = new int[2];
   item.getLocationInWindow(posView); //针对Item获取相对界面（window）的位置  
   int widthView = item.getWidth();         //获取Item的宽
   int[] posViewH = new int[2];  
   horizontalScrollView.getLocationInWindow(posViewH); //获取HorizontalScrollView的相对界面的（window）的位置
   int widthViewH = horizontalScrollView.getWidth();
   int intervalRight =  posView[0] + widthView - posViewH[0] - widthViewH; //就是针对整个window来讲item的右边位置到horizontalScrollView右边的位置的间距。 
   if(interalRight > 0 ) // 说明item已经出界，需要进行微调 (就是horizontalScrollview需要向左滑动intervalRight的距离，将Item完整的显示出来)
  { int  scrollX  = horizontalScrollview.getScrollX(); //获取horizontalScrollView的已经在X轴滑动的距离
   horozontalScrollView.smoothScrollTo((scrollX   + intervalRight),0); //这里的滑动是让horizontalScrollView滑动到那位置 }
 
针对C中左边的Item的情况分析：
    int[] posView = new int[2];
    item.getLocationInWindow(posView); //获取item在window中的位置
    int[] posViewH = new int[2];
    horizontalScrollView.getLocationInWindow(posViewH);
    int intervalLeft = posView[0] - posViewH[0];    
    if(intervalLeft < 0 )  //说明item的左边在horizontalScrollView的左边
    { int scrollX = horizontalScrollView.getScrollX();
    horizontalScrollView.smoothScrollTo(scrollX + intervalLeft,0);  //horizontalScrollView 向右移动intervalLeft距离}  

总结下：
  针对View在window的位置 以及触摸点相对父布局的位置，以及触发事件的控件先对父控件的位置。
  然后是针对View相对其他View的移动位置。