## 内容

1. 进入 ADB 目录

   Adb 命令在 AndroidSDK\platform-tools 下面，使用之前先进入该目录。Eg:

   Cd E:\AndroidSDK\platform-tools

2. 安装 app

   adb  install C:\Users\Administrator\Desktop\Baymaxa_yideng.apk

   强制安装  adb  install -r C:\Users\Administrator\Desktop\Baymaxa_yideng.apk

3. 卸载 app

    卸载以 app 包名的形式进行卸载，故应该知道要卸载 app 的包名

   adb uninstall com.cmsa.android.baymaxa

4. 查看设备上已经安装的应用包名

   adb shell pm list packages

5. 关闭或者开启 adb 服务

   关闭adb服务 adb kill-server

   开启adb服务 adb start-server

6. Android 应用安装涉及到如下几个目录

   system/app系统自带的应用程序，无法删除。

   data/app用户程序安装的目录，有删除权限。安装时把apk文件复制到此目录。

   data/data存放应用程序的数据。

   data/dalvik-cache将apk中的dex文件安装到dalvik-cache目录下(dex文件是dalvik虚拟机的可执行文件,其大小约为原始apk文件大小的四分之一)。

   APP安装过程：复制APK安装包到data/app目录下，解压并扫描安装包，把dex文件(Dalvik字节码)保存到dalvik-cache目录，并data/data目录下创建对应的应用数据目录。

   APP卸载过程：删除安装过程中在上述三个目录下创建的文件及目录。