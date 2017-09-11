安卓中经常会使用到获取View的位置，getX 和 getRawX 方法分别是指：
getX()是表示view相对于parent左上角的x坐标,
getRawX()是表示相对于屏幕左上角的x坐标值(注意:这个屏幕左上角是手机屏幕左上角,不管activity是否有titleBar或是否全屏幕)

其中view.getLeft()  getRight();  getTop()  getBottom()  这四个方法是针对view的父控件来讲的位置。
如果A是全屏的（没有状态栏），B是A中的子控件 ，那么 A.getTop()  A.getLeft()  都是0，A.getRight() A.getBottom()就是这个屏幕的分辨率。
 而B 的getTop() getLeft是相对A 来讲（这里是A是全屏，所以这里是相对圆点来讲。但是如果A不是全屏的，那么B的这些字就会与我们通常的理解有差异，这些都是需要理解。因为所有的子View的大小和布局都是来自其父控件measure之后才会有的，所有他的大小是相当于父控件）
view.getX view.getY这两个方法也是一样的，都是相对于父控件

安卓中获取View在屏幕中的绝对的位置方法是
int[] position = new int[2];
view.getLocationInWindow(position);  //position[0] X 坐标 position[1] Y坐标
int[] location = new  int[2] ;
view.getLocationInWindow(location); //获取在当前窗口内的绝对坐标
view.getLocationOnScreen(location);//获取在整个屏幕内的绝对坐标
location [0]--->x坐标,location [1]--->y坐标

getLocationOnScreen
，计算该视图在全局坐标系中的x，y值，（注意这个值是要从屏幕顶端算起，也就是索包括了通知栏的高度）//获取在当前屏幕内的绝对坐标

getLocationInWindow ，计算该视图在它所在的widnow的坐标x，y值，//获取在整个窗口内的绝对坐标

getLeft , getTop, getBottom,getRight, 这一组是获取相对在它父亲里的坐标