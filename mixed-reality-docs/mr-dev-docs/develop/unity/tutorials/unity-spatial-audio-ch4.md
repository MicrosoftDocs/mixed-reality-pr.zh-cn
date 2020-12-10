---
title: 空间音频教程-4。 在运行时启用和禁用空间音频
description: 使用按钮来启用和禁用运行时音频的 spatialization。
author: kegodin
ms.author: v-hferrone
ms.date: 12/01/2019
ms.topic: article
keywords: mixed reality，unity，教程，hololens2，空间音频，MRTK，混合现实工具包，UWP，Windows 10，HRTF，head 相关传输函数，回音，Microsoft Spatializer
ms.openlocfilehash: c9e510e544962c5d1a4c462d20dafa222c6a5289
ms.sourcegitcommit: fbeff51cae92add88d2b960c9b7bbfb04d5a0291
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97002602"
---
# <a name="enabling-and-disabling-spatialization-at-run-time"></a><span data-ttu-id="f34b6-105">在运行时启用和禁用 spatialization</span><span class="sxs-lookup"><span data-stu-id="f34b6-105">Enabling and disabling spatialization at run time</span></span>

## <a name="objectives"></a><span data-ttu-id="f34b6-106">目标</span><span class="sxs-lookup"><span data-stu-id="f34b6-106">Objectives</span></span>
<span data-ttu-id="f34b6-107">在此第4章中，你将：</span><span class="sxs-lookup"><span data-stu-id="f34b6-107">In this 4th chapter, you'll:</span></span>
* <span data-ttu-id="f34b6-108">添加新脚本以控制游戏对象上的 spatialization</span><span class="sxs-lookup"><span data-stu-id="f34b6-108">Add a new script to control spatialization on a game object</span></span>
* <span data-ttu-id="f34b6-109">从按钮操作驱动 spatialization 控件脚本</span><span class="sxs-lookup"><span data-stu-id="f34b6-109">Drive the spatialization control script from button actions</span></span>

## <a name="add-spatialization-control-script"></a><span data-ttu-id="f34b6-110">添加 spatialization 控件脚本</span><span class="sxs-lookup"><span data-stu-id="f34b6-110">Add spatialization control script</span></span>
<span data-ttu-id="f34b6-111">右键单击 " **项目** " 窗格，然后通过选择 " **> c # 脚本** 创建新的 c # 脚本"。</span><span class="sxs-lookup"><span data-stu-id="f34b6-111">Right-click in the **Project** pane and create a new C# script by choosing **Create -> C# Script**.</span></span> <span data-ttu-id="f34b6-112">将脚本命名为 "SpatializeOnOff"。</span><span class="sxs-lookup"><span data-stu-id="f34b6-112">Name your script "SpatializeOnOff".</span></span>

![创建脚本](images/spatial-audio/create-script.png)

<span data-ttu-id="f34b6-114">双击 " **项目** " 窗格中的脚本，在 Visual Studio 中将其打开。</span><span class="sxs-lookup"><span data-stu-id="f34b6-114">Double-click the script in the **Project** pane to open it in Visual Studio.</span></span> <span data-ttu-id="f34b6-115">将默认脚本内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="f34b6-115">Replace the default script contents with the following:</span></span>

> [!NOTE]
> <span data-ttu-id="f34b6-116">脚本的几行被注释掉。 [第5章](unity-spatial-audio-ch5.md)将取消注释这些行。</span><span class="sxs-lookup"><span data-stu-id="f34b6-116">Several lines of the script are commented out. These lines will be uncommented in [Chapter 5](unity-spatial-audio-ch5.md).</span></span>

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Audio;

[RequireComponent(typeof(AudioSource))]
public class SpatializeOnOff : MonoBehaviour
{
    public GameObject ButtonTextObject;
    //public AudioMixerGroup RoomEffectGroup;
    //public AudioMixerGroup MasterGroup;

    private AudioSource m_SourceObject;
    private bool m_IsSpatialized;
    private TMPro.TextMeshPro m_TextMeshPro;

    public void Start()
    {
        m_SourceObject = gameObject.GetComponent<AudioSource>();
        m_TextMeshPro = ButtonTextObject.GetComponent<TMPro.TextMeshPro>();
        SetSpatialized();
    }

    public void SwapSpatialization()
    {
        if (m_IsSpatialized)
        {
            SetStereo();
        }
        else
        {
            SetSpatialized();
        }
    }

    private void SetSpatialized()
    {
        m_IsSpatialized = true;
        m_SourceObject.spatialBlend = 1;
        m_TextMeshPro.SetText("Set Stereo");
        //m_SourceObject.outputAudioMixerGroup = RoomEffectGroup;
    }

    private void SetStereo()
    {
        m_IsSpatialized = false;
        m_SourceObject.spatialBlend = 0;
        m_TextMeshPro.SetText("Set Spatialized");
        //m_SourceObject.outputAudioMixerGroup = MasterGroup;
    }

}
```

> [!NOTE]
> <span data-ttu-id="f34b6-117">若要启用或禁用 spatialization，此脚本只会调整 **spatialBlend** 属性，使 **spatialization** 属性保持启用状态。</span><span class="sxs-lookup"><span data-stu-id="f34b6-117">To enable or disable spatialization, the script only adjusts the **spatialBlend** property, leaving the **spatialization** property enabled.</span></span> <span data-ttu-id="f34b6-118">在此模式下，Unity 仍会应用 **卷** 曲线。</span><span class="sxs-lookup"><span data-stu-id="f34b6-118">In this mode, Unity still applies the **Volume** curve.</span></span> <span data-ttu-id="f34b6-119">否则，如果用户在远距离源时禁用了 spatialization，则会听到音量突然增加。</span><span class="sxs-lookup"><span data-stu-id="f34b6-119">Otherwise, if the user were to disable spatialization when far from the source, they would hear the volume increase abruptly.</span></span> <br> <br>
> <span data-ttu-id="f34b6-120">如果希望完全禁用 spatialization，请修改脚本，同时调整 **SourceObject** 变量的 **spatialization** 布尔值属性。</span><span class="sxs-lookup"><span data-stu-id="f34b6-120">If you prefer to fully disable spatialization, modify the script to also adjust the **spatialization** boolean property of the **SourceObject** variable.</span></span>

## <a name="attach-your-script-and-drive-it-from-the-button"></a><span data-ttu-id="f34b6-121">附加脚本，然后从按钮中进行驱动器</span><span class="sxs-lookup"><span data-stu-id="f34b6-121">Attach your script and drive it from the button</span></span>
<span data-ttu-id="f34b6-122">在 **四** 个 "**检查器**" 窗格中，单击 "**添加组件**" 并添加 **Spatialize On** script：</span><span class="sxs-lookup"><span data-stu-id="f34b6-122">On the **Inspector** pane of the **Quad**, click **Add Component** and add the **Spatialize On Off** script:</span></span>

![将脚本添加到四个](images/spatial-audio/add-script-to-quad.png)

<span data-ttu-id="f34b6-124">在四个 **Spatialize** 的 **故障** 组件上：</span><span class="sxs-lookup"><span data-stu-id="f34b6-124">On the **Spatialize On Off** component of the **Quad**:</span></span>
1. <span data-ttu-id="f34b6-125">在 **层次结构** 中查找 **PressableButtonHoloLens2-> IconAndText-> TextMeshPro** 使用者：</span><span class="sxs-lookup"><span data-stu-id="f34b6-125">Find the **PressableButtonHoloLens2 -> IconAndText -> TextMeshPro** subject in the **Hierarchy**:</span></span>

![在层次结构中查找 PressableButtonHoloLens2 对象](images/spatial-audio/pressable-button-object.png)

2. <span data-ttu-id="f34b6-127">将 **TextMeshPro** subject 拖到 **Spatialize On Off** 组件的 **ButtonTextObject** 字段上</span><span class="sxs-lookup"><span data-stu-id="f34b6-127">Drag the **TextMeshPro** subject onto the **ButtonTextObject** field of the **Spatialize On Off** component</span></span>

<span data-ttu-id="f34b6-128">进行这些更改后，四个 **Spatialize** 组件的 **故障** 组件如下所示：</span><span class="sxs-lookup"><span data-stu-id="f34b6-128">After these changes, the **Spatialize On Off** component of the **Quad** will look like this:</span></span>

![Spatialize on basic](images/spatial-audio/spatialize-on-off-basic.png)

<span data-ttu-id="f34b6-130">若要将按钮设置为在释放按钮时调用 **Spatialize On On** 脚本，请打开 **PressableButtonHoloLens2** 对象的 **检查器** 窗格，查找 **种不可交互** 组件，并执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f34b6-130">To set the button to call the **Spatialize On Off** script when the button is released, open the **Inspector** pane of the **PressableButtonHoloLens2** object, find the **Interactable** component, and:</span></span>
1. <span data-ttu-id="f34b6-131">查找 "**事件**" 子节 **( # B1** 区域的 OnClick</span><span class="sxs-lookup"><span data-stu-id="f34b6-131">Find the **OnClick ()** region of the **Events** subsection</span></span>
2. <span data-ttu-id="f34b6-132">将 **四** 个部分从 **层次结构** 拖至目标对象槽。</span><span class="sxs-lookup"><span data-stu-id="f34b6-132">Drag the **Quad** from the **Hierarchy** into the target object slot.</span></span>
3. <span data-ttu-id="f34b6-133">从 "操作" 下拉框中选择 " **SpatializeOnOff"。**</span><span class="sxs-lookup"><span data-stu-id="f34b6-133">Select **SpatializeOnOff.SwapSpatialization** from the action drop-down box.</span></span>

<span data-ttu-id="f34b6-134">进行这些更改之后， **种不可交互** 组件将如下所示：</span><span class="sxs-lookup"><span data-stu-id="f34b6-134">After these changes, the **Interactable** component will look like this:</span></span>

![按钮操作设置](images/spatial-audio/button-action-settings.png)

## <a name="next-steps"></a><span data-ttu-id="f34b6-136">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f34b6-136">Next steps</span></span>
<span data-ttu-id="f34b6-137">在 HoloLens 2 上或在 Unity 编辑器中试用你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f34b6-137">Try out your app on a HoloLens 2 or in the Unity editor.</span></span> <span data-ttu-id="f34b6-138">在应用程序中，你现在可以触摸按钮以激活和停用视频上的 spatialization。</span><span class="sxs-lookup"><span data-stu-id="f34b6-138">In the app, you can now touch the button to activate and deactivate spatialization on the video.</span></span> <span data-ttu-id="f34b6-139">在 Unity 编辑器中测试时，按空格键并滚动鼠标滚轮以激活手动模拟。</span><span class="sxs-lookup"><span data-stu-id="f34b6-139">When testing in the Unity editor, press the space bar and scroll with the scroll wheel to activate hand simulation.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f34b6-140">第5章</span><span class="sxs-lookup"><span data-stu-id="f34b6-140">Chapter 5</span></span>](unity-spatial-audio-ch5.md) 

