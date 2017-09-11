数据库在日常开发中会经常使用到，移动端使用的数据基本上都是sqlite，体积小，功能强的数据库。安卓这块就是使用的sqlite的数据库。
使用sqlite数据库，安卓提供了SqliteOpenHelper基类，使用sqlite需要继承这个基类，基类中提供了两个方法，onCreate 和onUpdate.
两个方法的调用分别如下：
onCreate方法在数据第一次调用的时候,
例子如下： MyDBHelper extend  SqliteOpenHelper{
  onCreate();
  onUpdate(); 
}
MyDBHelper dbHelper = new MyDBHelper(Context);时并没有调用onCreate的方法，在第一次获取数据库的时候，才会真正的调用到数据的创建，也就是哦那Create的方法。
一般在OnCreate方法中我们是创建表或者是视图之类的动作，使用的方式是通过提供的database 来执行相应的sql语句。

onUpdate方法是在数据库升级的时候调用，这是就需要说到S群里特OpenHelper的构造方法了，在构造方法中需要传递的是context,name,CursorFactory，version. 最后一个参数是version，也就是说在我们创建我们自己的MyDBHelper的实例的时候，会要传version这个参数，当这个参数比上一次大时，就会执行onUpdate这个方法，在onUpdate这个方法中，我们一般也是执行相应的建表 建视图的操作，当然也包括对之前的数据表废弃删除的操作。onUpdate的方法页不是在创建MyDBHelper的时候调用，也是在获取数据库的时候才调用的(PS.获取数据的方法有 getReadableDatabase() 及getWriteableDatabase())这两个方法。
