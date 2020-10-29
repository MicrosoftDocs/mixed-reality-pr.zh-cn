---
title: WebVR 概述
description: 使用和开发 Windows Mixed Reality 中的 WebVR 概述
author: yonet
ms.author: ayyonet
ms.date: 04/10/2020
ms.topic: article
keywords: WebVR，WebXR，WinMR，WebAR，web vr，web xr，web mr，web ar，360，360视频，360视频，360照片，360照片，360内容，沉浸式 web，immersiveweb，IW
ms.openlocfilehash: fdff2acf7816f36129d867650b16d9760a92e375
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91678929"
---
# <a name="webvr-overview"></a><span data-ttu-id="d28c5-104">WebVR 概述</span><span class="sxs-lookup"><span data-stu-id="d28c5-104">WebVR Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d28c5-105">**WebVR 1.1 api** s 已弃用，并已替换为 **WebXR 设备 API** s。</span><span class="sxs-lookup"><span data-stu-id="d28c5-105">**WebVR 1.1 API** s are deprecated and replaced by **WebXR Device API** s.</span></span>

<span data-ttu-id="d28c5-106">WebVR 1.1 Api 已弃用，并已从 Chrome 和新的 Microsoft Edge 中删除。</span><span class="sxs-lookup"><span data-stu-id="d28c5-106">WebVR 1.1 APIs are deprecated and removed from Chrome and the new Microsoft Edge.</span></span> <span data-ttu-id="d28c5-107">WebVR Api 由 WebXR 设备 Api 取代。</span><span class="sxs-lookup"><span data-stu-id="d28c5-107">WebVR APIs are superseded by WebXR Device APIs.</span></span> <span data-ttu-id="d28c5-108">可以在 [caniuse.com](https://caniuse.com/#search=webvr)上检查当前支持 WebVR api 的浏览器列表。</span><span class="sxs-lookup"><span data-stu-id="d28c5-108">You can check the list of browsers currently supporting WebVR APIs on [caniuse.com](https://caniuse.com/#search=webvr).</span></span>

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="d28c5-109">查看 Windows Mixed Reality 沉浸式耳机中的 WebVR 内容</span><span class="sxs-lookup"><span data-stu-id="d28c5-109">Viewing WebVR content in Windows Mixed Reality immersive headsets</span></span>

<span data-ttu-id="d28c5-110">有关如何在 WebVR 的 **Microsoft Edge (15-18)** 中访问沉浸式耳机中的内容的说明，请参阅 [发烧指南](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr)。</span><span class="sxs-lookup"><span data-stu-id="d28c5-110">Instructions for accessing WebVR content in your immersive headsets with **older versions of Microsoft Edge(15-18)** can be found in the [Enthusiast's Guide](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span></span> <span data-ttu-id="d28c5-111">可以通过在 Edge 浏览器搜索栏中键入 "edge://version/" 来检查边缘版本。</span><span class="sxs-lookup"><span data-stu-id="d28c5-111">You can check your edge version by typing "edge://version/" in your Edge browsers search bar.</span></span>

## <a name="see-also"></a><span data-ttu-id="d28c5-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d28c5-112">See Also</span></span>

* [<span data-ttu-id="d28c5-113">WebXR 概述</span><span class="sxs-lookup"><span data-stu-id="d28c5-113">WebXR Overview</span></span>](webxr-overview.md)
* [<span data-ttu-id="d28c5-114">WebXR 设备 API 规范</span><span class="sxs-lookup"><span data-stu-id="d28c5-114">WebXR Device API specification</span></span>](https://immersive-web.github.io/webxr/)
* [<span data-ttu-id="d28c5-115">Windows Mixed Reality 和新的 Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d28c5-115">Windows Mixed Reality and the new Microsoft Edge</span></span>](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge)
* [<span data-ttu-id="d28c5-116">WebVR 信息</span><span class="sxs-lookup"><span data-stu-id="d28c5-116">WebVR information</span></span>](https://webvr.info)
* [<span data-ttu-id="d28c5-117">WebVR 规范</span><span class="sxs-lookup"><span data-stu-id="d28c5-117">WebVR specification</span></span>](https://w3c.github.io/webvr/)
* <span data-ttu-id="d28c5-118">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="d28c5-118">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span></span>
* <span data-ttu-id="d28c5-119">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="d28c5-119">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span></span>
* <span data-ttu-id="d28c5-120">[游戏板 API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) 和 [游戏板扩展](https://w3c.github.io/gamepad/extensions.html)</span><span class="sxs-lookup"><span data-stu-id="d28c5-120">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) and [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span></span>
* [<span data-ttu-id="d28c5-121">处理 WebGL 中丢失的上下文</span><span class="sxs-lookup"><span data-stu-id="d28c5-121">Handling Lost Context in WebGL</span></span>](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [<span data-ttu-id="d28c5-122">Pointerlock</span><span class="sxs-lookup"><span data-stu-id="d28c5-122">Pointerlock</span></span>](https://www.w3.org/TR/pointerlock/)
* [<span data-ttu-id="d28c5-123">glTF</span><span class="sxs-lookup"><span data-stu-id="d28c5-123">glTF</span></span>](https://www.khronos.org/gltf)
* [<span data-ttu-id="d28c5-124">使用 Babylon.js 启用 WebVR</span><span class="sxs-lookup"><span data-stu-id="d28c5-124">Using Babylon.js to enable WebVR</span></span>](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)
