按住开发中经常需要自定义view，自定义view通常的做法是继承原来已经存在的view，或者是通过组合的方式去组合view，最后一种就是自己去画view。所以安卓系统提供的原生态的view都是安卓自己自定义画出来的。

一：
自定义view三个构造方法，一定都得写。并且是必须调用super(params);才能创建成功，不然在使用时就是空指针的错。

二：
自定义属性，首先在value中进行声明，然后再在自定义控件中加载进来。记得typearray的释放，不然会有内存泄漏。

三：
绘制的基础。系统为我们提供了onmeasure 和 ondraw方法，执行顺序是 layout-->onmeasure onlayout draw-->ondraw
系统为我们提供canvas（画布），然后只要我们在onmeasure中计算我们希望画的尺寸，然后在ondraw中画出我们希望画出的东西就可以。
paint是画笔，在画布上进行绘制的工具，rect是一个区域，绘制的时候是在画布的一个区域中进行绘制。这就是自定义view绘制自己需要的图像的基础。

四：
onMeasure 和 onDraw方法
onMeasure（）方法是计算我们的view需要多大的尺寸，参数会有两个参数 (int widthMeasureSpec, int heightMeasureSpec)
这两个参数 是为计算尺寸的大小和模式 的参数，不是我们在布局中设置的大小。

20160711补：
1.试用系统的measure进行测量，是系统自己去测量的。所以在调用super.Measure(measureSpecWidth,measureSpecHeight);
之后可以获得相应的宽高值。getWidth() getHeight() getMeasureWidth() getMeasureHeight() 才有值。
2.如果是自己进行计算view的大小，首先需要获取定义的view测量是什么模式，获取模式的方式是
MeasureSpce.getMode(); 来获取测量的模式，然后再获取测量的大小MeasureSpec.getSize(); 
如果是自己测量view的大小 通过getWidth() getHeight() getMeasureWidth() getMeasureHeight() 是获取不到大小。
必须先进行 测量 然后进行设置setMeasureDimension(width,height); 最后使用获取宽高 才会有值，并且 通过日志显示测量的方法不止调用一次。

计算自定义view的大小有几种模式 a.精确值 b.最大值 c.未确定
我们在布局中经常使用的 match_parent 和 确定的大小 就是精确值模型，wrap_content就是 最大值 
几个常用的方法
getWidth();//获取自定义view的宽
getHeight();//获取自定义view的高
getMeasureWidth();
getMeasureHeight();
MeasureSpec.getMode();
MeasureSpec.getSize();
上边的几个方法都是获取自定义view的大小。都是在整个decView计算大小时才会计算到自定义view的大小。

onDraw()方法 是进行绘制的方法，在这个方法中需要自己将需要绘制的图像 文字 曲线，或者其他系统提供的基础东西，然后组合绘制成你所需要的图案。（这里说道在ondraw方法中多次绘制同一个图案，是说图案变化时是多种图案绘制的深浅来组成的，所以这里说是多次(不同的画笔)绘制）

五:
涉及到了几个方法：
一般针对我们自己来实现的view 一般都会要提供共有的 可设置的属性，然后自定义的view进行修改属性 再重新绘制，就能展示不通过的状态来。
requestLayout()方法调用之后会调用view的layout方法，从onmeasure到ondraw都会走一遍。
invalid方法是只会进行重新绘制，走draw()方法，进行ondraw绘制。
设置属性之后 需要要求自定义的view进行重绘制，这里需要做处理
例如设置一个alpha（float alpha）方法。然后这个方法中需要要求view进行重绘
一般会重写这样一个方法
invalidateView(){
if(Looper.getMainLooper == Looper.getMyLooper){
 invalidate(); //是在主线程中，就可以直接要求绘制
}else{
  postInvalidate();//不是在主线程中，这里是发送一个消息，要求主线程进行重绘自定义的那个view
}
}

六：
在自定义view中通常会涉及到一些状态的保存，这里需要重写两个方法：
    private static final String INSTANCE_STATE = "instance_state";
    private static final String STATE_ALPHA = "state_alpha";

    @Override
    protected Parcelable onSaveInstanceState() {
        Bundle bundle = new Bundle();
        bundle.putParcelable(INSTANCE_STATE,super.onSaveInstanceState());
        bundle.putFloat(STATE_ALPHA, mAlpha);
        return bundle;
    }

    @Override
    protected void onRestoreInstanceState(Parcelable state) {
        if(state instanceof  Bundle){
            Bundle bundle = (Bundle)state;
            mAlpha = bundle.getFloat(STATE_ALPHA);
            super.onRestoreInstanceState(bundle.getParcelable(INSTANCE_STATE));
        }else{
            super.onRestoreInstanceState(state);
        }
    }

因为在有些时候 整个view可能也会想其他的activity被销毁，所以这里需要自己做这样一个处理。