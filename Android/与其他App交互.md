# 与其他App交互

## 向另一个应用发送信息

默认情况下，系统基于所包含的 `Uri` 数据确定 `Intent` 需要的相应 MIME 类型。

举例：

1.发起电话呼叫

```java
Uri number = Uri.parse("tel:5551234");
Intent callIntent = new Intent(Intent.ACTION_DIAL, number);
startActivity(callIntent)
```

2.查看地图

```java
// Map point based on address
Uri location = Uri.parse("geo:0,0?q=1600+Amphitheatre+Parkway,+Mountain+View,+California");
// Or map point based on latitude/longitude
// Uri location = Uri.parse("geo:37.422219,-122.08364?z=14"); // z param is zoom level
Intent mapIntent = new Intent(Intent.ACTION_VIEW, location);
startActivity(mapIntent)
```

3.查看网页

```java
Uri webpage = Uri.parse("http://www.android.com");
Intent webIntent = new Intent(Intent.ACTION_VIEW, webpage);
startActivity(webIntent)
```

如果您未在 `Intent` 中包含 `Uri`，您通常应使用 `setType()` 指定与 `Intent` 关联的数据的类型。

举例：

1.发送带附件的电子邮件

```java
Intent emailIntent = new Intent(Intent.ACTION_SEND);
// The intent does not have a URI, so declare the "text/plain" MIME type
emailIntent.setType(HTTP.PLAIN_TEXT_TYPE);
emailIntent.putExtra(Intent.EXTRA_EMAIL, new String[] {"jon@example.com"}); // recipients
emailIntent.putExtra(Intent.EXTRA_SUBJECT, "Email subject");
emailIntent.putExtra(Intent.EXTRA_TEXT, "Email message text");
emailIntent.putExtra(Intent.EXTRA_STREAM, Uri.parse("content://path/to/email/attachment"));
// You can also attach multiple items by passing an ArrayList of Uris
```

2.创建日历事件

```java
Intent calendarIntent = new Intent(Intent.ACTION_INSERT, Events.CONTENT_URI);
Calendar beginTime = Calendar.getInstance().set(2012, 0, 19, 7, 30);
Calendar endTime = Calendar.getInstance().set(2012, 0, 19, 10, 30);
calendarIntent.putExtra(CalendarContract.EXTRA_EVENT_BEGIN_TIME, beginTime.getTimeInMillis());
calendarIntent.putExtra(CalendarContract.EXTRA_EVENT_END_TIME, endTime.getTimeInMillis());
calendarIntent.putExtra(Events.TITLE, "Ninja class");
calendarIntent.putExtra(Events.EVENT_LOCATION, "Secret dojo");
```

尽可能具体地定义您的 `Intent` 非常重要。例如，如果您想要使用 `ACTION_VIEW` Intent 显示图像，您应指定 `MIME` 类型 `image/*`。这可防止可“查看”数据的其他类型的应用（比如地图应用）被 Intent 触发。

具体的 `ACTION` 字段可以查看文档。

## 验证是否存在接收 `Intent` 的应用

尽管 `Android` 平台保证某些 Intent 可以分解为内置应用之一（比如，“电话”、“电子邮件”或“日历”应用），您应在调用 Intent 之前始终包含确认步骤。如果您调用了 `Intent`，但设备上没有可用于处理 Intent 的应用，您的应用将崩溃。

所以发送之前先确认非常重要。

```java
PackageManager packageManager = getPackageManager();
List activities = packageManager.queryIntentActivities(intent,
        PackageManager.MATCH_DEFAULT_ONLY);
boolean isIntentSafe = activities.size() > 0;
```

如果 `isIntentSafe` 是 `true`，则至少有一个应用将响应该 Intent。 如果它是 `false`，则没有任何应用处理该 `Intent`。

## 启动具有 `Intent` 的 `Activity`

一旦您已创建您的 `Intent` 并设置 extra 信息，调用 `startActivity()` 将其发送给系统。如果系统识别可处理 Intent 的多个 `Activity`，它会为用户显示对话框供其选择要使用的应用，并且用户可以选择默认使用哪个应用。但是，如果要执行的操作可由多个应用处理并且用户可能 习惯于每次选择不同的应用 — 比如“共享”操作， 用户有多个应用分享项目 — 您应明确显示选择器对话框，使用 `createChooser()` 创建Intent 并将其传递给 `startActivity()`。

举例：

```java
Intent intent = new Intent(Intent.ACTION_SEND);
...

// Always use string resources for UI text.
// This says something like "Share this photo with"
String title = getResources().getString(R.string.chooser_title);
// Create intent to show chooser
Intent chooser = Intent.createChooser(intent, title);

// Verify the intent will resolve to at least one activity
if (intent.resolveActivity(getPackageManager()) != null) {
    startActivity(chooser);
}
```