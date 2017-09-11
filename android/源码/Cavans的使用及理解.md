安卓中经常会遇到画某个东西，无论是图片还是其他的文件也好，经常使用到画布。这里做一个简单的介绍：
一般情况下 安卓需要画的内容是2D效果，大部分的Api在android.graphics android.graphics.drawable中，提供了canvas colorFilter point Retcf，还有些动画相关的：animationDrawable，bitmapDrawable，TransitionDrawable等。以图形处理来讲，我们最常使用的就是在一个View上画一些图片，形状或者自定义文本内容，这里我们都是使用canvas来实现，你可以获取View的canvas对象，绘制写自定义的形状，然后调用view的invalidate方法让view重新刷新，然后绘制一个新的形状，这样达到2D的效果。
canvas的获取有两种方式：一种是我们重写View.onDraw方法，view的canvas对象会以参数形式传递过来，我们操作这个canvas，效果就会直接在View中反应出来，另一种就是当你想创建一个canvas对象时使用的方法，通常是画图
   Bitmap bitmap = Bitmap.createBitmap(100,100,Bitmap.Config.ARGB_8888);
上边的代码是创建一个尺寸是100*100 的bitmap图，使用canvas操作对象，这时候canvas就是使用创建的方式。当你创建canvas在bitmap上执行绘制方法后，你还可以将绘制的结果提交另一个canvas，这样就可以达到两个canvas协作完成的效果，简化逻辑。但是android Sdk建议使用View.onDraw参数里提供的canvas就好，没有必要自己创建一个新的canvas对象。通常canvas可以绘制的图形有如下几种：
弧线(arcs) 填充颜色（argb和color） bitmap 圆（circle和oval）点(point) 线（line） 矩形（rect） 图片（picture） 圆角矩形（roundrect） 文本（text） 顶点（vertices） 路径（path）
 对通过位置转换的方式，我们可以画出很多有意思的图片出来，通常的位置转换方法有：ratate  scale translate skew(扭曲)等