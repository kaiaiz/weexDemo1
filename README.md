该项目必须有安卓开发环境
该项目 引入了 WeeX-UI的(导航、Tab切换导航)  相机拍照、打开相册的 功能

安卓环境搭建：http://www.androiddevtools.cn/ ` 安卓SDK中文网站`
```
1、下载Android Studio 选择"3.0.1正式版"的 android-studio-ide-171.4443003-windows32.zip
   下载完 解压到 D:\Android\AndroidStudio
   
2、下载SDK Tools 选择"24.41版"的 android-sdk_r24.4.1-windows.zip。
   下载完 解压到 D:\Android\sdk

3、运行 D:\Android\sdk 下的 SDK Manager.exe
   勾选 Tools下的AndroidSDK Build-tools 23.0.1 和23.0.2版本
   勾选 Android6.0(API23) 下的 Documentation for Android SDK、SDK Platform、Sources for Android SDK
   
4、配置环境变量
   变量名：ANDROID_HOME
   变量值： D:\Android\sdk
   修改path变量，在最后加入;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools
   
5、验证配置
   打开命令行窗口，输入adb，出来
   Android Debug Bridge version 1.0.39
   Version 27.0.0-4455170
   Installed as D:\andriod\Sdk\platform-tools\adb.exe
   表示配置正确，--- WeeX依赖的安卓环境 配置完毕
```

使用步骤：

安装Weektools: 
> npm install -g weex-toolkit   或   cnpm install -g weex-toolkit

检测安装是否成功：
> weex -v

出来如下提示，表示安装正确
  - v1.1.0-beta.7
  - weexpack : v0.4.7-beta.26
  - weex-builder : v0.2.13-beta.6
  - weex-previewer : v1.3.13-beta.13 

安装依赖：
> npm install 

添加安卓工程 
> weex platform add android

>配置照相机的功能

前往：https://github.com/voids/weex-image-crop-picker

###打包安卓APP
将手机与电脑连接,输入如下命令--

确保手机上开发者选项打开，USB调试打开
>weexpack run android 

