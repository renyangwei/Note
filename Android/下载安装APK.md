# 下载安装APK

分三个部分讲解。Android存储结构、下载文件和安装APK。

## Android文件存储

所有 Android 设备都有两个文件存储区域：[内部存储空间](https://developer.android.com/training/data-storage/files/internal?hl=zh-cn)和[外部存储空间](https://developer.android.com/training/data-storage/files/external?hl=zh-cn)。这些名称是在 Android 早期确定的，那时候大部分设备都提供内置的非易失性内存（内部存储空间）以及可移动存储媒介（如 Micro SD 卡，提供外部存储空间）。

> 可以理解为PC上的硬盘和U盘。

![文件存储](..\assets\android_storge.jpg)

通过 `context` 获取的路径在卸载应用之后都 **会** 被删除。

通过 `Environment` 获取的路径在卸载应用之后都 **不会** 被删除。

当在计算机上启用 USB 大容量存储来传输文件时，用户可对外部存储文件进行修改。

## 下载文件

下载文件有三种方式：

|          方式          |                            优缺点                            |
| :--------------------: | :----------------------------------------------------------: |
|        自己封装        |                相对比较麻烦，容易出现各种问题                |
|    DownloadManager     | API简洁，通知栏进度显示；缺点：兼容性不好，在某些品牌手机上不行 |
| 使用第三方网络请求框架 |                           推荐使用                           |

### 自己封装

```java
 /**
     * 下载文件
     *
     * @param fileUrl 文件地址
     * @return 字节
     */
    public static boolean download(String fileUrl, String filePath) {
        Log.i("jetpack", "filePath=" + filePath);
        HttpURLConnection connection = null;
        try {
            File file = new File(filePath);
            if (file.exists()) {
                file.delete();
            } else {
                file.mkdirs();
            }
            URL url = new URL(fileUrl);
            connection = (HttpURLConnection) url.openConnection();
            connection.setConnectTimeout(10000);
            connection.setReadTimeout(10000);
            int responseCode = connection.getResponseCode();
            if (responseCode == HttpsURLConnection.HTTP_OK) {
                InputStream in = new BufferedInputStream(connection.getInputStream());
                FileOutputStream outputStream = new FileOutputStream(file);
                byte[] buffer = new byte[1024];
                int len;
                while ((len = in.read(buffer)) != -1) {
                    outputStream.write(buffer, 0, len);
                }
                outputStream.close();
                in.close();
                Log.i("Jetpack", "http download file success! url=" + fileUrl);
            } else {
                return false;
            }
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        } finally {
            if (connection != null) {
                connection.disconnect();
            }
        }
        return true;
    }
```

使用：

```java
new Thread(() -> {
            String fileUrl = "http://10.20.6.63:5050/temp/app-debug.apk";
            String filePath = context.getExternalCacheDir().toString() + File.pathSeparator + "app-debug.apk";
            if (Utils.download(fileUrl, filePath)) {
                Log.d("jetpack", "下载成功");
            }
        }).start();
```

> 建议在 `IntentService` 中调用。

### 使用第三方库

这里介绍Retrofit。

**1.声明接口**

有两种方式，静态资源和动态资源。

```java
// option 1: a resource relative to your base URL
@GET("/resource/example.zip")
Call<ResponseBody> downloadFileWithFixedUrl();
// option 2: using a dynamic URL
@GET
Call<ResponseBody> downloadFileWithDynamicUrlSync(@Url String fileUrl); 
```

举例：

```java
@Streaming //大文件时要加不然会OOM
@GET("temp/app-debug.apk")
Call<ResponseBody> downloadFile();
```

**2.调用接口**

```java
retrofitInstance.download(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
                String filePath = getApplication().getExternalCacheDir() + File.pathSeparator + "aaa.apk";
                new Thread(() -> {
                    if (Utils.writeFileToSDCard(filePath, response.body())) {
                        Log.e("jetpack", "下载完成");
                    }
                }).start();

            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {
                Log.e("jetpack", t.getLocalizedMessage());
            }
        });
```

**3.写入文件**

```java
public static boolean writeFileToSDCard(String filePath, ResponseBody body) {
        try {
            File futureStudioIconFile = new File(filePath);
            InputStream inputStream = null;
            OutputStream outputStream = null;
            try {
                byte[] fileReader = new byte[4096];
                long fileSize = body.contentLength();
                long fileSizeDownloaded = 0;
                inputStream = body.byteStream();
                outputStream = new FileOutputStream(futureStudioIconFile);
                while (true) {
                    int read = inputStream.read(fileReader);
                    if (read == -1) {
                        break;
                    }
                    outputStream.write(fileReader, 0, read);
                    fileSizeDownloaded += read;
                    Log.d("jetpack", "file download: " + fileSizeDownloaded + " of " + fileSize);
                }
                outputStream.flush();
                return true;
            } catch (IOException e) {
                return false;
            } finally {
                if (inputStream != null) {
                    inputStream.close();
                }
                if (outputStream != null) {
                    outputStream.close();
                }
            }
        } catch (IOException e) {
            return false;
        }
    }
```

## 安装APK

在6.0、 7.0、 8.0上处理各有不同。

6.0之前比较随意，没有什么要求；7.0添加了提高了私有文件的安全性 `FileProvider`；8.0 新增了权限。



