
## Gradle下载慢的问题
修改 gradle-wrapper.properties 文件
在项目根目录中找到：gradle/wrapper/gradle-wrapper.properties，替换 distributionUrl 为阿里云或腾讯云的镜像地址：

```properties
### 阿里云镜像（通用性强）
distributionUrl=https\://mirrors.aliyun.com/gradle/distributions/gradle-8.6-bin.zip
### 腾讯云镜像（速度稳定）
distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-8.6-bin.zip
```
>注意：8.6 需替换为你项目实际需要的 Gradle 版本号。阿里云和腾讯云都支持绝大多数常用版本，若你用的版本较新但镜像站未收录，可尝试稍降版本1710。

>注意：稍高版本的gradle，路径在这个：gradle/distributions/

Gradle的下载慢的问题大多能通过这个解决

## Maven仓库下载慢的问题

```groovy
pluginManagement {
    repositories {
        google {
            content {
                includeGroupByRegex("com\\.android.*")
                includeGroupByRegex("com\\.google.*")
                includeGroupByRegex("androidx.*")
            }
        }
        // 国内镜像优先
        maven {
            name "AliyunGradlePlugin"
            url "https://maven.aliyun.com/repository/gradle-plugin"
        }
        mavenCentral()
        gradlePluginPortal()
    }
}
```
这google部分代码，加了之后，可以避免repo.maven.apache.org从这个地址下载，这个地址下载很慢，第一次同步项目很慢很慢。待后续继续评估。

## SDK下载快

可能跟这个有关系

```http proxy
https://mirrors.cloud.tencent.com/AndroidSDK/
```

## VPN

使用openvpn，可以在Android Studio完成验证登录Google账号和Gemini，用pac则不行

后续还可以尝试自己设置本地代理，看看能不能加速一下代码依赖下载
