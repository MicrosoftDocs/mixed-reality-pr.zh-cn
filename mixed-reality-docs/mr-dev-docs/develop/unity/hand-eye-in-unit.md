---
title: Unity 中的明确表述和眼睛跟踪
description: 您可以通过两种主要方式在 Unity、手型手势和运动控制器中执行操作。
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: 手势，运动控制器，unity，注视，输入
ms.openlocfilehash: b184cf1d9e6f35e3750015b51374058df79ed19d
ms.sourcegitcommit: 24d96bf3bb9a3143445e018195edae99d91684c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92683233"
---
# <a name="articulated-hand-and-eye-tracking-in-unity"></a>Unity 中的明确表述和眼睛跟踪

HoloLens 2 引入了一些新的令人兴奋的功能，如经过表述的手势和眼睛跟踪。

利用 Unity 中新功能的最简单方法是通过 MRTK v2。 此外，还提供了一些帮助您入门的示例场景。

* [MRTK v2 中的明确表述式入门](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/HandTracking.html)
* [MRTK v2 中的目视跟踪入门](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html)

## <a name="building-blocks-supporting-hands-eyes-and-others-in-mrtk-v2"></a>MRTK v2 中支持免提和其他的构建基块

MRTK v2 提供一组 UI 控件和构建基块，有助于加快开发速度。

|  [ ![ 按钮](images/MRTK_Button_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)[按钮](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) | [ ![ 边界框](images/MRTK_BoundingBox_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)[边界框](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) | [ ![ 操作处理程序](images/MRTK_Manipulation_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)[操作处理程序](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) |
|:--- | :--- | :--- |
| 支持各种输入法的按钮控件，包括 HoloLens2's 的有向的手写 | 用于在三维空间中操作对象的标准 UI | 用一或两次手操作对象的脚本 |
|  [ ![ 石板](images/MRTK_Slate_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html)[石板](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html) | [ ![ 系统键盘](images/MRTK_SystemKeyboard_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html)[系统键盘](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html) | [ ![ 种不可交互](images/InteractableExamples.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)[种不可交互](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html) |
| 支持用有向右输入滚动的2D 样式平面 | 在 Unity 中使用系统键盘的示例脚本  | 用于使对象种不可交互可视状态和主题支持的脚本 |
|  [ ![ 规划](images/MRTK_Solver_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)求解[求解](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) | [ ![ 对象集合](images/MRTK_ObjectCollection_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)[对象集合](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) | [ ![ 工具](images/MRTK_Tooltip_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html)提示[工具提示](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html) |
| 各种对象定位行为，如标记、正文锁定、常量视图大小和表面磁性 | 用于在三维形状中布局对象数组的脚本 | 具有灵活的定位点/透视系统的批注 UI，可用于标记运动控制器和对象。 |
|  [ ![ 应用栏](images/MRTK_AppBar_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)[应用栏](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html) | [ ![ 指针](images/MRTK_Pointer_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html)[指针](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html) | [ ![ 手指可视化](images/MRTK_FingertipVisualization_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html)[手指可视化](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html) |
| 边界框手动激活的 UI | 了解各种类型的指针 | 手指上的视觉对象 affordance，提高了直接交互的置信度 |
|  [ ![ 目视跟踪：目标选择](images/mrtk_et_targetselect.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html)[目视跟踪：目标选择](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) | [ ![ 目视跟踪：导航](images/mrtk_et_navigation.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html)[目视跟踪：导航](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html) | [ ![ 目视跟踪：热度地图](images/mrtk_et_heatmaps.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html)[眼睛跟踪：热度地图](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html) |
| 将眼睛、语音和手写输入与您的场景一起快速轻松地选择全息影像 | 了解如何根据要查看的内容自动滚动文本或流畅地缩放到聚焦内容| 记录、加载和可视化用户在应用中查看的内容的示例 |

## <a name="example-scenes"></a>示例场景

在 [此示例场景](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandInteractionExamples.html)中，探索 MRTK 的各种交互类型和 UI 控件。

可以在 " **资产/MixedRealityToolkit** " 下的 [混合现实工具包 GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity)中找到其他示例场景。

[![示例场景](images/MRTK_Examples.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandInteractionExamples.html)

## <a name="next-development-checkpoint"></a>下一个开发检查点

如果遵循我们规划的 Unity 的开发检查点旅程，则你在探索 MRTK 核心构建基块的过程中。 从这里，你可以进入下一个构建基块：

> [!div class="nextstepaction"]
> [空间映射](spatial-mapping-in-unity.md)

或跳转到混合现实平台功能和 API：

> [!div class="nextstepaction"]
> [共享体验](shared-experiences-in-unity.md)

你可以随时返回到 [Unity 开发检查点](unity-development-overview.md#2-core-building-blocks)。

## <a name="see-also"></a>另请参阅

* [基于眼睛的交互](../../design/eye-gaze-interaction.md)
* [HoloLens 2 中的眼动跟踪](../../design/eye-tracking.md)
* [凝视和提交](../../design/gaze-and-commit.md)
* [手 - 直接操作](../../design/direct-manipulation.md)
* [手 - 手势](../../design/gaze-and-commit.md#composite-gestures)
* [手 - 指向并提交](../../design/point-and-commit.md)
* [本能交互](../../design/interaction-fundamentals.md)
* [运动控制器](../../design/motion-controllers.md)
* [UnityEngine. XR](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [UnityEngine. XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
