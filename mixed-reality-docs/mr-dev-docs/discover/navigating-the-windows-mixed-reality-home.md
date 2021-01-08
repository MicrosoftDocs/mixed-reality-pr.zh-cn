---
title: 导航 Windows Mixed Reality 主页
description: 了解如何在 HoloLens 和 Windows Mixed Reality 耳机上导航 Windows Mixed Reality 主页。
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: shell，os，平台，cliff 房子，房子，home，环境，开始，开始菜单，主页菜单，pin，应用，启动应用，放置应用，传送，移动，导航，混合现实耳机，虚拟现实耳机，什么是虚拟现实
ms.openlocfilehash: 06e28c9c1f0f6244f7f502382d61d4740b5fb71f
ms.sourcegitcommit: 2329db5a76dfe1b844e21291dbc8ee3888ed1b81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2021
ms.locfileid: "98009687"
---
# <a name="navigating-the-windows-mixed-reality-home"></a>导航 Windows Mixed Reality 主页

正如 Windows PC 体验从桌面开始一样，Windows Mixed Reality 从家里开始。 Windows Mixed Reality 主页使用我们的原始功能来理解并浏览三维位置。 使用 HoloLens，你的家庭是物理空间，但使用沉浸式耳机，你的家庭是一个虚拟位置。

你还可以使用 "开始" 菜单打开和放置应用和内容。 您可以使用混合现实内容和多个应用程序同时使用多个应用程序。 即使您重新启动设备，您在家庭中放置的东西也会保留在那里。

## <a name="start-menu"></a>“开始”菜单

![Microsoft HoloLens 上的 "开始" 菜单](images/start-500px.png)

"开始" 菜单包括：
* 系统信息 (网络状态、电池百分比、当前时间和音量) 
* 沉浸式耳机上 Cortana (，开始磁贴;在 HoloLens 上，在 "开始) 
* 固定应用
* "所有应用" 按钮 (加号) 
* [混合现实捕获](../mixed-reality-capture.md)的照片和视频按钮

通过选择加号或减号按钮，在固定应用程序和所有应用程序视图之间切换。 若要在 HoloLens 上打开 "开始" 菜单，请使用布隆手势。 在沉浸式耳机上，按下控制器上的 Windows 按钮。

## <a name="launching-apps"></a>正在启动应用

若要启动应用，请在 "开始" 上选择它。 "开始" 菜单将消失，应用将在放置模式下打开，如2D 窗口或 [3d 模型](../distribute/implementing-3d-app-launchers.md)。

若要运行该应用，你需要将其放在家里：
1. 使用 [注视](../design/gaze-and-commit.md) 或控制器将应用定位到所需的位置。 它将自动调整 (大小和位置) 以符合放置它的空间。
2. 使用 "air" (HoloLens) 或 "选择" 按钮 (沉浸式耳机) 来放置应用。 若要取消并返回 "开始" 菜单，请使用布隆手势或 Windows 按钮。

可以使用[HOLOGRAPHICSPACE API](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx)将为桌面、移动或 Xbox 创建的[2d 应用](../develop/porting-apps/building-2d-apps.md)修改为作为混合现实沉浸式应用运行。 沉浸式应用使用户离开家里，并进入沉浸式体验。 用户可以使用布隆手势 (HoloLens) 或按其控制器上的 Windows 按钮 (沉浸式耳机) 来返回 home。

还可以通过应用程序到应用程序 API 或通过 Cortana 来启动应用。

![Windows Mixed Reality 主页中的应用](images/mixed-reality-home-500px.png)

## <a name="moving-and-adjusting-apps"></a>移动和调整应用

选择应用栏上的 " **调整** " 以显示移动、缩放和旋转混合现实内容的控件。 完成后，请选择 " **完成**"。

![调整模式下的商店石板 (蓝帧) 。 请注意，应用栏 (顶部) 已更改为包含 "完成" 和 "删除" 按钮。](images/adjust-500px.png)

不同的应用程序可能在应用栏上具有其他选项。 例如，Microsoft Edge 具有 *滚动*、 *拖动* 和 *缩放* 选项。 

![在 HoloLens 上运行的2D 应用的应用栏](images/holobar-500px.png)

" **后退** " 按钮导航回到应用中以前查看过的屏幕。 当你到达应用程序中显示的体验的开头时，它将停止，并且不会导航到其他应用。

## <a name="getting-around-your-home"></a>围绕你的家庭

使用 **HoloLens**，可以在物理空间间移动，在家里移动。

使用 **沉浸式耳机**，你可以在 playspace 中找到并四处浏览，在虚拟世界中的类似区域内移动。 若要在更远的距离间移动，请使用控制器上的操纵杆来几乎 "走到"，或者可以使用 *teleportation* 立即跳转到更长的距离。

![Windows Mixed Reality 主页中的 Teleportation](images/teleportation-500px.png)

**若要传送：**
1. 打开 teleportation reticle。
   * 使用 [运动控制器](../design/motion-controllers.md)：向前按操纵杆并将其放在该位置。
   * 使用 Xbox 控制器：向前按左操纵杆，并将其放在该位置。
   * 使用鼠标：按住右键单击鼠标按钮 (，并在传送) 时使用滚轮来旋转要面对的方向。
2. 将 reticle 放在要传送的位置。
   * 使用 [运动控制器](../design/motion-controllers.md)：倾斜要使操纵杆前进的控制器 () 移动 reticle。
   * 使用 Xbox 控制器：使用 [注视](../design/gaze-and-commit.md) 移动 reticle。
   * 使用鼠标：移动鼠标移动 reticle。
3. 释放按钮以传送 reticle 的位置。

**到真正的 "行走："**
* 使用 [运动控制器](../design/motion-controllers.md)：单击操纵杆并按下，并在要 "走进" 方向上移动操纵杆。
* 使用 Xbox 控制器：单击左侧操纵杆并按下，并在要 "走" 方向上移动操纵杆。

## <a name="immersive-headset-input-support"></a>沉浸式耳机输入支持

[Windows Mixed reality 沉浸式耳机](immersive-headset-hardware-details.md) 支持用于导航 Windows Mixed reality 主页的多种输入类型。 HoloLens 不支持用于导航的附件输入，因为你会以物理方式浏览并查看你的环境。 但是，HoloLens 支持与应用进行交互的 [输入](hardware-accessories.md) 。

### <a name="motion-controllers"></a>运动控制器

最佳的 Windows Mixed reality 体验将使用 Windows Mixed Reality [运动控制器](../design/motion-controllers.md) ，该控制器仅使用耳机中的传感器支持六个自由度跟踪-无需外部照相机或标记！

即将推出导航命令。

### <a name="gamepad"></a>游戏板
* **左操纵杆：**
  * 按住左操纵杆，使 [teleportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) reticle。
  * 向左、向右或向后移动操纵杆，以较小的增量向左、向右或向后移动。
  * 单击左侧操纵杆并按下，并按所需的方式移动操纵杆，使其以[实际](navigating-the-windows-mixed-reality-home.md#getting-around-your-home)的方向移动。
* 向左或向右点击 **右操纵杆** ，以将你的方向旋转45度。
* 按下 **按钮时，将选择** 并像 [单击 "轻敲](../design/gaze-and-commit.md#composite-gestures) " 手势。
* 按 " **指南** " 按钮将显示 " [开始" 菜单](navigating-the-windows-mixed-reality-home.md#start-menu) ，并类似于 " [布隆](../design/system-gesture.md#bloom) " 手势。
* 按 **左和右触发器** 可以放大和缩小要在家里交互的2d 桌面应用程序。

### <a name="keyboard-and-mouse"></a>键盘和鼠标

**注意：** 使用 **Windows 键 + Y** 在控制 PC 桌面和 Windows Mixed Reality 主页之间切换鼠标。

在 Windows Mixed Reality 主页中：
* 按住鼠标 **左键** 并按下鼠标按钮进行选择，并将其作用与 " [空中点击](../design/gaze-and-commit.md#composite-gestures) " 笔势类似。
* 按住 **右键单击** 鼠标按钮将打开 [teleportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) reticle。
* 按键盘上的 **Windows** 键打开 "开始" [菜单](navigating-the-windows-mixed-reality-home.md#start-menu) ，并与 [布隆](../design/system-gesture.md#bloom) 手势类似。
* 当 [gazing](../design/gaze-and-commit.md) 在2d 桌面应用中时，可以 **单击** 以选择， **右键单击** 以打开上下文菜单，然后 **使用滚轮滚动** (就像在 PC 桌面上) 。

## <a name="cortana"></a>Cortana

[Cortana](../design/voice-input.md#hey-cortana) 是 Windows Mixed Reality 的个人助手，就像在电脑和手机上一样。 HoloLens 有内置麦克风，但沉浸式耳机可能需要额外的硬件。 使用 Cortana 打开应用、重新启动设备、联机查找设备等。 开发人员也可以选择将 [Cortana 集成](https://dev.windows.com/cortana) 到其体验中。

你还可以使用语音命令来浏览你的主页。 例如，使用 " [注视](../design/gaze-and-commit.md) " 或 "控制器" (按钮，具体取决于设备) 并说 "选择"。 其他语音命令包括 "转到主页"、"放大"、"较小"、"关闭" 和 "面部我"。

## <a name="store-settings-and-system-apps"></a>存储、设置和系统应用

Windows Mixed Reality 包含多个内置应用，例如：
* **Microsoft Store** 获取应用和游戏
* 提交有关系统和系统应用的反馈的 **反馈中心**
* 用于配置系统设置的 **设置** ([包括网络](../connecting-to-wi-fi-on-hololens.md)和系统更新) 
* **Microsoft Edge** 浏览网站
* 查看并共享照片和视频的 **照片**
* **校准** (仅限 hololens) 用于调整当前用户的 hololens 体验
* **了解** (HoloLens) 手势或 **了解混合现实** (沉浸式耳机) 以了解如何使用你的设备
* **三维查看器** ，可在全球范围内装饰混合现实内容
* **混合现实门户** (桌面) 设置和管理沉浸式耳机，并流式传输耳机中视图的实时预览，供其他人查看。
* 观看360视频和最新电影和电视节目的 **电影和电视** 节目
* 所有虚拟助手需求的 **Cortana**
* **桌面** (沉浸式耳机) 用于在沉浸式耳机中查看桌面监视器
* **文件资源管理器** 访问设备上的文件和文件夹

## <a name="see-also"></a>另请参阅
* [应用视图](../design/app-views.md)
* [运动控制器](../design/motion-controllers.md)
* [硬件配件](hardware-accessories.md)
* [HoloLens 的环境注意事项](../environment-considerations-for-hololens.md)
* [实现 3D 应用启动器](../distribute/implementing-3d-app-launchers.md)
* [创建用于 Windows Mixed Reality 主页的3D 模型](../distribute/creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
