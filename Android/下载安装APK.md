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

参考 [Android 6.0 7.0 8.0三个版本Install Apk 采坑记录](https://juejin.im/post/5ad4499a6fb9a028b617fc1c)

在6.0、 7.0、 8.0上处理各有不同。

6.0之前比较随意，没有什么要求；7.0添加了提高了私有文件的安全性 `FileProvider`；8.0 新增了权限。

### 7.0 的 fileProvider

在 AndroidManifest.xml 文件声明：

```xml
<provider
            android:name="android.support.v4.content.FileProvider"
            android:authorities="{包名}.fileprovider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/file_paths"/>
</provider>
```

- `name`：v4包，也可以是androidx包里的
- `resource`：设置FileProvider访问的文件路径

首先我们在res文件下面创建一个xml文件夹,然后再xml中创建一个manifest中声明的文件 **file_paths.xml** 。这个名字看你自己定义的，但是必须和AndroidManifest.xml中声明的一致：

```xml
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <root-path
        name="root"
        path="" />
    <files-path
        name="files"
        path="." />

    <cache-path
        name="cache"
        path="." />

    <external-path
        name="external"
        path="." />

    <external-files-path
        name="external_file_path"
        path="." />
    <external-cache-path
        name="external_cache_path"
        path="." />

</paths>
```

### 8.0的权限

8.0上主要是权限问题，在 AndroidManifest.xml 里声明权限即可：

```xml
<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>
```

### 安装代码

```java
private void installApk(String filepath) {
		LogUtil.d("开始安装");
		File apk = new File(filepath);
		Intent intent = new Intent(Intent.ACTION_VIEW);
		intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
		String packageName = SDKDYB.getInstance().getContext().getPackageName();
		if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.N){
		    intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
		    Uri uri = FileProvider.getUriForFile(this, packageName + ".fileprovider", apk);
		    intent.setDataAndType(uri, "application/vnd.android.package-archive");
		}else{
		    intent.setDataAndType(Uri.fromFile(apk),"application/vnd.android.package-archive");
		}
		try {
		    startActivity(intent);
		}catch(Exception e){
		    e.printStackTrace();
		    LogUtil.e("安装失败：" + e.getMessage());
		}
	}
```



