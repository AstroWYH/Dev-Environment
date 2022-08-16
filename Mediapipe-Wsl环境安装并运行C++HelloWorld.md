# Mediapipe-Wsl环境安装并运行C++HelloWorld.md

[Installation - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/install.html#installing-on-windows)

[MediaPipe in C++ - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/cpp.html)

[Hello World! on Android - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/hello_world_android.html)

```shell
# 安装bazel
sudo apt install curl
curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
echo "deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
sudo apt-get update 
sudo apt-get install bazel # 安装bazel
sudo apt-get install --only-upgrade bazel # 升级bazel到最新版本

bazel version

# 安装opencv，采用官网提供的Option 2
Option 2. Run setup_opencv.sh to automatically build OpenCV from source and modify MediaPipe’s OpenCV config.

# 运行Hello World! in C++ example.
~/mediapipe$ export GLOG_logtostderr=1
~/mediapipe$ bazel run --define MEDIAPIPE_DISABLE_GPU=1 \
    mediapipe/examples/desktop/hello_world:hello_world

# Should print:
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
# Hello World!
```


### 完整安装后的mediapipe diff

```diff
diff --git a/WORKSPACE b/WORKSPACE
index 7a75537..730bc5b 100644
--- a/WORKSPACE
+++ b/WORKSPACE
@@ -191,7 +191,7 @@ http_archive(
 new_local_repository(
     name = "linux_opencv",
     build_file = "@//third_party:opencv_linux.BUILD",
-    path = "/usr",
+    path = "/usr/local",
 )
 
 new_local_repository(
@@ -417,3 +417,5 @@ libedgetpu_dependencies()
 
 load("@coral_crosstool//:configure.bzl", "cc_crosstool")
 cc_crosstool(name = "crosstool")
+android_sdk_repository(name = "androidsdk", path = "/home/hanbabang/1_software/mediapipe_tools/Sdk")
+android_ndk_repository(name = "androidndk", api_level=21, path = "/home/hanbabang/1_software/mediapipe_tools/Ndk/android-ndk-r21")
diff --git a/setup_android_sdk_and_ndk.sh b/setup_android_sdk_and_ndk.sh
index edb27de..bd056b0 100644
--- a/setup_android_sdk_and_ndk.sh
+++ b/setup_android_sdk_and_ndk.sh
@@ -18,6 +18,7 @@
 # usage:
 # $ cd <mediapipe root dir>
 # $ bash ./setup_android_sdk_and_ndk.sh ~/Android/Sdk ~/Android/Ndk r21 [--accept-licenses]
+# bash ./setup_android_sdk_and_ndk.sh /home/hanbabang/1_software/mediapipe_tools/Sdk /home/hanbabang/1_software/mediapipe_tools/Ndk
 
 set -e
 
@@ -59,7 +60,7 @@ then
   ndk_version="r21"
 fi
 
-if [ -d "$android_sdk_path" ]
+if [ -d "$android_sdk_path/some_version" ]
 then
   echo "Warning: android_sdk_path is non empty. Installation of the Android SDK will be skipped."
 else
diff --git a/third_party/opencv_linux.BUILD b/third_party/opencv_linux.BUILD
index 8445855..6ca91a0 100644
--- a/third_party/opencv_linux.BUILD
+++ b/third_party/opencv_linux.BUILD
@@ -28,6 +28,7 @@ cc_library(
         #"include/opencv4/",
     ],
     linkopts = [
+        "-L/usr/local/lib",
         "-l:libopencv_core.so",
         "-l:libopencv_calib3d.so",
         "-l:libopencv_features2d.so",
```





