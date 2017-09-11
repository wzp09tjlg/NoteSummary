不仅是安卓的开发会涉及到包，Java也会涉及到包。所以无论是针对安卓学习还是针对Java学习，都是需要对包有一个整体的概念，并且需要进一步的认识，通过包的管理，认识包是一个不错的途径，所以再学点packagemanager是很有必要的：
     * PackageManager介绍： 
     * 本类API是对所有基于加载信息的数据结构的封装，包括以下功能：  
     * 安装，卸载应用 查询permission相关信息 查询Application相关 
     * 信息(application，activity，receiver，service，provider及相应属性等） 
     * 查询已安装应用 增加，删除permission 清除用户数据、缓存，代码段等 非查询相关的API需要特定的权限。 
     * 主要包含了，安装在当前设备上的应用包的相关信息 
     * 如下：获取已经安装的应用程序的信息  

packagemanager 的获取
PackageManager  pm =  getPackageManager();

通过packagemanager 我们可以获得的数据如下：
1.获取 应用的信息，icon 、包名、启动activity 名字等信息
Drawable drawable  =  getApplicationIcon（）；
获取应用的icon

2.获取应用的ApplicationInfo 的信息，这些信息是针对manifeast中的Application 节点而言，能获取节点中的信息。
ApplicationInfo applicationInfo  = pm.getApplicationInfo();

3.获取已经安装的应用的Application的信息
List<ApplicationInfo> mListApplicationInfo = pm.getInstalledApplications(flag); 根据筛选条件来获系列的ApplicationInfo信息 （其中Flag 的值是  
//MATCH_DEFAULT_ONLY    ：Category必须带有CATEGORY_DEFAULT的Activity，才匹配
//                //GET_INTENT_FILTERS         ：匹配Intent条件即可
//                //GET_RESOLVED_FILTER    ：匹配Intent条件即可）

4.获取PackageInfo 的信息
List<PackageInfo> mListPakcage = pm.getInstalledPackages(flag);
 flag 类似 3）的值。获取包名的信息

通常情况下，使用packageManager就是使用上边的那些方法，获取相应的数据。
//              public ActivityInfo[]     activities        //           所有<activity>节点信息
//              public ApplicationInfo applicationInfo      // <application>节点信息，只有一个
//              public ActivityInfo[]    receivers          //        所有<receiver>节点信息，多个
//              public ServiceInfo[]    services            //      所有<service>节点信息 ，多个
这些数据也是可以通过pakcageManager 来获取得到的。

在PkacageManager 中 会涉及到几个类的继承关系：
              //packageInfo的几个类的继承关系
// PackageItemInfo <----ApplicationInfo  //包含application中的字段和参数
//                              <----ActivityInfo     //包含activity中的字段和参数
//                              <----ServiceInfo      //包含service中的字段和参数

PackageManager相关

      本类API是对所有基于加载信息的数据结构的封装，包括以下功能：

    安装，卸载应用
    查询permission相关信息
    查询Application相关信息(application，activity，receiver，service，provider及相应属性等）
    查询已安装应用
    增加，删除permission
    清除用户数据、缓存，代码段等

非查询相关的API需要特定的权限，具体的API请参考SDK文档。