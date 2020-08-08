# Java对象转Map的序列化

由于后台要求提交表单形式的参数，之前使用 Json 格式是可以序列化对象，但是对象序列化成键值对貌似没找到比较合适的库。于是自己动手写了一个简单的，模仿 Gson ，可以加注解，可以序列化父类。名曰 **Mapo** 。

## 注解

暂时只有两种注解，序列化名和是否序列化。

|               注解                |             说明             |
| :-------------------------------: | :--------------------------: |
|       `@SerializedName("")`       |           序列化名           |
| `@Expose(serialize = false/true)` | 是否序列化，不写的话默认true |

## 使用

父类

```java
public class BaseBean {

    @SerializedName("app_id")
    public String appId;

    @SerializedName("app_key")
    @Expose(serialize = false)
    public String appKey;


    public String getAppId() {
        return appId;
    }

    public void setAppId(String appId) {
        this.appId = appId;
    }

    public String getAppKey() {
        return appKey;
    }

    public void setAppKey(String appKey) {
        this.appKey = appKey;
    }

}
```

子类

```java
public class GreetBean extends BaseBean{

    @SerializedName("first_name")
    private String firstName;

    @SerializedName("last_name")
    private String lastName;

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

}
```

序列化

```java
GreetBean greetBean = new GreetBean();
greetBean.setFirstName("你好 *$#!^adsf");
greetBean.setLastName("formurl");
greetBean.setAppId("123456");
greetBean.setAppKey("dhaofanohkhjljk");
Mapo mapo = new Mapo();
Map<String, String> map = mapo.toMap(greetBean);
Log.d("TAG", mapo.toFormUrlString(map));
```

## 源码

主要是使用反射得到字段的注解、名称和值。

主类：

```java
/**
 * 键值对Map和对象相互转换
 */
public class Mapo {

    public Mapo() {
    }

    /**
     * 对象转换成键值对
     * @param object    对象
     * @return          Map
     */
    public Map<String, String> toMap(Object object) {
        Map<String, String> map = new HashMap<>();
        try {
            Class clazz = object.getClass();
            List<Field> fieldList = new ArrayList<>() ;
            while (clazz != null && !clazz.getName().toLowerCase().equals("java.lang.object")) {//当父类为null的时候说明到达了最上层的父类(Object类).
                fieldList.addAll(Arrays.asList(clazz .getDeclaredFields()));
                clazz = clazz.getSuperclass(); //得到父类,然后赋给自己
            }
            for (Field field : fieldList) {
                field.setAccessible(true);
                String key = field.getName();
                Object value = field.get(object);
                String s = String.valueOf(value);
                if (field.getAnnotations() != null) {
                    if (field.isAnnotationPresent(Expose.class)) {
                        Expose expose = field.getAnnotation(Expose.class);
                        if (!expose.serialize())
                            continue;
                    }
                    if (field.isAnnotationPresent(SerializedName.class)) {
                        SerializedName serializedName = field.getAnnotation(SerializedName.class);
                        String v = serializedName.value();
                        if (!TextUtils.isEmpty(v)) {
                            key = v;
                        }
                    }
                }
                map.put(key, s);
                Log.d(LOG_TAG, field.getName());
            }
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
        return map;
    }


    /**
     * 转化成FormUrl
     * @param map   键值对
     * @return      字符串
     */
    public String toFormUrlString(Map<String, String> map) {
        if (map.isEmpty()) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        Set<String> set = map.keySet();
        for (String key : set) {
            sb.append(key).append("=").append(map.get(key)).append("&");
        }
        return sb.toString().substring(0, sb.length()-1);
    }

}
```

两个注解类：

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 默认解析
 */
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.FIELD})
public @interface Expose {

    boolean serialize() default true;
}
```

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.FIELD})
public @interface SerializedName {

    String value();
}
```

> 反序列化暂时没实现，一般情况后端会返回Json格式，很少用键值对。