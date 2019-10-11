# Eclipse问题

## Eclipse中Android SDK Content Loader 0%的解决方法

进入 *C：\用户\用户名\\.android* 文件夹，删除 **cache** 文件夹和 **ddms.cfg** 文件。    

其中，**cache**文件夹中保存了Eclipse的缓存文件；**ddms.cfg**是Android平台自带调试工具DDMS（Dalvik Debug Monitor Server）的配置文件。删除了缓存文件和配置文件后，Eclipse就会使用默认的配置导入SDK。

此时，启动Eclipse，会弹出“是否向Google发送统计数据”对话框，如图3所示。选择“No”，之后点击“Finish”按键。Android SDK Content Loader导入开始，不会卡在0%处了。