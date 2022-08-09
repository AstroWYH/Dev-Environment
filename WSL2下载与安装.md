# WSL2下载与安装

### 下载安装

[参考链接：技术胖-Windows11 中安装Linux 教程 | WSL2的使用 (jspang.com)](http://jspang.com/detailed?id=80)

- **第一步**：启动WSL。用管理员身份打开`PowerShell`.(打开方法见视频)，然后在PowerShell中，输入下面的命令。

  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

- **第二步**：启动虚拟机给功能。同样在PoweShell中输入下面的命令。输入完命令后，要重启一下电脑，然后再进行第三步。

  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

- **第三步**：下载Linux内核更新包，并点击安装。

> 下载地址：https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

- **第四步**：将WSL2设置为默认版本。打开 PowerShell，然后在安装新的 Linux 发行版时运行以下命令，将 WSL 2 设置为默认版本，命令如下。

  wsl --set-default-version 2

- **第五步**：安装Ubuntu发行版

下载地址：[旧版 WSL 的手动安装步骤 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/wsl/install-manual#step-3---enable-virtual-machine-feature)

![image-20220810012835259](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/image-20220810012835259.png)

![image-20220810012902485](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/image-20220810012902485.png)

### 确认安装

参考链接：[安装 WSL | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/wsl/install)

![image-20220810012921619](https://hanbabang-1311741789.cos.ap-chengdu.myqcloud.com/image-20220810012921619.png)