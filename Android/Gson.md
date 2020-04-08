# Gson使用

Gson提供了`fromJson()` 和 `toJson()` 两个直接用于解析和生成的方法，前者实现反序列化，后者实现了序列化。

## 1 基本数据类型

用得很少，也就看一看。

```java
Gson gson = new Gson();
// 生成
String jsonNumber = gson.toJson(100);       // 100
String jsonBoolean = gson.toJson(false);    // false
String jsonString = gson.toJson("String"); //"String"

// 解析
int i = gson.fromJson("100", int.class); // 100
double d = gson.fromJson("\"99.99\"", double.class); // 99.99
boolean b = gson.fromJson("true", boolean.class); // true
String str = gson.fromJson("String", String.class); // String
```

## 2 POJO类的生成与解析

```java
public class User {

     public String name;

     // 解析成json字符串的字段，Go语言里也可以这样
     @SerializedName("Age")
     public int age;
     
     // alternate 是备选字段，三种里的任意一种都可以解析
     @SerializedName(value = "emailAddress", alternate = {"email", "email_address"})
     public String emailAddress;

     public User(String name, int age, String email) {
          this.name = name;
          this.age = age;
          emailAddress = email;
     }

     @Override
     public String toString() {
          return "{" +
               " name='" + name + "'" +
               ", age='" + age + "'" +
               ", emailAddress='" + emailAddress + "'" +
               "}";
     }

}
```

```java
Gson gson = new Gson();
// 反序列化
User user = new User("怪盗kidou", 24, "18673298768@163.com");
String jsonObject = gson.toJson(user);
System.out.println(jsonObject)
// 序列化
String jsonString = "{\"name\":\"怪盗kidou\",\"Age\":24, \"email\":\"1232443@163.com\"}";
User user1 = gson.fromJson(jsonString, User.class);
System.out.println(user1.toString());
```

> 注：当多种情况同时出时，以最后一个出现的值为准。

## 3 泛型

即根据传入的类型进行解析。

```java
Gson gson = new Gson();
String jsonArray = "[\"Android\",\"Java\",\"PHP\"]";
String[] strings = gson.fromJson(jsonArray, String[].class);
List<String> stringList = gson.fromJson(jsonArray, new TypeToken<List<String>>(){}.getType());
System.out.println(Arrays.toString(strings));
System.out.println(String.join(",", stringList));
```

举例：

服务端返回两种数据类型：

    {"code":"0","message":"success","data":{}}
    {"code":"0","message":"success","data":[]}

那么我们可以这样设计数据类：

```java
public class Result<T> {
    public int code;
    public String message;
    public T data;
}

public class Data {
    // 省略具体字段
}
```

解析：

```java
Gson gson = new Gson();
// 单个对象
Result<Data> result = gson.fromJson(json, new TypeToken<Result<Data>>(){}.getType());
// 列表
Result<List<Data>> result = gson.fromJson(json, new TypeToken<Result<List<Data>>>(){}.getType());
```

## 4 字段过滤

有的字段不需要解析。我们可以使用 `@Expose` 注解。

需要导出的字段上加上 `@Expose` 注解，不导出的字段不加。

举例：

```java
public class Category {
    @Expose public int id;
    @Expose public String name;
    @Expose public List<Category> children;
    //不需要序列化,所以不加 @Expose 注解，
    //等价于 @Expose(deserialize = false,serialize = false)
    public Category parent; 
}
```

初始化Gson

```java
Gson gson = new GsonBuilder()
        .excludeFieldsWithoutExposeAnnotation()
        .create();
gson.toJson(category);
```

基本用法先写到这里吧，够用了。