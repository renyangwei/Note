# Retrofit2

将HTTP请求转换为Java接口的库。

参考 [官网](https://square.github.io/retrofit/) 和 [搞定 Android Retrofit2 常用请求](https://www.jianshu.com/p/fe3e2052f46f) 。

## 导入

```groovy
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```

具体版本参考 [github retrofit](https://github.com/square/retrofit) 和 [converter-gson](https://mvnrepository.com/artifact/com.squareup.retrofit2/converter-gson) 。

## 使用

三步：

1. 创建接口，视情况使用注解；
2. 创建 `Retrofit` 对象，感觉可以做成单例类；
3. 生成接口实现类；
4. 执行接口中定义的方法。

## Get

### 接口

```java
public interface RetrofitService {
	// Get方法
  	// who 是路径变量
    @GET("greet/{who}")
    Call<ResponseBody> greet(@Path("who") String who);

}
```

### 创建Retrofit对象

```java
 Retrofit retrofit = new Retrofit.Builder()
     			// url
                .baseUrl("http://172.21.0.189:8888")
                .build();
```

### 生成接口实现类

```java
RetrofitService retrofitService = retrofit.create(RetrofitService.class);
```

### 执行接口中定义的方法

```java
 Call<ResponseBody> repo = retrofitService.greet("lang");
        repo.enqueue(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
                try {
                    // 获取response body
                    tv.setText(response.body().string());
                } catch (IOException e) {
                    e.printStackTrace();
                    tv.setText(e.getMessage());
                }
            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {
                tv.setText(t.getMessage());
            }
        });
```

## POST

### 接口

```java

public interface RetrofitService {

    // 发送非表单数据用 @Body，比如Json格式
    @POST("insert")
    Call<HttpRespBean> insert(@Body PostBody postBody);


    // 发送表单数据使用FieldMap
    @POST("blog")
    @FormUrlEncoded
    Call<HttpRespBean> blog(@FieldMap Map<String,String> map);

}
```

### 创建Retrofit对象

要配置 **Gson**

```java
 Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("http://172.21.0.189:8888")
     			// 要配置Gson
                .addConverterFactory(GsonConverterFactory.create())
                .build();
```

### 生成接口实现类

这一步都一样

```java
RetrofitService retrofitService = retrofit.create(RetrofitService.class);
```

### 执行接口中定义的方法

post json 格式的数据

```java
PostBody postBody = new PostBody("ren", "yangwei");
Call<HttpRespBean> repo = retrofitService.insert(postBody);
repo.enqueue(new Callback<HttpRespBean>() {
    @Override
    public void onResponse(Call<HttpRespBean> call, Response<HttpRespBean> response) {
           HttpRespBean respBean = response.body();
           tv.setText(respBean.toString());
    }

    @Override
    public void onFailure(Call<HttpRespBean> call, Throwable t) {
            tv.setText(t.getMessage());
     }
});
```

`postBody` 对象用 Gosn 解析

```java
public class PostBody {

    @SerializedName("first_name")
    private String firstName;

    @SerializedName("last_name")
    private String lastName;

    public PostBody(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    @Override
    public String toString() {
        return "PostBody{" +
                "firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                '}';
    }
}
```

返回的数据如果是json格式也可以用Gson解析

```java
![retrofit](F:\Note\assets\retrofit.png)public class HttpRespBean {

    private String code;

    private String data;

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public String getData() {
        return data;
    }

    public void setData(String data) {
        this.data = data;
    }

    @Override
    public String toString() {
        return "HttpRespBean{" +
                "code=" + code +
                ", data='" + data + '\'' +
                '}';
    }
}
```

post 表单数据，表单用键值对

```java
        HashMap<String, String> map = new HashMap<>();
        map.put("first_name", "ren");
        map.put("last_name", "1234");
        Call<HttpRespBean> repo = retrofitService.blog(map);
        repo.enqueue(new Callback<HttpRespBean>() {
            @Override
            public void onResponse(Call<HttpRespBean> call, Response<HttpRespBean> response) {
                HttpRespBean respBean = response.body();
                tv.setText(respBean.toString());
            }

            @Override
            public void onFailure(Call<HttpRespBean> call, Throwable t) {
                tv.setText(t.getMessage());
            }
        });
    }
```

## 注解说明

基本上所有的注解都在这里。

| 序号 | 注解            | 用途                                                 |
| ---- | --------------- | ---------------------------------------------------- |
| qq1  | @POST           | post 请求                                            |
| qq2  | @DELETE         | delete 请求                                          |
| qq3  | @PUT            | put 请求                                             |
| qq4  | @GET            | get 请求                                             |
| qq5  | @PATCH          | patch请求，该请求是对put请求的补充，用于更新局部资源 |
| qq6  | @HEAD           | head请求                                             |
| qq7  | @OPTIONS        | option请求                                           |
| qq8  | @HTTP           | http 请求 可以设置达到上面任意请求                   |
| cs1  | @Url            | 指定                                                 |
| cs2  | @Path           | url 替换                                             |
| cs3  | @Query          | 查询字符串                                           |
| cs4  | @QueryMap       | 比较多的查询字符串集合                               |
| cs5  | @Field          | 表单参数                                             |
| cs6  | @FieldMap       | 表单参数集合                                         |
| cs7  | @Headers        | 为方法添加请求响应头                                 |
| cs8  | @Header         | 为方法参数添加请求响应头                             |
| cs9  | @Part           | 与Multipart注解结合使用,适合文件上传                 |
| cs10 | @PartMap        | 默认接受的类型是Map<String,RequestBody>              |
| cs11 | @Body           | 请求上传的对象，发送非表单数据，如 传递json格式数据  |
| bj1  | @FormUrlEncoded | Form表单数据，每个键值对需要使用@Field注解           |
| bj2  | @Multipart      | 发送multipart数据，需要配合使用@Part @PartMap        |
| bj3  | @Streaming      | 响应用字节流的形式返回.多用于下载大文件              |

其他的以后再补充。