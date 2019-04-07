# Activity

## 声明权限

你可以通过权限控制哪些应用可以启动特定活动。

举例：

应用一

```xml
<activity android：name = “....” 
   android：permission = “com.google.socialapp.permission.SHARE_POST”
/>
```

应用二

```xml
<manifest>
   <uses-permission android：name =“com.google.socialapp.permission.SHARE_POST” />  
</manifest>
```

这样应用二才能启动应用一中对应的Activity

## 生命周期

![Activity](../assets/Activity.png)

## 启动模式 launchMode

| 启动模式 | 多个实例 | 注释 |
|---------|---------|-----|
| standard | 是 | 默认值。系统始终会在目标任务中创建新的 Activity 实例并向其传送 Intent。|
| singleTop | 有条件 | 如果目标任务的顶部已存在一个 `Activity` 实例，则系统会通过调用该实例的 `onNewIntent()` 方法向其传送 `Intent`，而不是创建新的 `Activity` 实例。 |
| singleTask | 否 | 系统在新任务的根位置创建 `Activity` 并向其传送 `Intent`。 不过，如果已存在一个 `Activity` 实例，则系统会通过调用该实例的 `onNewIntent()` 方法向其传送 `Intent`，而不是创建新的 `Activity` 实例。 |
| singleInstance | 否 | 与 `singleTask` 相同，只是系统不会将任何其他 `Activity` 启动到包含实例的任务中。 该 `Activity` 始终是其任务唯一仅有的成员。 |

`standard` 和 `singleTop` 适用于大多数 Activity 的正常启动

`singleTask` 和 `singleInstance` 专用启动
（不建议用作常规用途）

总结：主要还是在不同应用之间相互启动需要用到
