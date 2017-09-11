jni是Java native interface的缩写，意思就是调用本地的接口，这个接口就是使用cpp来实现的，为什么会使用jni，意义在于系统本身大部分是有cpp来编写的，所以就会出现调用系统提供的方法，来快速实现。

Jni 总结
   1.本地需要配置NDK的环境  记住这个路径下不允许于空格
   2.创建本地方法名之后 需要在工程文件下 手动的 编译 
D:\eclipse_workspace1\TestForJni>javah -classpath bin/classes -d jni com.example
.testforjni.JniClient
  然后刷新下工程就能生成相应的jni文件夹 和。H文件
   3.再 android Tool-->add Native library... 
   4.在使用的时候 记得在本地方法中 加入 
   static{
    System.loadLibrary("TestForJni");
    }
    注意这里的名字是有大小写之分的  