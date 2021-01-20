---
title: 混合现实中的共享体验
description: 全息应用可以共享从一个 HoloLens 到另一个 HoloLens 的空间定位点，使用户能够在真实世界的同一位置（跨多个设备）呈现一个全息影像。
author: thetuvix
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: 共享体验，混合现实，全息影像，空间锚，多用户，多
ms.openlocfilehash: 3383bcd8b87dad6e817262d96b8ac1ebb3d0c8f5
ms.sourcegitcommit: d3a3b4f13b3728cfdd4d43035c806c0791d3f2fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "98583151"
---
# <a name="shared-experiences-in-mixed-reality"></a>混合现实中的共享体验

全息影像不需要仅对一个用户保密。 全息版应用可能会从一个 HoloLens、iOS 或 Android 设备共享 [空间锚点](../../design/spatial-anchors.md) ，使用户能够在真实世界的同一位置跨多个设备渲染一张全息影像。

## <a name="six-questions-to-define-shared-scenarios"></a>定义共享方案的六个问题

在开始设计共享体验之前，定义目标方案非常重要。 这些方案有助于阐明要设计的内容，并建立一个共同术语，以帮助比较和对比你的体验中所需的功能。 了解核心问题和解决方案的不同途径是发现此新介质固有机会的关键所在。

通过我们的 HoloLens 合作伙伴机构的内部原型和探索，我们创建了六个问题来帮助你定义共享方案。 这些问题形成了一个框架，而不是一种全面的设计，旨在帮助用户更好地提取方案的重要属性。

### <a name="1-how-are-they-sharing"></a>1. 它们如何共享？

演示可能由单个虚拟用户导致，而多个用户可进行协作，或者教师可以向使用虚拟材料的虚拟学生提供指导，这种体验的复杂程度取决于用户在方案中具有或可以拥有的代理级别。

![表中的 holograph](images/man-and-women-with-holograph-on-table-500px.png)

有多种方法可以共享，但我们发现，其中的大多数方法分为三类：

* **演示**：在向多个用户显示相同内容时。 例如：教授使用同一个全息材料向每个人提供一个讲座给多名学生。 不过，教授可能会有自己的提示和注释，而其他人可能看不到这些内容。
* **协作**：当人们共同合作来实现某些共同的目标时。 例如：专家提供了一个项目，以了解如何进行心率。 学生配对并创建共享的技能实验室体验，使医疗学生可以在心形模型上进行协作并学习。
* **指南**：当一个人帮助他人解决一种更一对一的样式交互中的问题时。 例如：当用户在共享体验中执行 "视觉" 操作技能实验室时，为学生提供指导。

### <a name="2-what-is-the-group-size"></a>2. 组大小是多少？

**一对一** 共享体验可提供强大的基线，理想情况下，可以在此级别创建概念证明。 但要注意的是， (超过六名用户的大型组共享) 可能会导致技术 (数据和网络) ，同时社交，同时还会遇到 [多个头像](https://vimeo.com/160704056) (所造成的影响。 当你从 **小****组到大型组** 时，复杂性会以指数方式增加。

我们发现组的需求可能分为三个大小类别：
* 1:1
* 小型 < 7
* 大型 >= 7

组大小对重要问题有影响，因为它会影响：

* 全息空间中人员的表示形式
* 对象的小数位数
* 环境规模

### <a name="3-where-is-everyone"></a>3. 每个人是谁？

当在同一位置发生共享体验时，混合现实的强度会成为一种情况。 我们 **称之为这一** 定位。 相反，当分配组时，至少有一个参与者不在同一物理空间中 (例如，在使用) VR 的情况下，我们称之为 **远程体验**。 通常情况下，你的组具有协同工作的参与者和远程参与者 (例如，会议室) 的 **两个组** 。

![表上有 holograph 的三个用户](images/three-people-with-holograph-on-table-500px.png)

以下类别有助于传达用户所在的位置：

* 定位 **：所有** 用户都将处于相同的物理空间。
* **远程**：所有用户将位于不同的物理空间。
* **两者**：你的用户将混合使用协同定位和远程共享空间。

此问题很重要，因为它会影响：

* 用户如何通信？
    * 例如：是否应使用头像？
* 他们看到的对象。 是否共享所有对象？
* 是否需要适应自己的环境？

### <a name="4-when-are-they-sharing"></a>4. 他们何时共享？

我们通常会考虑一下共享体验时的 **同步** 体验：我们都在一起。 但如果包含由其他人添加的单个虚元素，则可以使用 **异步** 方案。 在虚拟环境中，假设有一个便笺或语音备忘录。 如何在设计中处理100虚拟备忘录？ 如果他们来自具有不同隐私级别的数十个用户怎么办？

假设你的体验是以下一类时间：

* **同步**：同时共享全息体验。 例如：两名学生同时执行技能实验室。
* **以异步方式**：在不同时间共享全息体验。 例如：两名学生执行技能实验室，但在不同时间使用单独的部分。
* **两者**：你的用户有时会以同步方式同步，但会以异步方式进行共享。 例如：一名教授在以后对学生完成分配的教授，并在下一天为学生留下笔记。

此问题很重要，因为它会影响：

* 对象和环境暂留。 例如：存储状态，以便可以检索它们。
* 用户透视。 例如：在离开便笺时，可能会记住用户正在查看的内容。

### <a name="5-how-similar-are-their-physical-environments"></a>5. 他们的物理环境有多相似？

除非这些环境的设计是相同的，否则两个完全相同的现实环境（即在协同工作的体验之外）的可能性很小。 更有可能拥有 **类似** 的环境。 例如，会议室是类似的，他们通常会有一个集中定位的表。 另一方面，生活场所是不同的 * *，可以在无限布局数组中包含任意数量的家具。

![表上的 Holograph](images/holograph-on-table-500px.png)

假设你的共享体验符合以下两个类别之一：

* **类似**：往往具有相似家具、环境光线和声音、物理房间大小的环境。 例如：教授在讲座厅 A 中，学生处于讲座厅 B。讲座厅的椅子可能比 B 小，但这两家公司可能都有物理办公桌来放置全息影像。
* **不同：家具** 设置、房间大小、光源和声音注意事项中的环境不同。 例如：教授在一个侧重点房间里，学生们处于大讲座厅，并与学生和老师一起填写。

[考虑环境](/hololens/hololens-environment-considerations)很重要，因为它会影响：

* 用户将如何体验这些对象。 例如：如果你的体验最适用于表，并且用户没有表？ 或在平面地面表面上，但用户的空间很混乱。
* 对象的小数位数。 例如：在表中放置一个六英尺的人类模型可能具有挑战性，但心形模型会很好。

### <a name="6-what-devices-are-they-using"></a>6. 它们使用哪些设备？

今天，你通常可能会看到两个 [**沉浸式设备**](../../discover/immersive-headset-hardware-details.md) 之间的共享体验 (这些设备对于按钮和相对功能可能略有不同，但在这些设备上，如果解决方案面向这些设备，则不会极大地) 或两个 **全息设备** 。 但请考虑是否需要将 **2d 设备** (移动/桌面参与者或观察者) 将是必需的注意事项，尤其是在 **混合2d 和3d 设备** 的情况下。 了解你的参与者将使用的设备类型很重要，不仅因为它们采用不同的保真度和数据约束和机会，而且是因为用户对每个平台都有独特的期望。

## <a name="exploring-the-potential-of-shared-experiences"></a>了解共享体验的潜力

可以结合上述问题的答案来更好地了解你的共享方案，并在扩展体验时 crystallizing 问题。 对于 Microsoft 的团队而言，这有助于建立道路地图来改善我们目前使用的体验、了解这些复杂问题的细微差别，以及如何利用混合现实中的共享体验。

例如，请考虑从 HoloLens 启动的 Skype 方案之一：用户使用了如何使用远程定位的专家的帮助 [修复损坏的光源交换机](https://www.youtube.com/watch?v=iBfzs3G8BEA) 。

![通过 Skype for HoloLens 修复带有协助的光源开关](images/fix-a-broken-switch-with-hololens-640px.jpg)

*专家提供从其 **2d** 桌面计算机到 **三维混合现实** 设备用户的 **1:1** 指导。本 **指南** 是 **同步** 的，物理环境是 **不同** 的。*

这种体验就是我们当前经验的一项变化，即，将视频和语音的模式应用到新媒体。 但正如我们所期待的，我们必须更好地定义应用场景和构建体验的机会，以反映混合现实的强度。

请考虑由 NASA 的 Jet 喷气实验室开发的 [OnSight 协作工具](https://www.youtube.com/watch?v=XtUyUJAVQ6w)。 使用 Mars 火星任务中数据的科学家可在 Martian 横向的数据内实时与同事进行协作。

![在以远程方式分开的同事之间进行协作，为 Mars 火星计划工作](images/onsight-nasa-jpl.gif)

*科研人员 **使用三维****和二维** 设备，通过一组较 **小** 的 **远程** 同事来浏览环境。**协作** (**同步**，但可以异步方式进行) 并且物理环境 (虚拟) **类似**。*

像 OnSight 这样的体验会带来新的合作机会。 从物理上指出虚拟环境中的元素，并在其解释其观点时共享其外观。 OnSight 使用浸入式和状态的镜头来重新考虑混合现实中的共享体验。

直观的协作是会话的成为，合作并了解我们如何将此直觉应用到混合现实的复杂性至关重要。 如果我们不仅可以在混合现实中重新创建共享体验，还可以提升它们，但对于未来的工作来说，这是一项转变。 在混合现实中设计共享体验是一项新的令人兴奋的空间-我们只是一开始。

## <a name="get-started-building-shared-experiences"></a>开始构建共享体验

根据您的应用程序和方案，将有各种要求来实现您所需的体验。 其中包括：

* **Match**：创建会话、播发会话、发现和邀请特定人员，同时在本地和远程加入会话。
* **定位点共享**：能够在一个公共的本地空间内对齐多个设备上的坐标，因此对于所有用户，全息影像都显示在同一位置。
* **网络**：能够在所有参与者之间实时同步用户和全息影像的位置、交互和移动。
* **状态存储**：能够在空间中存储全息图的特性和位置，以便进行中型会话加入，稍后重新调用，并抵御网络问题。

共享体验的关键是，多个用户在自己的设备上看到同一个全息影像，这通常通过共享锚点来跨设备对齐坐标来完成。

若要共享锚，请使用 [Azure 空间锚点](/azure/spatial-anchors)：

* 首先，用户放置全息影像。
* 应用创建 [空间锚](../../design/spatial-anchors.md)，以便在世界上准确固定该全息图。
* 可以通过 [Azure 空间锚点](/azure/spatial-anchors/)将锚点共享到 HoloLens、IOS 和 Android 设备。

使用共享空间定位点，每个设备上的应用现在都有一个可放置内容的 [通用坐标系统](../../design/coordinate-systems.md) 。 现在，应用可以确保在同一位置定位和定位全息影像。

在 HoloLens 设备上，你还可以从一个设备离线共享锚点。  使用以下链接来确定最适合你的应用程序。

## <a name="evaluating-tech-options"></a>评估技术选项

有各种服务和技术选项可用于帮助构建多用户混合现实体验。  选择路径可能比较困难，因此，要采用以方案为中心的角度，下面详细介绍了一些选项。

## <a name="shared-static-holograms-no-interactions"></a>共享静态全息影像 (无交互) 

在应用中利用 [Azure 空间锚](/azure/spatial-anchors/) 。  通过跨设备启用并共享空间锚，你可以创建一个应用程序，让用户同时查看同一位置的全息影像。  需要跨设备进行额外的同步，以使用户能够与全息影像交互，并查看影像的移动或状态更新。

## <a name="share-first-person-perspective"></a>共享第一人称视角

如果有受支持的 Miracast 接收方（如 PC 或电视），则对本地用户利用内置 Miracast 支持，无需其他应用代码。

在应用中利用 [MixedReality-WebRTC](https://github.com/microsoft/mixedreality-webrtc) ，对于远程用户，或在你具有要共享的非 Miracast 设备时。  启用 WebRTC 连接将在用户之间启用1:1 音频/视频流，并使用数据通道跨设备进行消息传送。  混合现实实现通过向其他人提供 HoloLens 用户视图的混合现实视频流，针对 HoloLens 进行优化。  如果要将视频流扩展到多个远程客户端，则通常使用一个 [MCU 服务提供程序](https://webrtcglossary.com/mcu/) (Multipoint 会议单位) ，如 [SignalWire](https://signalwire.com/)。  可通过 [Freeswitch](https://github.com/andywolk/azure-freeswitch-gpu-windows)获取对 Azure 的一键式 SignalWire 部署。

> [!NOTE]
> 请注意，SignalWire 是付费服务，不属于 Microsoft。

## <a name="presenter-spectator-applications-and-demos"></a>Presenter-Spectator 应用程序和演示

利用 [MixedReality-SpectatorView](https://github.com/microsoft/MixedReality-SpectatorView) 将 [spectator view 功能](spectator-view.md) 引入应用。  启用 (HL、Android、iOS 和摄像机) 的其他设备，以查看 HoloLens 在同一位置的不同透视中看到的内容，并接收有关与全息影像交互的主机 HoloLens 用户交互的更新。  使用同一个应用的 spectator 伴随空间，观看、拍摄照片并记录主机对应用程序中的全息影像执行的操作的视频。

**注意：** 图片是通过 iOS/Android 设备上的屏幕截图拍摄的。

## <a name="multi-user-collaborative-experience"></a>多用户协作体验

首先介绍[多用户学习教程](../unity/tutorials/mr-learning-sharing-02.md)，该教程利用了用于本地用户和[Photon SDK](https://www.photonengine.com/PUN)的[Azure 空间锚点](/azure/spatial-anchors/)来同步场景中的内容/状态。 创建本地协作应用程序，其中每个用户在场景中的全息影像上都有自己的观点，每个用户都可以完全与全息影像交互。  所有设备都提供更新，交互冲突管理由 Photon 处理。

> [!NOTE]
> 请注意， [Photon](https://www.photonengine.com/) 是一种非 Microsoft 产品，因此，可能需要使用 Photon 进行计费关系，以实现更高的使用量。

## <a name="future-work"></a>未来工作

组件功能和接口将帮助提供跨各种方案和基础技术的常见一致性和可靠支持。  在此之前，请选择与你要在应用程序中尝试实现的方案相符的最佳路径。

不同的方案或希望使用不同的技术/服务？ 请在此页底部的相应存储库中提供 GitHub 问题的反馈，或在 [HoloDevelopers 的时差](https://holodevelopers.slack.com/)上联系。

## <a name="see-also"></a>另请参阅

* [Azure 空间定位点](/azure/spatial-anchors)
* [DirectX 中的共享空间定位点](shared-spatial-anchors-in-directx.md)
* [Unity 中的共享体验](../unity/shared-experiences-in-unity.md)
* [旁观视图](spectator-view.md)