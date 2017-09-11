在安卓中，经常会需要显示对话框之类的东西，popupwindow就是类似这种功能的东西。
实例化popupwindow的构造方法：
PopupWindow popupWindow = new PopupWindow(view,width,height,focusable);
这种构造方法指定要显示的contentView(要显示的内容)，显示内容的宽和高。是否可以获取焦点。
当然也可以使用其他的构造方法，如：
PopupWindow(Context);
PopupWindow(ContentView,width,height);
PopupWindow(ContentView);
这三种构造方法虽然也很常用，但是构造之后还是得设置其他的参数，长宽，显示的view，及是否获取焦点等属性。综合所述，第一种构造方法是最便捷的。

一：显示
popupwindow的显示方法：
showAsDropDown(View); 显示在view的正下房
showAsDropDown(view,xoffset,yoffset); 显示在view的正下方，偏移量是xoffset,yoffset
showAtLocation(parent,Gravity,x,y); 相对parent的位置，显示在什么位置，x和y表示位置坐标。


二：
popupwindow的大小，如果显示的view是来着xml中，那么在xml中设置的第一层布局的大小对布局内无效，popupwindow的大小直接和xml中第一层的大小对应。

三：焦点和点击空白地方让popupwindow消失
在popupwindow中可以这是其是否获取焦点，setfocusable(true);
设置外部点击之后消失popupwindow,但是这个属性，即使设置之后，也会存在这种情况，点击外部不会消失。需要设置popupwindow的backgroud之后才能正常。不知道设计的人当初为啥会这样设置，导致设置按这样的流程走。

四：设置动画
在popupwindow中经常需要加入动画，popupwindow已经提供这样的动画方法，setAnimationStyle(int);