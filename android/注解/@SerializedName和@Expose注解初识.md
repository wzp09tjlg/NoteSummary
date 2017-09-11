google的@SerializedName和@Expose注解

在安卓项目中经常会遇到数据的来源不一样，但是我们的应用的数据需要统一，这时就需要进行数据的转换。这里有谷歌提供的第三方注解，方便我们队数据的转换。
1.@SerializedName
 使用方式 如下：
   @SerializedName（name）
   private String everyName;
   private String otherName;

然后在Gson进行序列化的时候，everyName 会被虚拟化成 name
 {"name":"zhangsan";"otherName":"lisi"}

2.@Expose
使用方式和SerializedName类似，作用是：
@Expose 
private String name;
private String password;
如果创建Gson 是使用一般创建方式 Gson gson = new Gson();
这时序列化时 没有任何的区别。
{"name":"zhangsan";"password":"1234"}

但是如果常见Gson时使用的是这种方式Gson gson =  new  GsonBuilder.excludeFieldsWithoutExposeAnnotation().create();
这时序列化时将不包括password
{"name":"zhangsan"}
