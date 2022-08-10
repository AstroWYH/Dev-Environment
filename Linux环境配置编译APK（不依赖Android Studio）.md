# Linux环境配置编译APK（不依赖Android Studio）

### 1 下载commandlinetools，配置SDK、NDK环境

下载地址：[Download Android Studio & App Tools - Android Developers (google.cn)](https://developer.android.google.cn/studio)

![image-20220810210628749](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220810210628749.png)

新建latest文件夹，并将cmdline-tools的内容全部mv到latest内，目录结构如下

![image-20220810210645577](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220810210645577.png)

找到bin文件夹下的sdkmanager，执行./sdkmanager --list

![image-20220810210655794](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220810210655794.png)

找到列表中的以下几个模块依次进行安装，分别执行./sdkmanager --install "platforms;android-28"; ......

![image-20220810210711604](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220810210711604.png)

依次安装好后，上述模块会出现在cmdline-tools的外层目录

![image-20220810210722722](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20220810210722722.png)

### 2 配置代码环境

在仓库根目录的local.properties配置SDK、NDK路径，如无local.properties则新建即可

![image-20220811010046561](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/image-20220811010046561.png)

确保仓库根目录的build.gradle版本，和gradle-wrapper.properties的gradle版本

```c
// 根目录build.gradle
    dependencies {
        classpath 'com.android.tools.build:gradle:4.0.0'
    }

// gradle-wrapper.properties
distributionUrl=https\://services.gradle.org/distributions/gradle-6.1.1-all.zip
```

### 3 通过Gradle编译生成Apk

./gradlew clean：如果之前没安装过gradle，此时会根据工程已有配置下载安装相应版本的gradle

./gradlew tasks：查看有哪些可以执行的任务

./gradlew [具体任务]