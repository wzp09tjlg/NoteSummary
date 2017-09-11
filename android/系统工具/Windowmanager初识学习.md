安卓开发中经常会涉及到windowmanager相关的东西，是针对window的管理。
WindowManager是Android中一个重要的Service,是全局且唯一的。WindowManager继承自ViewManager。
WindowManager主要用来管理窗口的一些状态、属性、view增加、删除、更新、窗口顺序、消息收集和处理等。Android中真正展示给用户的是window和view，activity所起的作用主要是处理一些逻辑问题，比如生命周期管理及建立窗口。
在WindowManager中还有一个重要的静态类LayoutParams.通过它可以设置和获得当前窗口的一些属性。
https://github.com/wzp09tjlg/noteResource/blob/master/android/view/64fca89f-f574-4ad4-a9af-35cba4283002.png
 image （这个图没有看太懂，以后还得再看看）

https://github.com/wzp09tjlg/noteResource/blob/master/android/view/90c5b6ad-ce19-4d39-b3bf-e042a9e44255.png
这个图是介绍Application Activity  Window Session windowState WindowManagerService之间的关系（比较好理解的一个图）

针对windowmanager的理解，知道windowmanager是针对window的 属性，窗口，状态，更新，窗口顺序，消息搜集和处理。其他的处理参考上边的两个图。