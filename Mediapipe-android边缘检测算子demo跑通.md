# Mediapipe-android边缘检测算子demo跑通

[Installation - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/install.html#installing-on-windows)

[MediaPipe in C++ - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/cpp.html)

[Hello World! on Android - mediapipe (google.github.io)](https://google.github.io/mediapipe/getting_started/hello_world_android.html)

### 此前，需保证C++ HelloWorld能成功跑通

```shell
# 配置SDK、NDK
bash ./setup_android_sdk_and_ndk.sh /home/hanbabang/1_software/mediapipe_tools/Sdk /home/hanbabang/1_software/mediapipe_tools/Ndk

# 执行android边缘检测算子demo
cd mediapipe/mediapipe/examples/android/src/java/com/google/mediapipe/apps/basic
bazel build -c opt --config=android_arm64 $APPLICATION_PATH:helloworld
# 会执行一大堆东西，包括下载库、jar包等
# 生成apk路径，bazel-bin在mediapipe根目录
bazel-bin -> /root/.cache/bazel/_bazel_root/4b7f38d105cd186c4a902278281b726c/execroot/mediapipe/bazel-out/arm64-v8a-opt/bin
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