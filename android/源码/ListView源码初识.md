在项目中经常会使用到ListView,显示大数据及相同数据不同展示类型的一个控件。

一：
ListView的继承关系
view
 --viewGroup
      --AdapterView
         --AbsListView
             --ListView
对listView显示数据，当然还有一个重要的类需要理解和认识，那就是Adapter
Adapter的继承关系
Adapter(interface)
   | --ListAdapter
   | --SpinnerAdapter
         --BaseAdapter
可以理解成ListView是一个viewGroup，专门存放View的容器，所以在这里显示的数据都是以View的形式显示出来，而Adapter是将数据以View为陈载体提供给listview这个ViewGroup。然后在listView对要显示的数据进行绘制，这样就能显示众多的数据了。

二：