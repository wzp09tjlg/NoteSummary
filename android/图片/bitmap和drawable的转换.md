在安卓开发中经常会使用到bitmap和drawable的转换，怎么转换才高效和方便，这里做一个总结:
一：bitmap 转 drawable
     1.在imageView中设置的是drawable，如果知道是bitmap
    那么drawable可以这样获得：
   Drawable drawable = new BitmapDrawable(bitmap);

二：drawable转bitmap
   1.能获得到drawable，生成bitmap
   Drawable drawable = getDrawable(); //能获得到drawable的方法
   Bitmap bitmap = Drawable2Bitmap(drawable);

   private Bitmap Drawable2Bitmap(Drawable drawable){
    Bimtap bitmap = new Bitmap(
      drawable.getIntrinsicWidth(),
      drawable.getIntrinsicHeight(),
      drawable.getOpacity()!= PicelFormat.OPAQUE?Bitmap.config.ARGB_8888:Bitmap.config.ARGB_565  
   );
      Canvas canvas = new Canvas(bitmap);
      drawable.setBounds(0,0,drawable,getIntrisicWidth(),drawable,getIntrinscHeight());
      drawable.draw(canvas);
      return bitmap;
   }
 

  2.能获得resource,File,inputStream或者是byte[] 生成Bitmap的方式
    Resuorce res = getResuorce();//能够获取资源的resource
   Bitmap bitmap = BitmapFactory.decodeResource(res);//其他带参数的方法

    File file = getFile();//能够获得图片的文件
    Bitmap bitmap = BitmapFactory.decodeFile(file);//这里还有其他的方法，带多个参数

   InputStream is = getInputStream();//获取inputStream的方法
   Bitmap bitmap = BitmapFactory.decodeStream(is);  

   byte[] bytes = getByte();//获取byte[]的方法
  Bitmap bitmap = BitmapFactory.decodeArray(bytes); // 这里还有其他的方法，带过个参数的