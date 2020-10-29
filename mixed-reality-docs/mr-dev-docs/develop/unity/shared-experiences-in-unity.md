---
title: Unity 中的共享体验
description: 在 Unity 应用程序的多个用户之间共享相同的全息影像。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: 共享、定位、WorldAnchor、MR 共享250、WorldAnchorTransferBatch、SpatialPerception、Azure、Azure 空间锚，ASA
ms.openlocfilehash: 324aecdc89b4996625ce93514616c32d2d064ffa
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91677332"
---
# <a name="shared-experiences-in-unity"></a>Unity 中的共享体验

共享体验是指多个用户，每个用户都有自己的 HoloLens、iOS 或 Android 设备，共同查看位于某个空间固定点的同一全息图并与之进行交互。 这是通过空间定位点共享来实现的。

## <a name="azure-spatial-anchors"></a>Azure 空间定位点

你可以使用 <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空间锚点</a> 来创建支持云的持久空间锚点，你的应用可以在多个 HoloLens、IOS 和 Android 设备上查找。  通过在多个设备之间共享公用空间定位点，每个用户都可以查看相对于同一物理位置中的定位点呈现的内容。  这可实现实时共享体验。

还可以使用 <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空间定位点</a>在 HoloLens、iOS 和 Android 设备上实现异步全息影像持久性。  通过共享持久的云空间定位点，多个设备可以随着时间推移观察相同的持久全息影像，即使这些设备没有同时出现，也是如此。

若要开始在 Unity 中构建共享体验，请尝试执行5分钟的 <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure 空间锚点 Unity 快速入门</a>。

启动并运行 Azure 空间锚点后，便可以 <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">在 Unity 中创建和定位锚</a>。

## <a name="local-anchor-transfers"></a>本地定位点传输

在不能使用 Azure 空间锚点的情况下， [本地定位点传输](../../out-of-scope/local-anchor-transfers-in-unity.md) 允许一台 hololens 设备导出要由第二个 hololens 设备导入的定位点。  请注意，此方法提供的定位回调比 Azure 空间定位点更少，并且不支持 iOS 和 Android 设备。

## <a name="next-development-checkpoint"></a>下一个开发检查点

如果遵循我们所说的 Unity 开发检查点旅程，就是探索混合现实平台功能和 Api。 在这里，你可以继续学习下一主题：

> [!div class="nextstepaction"]
> [可定位相机](locatable-camera-in-unity.md)

或直接跳到在设备或模拟器上部署应用：

> [!div class="nextstepaction"]
> [部署到 HoloLens 或 Windows Mixed Reality 沉浸式耳机](../platform-capabilities-and-apis/using-visual-studio.md)

随时可以随时返回到 [Unity 开发检查点](unity-development-overview.md#3-platform-capabilities-and-apis) 。

## <a name="see-also"></a>请参阅
* [混合现实中的共享体验](../platform-capabilities-and-apis/shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure 空间定位点</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">用于 Unity 的 Azure 空间定位点 SDK</a>
