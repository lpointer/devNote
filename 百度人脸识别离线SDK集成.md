

### 1.添加依赖

* 把人脸识别sdk包复制到项目

* 添加依赖包

  记得先不要点击 `Sync Now`

  1.打开 `settings.gradle` 文件，添加`:facelibrary`

  ```java
  include ':app',':library',':facelibrary'
  ```

  2.打开项目的 `app -> build.gradle` 文件，引入 `facelibrary` 包

  ```java
  compile project(':facelibrary')
  ```

  3.在`app -> build.gradle` 继续修改 `minSdkVersion` 版本，并且添加`ndk` ，修改 `compileSdkVersion` 为 26 。

  ```java
  android {
    compileSdkVersion 26
    defaultConfig {
      ...
    	minSdkVersion 21
      multiDexEnabled true
      ndk {
       moduleName "facesdk"
         ldLibs "log"
       abiFilters "armeabi-v7a" // "armeabi", "x86", "arm64-v8a"
      }
    }
    ...
  }
  ```

  * **如果该版本低于21的，则需要这样引入**

    ``` java
    android {
        defaultConfig {
            ...
            minSdkVersion 15 
            targetSdkVersion 25
            multiDexEnabled true
        }
        ...
    }
    
    dependencies {
      compile 'com.android.support:multidex:1.0.3'
    }
    ```

    

  * 如果不添加 `ndk` 在初始化人脸特征时候会失败

  **PS**

  > **添加 `multiDexEnabled true` 这个主要是因为防止添加了很多第三方库，会出现方法超多的问题，导致出现这个报错 <font color=red>Process 'command 'X:\xxx\bin\java.exe'' finished with non-zero exit value 2</font> 问题。**

  

  4. 打开 `facelibrary` 依赖包的 `facelibrary\src\main\AndroidManifest.xml` 。

     去掉 <font color=green>android:allowBackup="false"</font>

  5. 添加一下内容到 `app -> AndroidManifest.xml` 

     ``` xml
      <!-- 安全设备指纹接入 start -->
      	<activity
              android:name="com.baidu.liantian.LiantianActivity"
              android:excludeFromRecents="true"
              android:exported="true"
              android:launchMode="standard"
              android:theme="@android:style/Theme.Translucent">
              <intent-filter>
                  <action android:name="com.baidu.action.Liantian.VIEW" />
                 <category android:name="com.baidu.category.liantian" />
                  <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
          </activity>
     	<receiver
            android:name="com.baidu.liantian.LiantianReceiver"
            android:exported="false">
           <intent-filter>
              <action android:name="com.baidu.action.Liantian.VIEW" />
     		<category android:name="com.baidu.category.liantian" />
              <category android:name="android.intent.category.DEFAULT" />
           </intent-filter>
           <intent-filter android:priority="2147483647">
              <action android:name="android.intent.action.BOOT_COMPLETED" />
           </intent-filter>
          </receiver>
     	 <provider
              android:name="com.baidu.liantian.LiantianProvider"
              android:authorities="com.baidu.idl.face.demo.liantian.ac.provider"
              android:exported="false" />
     		 <service
                  android:name="com.baidu.liantian.LiantianService"
                  android:exported="false">
                    <intent-filter>
                       <action android:name="com.baidu.action.Liantian.VIEW" />
     				<category android:name="com.baidu.category.liantian" />
                       <category android:name="android.intent.category.DEFAULT" />
                    </intent-filter>
               </service>
     	<meta-data
              android:name="seckey_avscan"
              android:value="660346260f8a841a04ec2a56815b421b" />
                 <meta-data
                     android:name="appkey_avscan"
                     android:value="100034" />
     ```

  6. 修改开发工具 `android studo` 的环境， `File -> Project Structure` 

  7. 修改项目 `app` 的 `build.gradle` ，如下图

     `dependencies`级别下面的添加 `implementation project(':facelibrary')`

   9.最后点击 `Sync Now

  10. 根据报错的提示，在 `app -> build.gradle` 添加对应的配置，如下图红框所示。

完。
