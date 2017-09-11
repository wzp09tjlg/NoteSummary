在安卓开发中经常会使用到额外的文件，配置文件，音乐文件，其他的xml文件等。这些文件都能 放在raw 或者是asset文件下，那么针对这两个文件夹有什么区别呢？这里做一个小结：
（如果是想要把数据库文件或者是其他文件顺带apk一块发布出去的法，这些文件应该放在raw文件下。分析如下）
res/raw 和 assets 区别 
*res/raw 和 assets 的相同点: 
            1. 两者目录下的文件在打包后会原封不动的保存在 apk 包中,不会被编译成二进制。 
 *res/raw 和 assets 的不同点: 
            1. res/raw 中 的 文 件 会 被 映 射 到 R.java 文 件 中 , 访 问 的 时 候 直 接 使 用 资 源 ID 即R.id.filename ; assets 文 件 夹 下 的 文 件 不 会 被 映 射 到 R.java 中 , 访 问 的  时 候 需 要AssetManager 类。 
            2.res/raw 不可以有目录结构,而 assets 则可以有目录结构,也就是 assets 目录下可以再建立文件夹 
*读取文件资源: 
1.读取 res/raw 下的文件资源,通过以下方式获取输入流来进行写操作InputStream is = getResources().openRawResource(R.id.filename); 
2.读取 assets 下的文件资源,通过以下方式获取输入流来进行写操作 
AssetManager am = null; 
am = getAssets(); 
InputStream is = am.open("filename"); 
(用于内置文件但不知道文件名称,需要筛选出想要的文件然后拷贝到目标目录中,推荐内置在 assets 文件夹中) 
1.res/raw 目录: 
通过反射的方式得到 R.java 里面 raw 内部类里面所有的资源 ID 的名称,然后通过名称获取资源 ID 的值来读取我们想要的文件。 
2.assets 目录: 
getAssets().list("");来获取 assets 目录下所有文件夹和文件的名称,再通过这些名称读取我们想要的文件。另,在处理 asset 时,android 限制最大的数据是 1M,超出后会报错误。

来源： <http://www.open-open.com/lib/view/open1328776151311.html>
 