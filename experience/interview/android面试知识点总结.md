### android面试知识点总结

####目录：
    1.
    
#### 一：java知识
     1.八种基本数据类型
     2.抽象类和接口区别
     3.重写重载
     4.return break continue
     5.面向对象和面向过程
     6.equal ==
     7.设计模式
     8.string stringbuffer stringbuilder
     9.正则
     10.集合
     11.io
     12.线程
     13.数据库
     14.网络
     15.json html xml
     

#### 二：Android知识：
     1.mvc mvp mvvm
     2.四大组件 生命周期，调用方式。及深度的理解
     3，数据存储 文件，sp ，数据库
     4.线程之间通信 handler机制
     5.intent pendingIntent
     6.动画 帧动画 补间动画 属性动画
     7.Design设计的组件
     8.fragment生命周期
     9.兼容不同版本的方法
     ```java
     在使用高于minSdkVersion API level的方法需要:
用@TargeApi($API_LEVEL)使可以编译通过, 不建议使用@SuppressLint("NewApi");
运行时判断API level; 仅在足够高，有此方法的API level系统中，调用此方法;
保证功能完整性，保证低API版本通过其他方法提供功能实现。

     ```
     10.fragment的坑 replace会重新创建,add 和 show及hide不会重新创建。
     11.事件分发机制
     12.自定义view 及不同手机适配
     13.内存泄露问题，内存溢出问题。
     14.下拉刷新实现方案
     15.jvm 和 Dalvik区别
     16.加密方式 对称加密 des 3des 非对称加密 Ras
     17屏幕适配方案
     18.图片缓存
     19全面屏幕适配 
     ```java
     1、App AndroidManifest的Application标签下面增加下面一段代码：
<meta-data android:name="android.max_aspect" android:value="2.1" />
2、更换部分被拉伸的图片资源文件（相对布局采用XML的方式,或者.9图的解决方案）
3、布局文件的优化建议（使用百分比布局）

     ```
     20.进程间通信方案 及AIDL的实现原理
     

#### 三：计算机网络知识

#### 四：数据结构及算法

#### 五：设计模式
     1.设计原则：单一职责 开闭原则 替换原则 面向接口 拆分接口 依赖抽象而非具体
     2.三类设计模式 创建型 关系型。操作型

#### 六：新的技术思想

    