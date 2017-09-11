安卓中activity是承载于用户交互的唯一介质，绝大部分的应用程序中都会是需要activity的。
最近看源码从基础看起，activity是一个必经之路。PS说个题外话，就是在看代码的时候，第一个源码时View，这个源码有两万行，可真是长。虽然看得很粗糙，但是还是把其中的那些方法名看了一遍，把计算布局绘制及消息看了下。也很庆幸一直把这个view源码看完，虽然看完之后啥也没记住，但是针对能看完两万行的代码可以给人带来很大的信心的，于是再在以后看其他的源码时 发现行数就几千行，最多一万来行，简直是小巫见大巫。所以看起来就很轻松。当然也蛮有挑战的，就是看两万行代码就不能半途而废，不然以后看其他的代码会有阴影。

一：
层次关系
Context
 --ContextWrapper
 --ContextThemeWrapper
--Activity
简单对这几个类简介：
Context类是个抽象类，这个类中定义的基本都是抽象方法，方法大体可以分成这样几个分类：
获取资源，启动Activity，启动广播，注册广播，启动服务，权限这块。
ContextWrapper类是实现Context的子类，实现了Context的抽象方法，当然主要的方法还是分父类的几块。
ContextThemeWrapper 是ContextWrapper的子类，主要是针对主题做处理。
Activity是ContextThemeWrapper的子类，这里边有生命周期的概念，需要对在Activity中的window分发消息的动作，设置一些状态和属性，及对启动模式等的处理。

PS.对View Window Activity 关系做一个简单的介绍：
View 就是一个可以绘制的区域，是widget的基类。
window:是一个包含多个View及Layout参数的类，window中有一个treeView,treeView 的 root view 叫ViewRoot，也就是我们在window中经常用到的getDecoWindow();
Activity 中包含一个(是不是只包含一个待再深入研究)window,一个WindowManager,windowManager是当前应用管理Window的类，系统的WindowManager是得通过getSystemSevice()来获取的一个服务。
总之，每个window对会对应一个Window对象，一个根view和viewRoot对象。想要创建一个窗口，使用windowManager.addView();来将view添加到window的根view上。

二：
关于对activity的理解：
因为activity是一个包容很多东西的类，所以在这个类中需要对各种组件进行消息的分发及状态的控制。所以在源码中有很大一部分是做的这样的工作。
然后是针对activity生命周期：
简单的讲:
onCreate()
onStart()
onResume()
onPuase()
onStop()
onDestry()  
------------------------onRestart()
在Activity中会有主线程在一直绘制view，activity生命周期中的方法是在主线程中调用的，所以在主线程中不能进行长时间的动作，比如进行网络的请求数据库的查看等等耗时操作。在activity中进行交互的时间超过5秒就会出现ANR。在广播接受者中如果超过10秒也会出现ANR。

