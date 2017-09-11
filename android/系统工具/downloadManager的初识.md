安卓开发很多时候回使用到下载更新，自己写下载更新的模块也可行，但是系统也为我们提供这样一个服务，专门用来处理下载的任务。这里简单介绍下关于downloadmanager如何下载及源码中的内部结构：
类关系
 class  DownloadManager
     ---static class Request
     ---static class  Query
     ---static class  CursorTranslator extens CursorWraper
分别介绍下各个类的作用
   Request 类是为了请求下载的封装类，包含了下载的URI 及下载完成之后保存文件的URI 下载过程中的设置，是否需要显示状态栏，显示下载信息，网络类型，下载可见与否，及其他和下载前的设置相关的东西。

   Query 是提供下载中或者下载后查询下载状态的封装类，可以设置查询方式，内部有一个使用contentprovider的查询方法，工Query查询当前下载的信息和状态。

   CorsorTranslator 是封装下载过程中各种状态的类，下载出现异常，错误等信息。

DownloadManager 包含三个子类，将下载的信息插入到ContentProvider当中，然后使用Query查询下载的状态。
  下载过程中 如果需要对当前下载的任务，系统提供了一个内容被观察者,只需要实现观察者的一个方法，使用Query就能查询到下载的状态。当然系统每个下载任务下载之后都会发出一个下载完成的广播,所以只需要监听下载完成的广播，然后做判断处理就能知道下载任务是否已经完成。