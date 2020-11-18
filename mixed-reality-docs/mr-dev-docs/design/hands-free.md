---
title: 免手动
description: 了解用户可能会遇到的有关动手和控制器接口的问题，以及各种免提备选方案。
author: hferrone
ms.author: v-hferrone
ms.date: 04/20/2019
ms.topic: article
keywords: 混合现实，无人参与，注视，注视目标，交互，设计，混合现实耳机，windows mixed Reality 耳机，虚拟现实耳机，HoloLens，MRTK，混合现实工具包，语音输入，可用性
ms.openlocfilehash: 7f4d3a0ec8d2e7435f54164006a8bd122b1ebcba
ms.sourcegitcommit: 4f3ef057a285be2e260615e5d6c41f00d15d08f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94702133"
---
# <a name="hands-free"></a><span data-ttu-id="4f4ce-104">免手动</span><span class="sxs-lookup"><span data-stu-id="4f4ce-104">Hands-free</span></span>

## <a name="scenarios"></a><span data-ttu-id="4f4ce-105">方案</span><span class="sxs-lookup"><span data-stu-id="4f4ce-105">Scenarios</span></span>

<span data-ttu-id="4f4ce-106">如 [交互模型概述](interaction-fundamentals.md)中所述，一旦确定了用户及其目标，就可以在工作完成任务时询问自己面临的环境或环境挑战。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-106">As outlined in the [interaction model overview](interaction-fundamentals.md), once you have identified your users and their goals, ask yourself what environmental or situational challenges they might face as they work to accomplish their tasks.</span></span> <span data-ttu-id="4f4ce-107">例如，许多用户都需要使用自己的动手来实现其真实目标，并且与基于动手的接口的接口交互很困难。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-107">For example, many users need to use their hands to accomplish their real-world goals, and they will have difficulty interacting with a hands-and-controllers based interface.</span></span> 

<span data-ttu-id="4f4ce-108">一些具体方案包括：</span><span class="sxs-lookup"><span data-stu-id="4f4ce-108">Some specific scenarios include:</span></span> 
* <span data-ttu-id="4f4ce-109">在用户双手被占用时引导用户完成任务</span><span class="sxs-lookup"><span data-stu-id="4f4ce-109">Being guided through a task, while the user's hands are busy</span></span>
* <span data-ttu-id="4f4ce-110">在用户双手被占用时参考材料</span><span class="sxs-lookup"><span data-stu-id="4f4ce-110">Referencing materials while the user's hands are busy</span></span>
* <span data-ttu-id="4f4ce-111">手部疲劳</span><span class="sxs-lookup"><span data-stu-id="4f4ce-111">Hand fatigue</span></span>
* <span data-ttu-id="4f4ce-112">无法跟踪手套</span><span class="sxs-lookup"><span data-stu-id="4f4ce-112">Gloves that can't be tracked</span></span>
* <span data-ttu-id="4f4ce-113">手里拿着东西</span><span class="sxs-lookup"><span data-stu-id="4f4ce-113">Carrying something in their hands</span></span>
* <span data-ttu-id="4f4ce-114">社交 awkwardness 来执行大型手势</span><span class="sxs-lookup"><span data-stu-id="4f4ce-114">Social awkwardness to perform large hand gestures</span></span>
* <span data-ttu-id="4f4ce-115">狭小空间</span><span class="sxs-lookup"><span data-stu-id="4f4ce-115">Tight spaces</span></span>


## <a name="hands-free-modalities"></a><span data-ttu-id="4f4ce-116">无人参与情态</span><span class="sxs-lookup"><span data-stu-id="4f4ce-116">Hands-free modalities</span></span>

### <a name="voice-input"></a>[<span data-ttu-id="4f4ce-117">语音输入</span><span class="sxs-lookup"><span data-stu-id="4f4ce-117">Voice input</span></span>](voice-input.md)

<span data-ttu-id="4f4ce-118">使用语音执行命令和控制接口提供了一种便捷的方式来操作，并使用快捷方式灵活地跳过多个步骤（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-118">Using your voice to command and control an interface offers a convenient way to operate hands-free and to use shortcuts to flexibly skip multiple steps if desired.</span></span> <span data-ttu-id="4f4ce-119">使用语音输入，用户只需将任何按钮的名称放在一起即可激活， _( "查看它" )_ ，并与可以完成任务的数字代理进行联系。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-119">With voice input, the user can simply read any button's name out loud to activate it _("see it, say it")_ and converse with a digital agent who can accomplish tasks for you.</span></span>


### <a name="gaze-and-dwell"></a>[<span data-ttu-id="4f4ce-120">凝视和停留</span><span class="sxs-lookup"><span data-stu-id="4f4ce-120">Gaze and dwell</span></span>](gaze-and-dwell.md)

<span data-ttu-id="4f4ce-121">在某些免提情况下，使用语音并不理想或甚至可能。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-121">In some hands-free situations, using your voice is not ideal or even possible.</span></span> <span data-ttu-id="4f4ce-122">很大的工厂环境、隐私或社会规范都可以进行限制。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-122">Loud factory environments, privacy, or social norms can all be constraints.</span></span> <span data-ttu-id="4f4ce-123">"注视 + 停留" 模型允许用户在没有任何其他输入的情况下从其眼睛或打印头导航到应用：用户只需在目标位置) 的 gazing (，并在一段时间内 lingers。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-123">The gaze + dwell model allows the user to navigate an app without any additional input aside from their eye or head gaze: The user simply keeps gazing (with their head or eyes) at the target and lingers there for a moment to activate it.</span></span> <span data-ttu-id="4f4ce-124">若要详细了解注视和停留的各个设计注意事项，请查看 [眼睛和停留和眼睛](gaze-and-dwell-eyes.md) [+ 停留](gaze-and-dwell-head.md)。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-124">To learn more about the individual design considerations for gaze + dwell, check out [eye-gaze + dwell](gaze-and-dwell-eyes.md) and [head-gaze + dwell](gaze-and-dwell-head.md).</span></span>


## <a name="transitioning-in-and-out-of-hands-free"></a><span data-ttu-id="4f4ce-125">转换为无干预</span><span class="sxs-lookup"><span data-stu-id="4f4ce-125">Transitioning in and out of hands-free</span></span>

<span data-ttu-id="4f4ce-126">在这些情况下，让你可以轻松地与用于命令和导航的全息影像进行交互，范围可能是对应用程序的绝对要求，即端到端的应用程序的绝对要求。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-126">For these scenarios, freeing your hands from interacting with holograms for commanding and navigation can range from being an absolute requirement to operating the application, end-to-end, to an added convenience that the user can transition in and out of at any time.</span></span> 

<span data-ttu-id="4f4ce-127">如果应用程序的要求是始终使用免提，无论是通过使用停留、自定义语音命令还是使用单个语音命令，"选择"，都请确保在用户界面中提供合适的便利。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-127">If the requirement of the application is that it will always be used hands-free, whether by using dwell, custom voice commands, or the single voice command, "select", then make sure to make the appropriate accommodations in your UI.</span></span> 

<span data-ttu-id="4f4ce-128">如果你的目标用户需要能够自行从手切换到无人参与，则必须考虑以下原则。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-128">If your target user needs to be able to switch from hands to hands-free at their discretion, then it is important to take the following principles into account.</span></span>

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a><span data-ttu-id="4f4ce-129">假设用户已处于要切换到的模式</span><span class="sxs-lookup"><span data-stu-id="4f4ce-129">Assume the user is already in the mode that they want to switch to</span></span>
<span data-ttu-id="4f4ce-130">例如，如果用户在工厂地面上，观看其 HoloLens 上的视频参考，并决定提起扳手开始工作，则她很可能会开始免费工作，而无需将扳手按下按钮。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-130">For instance, if the user is on the factory floor, watching a video reference on her HoloLens, and decides to pick up a wrench to start working, she most likely would start working in hands-free without having to put down the wrench to press a button.</span></span> <span data-ttu-id="4f4ce-131">她应能够使用语音命令调用语音会话，停留在已可见的 UI 上，开始停留，或说 "选择" 一词。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-131">She should be able to invoke a voice session with a voice command, dwell on an already-visible UI to begin dwell, or say the word "select".</span></span>

<span data-ttu-id="4f4ce-132">用户应该能够：</span><span class="sxs-lookup"><span data-stu-id="4f4ce-132">The user should have the ability to:</span></span> 
* <span data-ttu-id="4f4ce-133">在无人参与的情况下切换到无人参与</span><span class="sxs-lookup"><span data-stu-id="4f4ce-133">Switch to hands-free while hands-free</span></span>
* <span data-ttu-id="4f4ce-134">用双手切换</span><span class="sxs-lookup"><span data-stu-id="4f4ce-134">Switch to hands with your hands</span></span>
* <span data-ttu-id="4f4ce-135">使用控制器切换到控制器</span><span class="sxs-lookup"><span data-stu-id="4f4ce-135">Switch to the controller using a controller</span></span> 

### <a name="create-redundant-ways-to-switch-modes"></a><span data-ttu-id="4f4ce-136">创建冗余方式来切换模式</span><span class="sxs-lookup"><span data-stu-id="4f4ce-136">Create redundant ways to switch modes</span></span>
<span data-ttu-id="4f4ce-137">第一个原则就是访问，另一个原则就是可用性。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-137">While the first principle is about access, the second one is about availability.</span></span> <span data-ttu-id="4f4ce-138">不应该只是一种在模式中执行转换的方法。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-138">There should not just be a single way to transition in and out of a mode.</span></span> 

<span data-ttu-id="4f4ce-139">以下是一些示例：</span><span class="sxs-lookup"><span data-stu-id="4f4ce-139">Some examples would be:</span></span> 
* <span data-ttu-id="4f4ce-140">用于开始语音交互的按钮</span><span class="sxs-lookup"><span data-stu-id="4f4ce-140">A button to begin voice interactions</span></span>
* <span data-ttu-id="4f4ce-141">用于转换到的语音命令，使用打印头和停留</span><span class="sxs-lookup"><span data-stu-id="4f4ce-141">A voice command to transition to, using head-gaze and dwell</span></span>

### <a name="add-a-dash-of-drama"></a><span data-ttu-id="4f4ce-142">添加 drama 的短划线</span><span class="sxs-lookup"><span data-stu-id="4f4ce-142">Add a dash of drama</span></span>
<span data-ttu-id="4f4ce-143">模式切换是一项很重要的事情，这一点很重要，在这些过渡发生时，它们是一种明显的、甚至是一个巨大的交换机，让用户知道发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-143">A mode switch is a big deal--it is important that when these transitions happen that they be an explicit, even a dramatic switch, to let the user know what happened.</span></span> 


## <a name="usability-checklist"></a><span data-ttu-id="4f4ce-144">可用性清单</span><span class="sxs-lookup"><span data-stu-id="4f4ce-144">Usability checklist</span></span>

<span data-ttu-id="4f4ce-145">**用户可以执行所有操作，也可以从端到端免费完成，**</span><span class="sxs-lookup"><span data-stu-id="4f4ce-145">**Can the user do everything and anything hands-free, end-to-end?**</span></span>
* <span data-ttu-id="4f4ce-146">每个种不可交互应可随时访问</span><span class="sxs-lookup"><span data-stu-id="4f4ce-146">Every interactable should be accessible hands-free</span></span>
* <span data-ttu-id="4f4ce-147">确保所有自定义手势都有替换，如调整大小、放置、swipes、点击等。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-147">Ensure that there is a replacement for all custom gestures, such as resizing, placing, swipes, taps, etc.</span></span>
* <span data-ttu-id="4f4ce-148">确保用户完全控制 UI 的存在、位置和详细程度</span><span class="sxs-lookup"><span data-stu-id="4f4ce-148">Ensure that the user has confident control of UI presence, placement, and verbosity at all times</span></span>
    * <span data-ttu-id="4f4ce-149">正在获取 UI</span><span class="sxs-lookup"><span data-stu-id="4f4ce-149">Getting UI out of the way</span></span>
    * <span data-ttu-id="4f4ce-150">对 (FOV) 的视图以外的 UI 进行寻址</span><span class="sxs-lookup"><span data-stu-id="4f4ce-150">Addressing UI that is out of field of view (FOV)</span></span>
    * <span data-ttu-id="4f4ce-151">我看到了多少，</span><span class="sxs-lookup"><span data-stu-id="4f4ce-151">How much I see, where, when</span></span>

<span data-ttu-id="4f4ce-152">**与正确的实用一起教授和加强的交互的机制是什么？**</span><span class="sxs-lookup"><span data-stu-id="4f4ce-152">**Are the mechanics of the interaction being taught and reinforced with the right affordances?**</span></span>

<span data-ttu-id="4f4ce-153">用户了解 .。。</span><span class="sxs-lookup"><span data-stu-id="4f4ce-153">Does the user understand ...</span></span>
* <span data-ttu-id="4f4ce-154">...它们处于哪种模式？</span><span class="sxs-lookup"><span data-stu-id="4f4ce-154">... What mode they are in?</span></span>
* <span data-ttu-id="4f4ce-155">...在此模式下可以执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="4f4ce-155">... What they can do in this mode?</span></span>
* <span data-ttu-id="4f4ce-156">...什么是当前状态？</span><span class="sxs-lookup"><span data-stu-id="4f4ce-156">... What is the current state?</span></span>
* <span data-ttu-id="4f4ce-157">...如何转换？</span><span class="sxs-lookup"><span data-stu-id="4f4ce-157">... How they can transition out?</span></span>
    
<span data-ttu-id="4f4ce-158">**UI 是否经过优化，无人参与？**</span><span class="sxs-lookup"><span data-stu-id="4f4ce-158">**Is the UI optimized for hands-free?**</span></span>   

* <span data-ttu-id="4f4ce-159">示例：停留实用不内置于典型的2D 模式</span><span class="sxs-lookup"><span data-stu-id="4f4ce-159">Example: Dwell affordances are not built-in to typical 2D patterns</span></span>
* <span data-ttu-id="4f4ce-160">示例：语音目标更适合对象突出显示</span><span class="sxs-lookup"><span data-stu-id="4f4ce-160">Example: Voice targeting is better with object highlighting</span></span>
* <span data-ttu-id="4f4ce-161">示例：对于需要打开的标题，语音交互更好</span><span class="sxs-lookup"><span data-stu-id="4f4ce-161">Example: Voice interactions are better with captions that need to be turned on</span></span>


## <a name="see-also"></a><span data-ttu-id="4f4ce-162">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4f4ce-162">See also</span></span>
* [<span data-ttu-id="4f4ce-163">HoloLens 2 中的眼动跟踪</span><span class="sxs-lookup"><span data-stu-id="4f4ce-163">Eye tracking on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="4f4ce-164">凝视和提交</span><span class="sxs-lookup"><span data-stu-id="4f4ce-164">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="4f4ce-165">凝视和停留</span><span class="sxs-lookup"><span data-stu-id="4f4ce-165">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="4f4ce-166">手 - 直接操作</span><span class="sxs-lookup"><span data-stu-id="4f4ce-166">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="4f4ce-167">手 - 手势</span><span class="sxs-lookup"><span data-stu-id="4f4ce-167">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="4f4ce-168">手 - 指向并提交</span><span class="sxs-lookup"><span data-stu-id="4f4ce-168">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="4f4ce-169">本能交互</span><span class="sxs-lookup"><span data-stu-id="4f4ce-169">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="4f4ce-170">语音输入</span><span class="sxs-lookup"><span data-stu-id="4f4ce-170">Voice input</span></span>](voice-input.md)
