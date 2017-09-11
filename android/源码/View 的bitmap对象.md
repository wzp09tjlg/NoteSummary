在安卓中 获取一个view的bitmap对象方法有如下一种，想将view的cache设置true再将缓存取出bitmap来
具体方法是;
View组件显示的内容可以通过cache机制保存为bitmap, 主要有以下方法:
void  setDrawingCacheEnabled(boolean flag), //必须先设置可以开启，记得在使用之后关闭
Bitmap  getDrawingCache(boolean autoScale), //然后开始获取，如果没有会自动调用build*方法
void  buildDrawingCache(boolean autoScale),   //使用得很少
void  destroyDrawingCache() //如果之前的已经取过缓存，再次取的法 要将缓存先destory，然后会重新建立
我们要获取cache首先要通过setDrawingCacheEnable方法开启cache，然后再调用getDrawingCache方法就可以获得view的cache图片了。

buildDrawingCache方法可以不用调用，因为调用getDrawingCache方法时，若果cache没有建立，系统会自动调用buildDrawingCache方法生成cache。

若想更新cache, 必须要调用destoryDrawingCache方法把旧的cache销毁，才能建立新的。
当调用setDrawingCacheEnabled方法设置为false, 系统也会自动把原来的cache销毁。

   
另外，ViewGroup在绘制子view时，也提供了两个方法

void setChildrenDrawingCacheEnabled(boolean enabled) 

setChildrenDrawnWithCacheEnabled(boolean enabled) 

setChildrenDrawingCacheEnabled方法可以使viewgroup里所有的子view开启cache;

setChildrenDrawnWithCacheEnabled使在绘制子view时，若该子view开启了cache, 则使用它的cache进行绘制，从而节省绘制时间。

获取cache通常会占用一定的内存，所以通常不需要的时候有必要对其进行清理，通过destroyDrawingCache或setDrawingCacheEnabled(false)实现。