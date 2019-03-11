#### 整理的Android面试技术点

#### 目录
    1.
    
#### 一：
     1.lru算法
     2.binder机制
     3.EventBus实现原理 及 为什么不能夸进程
     4.Handler机制，如何在handleMessage之前拦截发出的消息
     5.二分法查找 冒泡，快速，插入，选择
     6.threadLocal原理
     7.夸进程通信方式
     
#### 二：
     1.handleThread原理
     2.Mvp设计模式 Mvc模式 mvvm模式
     3.kotlin协程
     4.堆内存，栈内存 。栈内存如何转换成堆内存。内存泄露是在什么位置。
     5.leakCannary原理
     6.LinkedHashMap 和HashMap底层实现
     7.字符串分配内存及定义方式
     
#### 三：
     1.为什么建议equal方法需要重写hashCode
     2.Handler机制
     3.Service与activity 通信
     4.HashMap实现原理，及散列碰撞问题。为什么底层不是线程安全的？
     5.Http 和https的握手及挥手
     6.HandleThread 的优势 及相对Thread的好处
     7.eventBus原理
     8.Handle postDelay实现原理
     9.Application启动过程
     10.测试应用启动事件（打桩和命令）
     11时间复杂度和空间复杂度
     
#### 四：
     1.断点续传
     2.代理模式和装饰器模式区别
     3.app启动优化点
     4.android 5.0-8.0新特性
     5.Dalvik和Art区别
     6.进程保活
     7.retrofit createApi实现原理
     
#### 五：  
     1.retrofit实现文件上传
     2.自定义属性attr 及是否可以系统同名
     3.自定义view的测量方式，及测量模式
     4.为什么looper.loop没有卡死。 因为linnux在创建是会生成一个pipe管道，这个管道可以使消息空闲时主线程处于空闲等待状态，wait，有消息时会通知唤醒主线程开始处理消息。
     5.web view拦截url 和 cookie
     6.多线程处理数据库问题
     7.应用如何处理应用内存限制问题：多经进程
     8.大图加载
     9.引用分类，弱应用使用场景
     10.handler的延迟消息 如何不阻塞ui线程
     
#### 六：
     1.Rxjava 的变换操作符号：map flatMap concatMap buffer
```java
     
     常用的变换操作符
map：【数据类型转换】将被观察者发送的事件转换为另一种类型的事件
flatMap：【化解循环嵌套和接口嵌套】将被观察者发送的事件序列进行拆分 & 转换 后合并成一个新的事件序列，最后再进行发送
concatMap：【有序】与 flatMap 的 区别在于，拆分 & 重新合并生成的事件序列 的顺序与被观察者旧序列生产的顺序一致
flatMapIterable：相当于对 flatMap 的数据进行了二次扁平化
buffer：定期从被观察者发送的事件中获取一定数量的事件并放到缓存区中，然后把这些数据集合打包发射

```
     2.装饰器和代理模式的区别
     
```java
     代理模式，注重对对象某一功能的流程把控和辅助。它可以控制对象做某些事，重心是为了借用对象的功能完成某一流程，而非对象功能如何。
装饰模式，注重对对象功能的扩展，它不关心外界如何调用，只注重对对象功能的加强，装饰后还是对象本身。
所以：
对于代理类，如何调用对象的某一功能是思考重点，而不需要兼顾对象的所有功能；
对于装饰类，如何扩展对象的某一功能是思考重点，同时也需要兼顾对象的其它功能，因为再怎么装饰，本质也是对象本身，要担负起对象应有的职责
```
     3.HashMap如何实现一个Key对于多个valueshi
     实现方案 HashMap + ArrayList
     
     4.Android中ClassLoader的种类&特点
```java
     BootClassLoader（Java的BootStrap ClassLoader）
用于加载Android Framework层class文件。
PathClassLoader（Java的App ClassLoader）
用于加载已经安装到系统中的apk中的class文件。
DexClassLoader（Java的Custom ClassLoader）
用于加载指定目录中的class文件。
BaseDexClassLoader
是PathClassLoader和DexClassLoader的父类。

因为遵循双亲委派模型，Android中的ClassLoader具有两个特点：

类加载共享
当一个class文件被任何一个ClassLoader加载过，就不会再被其他ClassLoader加载。
类加载隔离
不同ClassLoader加载的class文件肯定不是一个。举个栗子，一些系统层级的class文件在系统初始化的时候被加载，比如java.net.String，这个是在应用启动前就被系统加载好的。如果在一个应用里能简单地用一个自定义的String类把这个String类替换掉的话，将有严重的安全问题。
```
     
     
#### 总结
    引用：https://www.jianshu.com/p/57ba1ed23c49?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation    