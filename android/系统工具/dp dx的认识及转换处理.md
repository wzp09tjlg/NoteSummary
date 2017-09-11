安卓中设置尺寸的大小有几种单位，他们之间是怎么转换的呢？这里组一个总结
dip（也叫dp） 设备独立像素，与设备有关的。不同的设备的dip是不一样的。
dx 与设备无关，设置之后不会因为设备不同值受到改变。
sp 放大像素，主要是设置文字的大小。
其中dx dp 之间的转化公式：dx = dp * density /160 + 0.5f;
                                     dp = dx * 160 / density + 0.5f;
sp dx 之间的转换公式： dx = sp * sp / 160 + 0.5f;
                                 sp = dx * 160 / density + 0.5f;

其中我们把 scale = context.getResources().getDisplayMetrics().density;称为比例因子，
               上边的公式也是可以转换成这样：
                dx = dp * scale + 0.5f;
                dp = dx / scale + 0.5f;
                dx  = sp * scale + 0.5f;
                 sp = dx / scale + 0.5f; 

如果屏幕是在160下，1dp = 1dx = 1sp 
当屏幕变成320之后，同样尺寸的显示屏，定义的dx长度的尺寸会变成160(每英寸160点的显示器)下的一半长。但是dp 会自动换算，保证长度不变。