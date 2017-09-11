安卓开发中经常会涉及到安卓的层次，Linux内核  核心库 框架成 应用层，
做应用 基本都是在应用层上忙活，对于框架层的理解和认识不够，因此在未来的一段时间内 ，方向和任务还是继续向框架层进步。

框架层的功能;
 Framework层为我们开发应用程序提供了非常多的API，我们通过调用特殊的API构造我们的APP，满足我们业务上的需求。写APP的人都知道，学习Android开发的第一步就是去学习各种各样的API，什么Activity,Service,Notification等。这些都是framework提供给我们的，那么我就详细的讲讲Framework到底在整个Android架构中扮演着什么角色.

Framework其实可以简单的理解为一些API的库房，android开发人员将一些基本功能实现，通过接口提供给上层调用，可以重复的调用

         我们可以称Framework层才真正是Java语言实现的层，在这层里定义的API都是用Java语言编写。但是又因为它包含了JNI的方法，JNI用C/C++编写接口，根据函数表查询调用核心库层里的底层方法，最终访问到Linux内核。那么Framework层的作用就有2个。

1.用Java语言编写一些规范化的模块封装成框架，供APP层开发者调用开发出具有特殊业务的手机应用。

2.用Java Native Interface调用core lib层的本地方法，JNI的库是在Dalvik虚拟机启动时加载进去的，Dalvik会直接去寻址这个JNI方法，然后去调用。

        2种方式的结合达到了Java方法和操作系统的相互通信。Android为什么要用Java编写Framework层呢？直接用C或C++不是更好？有关专家给出了如下解释：

      C/C++过于底层，开发者要花很多的经历对C/C++的语言研究清楚，例如C/C++的内存机制，如果稍不注意，就会忘了开启或者释放。而Java的GC会自动处理这些，省去了很多的时间让开发者专注于自己的业务。所以才会从C/C++的底层慢慢向上变成了JAVA的开发语言，该层通过JNI和核心运行库层进行交互。

         其实这些也是Java能发展这么迅速的原因，面对对象语言的优势。不用太关注内存，放心大胆的去做实现，才有时间去创造新的事物。

  常用框架层提供的几个类：

Activity Manager

 用来管理应用程序生命周期并提供常用的导航回退功能。

 Window Manager

 提供一些我们访问手机屏幕的方法。屏幕的透明度、亮度、背景。

 Content Providers

 使得应用程序可以访问另一个应用程序的数据（如联系人数据库)， 或者共享它们自己的数据。

 View System

 可以用来构建应用程序， 它包括列表（Lists)，网格（Grids)，文本框（Text boxes)，按钮（Buttons)， 甚至可嵌入的web浏览器。

 Notification Manager

 使得应用程序可以在状态栏中显示自定义的提示信息。

 Package Manager

 提供对系统的安装包的访问。包括安装、卸载应用，查询permission相关信息，查询Application相关信息等。

 Telephony Manager

 主要提供了一系列用于访问与手机通讯相关的状态和信息的方法，查询电信网络状态信息，sim卡的信息等。

 Resource Manager

 提供非代码资源的访问，如本地字符串，图形，和布局文件（Layout files )。

 Location Manager

 提供设备的地址位置的获取方式。很显然，GPS导航肯定能用到位置服务。

 XMPP

可扩展通讯和表示协议。前身为Jabber，提供即时通信服务。例如推送功能,Google Talk。
 
 
