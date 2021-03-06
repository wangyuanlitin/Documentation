
---
title: 实时音视频计费
description: 
platform: All Platforms
updatedAt: Mon Jun 22 2020 07:39:25 GMT+0800 (CST)
---
# 实时音视频计费
本文展示 Agora 实时音视频服务的计费方式。

<div class="alert note">如果你已与我们的销售签约，则实际计费信息以合同为准。</div>

## 概述

Agora 会按月统计你的开发者账户下所有项目产生的费用。

当你使用 Agora RTC SDK 在你的项目中实现了实时音视频功能，如语音通话、视频群聊、互动直播后，Agora 会收取实时音视频费用，并按月发布账单、进行扣款。详见[账单、扣费与账户冻结](https://docs.agora.io/cn/faq/billing_account)。

<div class="alert note">
	<ul>
		<li>Agora 给予每个 Agora 开发者账号每个月一万分钟的免费时长。具体的扣除顺序和适用范围请参考<a href="https://docs.agora.io/cn/faq/billing_free">每月一万分钟免费说明</a>。</li>
		<li>如果你的场景中涉及 RTMP 转码推流，除实时音视频费用外，还需要计算转码的费用。</li>
	</ul>
</div>

## 费用组成

Agora 根据你的项目所产生的会话进行计费。每个会话的费用，是这个会话中所有用户产生的费用之和。

针对每个用户，Agora 基于其在频道中的具体订阅情况计费。一个会话中，每个用户可能会产生两种费用：

- 视频费用：如果用户成功订阅了视频流，则产生视频费用。
- 音频费用：如果用户没有订阅视频流，则无论其是否订阅了音频流，都会产生音频费用。

**费用 = 视频费用 + 音频费用 = 视频单价 × 视频时长 + 音频单价 × 音频时长。**

<div class="alert note">
	<ul>
		<li>同一时间内，如果用户既订阅了音频流，也订阅了视频流，则只计算视频费用。</li>
		<li>如果会话中只有一个用户，则该会话的费用，按会话时长 × 音频单价计费。</li>
	</ul>
</div>

## 单价

Agora 音视频单价如下：

| 单价 | 单价（元/千分钟） |
| ---------------- | ---------------- |
| 音频      | 7      |
| 视频      |<ul><li>高清（HD）：28</li><li>超清（HD+）：105</li></ul> |

如果你使用的是微信小程序 SDK，则音视频单价如下：

| 单价 | 单价（元/千分钟）|
| ---------------- | ---------------- |
| 音频      | 10      | 
| 视频      | 30      |

### 视频档位与集合分辨率

Agora 视频单价分两档：

- 高清（HD）：当用户订阅的视频分辨率 ≤ 921600（1280 × 720）时，按高清档计费。
- 超清（HD+）：当用户订阅的视频分辨率 > 921600（1280 × 720）时，按超清档计费。

用户订阅的视频分辨率，为该用户成功订阅的所有视频分辨率之和，也称“**集合分辨率**”。

以用户 A 为例。假设用户 A 在 RTC 频道中，始终订阅 B、C、D 三个用户的视频流。

**示例一**

如果 A 订阅的视频分辨率分别如下：

- A 订阅 B 的分辨率：640 × 360
- A 订阅 C 的分辨率：640 × 360
- A 订阅 D 的分辨率：640 × 360

则用户 A 订阅的集合分辨率 =  640 × 360 +  640 × 360 +  640 × 360 = 691200

由于 691200 小于 921600，用户 A 的订阅集合分辨率属于高清档位，单价按 28 元/1000 分钟计。

**示例二**

如果 A 订阅的视频分辨率发生了改变：

- A 订阅 B 的分辨率：640 × 360
- A 订阅 C 的分辨率
  - 前 10 分钟：640 × 360
  - 后 10 分钟：240 × 180
- A 订阅 D 的分辨率
  - 前 10 分钟：640 × 360
  - 后 10 分钟：1280 × 720

则用户 A 订阅的集合分辨率分两个阶段计：

| 计算阶段 | A 订阅 B 的分辨率 | A 订阅 C 的分辨率 | A 订阅 D 的分辨率 | A 订阅的集合分辨率 |
| ---------------- | ---------------- | ---------------- | ---------------- | ---------------- |
| 后 10 分钟 | 640 × 360      | 240 × 180      | 1280 × 720 | 1195200 |
| 前 10 分钟 | 640 × 360      | 640 × 360      | 640 × 360   | 691200 |

根据上表计算：

- 前 10 分钟 A 订阅的集合分辨率为 691200，小于 921600，属于高清档位，单价按 28 元/1000 分钟计。
- 后 10 分钟 A 订阅的集合分辨率为 1195200，大于 921600，属于超清档位，单价按 105 元/1000 分钟计。

## 时长

针对每个用户，Agora 从其加入频道开始计时，到离开这个频道结束计时。时长的精度为秒。

根据用户在会话中是否订阅视频流，时长可分为如下两类：

- 视频时长：用户接收到视频流的时长，就是视频时长。
- 音频时长：用户在 RTC 频道内的总时长，减去收到视频流的时长后所得剩余时间，无论是否订阅了音频流，都算作是音频时长。

<div class="alert note">如果用户同时订阅多路音频流和视频流，则其订阅的时长不会叠加计算。
<ul>
	<li>如果用户 A 同时订阅用户 B 和 C 的视频流 10 分钟，则用户 A 产生的费用就是 10 分钟视频的费用。</li>
	<li>如果用户 A 同时订阅用户 B 的音频流和用户 C 的视频流 10 分钟，则用户 A 产生的费用也是 10 分钟视频的费用。</li>
</ul>
</div>

## 计费示例

<div class="alert note">本章节中，所有提及视频单价处，均指各用户订阅的视频集合分辨率所对应的视频单价。</div>

### 二人视频通话

**场景描述**：A、B 二人同时加入频道，进行视频通话 20 分钟。

**计费方案**：该会话中 A 和 B 都产生了视频费用。 费用 = A 订阅 B 的视频单价 × 20 分钟/1000 分钟 + B 订阅 A 的视频单价 × 20 分钟/1000 分钟。

### 三人语音通话

**场景描述**：A、B、C 三人同时加入频道，进行语音通话 20 分钟。

**计费方案**：该会话中 A、B 和 C 都产生了音频费用。费用 = 音频单价 × 20 分钟/1000 分钟 + 音频单价 × 20 分钟/1000 分钟 + 音频单价 × 20 分钟/1000 分钟。

### 四人视频通话

**场景描述**：A、B、C 同时三个加入频道，纯音频通话 10 分钟后，D 加入频道，然后四人一起视频通话 10 分钟。

**计费方案**：该会话中 A、B、C、D 都产生了费用。

- A 产生的费用
  - 前十分钟：订阅 B 和 C 音频的费用 = 音频单价 × 10 分钟/1000 分钟
  - 后十分钟：订阅 B、C、D 视频的费用 = 视频单价 × 10 分钟/1000 分钟
- B、C 产生的费用同 A
- D 产生的费用
  - 前十分钟：未产生费用
  - 后十分钟：订阅 A、B、C 视频的费用 = 视频单价 × 10 分钟/1000 分钟

### 单人视频直播

**场景描述**：A 在频道内进行视频直播 20 分钟，有六名观众观看。其中三名观众订阅视频流，三名观众订阅音频流。

**计费方案**：由于 A 在频道内没有订阅行为，因此 A 产生的费用按音频计；六名观众中，三名按视频计，三名按音频计。

费用 = A 产生的音频费用 + 三名观众订阅 A 视频的费用 + 三名观众订阅 A 音频的费用 = 音频单价 × 20 分钟/1000 分钟 + 3 × 视频单价 × 20 分钟/1000 分钟 + 3 × 音频单价 × 20 分钟/1000 分钟。

### 连麦直播

**场景描述**：A 在频道内进行视频直播 10 分钟，有六名观众观看。10 分钟后观众 B 上麦，与 A 视频连麦 10 分钟，其余观众继续观看。

**计费方案**：该会话中 A、B 和所有观众都产生了费用。

- A 产生的费用
  - 前 10 分钟：由于没有订阅行为，因此只产生音频费用 = 音频单价 × 10 分钟/1000 分钟
  - 后 10 分钟：订阅 B 产生的费用 = 视频单价 × 10 分钟/1000 分钟
- B 产生的费用：全程订阅 A 产生的费用 = 视频单价 × 20 分钟/1000 分钟
- 剩余五名观众的费用
  - 前 10 分钟：订阅 A 产生的费用 = 5 × 视频单价 × 10 分钟/1000 分钟
  - 后 10 分钟：订阅 A 和 B 产生的费用 =  5 × 视频单价 × 10 分钟/1000 分钟

## 注意事项

### 双流分辨率

双流模式下，用户的分辨率计算方式如下：

- 如果订阅的是大流，则用户的集合分辨率根据发送端设置的大流分辨率计算。
- 如果订阅的是小流，则用户的集合分辨率根据用户实际收到的分辨率计算。

### 分辨率校准

计算集合分辨率时，我们会将分辨率为 225280（640 × 352）的视频流按分辨率 640 × 360 计算。

## 常见问题

<details><summary><font color="#3ab7f8">为什么只订阅了视频，却在账单中看到了音频分钟数？</font></summary>
<ul>
	<li>如果频道中有用户只发布，却没有订阅任何视频流，那么该用户的集合分辨率为 0，其产生的分钟数就是音频分钟数。</li>
	<li>如果因网络等原因导致某用户没有收到视频，则此刻该用户的集合分辨率计为 0，其对应的分钟数也是音频分钟数。</li>
</ul>
</details>
<details><summary><font color="#3ab7f8">为什么所有用户订阅的都是 360 × 640 的视频流，我的单价却被定在超高清档？</font></summary>
视频档位基于集合分辨率而定，即对你订阅的流的分辨率进行求和。所以，你订阅的视频流越多，你的集合分辨率越有可能超过 1280 x 720 的超清档。
</details>

## 相关文档

- [每月一万分钟免费声明](https://docs.agora.io/cn/faq/billing_free)
- [账单、扣费与账户冻结](https://docs.agora.io/cn/faq/billing_account)
- [如何实现业务层的通话计费？](https://docs.agora.io/cn/faq/business_billing)
- [声网针对预付费是否有响应的优惠策略？](https://docs.agora.io/cn/faq/pricing_package_minute)
