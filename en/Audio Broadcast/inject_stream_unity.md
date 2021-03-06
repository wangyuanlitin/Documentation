
---
title: Inject Online Media Stream
description: 
platform: Unity
updatedAt: Mon Jun 08 2020 02:56:16 GMT+0800 (CST)
---
# Inject Online Media Stream
## Introduction

**Injecting an online media stream** is the action of adding an external audio or video stream to an ongoing live-broadcast channel. It enables the hosts and audience in the channel to hear and see the additional stream while interacting with each other.

### Applicable scenarios

- Live sports: The host and audience can watch and simultaneously comment on events.
- Music concerts, movies, and other entertainments: The hosts and audience can participate in real-time discussions while watching them.
- Additional perspectives: The host can inject video streams captured by drones or network cameras into a live broadcast.

### Working principles

The host in a live-broadcast channel pulls an online media stream and pushes it through the Video Inject Server to the Agora Software-Defined Real-time Network (SD-RTN™) and the channel.

![](https://web-cdn.agora.io/docs-files/1576059890625)

- The host and audience in the channel can hear and see the media stream.
- If the host enables Content Delivery Network (CDN) live streaming, the injected media stream is also pushed to the CDN so that the CDN audience can hear and see the media stream.

>- Only one online media stream can be injected into the same channel at the same time.
>- Supported codec type: AAC for audio, H.264 for video.
>- Audio-only streams are also supported.
>- Only the host (broadcaster) can inject and remove an injected media stream. Neither the delegated host nor the audience can do that.


## Implementation

Before proceeding, ensure that you implement a basic live broadcast in your project. See [Start a Live Broadcast](../../en/Audio%20Broadcast/start_live_unity.md) for details.

<div class="alert note">Ensure that you enable the RTMP Converter service before using this function. See <a href="../../en/Audio%20Broadcast/cdn_streaming_unity.md">Prerequisites</a >.</div>

Refer to the following steps to inject an online media stream:

1. The host in a channel calls the `AddInjectStreamUrl` method to inject an online media stream to the live broadcast channel. You can modify the parameter values of `streamConfig` to set the resolution, bitrate and frame rate of the injected stream. See [`InjectStreamConfig`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/structagora__gaming__rtc_1_1_inject_stream_config.html).
	
	<div class="alert note">Only one online media stream can be injected into the same channel at the same time.</div>

	If the method call is successful, SDK triggers the `OnUserJoinedHandler (uid:666)` callback to all the users in the channel, and triggers the `OnStreamInjectedStatusHandler` callback to the local host.
	
	<div class="alert note">The local host can troubleshoot with <a href="#api">API Reference</a > when exceptions occur.</div>
	
2. The host in a channel calls the `RemoveInjectStreamUrl` method to remove the injected media stream.
	If the method call is successful, SDK triggers the `OnUserOfflineHandler (uid:666)` callback to all the users in the channel.
	
	<div class="alert note">You do not need to call the <tt>RemoveInjectStreamUrl</tt> method if the host has left the channel.</div>


### Sample code

```c#
InjectStreamConfig injectStreamConfig = new InjectStreamConfig();
injectStreamConfig.width = 0;
injectStreamConfig.height = 0;
injectStreamConfig.videoGop = 30;
injectStreamConfig.videoFramerate = 15;
injectStreamConfig.videoBitrate = 400;
injectStreamConfig.audioSampleRate = AUDIO_SAMPLE_RATE_TYPE.AUDIO_SAMPLE_RATE_48000;
injectStreamConfig.audioChannels = 1;
injectStreamConfig.audioBitrate = 48;

// Inject an online media stream.
mRtcEngine.AddInjectStreamUrl(url, injectStreamConfig);
// Remove an online media stream.
mRtcEngine.RemoveInjectStreamUrl(url);
```

<a name="api"></a>
### API reference

- [`AddInjectStreamUrl`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/classagora__gaming__rtc_1_1_i_rtc_engine.html#abe43084af3a653224b29f8cce889d5a1)
- [`RemoveInjectStreamUrl`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/classagora__gaming__rtc_1_1_i_rtc_engine.html#aadd1aa9a403c124d7411297680d1e75a)
- [`OnStreamInjectedStatusHandler`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/namespaceagora__gaming__rtc.html#a95f6a0d38bd007ba3ee5cfc81c14fa52)
- [`OnUserJoinedHandler`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/namespaceagora__gaming__rtc.html#a86b22a3338223db2b36d53020a55d3a9)
- [`OnUserOfflineHandler`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/unity/namespaceagora__gaming__rtc.html#a98bfb4310e947f95dbc43c071c2f8ccf)

## Considerations
To receive the injected media stream, the audience need to subscribe to the host.
