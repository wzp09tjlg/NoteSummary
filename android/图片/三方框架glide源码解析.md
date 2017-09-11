Glide是一个很强大的图片从处理框架，
基本思路和ImageLoader 及Paciso等网络框架类似。都是先将要请求的资源在内存及磁盘中进行查询，如果不存在再进行网络请求的过程。
Glide虽然也是实现这样一个简单的过程，但是支持多种类型及提供多种结果的数据类型，功能完全盖过了其他三方的图片处理框架。所以值得去深究下源码：
源码很难，也没完全看懂，自己去深究之后，页通过网上的其他小伙伴写的博客，整理除了这样一篇针对Glide的源码框架。
Glide的基本用法：
Glide.with(Context).load(url).into(ImageView);
主要特点：
1.支持Memory 和 Disk的缓存。并且可以自己去配置缓存的大小及位置。
2.支持gif 和 webp格式的图片。其他的框架貌似是没有的支持的。
3.可以根据传入的Context，根据Context的生命周期动态控制Glide请求的生命周期。 这是非常强大的功能，能够很方便也很便捷的处理了针对网络请求耗费有限资源的难题。其他框架是没有这样的功能。
4.提供了BitmapPool，支持多种图片缓存策略，达到Bitmap的复用。其他的网络框架是不存在的。
5.对Bitmap的回收，可以很好的处理耗费内存的图片难题。

整体的设计：
                       http://caij.github.io/image/glide/design.png

涉及到上图中的基本概念：
requestManager，请求的管理类，每个Activity度会创建一个RequestManager，维护这个Activity中的request。便于Activity的生命周期对请求的控制。
Engine:加载图片的引擎，根据Request创建EngineJob 和 DecodeJob
EngineJob：图片加载
DecodeJob:图片处理

整体的流程：
http://caij.github.io/image/glide/all_sque.png

其实获取图片的流程和ImageLoader 类似，但是因为中添加了其他的控制，请求的生命周期及BitmapPool的控制，流程类似，源码实现大有不同。
针对请求的流程判断如下：
RequestManager创建流程图

其中几个重要的点如下：
1.如果在内存及磁盘中没有找到请求的资源，就会创建一个Request，添加到RequestManager中，进行请求。获取资源。
2.请求的Request封装到EngineJob中，然后使用Java自带的HttpUrlConnection的网络框架进行请求。
3.请求回来之后，将获得数据资源缓存内存及磁盘中，及genuine设置的缓存策略将图片缓存到图片缓存池中。
4.load()方法中做了很多的动作，之后做的变换或者是动画操作都是针对获得数据之后做的操作。