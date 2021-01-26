---
title: 具有 Windows Mixed Reality 的基于位置的娱乐
description: 了解基于位置娱乐的 Windows Mixed Reality-硬件、背包 Pc、跟踪、配置和支持。
author: jessemcculloch
ms.author: ishitak
ms.date: 08/03/2020
ms.topic: article
keywords: mixed reality，vr，lbe，位置，混合现实耳机，windows mixed reality 耳机，虚拟现实耳机，硬件，HoloLens，多玩家，云服务，azure
ms.openlocfilehash: 1cc54ad0ef4b9892c49e13c7437a4d5356093c79
ms.sourcegitcommit: 63b7f6d5237327adc51486afcd92424b79e6118b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98810101"
---
# <a name="location-based-entertainment-with-windows-mixed-reality"></a>具有 Windows Mixed Reality 的基于位置的娱乐

在过去几年中，我们在基于地点的娱乐类别中看到了惊人的增长和创新。 传统的会场（如主题公园和电影院）已开始提供沉浸式多玩家体验，作为现有搭乘和安装的免费体验。 新的操作员和会场为面向大众带来了独特的多 sensorial、多玩家体验。 所有这些经验都是通过推送信封来实现混合现实。

本文档是在基于位置的娱乐类别中开始使用 Windows Mixed Reality 的指南。 下面的指南可能还适用于超出娱乐的位置体验，例如培训、产品设计和其他用例。

## <a name="engineering-faq"></a>工程常见问题

### <a name="hardware"></a>硬件

**问： Microsoft 及其合作伙伴提供的可在我的设置中使用的硬件**

答： Microsoft 及其 OEM 合作伙伴提供了一套极具吸引力的设备，可根据需要进行选择。  

如果你向客户提供的体验需要虚拟现实耳机，HP、Samsung 和 Acer 的市场耳机都非常合适。 每个耳机都有其各自的不同属性。 以下各项的详细信息。

HP 回音： [详细信息](https://hp.com/go/Reverbpro)

Samsung 太空 +： [详细信息](https://www.samsung.com/us/computing/hmd/windows-mixed-reality/hmd-odyssey-windows-mixed-reality-headset-xe800zba-hc1us/)

Acer： [详细信息](https://www.acer.com/ac/en/US/content/model/VD.R05AP.002)

如果你的位置专门使用 "查看" 耳机来实现混合或扩充的现实体验，请查看 Microsoft HoloLens 2。  

HoloLens 2： [订购利息](https://www.microsoft.com//hololens/buy)

如果你正在试验使用高级计算机视觉、语音和正文跟踪的体验，Azure Kinect 深色的优点非常合适。  

Azure Kinect： [详细信息](https://azure.microsoft.com//services/kinect-dk/)

**问：我可以使用哪些背包电脑组合来运行我的电脑-受限 VR 体验？**

对于电脑受限 VR 体验，我们的 Oem 提供了令人难以置信地选择的背包 Pc。

HP 刚刚启动了其 HP VR 背包 G2，这是世界上最强大的可穿戴 PC –为自由漫游体验进行了优化，现在，在内部使用 RTX 2080 GPU 可提高30% 的电量。 [详细信息](https://www8.hp.com/us/en/vr/vr-backpack.html)

### <a name="setup"></a>设置

**问：如何更轻松地配置安装并为 LBE 自定义混合现实门户？**

>[!NOTE]
>此功能需要2000.19061.1011.0 或更高版本。  

你可能会发现，你需要对混合现实门户进行更多的自定义，而不是通常通过用于将应用部署到展台或自定义体验的应用使用。 混合现实门户的最新7月更新支持多个高级设置，你可以通过配置文件进行设置：  

允许故障系统检查–在完成安装程序之前，安装过程通常会检查 PC 与 Windows Mixed Reality 的兼容性。 如果存在兼容性问题，则在尝试运行 Windows Mixed Reality 时，绕过兼容性检查可能会导致问题。  

跳过设备辅助应用– DCA 提供制造商提供的耳机特定的设置步骤，并允许更新耳机固件。  

跳过房间安装-不会提示你创建房间边界，你可以继续在 "固定"/"固定" 模式下直接进入耳机。  

跳过从应用商店安装应用-普通安装程序将安装多个应用商店应用，包括3D 查看器和 Edge 360 查看器加载项。 这会跳过这些应用的安装，但可能缺少设备功能。  

全屏显示预览–混合现实门户将默认为在使用耳机时在台式计算机上全屏显示耳机预览。  

隐藏侧面板的新增部分–禁止在启动混合现实门户时展开面板的新新。  

#### <a name="how-to-configure"></a>配置方式：  

若要设置这些配置中的任何一种，需要在此目录下创建一个名为 _UserConfig.js_ 的文件： _$env \\ ： localappdata\packages\ Microsoft.MixedReality.Portal_8wekyb3d8bbwe \localstate_

对于大多数用户，此内容如下所示： _C:\Users \<username> \Appdata\local\packages\ microsoft.mixedreality.portal_8wekyb3d8bbwe \\ \localstate_

对于您想要启用的任意设置，JSON 文件的内容应为 "true"：  

```
{

  "shouldAllowFailedSystemChecks": true,

  "shouldSkipDcaApp": true,

  "shouldSkipRoomSetup": true,

  "shouldSkipStoreAppInstall": true,

  "shouldShowPreviewFullScreen": true,

  "shouldHideEngagementPane": true

}
```
 
**问：是否有关于配置 playspace 的指导？**

答：配置 playspace 应像使用使用者安装体验一样完成。 房间设置过程还将允许您定义房间边界。 有关配置空间边界的详细信息，请参阅 [此处](/windows/mixed-reality/enthusiast-guide/set-up-windows-mixed-reality#set-up-your-room-boundary)。

如以上文档中所述，最大合理的单个坐标 playspace 是围绕5mx5m 的。 如果要获得更大的区域，可以使用 Windows 全息 API 堆栈中的空间锚功能。 使用此 API 需要在生成的体验中进行自定义工程。  

可在 [此处](/windows/mixed-reality/coordinate-systems)阅读有关如何针对不同的空间大小优化内容的更多详细信息。
 

**问：我的空间太大了，在尝试使用边界建立持续的体验时，我遇到了错误。设置大的免费漫游体验应该怎么办？**

答：若要设置比 ~ 18x18ft 更大的空间，则无法使用系统提供的边界体验。  边界系统依赖于单个固定坐标 "锚点"，当用户离中心舞台锚点太远时，这会变得不稳定。 

你可以设置 "固定" 模式，这种模式不会显示边界，也不会配置阶段边界或 playspace。  需要在应用程序中配置多个空间锚点以引用物理边界区域。 

应用程序开发人员负责显示必要的安全措施，使用户不会与物理环境发生冲突。  这可能是经验或自定义游戏边界视觉对象中的数字背景。 

可在 [此处](/windows/mixed-reality/enthusiast-guide/set-up-windows-mixed-reality#set-up-your-room-boundary)找到有关通过 WMR 设置空间边界的指南。

**问： playspace 的来源是什么？**

答： playspace 的来源取决于房间安装体验，更具体地说是在安装过程中按下中心按钮时的 HMD 位置。 

### <a name="multi-player-setup"></a>多玩家安装

**问：我在我的场所部署了多玩家体验。Windows Mixed Reality 是否支持？**

答：如果你通过我们的预览体验计划选择加入 Windows 20H1 或更高版本，则可以访问用于地图共享的新接口。 此新功能可通过 Windows 设备门户的 " [映射管理器](../develop/platform-capabilities-and-apis/using-the-windows-device-portal.md#map-manager) " 界面获得。 若要使用此工具，请执行以下步骤：
* 请确保选择加入20H1 或更高版本（2019年9月之后），这意味着使用预览体验计划
* 使用以下[说明](/windows/uwp/debug-test-perf/device-portal-desktop)启用 Windows 设备门户 (WDP) 
* 插入想要从其下载现有映射的 Windows Mixed Reality HMD，或导入新的映射
* 使用在 "设置" 屏幕中提供的 URL，在所选浏览器中导航到 WDP。
    * 导航到 "Mixed Reality" 部分，然后选择 "映射管理器"。
    * 你现在可以使用 "下载" 按钮从计算机导出现有映射。
    * 您可以使用 "上传地图文件" 按钮从上一个导出 (导入地图，) 。
    * 您可以使用 "导入" 使系统能够在此计算机上为此 HMD 使用该映射。

> [!NOTE] 
> 以前，可以使用空间数据包装器工具，不过，该工具最初发布为不受支持的功能，现已正式弃用并且在20H1 上不再可用。 请改用上文所述的收件箱 [地图管理器](../develop/platform-capabilities-and-apis/using-the-windows-device-portal.md#map-manager) 工具。 

### <a name="tracking"></a>字距

问： Windows Mixed Reality 耳机中的跟踪技术是如何工作的？  

混合现实与 HoloLens 共享相同的跟踪技术。 若要详细了解内部输出跟踪系统，请查看 [此处](/windows/mixed-reality/enthusiast-guide/tracking-system)的文档。

有关更高级的空间映射系统的工作原理的说明，请参阅 [此处](../design/spatial-mapping.md)的说明。

**问：是否有用于获取可靠跟踪卷的最佳实践？**

为了最好地配置用于跟踪成功的环境，您可以阅读此 [文章](/hololens/hololens-environment-considerations)中的最佳实践。

**问：在仓库规模空间或要考虑的优化中，是否有任何特定的细微差别？**

答：以下做法可帮助获取更可靠的跟踪卷：  

在房间中提供与多个位置重叠的不同功能将有助于跟踪系统获得稳定锁定。 请考虑随机绘制 splatters 和阴影，而不是使用纯色等高线样式线条。 

尽可能最大程度地减小区域中的光线的动态范围。 混合现实 HMDs 上的跟踪相机并不是 HDR，AGC (自动) ，而 AEC (自动曝光) 处理不同的照明。 根据不同的表面效果、图案和对比度，无论是 AGC 还是 AEC，都可以使您完全成为所有白色或黑色房间，这会使您的功能变得相对 "颜色"。 如果你正在尝试在具有鲜日光的外部窗口的前方拍摄内部图片，并调整了曝光以便查看外的详细信息，则内部的所有内容都是 underexposed 和黑色。 或者，如果在内部设置，则所有外部的内容现在都是 overexposed，所有白色。  

在房间中的聚光灯 (甚至是在) 的情况下，如果跟踪相机有时原因，这会导致跟踪相机的 AEC/AGC 混乱。 平面/散射照明可帮助。  

### <a name="mixed-reality-cloud-services-and-azure"></a>混合现实云服务和 AZURE 

**问： Microsoft Azure 如何帮助我的业务规模？**

答：基于 Azure 的现场和远程管理可帮助你的企业进行数据驱动，降低运营成本并在现有和新位置扩展部署。 Azure 云服务（例如 Azure 存储、Azure Functions、应用服务、Azure 网络和 IOT 中心）可帮助解决以下用例：  

远程设备部署 & 管理 

Real-Time 现场分析 

智能适应性 LBE 游戏 

LBE 内容流式处理和部署 

LBE Player 首选项热度地图 

LBE 预订系统和预订系统 

**问：我要开发一个空间 MMOG 来部署大量占用空间。有助于管理内容和对象持久性的任何服务？**

答： Azure 空间锚点是一项新的混合现实服务，可实现通过 HoloLens、iOS 和 Android 设备的多用户、空间丰富的混合现实体验。 可在 [此处](https://azure.microsoft.com//services/spatial-anchors/)了解有关 Azure 空间定位点的详细信息。

**：.我们的场地专用于多玩家体验，我想将开发时间集中在内容和前端开发上。是否有可帮助我启动或卸载后端开发的产品？**

答： Azure PlayFab 是适用于现场游戏的完整后端平台。 可在 [此处](https://playfab.com/)了解详细信息。

### <a name="misc"></a>杂项

**问：我使用 SteamVR 来部署我的体验。Windows Mixed Reality 是否适用于 SteamVR？**

答： SteamVR 的 Windows Mixed Reality 允许用户在 Windows Mixed Reality 沉浸式耳机上运行 SteamVR 体验。 [在此处](/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality)了解有关 SteamVR 的详细信息。

### <a name="support-and-community"></a>支持和社区  

我们提供了一些有用的资源，可帮助你在我们的团队中与行业专家进行合作，获取故障排除支持，并为更广泛的混合现实开发社区提供帮助。  

如果遇到任何公开发布功能的问题，请使用反馈中心提交 bug。有关指南，请参阅此 [页](/windows/mixed-reality/enthusiast-guide/filing-feedback)。

有关 WMR 的其他故障排除帮助，请向我们的客户支持团队提供 [支持请求](https://support.microsoft.com//supportforbusiness/productselection?sapId=96bfb202-bc79-741b-bf7a-774d8b767782) 。

加入我们的 HoloDevelopers 时差通道，与混合现实开发人员和主题专家合作： [aka.ms/holodevelopers](https://aka.ms/holodevelopers)

Twitter：关注混合现实开发人员关系团队以获取新闻、活动和更新 @MxdRealityDev 

如果你的工作发生在旧金山或周围，则 Microsoft 反应器中始终会出现一些问题。 [此处](https://developer.microsoft.com//reactor/Location/San%20Francisco)可以看到我们的事件日历。