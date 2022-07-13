## adb 常用命令

查看设备网络信息：

```cmd
adb shell ifconfig
```

查看网络地址和端口：

``` cmd
adb shell netstat
```

重置tcpip端口：

``` cmd
adb tcpip 5555
```

Android Studio 使用WiFi连接设备

``` cmd
adb connect 192.168.x.x:5555
```

改变设备宽高：

``` cmd
adb shell wm size 2400x1200 #调整当前连接设备宽度
```

返回上一页：

```cmd 
adb shell input keyevent number(4)/KEY(BACK)
```

打开设置页面：

``` cmd
adb shell am start com.android.settings/com.android.settings.Settings
```

获取序列号：

```csharp
 adb get-serialno
```

查看连接计算机的设备：

``` cmd
 adb devices
```

重启机器：

``` cmd
 adb reboot
```

重启到bootloader，即刷机模式：

``` cmd
 adb reboot bootloader
```

重启到recovery，即恢复模式：

``` cmd
 adb reboot recovery
```

查看log：

``` cmd
 adb logcat
```

``` cmd
adb logcat > E:\logcat\log.log	# 把所有的log信息都输出到log文件

adb logcat TAGName:T	# 输出TAG为TAGName的I级别信息

```

终止adb服务进程：

```bash
 adb kill-server
```

重启adb服务进程：

``` cmd
 adb start-server
```

获取机器MAC地址：

```kotlin
 adb shell  cat /sys/class/net/wlan0/address
```

获取CPU序列号：

```undefined
adb shell cat /proc/cpuinfo
```

安装APK：

```cpp
adb install <apkfile> //比如：adb install baidu.apk
```

保留数据和缓存文件，重新安装apk：

```cpp
adb install -r <apkfile> //比如：adb install -r baidu.apk
```

安装apk到sd卡：

```cpp
adb install -s <apkfile> // 比如：adb install -s baidu.apk
```

卸载APK：

```go
adb uninstall <package> //比如：adb uninstall com.baidu.search
```

卸载app但保留数据和缓存文件：

```go
adb uninstall -k <package> //比如：adb uninstall -k com.baidu.search
```

启动应用：

```xml
adb shell am start -n <package_name>/.<activity_class_name>
```

查看设备cpu和内存占用情况：

```undefined
adb shell top
```

查看占用内存前6的app：

```undefined
adb shell top -m 6
```

刷新一次内存信息，然后返回：

```undefined
adb shell top -n 1
```

查询各进程内存使用情况：


```undefined
adb shell procrank
```
杀死一个进程：

```bash
adb shell kill [pid]
```
查看进程列表：

```undefined
adb shell ps
```
查看指定进程状态：

```css
adb shell ps -x [PID]
```
查看后台services信息：

```cpp
adb shell service list
```

查看当前内存占用：

```undefined
adb shell cat /proc/meminfo
```

查看IO内存分区：

```undefined
adb shell cat /proc/iomem
```

将system分区重新挂载为可读写分区：

```undefined
adb remount
```

从本地复制文件到设备：

```xml
adb push <local> <remote>
```

从设备复制文件到本地：

```xml
adb pull <remote>  <local>
```

列出目录下的文件和文件夹，等同于dos中的dir命令：

```undefined
adb shell ls
```

进入文件夹，等同于dos中的cd 命令：

```bash
adb shell cd <folder>
```

重命名文件：

```undefined
adb shell rename path/oldfilename path/newfilename
```

删除system/avi.apk：

```undefined
adb shell rm /system/avi.apk
```

删除文件夹及其下面所有文件：

```xml
adb shell rm -r <folder>
```

移动文件：

```undefined
adb shell mv path/file newpath/file
```

设置文件权限：

```undefined
adb shell chmod 777 /system/fonts/DroidSansFallback.ttf
```

新建文件夹：

```undefined
adb shell mkdir path/foldelname
```

查看文件内容：

```xml
adb shell cat <file>
```

查看wifi密码：

```kotlin
adb shell cat /data/misc/wifi/*.conf
```

清除log缓存：

```swift
adb logcat -c
```

查看bug报告：

```undefined
adb bugreport
```

获取设备名称：

```undefined
adb shell cat /system/build.prop
```

查看ADB帮助：

```bash
adb help
```

跑monkey：

```css
adb shel
```

设置屏幕自动息屏时间：

```cmd
adb shell settings put system screen_off_timeout 10000 # 10秒
```

获取屏幕自动息屏时间：

``` cmake
adb shell settings list system grep timeout
```

