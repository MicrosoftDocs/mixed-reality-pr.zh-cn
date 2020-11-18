---
title: 手部和运动控制器
description: 了解免提和运动控制器交互模型，这些模型可删除虚拟与物理之间的边界。
author: shengkait
ms.author: shentan
ms.date: 04/26/2019
ms.topic: article
keywords: 混合现实，动手，运动控制器，交互，设计，混合现实耳机，windows mixed reality 耳机，虚拟现实耳机，HoloLens，MRTK，混合现实工具包
ms.openlocfilehash: e931e5ec11548d9aab0d1dd7f8921dbc7554abab
ms.sourcegitcommit: 4f3ef057a285be2e260615e5d6c41f00d15d08f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94702153"
---
# <a name="hands-and-motion-controllers"></a><span data-ttu-id="07ed4-104">手部和运动控制器</span><span class="sxs-lookup"><span data-stu-id="07ed4-104">Hands and motion controllers</span></span>
## <a name="scenarios"></a><span data-ttu-id="07ed4-105">方案</span><span class="sxs-lookup"><span data-stu-id="07ed4-105">Scenarios</span></span>
<span data-ttu-id="07ed4-106">如果在阅读 [交互概述](interaction-fundamentals.md)后选择采用此交互模型，这意味着您正在开发一个应用程序，要求用户使用两次手与全息世界交互。</span><span class="sxs-lookup"><span data-stu-id="07ed4-106">If you choose to adopt this interaction model after reading the [interaction overview](interaction-fundamentals.md), it means that you are developing an application requiring users to use two hands to interact with the holographic world.</span></span> <span data-ttu-id="07ed4-107">您的应用程序将实现删除虚拟与物理之间边界的目标。</span><span class="sxs-lookup"><span data-stu-id="07ed4-107">Your application is going to achieve the goal of removing the boundary between virtual and physical.</span></span>

<span data-ttu-id="07ed4-108">某些特定情况可能如下：</span><span class="sxs-lookup"><span data-stu-id="07ed4-108">Some specific scenarios might be:</span></span>
* <span data-ttu-id="07ed4-109">为信息工作者提供包含 UI 的 2D 虚拟屏幕来显示和控制内容</span><span class="sxs-lookup"><span data-stu-id="07ed4-109">Providing information workers 2D virtual screens with UI affordances to display and control content</span></span>
* <span data-ttu-id="07ed4-110">为工厂程序集线提供第一行工作人员教程和指南</span><span class="sxs-lookup"><span data-stu-id="07ed4-110">Providing first line workers tutorials and guides for factory assembly lines</span></span>
* <span data-ttu-id="07ed4-111">开发用于协助和教育医疗专业人员的专业工具</span><span class="sxs-lookup"><span data-stu-id="07ed4-111">Developing professional tools for assisting and educating medical professionals</span></span>  
* <span data-ttu-id="07ed4-112">使用 3D 虚拟对象来装饰现实世界，或创建第二世界</span><span class="sxs-lookup"><span data-stu-id="07ed4-112">Using 3D virtual objects to decorate the real world or to create a second world</span></span> 
* <span data-ttu-id="07ed4-113">以现实世界为背景创建基于位置的服务和游戏</span><span class="sxs-lookup"><span data-stu-id="07ed4-113">Creating location-based services and games using the real world as a background</span></span>

<br>

---

## <a name="hands-and-motion-controllers-modalities"></a><span data-ttu-id="07ed4-114">双手和运动控制器情态</span><span class="sxs-lookup"><span data-stu-id="07ed4-114">Hands and motion controllers modalities</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="07ed4-115">[![用手直接操作](images/hands-and-controllers-direct-manipulation.jpg)](direct-manipulation.md)</span><span class="sxs-lookup"><span data-stu-id="07ed4-115">[![Direct manipulation with hands](images/hands-and-controllers-direct-manipulation.jpg)](direct-manipulation.md)</span></span><br>
       ### <a name="direct-manipulation-with-handsbr"></a>[<span data-ttu-id="07ed4-116">使用手直接操作</span><span class="sxs-lookup"><span data-stu-id="07ed4-116">Direct manipulation with hands</span></span>](direct-manipulation.md)<br>
       <span data-ttu-id="07ed4-117">这是一种使用手的强大功能的模态，用户可以直接接触和操作全息影像。</span><span class="sxs-lookup"><span data-stu-id="07ed4-117">This is a modality leveraging the power of hands, with which users are capable of touching and manipulating the holograms directly.</span></span> <span data-ttu-id="07ed4-118">通过利用日常经验并提供适当的视觉实用，用户可以使用相同的方法来操作现实世界对象，以便与虚拟对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="07ed4-118">By leveraging daily life experiences and providing proper visual affordances, users are able to use the same way of manipulating real world objects to interact with virtual ones.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="07ed4-119">[![使用手指向和提交](images/hands-and-controllers-point-and-commit.jpg)](point-and-commit.md)</span><span class="sxs-lookup"><span data-stu-id="07ed4-119">[![Point and commit with hands](images/hands-and-controllers-point-and-commit.jpg)](point-and-commit.md)</span></span><br>
        ### <a name="point-and-commit-with-handsbr"></a>[<span data-ttu-id="07ed4-120">使用手指向和提交</span><span class="sxs-lookup"><span data-stu-id="07ed4-120">Point and commit with hands</span></span>](point-and-commit.md)<br>
        <span data-ttu-id="07ed4-121">这种模态使用户能够在远处与全息影像交互。</span><span class="sxs-lookup"><span data-stu-id="07ed4-121">This modality empowers users to interact with holograms in a distance.</span></span> <span data-ttu-id="07ed4-122">它使用户能够充分利用环境。</span><span class="sxs-lookup"><span data-stu-id="07ed4-122">It enables users to make the best use of surroundings.</span></span> <span data-ttu-id="07ed4-123">用户可以在任何位置放置全息影像，同时仍然可以从任意距离访问。</span><span class="sxs-lookup"><span data-stu-id="07ed4-123">Users can place holograms anywhere and still access them from any distance.</span></span> <span data-ttu-id="07ed4-124">用于控制和操作2D 和3D 全息影像的心理模型和手势与直接操作的情况有关。</span><span class="sxs-lookup"><span data-stu-id="07ed4-124">The mental models and gestures for controlling and manipulating 2D and 3D holograms are highly in sync with those of direct manipulation.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="07ed4-125">[![运动控制器](images/hands-and-controllers-motion-controllers.jpg)](motion-controllers.md)</span><span class="sxs-lookup"><span data-stu-id="07ed4-125">[![Motion controllers](images/hands-and-controllers-motion-controllers.jpg)](motion-controllers.md)</span></span><br>
       ### <a name="motion-controllersbr"></a>[<span data-ttu-id="07ed4-126">运动控制器</span><span class="sxs-lookup"><span data-stu-id="07ed4-126">Motion controllers</span></span>](motion-controllers.md)<br>
       <span data-ttu-id="07ed4-127">运动控制器是通过在使用一种或两种手时跨大量距离提供精确交互来扩展用户的物理功能的工具。</span><span class="sxs-lookup"><span data-stu-id="07ed4-127">Motion controllers are tools that extend the user's physical capabilities by providing precise interactions across a large range of distances while using one or both hands.</span></span> <span data-ttu-id="07ed4-128">这些硬件附件提供了许多常用交互的快捷方式，并为各种操作提供了 surefooted、tactile 的反馈。</span><span class="sxs-lookup"><span data-stu-id="07ed4-128">These hardware accessories provide shortcuts to many commonly-used interactions and provide surefooted, tactile feedback for a variety of actions.</span></span> <span data-ttu-id="07ed4-129">目前，运动控制器仅适用于 Windows Mixed Reality (WMR) 方案。</span><span class="sxs-lookup"><span data-stu-id="07ed4-129">Currently, motion controllers are only available for Windows Mixed Reality (WMR) scenarios.</span></span> 
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a><span data-ttu-id="07ed4-130">另请参阅</span><span class="sxs-lookup"><span data-stu-id="07ed4-130">See also</span></span>
* [<span data-ttu-id="07ed4-131">头部凝视并提交</span><span class="sxs-lookup"><span data-stu-id="07ed4-131">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="07ed4-132">头部凝视和停留</span><span class="sxs-lookup"><span data-stu-id="07ed4-132">Head-gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="07ed4-133">使用手直接操作</span><span class="sxs-lookup"><span data-stu-id="07ed4-133">Direct manipulation with hands</span></span>](direct-manipulation.md)
* [<span data-ttu-id="07ed4-134">使用手指向和提交</span><span class="sxs-lookup"><span data-stu-id="07ed4-134">Point and commit with hands</span></span>](point-and-commit.md)
* [<span data-ttu-id="07ed4-135">免动手操作</span><span class="sxs-lookup"><span data-stu-id="07ed4-135">Hands-free</span></span>](hands-free.md)
