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

