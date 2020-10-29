---
title: Unity 的输入移植指南
description: 了解如何在 Unity 中处理 Windows Mixed Reality 的输入。
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: 输入、unity、移植
ms.openlocfilehash: 4ad4b66b8238b3d00142fd14161113c6b912641c
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91676966"
---
# <a name="input-porting-guide-for-unity"></a><span data-ttu-id="7299f-104">Unity 的输入移植指南</span><span class="sxs-lookup"><span data-stu-id="7299f-104">Input porting guide for Unity</span></span>

<span data-ttu-id="7299f-105">你可以使用以下两种方法之一将输入逻辑移植到 Windows Mixed Reality： Unity 的一般输入. GetButton/GetAxis Api，跨越多个平台或特定于 Windows 的 XR。WSA.输入 Api，专门为运动控制器和 HoloLens 提供更丰富的数据。</span><span class="sxs-lookup"><span data-stu-id="7299f-105">You can port your input logic to Windows Mixed Reality using one of two approaches, Unity's general Input.GetButton/GetAxis APIs that span across multiple platforms, or the Windows-specific XR.WSA.Input APIs that offer richer data specifically for motion controllers and HoloLens hands.</span></span>

## <a name="general-inputgetbuttongetaxis-apis"></a><span data-ttu-id="7299f-106">General GetButton/GetAxis Api</span><span class="sxs-lookup"><span data-stu-id="7299f-106">General Input.GetButton/GetAxis APIs</span></span>

<span data-ttu-id="7299f-107">Unity 目前使用其常规输入. GetButton/GetAxis Api 来公开 [OCULUS SDK](https://docs.unity3d.com/Manual/OculusControllers.html) 和 [OpenVR SDK](https://docs.unity3d.com/Manual/OpenVRControllers.html)的输入。</span><span class="sxs-lookup"><span data-stu-id="7299f-107">Unity currently uses its general Input.GetButton/Input.GetAxis APIs to expose input for [the Oculus SDK](https://docs.unity3d.com/Manual/OculusControllers.html) and [the OpenVR SDK](https://docs.unity3d.com/Manual/OpenVRControllers.html).</span></span> <span data-ttu-id="7299f-108">如果你的应用程序已在使用这些 Api 进行输入，则这是在 Windows Mixed Reality 中支持运动控制器的最简单途径：只需重新映射输入管理器中的按钮和轴即可。</span><span class="sxs-lookup"><span data-stu-id="7299f-108">If your apps are already using these APIs for input, this is the easiest path for supporting motion controllers in Windows Mixed Reality: you should just need to remap buttons and axes in the Input Manager.</span></span>

<span data-ttu-id="7299f-109">有关详细信息，请参阅 [Unity 按钮/轴映射表](../unity/gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table) 和 [常见 Unity api 的概述](../unity/gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis)。</span><span class="sxs-lookup"><span data-stu-id="7299f-109">For more information, see the [Unity button/axis mapping table](../unity/gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table) and the [overview of the common Unity APIs](../unity/gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis).</span></span>

## <a name="windows-specific-xrwsainput-apis"></a><span data-ttu-id="7299f-110">Windows 特定的 XR。WSA.输入 Api</span><span class="sxs-lookup"><span data-stu-id="7299f-110">Windows-specific XR.WSA.Input APIs</span></span>

<span data-ttu-id="7299f-111">如果应用已为每个平台构建自定义输入逻辑，则可以选择在 **UnityEngine** 命名空间下使用特定于 Windows 的空间输入 api。</span><span class="sxs-lookup"><span data-stu-id="7299f-111">If your app already builds custom input logic for each platform, you can choose to use the Windows-specific spatial input APIs under the **UnityEngine.XR.WSA.Input** namespace.</span></span> <span data-ttu-id="7299f-112">这样，你就可以访问其他信息（如位置准确性或源类型），从而让你能够在 HoloLens 上区分双手和控制器。</span><span class="sxs-lookup"><span data-stu-id="7299f-112">This lets you access additional information, such as position accuracy or the source kind, letting you tell hands and controllers apart on HoloLens.</span></span>

<span data-ttu-id="7299f-113">有关详细信息，请参阅 [UNITYENGINE XR api 概述](../unity/gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xrwsainput)。</span><span class="sxs-lookup"><span data-stu-id="7299f-113">For more information, see the [overview of the UnityEngine.XR.WSA.Input APIs](../unity/gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xrwsainput).</span></span>

## <a name="grip-pose-vs-pointing-pose"></a><span data-ttu-id="7299f-114">手柄姿势与指针姿势</span><span class="sxs-lookup"><span data-stu-id="7299f-114">Grip pose vs. pointing pose</span></span>

<span data-ttu-id="7299f-115">Windows Mixed Reality 支持各种外形规格的运动控制器，其中每个控制器的设计在用户的手位置与应用程序在呈现控制器时应使用的自然 "前进" 方向不同。</span><span class="sxs-lookup"><span data-stu-id="7299f-115">Windows Mixed Reality supports motion controllers in a variety of form factors, with each controller's design differing in its relationship between the user's hand position and the natural "forward" direction that apps should use for pointing when rendering the controller.</span></span>

<span data-ttu-id="7299f-116">为了更好地表示这些控制器，可以针对每个交互源调查以下两种类型：</span><span class="sxs-lookup"><span data-stu-id="7299f-116">To better represent these controllers, there are two kinds of poses you can investigate for each interaction source:</span></span>

* <span data-ttu-id="7299f-117">**手柄姿势** ，表示由 HoloLens 检测到的掌托的位置，或包含运动控制器的掌托的位置。</span><span class="sxs-lookup"><span data-stu-id="7299f-117">The **grip pose** , representing the location of either the palm of a hand detected by a HoloLens, or the palm holding a motion controller.</span></span>
    * <span data-ttu-id="7299f-118">在沉浸式耳机上，这种姿势最适合用于呈现 **用户的手** 或 **持有用户的对象** ，例如剑或机枪。</span><span class="sxs-lookup"><span data-stu-id="7299f-118">On immersive headsets, this pose is best used to render **the user's hand** or **an object held in the user's hand** , such as a sword or gun.</span></span>
    * <span data-ttu-id="7299f-119">**手柄位置** ：在固定控制器时，掌上质心，向左或向右调整以使其在手柄内居中。</span><span class="sxs-lookup"><span data-stu-id="7299f-119">The **grip position** : The palm centroid when holding the controller naturally, adjusted left or right to center the position within the grip.</span></span>
    * <span data-ttu-id="7299f-120">**手柄方向的右轴** ：当你完全打开手形成一个平面的5指形姿势时，与你的掌上的光线 (从右手掌向后) </span><span class="sxs-lookup"><span data-stu-id="7299f-120">The **grip orientation's Right axis** : When you completely open your hand to form a flat 5-finger pose, the ray that is normal to your palm (forward from left palm, backward from right palm)</span></span>
    * <span data-ttu-id="7299f-121">**手柄方向的正向轴** ：当您关闭手中的部分 (时，就如同按住控制器) 一样，通过您的非拇指形来表示 "转发" 的射线。</span><span class="sxs-lookup"><span data-stu-id="7299f-121">The **grip orientation's Forward axis** : When you close your hand partially (as if holding the controller), the ray that points "forward" through the tube formed by your non-thumb fingers.</span></span>
    * <span data-ttu-id="7299f-122">**手柄方向的上轴** ：向右和向后定义隐含的上轴。</span><span class="sxs-lookup"><span data-stu-id="7299f-122">The **grip orientation's Up axis** : The Up axis implied by the Right and Forward definitions.</span></span>
    * <span data-ttu-id="7299f-123">可以通过 Unity 的跨供应商输入 API (XR 来访问抓握姿势 **[。InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)。GetLocalPosition/旋转** ) 或通过特定于 Windows 的 API ( **sourcePose TryGetPosition/旋转** ，) 请求手柄姿势。</span><span class="sxs-lookup"><span data-stu-id="7299f-123">You can access the grip pose through either Unity's cross-vendor input API ( **[XR.InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html).GetLocalPosition/Rotation** ) or through the Windows-specific API ( **sourceState.sourcePose.TryGetPosition/Rotation** , requesting the Grip pose).</span></span>
* <span data-ttu-id="7299f-124">**指针姿势** ，表示控制器的末端。</span><span class="sxs-lookup"><span data-stu-id="7299f-124">The **pointer pose** , representing the tip of the controller pointing forward.</span></span>
    * <span data-ttu-id="7299f-125">这种姿势最适用于在呈现控制器模型本身时 **指向 UI** 时进行 raycast。</span><span class="sxs-lookup"><span data-stu-id="7299f-125">This pose is best used to raycast when **pointing at UI** when you are rendering the controller model itself.</span></span>
    * <span data-ttu-id="7299f-126">目前，指针姿势仅可通过特定于 Windows 的 API ( **TryGetPosition/旋转** ，请求指针) 。</span><span class="sxs-lookup"><span data-stu-id="7299f-126">Currently, the pointer pose is available only through the Windows-specific API ( **sourceState.sourcePose.TryGetPosition/Rotation** , requesting the Pointer pose).</span></span>

<span data-ttu-id="7299f-127">这些姿势坐标全部用 Unity 世界坐标表示。</span><span class="sxs-lookup"><span data-stu-id="7299f-127">These pose coordinates are all expressed in Unity world coordinates.</span></span>

## <a name="see-also"></a><span data-ttu-id="7299f-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="7299f-128">See also</span></span>
* <span data-ttu-id="7299f-129">[运动控制器]().。。/../design/motion-controllers.md) </span><span class="sxs-lookup"><span data-stu-id="7299f-129">[Motion controllers]()../../design/motion-controllers.md)</span></span>
* [<span data-ttu-id="7299f-130">Unity 中的手势和运动控制器</span><span class="sxs-lookup"><span data-stu-id="7299f-130">Gestures and motion controllers in Unity</span></span>](../unity/gestures-and-motion-controllers-in-unity.md)
* [<span data-ttu-id="7299f-131">UnityEngine. XR</span><span class="sxs-lookup"><span data-stu-id="7299f-131">UnityEngine.XR.WSA.Input</span></span>](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [<span data-ttu-id="7299f-132">UnityEngine. XR. InputTracking</span><span class="sxs-lookup"><span data-stu-id="7299f-132">UnityEngine.XR.InputTracking</span></span>](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
* [<span data-ttu-id="7299f-133">移植指南</span><span class="sxs-lookup"><span data-stu-id="7299f-133">Porting guides</span></span>](porting-guides.md)
