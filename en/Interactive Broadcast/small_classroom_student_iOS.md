
---
title: Build a Client for the Student
description: 
platform: iOS
updatedAt: Wed May 13 2020 08:11:36 GMT+0800 (CST)
---
# Build a Client for the Student
This section describes how to implement an iOS client for the student.

## Flowchart

This flowchart shows the major logic of the student joining and leaving the classroom:

![](https://web-cdn.agora.io/docs-files/1589357486215)

## Integrate the SDK

Refer to the following table to download the SDKs, and integrate the SDKs into your project.


| Product | SDK download | Integration guide |
| ---------------- | ---------------- | ---------------- |
| [RTC (Real-time Communication) SDK](https://docs.agora.io/en/Interactive%20Broadcast/product_live?platform=All%20Platforms)      | [Agora SDK for iOS](https://download.agora.io/sdk/release/Agora_Native_SDK_for_iOS_v2_9_0_102_FULL_20200216_2115.zip)     | [Start a Live Broadcast](https://docs.agora.io/en/Interactive%20Broadcast/start_live_ios?platform=iOS) |
| [RTM (Real-time Messaging) SDK](https://docs.agora.io/en/Real-time-Messaging/product_rtm?platform=All%20Platforms) | [Real-time messaging SDK](https://docs.agora.io/en/Real-time-Messaging/downloads) | [Peer-to-peer or Channel Messaging](https://docs.agora.io/en/Real-time-Messaging/messaging_ios?platform=iOS) |
| Agora Edu Cloud Service | / | [Agora Edu Cloud Service quickstart](https://github.com/AgoraIO-Usecase/eEducation/wiki/Agora-Edu-Cloud-Service) |
| [Whiteboard](https://developer-en.netless.link/docs/ios/overview/ios-introduction/) | [White SDK](https://developer-en.netless.link/docs/ios/quick-start/ios-prepare/) | [Whiteboard quickstart](https://developer-en.netless.link/docs/ios/quick-start/ios-init-sdk/) | 


## Core API call sequence

Refer to the following diagram to implement the basic real-time communication and messaging functions in your project with the Agora RTC SDK, Agora RTM SDK, and Agora Edu Cloud Service.

![](https://web-cdn.agora.io/docs-files/1589352187525)

## Core API reference

- Agora Edu Cloud Service

| API | Function |
| ---------------- | ---------------- |
| [entry](https://github.com/AgoraIO-Usecase/eEducation/wiki/Agora-Edu-Cloud-Service#enter-a-classroom) | Enter a room. |
| [get room info](https://github.com/AgoraIO-Usecase/eEducation/wiki/Agora-Edu-Cloud-Service#initialize-a-classroom) | Get the room info. |
| [change room info](https://github.com/AgoraIO-Usecase/eEducation/wiki/Agora-Edu-Cloud-Service#change-room-info) | Change the room info. |
| [change user info](https://github.com/AgoraIO-Usecase/eEducation/wiki/Agora-Edu-Cloud-Service#change-user-info) | Change the user info. |
 
- Agora RTM SDK

| API | Function |
| ---------------- | ---------------- |
| [initWithAppId](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/initWithAppId:delegate:)      | Creates an AgoraRtmKit object.   |
| [loginByToken](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/loginByToken:user:completion:) | Logs into the Agora RTM system. |
| [createChannelWithId](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/createChannelWithId:delegate:) | Creates an Agora RTM channel. You can create multiple channels with an AgoraRtmKit object. |
| [joinWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/joinWithCompletion:) | Joins an Agora RTM channel. |
| [initWithText](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmMessage.html#//api/name/initWithText:) | Creates an AgoraRtmMessage object. |
| [sendMessage](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/sendMessage:completion:) | Sends a channel message, which can be received by all the users in the channel. |
| [leaveWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/leaveWithCompletion:) | Leaves the RTM channel. |
| [logoutWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/logoutWithCompletion:) | Logs out of the RTM system. |

- Agora RTC SDK


| API | Function |
| ---------------- | ---------------- |
| [sharedEngineWithAppId](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/sharedEngineWithAppId:delegate:)      | Initialize an AgoraRtcEngineKit object.      |
| [setChannelProfile](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setChannelProfile:) | Sets the channel profile. In this scenario, we set the channel profile as Live Broadcast.|
| [setClientRole](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setClientRole:) | Sets the user role in a live broadcast. In this scenario, we set the role of students as broadcaster before they join the channel. During the class, the students and the teacher can see and talk to each other in real time. |
| [enableVIdeo](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/enableVideo:) | Enables the video module. |
| [setVideoEncoderConfiguration](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setVideoEncoderConfiguration:) | Sets the video encoder configuration. |
| [setupLocalVideo](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setupLocalVideo:) | Sets the local video view. |
| [joinChannelByToken](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/joinChannelByToken:channelId:info:uid:joinSuccess:) | Joins an Agora RTC channel. You can call [startPreview](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/java/classio_1_1agora_1_1rtc_1_1_rtc_engine.html#a9143c9bb03165fe8b07c0c1e5a455ffb) to start the local video preview before joining a channel. |
| [setupRemoteVideo](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setupRemoteVideo:) | Sets the remote video view. |
| [leaveChannel](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/leaveChannel:) | Leaves the RTC channel.  |


## Additional functions

For more features and functions available for an  online class, you can refer to the following:


<details>
<summary>Monitor the network quality</summary>
Use the <code>networkQuality</code> callback of the Agora RTC SDK  to monitor the last-mile uplink and downlink network quality of every user in the channel. 
For more methods for reporting the real-time network quality, see the following guides:
<li><a href="https://docs.agora.io/en/Interactive%20Broadcast/lastmile_quality_apple?platform=iOS">Lastmile tests</a></li>
<li><a href="https://docs.agora.io/en/Interactive%20Broadcast/in-call_quality_apple?platform=iOS">In-call Stats</a></li>
</details>
<details>
<summary>Mute the local audio or video</summary>
Call the following methods provided by the Agora RTC SDK:
<li><code>muteLocalAudioStream</code>, to stop or resume sending the local audio stream.</li>
<li><code>muteLocalVideoStream</code>, to stop or resume sending the local video stream.</li>
</details>
<details>
<summary>Voice detection</summary>
For RTC SDKs later than v2.9.2, you can enable voice detection by calling <code>enableAudioVolumeInfication</code>, and setting the <code>report_vad</code> parameter as <code>true</code>.
Once enabled, the <code>reportAudioVolumeIndicationOfSpeakers</code> callback reports whether the local user is speaking in the <code>AgoraRtcAudioVolumeInfo</code> struct.
</details>
<details>
<summary>Whiteboard</summary>
Implement the following whiteboard functions in your project:
	<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-document/">Document Conversion</a></li>
		<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-state/">State Management</a></li>
	<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-tools/">Tools</a></li>
	<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-view/">Perspective operation</a></li>
	<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-operation/">Whiteboard Operation</a></li>
	<li><a href="https://developer-en.netless.link/docs/ios/guides/ios-scenes/">Page (Scene) Management</a></li>
</details>


## Open-source demo project

Agora provides an open-source demo for [Small Classroom](https://github.com/AgoraIO-Usecase/eEducation) on GitHub to download as a source code reference.
