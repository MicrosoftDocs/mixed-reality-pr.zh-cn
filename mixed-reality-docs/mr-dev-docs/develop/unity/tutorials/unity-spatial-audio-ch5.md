---
title: 使用混响为空间音频添加距离感
description: 了解如何添加回音效果，以增强混合现实应用程序中对空间音频的距离变化方式。
author: kegodin
ms.author: v-hferrone
ms.date: 12/01/2019
ms.topic: article
keywords: mixed reality，unity，教程，hololens2，空间音频，MRTK，混合现实工具包，UWP，Windows 10，HRTF，头相关传输函数，回音，Microsoft Spatializer，音频混合器，SFX 回音
ms.openlocfilehash: 6c04ac1e4b52c7eb6104d54c184c789bec413852
ms.sourcegitcommit: 2329db5a76dfe1b844e21291dbc8ee3888ed1b81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2021
ms.locfileid: "98006357"
---
# <a name="using-reverb-to-add-distance-to-spatial-audio"></a><span data-ttu-id="03059-104">使用混响为空间音频添加距离感</span><span class="sxs-lookup"><span data-stu-id="03059-104">Using reverb to add distance to spatial audio</span></span>

## <a name="objectives"></a><span data-ttu-id="03059-105">目标</span><span class="sxs-lookup"><span data-stu-id="03059-105">Objectives</span></span>

<span data-ttu-id="03059-106">在前面的章节中，我们将 spatialization 添加到声音，使其成为一种方向。</span><span class="sxs-lookup"><span data-stu-id="03059-106">In previous chapters, we added spatialization to sounds to give them a sense of direction.</span></span> <span data-ttu-id="03059-107">在本5章节中，我们将添加一个回音效果，为声音指定距离。</span><span class="sxs-lookup"><span data-stu-id="03059-107">In this 5th chapter, we'll add a reverb effect to give sounds a sense of distance.</span></span> <span data-ttu-id="03059-108">我们的目标是：</span><span class="sxs-lookup"><span data-stu-id="03059-108">Our objectives are to:</span></span>
* <span data-ttu-id="03059-109">通过添加回音来改善声音源的感知距离</span><span class="sxs-lookup"><span data-stu-id="03059-109">Improve perceived distance of sound sources by adding reverb</span></span>
* <span data-ttu-id="03059-110">使用侦听器与全息图的距离控制声音的已知距离</span><span class="sxs-lookup"><span data-stu-id="03059-110">Control perceived distance of the sound using the listener's distance to the hologram</span></span>

## <a name="add-a-mixer-group-and-a-reverb-effect"></a><span data-ttu-id="03059-111">添加混音器组和回音效果</span><span class="sxs-lookup"><span data-stu-id="03059-111">Add a mixer group and a reverb effect</span></span>

<span data-ttu-id="03059-112">在 [第2章](unity-spatial-audio-ch2.md)，我们添加了一个混音器。</span><span class="sxs-lookup"><span data-stu-id="03059-112">In [Chapter 2](unity-spatial-audio-ch2.md), we added a mixer.</span></span> <span data-ttu-id="03059-113">混音器默认包含一个名为 **Master** 的 **组**。</span><span class="sxs-lookup"><span data-stu-id="03059-113">The mixer includes one **Group** by default called **Master**.</span></span> <span data-ttu-id="03059-114">因为我们只是想要将回音效果应用到一些声音，接下来要为这些声音添加另一个 **组** 。</span><span class="sxs-lookup"><span data-stu-id="03059-114">Because we'll only want to apply a reverb effect to some sounds, let's add a second **Group** for those sounds.</span></span> <span data-ttu-id="03059-115">若要添加 **组**，请在 **音频混合器** 中右键单击 **主控** 组，然后选择 "**添加子组**"：</span><span class="sxs-lookup"><span data-stu-id="03059-115">To add a **Group**, right click on the **Master** group in the **Audio Mixer** and choose **Add child group**:</span></span>

![添加子组](images/spatial-audio/add-child-group.png)

<span data-ttu-id="03059-117">在此示例中，我们已将新组命名为 "房间效果"。</span><span class="sxs-lookup"><span data-stu-id="03059-117">In this example, we've named the new group "Room Effect".</span></span>

<span data-ttu-id="03059-118">每个 **组** 都有自己的效果集。</span><span class="sxs-lookup"><span data-stu-id="03059-118">Each **Group** has its own set of effects.</span></span> <span data-ttu-id="03059-119">通过在新组中单击 " **添加 ...** " 并选择 " **SFX 回音**"，向新组添加回音效果：</span><span class="sxs-lookup"><span data-stu-id="03059-119">Add a reverb effect to the new group by clicking **Add...** on the new group, and choosing **SFX Reverb**:</span></span>

![添加 SFX 回音](images/spatial-audio/add-sfx-reverb.png)

<span data-ttu-id="03059-121">在音频术语中，原始、unreverberated 的音频称为 _晾干路径_，筛选后的音频被称为 _湿路径_。</span><span class="sxs-lookup"><span data-stu-id="03059-121">In audio terminology, the original, unreverberated audio is called the _dry path_, and the audio after filtering with the reverb filter is called the _wet path_.</span></span> <span data-ttu-id="03059-122">这两个路径都发送到音频输出，在此组合中，其相对强度称为 _湿/干燥混合_。</span><span class="sxs-lookup"><span data-stu-id="03059-122">Both paths are sent to the audio output, and their relative strengths in this mixture is called the _wet/dry mix_.</span></span> <span data-ttu-id="03059-123">湿/干燥混合会对距离的理解产生很大影响。</span><span class="sxs-lookup"><span data-stu-id="03059-123">The wet/dry mix strongly affects the sense of distance.</span></span>

<span data-ttu-id="03059-124">**SFX 回音** 包含用于在效果内调整湿/干燥混合的控件。</span><span class="sxs-lookup"><span data-stu-id="03059-124">The **SFX Reverb** includes controls to adjust the wet/dry mix within the effect.</span></span> <span data-ttu-id="03059-125">由于 **Microsoft Spatializer** 插件处理晾干路径，因此，我们只为湿路径使用 **SFX 回音** 。</span><span class="sxs-lookup"><span data-stu-id="03059-125">Because the **Microsoft Spatializer** plugin handles the dry path, we'll be using the **SFX Reverb** only for the wet path.</span></span> <span data-ttu-id="03059-126">在 **SFX 回音** 的 "**检查器**" 窗格上：</span><span class="sxs-lookup"><span data-stu-id="03059-126">On the **Inspector** pane of your **SFX Reverb**:</span></span>
* <span data-ttu-id="03059-127">将 "晾干级别" 属性设置为最低 (-10000 mB) </span><span class="sxs-lookup"><span data-stu-id="03059-127">Set the Dry Level property to the lowest setting (-10000 mB)</span></span>
* <span data-ttu-id="03059-128">将 "房间" 属性设置为最高 (0 mB) </span><span class="sxs-lookup"><span data-stu-id="03059-128">Set the Room property to the highest setting (0 mB)</span></span>

<span data-ttu-id="03059-129">进行这些更改后， **SFX 回音** 的 "**检查器**" 窗格将如下所示：</span><span class="sxs-lookup"><span data-stu-id="03059-129">After these changes, the **Inspector** pane of the **SFX Reverb** will look like this:</span></span>

![SFX 回音属性](images/spatial-audio/sfx-reverb-properties.png)

<span data-ttu-id="03059-131">其他设置控制模拟房间的感觉。</span><span class="sxs-lookup"><span data-stu-id="03059-131">The other settings control the feel of the simulated room.</span></span> <span data-ttu-id="03059-132">具体而言， **衰减时间** 与感知到的空间大小相关。</span><span class="sxs-lookup"><span data-stu-id="03059-132">In particular, **Decay Time** is related to perceived room size.</span></span> 

## <a name="enable-reverb-on-the-video-playback"></a><span data-ttu-id="03059-133">启用视频播放时播放回音</span><span class="sxs-lookup"><span data-stu-id="03059-133">Enable reverb on the video playback</span></span>

<span data-ttu-id="03059-134">在音频源上启用回音的步骤有两个：</span><span class="sxs-lookup"><span data-stu-id="03059-134">There are two steps to enable reverb on an audio source:</span></span>
* <span data-ttu-id="03059-135">将 **音频源** 路由到相应的 **组**</span><span class="sxs-lookup"><span data-stu-id="03059-135">Route the **Audio Source** to the appropriate **Group**</span></span>
* <span data-ttu-id="03059-136">设置 **Microsoft Spatializer** 插件以将音频传递到 **组** 进行处理</span><span class="sxs-lookup"><span data-stu-id="03059-136">Set the **Microsoft Spatializer** plugin to pass audio into the **Group** for processing</span></span>

<span data-ttu-id="03059-137">在以下步骤中，我们将调整脚本以控制音频路由，并附加 **Microsoft Spatializer** 插件提供的控制脚本，将数据送入回音。</span><span class="sxs-lookup"><span data-stu-id="03059-137">In the following steps, we'll adjust our script to control the audio routing, and attach a control script provided with the **Microsoft Spatializer** plugin to feed data into the reverb.</span></span>

<span data-ttu-id="03059-138">在 "**四核\*\*\*\*检查器**" 窗格中，单击 "**添加组件**" 并添加 "**房间效果发送级别** 脚本"：</span><span class="sxs-lookup"><span data-stu-id="03059-138">On the **Inspector** pane for the **Quad**, click **Add Component** and add the **Room Effect Send Level** script:</span></span>

![添加发送级别脚本](images/spatial-audio/add-send-level-script.png)

> [!NOTE]
> <span data-ttu-id="03059-140">除非你启用 **Microsoft Spatializer** 插件的 **会议室效果发送级别** 功能，否则它不会将任何音频发送回 Unity 音频引擎以进行有效处理。</span><span class="sxs-lookup"><span data-stu-id="03059-140">Unless you enable **Room Effect Send Level** feature of the **Microsoft Spatializer** plugin, it doesn't send any audio back to the Unity audio engine for effect processing.</span></span>

<span data-ttu-id="03059-141">" **房间效果发送级别** " 组件包括一个图形控件，该控件设置发送到 Unity 音频引擎以进行回音处理的音频级别。</span><span class="sxs-lookup"><span data-stu-id="03059-141">The **Room Effect Send Level** component includes a graph control that sets the level of the audio sent to the Unity audio engine for reverb processing.</span></span> <span data-ttu-id="03059-142">单击并向下拖动曲线，将级别设置为30dB：</span><span class="sxs-lookup"><span data-stu-id="03059-142">Click and drag the curve downwards to set the level to about -30dB:</span></span>

![调整回音曲线](images/spatial-audio/adjust-reverb-curve.png)

<span data-ttu-id="03059-144">接下来，取消注释 **SpatializeOnOff** 脚本中的4个注释行。</span><span class="sxs-lookup"><span data-stu-id="03059-144">Next, uncomment the 4 commented lines in the **SpatializeOnOff** script.</span></span> <span data-ttu-id="03059-145">该脚本现在将如下所示：</span><span class="sxs-lookup"><span data-stu-id="03059-145">The script will now look like this:</span></span>
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Audio;

[RequireComponent(typeof(AudioSource))]
public class SpatializeOnOff : MonoBehaviour
{
    public GameObject ButtonTextObject;
    public AudioMixerGroup RoomEffectGroup;
    public AudioMixerGroup MasterGroup;

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
        m_SourceObject.outputAudioMixerGroup = RoomEffectGroup;
    }

    private void SetStereo()
    {
        m_IsSpatialized = false;
        m_SourceObject.spatialBlend = 0;
        m_TextMeshPro.SetText("Set Spatialized");
        m_SourceObject.outputAudioMixerGroup = MasterGroup;
    }

}
```

<span data-ttu-id="03059-146">取消注释这些行将两个属性添加到脚本的 " **检查器** " 窗格中。</span><span class="sxs-lookup"><span data-stu-id="03059-146">Uncommenting these lines adds two properties to the **Inspector** pane for the script.</span></span> <span data-ttu-id="03059-147">若要设置这些设置，请在 Spatialize 的 "**关闭** 组件" 组件的 "**检查器**" 窗格 **中：**</span><span class="sxs-lookup"><span data-stu-id="03059-147">To set these, on the **Inspector** pane of the **Spatialize On Off** component of the **Quad**:</span></span>
* <span data-ttu-id="03059-148">将 " **房间效果组** " 属性设置为新的 "房间效果" 混音器组</span><span class="sxs-lookup"><span data-stu-id="03059-148">Set the **Room Effect Group** property to your new Room Effect mixer group</span></span>
* <span data-ttu-id="03059-149">将 " **主组** " 属性设置为 "主混音器" 组</span><span class="sxs-lookup"><span data-stu-id="03059-149">Set the **Master Group** property to the Master mixer group</span></span>

<span data-ttu-id="03059-150">完成这些更改后， **Spatialize On** 属性将如下所示：</span><span class="sxs-lookup"><span data-stu-id="03059-150">After these changes, the **Spatialize On Off** properties will look like this:</span></span>

![Spatialize 扩展](images/spatial-audio/spatialize-on-off-extended.png)

## <a name="next-steps"></a><span data-ttu-id="03059-152">后续步骤</span><span class="sxs-lookup"><span data-stu-id="03059-152">Next steps</span></span>

<span data-ttu-id="03059-153">在 HoloLens 2 上或在 Unity 编辑器中试用你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="03059-153">Try out your app on a HoloLens 2 or in the Unity editor.</span></span> <span data-ttu-id="03059-154">现在，在接触应用中的按钮以激活 spatialization 时，该脚本会将视频的音频路由到房间效果组以添加回音。</span><span class="sxs-lookup"><span data-stu-id="03059-154">Now, when touching the button in the app to activate spatialization, the script will route the video's audio to the Room Effect Group to add reverb.</span></span> <span data-ttu-id="03059-155">切换到立体声时，它会将音频路由到主组，并避免添加回音。</span><span class="sxs-lookup"><span data-stu-id="03059-155">When switching to stereo, it will route the audio to the Master group, and avoid adding reverb.</span></span>

<span data-ttu-id="03059-156">已完成适用于 Unity 的 HoloLens 2 空间音频教程。</span><span class="sxs-lookup"><span data-stu-id="03059-156">You've completed the HoloLens 2 spatial audio tutorials for Unity.</span></span> <span data-ttu-id="03059-157">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="03059-157">Congratulations!</span></span>


