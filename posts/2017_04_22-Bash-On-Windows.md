# Windows+Linux
## 冗长的背景
想必很多同行都很纠结到底应该用哪个系统——Windows稳定、易用、应用程序多；但却定制性差、在开发上有很多限制。平时用的话肯定是Windows更省事儿一点，但搬砖的时候还是首选Linux。以至于很多人都无奈地装上了双系统或者虚拟机，双系统浪费空间、不能随时切换；而虚拟机不能充分利用机器资源、特别是GPU...   

最近在查资料时发现Win10竟然有`subsystem`这么一个东西，目前还在测试版。简单的说，就是在Windows上拿出几个G的空间放上Ubuntu14.04的文件系统，以及在Windows上支持使用Ubuntu的bash，相当于在Windows上装了一个Ubuntu系统，操作起来的感觉跟远程ssh服务器没什么区别。但是，一点点的改进就是质变——由于subsystem就在Windows，其文件系统是共享的！！！这也就意味着，你可以开着Windows的编辑器/IDE写程序，然后随便开一个bash在Linux上运行，之间的衔接毫无违和感。

## 准备
系统>= Windows RedStone(Anniversary)
[官网](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)

## 安装（官方翻译版）
* 打开电脑的设置->更新和安全->针对开发人员->使用开发人员功能->开发人员模式; 如果安装功能失败的自行去系统服务里启动Windows Update
* 在搜索框里搜“Turn Windows features on or off”，然后选择“启动或关闭Windows功能”，勾选“适用于Linux的Windows子系统（beta）”
* 在搜索框里搜“Powershell”，右键管理员模式启动“Powershell”，运行命令“Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux”
* 重启
* 随便开一个cmd，输入bash，按提示完成创建账户操作
* 安装完成，以后在命令行输入bash即可进入Linux

## 补充
* PowerShell不能启动bash：可能的权限问题——“Set-ExecutionPolicy RemoteSigned -Scope CurrentUser”来更改执行脚本的权限。
* Atom中的PowerShell不能启动bash：原因在于bash.exe在系统文件夹中，Atom根本看不到bash.exe——把bash.exe随便copy到一个没权限的但却在环境变量path里的位置，即时见效。
* 设置图形界面——export DISPLAY=:0


## 没什么意思的后记
用Atom写代码，下面开着Windows的PowerShell和Linux的bash，Linux中装有tf、torch、gym等环境，图形界面如果需要的话再开一个X-manager，惊喜的组合。

于是忍不住要安利一下Win10，为什么使用Win10：
1. 状态栏的搜索框
2. 多工作空间（目前只支持水平的还不够爽，看看会不会改成循环的或者二维的）
3. Bash On Windows

当然，如果你用的是2~3年前的旧机器，慎用Win10，慎用Win10，慎用Win10！硬件问题可能会让你得到完全不同的体验。

还有说用Mac的？你用Mac还能看到这儿？也是够无聊的。。。