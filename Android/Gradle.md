# Gradle

Gradle 是一个能通过插件形式自定义构建逻辑的优秀构建工具。Android就使用了Gradle来构建工程。

它使用基于Groovy的特定领域语言(DSL)来声明项目，而不再是XML。

Grovvy：基于Java虚拟机的动态语言

# 项目构建历史

1.石器时代

将依赖库放到lib目录，通过Eclipse打包然后上传服务器

纯手动，重复且繁琐。

2.工业时代

出现了构建工具，做依赖管理，自动化测试打包发布。

**Ant** -> **Maven** -> **Gradle**

## 项目结构

| 目录 | 说明 |
|---|---|
| `src/main/java` | 正式代码 |
| `src/main/resource` | 正式资源 |
| `src/test/java` | 测试代码 |
| `src/test/resource` | 测试资源 |
| `src/main/webapp` | 页面，html，css，js等 |

## 语法

```Grovvy
// 和Python类似，脚本语言风格
hello = "hello Grovvy"

println(hello)

// 列表
mlist = []
mlist.add(1)
mlist.add(2)
mlist.add(3)
mlist.add(4)
println(mlist)

// 字典
map = ["a":1, "b":2]
println(map)

// 函数用def
def add(int a, int b) {
    return a + b
}

println(add(1, 5))

// 类
class MyClass {
    private name
    private age
}

// 闭包
// 就是一段代码，把它当做参数
bb = {
    println("hehehe")
}

def m1(Closure closure) {
    closure()
}
// 调用
m1(bb)
// 也可以直接写在函数里
m1 {
    println("hahaha")
}

// 带参数的闭包
def bba = {
    v ->
        println("good ${v}")
}
def m2(Closure closure) {
    closure("boy")
}
m2(bba)
```

## 配置文件

Gradle 工程所有依赖都在 dependencies 属性内

每个依赖有三个基本元素：group、name和version。

test开头的依赖表示依赖在测试的时候起作用。

写法有几种：

**group:name:version**

    implementation 'commons-lang:commons-lang:2.6'

**键值对**

    implementation group: 'com.google.code.guice', name: 'guice', version: '1.0'

**依赖文件**

    implementation files('hibernate.jar', 'libs/spring.jar')

**依赖文件夹**

    implementation fileTree('libs')

**依赖模块**

    implementation project(':someProject') // 只能访问依赖模块的接口，而不能访问依赖的依赖
    api project(':someProject') // 可以访问依赖的依赖

比如：

``` 
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.0.2'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation 'androidx.lifecycle:lifecycle-extensions:2.0.0'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
    implementation project(':myservice')
}
```

## 仓库

依赖的jar包需要从仓库中下载，所以我们还需要指定仓库。

```
// 表示所有模块都能使用
allprojects {
    // 指定使用的仓库，按照顺序找
    repositories {
        // https://dl.google.com/dl/android/maven2/
        google()
        // https://jcenter.bintray.com/
        jcenter()
        // Maven 中央仓库
        mavenCentral()
        // Maven本地仓库
        mavenLocal()
    }
}
```

## 构建任务

```
// 任务t1
task t1 {
    println("hello t1")
}

// 任务t2，依赖于任务t1
task t2(dependsOn: 't1') {
    doFirst {
        println('t2 do first')
    }
    println('hello t2')
    doLast {
        println('t2 do last')
    }
}
```

执行任务t2时的输出：

```
> Configure project :myservice
hello t1
hello t2

> Task :myservice:t1 UP-TO-DATE

> Task :myservice:t2
t2 do first
t2 do last

BUILD SUCCESSFUL in 89ms
1 actionable task: 1 executed
1:24:27 PM: Task execution finished 't2'.
```

结论：构建工程时就调用了任务t1和t2，但是执行t2时才执行doFirst和doLast里的内容。

## 发布项目

1. 添加插件，比如：Maven-publish
2. 配置发布任务
3. 执行发布(远程私有仓库、本地仓库或者中央仓库)

发布jar包举例：

```
// 声明插件
apply plugin: 'maven-publish'

// 发布任务
publishing {
    // 发布工程
    publications {
        // publishProject 为自定义名称，可写多个发布任务
        publishProject (MavenPublication) {
            from components.java // 发布jar包
        }
    }
    repositories {
        // Maven仓库地址
        maven {
            url=""
            // 用户名和密码
            credentials {
                username 'root'
                password 'admin'
            }
        }
    }
}
```

发布aar文件举例：

```
// Because the components are created only during the afterEvaluate phase, you must
// configure your publications using the afterEvaluate() lifecycle method.
afterEvaluate {
    publishing {
        publications {
            // Creates a Maven publication called "release".
            release(MavenPublication) {
                // Applies the component for the release build variant.
                from components.release

                // You can then customize attributes of the publication as shown below.
                groupId = 'com.example.MyLibrary'
                artifactId = 'final'
                version = '1.0'
            }
            // Creates a Maven publication called “debug”.
            debug(MavenPublication) {
                // Applies the component for the debug build variant.
                from components.debug

                groupId = 'com.example.MyLibrary'
                artifactId = 'final-debug'
                version = '1.0'
            }
        }
    }
}
```

点击IDEA右侧的Gradle边栏，执行publishing中的任务即可。

参考 [官网使用 Maven Publish 插件](https://developer.android.google.cn/studio/build/maven-publish-plugin?hl=zh_cn) 。