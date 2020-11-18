---
title: 头部凝视和提交
description: 头部凝视和提交输入模型概述
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: Mixed Reality，注视，注视目标，交互，设计，混合现实耳机，windows mixed Reality 耳机，虚拟现实耳机，HoloLens，MRTK，混合现实工具包，目标，焦点，平滑
ms.openlocfilehash: d913ac81e20962d38178223a050fdccfb51d8632
ms.sourcegitcommit: 4f3ef057a285be2e260615e5d6c41f00d15d08f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94702383"
---
# <a name="head-gaze-and-commit"></a><span data-ttu-id="4695f-104">头部凝视和提交</span><span class="sxs-lookup"><span data-stu-id="4695f-104">Head-gaze and commit</span></span>
<span data-ttu-id="4695f-105">"[注视](gaze-and-commit.md)" 和 "提交" 输入 _模型是一_ 种特殊情况，它涉及到对象的方向为 "向前" (head 方向) ，然后使用辅助输入（例如，手势分流或语音命令 "Select"）来定位对象。</span><span class="sxs-lookup"><span data-stu-id="4695f-105">_Head-gaze and commit_ is a special case of the [gaze and commit](gaze-and-commit.md) input model that involves targeting an object with the direction of your head pointing forward (head-direction), and then acting on it with a secondary input, such as the hand gesture air tap or the voice command "Select".</span></span> 

## <a name="device-support"></a><span data-ttu-id="4695f-106">设备支持</span><span class="sxs-lookup"><span data-stu-id="4695f-106">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="4695f-107"><strong>输入模型</strong></span><span class="sxs-lookup"><span data-stu-id="4695f-107"><strong>Input model</strong></span></span></td>
        <td><span data-ttu-id="4695f-108"><a href="../hololens-hardware-details.md"><strong>HoloLens（第 1 代）</strong></a></span><span class="sxs-lookup"><span data-stu-id="4695f-108"><a href="../hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="4695f-109"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="4695f-109"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="4695f-110"><a href="../discover/immersive-headset-hardware-details.md"><strong>沉浸式头戴显示设备</strong></a></span><span class="sxs-lookup"><span data-stu-id="4695f-110"><a href="../discover/immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="4695f-111">头部凝视和提交</span><span class="sxs-lookup"><span data-stu-id="4695f-111">Head-gaze and commit</span></span></td>
        <td><span data-ttu-id="4695f-112">✔️ 推荐</span><span class="sxs-lookup"><span data-stu-id="4695f-112">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="4695f-113">✔️推荐（第三个选择 - <a href="interaction-fundamentals.md">查看其他选项</a>）</span><span class="sxs-lookup"><span data-stu-id="4695f-113">✔️ Recommended (third choice - <a href="interaction-fundamentals.md">See the other options</a>)</span></span></td>
        <td><span data-ttu-id="4695f-114">➕ 备用选项</span><span class="sxs-lookup"><span data-stu-id="4695f-114">➕ Alternate option</span></span></td>
    </tr>
</table>

---

## <a name="target-sizing-and-feedback"></a><span data-ttu-id="4695f-115">目标大小调整和反馈</span><span class="sxs-lookup"><span data-stu-id="4695f-115">Target sizing and feedback</span></span>
<span data-ttu-id="4695f-116">一直看着打印头向量，使其可用于精细定位，但通常最适用于毛目标-获取稍大的目标。</span><span class="sxs-lookup"><span data-stu-id="4695f-116">The head gaze vector has been shown repeatedly to be usable for fine targeting, but often works best for gross targeting--acquiring somewhat larger targets.</span></span> <span data-ttu-id="4695f-117">在大多数情况下，最小目标大小为1到1.5 度允许成功的用户操作，尽管目标为3度，但通常可以提高速度。</span><span class="sxs-lookup"><span data-stu-id="4695f-117">Minimum target sizes of 1 to 1.5 degrees allow successful user actions in most scenarios, though targets of 3 degrees often allow for greater speed.</span></span> <span data-ttu-id="4695f-118">请注意，即使对于 3D 元素，用户设定为目标的尺寸实际上也是 2D 区域，3D 元素的投影即是可设定为目标的区域。</span><span class="sxs-lookup"><span data-stu-id="4695f-118">Note that the size that the user targets is effectively a 2D area even for 3D elements--whichever projection is facing them should be the targetable area.</span></span> <span data-ttu-id="4695f-119">提供一些突出的提示，指出某个元素处于 "活动" 状态， (用户为该元素设定目标) 特别有用。</span><span class="sxs-lookup"><span data-stu-id="4695f-119">Providing some salient cue that an element is "active" (that the user is targeting it) is extremely helpful.</span></span> <span data-ttu-id="4695f-120">这可能包括处理方式（如可见的 "悬停" 效果、音频突出显示或单击），或通过元素清晰显示光标。</span><span class="sxs-lookup"><span data-stu-id="4695f-120">This can include treatments like visible "hover" effects, audio highlights or clicks, or clear alignment of a cursor with an element.</span></span>

<span data-ttu-id="4695f-121">![2 米远处的最佳目标大小](images/gazetargeting-size-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="4695f-121">![Optimal target size at 2 meter distance](images/gazetargeting-size-1000px.jpg)</span></span><br>
<span data-ttu-id="4695f-122">*2 米远处的最佳目标大小*</span><span class="sxs-lookup"><span data-stu-id="4695f-122">*Optimal target size at 2 meter distance*</span></span>

<br>

<span data-ttu-id="4695f-123">![突出显示凝视目标对象的示例](images/gazetargeting-highlighting-940px.jpg)</span><span class="sxs-lookup"><span data-stu-id="4695f-123">![An example of highlighting a gaze targeted object](images/gazetargeting-highlighting-940px.jpg)</span></span><br>
<span data-ttu-id="4695f-124">*突出显示凝视目标对象的示例*</span><span class="sxs-lookup"><span data-stu-id="4695f-124">*An example of highlighting a gaze targeted object*</span></span>

## <a name="target-placement"></a><span data-ttu-id="4695f-125">目标位置</span><span class="sxs-lookup"><span data-stu-id="4695f-125">Target placement</span></span>
<span data-ttu-id="4695f-126">用户经常找不到在其视图字段中定位很高或极低的 UI 元素，这就是他们对其主要关注点的关注点（大约在眼睛上）。</span><span class="sxs-lookup"><span data-stu-id="4695f-126">Users often fail to find UI elements that are positioned very high or very low in their field of view, focusing most of their attention on areas around their main focus, which is approximately at eye level.</span></span> <span data-ttu-id="4695f-127">将大多数目标放在视平线位置附近的某个合理范围内可能有所帮助。</span><span class="sxs-lookup"><span data-stu-id="4695f-127">Placing most targets in some reasonable band around eye level can help.</span></span> <span data-ttu-id="4695f-128">考虑到用户在任何时候都倾向于关注一个相对较小的可视区域（注意力视锥大约为 10 度），通过将 UI 元素分组到在概念上相关的位置，可以在用户的视线通过某个区域时利用各项目之间的注意力链锁作用。</span><span class="sxs-lookup"><span data-stu-id="4695f-128">Given the tendency for users to focus on a relatively small visual area at any time (the attentional cone of vision is roughly 10 degrees), grouping UI elements together to the degree that they're related conceptually can leverage attention-chaining behaviors from item to item as a user moves their gaze through an area.</span></span> <span data-ttu-id="4695f-129">在设计 UI 时，请注意 HoloLens 和沉浸式头戴显示设备之间视野的巨大差异。</span><span class="sxs-lookup"><span data-stu-id="4695f-129">When designing UI, keep in mind the potential large variation in field of view between HoloLens and immersive headsets.</span></span>

<span data-ttu-id="4695f-130">![在 Galaxy Explorer 中使用分组 UI 元素简化凝视目标设定的示例](images/gazetargeting-grouping-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="4695f-130">![An example of grouped UI elements for easier gaze targeting in Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)</span></span><br>
<span data-ttu-id="4695f-131">*在 Galaxy Explorer 中使用分组 UI 元素简化凝视目标设定的示例*</span><span class="sxs-lookup"><span data-stu-id="4695f-131">*An example of grouped UI elements for easier gaze targeting in Galaxy Explorer*</span></span>

## <a name="improving-targeting-behaviors"></a><span data-ttu-id="4695f-132">改进目标设定行为</span><span class="sxs-lookup"><span data-stu-id="4695f-132">Improving targeting behaviors</span></span>
<span data-ttu-id="4695f-133">如果可将用户意向定位到 (或大致接近) ，则在交互时接受接近的未命中尝试，就像它们的目标是正确的一样。</span><span class="sxs-lookup"><span data-stu-id="4695f-133">If user intent to target something can be determined (or approximated closely), it can be very helpful to accept near miss attempts at interaction as though they were targeted correctly.</span></span> <span data-ttu-id="4695f-134">下面是一些可在混合现实体验中结合使用的成功方法：</span><span class="sxs-lookup"><span data-stu-id="4695f-134">Here are a handful of successful methods that can be incorporated in mixed reality experiences:</span></span>

### <a name="head-gaze-stabilization-gravity-wells"></a><span data-ttu-id="4695f-135">头部凝视防抖动（“重力井”）</span><span class="sxs-lookup"><span data-stu-id="4695f-135">Head-gaze stabilization ("gravity wells")</span></span>
<span data-ttu-id="4695f-136">这应该是最多或全部开启。</span><span class="sxs-lookup"><span data-stu-id="4695f-136">This should be turned on most or all of the time.</span></span> <span data-ttu-id="4695f-137">此方法可删除用户在查找和讲话行为上可能具有的移动的自然头和抖动。</span><span class="sxs-lookup"><span data-stu-id="4695f-137">This technique removes the natural head and neck jitters that users might have as well movement due to looking and speaking behaviors.</span></span>

### <a name="closest-link-algorithms"></a><span data-ttu-id="4695f-138">最邻近链接算法</span><span class="sxs-lookup"><span data-stu-id="4695f-138">Closest link algorithms</span></span>
<span data-ttu-id="4695f-139">这些方法在交互内容稀少的区域效果最好。</span><span class="sxs-lookup"><span data-stu-id="4695f-139">These work best in areas with sparse interactive content.</span></span> <span data-ttu-id="4695f-140">如果很有可能确定用户尝试与之交互的概率很高，则可以通过假定某些级别来补充其目标功能。</span><span class="sxs-lookup"><span data-stu-id="4695f-140">If there is a high probability that you can determine what a user was attempting to interact with, you can supplement their targeting abilities by assuming some level of intent.</span></span>

### <a name="backdating-and-postdating-actions"></a><span data-ttu-id="4695f-141">Backdating 和 postdating 操作</span><span class="sxs-lookup"><span data-stu-id="4695f-141">Backdating and postdating actions</span></span>
<span data-ttu-id="4695f-142">此机制非常适合需要快速完成的任务。</span><span class="sxs-lookup"><span data-stu-id="4695f-142">This mechanism is useful in tasks requiring speed.</span></span> <span data-ttu-id="4695f-143">当用户通过一系列的目标和激活设法使其来实现速度提高时，采用某种目的是非常有用的，并允许缺少 50 (的步骤处理用户在) 之前或之后稍微突出的目标，而不是在早期测试生效之前/之后发生。</span><span class="sxs-lookup"><span data-stu-id="4695f-143">When a user is moving through a series of targeting and activation maneuvers at speed, it is useful to assume some intent, and allow missed steps to act upon targets that the user had in focus slightly before or slightly after the tap (50 ms before/after was effective in early testing).</span></span>

### <a name="smoothing"></a><span data-ttu-id="4695f-144">平滑处理</span><span class="sxs-lookup"><span data-stu-id="4695f-144">Smoothing</span></span>
<span data-ttu-id="4695f-145">此机制对于路径移动非常有用，因为自然移动特征会降低轻微的抖动和 wobble。</span><span class="sxs-lookup"><span data-stu-id="4695f-145">This mechanism is useful for pathing movements, reducing the slight jitter and wobble due to natural head movement characteristics.</span></span> <span data-ttu-id="4695f-146">对路径运动进行平滑处理时，按移动的大小和距离而不是一段时间来平滑。</span><span class="sxs-lookup"><span data-stu-id="4695f-146">When smoothing over pathing motions, smooth by the size and distance of movements rather than over time.</span></span>

### <a name="magnetism"></a><span data-ttu-id="4695f-147">磁吸</span><span class="sxs-lookup"><span data-stu-id="4695f-147">Magnetism</span></span>
<span data-ttu-id="4695f-148">此机制可被视为最近的链接算法的更通用版本，即根据目标绘制游标，或者只是直观或不增加 hitboxes，因为用户通过使用一些交互式布局了解来更好地利用用户意图来实现目标。</span><span class="sxs-lookup"><span data-stu-id="4695f-148">This mechanism can be thought of as a more general version of closest link algorithms--drawing a cursor toward a target or simply increasing hitboxes, whether visibly or not, as users approach likely targets by using some knowledge of the interactive layout to better approach user intent.</span></span> <span data-ttu-id="4695f-149">这对于小型目标尤其有用。</span><span class="sxs-lookup"><span data-stu-id="4695f-149">This can be particularly powerful for small targets.</span></span>

### <a name="focus-stickiness"></a><span data-ttu-id="4695f-150">焦点粘性</span><span class="sxs-lookup"><span data-stu-id="4695f-150">Focus stickiness</span></span>
<span data-ttu-id="4695f-151">在确定要将焦点放到哪些附近的交互式元素时，焦点将为当前聚焦的元素提供偏移。</span><span class="sxs-lookup"><span data-stu-id="4695f-151">When determining which nearby interactive elements to give focus to, focus stickiness provides a bias to the element that is currently focused.</span></span> <span data-ttu-id="4695f-152">当在两个元素之间的中间点处浮动时，这有助于减少不稳定的焦点切换行为。</span><span class="sxs-lookup"><span data-stu-id="4695f-152">This helps reduce erratic focus switching behaviors when floating at a midpoint between two elements with natural noise.</span></span>


## <a name="see-also"></a><span data-ttu-id="4695f-153">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4695f-153">See also</span></span>
* [<span data-ttu-id="4695f-154">基于眼睛的交互</span><span class="sxs-lookup"><span data-stu-id="4695f-154">Eye-based interaction</span></span>](eye-gaze-interaction.md)
* [<span data-ttu-id="4695f-155">凝视和停留</span><span class="sxs-lookup"><span data-stu-id="4695f-155">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="4695f-156">手 - 直接操作</span><span class="sxs-lookup"><span data-stu-id="4695f-156">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="4695f-157">手 - 手势</span><span class="sxs-lookup"><span data-stu-id="4695f-157">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="4695f-158">手 - 指向并提交</span><span class="sxs-lookup"><span data-stu-id="4695f-158">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="4695f-159">本能交互</span><span class="sxs-lookup"><span data-stu-id="4695f-159">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="4695f-160">语音输入</span><span class="sxs-lookup"><span data-stu-id="4695f-160">Voice input</span></span>](voice-input.md)



