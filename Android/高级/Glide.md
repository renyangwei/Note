# Glide

图片加载库。使用流式API。

思路：

1. 从网络、本地和内存中加载图片，图片名称用url的MD5值；
2. 展示到控件上；
3. 提供加载回调；
4. 每个请求放入队列中，避免多个线程发送同一个请求；
5. 开启线程处理请求

部分代码：

```java
// 添加到队列中
public void addRequestQueue(request) {
    if (!requestQueue.contains(request)) {
        requestQueue.add(request)
    }
}

// 保存线程对象
private MyThread[] tasks;

// 执行加载图片的工作
public void dispatcher() {
    // 获取虚拟机可用的最大处理器个数，不会小于1个
    int threadCount = Runtime.getRuntime().availableProcessors();
    tasks = new MyThread[threadCount];
    for (int i=0; i < threadCount; i++) {
        MyThread thread = new MyThread(requestQueue);
        thread.start();
        tasks[i] = thread;
    }
}

// 中断线程
public void stop() {
    if (tasks.length() > 0) {
        for (MyThread thread : tasks) {
            if (!thread.isInterrupted()) {
                thread.interrupt();
            }
        }
    }
}
```


```java
public class MyThread extends Thread {
    // 用于在主线程中刷新控件
    private Handle handle;
    // 保存传过来的队列，RequestBuilder 可以看成是保存参数的类
    private LinkedBlockingQueue<RequestBuilder> requestQueue;

    public MyThread(LinkedBlockingQueue<RequestBuilder> requestQueue) {
        this.requestQueue = requestQueue;
        handle = new Handle(Looper.getMainLooper());
    }

    public void run() {
        super.run();
        while (!isInterrupted()) {
            try {
                // 获取参数对象
                RequestBuilder builder = requestQueue.take();
                // 设置占位图
                placeholder(builder);
                // 从网络加载图片
                Bitmap bitmap = loaderFromNet(builder);
                // 在控件中显示
                show(builder, bitmap);
            } catch (Exception e) {
                //TODO: handle exception
            }
        }
    }

    private void show(Builder builder, Bitmap bitmap) {
        if (builder.getImageView() != null && bitmap != null) {
            handle.post(new Runnable() {
                builder.getImageView().setImageBitmap(bitmap);
                if (builder.getListener() != null) {
                    builder.getListener().onLoadReady(bitmap);
                }
            });
        }
    }

    // 设置占位符
    private void placeholder(RequestBuilder builder) {
        if (builder.getPlaceholderId() > 0 && builder.getImageView() != null) {
            // 在主线程中执行
            handle.post(new Runnable() {
                public void run() {
                    builder.getImageView.setImageResource(builder.getPlaceholderId());
                }
            })
        }
    }
    // 从网络加载图片
    // 后续还可以添加保存到本地、添加缓存策略等，LurCache
    private Bitmap loaderFromNet(Builder builder) {
        InputStream is = null;
        Bitmap bitmap = null;
        try {
            URL url = new URL(builder.getUrl());
            HttpURLConnection conn = url.openConnection();
            is = conn.getInputStream();
            bitmap = BitmapFactory.decodeStream(is);
        } catch (Exception e) {
            //TODO: handle exception
            e.printStackTrace();
        } finally {
            if (is != null)
                is.close();
        }
    }
    return bitmap;
}
```