# RxJava

响应式编程(Reactive Programming)就是一个编程范式，它是基于数据流和变化传播。

将操作抽象成一个个事件，然后监听事件的结果。在异步方面表现出色。

最直接的替代就是 handler，切换线程。

**总体思路**

1. 创建事件，可以数据，也可以是用户操作，比如点击等；
2. 处理事件，比如验证输入是否合法、将输入的内容发送到网络上等；
3. 接收结果，有正确结果、错误结果等。

**创建事件**

- create() 
- just()
- from()
- ...

**处理事件**

- map()
- flapMap()
- scan()
- filter()
- ...

**结果回调**

- subscribe()

如果实现 Observer 接口则监听多种情况，如果实现 Consumer 则只监听正常的回调。

## 使用

最新版请参考 [官网](https://github.com/ReactiveX/RxAndroid) 。

### 导入

设置仓库，以及两个库，rxandroid 是针对Android设计的，有专门的线程调度。

```
allprojects {
    repositories {
        maven { url "https://oss.jfrog.org/libs-snapshot" }
    }
}

dependencies {
    implementation 'io.reactivex.rxjava3:rxandroid:3.0.0'
    // Because RxAndroid releases are few and far between, it is recommended you also
    // explicitly depend on RxJava's latest version for bug fixes and new features.
    // (see https://github.com/ReactiveX/RxJava/releases for latest 3.x.x version)
    implementation 'io.reactivex.rxjava3:rxjava:3.0.0'
}
```

### 用法示例

简单用法

```java
// 生成 Observable 事件，这里输入字符串
Observable.just(editText.getText().toString())
        // 处理事件
        .map(new Function<String, Integer>() {
            @Override
            public Integer apply(String s) throws Throwable {
                Log.d(TAG, "apply: " + s);
                return s.length();
            }
        })
        // 处理事件的线程
        .subscribeOn(Schedulers.io())
        // 接收事件的线程，Android中一般都在主线程
        .observeOn(AndroidSchedulers.mainThread())
        // 接收结果
        .subscribe(new Consumer<Integer>() {
            @Override
            public void accept(Integer length) throws Throwable {
                Log.d(TAG, "accept: length=" + length);
            }
        });
```

异步加载图片

```java
String path = "http://www.xxoo.com/1.png"
Observable.just()
        .map(new Function<String, Bitmap>() {
            @Override
            public Bitmap apply(@NonNull String s) throws Exception {
                // 从网络获取数据，返回Bitmap类型
            }
        })
        .subscribeOn(AndroidSchedulers.mainThread())
        .observeOn(Schedulers.newThread())
        .subscribe(new Consumer<Bitmap>() {
            @Override
            public void accept(Bitmap bitmap) throws Exception {
                
            }
        });
```

界面需要等到多个接口并发取完数据，再更新

```java
Observable<String> observable1 = Observable.create(new ObservableOnSubscribe<String>() {
        @Override
        public void subscribe(ObservableEmitter<String> e) throws Exception {
            e.onNext("haha");
        }
    }).subscribeOn(Schedulers.newThread());

    Observable<String> observable2 = Observable.create(new ObservableOnSubscribe<String>() {
        @Override
        public void subscribe(ObservableEmitter<String> e) throws Exception {
            e.onNext("hehe");
        }
    }).subscribeOn(Schedulers.newThread());


    Observable.merge(observable1, observable2)
            .subscribeOn(Schedulers.newThread())
            .subscribe(new Observer<String>() {
                @Override
                public void onSubscribe(Disposable d) {

                }

                @Override
                public void onNext(String value) {
                    Log.d(TAG,value);
                }

                @Override
                public void onError(Throwable e) {

                }

                @Override
                public void onComplete() {

                }
            });
```