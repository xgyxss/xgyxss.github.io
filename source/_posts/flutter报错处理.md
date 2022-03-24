---
title: flutter报错处理
date: 2022-03-19 20:00:00
tags: [flutter, 报错处理]
categories: 解决方案
---

- <a href="#target1">The relevant error-causing widget was Swiper</a>
- <a href="#target2">Your project requires a newer version of the Kotlin Gradle plugin</a>
- <a href="#target3">Error: Expected named argument</a>
- <a href="#target4">exception caught by widgets library</a>
- <a href="#target5">LateInitializationError: Field 'data' has not been initialized, got error</a>
- <a href="#target6">ohmyzsh更新报错；flutter升级更新报错</a>

- <a href="#target7">HTTP Host Availability</a>

- <a href="#target8">Warning: The plugin *** requires Android SDK version 31</a>

<!-- more -->

### <a name="target1">The relevant error-causing widget was Swiper</a>

flutter_swiper_plus: ^2.0.4

直接引入报错：

```dart
Swiper(
  itemBuilder: (BuildContext context,int index){
    return new Image.network("http://via.placeholder.com/350x150",fit: BoxFit.fill,);
  },
  itemCount: 3,
  pagination: new SwiperPagination(),
  control: new SwiperControl(),
),
```

```bash
════════ Exception caught by rendering library ═════════════════════════════════
RenderBox was not laid out: RenderViewport#3e1ad NEEDS-PAINT
'package:flutter/src/rendering/box.dart':
package:flutter/…/rendering/box.dart:1
Failed assertion: line 1927 pos 12: 'hasSize'

The relevant error-causing widget was
Swiper
lib/home/home.dart:70
```

改进：

```dart
Container(
  height: 200,
  padding: EdgeInsets.all(10.0),
  child: Swiper(
    itemBuilder: (BuildContext context,int index){
      var images = <String> [
        // "http://www.quanjing.com/image/2018image/homepage/1.jpg?v=8",
        "https://via.placeholder.com/288x188",
        "https://via.placeholder.com/200x100",
        "https://via.placeholder.com/200x150",
      ];
      return new Image.network(
        images[index % images.length],
        fit: BoxFit.fill,
      );
    },
    autoplay: true,
    itemCount: 3,
    pagination: new SwiperPagination(),
    control: new SwiperControl(),
  ),
),
```

### <a name="target2">Your project requires a newer version of the Kotlin Gradle plugin</a>

```bash
Launching lib/main.dart on Android SDK built for x86 in debug mode...
lib/main.dart:1
e: Incompatible classes were found in dependencies. Remove them from the classpath or use '-Xskip-metadata-version-check' to suppress errors
e: /Users/guanguan/.gradle/caches/transforms-2/files-2.1/0464082e81de712709b8918eac577657/jetified-kotlin-stdlib-jdk7-1.6.10.jar!/META-INF/kotlin-stdlib-jdk7.kotlin_module: Module was compiled with an incompatible version of Kotlin. The binary version of its metadata is 1.6.0, expected version is 1.1.15.

...(一系列和上面一样的报错)

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':fluttertoast:compileDebugKotlin'.
> Compilation error. See log for more details

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 33s
[!] Your project requires a newer version of the Kotlin Gradle plugin.
    Find the latest version on https://kotlinlang.org/docs/gradle.html#plugin-and-versions, then update /Users/guanguan/Downloads/Github/app/android/build.gradle:
    ext.kotlin_version = '<latest-version>'
Exception: Gradle task assembleDebug failed with exit code 1
Exited (sigterm)
```

将 android - build.gradle 文件中的 ext.kotlin_version 改为最新的版本即可。附上Kotlin 最新的[版本地址](https://kotlinlang.org/docs/gradle.html#plugin-and-versions)。

1.3.50 -> 1.6.10

### <a name="target3">Error: Expected named argument</a>

```bash
: Error: Expected named argument.
lib/mine/userinfo.dart:162
                  _sample == null ? _buildOpeningImage() : _buildCroppingImage(),
                                  ^
: Error: No named parameter with the name '#1'.
lib/mine/userinfo.dart:153
                title: Container(
                                ^^...
: Context: Found this candidate, but the arguments don't match.
../…/widgets/container.dart:253
  Container({

  ^^^^^^^^^
Restarted application in 804ms.
```

在Container 组件下，将`child:`添加在`_sample == null ? _buildOpeningImage() : _buildCroppingImage(),`这句的前面即可。

### <a name="target4">exception caught by widgets library</a>

```bash
════════ Exception caught by image resource service ════════════════════════════
The following HttpException was thrown resolving an image codec:
Connection closed while receiving data, uri = http://www.bobdy.com/pic/app/2021/12/163982066976162464.jpg
...
```

错误原因：

服务器的图片未成功加载。后端解决了。

### <a name="target5">LateInitializationError: Field 'data' has not been initialized, got error。</a>

Cause of Error:

在初始化之前使用后期变量时会发生此错误。必须记住一件事，已经使用了一些声明为`late`的数据或变量，但它们的值在使用之前没有更改或存储。

```dart
//For example:
late String name;
@override
Widget build(BuildContext context) {
  return Scaffold(
        body: Text(name)
        //runtime error: 
        //LateInitializationError: Field 'name' has not been initialized.
  );
} 
//How to solved?
late String name; -> String? name;
//请记住：在使用之前，必须在后期变量分配一些东西。
```

**How to solve such problems?**

> just change
>
> ```dart
> late Mydata data;
> ```
>
> to
>
> ```dart
> Mydata? data;
> ```

### <a name="target6">ohmyzsh更新报错；flutter升级更新报错。</a>

ohmyzsh不能更新，报错：

```bash
fatal: unable to access 'https://github.com/ohmyzsh/ohmyzsh.git/': Failed to connect to github.com port 443: Operation timed out
```

另外一个报错就是flutter升级更新：

```bash
ProcessException: Process exited abnormally:
fatal: 无法访问 'https://github.com/flutter/flutter.git/'：LibreSSL SSL_read: error:02FFF03C:system
library:func(4095):Operation timed out, errno 60
  Command: git fetch --tags
```

还有然后修改了一下host文件：

```bash
sudo vi /etc/hosts
```

虽然还能ping通github的地址，但报错443，请求超时，代理的问题。于是，将其中所有的github的dns都注释/删掉：

```markdown
#140.82.113.4                   github.com
#199.232.69.194                 github.global.ssl.fastly.net
#185.199.108.153                assets-cdn.github.com
#185.199.109.153                assets-cdn.github.com
#185.199.110.153                assets-cdn.github.com
#185.199.111.153                assets-cdn.github.com
```

OK，然后科学上网，升级，flutter从2.8.1升到了2.10.3，本以为到此就结束了。然后后续又出现了下列问题：

### <a name="target7">HTTP Host Availability</a>

```bash
#flutter doctor -v
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 2.10.3, on macOS 12.3 21E230 darwin-x64, locale zh-Hans-CN)
[✓] Android toolchain - develop for Android devices (Android SDK version 29.0.2)
[✓] Xcode - develop for iOS and macOS (Xcode 13.3)
[✓] Chrome - develop for the web
[✓] Android Studio (version 4.1)
[✓] IntelliJ IDEA Ultimate Edition (version 2021.1.1)
[✓] VS Code (version 1.65.2)
[✓] Connected device (2 available)
[!] HTTP Host Availability
    ✗ HTTP host https://maven.google.com/ is not reachable. Reason: An error occurred while checking the HTTP host: Operation timed out
```

github上也找到了同样的问题，分别是[Windows版本](https://github.com/flutter/flutter/issues/98170)和[Mac版本](https://github.com/flutter/flutter/issues/98239)，科学上网也仍然ping不通maven.google.com：

```bash
ping maven.google.com
PING www3.l.google.com (142.251.42.238): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3
Request timeout for icmp_seq 4
Request timeout for icmp_seq 5
Request timeout for icmp_seq 6
Request timeout for icmp_seq 7
^C
--- www3.l.google.com ping statistics ---
9 packets transmitted, 0 packets received, 100.0% packet loss
```

然后顺着网址访问了www3.l.google.com：

```markdown
您的连接不是私密连接
攻击者可能会试图从 www3.l.google.com 窃取您的信息（例如：密码、通讯内容或信用卡信息）。了解详情
NET::ERR_CERT_COMMON_NAME_INVALID

www3.l.google.com 通常会使用加密技术来保护您的信息。Chrome 此次尝试连接到 www3.l.google.com 时，该网站发回了异常的错误凭据。这可能是因为有攻击者在试图冒充 www3.l.google.com，或者 Wi-Fi 登录屏幕中断了此次连接。请放心，您的信息仍然是安全的，因为 Chrome 尚未进行任何数据交换便停止了连接。

您目前无法访问 www3.l.google.com，因为此网站使用了 HSTS。网络错误和攻击通常是暂时的，因此，此网页稍后可能会恢复正常。
```

访问maven.google.com/web/index：

```markdown
404. That’s an error.

The requested URL /web/index was not found on this server. That’s all we know.
```

[这里](https://github.com/android/architecture-components-samples/issues/4)也有关于maven.google.com 404的问题。

> 知识拓展：ping不通，可能是因为ICMP协议被限制了。ICMP是（Internet Control Message Protocol）Internet控制报文协议。它是TCP/IP协议族的一个子协议，用于在IP主机、路由器之间传递控制消息。控制消息是指网络通不通、主机是否可达、路由是否可用等网络本身的消息。这些控制消息虽然并不传输用户数据，但是对于用户数据的传递起着重要的作用。

悬而未决～

后续：

找到[这篇文章](https://github.com/flutter/flutter/issues/98170)，文末，笔者**[christopherfujino](https://github.com/christopherfujino)**在昨天（2022-03-22）回复到：

> I am locking this issue as it has been fixed in [#98293](https://github.com/flutter/flutter/pull/98293), which is currently in the beta release (and will be in the next stable).
>
> Even if you are hitting this issue on stable, it is safe to ignore it.

意思是可以忽略它。

### <a name="target8">Warning: The plugin *** requires Android SDK version 31.</a>

在更新完后，运行flutter项目，报错：

```bash
Running "flutter pub get" in app...
Launching lib/main.dart on Android SDK built for x86 in debug mode...
lib/main.dart:1
Warning: The plugin flutter_plugin_android_lifecycle requires Android SDK version 31.
Warning: The plugin image_picker requires Android SDK version 31.
Warning: The plugin path_provider_android requires Android SDK version 31.
Warning: The plugin video_player_android requires Android SDK version 31.
One or more plugins require a higher Android SDK version.
Fix this issue by adding the following to /Users/guanguan/Downloads/Github/app/android/app/build.gradle:
android {
  compileSdkVersion 31
  ...
}


FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:checkDebugAarMetadata'.
> Multiple task action failures occurred:
   > A failure occurred while executing com.android.build.gradle.internal.tasks.CheckAarMetadataWorkAction
      > The minCompileSdk (31) specified in a
        dependency's AAR metadata (META-INF/com/android/build/gradle/aar-metadata.properties)
        is greater than this module's compileSdkVersion (android-30).
        Dependency: androidx.window:window-java:1.0.0-beta04.
        AAR metadata file: /Users/guanguan/.gradle/caches/transforms-2/files-2.1/ad201fac15a88598107ec645f351f5b4/jetified-window-java-1.0.0-beta04/META-INF/com/android/build/gradle/aar-metadata.properties.
   > A failure occurred while executing com.android.build.gradle.internal.tasks.CheckAarMetadataWorkAction
      > The minCompileSdk (31) specified in a
        dependency's AAR metadata (META-INF/com/android/build/gradle/aar-metadata.properties)
        is greater than this module's compileSdkVersion (android-30).
        Dependency: androidx.window:window:1.0.0-beta04.
        AAR metadata file: /Users/guanguan/.gradle/caches/transforms-2/files-2.1/03c633e46d75bfb21f082f0417f55161/jetified-window-1.0.0-beta04/META-INF/com/android/build/gradle/aar-metadata.properties.

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 1m 14s
Exception: Gradle task assembleDebug failed with exit code 1
Exited (sigterm)
```

可以发现，有四个插件要求Android SDK version 31，根据提示修改文件，项目/android/app/build.gradle，将compileSdkVersion 从30改为31即可。重新编译，有三个警告，但正常运行。

```bash
注: /Users/guanguan/Applications/flutter/.pub-cache/hosted/pub.dartlang.org/device_info-2.0.3/android/src/main/java/io/flutter/plugins/deviceinfo/DeviceInfoPlugin.java使用了未经检查或不安全的操作。
注: 有关详细信息, 请使用 -Xlint:unchecked 重新编译。
注: /Users/guanguan/Applications/flutter/.pub-cache/hosted/pub.dartlang.org/image_crop-0.4.0/android/src/main/java/com/lykhonis/imagecrop/ImageCropPlugin.java使用或覆盖了已过时的 API。
注: 有关详细信息, 请使用 -Xlint:deprecation 重新编译。
注: /Users/guanguan/Applications/flutter/.pub-cache/hosted/pub.dartlang.org/path_provider_android-2.0.12/android/src/main/java/io/flutter/plugins/pathprovider/PathProviderPlugin.java使用了未经检查或不安全的操作。
注: 有关详细信息, 请使用 -Xlint:unchecked 重新编译。
```



<div style="color:skyblue;font-weight:bold;text-align:center;margin-top:5rem;margin-bottom:5rem;">————————TBC————————</div>

