### 使用VS2017的“高级保存选项”

由于这个选项在vs2017中是默认隐藏的，需要手动调出来。具体操作方法如下：

1、单击“工具”➡“自定义”，弹出“自定义”对话框。
2、单击“命令”标签➡进入“命令”选项卡。
3、“菜单栏”下拉列表➡选择“文件”选项。
4、单击“添加命令”➡弹出“添加命令”对话框。
5、在“类别”列表中，选择“文件”选项；在“命令”列表中，选择“高级保存选项”选项。
6、单击“确定”按钮，关闭“添加命令”对话框。
7、选中“控件”列表中的“高级保存选项”选项，单击“上移”或者“下移”按钮，可以调整该命令的位置。
8、单击“关闭”按钮，完成“高级保存选项”命令的添加操作

然后选中高级保存选项，弹出的对话框可以选择编码utf-8。

![image-20221130145530436](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221130145530436.png)

![image-20221130145543112](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221130145543112.png)

### **使用ForceUTF8插件**

工具➡拓展和更新➡联机➡搜索框输入“**ForceUTF8**”➡下载安装

安装此插件后，所有文件均会以utf-8编码格式保存，方便省心。

![image-20221130145557837](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221130145557837.png)

### **指定使用utf-8编译**

**选中当前项目——右键属性——配置属性——C/C++——命令行——输入/utf-8**
只有完成这一步，warning信息才会真正消失。

![image-20221130145620983](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/Pics/image-20221130145620983.png)

然而，改完后我又发现了一个新问题，那就是vs2017的控制台也是默认使用GB2313编码的，所以控制台又乱码了→_→(我太难了)…
ps：查看控制台所用编码的方法：点击控制台标题栏左上角–>属性–>选项–>找到当前代码页能看到编码格式。

### 更改控制台的编码格式为utf-8

1.按下**win(windows键)+R**，输入**regedit**然后回车进入到**注册表编辑器**

2.找到 **计算机\HKEY_CURRENT_USER\Console**

3.寻找有**vs、console**等字符串的相关项

4.修改**CodePage**值

选中右边栏CodePage，右键将其值936(该值对应GB2312)修改其值为65001（该值对应的就是utf-8编码），上图我已经更改过了。
修改完后，用vs编译运行C++就不会出现控制台乱码了。

ps:以上方法也同样适合更改windows系统控制台的编码格式。

如果注册表没找到，则在代码main.cpp中设置也行：

```cpp
#include <windows.h>

int main() {
    SetConsoleOutputCP(CP_UTF8);
}
```

#### 参考链接

[(36条消息) VS2017修改编码格式为utf-8，再也不用担心乱码了_夏虫爱语冰的博客-CSDN博客_vs的编码格式](https://blog.csdn.net/Love_Point/article/details/105658241)

[(36条消息) C++ cout输出中文信息乱码问题解决_一个与程序bug抗争的程序员的博客-CSDN博客_setconsoleoutputcp(cp_utf8);](https://blog.csdn.net/qq_42416602/article/details/124370399)

