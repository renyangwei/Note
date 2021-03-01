# Handler

是Android中提供跨线程通信的解决方案。

实现思路：

每个线程有且只有一个消息队列MessageQueue，有且只有一个Looper类不断遍历消息队列，如果没有消息线程就会停止(主线程不会停止)

## 角色说明

**Handler**

主线程中创建，子线程会持有，用于发送数据和接收数据

**MessageQueue**

消息队列，添加消息和消费消息加了互斥锁，保证不会出错

**Looper**

遍历消息队列，如果有消息，则使用Message持有的Handler对象处理消息(dispatchMessage)

使用ThreadLocal保证唯一性，ThreadLocal用键值对保存了对象，键是当前线程，值是Looper

持有消息队列对象，所以MessageQueue也是唯一的

**Message**

消息类，持有handler对象

## 基本用法

```java
/**
 * 传统模式下载
 */
private void downloadPic() {
    // 开启线程
    new Thread(() -> {
        try {
            Bitmap bitmap = downloadBitmap(path);
            // 返回给主线程
            Message message = handler.obtainMessage();
            message.obj = bitmap;
            handler.sendMessage(message);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }).start();
}

private Bitmap downloadBitmap(String path) throws IOException {
    URL url = new URL(path);
    URLConnection connection = url.openConnection();
    HttpURLConnection httpURLConnection = (HttpURLConnection) connection;
    int code = httpURLConnection.getResponseCode();
    if (code == HttpURLConnection.HTTP_OK) {
        return BitmapFactory.decodeStream(httpURLConnection.getInputStream());
    }
    return null;
}


private Handler handler = new Handler(new Handler.Callback() {
    @Override
    public boolean handleMessage(@NonNull Message msg) {
        Log.d(MTAG, "handleMessage:");
        Bitmap bitmap = (Bitmap) msg.obj;
        imageView.setImageBitmap(bitmap);
        return false;
    }
});
```

## Handler 的改进

```java

/**
 * 为避免handler造成的内存泄漏
 * 1、使用静态的handler，对外部类不保持对象的引用
 * 2、但Handler需要与Activity通信，所以需要增加一个对Activity的弱引用
 */
private static class MyHandler extends Handler {
    private final WeakReference<Activity> mActivityReference;    

    MyHandler(Activity activity) {
        this.mActivityReference = new WeakReference<Activity>(activity);
    }

    @Override
    public void handleMessage(Message msg) {
        super.handleMessage(msg);
        MainActivity activity = (MainActivity) mActivityReference.get();  //获取弱引用队列中的activity
        switch (msg.what) {    //获取消息，更新UI
            case 1:
                byte[] data = (byte[]) msg.obj;
                activity.threadIv.setImageBitmap(activity.getBitmap(data));
                break;
        }
    }
}
```
