---
title: flutter报错处理-四
date: 2022-05-19 17:31:19
tags: [flutter, 报错处理, 202205]
categories: 解决方案
---

将 flutter 2.10.5 升级到 3.0.0 ，之后 [根据提示](https://guides.cocoapods.org/using/getting-started.html#installation) 升级 CocoaPods，省流提示命令：`sudo gem install cocoapods`。

意外地解决了之前的遗留问题：<a href="#target1">HTTP Host Availability</a>，又出现了新的官方问题：

- <a href="#target2">Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.</a>

详细如下...

<!-- more -->

### <a name="target7">HTTP Host Availability</a>

升级前：

```bash
flutter doctor -v
[✓] Flutter (Channel stable, 2.10.5, on macOS 12.4 21F79 darwin-x64, locale zh-Hans-CN)
    • Flutter version 2.10.5 at /Users/guanguan/Applications/flutter
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision 5464c5bac7 (4 周前), 2022-04-18 09:55:37 -0700
    • Engine revision 57d3bac3dd
    • Dart version 2.16.2
    • DevTools version 2.9.2
    • Pub download mirror https://pub.flutter-io.cn
    • Flutter download mirror https://storage.flutter-io.cn

[✓] Android toolchain - develop for Android devices (Android SDK version 29.0.2)
    • Android SDK at /Users/guanguan/Library/Android/sdk
    • Platform android-31, build-tools 29.0.2
    • Java binary at: /Applications/Android Studio.app/Contents/jre/Contents/Home/bin/java
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)
    • All Android licenses accepted.

[✓] Xcode - develop for iOS and macOS (Xcode 13.4)
    • Xcode at /Applications/Xcode.app/Contents/Developer
    • CocoaPods version 1.10.1

[✓] Chrome - develop for the web
    • Chrome at /Applications/Google Chrome.app/Contents/MacOS/Google Chrome

[✓] Android Studio (version 2021.2)
    • Android Studio at /Applications/Android Studio.app/Contents
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)

[✓] IntelliJ IDEA Ultimate Edition (version 2021.1.1)
    • IntelliJ at /Applications/IntelliJ IDEA.app
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart

[✓] VS Code (version 1.67.1)
    • VS Code at /Applications/Visual Studio Code.app/Contents
    • Flutter extension version 3.40.0

[✓] Connected device (2 available)
    • Android SDK built for x86 (mobile) • emulator-5554 • android-x86    • Android 8.0.0 (API 26) (emulator)
    • Chrome (web)                       • chrome        • web-javascript • Google Chrome 101.0.4951.64

[!] HTTP Host Availability
    ✗ HTTP host https://maven.google.com/ is not reachable. Reason: An error occurred while checking the HTTP host: Operation
      timed out

! Doctor found issues in 1 category.
```

升级后：

```bash
Upgrading Flutter to 3.0.0 from 2.10.5 in /Users/guanguan/Applications/flutter...
Downloading Darwin x64 Dart SDK from Flutter engine d1b9a6938ad77326ac3a94d92bbc77933ed829ed...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed

  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0  205M    0 1497k    0     0  1186k      0  0:02:57  0:00:01  0:02:56 1196k
  2  205M    2 4296k    0     0  1898k      0  0:01:51  0:00:02  0:01:49 1906k
  3  205M    3 7370k    0     0  2262k      0  0:01:33  0:00:03  0:01:30 2269k
  4  205M    4  9.8M    0     0  2364k      0  0:01:29  0:00:04  0:01:25 2370k
  6  205M    6 12.4M    0     0  2436k      0  0:01:26  0:00:05  0:01:21 2558k
  7  205M    7 15.2M    0     0  2489k      0  0:01:24  0:00:06  0:01:18 2818k
  8  205M    8 17.8M    0     0  2524k      0  0:01:23  0:00:07  0:01:16 2809k
  9  205M    9 20.2M    0     0  2516k      0  0:01:23  0:00:08  0:01:15 2681k
 10  205M   10 22.5M    0     0  2494k      0  0:01:24  0:00:09  0:01:15 2605k
 12  205M   12 24.8M    0     0  2481k      0  0:01:24  0:00:10  0:01:14 2529k
 13  205M   13 27.0M    0     0  2463k      0  0:01:25  0:00:11  0:01:14 2430k
 14  205M   14 29.8M    0     0  2496k      0  0:01:24  0:00:12  0:01:12 2455k
 15  205M   15 32.1M    0     0  2484k      0  0:01:24  0:00:13  0:01:11 2430k
 16  205M   16 34.3M    0     0  2469k      0  0:01:25  0:00:14  0:01:11 2421k
 17  205M   17 36.7M    0     0  2470k      0  0:01:25  0:00:15  0:01:10 2446k
 18  205M   18 38.2M    0     0  2412k      0  0:01:27  0:00:16  0:01:11 2299k
 20  205M   20 41.1M    0     0  2446k      0  0:01:26  0:00:17  0:01:09 2323k
 21  205M   21 43.7M    0     0  2456k      0  0:01:25  0:00:18  0:01:07 2381k
 22  205M   22 46.6M    0     0  2483k      0  0:01:24  0:00:19  0:01:05 2525k
 23  205M   23 49.4M    0     0  2498k      0  0:01:24  0:00:20  0:01:04 2583k
 25  205M   25 52.2M    0     0  2512k      0  0:01:23  0:00:21  0:01:02 2834k
 26  205M   26 54.5M    0     0  2510k      0  0:01:23  0:00:22  0:01:01 2730k
 27  205M   27 57.3M    0     0  2524k      0  0:01:23  0:00:23  0:01:00 2775k
 28  205M   28 59.7M    0     0  2521k      0  0:01:23  0:00:24  0:00:59 2665k
 30  205M   30 62.1M    0     0  2518k      0  0:01:23  0:00:25  0:00:58 2600k
 31  205M   31 65.5M    0     0  2557k      0  0:01:22  0:00:26  0:00:56 2749k
 33  205M   33 68.1M    0     0  2561k      0  0:01:22  0:00:27  0:00:55 2789k
 34  205M   34 70.6M    0     0  2560k      0  0:01:22  0:00:28  0:00:54 2725k
 35  205M   35 73.2M    0     0  2566k      0  0:01:22  0:00:29  0:00:53 2784k
 36  205M   36 75.2M    0     0  2516k      0  0:01:23  0:00:30  0:00:53 2507k
 36  205M   36 75.8M    0     0  2486k      0  0:01:24  0:00:31  0:00:53 2113k
 37  205M   37 77.2M    0     0  2452k      0  0:01:25  0:00:32  0:00:53 1857k
 38  205M   38 79.8M    0     0  2458k      0  0:01:25  0:00:33  0:00:52 1886k
 40  205M   40 82.4M    0     0  2464k      0  0:01:25  0:00:34  0:00:51 1869k
 41  205M   41 84.7M    0     0  2450k      0  0:01:26  0:00:35  0:00:51 2030k
 42  205M   42 87.6M    0     0  2475k      0  0:01:25  0:00:36  0:00:49 2407k
 43  205M   43 90.3M    0     0  2483k      0  0:01:24  0:00:37  0:00:47 2682k
 45  205M   45 93.5M    0     0  2504k      0  0:01:24  0:00:38  0:00:46 2809k
 46  205M   46 96.1M    0     0  2507k      0  0:01:24  0:00:39  0:00:45 2804k
 48  205M   48 99.1M    0     0  2522k      0  0:01:23  0:00:40  0:00:43 3043k
 49  205M   49  101M    0     0  2527k      0  0:01:23  0:00:41  0:00:42 2908k
 50  205M   50  104M    0     0  2539k      0  0:01:23  0:00:42  0:00:41 2958k
 52  205M   52  107M    0     0  2541k      0  0:01:22  0:00:43  0:00:39 2825k
 53  205M   53  110M    0     0  2545k      0  0:01:22  0:00:44  0:00:38 2845k
 54  205M   54  113M    0     0  2556k      0  0:01:22  0:00:45  0:00:37 2829k
 56  205M   56  115M    0     0  2566k      0  0:01:22  0:00:46  0:00:36 2883k
 57  205M   57  118M    0     0  2567k      0  0:01:22  0:00:47  0:00:35 2800k
 58  205M   58  121M    0     0  2577k      0  0:01:21  0:00:48  0:00:33 2888k
 60  205M   60  124M    0     0  2585k      0  0:01:21  0:00:49  0:00:32 2939k
  61  205M   61  126M    0     0  2582k      0  0:01:21  0:00:50  0:00:31 2823k
             62  205M   62  128M    0     0  2574k      0  0:01:21  0:00:51  0:00:30 2644k
            64  205M   64  131M    0     0  2585k      0  0:01:21  0:00:52  0:00:29 2761k
 65  205M   65  134M    0     0  2590k      0  0:01:21  0:00:53  0:00:28 2712k
 67  205M   67  138M    0     0  2605k      0  0:01:20  0:00:54  0:00:26 2803k
 68  205M   68  141M    0     0  2621k      0  0:01:20  0:00:55  0:00:25 3007k
 70  205M   70  144M    0     0  2631k      0  0:01:20  0:00:56  0:00:24 3218k
 71  205M   71  147M    0     0  2641k      0  0:01:19  0:00:57  0:00:22 3223k
 73  205M   73  150M    0     0  2654k      0  0:01:19  0:00:58  0:00:21 3342k
 74  205M   74  154M    0     0  2667k      0  0:01:19  0:00:59  0:00:20 3333k
 76  205M   76  157M    0     0  2679k      0  0:01:18  0:01:00  0:00:18 3322k
 78  205M   78  161M    0     0  2695k      0  0:01:18  0:01:01  0:00:17 3413k
 79  205M   79  163M    0     0  2692k      0  0:01:18  0:01:02  0:00:16 3277k
 81  205M   81  167M    0     0  2704k      0  0:01:17  0:01:03  0:00:14 3279k
 82  205M   82  170M    0     0  2720k      0  0:01:17  0:01:04  0:00:13 3347k
 83  205M   83  172M    0     0  2714k      0  0:01:17  0:01:05  0:00:12 3136k
 85  205M   85  176M    0     0  2725k      0  0:01:17  0:01:06  0:00:11 3102k
 87  205M   87  179M    0     0  2733k      0  0:01:17  0:01:07  0:00:10 3238k
 88  205M   88  183M    0     0  2746k      0  0:01:16  0:01:08  0:00:08 3284k
 90  205M   90  186M    0     0  2758k      0  0:01:16  0:01:09  0:00:07 3254k
 91  205M   91  189M    0     0  2758k      0  0:01:16  0:01:10  0:00:06 3328k
 93  205M   93  192M    0     0  2763k      0  0:01:16  0:01:11  0:00:05 3263k
 95  205M   95  195M    0     0  2776k      0  0:01:15  0:01:12  0:00:03 3356k
 96  205M   96  198M    0     0  2780k      0  0:01:15  0:01:13  0:00:02 3242k
 97  205M   97  201M    0     0  2778k      0  0:01:15  0:01:14  0:00:01 3057k
 99  205M   99  203M    0     0  2774k      0  0:01:15  0:01:15 --:--:-- 3007k
100  205M  100  205M    0     0  2781k      0  0:01:15  0:01:15 --:--:-- 3064k
Building flutter tool...

Upgrading engine...
Flutter assets will be downloaded from https://storage.flutter-io.cn. Make sure you trust this source!
Downloading Material fonts...                                    1,130ms
Downloading android-arm-profile/darwin-x64 tools...              1,245ms
Downloading android-arm-release/darwin-x64 tools...              2,121ms
Downloading android-arm64-profile/darwin-x64 tools...            1,506ms
Downloading android-arm64-release/darwin-x64 tools...              22.5s
Downloading android-x64-profile/darwin-x64 tools...              2,979ms
Downloading android-x64-release/darwin-x64 tools...              1,268ms
Downloading android-x86 tools...                                    4.1s
Downloading android-x64 tools...                                    4.9s
Downloading android-arm tools...                                    4.2s
Downloading android-arm-profile tools...                         2,765ms
Downloading android-arm-release tools...                         1,596ms
Downloading android-arm64 tools...                                  4.1s
Downloading android-arm64-profile tools...                       2,656ms
Downloading android-arm64-release tools...                       1,451ms
Downloading android-x64-profile tools...                         2,992ms
Downloading android-x64-release tools...                         1,652ms
Downloading android-x86-jit-release tools...                     2,803ms
Downloading ios tools...                                           20.2s
Downloading ios-profile tools...                                   15.4s
Downloading ios-release tools...                                   90.0s
Downloading Web SDK...                                             11.2s
Downloading CanvasKit...                                         1,934ms
Downloading darwin-x64/FlutterMacOS.framework tools...              8.4s
Downloading darwin-x64/gen_snapshot tools...                        3.1s
Downloading darwin-x64-profile/FlutterMacOS.framework tools...         5.0s
Downloading darwin-x64-profile tools...                          1,208ms
Downloading darwin-x64-profile/gen_snapshot tools...             2,256ms
Downloading darwin-x64-release/FlutterMacOS.framework tools...         3.6s
Downloading darwin-x64-release tools...                          1,146ms
Downloading darwin-x64-release/gen_snapshot tools...             2,208ms

Flutter 3.0.0 • channel stable • https://github.com/flutter/flutter.git
Framework • revision ee4e09cce0 (9 天前) • 2022-05-09 16:45:18 -0700
Engine • revision d1b9a6938a
Tools • Dart 2.17.0 • DevTools 2.12.2

Running flutter doctor...
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 3.0.0, on macOS 12.4 21F79 darwin-x64, locale zh-Hans-CN)
[✓] Android toolchain - develop for Android devices (Android SDK version 29.0.2)
[!] Xcode - develop for iOS and macOS (Xcode 13.4)
    ! CocoaPods 1.10.1 out of date (1.11.0 is recommended).
        CocoaPods is used to retrieve the iOS and macOS platform side's plugin code that responds to your plugin usage on the Dart side.
        Without CocoaPods, plugins will not work on iOS or macOS.
        For more info, see https://flutter.dev/platform-plugins
      To upgrade see https://guides.cocoapods.org/using/getting-started.html#installation for instructions.
[✓] Chrome - develop for the web
[✓] Android Studio (version 2021.2)
[✓] IntelliJ IDEA Ultimate Edition (version 2021.1.1)
[✓] VS Code (version 1.67.1)
[✓] Connected device (3 available)
[✓] HTTP Host Availability

! Doctor found issues in 1 category.
```

[根据提示](https://guides.cocoapods.org/using/getting-started.html#installation) ，升级 Cocoapods：

```bash
sudo gem install cocoapods
Password:
Ignoring ffi-1.15.0 because its extensions are not built. Try: gem pristine ffi --version 1.15.0
Fetching addressable-2.8.0.gem
Fetching cocoapods-core-1.11.3.gem
Fetching molinillo-0.8.0.gem
Fetching rexml-3.2.5.gem
Fetching xcodeproj-1.21.0.gem
Fetching cocoapods-1.11.3.gem
Successfully installed addressable-2.8.0
Successfully installed cocoapods-core-1.11.3
Successfully installed molinillo-0.8.0
Successfully installed rexml-3.2.5
Successfully installed xcodeproj-1.21.0
Successfully installed cocoapods-1.11.3
Parsing documentation for addressable-2.8.0
Installing ri documentation for addressable-2.8.0
Parsing documentation for cocoapods-core-1.11.3
Installing ri documentation for cocoapods-core-1.11.3
Parsing documentation for molinillo-0.8.0
Installing ri documentation for molinillo-0.8.0
Parsing documentation for rexml-3.2.5
Installing ri documentation for rexml-3.2.5
Parsing documentation for xcodeproj-1.21.0
Installing ri documentation for xcodeproj-1.21.0
Parsing documentation for cocoapods-1.11.3
Installing ri documentation for cocoapods-1.11.3
Done installing documentation for addressable, cocoapods-core, molinillo, rexml, xcodeproj, cocoapods after 5 seconds
6 gems installed
```

再次查看 flutter 环境：

```bash
flutter doctor -v
[✓] Flutter (Channel stable, 3.0.0, on macOS 12.4 21F79 darwin-x64, locale zh-Hans-CN)
    • Flutter version 3.0.0 at /Users/guanguan/Applications/flutter
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision ee4e09cce0 (9 天前), 2022-05-09 16:45:18 -0700
    • Engine revision d1b9a6938a
    • Dart version 2.17.0
    • DevTools version 2.12.2
    • Pub download mirror https://pub.flutter-io.cn
    • Flutter download mirror https://storage.flutter-io.cn

[✓] Android toolchain - develop for Android devices (Android SDK version 29.0.2)
    • Android SDK at /Users/guanguan/Library/Android/sdk
    • Platform android-31, build-tools 29.0.2
    • Java binary at: /Applications/Android Studio.app/Contents/jre/Contents/Home/bin/java
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)
    • All Android licenses accepted.

[✓] Xcode - develop for iOS and macOS (Xcode 13.4)
    • Xcode at /Applications/Xcode.app/Contents/Developer
    • CocoaPods version 1.11.3

[✓] Chrome - develop for the web
    • Chrome at /Applications/Google Chrome.app/Contents/MacOS/Google Chrome

[✓] Android Studio (version 2021.2)
    • Android Studio at /Applications/Android Studio.app/Contents
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 11.0.12+0-b1504.28-7817840)

[✓] IntelliJ IDEA Ultimate Edition (version 2021.1.1)
    • IntelliJ at /Applications/IntelliJ IDEA.app
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart

[✓] VS Code (version 1.67.1)
    • VS Code at /Applications/Visual Studio Code.app/Contents
    • Flutter extension version 3.40.0

[✓] Connected device (3 available)
    • Android SDK built for x86 (mobile) • emulator-5554 • android-x86    • Android 8.0.0 (API 26) (emulator)
    • macOS (desktop)                    • macos         • darwin-x64     • macOS 12.4 21F79 darwin-x64
    • Chrome (web)                       • chrome        • web-javascript • Google Chrome 101.0.4951.64

[✓] HTTP Host Availability
    • All required HTTP hosts are available

• No issues found!
```

HTTP Host Availability 问题解决！

### <a name="target2">Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.</a>

这是更新 flutter 到3.0 出现的新问题，解决方案参考官网：

> rf.
>
> https://docs.flutter.dev/development/tools/sdk/release-notes/release-notes-3.0.0#if-you-see-warnings-about-bindings
>
> [Warning: Operand of null-aware operation '?.' has type 'WidgetsBinding' which excludes null #769](https://github.com/daohoangson/flutter_widget_from_html/issues/769)
>
> [ 'WidgetsBinding' runtime warnings using 3.0.0 stable release #103561](https://github.com/flutter/flutter/issues/103561#)【官方推荐】

详细报错：

```dart
Running "flutter pub get" in app...
Launching lib/main.dart on Android SDK built for x86 in debug mode...
Running Gradle task 'assembleDebug'...
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/cached_network_image-3.2.0/lib/src/image_provider/cached_network_image_provider.dart:109:29: Warning: Operand of null-aware operation '?.' has type 'PaintingBinding' which excludes null.
 - 'PaintingBinding' is from 'package:flutter/src/painting/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/painting/binding.dart').
      () => PaintingBinding.instance?.imageCache?.evict(key),
                            ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/cached_network_image-3.2.0/lib/src/image_provider/multi_image_stream_completer.dart:152:22: Warning: Operand of null-aware operation '?.' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
    SchedulerBinding.instance?.scheduleFrameCallback(_handleAppFrame);
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/custom_layout.dart:32:20: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
    WidgetsBinding.instance!.addPostFrameCallback(_getSize);
                   ^
lib/widget/animation_cart.dart:39:20: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
    WidgetsBinding.instance!.addPostFrameCallback((_) {
                   ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/transformer_page_view/transformer_page_view.dart:516:22: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
      WidgetsBinding.instance!.addPostFrameCallback(_onGetSize);
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/transformer_page_view/transformer_page_view.dart:533:22: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
      WidgetsBinding.instance!.addPostFrameCallback(_onGetSize);
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_state_manager/src/rx_flutter/rx_disposable.dart:20:22: Warning: Operand of null-aware operation '?.' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
    SchedulerBinding.instance?.addPostFrameCallback((_) => onReady());
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_state_manager/src/rx_flutter/rx_notifier.dart:130:22: Warning: Operand of null-aware operation '?.' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
    SchedulerBinding.instance?.addPostFrameCallback((_) => onReady());
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_state_manager/src/simple/get_controllers.dart:90:20: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
    WidgetsBinding.instance!.addObserver(this);
                   ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_state_manager/src/simple/get_controllers.dart:96:20: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
    WidgetsBinding.instance!.removeObserver(this);
                   ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_navigation/src/extension_navigation.dart:357:24: Warning: Operand of null-aware operation '!' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
      SchedulerBinding.instance!.addPostFrameCallback((_) {
                       ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_navigation/src/extension_navigation.dart:468:24: Warning: Operand of null-aware operation '!' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
      SchedulerBinding.instance!.addPostFrameCallback((_) {
                       ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_navigation/src/snackbar/snackbar.dart:452:22: Warning: Operand of null-aware operation '!' has type 'SchedulerBinding' which excludes null.
 - 'SchedulerBinding' is from 'package:flutter/src/scheduler/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/scheduler/binding.dart').
    SchedulerBinding.instance!.addPostFrameCallback(
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/get-4.6.1/lib/get_navigation/src/router_report.dart:53:22: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
      WidgetsBinding.instance!.addPostFrameCallback((_) {
                     ^
```

根据官方推荐`dart fix --apply`，运行程序，报错信息只剩下：

```
Performing hot reload...
Syncing files to device Android SDK built for x86...
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/custom_layout.dart:32:20: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
    WidgetsBinding.instance!.addPostFrameCallback(_getSize);
                   ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/transformer_page_view/transformer_page_view.dart:516:22: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
      WidgetsBinding.instance!.addPostFrameCallback(_onGetSize);
                     ^
../../../Applications/flutter/.pub-cache/hosted/pub.dartlang.org/flutter_swiper_plus-2.0.4/lib/src/transformer_page_view/transformer_page_view.dart:533:22: Warning: Operand of null-aware operation '!' has type 'WidgetsBinding' which excludes null.
 - 'WidgetsBinding' is from 'package:flutter/src/widgets/binding.dart' ('../../../Applications/flutter/packages/flutter/lib/src/widgets/binding.dart').
      WidgetsBinding.instance!.addPostFrameCallback(_onGetSize);
                     ^
Reloaded 9 of 1563 libraries in 796ms.
```

这里的报错应该就是第三方插件`flutter_swiper_plus`的缓存问题。

> rf.
>
> [Clean up the bindings APIs. #89451](https://github.com/flutter/flutter/pull/89451)
>
> - Make accesses to `instance` not required `!`.
>
>   使用 `instance`不需要`!`。

根据提示的文件及行号，在电脑中找到对应的三个文件的位置，依次修改即可：

```dart
//custom_layout.dart:32:20
WidgetsBinding.instance.addPostFrameCallback(_getSize);
//transformer_page_view.dart:516:22
WidgetsBinding.instance.addPostFrameCallback(_onGetSize);
//transformer_page_view.dart:533:22
WidgetsBinding.instance.addPostFrameCallback(_onGetSize);
```

至此，解决！



























