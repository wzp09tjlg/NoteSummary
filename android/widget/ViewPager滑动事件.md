安卓编程中经常会使用到viewpager，针对viewpager的滑动之后 会联动其他的滑动，因此需要针对viewpager的滑动做监听处理。
viewpager.OnPageChangeListener(){
 onPageScrollStateChanged(int arg0)
 onPageScrolled(int arg0,float arg1,int arg2)
 onPageSelected(int arg0)
}
针对onPageScrollStateChanged(int arg0): arg0 取值 0  1 2。1表示正在滑动，2表示滑动已经完毕，0表示什么都没有做。当页面开始滑动时 三种状态的变化时（1,2,0）
针对onPageScrolled(int arg0,float arg1,int arg2) ,在滑动被停止之前，此方法一直会被调用，三个参数表示arg0表示当前页面，arg1当前页面便宜的百分比，arg2当前页面便宜的像素位置。
 onPageSelected(int arg0) 此方法是页面跳转完之后得到调用，arg0是你当前选中的页面的position
