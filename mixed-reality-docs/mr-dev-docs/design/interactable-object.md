---
title: 可交互对象
description: "\"Button\" 是一种用于在二维抽象环境中触发事件的比喻。 在这三维混合现实世界中，我们不必再局限于这种抽象领域。"
author: cre8ivepark
ms.author: v-hferrone
ms.date: 06/06/2019
ms.topic: article
keywords: 混合现实，控件，交互，提示，ui，ux，混合现实耳机，windows mixed Reality 耳机，虚拟现实耳机，HoloLens，MRTK，混合现实工具包，音频
ms.openlocfilehash: fb7004c22602683e4edb1e38784cac5c0b7479c4
ms.sourcegitcommit: d340303cda71c31e6c3320231473d623c0930d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2021
ms.locfileid: "97847857"
---
# <a name="interactable-object"></a><span data-ttu-id="58984-105">可交互对象</span><span class="sxs-lookup"><span data-stu-id="58984-105">Interactable object</span></span>

![Interactible 对象](images/UX_Hero_Interactable.jpg)

<span data-ttu-id="58984-107">"Button" 是一种用于在二维抽象环境中触发事件的比喻。</span><span class="sxs-lookup"><span data-stu-id="58984-107">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="58984-108">在这三维混合现实世界中，我们不必再局限于这种抽象领域。</span><span class="sxs-lookup"><span data-stu-id="58984-108">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="58984-109">任何内容都可以是触发事件的 **种不可交互对象** 。</span><span class="sxs-lookup"><span data-stu-id="58984-109">Anything can be an **interactable object** that triggers an event.</span></span> <span data-ttu-id="58984-110">种不可交互对象可以是从表上的咖啡杯到 midair 中的气球的任何内容。</span><span class="sxs-lookup"><span data-stu-id="58984-110">An interactable object can be anything from a coffee cup on a table to a balloon in midair.</span></span> <span data-ttu-id="58984-111">在某些情况下（例如，在对话框 UI 中），我们仍要使用传统按钮。</span><span class="sxs-lookup"><span data-stu-id="58984-111">We still do make use of traditional buttons in certain situation such as in dialog UI.</span></span> <span data-ttu-id="58984-112">按钮的可视化表示形式取决于上下文。</span><span class="sxs-lookup"><span data-stu-id="58984-112">The visual representation of the button depends on the context.</span></span>

<br>

---

## <a name="important-properties-of-the-interactable-object"></a><span data-ttu-id="58984-113">种不可交互对象的重要属性</span><span class="sxs-lookup"><span data-stu-id="58984-113">Important properties of the interactable object</span></span>

### <a name="visual-cues"></a><span data-ttu-id="58984-114">视觉提示</span><span class="sxs-lookup"><span data-stu-id="58984-114">Visual cues</span></span>

<span data-ttu-id="58984-115">视觉提示是传感器的提示，由眼睛接收，由视觉对象系统在视觉对象中进行处理。</span><span class="sxs-lookup"><span data-stu-id="58984-115">Visual cues are sensory cues from light, received by the eye, and processed by the visual system during visual perception.</span></span> <span data-ttu-id="58984-116">由于视觉对象系统在很多物种中是主导的，尤其是在人们看来，直观提示是了解世界上的信息。</span><span class="sxs-lookup"><span data-stu-id="58984-116">Since the visual system is dominant in many species, especially humans, visual cues are a large source of information in how the world is perceived.</span></span>

<span data-ttu-id="58984-117">由于全息对象与混合现实中的实际环境混合，因此很难理解您可以与哪些对象交互。</span><span class="sxs-lookup"><span data-stu-id="58984-117">Since the holographic objects are blended with the real-world environment in mixed reality, it could be difficult to understand which objects you can interact with.</span></span> <span data-ttu-id="58984-118">对于你的体验中的任何种不可交互对象，为每个输入状态提供不同的视觉提示非常重要。</span><span class="sxs-lookup"><span data-stu-id="58984-118">For any interactable objects in your experience, it's important to provide differentiated visual cues for each input state.</span></span> <span data-ttu-id="58984-119">这可以帮助用户了解你的体验的哪个部分是种不可交互的，并通过使用一致的交互方法使用户更自信。</span><span class="sxs-lookup"><span data-stu-id="58984-119">This helps the user understand which part of your experience is interactable and makes the user confident by using a consistent interaction method.</span></span>

<br>

---

### <a name="far-interactions"></a><span data-ttu-id="58984-120">远距离交互</span><span class="sxs-lookup"><span data-stu-id="58984-120">Far interactions</span></span>

<span data-ttu-id="58984-121">对于用户可与 "注视"、"手 ray" 和 "运动控制器" 射线交互的任何对象，我们建议为这三个输入状态提供不同的视觉提示：</span><span class="sxs-lookup"><span data-stu-id="58984-121">For any objects that user can interact with gaze, hand ray, and motion controller's ray, we recommend having different visual cue for these three input states:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="58984-122">![interactibleobject-默认值](images/interactibleobject-states-default.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-122">![interactibleobject-states-default](images/interactibleobject-states-default.jpg)</span></span><br>
       <span data-ttu-id="58984-123">**默认 (观察) 状态**</span><span class="sxs-lookup"><span data-stu-id="58984-123">**Default (Observation) state**</span></span><br>
        <span data-ttu-id="58984-124">对象的默认空闲状态。</span><span class="sxs-lookup"><span data-stu-id="58984-124">Default idle state of the object.</span></span>
    <span data-ttu-id="58984-125">光标不在对象上。</span><span class="sxs-lookup"><span data-stu-id="58984-125">The cursor isn't on the object.</span></span> <span data-ttu-id="58984-126">未检测到手写。</span><span class="sxs-lookup"><span data-stu-id="58984-126">Hand isn't detected.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="58984-127">![interactibleobject-目标](images/interactibleobject-states-targeted.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-127">![interactibleobject-states-targeted](images/interactibleobject-states-targeted.jpg)</span></span><br>
        <span data-ttu-id="58984-128">**目标 (悬停) 状态**</span><span class="sxs-lookup"><span data-stu-id="58984-128">**Targeted (Hover) state**</span></span><br>
        <span data-ttu-id="58984-129">当对象面向注视光标时，指的是指邻近的或运动控制器的指针。</span><span class="sxs-lookup"><span data-stu-id="58984-129">When the object is targeted with gaze cursor, finger proximity or motion controller's pointer.</span></span>
    <span data-ttu-id="58984-130">光标位于对象上。</span><span class="sxs-lookup"><span data-stu-id="58984-130">The cursor is on the object.</span></span> <span data-ttu-id="58984-131">已检测到手型，准备就绪。</span><span class="sxs-lookup"><span data-stu-id="58984-131">Hand is detected, ready.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="58984-132">![interactibleobject-按下](images/interactibleobject-states-pressed.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-132">![interactibleobject-states-pressed](images/interactibleobject-states-pressed.jpg)</span></span><br>
       <span data-ttu-id="58984-133">**按下状态**</span><span class="sxs-lookup"><span data-stu-id="58984-133">**Pressed state**</span></span><br>
        <span data-ttu-id="58984-134">如果按下了按压按钮，请按下或运动控制器的选择按钮。</span><span class="sxs-lookup"><span data-stu-id="58984-134">When the object is pressed with an air tap gesture, finger press or motion controller's select button.</span></span>
    <span data-ttu-id="58984-135">光标位于对象上。</span><span class="sxs-lookup"><span data-stu-id="58984-135">The cursor is on the object.</span></span> <span data-ttu-id="58984-136">检测到手型，并攻丝。</span><span class="sxs-lookup"><span data-stu-id="58984-136">Hand is detected, air tapped.</span></span>
    :::column-end:::
:::row-end:::

<br>

---

<span data-ttu-id="58984-137">您可以使用诸如突出显示或缩放等方法为用户输入状态提供视觉提示。</span><span class="sxs-lookup"><span data-stu-id="58984-137">You can use techniques such as highlighting or scaling to provide visual cues for the user’s input state.</span></span> <span data-ttu-id="58984-138">在混合现实中，可以在 "开始" 菜单和应用栏按钮中查找可视化不同输入状态的示例。</span><span class="sxs-lookup"><span data-stu-id="58984-138">In mixed reality, you can find examples of visualizing different input states on the Start menu and with app bar buttons.</span></span> 

<span data-ttu-id="58984-139">下面是 **全息按钮** 上这些状态的外观：</span><span class="sxs-lookup"><span data-stu-id="58984-139">Here's what these states look like on a **holographic button**:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="58984-140">![interactibleobject-默认值](images/MRTK_InteractableState-default.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-140">![interactibleobject-states-default](images/MRTK_InteractableState-default.jpg)</span></span><br>
       <span data-ttu-id="58984-141">**默认 (观察) 状态**</span><span class="sxs-lookup"><span data-stu-id="58984-141">**Default (Observation) state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="58984-142">![interactibleobject-目标](images/MRTK_InteractableState-targeted.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-142">![interactibleobject-states-targeted](images/MRTK_InteractableState-targeted.jpg)</span></span><br>
        <span data-ttu-id="58984-143">**目标 (悬停) 状态**</span><span class="sxs-lookup"><span data-stu-id="58984-143">**Targeted (Hover) state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="58984-144">![interactibleobject-按下](images/MRTK_InteractableState-pressed.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-144">![interactibleobject-states-pressed](images/MRTK_InteractableState-pressed.jpg)</span></span><br>
       <span data-ttu-id="58984-145">**按下状态**</span><span class="sxs-lookup"><span data-stu-id="58984-145">**Pressed state**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

### <a name="near-interactions-direct"></a><span data-ttu-id="58984-146">接近交互 (直接) </span><span class="sxs-lookup"><span data-stu-id="58984-146">Near interactions (direct)</span></span> 

<span data-ttu-id="58984-147">HoloLens 2 支持已表述的手动跟踪输入，这允许您与对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="58984-147">HoloLens 2 supports articulated hand tracking input, which allows you to interact with objects.</span></span> <span data-ttu-id="58984-148">如果没有 haptic 的反馈和完美的深度认识，则很难判断你手中的距离是从一个对象还是正在触摸。</span><span class="sxs-lookup"><span data-stu-id="58984-148">Without haptic feedback and perfect depth perception, it can be hard to tell how far away your hand is from an object or whether you're touching it.</span></span> <span data-ttu-id="58984-149">务必提供足够的视觉提示来传达对象的状态，特别是根据对象的状态。</span><span class="sxs-lookup"><span data-stu-id="58984-149">It's important to provide enough visual cues to communicate the state of the object, in particular the state of your hands based on that object.</span></span>

<span data-ttu-id="58984-150">使用视觉反馈传达以下状态：</span><span class="sxs-lookup"><span data-stu-id="58984-150">Use visual feedback to communicate the following states:</span></span>
* <span data-ttu-id="58984-151">**默认 (观察)**：对象的默认空闲状态。</span><span class="sxs-lookup"><span data-stu-id="58984-151">**Default (Observation)**: Default idle state of the object.</span></span>
* <span data-ttu-id="58984-152">**悬停**：当手接近全息图时，请更改视觉对象，以便与全息图建立通信。</span><span class="sxs-lookup"><span data-stu-id="58984-152">**Hover**: When a hand is near a hologram, change visuals to communicate that hand is targeting hologram.</span></span> 
* <span data-ttu-id="58984-153">**距离和交互点**：作为一种方法，即使用全息图，设计反馈来传达投影的交互点，以及从对象到手指的距离</span><span class="sxs-lookup"><span data-stu-id="58984-153">**Distance and point of interaction**: As the hand approaches a hologram, design feedback to communicate the projected point of interaction, and how far from the object the finger is</span></span>
* <span data-ttu-id="58984-154">**联系人开始**：更改视觉对象 (光源、颜色) ，传达触摸已发生的情况</span><span class="sxs-lookup"><span data-stu-id="58984-154">**Contact begins**: Change visuals (light, color) to communicate that a touch has occurred</span></span>
* <span data-ttu-id="58984-155">**Grasped**：在 Grasped 对象时更改视觉对象 (光源、颜色) </span><span class="sxs-lookup"><span data-stu-id="58984-155">**Grasped**: Change visuals (light, color) when the object is grasped</span></span>
* <span data-ttu-id="58984-156">**联系人结束**：在触摸结束时，更改视觉对象 (光源、颜色) </span><span class="sxs-lookup"><span data-stu-id="58984-156">**Contact ends**: Change visuals (light, color) when touch has ended</span></span>

<br>

---

:::row:::
    :::column:::
        <span data-ttu-id="58984-157">![悬停 (远处) ](images/640px-interactibleobject-states-near-hover.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-157">![Hover (Far)](images/640px-interactibleobject-states-near-hover.jpg)</span></span><br>
        <span data-ttu-id="58984-158">**悬停 (远处)**</span><span class="sxs-lookup"><span data-stu-id="58984-158">**Hover (Far)**</span></span><br>
        <span data-ttu-id="58984-159">根据手的邻近性突出显示。</span><span class="sxs-lookup"><span data-stu-id="58984-159">Highlighting based on the proximity of the hand.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="58984-160">![悬停 (接近) ](images/640px-interactibleobject-states-near-hovernear.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-160">![Hover (Near)](images/640px-interactibleobject-states-near-hovernear.jpg)</span></span><br>
        <span data-ttu-id="58984-161">**悬停 (接近)**</span><span class="sxs-lookup"><span data-stu-id="58984-161">**Hover (Near)**</span></span><br>
        <span data-ttu-id="58984-162">根据与手型的距离突出显示大小变化。</span><span class="sxs-lookup"><span data-stu-id="58984-162">Highlight size changes based on the distance to the hand.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="58984-163">![触摸/按](images/640px-interactibleobject-states-near-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-163">![Touch / press](images/640px-interactibleobject-states-near-press.jpg)</span></span><br>
        <span data-ttu-id="58984-164">**触摸/按**</span><span class="sxs-lookup"><span data-stu-id="58984-164">**Touch / press**</span></span><br>
        <span data-ttu-id="58984-165">视觉对象和音频反馈。</span><span class="sxs-lookup"><span data-stu-id="58984-165">Visual plus audio feedback.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="58984-166">![掌握](images/640px-interactibleobject-states-near-grasp.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-166">![Grasp](images/640px-interactibleobject-states-near-grasp.jpg)</span></span><br>
        <span data-ttu-id="58984-167">**掌握**</span><span class="sxs-lookup"><span data-stu-id="58984-167">**Grasp**</span></span><br>
        <span data-ttu-id="58984-168">视觉对象和音频反馈。</span><span class="sxs-lookup"><span data-stu-id="58984-168">Visual plus audio feedback.</span></span>
    :::column-end:::
:::row-end:::

<br>

<br>

---

<span data-ttu-id="58984-169">[HoloLens 2 上的按钮](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)是如何可视化不同输入交互状态的示例：</span><span class="sxs-lookup"><span data-stu-id="58984-169">A [button on HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) is an example of how the different input interaction states are visualized:</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="58984-170">![默认](images/640px-interactibleobject-pressablebutton-default.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-170">![Default](images/640px-interactibleobject-pressablebutton-default.jpg)</span></span><br>
        <span data-ttu-id="58984-171">**默认**</span><span class="sxs-lookup"><span data-stu-id="58984-171">**Default**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="58984-172">![悬停](images/640px-interactibleobject-pressablebutton-hover.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-172">![Hover](images/640px-interactibleobject-pressablebutton-hover.jpg)</span></span><br>
        <span data-ttu-id="58984-173">**悬停**</span><span class="sxs-lookup"><span data-stu-id="58984-173">**Hover**</span></span><br>
        <span data-ttu-id="58984-174">显示基于近程的照明效果。</span><span class="sxs-lookup"><span data-stu-id="58984-174">Reveal a proximity-based lighting effect.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="58984-175">![触控](images/640px-interactibleobject-pressablebutton-touch.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-175">![Touch](images/640px-interactibleobject-pressablebutton-touch.jpg)</span></span><br>
        <span data-ttu-id="58984-176">**触控**</span><span class="sxs-lookup"><span data-stu-id="58984-176">**Touch**</span></span><br>
        <span data-ttu-id="58984-177">显示波纹效果。</span><span class="sxs-lookup"><span data-stu-id="58984-177">Show ripple effect.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="58984-178">![请按](images/640px-interactibleobject-pressablebutton-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-178">![Press](images/640px-interactibleobject-pressablebutton-press.jpg)</span></span><br>
        <span data-ttu-id="58984-179">**请按**</span><span class="sxs-lookup"><span data-stu-id="58984-179">**Press**</span></span><br>
        <span data-ttu-id="58984-180">移动前面板。</span><span class="sxs-lookup"><span data-stu-id="58984-180">Move the front plate.</span></span>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="the-ring-visual-cue-on-hololens-2br"></a><span data-ttu-id="58984-181">HoloLens 2 上的 "环" 视觉提示</span><span class="sxs-lookup"><span data-stu-id="58984-181">The "ring" visual cue on HoloLens 2</span></span><br>
        <span data-ttu-id="58984-182">在 HoloLens 2 上，有一个额外的视觉提示，可帮助用户了解深度。</span><span class="sxs-lookup"><span data-stu-id="58984-182">On HoloLens 2, there's an extra visual cue, which can help the user's perception of depth.</span></span> <span data-ttu-id="58984-183">当手指更接近对象时，其手指附近的圆圈会显示并缩小。</span><span class="sxs-lookup"><span data-stu-id="58984-183">A ring near their fingertip shows up and scales down as the fingertip gets closer to the object.</span></span> <span data-ttu-id="58984-184">当达到按下状态时，环最终汇聚为一个点。</span><span class="sxs-lookup"><span data-stu-id="58984-184">The ring eventually converges into a dot when the pressed state is reached.</span></span> <span data-ttu-id="58984-185">此视觉对象 affordance 可帮助用户了解其在对象中的距离。</span><span class="sxs-lookup"><span data-stu-id="58984-185">This visual affordance helps the user understand how far they are from the object.</span></span><br>
        <br>
        <span data-ttu-id="58984-186">*视频循环：基于与边界框的邻近的视觉反馈示例*</span><span class="sxs-lookup"><span data-stu-id="58984-186">*Video loop: Example of visual feedback based on proximity to a bounding box*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="58984-187">![space](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="58984-187">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="58984-188">![视觉对象反馈](images/HoloLens2_Proximity.gif)</span><span class="sxs-lookup"><span data-stu-id="58984-188">![Visual feedback on hand proximity](images/HoloLens2_Proximity.gif)</span></span><br>
    :::column-end:::
:::row-end:::


<br>

---


### <a name="audio-cues"></a><span data-ttu-id="58984-189">音频提示</span><span class="sxs-lookup"><span data-stu-id="58984-189">Audio cues</span></span>

<span data-ttu-id="58984-190">对于直接交互，正确的音频反馈可显著改善用户体验。</span><span class="sxs-lookup"><span data-stu-id="58984-190">For direct hand interactions, proper audio feedback can dramatically improve the user experience.</span></span> <span data-ttu-id="58984-191">使用音频反馈来传达以下提示：</span><span class="sxs-lookup"><span data-stu-id="58984-191">Use audio feedback to communicate the following cues:</span></span>
* <span data-ttu-id="58984-192">**联系人开始**：触控开始时播放声音</span><span class="sxs-lookup"><span data-stu-id="58984-192">**Contact begins**: Play sound when touch begins</span></span>
* <span data-ttu-id="58984-193">**联系人结束**：在 touch 端上播放声音</span><span class="sxs-lookup"><span data-stu-id="58984-193">**Contact ends**: Play sound on touch end</span></span>
* <span data-ttu-id="58984-194">**开始获取**：开始播放时播放声音</span><span class="sxs-lookup"><span data-stu-id="58984-194">**Grab begins**: Play sound when grab starts</span></span>
* <span data-ttu-id="58984-195">**抓取结束**：在抓取结束时播放声音</span><span class="sxs-lookup"><span data-stu-id="58984-195">**Grab ends**: Play sound when grab ends</span></span>

<br>

---

:::row:::
    :::column:::
        ### <a name="voice-commandingbr"></a><span data-ttu-id="58984-196">语音命令</span><span class="sxs-lookup"><span data-stu-id="58984-196">Voice commanding</span></span><br>
        <span data-ttu-id="58984-197">对于任何种不可交互对象，支持替代交互选项非常重要。</span><span class="sxs-lookup"><span data-stu-id="58984-197">For any interactable objects, it's important to support alternative interaction options.</span></span> <span data-ttu-id="58984-198">默认情况下，我们建议为种不可交互的任何对象支持 [语音命令](../out-of-scope/voice-design.md) 。</span><span class="sxs-lookup"><span data-stu-id="58984-198">By default, we recommend that [voice commanding](../out-of-scope/voice-design.md) be supported for any objects that are interactable.</span></span> <span data-ttu-id="58984-199">若要改善可发现性，还可以在悬停状态中提供工具提示。</span><span class="sxs-lookup"><span data-stu-id="58984-199">To improve discoverability, you can also provide a tooltip during the hover state.</span></span><br>
        <br>
        <span data-ttu-id="58984-200">*Image：语音命令的工具提示*</span><span class="sxs-lookup"><span data-stu-id="58984-200">*Image: Tooltip for the voice command*</span></span>
    :::column-end:::
        :::column:::
       ![语音命令](images/640px-interactibleobject-voicecommand.png)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="sizing-recommendations"></a><span data-ttu-id="58984-202">重设大小建议</span><span class="sxs-lookup"><span data-stu-id="58984-202">Sizing recommendations</span></span> 

<span data-ttu-id="58984-203">为了确保可以轻松地接触所有种不可交互对象，我们建议确保种不可交互根据其从用户的距离来确定最小大小。</span><span class="sxs-lookup"><span data-stu-id="58984-203">To ensure all interactable objects can easily be touched, we recommend making sure the interactable meets a minimum size based on the distance it's placed from the user.</span></span> <span data-ttu-id="58984-204">视觉角度通常以视觉弧的度数来度量。视觉角度基于用户眼睛与对象之间的距离并保持不变，而目标的物理大小可能会随用户更改的距离而更改。</span><span class="sxs-lookup"><span data-stu-id="58984-204">The visual angle is often measured in degrees of visual arc. Visual angle is based on the distance between the user's eyes and the object and stays constant, while the physical size of the target may change as the distance from the user changes.</span></span> <span data-ttu-id="58984-205">若要根据用户的距离确定对象的必要物理大小，请尝试使用视觉角度计算器（如 [此](https://elvers.us/perception/visualAngle/)类）。</span><span class="sxs-lookup"><span data-stu-id="58984-205">To determine the necessary physical size of an object based on the distance from the user, try using a visual angle calculator such as [this one](https://elvers.us/perception/visualAngle/).</span></span>

<span data-ttu-id="58984-206">下面是有关种不可交互内容的最小大小建议。</span><span class="sxs-lookup"><span data-stu-id="58984-206">Below are the recommendations for minimum sizes of interactable content.</span></span>


### <a name="target-size-for-direct-hand-interaction"></a><span data-ttu-id="58984-207">直接手动交互的目标大小</span><span class="sxs-lookup"><span data-stu-id="58984-207">Target size for direct hand interaction</span></span>

| <span data-ttu-id="58984-208">距离</span><span class="sxs-lookup"><span data-stu-id="58984-208">Distance</span></span> | <span data-ttu-id="58984-209">查看角度</span><span class="sxs-lookup"><span data-stu-id="58984-209">Viewing angle</span></span> | <span data-ttu-id="58984-210">大小</span><span class="sxs-lookup"><span data-stu-id="58984-210">Size</span></span> |
|---------|---------|---------|
| <span data-ttu-id="58984-211">45厘米</span><span class="sxs-lookup"><span data-stu-id="58984-211">45 cm</span></span>  | <span data-ttu-id="58984-212">不小于2°</span><span class="sxs-lookup"><span data-stu-id="58984-212">no smaller than 2°</span></span> | <span data-ttu-id="58984-213">1.6 x 1.6 厘米</span><span class="sxs-lookup"><span data-stu-id="58984-213">1.6 x 1.6 cm</span></span> |

<span data-ttu-id="58984-214">![直接手动交互的目标大小](images/TargetSizingNear.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-214">![Target size for direct hand interaction](images/TargetSizingNear.jpg)</span></span><br>
<span data-ttu-id="58984-215">*直接手动交互的目标大小*</span><span class="sxs-lookup"><span data-stu-id="58984-215">*Target size for direct hand interaction*</span></span>

<br>

### <a name="target-size-for-buttons"></a><span data-ttu-id="58984-216">按钮的目标大小</span><span class="sxs-lookup"><span data-stu-id="58984-216">Target size for buttons</span></span>

<span data-ttu-id="58984-217">创建直接交互的按钮时，建议使用较大的最小 3.2 x 3.2 厘米，以确保有足够的空间来包含图标，并可能有一些文本。</span><span class="sxs-lookup"><span data-stu-id="58984-217">When creating buttons for direct interaction, we recommend a larger minimum size of 3.2 x 3.2 cm to ensure that there's enough space to contain an icon and potentially some text.</span></span>

| <span data-ttu-id="58984-218">距离</span><span class="sxs-lookup"><span data-stu-id="58984-218">Distance</span></span> | <span data-ttu-id="58984-219">最小大小</span><span class="sxs-lookup"><span data-stu-id="58984-219">Minimum size</span></span> |
|---------|---------|
| <span data-ttu-id="58984-220">45厘米</span><span class="sxs-lookup"><span data-stu-id="58984-220">45 cm</span></span>  | <span data-ttu-id="58984-221">3.2 x 3.2 厘米</span><span class="sxs-lookup"><span data-stu-id="58984-221">3.2 x 3.2 cm</span></span> |

<span data-ttu-id="58984-222">![按钮的目标大小](images/TargetSizingButtons.png)</span><span class="sxs-lookup"><span data-stu-id="58984-222">![Target size for the buttons](images/TargetSizingButtons.png)</span></span><br>
<span data-ttu-id="58984-223">*按钮的目标大小*</span><span class="sxs-lookup"><span data-stu-id="58984-223">*Target size for the buttons*</span></span>

<br>

### <a name="target-size-for-hand-ray-or-gaze-interaction"></a><span data-ttu-id="58984-224">手动 ray 或注视交互的目标大小</span><span class="sxs-lookup"><span data-stu-id="58984-224">Target size for hand ray or gaze interaction</span></span>
| <span data-ttu-id="58984-225">距离</span><span class="sxs-lookup"><span data-stu-id="58984-225">Distance</span></span> | <span data-ttu-id="58984-226">查看角度</span><span class="sxs-lookup"><span data-stu-id="58984-226">Viewing angle</span></span> | <span data-ttu-id="58984-227">大小</span><span class="sxs-lookup"><span data-stu-id="58984-227">Size</span></span> |
|---------|---------|---------|
| <span data-ttu-id="58984-228">2 m</span><span class="sxs-lookup"><span data-stu-id="58984-228">2 m</span></span>  | <span data-ttu-id="58984-229">不小于1°</span><span class="sxs-lookup"><span data-stu-id="58984-229">no smaller than 1°</span></span> | <span data-ttu-id="58984-230">3.5 x 3.5 厘米</span><span class="sxs-lookup"><span data-stu-id="58984-230">3.5 x 3.5 cm</span></span> |

<span data-ttu-id="58984-231">![手动 ray 或注视交互的目标大小](images/TargetSizingFar.jpg)</span><span class="sxs-lookup"><span data-stu-id="58984-231">![Target size for hand ray or gaze interaction](images/TargetSizingFar.jpg)</span></span><br>
<span data-ttu-id="58984-232">*手动 ray 或注视交互的目标大小*</span><span class="sxs-lookup"><span data-stu-id="58984-232">*Target size for hand ray or gaze interaction*</span></span>


<br>

---


## <a name="interactable-object-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="58984-233">MRTK 中的种不可交互对象 (Unity 的混合现实工具包) </span><span class="sxs-lookup"><span data-stu-id="58984-233">Interactable object in MRTK (Mixed Reality Toolkit) for Unity</span></span>

<span data-ttu-id="58984-234">在 **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** 中，可以使用脚本 [**种不可交互**](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Interactable/Scripts) 使对象对各种类型的输入交互状态进行响应。</span><span class="sxs-lookup"><span data-stu-id="58984-234">In **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, you can use the script [**Interactable**](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Interactable/Scripts) to make objects respond to various types of input interaction states.</span></span> <span data-ttu-id="58984-235">它支持各种类型的主题，这些主题允许您通过控制对象属性（如颜色、大小、材料和着色器）来定义可视状态。</span><span class="sxs-lookup"><span data-stu-id="58984-235">It supports various types of themes that allow you define visual states by controlling object properties such as color, size, material, and shader.</span></span>

* [<span data-ttu-id="58984-236">种不可交互</span><span class="sxs-lookup"><span data-stu-id="58984-236">Interactable</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)
* [<span data-ttu-id="58984-237">Button</span><span class="sxs-lookup"><span data-stu-id="58984-237">Button</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [<span data-ttu-id="58984-238">手动交互示例场景</span><span class="sxs-lookup"><span data-stu-id="58984-238">Hand interaction examples scene</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_HandInteractionExamples.md)

<span data-ttu-id="58984-239">MixedRealityToolkit 的标准着色器提供了各种选项 **，例如，可** 帮助您创建视觉对象和音频提示。</span><span class="sxs-lookup"><span data-stu-id="58984-239">MixedRealityToolkit's Standard shader provides various options such as **proximity light** that helps you create visual and audio cues.</span></span>
* [<span data-ttu-id="58984-240">MRTK 标准着色器</span><span class="sxs-lookup"><span data-stu-id="58984-240">MRTK Standard Shader</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md)


<br>

---


## <a name="see-also"></a><span data-ttu-id="58984-241">另请参阅</span><span class="sxs-lookup"><span data-stu-id="58984-241">See also</span></span>

* [<span data-ttu-id="58984-242">光标</span><span class="sxs-lookup"><span data-stu-id="58984-242">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="58984-243">手部射线</span><span class="sxs-lookup"><span data-stu-id="58984-243">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="58984-244">Button</span><span class="sxs-lookup"><span data-stu-id="58984-244">Button</span></span>](button.md)
* [<span data-ttu-id="58984-245">可交互对象</span><span class="sxs-lookup"><span data-stu-id="58984-245">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="58984-246">边界框和应用栏</span><span class="sxs-lookup"><span data-stu-id="58984-246">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="58984-247">操作</span><span class="sxs-lookup"><span data-stu-id="58984-247">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="58984-248">手动菜单</span><span class="sxs-lookup"><span data-stu-id="58984-248">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="58984-249">追踪菜单</span><span class="sxs-lookup"><span data-stu-id="58984-249">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="58984-250">对象集合</span><span class="sxs-lookup"><span data-stu-id="58984-250">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="58984-251">语音命令</span><span class="sxs-lookup"><span data-stu-id="58984-251">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="58984-252">键盘</span><span class="sxs-lookup"><span data-stu-id="58984-252">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="58984-253">工具提示</span><span class="sxs-lookup"><span data-stu-id="58984-253">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="58984-254">平板</span><span class="sxs-lookup"><span data-stu-id="58984-254">Slate</span></span>](slate.md)
* [<span data-ttu-id="58984-255">滑块</span><span class="sxs-lookup"><span data-stu-id="58984-255">Slider</span></span>](slider.md)
* [<span data-ttu-id="58984-256">着色器</span><span class="sxs-lookup"><span data-stu-id="58984-256">Shader</span></span>](shader.md)
* [<span data-ttu-id="58984-257">公告和尾随</span><span class="sxs-lookup"><span data-stu-id="58984-257">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="58984-258">显示进度</span><span class="sxs-lookup"><span data-stu-id="58984-258">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="58984-259">表面磁吸</span><span class="sxs-lookup"><span data-stu-id="58984-259">Surface magnetism</span></span>](surface-magnetism.md)
