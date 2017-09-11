在安卓系统中，进程之间不能共享内存。如果两个不同的应用程序之间需要通信应该怎么处理呢？这时安卓系统就提出了这样的处理方案AIDL.
那么AIDL应该怎么使用呢，以及使用的场景是什么呢？
上边已经提及AIDL就是在不同进程之间通信的，所以使用场景就是服务端提供aidl这种通信方式的接口，工客户端去访问和调用。
 在服务端(可以这样理解成服务端) 创建aidl文件，安卓系统会自动生成相应的Java文件，不过位置是在gen目录下，
 在客户端创建相同的包及aidl文件，然后也会自动生成相应的Java文件。

一般而言，aidl都是为客户端提供一个服务(service)，所以通过bind()将服务的一个引用传递给客户端。
  IBinder onBind(Intent intent){
    return mBinder;  
   }
其中mBinder就是通过AIDL的stub()创建。
 private AidlService.Stub mBinder = new AidlService.Stub() {        
        @Override
        public double getInfo(String value) throws    
                                                RemoteException {
            log(" AidlService.Stub  -> mBinder : getInfo() :" + value);
            return 100.0;
        }
    };  
 
客户端通过bingService(intent);绑定service，然后将就可以调用服务提供的方法，进行进程间的通信。
    private ServiceConnection mServiceConnection = new ServiceConnection(){
    @Override
    public void onServiceConnected(ComponentName arg0, IBinder arg1) {
        // TODO Auto-generated method stub
        mAidlService = AidlService.Stub.asInterface(arg1);     
    } 
    @Override
    public void onServiceDisconnected(ComponentName arg0) {
        // TODO Auto-generated method stub
       mAidlService = null;          
    }
   }; 
进行绑定操作：
       Bundle args = new Bundle();
       Intent intent = new Intent("com.example.aidlservice.MyService");
       intent.putExtras(args);
       bindService(intent, mServiceConnection, Context.BIND_AUTO_CREATE);
  
例如可以调用服务提供的方法
  mAidlService.getInfo();  //这个方法是在服务端AIDL中定义的方法
 当然客户端访问服务之后需要做好解除绑定的操作。
   unbindService(mServiceConnection);

好了，这就是简单的一个客户端到服务端的跨进程通信操作。
   