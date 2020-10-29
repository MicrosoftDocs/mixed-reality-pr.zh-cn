---
title: 缩放
description: 如果要显示看起来十分逼真的全息形式的内容，其关键是尽可能真实地模拟现实世界的视觉统计数据。
author: shengkait
ms.author: shentan
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality，样式，设计
ms.openlocfilehash: a9a02d681986df3d73c7990fc975e659e5326981
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91677134"
---
# <a name="scale"></a><span data-ttu-id="92e7d-104">缩放</span><span class="sxs-lookup"><span data-stu-id="92e7d-104">Scale</span></span>

<span data-ttu-id="92e7d-105">如果要显示看起来十分逼真的全息形式的内容，其关键是尽可能真实地模拟现实世界的视觉统计数据。</span><span class="sxs-lookup"><span data-stu-id="92e7d-105">A key to displaying content that looks realistic in holographic form is to mimic the visual statistics of the real world as closely as possible.</span></span> <span data-ttu-id="92e7d-106">这意味着将尽可能多的、可以帮助我们（在现实世界中）了解对象的位置、大小及其组成部分的视觉提示整合在一起。</span><span class="sxs-lookup"><span data-stu-id="92e7d-106">This means incorporating as many of the visual cues as we can that help us (in the real world) understand where objects are, how big they are, and what they’re made of.</span></span> <span data-ttu-id="92e7d-107">对象的小数位数是这些视觉对象提示中最重要的一种，为查看器提供对象的大小并提示其位置 (尤其是对于具有已知大小) 的对象。</span><span class="sxs-lookup"><span data-stu-id="92e7d-107">The scale of an object is one of the most important of those visual cues, giving a viewer a sense of the size of an object as well as cues to its location (especially for objects which have a known size).</span></span> <span data-ttu-id="92e7d-108">此外，查看真实规模的对象已被视为一般的混合现实中的一个关键体验优势，即以前不能在屏幕上查看的内容。</span><span class="sxs-lookup"><span data-stu-id="92e7d-108">Further, viewing objects at real scale has been seen as one of the key experience differentiators for mixed reality in general – something that hasn’t been possible on screen-based viewing previously.</span></span>

<br>

---

## <a name="how-to-suggest-the-scale-of-objects-and-environments"></a><span data-ttu-id="92e7d-109">如何建议对象和环境的规模</span><span class="sxs-lookup"><span data-stu-id="92e7d-109">How to suggest the scale of objects and environments</span></span>

<span data-ttu-id="92e7d-110">有多种方法可建议对象的规模，其中一些方法可能会对其他可感知因素产生影响。</span><span class="sxs-lookup"><span data-stu-id="92e7d-110">There are many ways to suggest the scale of an object, some of which have possible effects on other perceptual factors.</span></span> <span data-ttu-id="92e7d-111">第一项是只显示 "真实" 大小的对象，并在用户移动时保持真实大小。</span><span class="sxs-lookup"><span data-stu-id="92e7d-111">The key one is to simply display objects at a ‘real’ size, and maintain that realistic size as users move.</span></span> <span data-ttu-id="92e7d-112">这意味着，全息影像会占用用户的用户视觉角度，因为这些用户的视觉对象比实际对象更近或更远。</span><span class="sxs-lookup"><span data-stu-id="92e7d-112">This means holograms will take up a different amount of a user’s visual angle of a user as they come closer or further away, the same way that real objects do.</span></span>

### <a name="utilize-the-distance-of-objects-as-they-are-presented-to-the-user"></a><span data-ttu-id="92e7d-113">利用对象在向用户显示时的距离</span><span class="sxs-lookup"><span data-stu-id="92e7d-113">Utilize the distance of objects as they are presented to the user</span></span>

<span data-ttu-id="92e7d-114">一种常见方法是利用对象在向用户显示时的距离。</span><span class="sxs-lookup"><span data-stu-id="92e7d-114">One common method is to utilize the distance of objects as they are presented to the user.</span></span> <span data-ttu-id="92e7d-115">例如，请考虑在用户的正面直观呈现大型家族汽车。</span><span class="sxs-lookup"><span data-stu-id="92e7d-115">For example, consider visualizing a large family car in front of the user.</span></span> <span data-ttu-id="92e7d-116">如果轿车直接位于其前面，则在 arm 的长度内，可能会太大而无法容纳在用户的视图中。</span><span class="sxs-lookup"><span data-stu-id="92e7d-116">If the car were directly in front of them, within arm’s length, it would be too large to fit in the user’s field of view.</span></span> <span data-ttu-id="92e7d-117">这将要求用户移动其头和正文以了解对象的整体。</span><span class="sxs-lookup"><span data-stu-id="92e7d-117">This would require the user to move their head and body to understand the entirety of the object.</span></span> <span data-ttu-id="92e7d-118">如果将汽车置于房间外 () ，则用户可以通过在其视图字段中查看全部对象来建立一种规模，然后将其移动到更靠近它的位置来更详细地检查区域。</span><span class="sxs-lookup"><span data-stu-id="92e7d-118">If the car were placed further away (across the room), the user can establish a sense of scale by seeing the entirety of the object in their field of view, then moving themselves closer to it to inspect areas in detail.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="92e7d-119">**[Volvo 使用此方法为新汽车创造了 showroom](https://www.youtube.com/watch?v=DilzwF90vec)** 的体验，利用全息汽车的规模，以一种对用户来说切实可行、直观的方式。</span><span class="sxs-lookup"><span data-stu-id="92e7d-119">**[Volvo used this technique to create a showroom](https://www.youtube.com/watch?v=DilzwF90vec)** experience for a new car, utilizing the scale of the holographic car in a way that felt realistic and intuitive to the user.</span></span> <span data-ttu-id="92e7d-120">此体验始于一个物理表中的汽车全息图，使用户能够了解模型的总大小和形状。</span><span class="sxs-lookup"><span data-stu-id="92e7d-120">The experience begins with a hologram of the car on a physical table, allowing the user to understand the total size and shape of the model.</span></span> <span data-ttu-id="92e7d-121">在此体验中，汽车扩展到的 (超出了设备的视图) 大小，但由于用户已从较小的模型获取了引用帧，因此可以充分地浏览汽车的功能。</span><span class="sxs-lookup"><span data-stu-id="92e7d-121">Later in the experience, the car expands to a larger scale (beyond the size of the device's field of view) but, since the user already acquired a frame of reference from the smaller model, they can adequately navigate around features of the car.</span></span><br>
        <br>
        <span data-ttu-id="92e7d-122">*图像： Volvo 汽车的 HoloLens 体验*</span><span class="sxs-lookup"><span data-stu-id="92e7d-122">*Image: Volvo Cars experience for HoloLens*</span></span>
    :::column-end:::
        :::column:::
       ![HoloLens 的 Volvo 汽车体验](images/volvo-cars-microsoft-hololens-experience01-640px.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---

### <a name="use-holograms-to-modify-the-users-real-space"></a><span data-ttu-id="92e7d-124">使用全息影像修改用户的真实空间</span><span class="sxs-lookup"><span data-stu-id="92e7d-124">Use holograms to modify the user's real space</span></span>

<span data-ttu-id="92e7d-125">另一种方法是使用全息影像来修改用户的实际空间，将现有的墙壁或上限替换为环境，或者追加 "洞" 或 "windows"，允许大小过度的对象看似 "突破" 物理空间。</span><span class="sxs-lookup"><span data-stu-id="92e7d-125">Another method is to use holograms to modify the user's real space, replacing the existing walls or ceilings with environments or appending ‘holes’ or ‘windows’, allowing over-sized objects to seemingly 'break-through' the physical space.</span></span> <span data-ttu-id="92e7d-126">例如，大型树可能不适合大多数用户的生活空间，但通过将虚拟天空置于天花板上，物理空间将扩展到虚拟。</span><span class="sxs-lookup"><span data-stu-id="92e7d-126">For example, a large tree might not fit in most users’ living rooms, but by putting a virtual sky on their ceiling, the physical space expands into the virtual.</span></span> <span data-ttu-id="92e7d-127">这样，用户就可以在虚拟树的基础上进行探讨，并收集它在现实生活中的显示方式，并查看它是否超出了房间的物理空间。</span><span class="sxs-lookup"><span data-stu-id="92e7d-127">This allows the user to walk around the base of the virtual tree, and gather a sense of scale of how it would appear in real life, then look up to see it extend far beyond the physical space of the room.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="92e7d-128">**[Minecraft 开发了](https://minecraft.net/)** 使用类似技术的概念。</span><span class="sxs-lookup"><span data-stu-id="92e7d-128">**[Minecraft developed a concept experiences](https://minecraft.net/)** using a similar technique.</span></span> <span data-ttu-id="92e7d-129">通过将虚拟窗口添加到房间中的物理表面上，房间中的现有对象会置于更大的环境中，而不会超出空间的物理规模限制。</span><span class="sxs-lookup"><span data-stu-id="92e7d-129">By adding a virtual window to a physical surface in a room, the existing objects in the room are placed in the context of a vastly larger environment, beyond the physical scale limitations of the room.</span></span><br>
        <br>
        <span data-ttu-id="92e7d-130">*Image： HoloLens 的 Minecraft 概念体验*</span><span class="sxs-lookup"><span data-stu-id="92e7d-130">*Image: Minecraft concept experience for HoloLens*</span></span>
    :::column-end:::
        :::column:::
       ![HoloLens 的 Minecraft 概念体验](images/800px-minecraftwindow-640px.jpg)<br><br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="experimenting-with-scale"></a><span data-ttu-id="92e7d-132">进行大规模试验</span><span class="sxs-lookup"><span data-stu-id="92e7d-132">Experimenting with scale</span></span>

<span data-ttu-id="92e7d-133">在某些情况下，设计人员 vspackage 通过更改对象的显示 "真正" 大小来修改缩放 () 同时保持对象的单个位置，以使对象接近或更接近查看器而不进行任何实际移动。</span><span class="sxs-lookup"><span data-stu-id="92e7d-133">In some cases, designers have experimented with modifying the scale (by changing the displayed ‘real’ size of the object) while maintaining a single position of the object, to approximate an object getting closer or further to a viewer without any actual movement.</span></span> <span data-ttu-id="92e7d-134">在某些情况下，在某些情况下会对此进行测试，这是一种模拟多个项的方式，同时仍然遵从查看虚拟内容的可能舒适的限制，而不会建议使用。</span><span class="sxs-lookup"><span data-stu-id="92e7d-134">This was tested in some cases as a way to simulate up-close viewing of items while still respecting potential comfort limitations of viewing virtual content closer than the “zone of comfort” would suggest.</span></span>

<span data-ttu-id="92e7d-135">但这可能会在经验中创建几个可能的项目：</span><span class="sxs-lookup"><span data-stu-id="92e7d-135">This can create a few possible artifacts in the experience however:</span></span>
* <span data-ttu-id="92e7d-136">对于表示查看器大小为 "已知" 的对象的虚拟对象，在不更改位置的情况下更改缩放将导致出现冲突的视觉提示，该眼睛仍可能会因为 vergence (提示而在某种程度) 上看到对象[Comfort](comfort.md) ，但大小是 monocular 的，提示对象可能会更接近。</span><span class="sxs-lookup"><span data-stu-id="92e7d-136">For virtual objects that represent some object with a ‘known’ size to the viewer, changing the scale without changing the position leads to conflicting visual cues – the eyes may still ‘see’ the object at some depth due to vergence cues (see the [Comfort](comfort.md) article for more on this), but the size acts as a monocular cue that the object might be getting closer.</span></span> <span data-ttu-id="92e7d-137">这些冲突的提示会导致混乱的认知，查看器通常会将对象视为就地 (由于恒定的深度提示) 但会迅速增长。</span><span class="sxs-lookup"><span data-stu-id="92e7d-137">These conflicting cues lead to confused perceptions – viewers often see the object as staying in place (due to the constant depth cue) but growing rapidly.</span></span>
* <span data-ttu-id="92e7d-138">在某些情况下，更改规模会被视为 "临近" 提示，在该对象中，可能会或不会看到对象通过查看器进行缩放，但看起来像是在查看者的眼睛 (，这可能是成名的) 。</span><span class="sxs-lookup"><span data-stu-id="92e7d-138">In some cases, change of scale is seen as a ‘looming’ cue instead, where the object may or may not be seen to change scale by a viewer, but does appear to be moving directly toward the viewer’s eyes (which can be an uncomfortable sensation).</span></span>
* <span data-ttu-id="92e7d-139">在现实世界中的比较面上，此类缩放更改有时会被视为随着多个轴的变化位置，在某些情况) 下，对象可能看起来降低，而不是以更近的方向 (类似于三维移动的2D 投影。</span><span class="sxs-lookup"><span data-stu-id="92e7d-139">With comparison surfaces in the real world, such scaling changes are sometimes seen as changing position along multiple axes – objects may appear to drop lower instead of moving closer (similar in a 2D projection of 3D movement in some cases).</span></span>
* <span data-ttu-id="92e7d-140">最后，对于没有已知 "实际大小" 的对象 (例如任意大小、UI 元素 ) 等的任意形状），更改规模可能会以某种方式进行操作，以模拟距离变化–查看器不具有与对象的真实大小或位置有关的任何预先存在的自顶向下提示，因此可将该刻度作为更重要的提示进行处理。</span><span class="sxs-lookup"><span data-stu-id="92e7d-140">Finally, for objects without a known ‘real world’ size (e.g. arbitrary shapes with arbitrary sizes, UI elements, etc.), changing scale may act functionally as a way to mimic changes in distance – viewers do not have as many preexisting top-down cues by which to understand the object’s true size or location, so the scale can be processed as a more important cue.</span></span>

<br>

---

## <a name="see-also"></a><span data-ttu-id="92e7d-141">请参阅</span><span class="sxs-lookup"><span data-stu-id="92e7d-141">See also</span></span>
* [<span data-ttu-id="92e7d-142">颜色、光线和材料</span><span class="sxs-lookup"><span data-stu-id="92e7d-142">Color, light and materials</span></span>](../color,-light-and-materials.md)
* [<span data-ttu-id="92e7d-143">版式</span><span class="sxs-lookup"><span data-stu-id="92e7d-143">Typography</span></span>](typography.md)
* [<span data-ttu-id="92e7d-144">空间音效设计</span><span class="sxs-lookup"><span data-stu-id="92e7d-144">Spatial sound design</span></span>](spatial-sound-design.md)
