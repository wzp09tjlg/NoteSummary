在安卓开发中经常需要对网络的请求，当下也存在一些第三方库对网络的封装，譬如Volley，OkHttp等。
这些都是非常优秀的第三方库，值得我们实用。
但是在使用过程中我们经常会遇到各种各样的场景，有的时候使用第三方库不能完全解决和适应我们的场景，自己写吧技术有限，很多地方又顾忌不到。这里介绍下使用retrofit对网络请求的访问。

retrofit 是square团队开发的第三方库。该团队为人熟知的三方库有volley，piacsso，当然还有今天retrofit。（还有很多的很好的库，这里不一一列举了）。

言归正传,retrofit 改如何使用呢？
准备工作
a 猪脚: Retrofit retrofit = new Retrofit.Builder().....build();  这就是我们使用的猪脚。
   其次次猪脚1：需要定义一个interface  名字随便写， 
   public   interface RetrofitInterface{
      //这里定义访问的接口
     @GET('index.php')
     String callIndexSynchronous();

     @GET('/user/{username}')
      void callSomeAsnchronous(CallBack<String> callback);    
    }
  上边定义了两个接口，一个是同步的接口，一个是异步的接口。请求的方式都是GET，当然在retrofit请求网络时支持其他的几种访问方式POST,HEAD,PUT,DELETE等方式。定义接口与GET类似。
    次猪脚2：定义一个在gson中转换的bean（并不一定需要，简单的请求只要猪脚和次猪脚1 就可以了）

如何使用：
  同步使用方式：
        new Thread(new Runnable() {
          @Override
          public void run() {
              RetrofitInterface interf  = retrofit.create(RetrofitInterface.class);
             String result =  interf.callIndexSynchronoue();
              Log.e(TAG,"doRetrofitSynchronous:------>" + result);
          }
      }).start();
异步使用（需要一个传入的参数String input）：
           RetrofitInterface interf  = retrofit.create(RetrofitInterface.class);
        Call call = interf.getUser(input);
        call.enqueue(new Callback() {
            @Override
            public void onResponse(Response response, Retrofit retrofit) {
               User user = (User)response.body();
                if(user==null){
                    Log.e(TAG,"doretrofitAsnchronous   ----> Response is null");
                }else{
                    mTextResult.setText("Github Name :" + user.getName()
                            + "\nWebsite :" + user.getBlog()
                            + "\nCompany Name :" + user.getCompany());
                }
            }

            @Override
            public void onFailure(Throwable t) {
              Log.e(TAG,"Failure:" + t.getMessage().toString());
            }
        });

然后其他的任务就交给Retrofit来完成，retrofit 会动态创建接口的实例，然后可以动态的改变请求的url。十分方便。

  