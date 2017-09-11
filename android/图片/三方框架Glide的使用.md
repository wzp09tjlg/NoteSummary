在行移动端开发的时候，经常会使用到图片，而大多数的图片都是从网络上获取得到的，所以针对如何快捷的使用网上的图片，第三方图片框架是不错的选择。当前来讲使用glide的网络框架是比较主流的。
简单介绍下如何使用glide的使用，及简单的api介绍：
1.引入
dependencies {
     compile 'com.github.bumptech.glide:glide:3.6.1'
     }
glide存在很多的版本，建议使用最新的版本，支持更多的功能。
2.使用
    a)可以使用glide默认的属性配置，当然也可以使用自己的重写的GlideModual 来进行特定的配置。
  创建一个 GlideModel子类，在清单文件中 添加进来，如图示：
<!-- 处理的是glide图片处理 -->
<meta-data android:name="com.sina.crowclub.utils.CustomCachingGlideModule"
     android:value="GlideModule"/>
  使用glide时，glide会自动调用配置的属性。
  GlideModual 中需要重写两个方法：
  applyOptions()  和 registerComponents()
  在applyOptions()中 设置公用的属性：
int diskSize = 1024 * 1024 * 100;
int memorySize = (int) (Runtime.getRuntime().maxMemory()) / 8;  // 取1/8最大内存作为最大缓存

// 定义缓存大小和位置
builder.setDiskCache(new InternalCacheDiskCacheFactory(context, diskSize));  //内存中
builder.setDiskCache(new ExternalCacheDiskCacheFactory(context, "cache", diskSize)); //sd卡中

// 默认内存和图片池大小
MemorySizeCalculator calculator = new MemorySizeCalculator(context);
int defaultMemoryCacheSize = calculator.getMemoryCacheSize(); // 默认内存大小
int defaultBitmapPoolSize = calculator.getBitmapPoolSize(); // 默认图片池大小
builder.setMemoryCache(new LruResourceCache(defaultMemoryCacheSize)); // 该两句无需设置，是默认的
builder.setBitmapPool(new LruBitmapPool(defaultBitmapPoolSize));

// 自定义内存和图片池大小
builder.setMemoryCache(new LruResourceCache(memorySize));
builder.setBitmapPool(new LruBitmapPool(memorySize));

// 定义图片格式
builder.setDecodeFormat(DecodeFormat.PREFER_ARGB_8888);
builder.setDecodeFormat(DecodeFormat.PREFER_RGB_565); // 默认
这里需要确认下针对图片的处理，glide是像素色值采用的是RGB565默认，其他的三方框架是ARGB8888，在针对不是特别针对图片要求的情况下，RGB565是完全足够使用的。
在混淆文件中 需要添加混淆文件：
-keepclassnames class * com.sina.crowclib.uitls.CustomCachingGlideModual
PS.Glide底层的网络使用的HTTPURLConnection，针对底层的网络框架，Glide页可以集成了OKHttp 和 Volley。
在集成OKHttp 或者是 Volley时，需要重写GlideModual中的registerComponents();方法
上边所述的设置glide的缓存参数，重写的两个方法中 设置缓存参数，第二个是设置网络的底层框架。
 b.基本使用
   1) Glide.with(Context).load("xx.png").into(ImageView);
   其中Context 是可以有 Context,Activity,FragmentActivity,Fragment;
   加载的目标资源可以有：Uri,uriString,File,Byte[],String;
   加载完之后做什么处理，Glide接受三中参数：ImageView,Target(),into(w,h);
   into(ImageView)是直接将图片加载到ImageView中，into(new SimpleTarget<Bitmap>{...}) 或者是into(new Target<Bitmap>(){...//可以重写加载过程中 加载失败，加载成功，加载被取消等情况的Drawable})  ,into(w,h) 获取到图片之后，针对图片的长宽做缩放处理。
  其中通过into(w,h)的方式需要在子线程中处理，因为处理的过程可能会影响到主线程。
   new Thread(new Runnable(){
    Bitmap bitmap = Glide.with(context).load(url).into(w,h).get();//获取得到w*h的图片   
})  
   2)asBitmap() 默认就是生成bitmap();不用设置
     asGif();生成gif
    3)override(w,h) 设置图片的大小。根据网上的测验，如果加载的图片是500*500，但是override(100,100),加载出来的图片就是100*100.如果加载的图片是720*1280，设置的是720*500，该图片就会根据设置高是500的比例进行缩放。
     4)thumbnail(0.1f);对加载的图片加载缩略图，参数范围在0~1之间。
     5)placeholder(LocalDrawable) 占位图
        eror(LocalDrawable) 发生错误的图片
     6)加载动画
       crossFade()//默认的渐变加载效果
       dontAnimation()//不使用动画
       animate(Animator) 或者animate(animationId) 或者 animate(animation) 设置加载的动画
     7)图片的scaleType 
       centerCrop()长的一边撑满
       fitCenter（）短的一边撑满 
     8)暂停和恢复 加载的动作
       Glide.with(Context).resumeRequest()//恢复加载的请求
       Glide.with(Context).pauseRequest()//暂停加载的请求
     设置滚动加载，不滚动时不加载，提高listview的效率：
     监听滚动： 
       public void onScrollStateChanged(AbsListView view,int scrollState){
       switch(scrollState){
         case SCROLL_STATE_FLING://滑动之后 附带惯性的继续滑动
              Glide.with(getApplicationContext()).pauseRequests();
              break;
         case SCROLL_STATE_IDLE://滑动已经停止
              Glide.with(getApplicationContext()).resumeRequests();
              break;
         case SCROLL_STATE_TOUCH_SCROLL://没有离开屏幕,正在滚动
              Glide.with(getApplicationContext()).resumeRequests();
              break;
       }
      }
      9)在后台线程中进行加载或者缓存
        downloadOnly(w,h) 
        downloadOnly（Target）
        new Thread(new Runnable(){
         public void run(){
          FutreTarget<File> future = Glide.with(context).load(url).doanloadOnly(w,h);
           File cacheFile = future.get();//获取下载的缓存图片  ps.此时下载的图片是以二进制的文件格式下载到磁盘缓存的，是为方便后续使用
          }       
       })
      10）缓存策略
        Glide提供了四种缓存策略(在各个项目中 需要针对各个需求做缓存处理)
         DiskCacheStrategy.NONE;//不缓存
         DiskCacheStrategy.SOURCE;//缓存原始图片
         DiskCacheStrategy.RESULT;//缓存压缩过后的图片
         DiskCacheStrategy.ALL;//两个都缓存
      11)设置转换器
         其实在上边已经介绍图片加载之后的转换效果centerCrop 和 fitCenter
         当然也有其他的集成转换工具
         毛玻璃的转换器效果 BlurTransformation(this,20) 毛玻璃百分之二十的效果
         Glide.with(Context).load(url).bitmapTransform(new BlurTransformation(this,20)).into(ImageView);
         圆角转换器:CropCircleTransformation(this);
         Glide.with(Context).load(url).bitmapTransform(new CropCircleformation(this)).into(ImageView);
                 当然也可以使用多个集成的转换器：
                 Glide.with(Context).load(url).bitmapTransform(new BlurTransformation(this,20)，new CropCircleTransformation(this)).into(ImageView); //叠加了毛玻璃和圆角的转换器
                 Glide中有很多的转换器支持库
                 需要加载
dependencies {
    /** 图片第三发框架 */
    compile 'jp.wasabeef:glide-transformations:1.2.1'//Glide转换器支持库
    compile 'com.github.bumptech.glide:glide:3.7.0'//Glide基本支持库
    compile 'jp.co.cyberagent.android.gpuimage:gpuimage-library:1.3.0'//GPU加速渲染库
}
        简单的效果可见网友的demo效果: http://blog.csdn.net/u014752325/article/details/53178003          
        GrayscaleTransformation(context);//灰白色
        CropTransformation(context);//
       CropSquareTransformation(context);//
        CropCircleTransformation(context);//圆形
    RoundedCornersTransformation(context,50,0);//圆角
        BlurTransformation(context);//毛玻璃
       MaskTransformation(contexy,R.mipmap.ic_launcher);//和给定的图做交集效果
       ToonFilterTransformation(context);//卡通过滤效果
       SepiaFilterTransformation(context);//复古效果
       PixelationFilterTransformation(context);//马赛克效果
    当然这里还有更多的效果，待继续测验：
    SepiaFilterTransformation
         ContrastFilterTransformation
         InvertFilterTransformation
         SketchFilterTransformation
         SwirlFilterTransformation
        BrightnessFilterTransformation
        KuwaharaFilterTransformation
         VignetteFilterTransformation  
    自定义的转换器实现效果如下：
    public static class SelfTransformation extends BitmapTransfrmation{
      public SelfTransformation(Context context){
      super(context);
      }
      //重写两个方法transform() 和 getId()
      protected Bitmap transform(BitmapPool pool,Bitmap toTransform,int outWidth,int outHeight){
      Bitmap selfTransformedBitmap = ...//自己做图片的转换动作，自己裁剪一样
      return selfTransformedBitmap ;
}   
    public String getId(){
      return "com.sina.crowclub.Utils.SelfTransformation"; 
    }
} 
      使用替换的动作和转换库中使用一样
      12)清除缓存
         Glide.get(context).clearMemort();//这个代码必须在主线程中执行
         或者
         new Thread(new Runnable(){
           public void run(){
            Glide.get(getApplicationContext()).clearDiskCache();//在子线程中执行
           }
         })
  



