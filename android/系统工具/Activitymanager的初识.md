Activitymanager的初识在安卓开发中进程会使用activity，但是真正对于activity的了解基本上也只是在简单的使用层面上的了解，真正的对其有深入的了解还是不够的。所以很有必要针对activitymanager（activity的管理者做一个介绍）
activitymanager 负责activity thread的创建，针对创建的activity的生命周期进行维护，学习activity的静态结构图如下：
http://s8.sinaimg.cn/large/8984d3f3tb53c4aceb5b7&690
 其中绿色的是在SDK中进行暴露的接口或者对象方法，也就是我们能使用的。蓝色表示activity进行操作，比如进程间通信的承载者。真正干活处理动的是红色的activitymanagerService，这个服务是在system_process中，咱们使用的activitymanager是在activity_process中。

针对activitymanager学习的动态序列图（就是使用activitymanager的方法调用及消息(或者是动作的传递)）：
https://github.com/wzp09tjlg/noteResource/blob/master/android/view/c2200c13-9f8d-4bfa-a1f0-9370d2fdc002.gif
在SDK中我们通常使用的是activitymanager，暴露的方法很多，但是常用的总结如下几个：
1.am.getRunningAppProcesses();  //获取当前设备上运行的进程，包括用户启动的 也包括系统启动的
2.am.getRunningServices(num of you wangt to explain); //获取运行的service
3.am.getRecentTasks(number of you want to explain,flag); // 获取最近打开的任务
4.am.getRunningTasks(number of you want to explain);  //获取正在运行的应用的activity 主页
其他还有 5.restartPackage(packageName);   killBackgroundProcesses(packageName);    forceStopPackage(package) ; 这些方法。

总之，activitymanager 是是在sdk层面上暴露出来的类，提供给用户系统的信息，真正的操作都是运行在system_process上的activitymanagerService 操作的。
 
ActivityManager相关

      本类API是对运行时管理功能和运行时数据结构的封装，包括以下功能

    激活／去激活activity
    注册／取消注册动态接受intent
    发送／取消发送intent
    activity生命周期管理（暂停，恢复，停止，销毁等）
    activity task管理（前台－>后台，后台－>前台，最近task查询，运行时task查询）
    激活／去激活service
    激活／去激活provider等

task管理相关API需要特定的权限，具体API可参考SDK文档。