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

~~建议使用最后一版 23 版本的 NDK（已测试无编译报错）~~

编译报错原因为内存不足

#### 屏幕朝向问题

* 修改构建脚本的屏幕方向（未测试）

* 修改构建的安卓项目中的 mainfests/AndroidMainfests.xml 中的 `android:screenOrientation="屏幕朝向"` （测试有效）

#### 无法调用广告

检查项目中是否有运行环境控制，例如测试环境，该环境下可能不调起广告

## Android

### 接入 SDK

#### ADMob

> 广告的展示需要在主线程执行，因此需要以 `runOnUiThread` 执行调用。

官方文档见 [
Mobile Ads SDK (Android)](https://developers.google.com/admob/android/quick-start?hl=zh-cn#import_the_mobile_ads_sdk)

##### Gradle 版本

集成 ADMob 需要较高的 Gradle 版本才能编译，可以通过 File -> Project Structure -> Project 修改（目前使用 8.4.2 版本， Gradle 版本为 8.6）

##### Compile SDK 版本

需要33版本以上，可以通过 File -> Project Structure -> Module -> 具体的项目模块 修改

#### Adjust

官方文档见 [Adjust](https://dev.adjust.com/zh/sdk/android?version=v4)

### 遇到的问题

#### 无法 Debug

修改编译的目标版本，通过以下操作实现：

菜单栏 Build -> Select Build Variant ，然后选择对应的版本即可

#### 无法嵌入广告的 View

参考 [cocos-google-admob](https://github.com/cocos/cocos-google-admob/blob/581874a39503d57d735a294784ccee3d405e12e7/extensions/GoogleAdMob/template/android/libadmob/src/com/cocos/admob/service/BannerService.java#L44)

不能使用 `setContentView` 来创建界面，会导致游戏无法运行。

而是使用以下方法创建 Banner 广告的 View 容器

``` Java
 //创建Banner容器
_adContainerView = new RelativeLayout(context);
Window w = context.getWindow();
ViewGroup vg = (ViewGroup) w.getDecorView();
RelativeLayout rl = new RelativeLayout(context);
RelativeLayout.LayoutParams lp = new RelativeLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT,
ViewGroup.LayoutParams.WRAP_CONTENT);
lp.addRule(RelativeLayout.ALIGN_TOP);
lp.addRule(RelativeLayout.CENTER_HORIZONTAL);
_adContainerView.setLayoutParams(lp);
vg.addView(rl);
```


