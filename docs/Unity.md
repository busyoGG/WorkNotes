# Unity 打包

## SDK

### [AdMob](https://developers.google.com/admob/unity/quick-start?hl=zh-cn#android)

#### 引入

1. 使用 npm 安装 [openupm-cli](https://github.com/openupm/openupm-cli?tab=readme-ov-file#windows-platform-troubleshooting)

    `npm install -g openupm-cli`

2. 使用 openupm-cli 安装 Unity 的 AdMob SDK

    1. 进入 Unity 项目根目录
    2. 打开 cmd 或者 powershell
    3. 使用 `openupm add com.google.ads.mobile` 命令集成 SDK
    4. 设置依赖项

        转到项目设置 >播放器 >Android >发布设置 >构建 然后选择：

        * 自定义主 Gradle 模板
        * 自定义 Gradle 属性模板

            ![](https://developers.google.com/static/admob/images/unity_projectsettings_gradle.png?hl=zh-cn)

    5.执行Assets >External Dependency Manager >Android Resolver >Resolve
        
    6.设置 AdMob 应用 ID

        ![](https://developers.google.com/static/admob/images/unity_gma_inspector_menu.png?hl=zh-cn)

#### 配置

访问 `Assets/Resources/Configs/SO/AdMobAdID` 来修改广告配置
