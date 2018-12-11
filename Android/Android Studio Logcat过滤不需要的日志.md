使用模拟器经常会打印出很多不想看的系统日志

这时候在`EditFileterConfig`里新建一个过滤，在`Log Tag`里输入

    ^(?!.*(TAG1|TAG2)).*$
    
TAG1和TAG2表示你要过滤的标签

很nice！