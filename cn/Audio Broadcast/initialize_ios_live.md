
---
title: 初始化 AgoraRtcEngineKit
description: iOS平台初始化
platform: iOS
updatedAt: Thu Dec 13 2018 07:50:12 GMT+0800 (CST)
---
# 初始化 AgoraRtcEngineKit
在初始化 AgoraRtcEngineKit 前，请确保你已完成环境准备、安装包获取等步骤，详见[集成客户端](../../cn/Interactive%20Broadcast/ios_video.md)。

## 实现方法

进入频道之前，调用 `sharedEngineWithAppId` 方法创建一个 AgoraRtcEngine 实例。

在该方法中：

- 填入获取到的 App ID 。只有 App ID 相同的应用程序才能进入同一个频道进行互通。
- 指定一个 delegate 对象。SDK 通过指定的 delegate 通知应用程序 SDK 的运行事件，如：加入或离开频道、新用户加入频道等。

```objective-c
//Objective-C
#import <AgoraRtcEngineKit/AgoraRtcEngineKit.h>

...

- (void)initializeAgoraEngine {
  self.agoraKit = [AgoraRtcEngineKit sharedEngineWithAppId:@"Your App ID" delegate:self];
}
```

```swift
//Swift
import AgoraRtcEngineKit

...

func initializeAgoraEngine() {
   agoraKit = AgoraRtcEngineKit.sharedEngine(withAppId: "Your App ID", delegate: self)
}
```

> 请确保在调用其他 API 前先调用 `initializeEngineWithAppId` 方法创建并初始化 AgoraRtcEngine。

## 相关文档
完成创建实例后，你可以使用 Agora SDK，依次实现如下功能进行互动直播：
* [加入频道](../../cn/Interactive%20Broadcast/join_live_ios.md)
* [切换用户角色](../../cn/Interactive%20Broadcast/role_ios.md)
* [发布和订阅音频流](../../cn/Interactive%20Broadcast/publish_ios_live.md)

如果对网络或音质有特殊的需求，你还可以在加入频道前：
* [进行通话前网络质量监测](../../cn/Interactive%20Broadcast/lastmile_ios.md)
* [使用双声道/高音质](../../cn/Interactive%20Broadcast/audio_profile_ios_audio.md)
