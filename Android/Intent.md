# Intent

本节介绍几种可用于执行常见操作的隐式 `Intent`

当您调用 `startActivity()` 或 `startActivityForResult()` 并向其传递隐式 `Intent` 时，系统会 将 `Intent` 解析为可处理该 `Intent` 的应用并启动其对应的 `Activity`。 如果有多个应用可处理 Intent，系统会为用户显示一个对话框，供其选择要使用的应用。

> 注意：如果设备上没有可接收隐式 `Intent` 的应用，您的应用将在调用 `startActivity()` 时崩溃。所以要先对 `Intent` 对象调用 `resolveActivity()`。如果结果为非空，则至少有一个应用能够处理，如果结果为空，则您不应使用该 `Intent`。

## 闹铃

### 创建闹铃

```java
public void createAlarm(String message, int hour, int minutes) {
    Intent intent = new Intent(AlarmClock.ACTION_SET_ALARM)
            .putExtra(AlarmClock.EXTRA_MESSAGE, message)
            .putExtra(AlarmClock.EXTRA_HOUR, hour)
            .putExtra(AlarmClock.EXTRA_MINUTES, minutes);
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivity(intent);
    }
}
```

| 参数 | 说明 |
|------|------|
| EXTRA_HOUR | 闹铃的小时 |
| EXTRA_MINUTES | 闹铃的分钟 |
| EXTRA_MESSAGE | 用于标识闹铃的自定义消息 |
| EXTRA_DAYS | 一个 ArrayList，其中包括应重复触发该闹铃的每个周日。 每一天都必须使用 Calendar 类中的某个整型值（如 MONDAY）进行声明。对于一次性闹铃，无需指定此 extra |
| EXTRA_VIBRATE | 一个布尔型值，用于指定该闹铃触发时是否振动 |
| EXTRA_RINGTONE | 一个 content: URI，用于指定闹铃使用的铃声，也可指定 VALUE_RINGTONE_SILENT 以不使用铃声。如需使用默认铃声，则无需指定此 extra |
| EXTRA_SKIP_UI | 一个布尔型值，用于指定响应闹铃的应用在设置闹铃时是否应跳过其 UI。 若为 true，则应用应跳过任何确认 UI，直接设置指定的闹铃 |

所需权限

```xml
<uses-permission android:name="com.android.alarm.permission.SET_ALARM" />
```

### 创建定时器

```java
public void startTimer(String message, int seconds) {
    Intent intent = new Intent(AlarmClock.ACTION_SET_TIMER)
            .putExtra(AlarmClock.EXTRA_MESSAGE, message)
            .putExtra(AlarmClock.EXTRA_LENGTH, seconds)
            .putExtra(AlarmClock.EXTRA_SKIP_UI, true);
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivity(intent);
    }
}
```

| 参数 | 说明 |
|------|------|
| EXTRA_LENGTH | 以秒为单位的定时器定时长度 |
| EXTRA_MESSAGE | 用于标识定时器的自定义消息 |
| EXTRA_SKIP_UI | 一个布尔型值，用于指定响应定时器的应用在设置定时器时是否应跳过其 UI。 若为 true，则应用应跳过任何确认 UI，直接启动指定的定时器 |

所需权限

```xml
<uses-permission android:name="com.android.alarm.permission.SET_ALARM" />
```

### 显示所有闹铃

操作：

    ACTION_SHOW_ALARMS

## 相机

### 拍摄照片或视频并将其返回

```java
static final int REQUEST_IMAGE_CAPTURE = 1;
static final Uri mLocationForPhotos;

public void capturePhoto(String targetFilename) {
    Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
    intent.putExtra(MediaStore.EXTRA_OUTPUT,
            Uri.withAppendedPath(mLocationForPhotos, targetFilename));
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivityForResult(intent, REQUEST_IMAGE_CAPTURE);
    }
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_IMAGE_CAPTURE && resultCode == RESULT_OK) {
        Bitmap thumbnail = data.getParcelable("data");
        // Do other work with full size photo saved in mLocationForPhotos
        ...
    }
}
```

| 参数 | 说明 |
|------|------|
| ACTION_IMAGE_CAPTURE | 打开相机拍摄照片 |
| ACTION_VIDEO_CAPTURE | 打开相机拍摄视频 |
| EXTRA_OUTPUT | 相机应用应将照片或视频文件保存到的 URI 位置（Uri 对象形式）|

如需了解有关如何使用此 Intent 拍摄照片的详细信息,请阅读[只拍摄照片](https://developer.android.google.cn/training/camera/photobasics.html?hl=zh-cn)或[只拍摄视频](https://developer.android.google.cn/training/camera/videobasics.html?hl=zh-cn)

## 联系人\通讯录

### 选择联系人

让用户选择联系人和为您的应用提供对所有联系人信息的访问权限

`onActivityResult()` 会收到回调结果，响应会利用 `Contacts Provider API` 为您的应用授予该联系人的临时读取权限，即使您的应用不具备 `READ_CONTACTS` 权限也没有关系。

```java
static final int REQUEST_SELECT_CONTACT = 1;

public void selectContact() {
    Intent intent = new Intent(Intent.ACTION_PICK);
    intent.setType(ContactsContract.Contacts.CONTENT_TYPE);
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivityForResult(intent, REQUEST_SELECT_CONTACT);
    }
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_SELECT_CONTACT && resultCode == RESULT_OK) {
        Uri contactUri = data.getData();
        // Do something with the selected contact at contactUri
        ...
    }
}
```

如需了解有关在获得联系人 `URI` 后如何检索联系人详情的信息，请阅读[检索联系人详情](https://developer.android.google.cn/training/contacts-provider/retrieve-details.html?hl=zh-cn)。 请谨记，使用以上 Intent 检索联系人 `URI` 时，读取该联系人的详情并不需要 `READ_CONTACTS` 权限

返回值示例：

    content://com.android.contacts/contacts/lookup/3857r23-55A08703/23

### 选择特定联系人数据

让用户选择某一条联系人信息，如电话号码、电子邮件地址或其他数据类型

`onActivityResult()` 会收到回调结果，响应会利用 `Contacts Provider API` 为您的应用授予该联系人的临时读取权限，即使您的应用不具备 `READ_CONTACTS` 权限也没有关系。

```java
static final int REQUEST_SELECT_PHONE_NUMBER = 1;

public void selectContact() {
    // Start an activity for the user to pick a phone number from contacts
    Intent intent = new Intent(Intent.ACTION_PICK);
    intent.setType(CommonDataKinds.Phone.CONTENT_TYPE);
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivityForResult(intent, REQUEST_SELECT_PHONE_NUMBER);
    }
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_SELECT_PHONE_NUMBER && resultCode == RESULT_OK) {
        // Get the URI and query the content provider for the phone number
        Uri contactUri = data.getData();
        String[] projection = new String[]{CommonDataKinds.Phone.NUMBER};
        Cursor cursor = getContentResolver().query(contactUri, projection,
                null, null, null);
        // If the cursor returned is valid, get the phone number
        if (cursor != null && cursor.moveToFirst()) {
            int numberIndex = cursor.getColumnIndex(CommonDataKinds.Phone.NUMBER);
            String number = cursor.getString(numberIndex);
            // Do something with the phone number
            ...
        }
    }
}
```

| MIME 类型 | 说明 |
|------|------|
| CommonDataKinds.Phone.CONTENT_TYPE | 从有电话号码的联系人中选取 |
| CommonDataKinds.Email.CONTENT_TYPE | 从有电子邮件地址的联系人中选取 |
| CommonDataKinds.StructuredPostal.CONTENT_TYPE | 从有邮政地址的联系人中选取 |

或者 `ContactsContract` 下众多其他 `CONTENT_TYPE` 值中的一个

### 查看联系人

显示已知联系人的详情，并使用 `content: URI` 作为 `Intent` 数据指定联系人

```java
public void viewContact(Uri contactUri) {
    Intent intent = new Intent(Intent.ACTION_VIEW, contactUri);
    if (intent.resolveActivity(getPackageManager()) != null) {
        startActivity(intent);
    }
}
```

> 貌似并没有什么用

## 电子邮件

