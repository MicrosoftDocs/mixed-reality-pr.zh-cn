---
title: Unity 播放模式
description: 在 Unity 编辑器中使用播放模式，无需部署应用即可在设备上预览所做的更改。
author: jonmlyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity、远程处理、全息远程处理、全息远程处理播放器
ms.openlocfilehash: 4239eba84bd94c0bdc596392fdf7a0c780778850
ms.sourcegitcommit: 520c69eb761ad6083b36f448bbcfab89e343e40d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549090"
---
# <a name="unity-play-mode"></a><span data-ttu-id="06c74-104">Unity 播放模式</span><span class="sxs-lookup"><span data-stu-id="06c74-104">Unity Play Mode</span></span>

<span data-ttu-id="06c74-105">处理 Unity 项目的快速方法是使用 "播放模式"。</span><span class="sxs-lookup"><span data-stu-id="06c74-105">A fast way to work on your Unity project is to use "Play Mode".</span></span> <span data-ttu-id="06c74-106">这会在你的电脑上以本地方式在 Unity 编辑器中运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="06c74-106">This runs your app locally in the Unity editor on your PC.</span></span> <span data-ttu-id="06c74-107">Unity 使用全息远程处理提供一种在真实的 HoloLens 设备上快速预览内容的方式。</span><span class="sxs-lookup"><span data-stu-id="06c74-107">Unity uses Holographic Remoting to provide a fast way to preview your content on a real HoloLens device.</span></span> <span data-ttu-id="06c74-108">播放模式还可与附加到开发 PC 的 Windows Mixed Reality 耳机一起使用。</span><span class="sxs-lookup"><span data-stu-id="06c74-108">Play Mode can also be used with a Windows Mixed Reality headset attached to your development PC.</span></span>

## <a name="unity-play-mode-with-holographic-remoting"></a><span data-ttu-id="06c74-109">采用全息远程处理的 Unity 播放模式</span><span class="sxs-lookup"><span data-stu-id="06c74-109">Unity Play Mode with Holographic Remoting</span></span>

<span data-ttu-id="06c74-110">通过全息远程处理，你可以在 HoloLens 上体验你的应用程序，而在你的电脑上运行 Unity 编辑器。</span><span class="sxs-lookup"><span data-stu-id="06c74-110">With Holographic Remoting, you can experience your app on the HoloLens, while it runs in the Unity editor on your PC.</span></span> <span data-ttu-id="06c74-111">注视、手势、语音和空间映射输入将从你的 HoloLens 发送到你的电脑。</span><span class="sxs-lookup"><span data-stu-id="06c74-111">Gaze, gesture, voice, and spatial mapping input is sent from your HoloLens to your PC.</span></span> <span data-ttu-id="06c74-112">然后，将呈现的帧发送回 HoloLens。</span><span class="sxs-lookup"><span data-stu-id="06c74-112">Rendered frames are then sent back to your HoloLens.</span></span> <span data-ttu-id="06c74-113">这是一种快速调试应用程序的绝佳方式，无需生成和部署完整项目。</span><span class="sxs-lookup"><span data-stu-id="06c74-113">This is a great way to quickly debug your app without building and deploying a full project.</span></span>
1. <span data-ttu-id="06c74-114">在 HoloLens 上，中转到 **Microsoft Store** 并安装 **[全息远程处理播放器](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** 应用。</span><span class="sxs-lookup"><span data-stu-id="06c74-114">On your HoloLens, go to the **Microsoft Store** and install the **[Holographic Remoting Player](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** app.</span></span>
2. <span data-ttu-id="06c74-115">在 HoloLens 上，启动 **全息远程处理播放器** 应用。</span><span class="sxs-lookup"><span data-stu-id="06c74-115">On your HoloLens, start the **Holographic Remoting Player** app.</span></span>
3. <span data-ttu-id="06c74-116">在 Unity 中，单击 " **窗口** " 菜单，展开 " **XR** " 子菜单，然后选择 " **全息模拟** "。</span><span class="sxs-lookup"><span data-stu-id="06c74-116">In Unity, go to the **Window** menu, expand the **XR** sub-menu, and select **Holographic Emulation**.</span></span>
4. <span data-ttu-id="06c74-117">将 **仿真模式** 设置为 **远程设备** 。</span><span class="sxs-lookup"><span data-stu-id="06c74-117">Set **Emulation Mode** to **Remote to Device**.</span></span>
5. <span data-ttu-id="06c74-118">对于 **远程计算机** ，请输入 HOLOLENS 的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="06c74-118">For **Remote Machine** , enter the IP address of your HoloLens.</span></span>
6. <span data-ttu-id="06c74-119">单击“连接”。</span><span class="sxs-lookup"><span data-stu-id="06c74-119">Click **Connect**.</span></span> <span data-ttu-id="06c74-120">应会看到 **连接状态** 更改为 " **已连接** "，并且会在 HoloLens 中看到屏幕显示为空白。</span><span class="sxs-lookup"><span data-stu-id="06c74-120">You should see **Connection Status** change to **Connected** and see the screen go blank in the HoloLens.</span></span>
7. <span data-ttu-id="06c74-121">单击 " **播放** " 按钮以启动播放模式，并在 HoloLens 上体验应用。</span><span class="sxs-lookup"><span data-stu-id="06c74-121">Click the **Play** button to start Play Mode and experience the app on your HoloLens.</span></span>

<span data-ttu-id="06c74-122">全息远程处理需要快速的 PC 和 Wi-Fi 的连接。</span><span class="sxs-lookup"><span data-stu-id="06c74-122">Holographic Remoting requires a fast PC and Wi-Fi connection.</span></span> <span data-ttu-id="06c74-123">有关完整详细信息，请参阅 [全息远程处理播放器](../platform-capabilities-and-apis/holographic-remoting-player.md) 。</span><span class="sxs-lookup"><span data-stu-id="06c74-123">See [Holographic Remoting Player](../platform-capabilities-and-apis/holographic-remoting-player.md) for full details.</span></span>

<span data-ttu-id="06c74-124">为了获得最佳结果，请确保应用正确设置了 [焦点](focus-point-in-unity.md)。</span><span class="sxs-lookup"><span data-stu-id="06c74-124">For best results, make sure your app properly sets the [focus point](focus-point-in-unity.md).</span></span> <span data-ttu-id="06c74-125">这有助于全息远程处理最好地使场景适应无线连接的延迟。</span><span class="sxs-lookup"><span data-stu-id="06c74-125">This helps Holographic Remoting to best adapt your scene to the latency of your wireless connection.</span></span>

## <a name="see-also"></a><span data-ttu-id="06c74-126">另请参阅</span><span class="sxs-lookup"><span data-stu-id="06c74-126">See Also</span></span>
* [<span data-ttu-id="06c74-127">全息远程播放器</span><span class="sxs-lookup"><span data-stu-id="06c74-127">Holographic Remoting Player</span></span>](../platform-capabilities-and-apis/holographic-remoting-player.md)
