# Cocos打包安卓

## Cocos

### 安卓环境配置

详情见 [Android 原生开发环境配置](https://docs.cocos.com/creator/3.8/manual/zh/editor/publish/android/build-setup-evn-android.html)

主要需要配置两个参数

1. SDK路径
2. NDK路径

> SDK路径只到SDK根目录，NDK路径需要具体到对应版本的NDK

### Java 与 Javascript 代码交互

参考官方文档 [使用 JsbBridge 实现 JavaScript 与 Java 通信](https://docs.cocos.com/creator/3.8/manual/zh/advanced-topics/js-java-bridge.html)

> 部分交互需要线程安全，如调用原生 Toast ， 参考 [线程安全](https://docs.cocos.com/creator/3.8/manual/zh/advanced-topics/thread-safety.html) 构建代码

### 遇到的问题

#### 游戏加载报错

确认构建的入口场景是否为正确的游戏入口

#### 编译 Debug 版本报错

建议使用最后一版 23 版本的 NDK（已测试无编译报错）

#### 屏幕朝向问题

* 修改构建脚本的屏幕方向（未测试）

* 修改构建的安卓项目中的 mainfests/AndroidMainfests.xml 中的 `android:screenOrientation="屏幕朝向"` （测试有效）

## Android

### 遇到的问题

#### 无法 Debug

修改编译的目标版本，通过以下操作实现：

菜单栏 Build -> Select Build Variant ，然后选择对应的版本即可


