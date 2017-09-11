在安卓开发中，经常会用到其他应用提供的数据。在安卓这个平台下就是使用的是contentProvider提供数据，然后使用contentResolver来获取数据，
这里使用获取本地的联系人的信息 来介绍下 使用contentResolver。
在获取本地联系人时需要添加获取联系人的权限：
android.permission.READ_CONTACTS

一：获取本地的contentResolver
  ContentResolver resolver = getContentResolver();
  其实这里可以参考从数据库中查询数据来理解contentResolver.(其实安卓在contentResolver的设计原理中就是使用数据库来保存的这样的数据)
 获取数据得到的是一个游标Cursor
Uri contactUri = ContactsContact.Contacts.CONTENT_URI;
Uri phoneUri  = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;
Uri emailUri = ContactsContract.CommonDataKinds.Email.CONTENT_URI;
Uri iconUri = Uri.parse("content://com.android.contacts/data");  //创建一个Uri 获取联系人的icon
Cursor cursorContact = resolver.query(contactsUri, null, null, null, null);  
//参数说明  uri ， [String[]]() projection,[String]() selection,[String[]]() selectionArgs, [String ]()sortOrder 
// URI , 想要查询的列，选择的条件 ，选择条件的参数，排序的参数
//然后循环的去查数据
while(cursorContact.moveNext()){
  //获取数据的处理  获取联系人的ID  NAME
 int id = cursorContact.getInt(cursorContact.getColumnIndex(ContactsContact.Contacts._ID));
 String name = cursorContact.getString(cursorContact.getColumnIndex(ContactsContact.Contacts.DISPLAY_NAME)); 
   Corsor cursorPhone = contentResolver.query(phoneUri,null,ContactsContact.CommonDataKinds.Phone.CONTACT_ID+ "=?",new String[]{id + "",null});

//查电话号码
  String phone = "";
while(cursor.moveNext()){
phone =  cursorPhone.getString(cursorPhone.getColumnIndex(ContactsContact.CommonDataKinds.Phone.NUMBER));
} 
 cursorPhone.close();

//查邮箱
String email = "";
Cursor  cursorEamil = contentResolver.query(emailUri ,null,ContactsContact.CommonDataKinds.Email.CONTACT_ID),new String[]{id + ""},null );
while(cursor.moveNext()){
  email = corsurEmail.getString(cursor.getColumnIndex(ContactsContact.CommonDataKinds.Email.DATA));
}
cursorEmail.close();

//查联系人头像
Bitmap icon = null;
byte[] data = null;
Cursor cursorIcon = contentResolver.query(uriIcon,null,"raw_contact_id = " + personId + " AND mimetype ='vnd.android.cursor.item/photo'",null,null);
while(cursorIcon.moveNext()){
    data = cursorIcon.getBlob(cursorIcon.getCulomnIndex("data15"));
}
cursorIcon.close();
if(data == null || data.length == 0)
icon = BitmapFactory.decodeResource(getResource(),R.drawable.defualtIcon);
else
icon = BitmapFactory.decodeByteArray(data,0,data.length); //这里进行decodeBitmap方法有很多
}
 sursorContact.close(); //查询完之后需要关闭 游标，不然会一直占用资源

通过上边的这些方式，就能将contentProvider的数据查询出来。
