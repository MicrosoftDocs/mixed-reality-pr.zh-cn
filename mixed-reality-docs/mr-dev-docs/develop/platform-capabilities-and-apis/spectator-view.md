---
title: 旁观视图
description: 在外部设备中将全息影像可视化，通过这种方式在外部显示器上演示混合现实体验，或者录制混合现实体验的视频。
author: chrisfromwork
ms.author: chriba
ms.date: 02/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: 旁观视图, iPhone, iOS, iPad, OpenCV, 相机, ARKit, HoloLens, 混合现实, MixedRealityToolkit, 演示, 录制
ms.openlocfilehash: 7b48315753ada0ae7a94abca5377a083ac659a34
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91696540"
---
# <a name="spectator-view-for-hololens-and-hololens-2"></a><span data-ttu-id="1190f-104">HoloLens 和 HoloLens 2 的旁观视图</span><span class="sxs-lookup"><span data-stu-id="1190f-104">Spectator View for HoloLens and HoloLens 2</span></span>

![记号笔](images/SpecViewPhoneHero.jpg)

## <a name="overview"></a><span data-ttu-id="1190f-106">概述</span><span class="sxs-lookup"><span data-stu-id="1190f-106">Overview</span></span>

<span data-ttu-id="1190f-107">戴上 HoloLens 时，我们通常会忘记这样一件事：没有戴上它的人无法体验到我们所能体验到的神奇感受。</span><span class="sxs-lookup"><span data-stu-id="1190f-107">When wearing a HoloLens, we often forget that a person who does not have it on is unable to experience the wonders that we can.</span></span> <span data-ttu-id="1190f-108">旁观视图可以让他人在 2D 屏幕上观看 HoloLens 用户在其世界中看到的东西。</span><span class="sxs-lookup"><span data-stu-id="1190f-108">Spectator View allows others to see on a 2D screen what a HoloLens user sees in their world.</span></span>
<span data-ttu-id="1190f-109">有了旁观视图，就可以通过快速且经济的方式在移动设备中录制高清全息影像。</span><span class="sxs-lookup"><span data-stu-id="1190f-109">Spectator View offers a fast and affordable approach to recording holograms in HD with mobile devices.</span></span> <span data-ttu-id="1190f-110">有了它，还可以通过摄像机对全息影像进行专业质量的录制。</span><span class="sxs-lookup"><span data-stu-id="1190f-110">It also offers a professional quality recording of holograms with video cameras.</span></span>

## <a name="key-resources"></a><span data-ttu-id="1190f-111">重要资源</span><span class="sxs-lookup"><span data-stu-id="1190f-111">Key Resources</span></span>

* [<span data-ttu-id="1190f-112">**GitHub 上的旁观视图**</span><span class="sxs-lookup"><span data-stu-id="1190f-112">**Spectator View on GitHub**</span></span>](https://github.com/microsoft/MixedReality-SpectatorView)
* [<span data-ttu-id="1190f-113">**旁观视图文档**</span><span class="sxs-lookup"><span data-stu-id="1190f-113">**Spectator View Documentation**</span></span>](https://microsoft.github.io/MixedReality-SpectatorView/README.html)
* [<span data-ttu-id="1190f-114">**旁观视图示例**</span><span class="sxs-lookup"><span data-stu-id="1190f-114">**Spectator View Samples**</span></span>](https://github.com/microsoft/MixedReality-SpectatorView/tree/master/samples)

## <a name="use-cases"></a><span data-ttu-id="1190f-115">用例</span><span class="sxs-lookup"><span data-stu-id="1190f-115">Use Cases</span></span>
* <span data-ttu-id="1190f-116">可以使用 iPhone 或 Android 设备录制混合现实体验。</span><span class="sxs-lookup"><span data-stu-id="1190f-116">You can record a mixed reality experience using an iPhone or Android device.</span></span> <span data-ttu-id="1190f-117">以全高清进行录制，对全息影像甚至阴影应用抗锯齿效果。</span><span class="sxs-lookup"><span data-stu-id="1190f-117">Record in full HD and apply anti-aliasing to holograms and even shadows.</span></span> <span data-ttu-id="1190f-118">这样可以经济高效且快速地捕获全息影像的视频。</span><span class="sxs-lookup"><span data-stu-id="1190f-118">It is a cost-effective and quick way to capture video of holograms.</span></span>
* <span data-ttu-id="1190f-119">将实时混合现实体验直接从 iPhone 或 iPad 流式传输到 Apple TV，没有任何延迟！</span><span class="sxs-lookup"><span data-stu-id="1190f-119">Stream live mixed reality experiences to an Apple TV directly from your iPhone or iPad, lag-free!</span></span>
* <span data-ttu-id="1190f-120">与来宾共享此体验：让非 HoloLens 用户直接在其手机或平板电脑上体验全息影像。</span><span class="sxs-lookup"><span data-stu-id="1190f-120">Share the experience with guests: Let non-HoloLens users experience holograms directly from their phones or tablets.</span></span>

## <a name="current-features"></a><span data-ttu-id="1190f-121">当前功能</span><span class="sxs-lookup"><span data-stu-id="1190f-121">Current Features</span></span>

* <span data-ttu-id="1190f-122">对全息影像进行空间同步，使每个人都能在完全相同的位置观看全息影像。</span><span class="sxs-lookup"><span data-stu-id="1190f-122">Spatial synchronization of Holograms, so everyone sees holograms in the exact same place.</span></span>
* <span data-ttu-id="1190f-123">iOS（支持 ARKit 的设备）和 Android（支持 ARCore 的设备）支持。</span><span class="sxs-lookup"><span data-stu-id="1190f-123">iOS (ARKit-enabled devices) and Android (ARCore-enabled devices) support.</span></span>
<span data-ttu-id="1190f-124">多个 iOS 来宾。</span><span class="sxs-lookup"><span data-stu-id="1190f-124">Multiple iOS guests.</span></span>
<span data-ttu-id="1190f-125">录制视频 + 全息影像 + 环境音效 + 全息音效。</span><span class="sxs-lookup"><span data-stu-id="1190f-125">Recording of video + holograms + ambient sound + hologram sound.</span></span>
<span data-ttu-id="1190f-126">共享表，用于保存视频、通过电子邮件发送视频或将其与其他支持应用共享。</span><span class="sxs-lookup"><span data-stu-id="1190f-126">Share sheet so you can save video, email it, or share with other supporting apps.</span></span>

<span data-ttu-id="1190f-127">![标记](images/SpecViewPhoneDemo.jpg)
![标记](images/hololensspectatorview-500px.jpg) ![标记](images/spectatorview-300px.png)</span><span class="sxs-lookup"><span data-stu-id="1190f-127">![Marker](images/SpecViewPhoneDemo.jpg)
![Marker](images/hololensspectatorview-500px.jpg) ![Marker](images/spectatorview-300px.png)</span></span>

<span data-ttu-id="1190f-128">下表显示了不同的旁观视图功能。</span><span class="sxs-lookup"><span data-stu-id="1190f-128">The following table shows different Spectator View functionality and their capabilities.</span></span> <span data-ttu-id="1190f-129">请选择最符合你的视频录制需求的选项：</span><span class="sxs-lookup"><span data-stu-id="1190f-129">Choose the option that best fits your video recording needs:</span></span>

|      <span data-ttu-id="1190f-130">功能</span><span class="sxs-lookup"><span data-stu-id="1190f-130">Functionality</span></span>                                | <span data-ttu-id="1190f-131">移动型</span><span class="sxs-lookup"><span data-stu-id="1190f-131">Mobile</span></span>                  |                    <span data-ttu-id="1190f-132">摄像机</span><span class="sxs-lookup"><span data-stu-id="1190f-132">Video Camera</span></span>              |
|--------------------------------------|:-----------------------:|:-------------------------------------------:|
| <span data-ttu-id="1190f-133">高清质量</span><span class="sxs-lookup"><span data-stu-id="1190f-133">HD quality</span></span>                           |         <span data-ttu-id="1190f-134">全高清</span><span class="sxs-lookup"><span data-stu-id="1190f-134">Full HD</span></span>         |        <span data-ttu-id="1190f-135">专业质量摄影（取决于摄像机）</span><span class="sxs-lookup"><span data-stu-id="1190f-135">Professional quality filming (as determined by video camera)</span></span>      |
| <span data-ttu-id="1190f-136">相机移动轻松</span><span class="sxs-lookup"><span data-stu-id="1190f-136">Easy camera movement</span></span>                 |            <span data-ttu-id="1190f-137">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-137">✔</span></span>            |                      <span data-ttu-id="1190f-138">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-138">✔</span></span>                      |
| <span data-ttu-id="1190f-139">第三人称视图</span><span class="sxs-lookup"><span data-stu-id="1190f-139">Third-person view</span></span>                    |            <span data-ttu-id="1190f-140">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-140">✔</span></span>            |                      <span data-ttu-id="1190f-141">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-141">✔</span></span>                      |
| <span data-ttu-id="1190f-142">可以流式传输到屏幕</span><span class="sxs-lookup"><span data-stu-id="1190f-142">Can be streamed to screens</span></span>           |            <span data-ttu-id="1190f-143">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-143">✔</span></span>            |                      <span data-ttu-id="1190f-144">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-144">✔</span></span>                      |
| <span data-ttu-id="1190f-145">可移植</span><span class="sxs-lookup"><span data-stu-id="1190f-145">Portable</span></span>                             |            <span data-ttu-id="1190f-146">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-146">✔</span></span>            |                                             |
| <span data-ttu-id="1190f-147">无线</span><span class="sxs-lookup"><span data-stu-id="1190f-147">Wireless</span></span>                             |            <span data-ttu-id="1190f-148">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-148">✔</span></span>            |                                             |
| <span data-ttu-id="1190f-149">其他必需硬件</span><span class="sxs-lookup"><span data-stu-id="1190f-149">Additional required hardware</span></span>         |     <span data-ttu-id="1190f-150">Android 手机、iPhone</span><span class="sxs-lookup"><span data-stu-id="1190f-150">Android phone, iPhone</span></span>    | <span data-ttu-id="1190f-151">HoloLens + 支架 + 三脚架 + 摄像机 + 电脑 + Unity</span><span class="sxs-lookup"><span data-stu-id="1190f-151">HoloLens + Rig + Tripod + Video Camera + PC + Unity</span></span> |
| <span data-ttu-id="1190f-152">硬件投资</span><span class="sxs-lookup"><span data-stu-id="1190f-152">Hardware investment</span></span>                  |           <span data-ttu-id="1190f-153">低</span><span class="sxs-lookup"><span data-stu-id="1190f-153">Low</span></span>            |                     <span data-ttu-id="1190f-154">高</span><span class="sxs-lookup"><span data-stu-id="1190f-154">High</span></span>                    |
| <span data-ttu-id="1190f-155">跨平台</span><span class="sxs-lookup"><span data-stu-id="1190f-155">Cross-platform</span></span>                       |           <span data-ttu-id="1190f-156">Android、iOS</span><span class="sxs-lookup"><span data-stu-id="1190f-156">Android, iOS</span></span>   |                                             |
| <span data-ttu-id="1190f-157">同步的内容</span><span class="sxs-lookup"><span data-stu-id="1190f-157">Synchronized content</span></span>                 |            <span data-ttu-id="1190f-158">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-158">✔</span></span>            |                      <span data-ttu-id="1190f-159">✔</span><span class="sxs-lookup"><span data-stu-id="1190f-159">✔</span></span>                      |
| <span data-ttu-id="1190f-160">运行时设置持续时间</span><span class="sxs-lookup"><span data-stu-id="1190f-160">Runtime setup duration</span></span>               |         <span data-ttu-id="1190f-161">即时</span><span class="sxs-lookup"><span data-stu-id="1190f-161">Instant</span></span>          |                     <span data-ttu-id="1190f-162">慢</span><span class="sxs-lookup"><span data-stu-id="1190f-162">Slow</span></span>                    |
## <a name="see-also"></a><span data-ttu-id="1190f-163">请参阅</span><span class="sxs-lookup"><span data-stu-id="1190f-163">See also</span></span>

* [<span data-ttu-id="1190f-164">混合现实捕获</span><span class="sxs-lookup"><span data-stu-id="1190f-164">Mixed reality capture</span></span>](../../mixed-reality-capture.md) 
* [<span data-ttu-id="1190f-165">面向开发人员的混合现实捕获</span><span class="sxs-lookup"><span data-stu-id="1190f-165">Mixed reality capture for developers</span></span>](mixed-reality-capture-for-developers.md)
* [<span data-ttu-id="1190f-166">混合现实中的共享体验</span><span class="sxs-lookup"><span data-stu-id="1190f-166">Shared experiences in mixed reality</span></span>](shared-experiences-in-mixed-reality.md)
