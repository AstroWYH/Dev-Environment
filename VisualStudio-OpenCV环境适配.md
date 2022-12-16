[(39条消息) VS配置永久OpenCV（小萌轻松操作）：超细致_小胖子aba的博客-CSDN博客_vsopencv配置](https://blog.csdn.net/weixin_54583016/article/details/121424060?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-121424060-blog-122349918.pc_relevant_landingrelevant&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~Rate-1-121424060-blog-122349918.pc_relevant_landingrelevant&utm_relevant_index=1)

### 环境变量

D:\OpenCV4.5\opencv\build\x64\vc15\bin
D:\OpenCV4.5\opencv\build\x64\vc15\lib

### 属性表

对属性表进行配置：VC++目录—>包含目录—>库目录。包含目录中添加：
D:\opencv\build\include
D:\opencv\build\include\opencv2

在库目录中添加：D:\opencv\build\x64\vc15\lib

然后对链接器—>输入—>附加依赖项—>编辑
附加依赖项中添加（库文件名）：opencv_world450d.lib

如果配置为Debug，选择opencv_world450d.lib
如果为Release，选择opencv_world450.lib