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

查看单个app的内存使用情况：

```undefined
adb shell dumpsys meminfo app的包名
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
adb pull /sdcard/logs/xxx.log  e:\log
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

全局搜索文件：

``` cmake
busybox find / | grep filename
```

查看所有包名：

``` cmake
adb shell pm list packages
```


1. 获取内部版本号： adb shell getprop ro.build.display.innerver
2. 获取按键值： adb shell getevent
3. 获取apk信息： adb shell dumpsys package 包名 ->info.txt
4. 获取应用包名：adb shell dumpsys window windows | grep mFocusedApp  或者 adb shell dumpsys window windows | findstr mFocusedApp
5. 打开WiFi设置界面：adb shell am start -a android.intent.action.MAIN -n com.android.settings/.wifi.WifiSettings
6. 打开热点设置界面：adb shell am start -n com.android.settings/.TetherSettings
7. 查询蓝牙是否开启：
adb shell settings get global bluetooth_on   返回结果0代表关闭，1代表开启
adb shell dumpsys bluetooth_manager | findstr enabled     返回结果是true或者false，说明开启或关闭
8. 查询WiFi是否开启：adb shell settings get global wifi_on     返回结果0代表关闭，1代表开启 
9. 查询蓝牙地址：adb shell settings get secure bluetooth_address
10. 查询WiFi地址：adb shell cat /sys/class/net/wlan0/address
11. 开启WiFi：adb shell svc wifi enable
12. 关闭WiFi：adb shell svc wifi disable
13. 打开蓝牙设置界面：adb shell am start -a android.settings.BLUETOOTH_SETTINGS
14. 打开蓝牙：adb shell svc bluetooth enable
15. 关闭蓝牙：adb shell svc bluetooth disable
16. 强制安装版本号更低的apk：adb install -r -d “C:\xx.apk”
17. 对指定应用进行500次模拟触摸事件：adb shell monkey -p com.yzl.test -v 500
18. 查看蓝牙btsnoop日志setprop persist.bluetooth.btsnoopenable true
setprop persist.bluetooth.btsnoopsavelast true
setprop persist.bluetooth.btsnooppath /data/misc/bluedroid/btsnoop_hci.cfa
setprop persist.bluetooth.btsnooplogmode full
set完后重新开关一下蓝牙，可以看到/data/misc/bluedroid/下多了btsnoop_hci.cfa
19. 获取手机休眠时间：adb shell settings get system screen_off_timeout
20. 更改手机休眠时间：adb shell settings put system screen_off_timeout 600000（10分钟）
21. 获取系统默认输入法：adb shell settings get secure default_input_method
22. 获取手机是否为自动亮度：adb shell settings get system screen_brightness_mode  （0代表非自动，1代表为自动）
23. 设置手机为自动调整亮度：adb shell settings put system screen_brightness_mode 1    
24. 获取手机当前亮度：adb shell settings get system screen_brightness
25. 设置手机亮度（0-255）：adb shell settings put system screen_brightness 350
26. 打开定位设置界面：adb shell am start -a android.settings.LOCATION_SOURCE_SETTINGS
27. 开启定位：adb shell settings put secure location_providers_allowed +gps
28. 关闭定位：adb shell settings put secure location_providers_allowed -gps
29. 查看定位方式：adb shell settings get secure location_providers_allowed  （前提是位置信息开启）
30. 拨打电话：adb shell am start -a android.intent.action.CALL tel:8888888888888
31. 发送短信：adb shell am start -a android.intent.action.SENDTO -d sms:10086（发送目的号码） --es sms_body "hello"（短信内容） --ez exit_on_sent true 
32. 获取应用包名：adb shell dumpsys window windows | findstr  mFocusedApp 
33. 清除应用数据与缓存: adb shell pm clear cn.com.test.mobile
34. 启动应用: adb shell am start -n cn.com.test.mobile/.ui.SplashActivity 
35. 停止应用：adb shell am force-stop cn.com.test.mobile
36. 飞行模式：adb shell settings set global airplane_mode_on   (0==关闭，1==开启)
37. 开启飞行模式：adb shell settings put global airplane_mode_on 1
38. 手机震动测试（前提手机root）：①adb shell ②echo '3000'>/sys/devices/virtual/timed_output/vibrator/enable
39. 向上滑：adb shell input touchscreen swipe 930 880 930 380 
40. 向下滑：adb shell input touchscreen swipe 930 380 930 880
41. 向右滑：adb shell input touchscreen swipe 330 880 930 880 
42. 向左滑：adb shell input touchscreen swipe 930 880 330 880
43. 模拟鼠标点击操作：adb shell input mouse tap 100 500
44. 长按：adb shell input swipe startX startY startX startY 500
45. 滑动解锁：adb shell input swipe 300 1000 300 500
46. 冷启动app：adb shell am start -W -n package/activity
47. 热启动：①停止app： adb shell input keyevent 3  ②adb shell am start -W -n package/activity
48. 查看内存占用情况：adb -s 设备号 shell top -m 进程数量 -n 数据的刷新次数 -s 按哪列进行排序 -d 刷新时间间隔（默认5秒）
49. 切换手机电池为非充电状态： adb shell dumpsys battery set status 1
50. 改变手机电量： adb shell dumpsys battery set level 58
51. 获取当前电量：adb shell cat /sys/class/power_supply/battery/capacity
52. 手机截屏：adb shell /system/bin/screencap -p /sdcard/screenshot.png
53. 录制屏幕：adb shell screenrecord --time-limit 10 /sdcard/demo.mp4
54. 获取手机型号：adb shell getprop ro.product.model
55. 获取电池信息：adb shell dumpsys battery  
56. 获取屏幕分辨率：adb shell wm size
57. 获取屏幕密度：adb shell wm density
58. 显示屏参数：adb shell dumpsys window displays
59. 获取手机IP地址：adb shell ifconfig | findstr Mask
60. 查看WiFi局域网地址：adb shell ifconfig wlan0
61. 显示区域位置：adb shell wm overscan 0,0,0,200  （四个数字分别表示距离左、上、右、下边缘的留白像素，以上命令表示将屏幕底部 200px 留白）
62. 恢复原显示区域命令：adb shell wm overscan reset
63. 获取USB调试模式：adb shell settings get global adb_enabled
64. 关闭USB调试模式：adb shell settings put global adb_enabled 0
65. 状态栏和导航栏的显示隐藏：
adb shell settings put global policy_control <key-values>
<key-values> 可由如下几种键及其对应的值组成，格式为 <key1>=<value1>:<key2>=<value2>。
  immersive.full----------同时隐藏
  immersive.status----------隐藏状态栏
  immersive.navigation----------隐藏导航栏
  immersive.preconfirms----------?
这些键对应的值可则如下值用逗号组合：
  apps----------所有应用
  *----------所有界面
  packagename----------指定应用
 -packagename----------排除指定应用
例如：
adb shell settings put global policy_control immersive.full=*
表示设置在所有界面下都同时隐藏状态栏和导航栏。
adb shell settings put global policy_control immersive.status=com.package1,com.package2:immersive.navigation=apps,-com.package3
表示设置在包名为 com.package1 和 com.package2 的应用里隐藏状态栏，在除了包名为 com.package3 的所有应用里隐藏导航栏。
61. 打开网页： adb shell am start -a android.intent.action.VIEW -d http://www.baidu.com
62. 查看通信日志 ：adb logcat -b radio (常用于查看详细的通话状态)
63. 获取界面控件：adb uiautomator dump
64. 列出输入法：adb shell ime list -s 
65. 永不休眠：adb shell settings put system screen_off_timeout 2147483647
66. 关闭\打开自动旋转：adb shell settings put system accelerometer_rotation 0\1


