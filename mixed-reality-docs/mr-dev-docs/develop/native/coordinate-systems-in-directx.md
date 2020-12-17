---
title: DirectX 中的坐标系统
description: 了解如何在 DirectX 中协调系统，以及如何利用空间定位器、参考框架和空间锚点实现混合现实。 使用 SpatialStage 和处理跟踪丢失，保存和加载定位点，以及图像稳定性。
author: thetuvix
ms.author: alexturn
ms.date: 08/04/2020
ms.topic: article
keywords: 混合现实，空间定位器，空间参考框架，空间坐标系统，空间贴图，示例代码，图像稳定，空间锚，空间锚定存储，跟踪丢失，演练，混合现实耳机，windows mixed Reality 耳机，虚拟现实耳机
ms.openlocfilehash: 7bf2309f3fb6264d6b1a5232f7ead78b771c1649
ms.sourcegitcommit: 2bf79eef6a9b845494484f458443ef4f89d7efc0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97613111"
---
# <a name="coordinate-systems-in-directx"></a><span data-ttu-id="c0967-105">DirectX 中的坐标系统</span><span class="sxs-lookup"><span data-stu-id="c0967-105">Coordinate systems in DirectX</span></span>

> [!NOTE]
> <span data-ttu-id="c0967-106">本文与旧版 WinRT 本机 Api 相关。</span><span class="sxs-lookup"><span data-stu-id="c0967-106">This article relates to the legacy WinRT native APIs.</span></span>  <span data-ttu-id="c0967-107">对于新的本机应用项目，建议使用 **[OPENXR API](openxr-getting-started.md)**。</span><span class="sxs-lookup"><span data-stu-id="c0967-107">For new native app projects, we recommend using the **[OpenXR API](openxr-getting-started.md)**.</span></span>

<span data-ttu-id="c0967-108">[坐标系统](../../design/coordinate-systems.md) 构成 Windows Mixed Reality api 提供的空间理解的基础。</span><span class="sxs-lookup"><span data-stu-id="c0967-108">[Coordinate systems](../../design/coordinate-systems.md) form the basis for spatial understanding offered by Windows Mixed Reality APIs.</span></span>

<span data-ttu-id="c0967-109">如今，原来的 VR 或单一房间的 vr 设备为其所跟踪的空间建立了一个主坐标系。</span><span class="sxs-lookup"><span data-stu-id="c0967-109">Today's seated VR or single-room VR devices establish one primary coordinate system for their tracked space.</span></span> <span data-ttu-id="c0967-110">适用于较大未定义环境的混合现实设备是为大型未定义环境设计的，在用户浏览时，设备会发现并了解其环境。</span><span class="sxs-lookup"><span data-stu-id="c0967-110">Mixed Reality devices like HoloLens are designed for large undefined environments, with the device discovering and learning about its surroundings as the user walks around.</span></span> <span data-ttu-id="c0967-111">设备可适应不断提高用户会议室的知识，但会导致在应用程序生命周期内改变其关系的坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-111">The device adapts to continually improving knowledge about the user's rooms, but results in coordinate systems that change their relationship to one another over the apps lifetime.</span></span> <span data-ttu-id="c0967-112">Windows Mixed Reality 支持范围广泛的设备，这些设备包括通过世界附加的参考帧从固定的沉浸式耳机。</span><span class="sxs-lookup"><span data-stu-id="c0967-112">Windows Mixed Reality supports a wide spectrum of devices, ranging from seated immersive headsets through world-attached reference frames.</span></span>

>[!NOTE]
><span data-ttu-id="c0967-113">本文中的代码片段当前演示了如何 [使用 c +](creating-a-holographic-directx-project.md)+/cx 中的 c + +/cx 而不是 c + + 17 兼容 c + +/WinRT。</span><span class="sxs-lookup"><span data-stu-id="c0967-113">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="c0967-114">概念与 c + +/WinRT 项目等效，但你将需要转换代码。</span><span class="sxs-lookup"><span data-stu-id="c0967-114">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="spatial-coordinate-systems-in-windows"></a><span data-ttu-id="c0967-115">Windows 中的空间坐标系统</span><span class="sxs-lookup"><span data-stu-id="c0967-115">Spatial coordinate systems in Windows</span></span>

<span data-ttu-id="c0967-116">用于 Windows 中的实际坐标系统原因的核心类型是 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>。</span><span class="sxs-lookup"><span data-stu-id="c0967-116">The core type used to reason about real-world coordinate systems in Windows is the <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>.</span></span> <span data-ttu-id="c0967-117">此类型的实例表示任意坐标系统，该方法提供了一种方法，用于获取可用于在两个坐标系之间进行转换的方法，而不了解每个坐标系统的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0967-117">An instance of this type represents an arbitrary coordinate system, providing a method for getting transformation matrix data that you can use to transform between two coordinate systems without understanding the details of each.</span></span>

<span data-ttu-id="c0967-118">返回空间信息的方法将接受 SpatialCoordinateSystem 参数，以使你能够确定最适合要返回的坐标的坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-118">Methods that return spatial information will accept a SpatialCoordinateSystem parameter to let you decide the coordinate system in which it's most useful for those coordinates to be returned.</span></span> <span data-ttu-id="c0967-119">空间信息表示为用户的环境中的点、光或卷，这些坐标的单位将始终以米为单位。</span><span class="sxs-lookup"><span data-stu-id="c0967-119">Spatial information is represented as points, rays, or volumes in the user's surroundings, and the units for these coordinates will always be in meters.</span></span>

<span data-ttu-id="c0967-120">SpatialCoordinateSystem 与其他坐标系统（包括表示设备位置的系统）具有动态关系。</span><span class="sxs-lookup"><span data-stu-id="c0967-120">A SpatialCoordinateSystem has a dynamic relationship with other coordinate systems, including those that represent the device's position.</span></span> <span data-ttu-id="c0967-121">在任何时候，设备都可以定位某些坐标系统而不是其他坐标系。</span><span class="sxs-lookup"><span data-stu-id="c0967-121">At any point, the device can locate some coordinate systems and not others.</span></span> <span data-ttu-id="c0967-122">对于大多数坐标系统，您的应用程序必须准备好处理无法找到的时间段。</span><span class="sxs-lookup"><span data-stu-id="c0967-122">For most coordinate systems, your app must be ready to handle periods of time during which they cannot be located.</span></span>

<span data-ttu-id="c0967-123">您的应用程序不应直接创建 SpatialCoordinateSystems，而应通过感知 Api 来使用。</span><span class="sxs-lookup"><span data-stu-id="c0967-123">Your application shouldn't create SpatialCoordinateSystems directly - rather they should be consumed via the Perception APIs.</span></span> <span data-ttu-id="c0967-124">感知 Api 中有三个主要的坐标系统源，其中每个源都映射到 " [坐标系统](../../design/coordinate-systems.md) " 页上所述的概念：</span><span class="sxs-lookup"><span data-stu-id="c0967-124">There are three primary sources of coordinate systems in the Perception APIs, each of which map to a concept described on the [Coordinate systems](../../design/coordinate-systems.md) page:</span></span>
* <span data-ttu-id="c0967-125">若要获取固定的引用框架，请创建一个 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> 或从当前的 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>获取一个引用框架。</span><span class="sxs-lookup"><span data-stu-id="c0967-125">To get a stationary frame of reference, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> or obtain one from the current <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>.</span></span>
* <span data-ttu-id="c0967-126">若要获取空间定位点，请创建一个 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>。</span><span class="sxs-lookup"><span data-stu-id="c0967-126">To get a spatial anchor, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>.</span></span>
* <span data-ttu-id="c0967-127">若要获取附加的引用框架，请创建一个 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>。</span><span class="sxs-lookup"><span data-stu-id="c0967-127">To get an attached frame of reference, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>.</span></span>

<span data-ttu-id="c0967-128">这些对象返回的所有坐标系统都是右手的，其中 + y 向上，+ x 向右，+ z 向后。</span><span class="sxs-lookup"><span data-stu-id="c0967-128">All of the coordinate systems returned by these objects are right-handed, with +y up, +x to the right and +z backwards.</span></span> <span data-ttu-id="c0967-129">您可以通过在正 x 方向上向左或向右箭头，然后将它们运行为 y 方向，来记住哪个 z 轴的方向。</span><span class="sxs-lookup"><span data-stu-id="c0967-129">You can remember which direction the positive z-axis points by pointing the fingers of either your left or right hand in the positive x direction and curling them into the positive y direction.</span></span> <span data-ttu-id="c0967-130">你的拇指指向的方向（无论指向你还是相反方向）就是正 z 轴为坐标系统所指的方向。</span><span class="sxs-lookup"><span data-stu-id="c0967-130">The direction your thumb points, either toward or away from you, is the direction that the positive z-axis points for that coordinate system.</span></span> <span data-ttu-id="c0967-131">下面的图例显示了这两个坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-131">The following illustration shows these two coordinate systems.</span></span>

<span data-ttu-id="c0967-132">![左手和右手坐标系统](images/left-hand-right-hand.gif)</span><span class="sxs-lookup"><span data-stu-id="c0967-132">![Left-hand and right-hand coordinate systems](images/left-hand-right-hand.gif)</span></span><br>
<span data-ttu-id="c0967-133">*左手和右手坐标系统*</span><span class="sxs-lookup"><span data-stu-id="c0967-133">*Left-hand and right-hand coordinate systems*</span></span>

<span data-ttu-id="c0967-134">使用 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> 类创建一个附加或固定的引用框架，使其基于 HoloLens 位置在 SpatialCoordinateSystem 中启动。</span><span class="sxs-lookup"><span data-stu-id="c0967-134">Use the <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> class to create either an attached or stationary frame of reference to bootstrap into a SpatialCoordinateSystem based on the HoloLens position.</span></span> <span data-ttu-id="c0967-135">转到下一节，了解有关此过程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0967-135">Continue to the next section to learn more about this process.</span></span>

## <a name="place-holograms-in-the-world-using-a-spatial-stage"></a><span data-ttu-id="c0967-136">使用空间暂存在世界中放置全息影像</span><span class="sxs-lookup"><span data-stu-id="c0967-136">Place holograms in the world using a spatial stage</span></span>

<span data-ttu-id="c0967-137">不透明的 Windows Mixed Reality 沉浸式耳机的坐标系统使用静态 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference：： Current</a> 属性进行访问。</span><span class="sxs-lookup"><span data-stu-id="c0967-137">The coordinate system for opaque Windows Mixed Reality immersive headsets is accessed using the static <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference::Current</a> property.</span></span> <span data-ttu-id="c0967-138">此 API 提供：</span><span class="sxs-lookup"><span data-stu-id="c0967-138">This API provides:</span></span>

* <span data-ttu-id="c0967-139">坐标系统</span><span class="sxs-lookup"><span data-stu-id="c0967-139">A coordinate system</span></span>
* <span data-ttu-id="c0967-140">有关播放机是已安装还是移动设备的信息</span><span class="sxs-lookup"><span data-stu-id="c0967-140">Information about whether the player is seated or mobile</span></span>
* <span data-ttu-id="c0967-141">用于在播放机是移动设备时进行浏览的安全区域边界</span><span class="sxs-lookup"><span data-stu-id="c0967-141">The boundary of a safe area for walking around if the player is mobile</span></span>
* <span data-ttu-id="c0967-142">指示头戴式耳机是否定向。</span><span class="sxs-lookup"><span data-stu-id="c0967-142">An indication of whether the headset is directional.</span></span> 
* <span data-ttu-id="c0967-143">空间阶段更新的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="c0967-143">An event handler for updates to the spatial stage.</span></span>

<span data-ttu-id="c0967-144">首先，我们获取空间阶段并订阅其更新：</span><span class="sxs-lookup"><span data-stu-id="c0967-144">First, we get the spatial stage and subscribe for updates to it:</span></span> 

<span data-ttu-id="c0967-145">**空间阶段初始化** 代码</span><span class="sxs-lookup"><span data-stu-id="c0967-145">Code for **Spatial stage initialization**</span></span>

```
SpatialStageManager::SpatialStageManager(
    const std::shared_ptr<DX::DeviceResources>& deviceResources, 
    const std::shared_ptr<SceneController>& sceneController)
    : m_deviceResources(deviceResources), m_sceneController(sceneController)
{
    // Get notified when the stage is updated.
    m_spatialStageChangedEventToken = SpatialStageFrameOfReference::CurrentChanged +=
        ref new EventHandler<Object^>(std::bind(&SpatialStageManager::OnCurrentChanged, this, _1));

    // Make sure to get the current spatial stage.
    OnCurrentChanged(nullptr);
}
```

<span data-ttu-id="c0967-146">在 OnCurrentChanged 方法中，你的应用程序应检查空间阶段并更新播放机体验。</span><span class="sxs-lookup"><span data-stu-id="c0967-146">In the OnCurrentChanged method, your app should inspect the spatial stage and update the player experience.</span></span> <span data-ttu-id="c0967-147">在此示例中，我们提供了舞台边界的可视化效果，以及用户指定的起始位置和阶段的视图范围以及移动属性范围。</span><span class="sxs-lookup"><span data-stu-id="c0967-147">In this example, we provide a visualization of the stage boundary and the start position specified by the user and the stage's range of view and range of movement properties.</span></span> <span data-ttu-id="c0967-148">如果无法提供阶段，我们还会回退到我们自己的固定坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-148">We also fall back to our own stationary coordinate system, when a stage cannot be provided.</span></span>


<span data-ttu-id="c0967-149">**空间阶段更新** 代码</span><span class="sxs-lookup"><span data-stu-id="c0967-149">Code for **Spatial stage update**</span></span>

```
void SpatialStageManager::OnCurrentChanged(Object^ /*o*/)
{
    // The event notifies us that a new stage is available.
    // Get the current stage.
    m_currentStage = SpatialStageFrameOfReference::Current;

    // Clear previous content.
    m_sceneController->ClearSceneObjects();

    if (m_currentStage != nullptr)
    {
        // Obtain stage geometry.
        auto stageCoordinateSystem = m_currentStage->CoordinateSystem;
        auto boundsVertexArray = m_currentStage->TryGetMovementBounds(stageCoordinateSystem);

        // Visualize the area where the user can move around.
        std::vector<float3> boundsVertices;
        boundsVertices.resize(boundsVertexArray->Length);
        memcpy(boundsVertices.data(), boundsVertexArray->Data, boundsVertexArray->Length * sizeof(float3));
        std::vector<unsigned short> indices = TriangulatePoints(boundsVertices);
        m_stageBoundsShape =
            std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(boundsVertices),
                    indices,
                    XMFLOAT3(DirectX::Colors::SeaGreen),
                    stageCoordinateSystem);
        m_sceneController->AddSceneObject(m_stageBoundsShape);

        // In this sample, we draw a visual indicator for some spatial stage properties.
        // If the view is forward-only, the indicator is a half circle pointing forward - otherwise, it
        // is a full circle.
        // If the user can walk around, the indicator is blue. If the user is seated, it is red.

        // The indicator is rendered at the origin - which is where the user declared the center of the
        // stage to be during setup - above the plane of the stage bounds object.
        float3 visibleAreaCenter = float3(0.f, 0.001f, 0.f);

        // Its shape depends on the look direction range.
        std::vector<float3> visibleAreaIndicatorVertices;
        if (m_currentStage->LookDirectionRange == SpatialLookDirectionRange::ForwardOnly)
        {
            // Half circle for forward-only look direction range.
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.25f, 9, XM_PI);
        }
        else
        {
            // Full circle for omnidirectional look direction range.
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.25f, 16, XM_2PI);
        }

        // Its color depends on the movement range.
        XMFLOAT3 visibleAreaColor;
        if (m_currentStage->MovementRange == SpatialMovementRange::NoMovement)
        {
            visibleAreaColor = XMFLOAT3(DirectX::Colors::OrangeRed);
        }
        else
        {
            visibleAreaColor = XMFLOAT3(DirectX::Colors::Aqua);
        }

        std::vector<unsigned short> visibleAreaIndicatorIndices = TriangulatePoints(visibleAreaIndicatorVertices);

        // Visualize the look direction range.
        m_stageVisibleAreaIndicatorShape =
            std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(visibleAreaIndicatorVertices),
                    visibleAreaIndicatorIndices,
                    visibleAreaColor,
                    stageCoordinateSystem);
        m_sceneController->AddSceneObject(m_stageVisibleAreaIndicatorShape);
    }
    else
    {
        // No spatial stage was found.
        // Fall back to a stationary coordinate system.
        auto locator = SpatialLocator::GetDefault();
        if (locator)
        {
            m_stationaryFrameOfReference = locator->CreateStationaryFrameOfReferenceAtCurrentLocation();

            // Render an indicator, so that we know we fell back to a mode without a stage.
            std::vector<float3> visibleAreaIndicatorVertices;
            float3 visibleAreaCenter = float3(0.f, -2.0f, 0.f);
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.125f, 16, XM_2PI);
            std::vector<unsigned short> visibleAreaIndicatorIndices = TriangulatePoints(visibleAreaIndicatorVertices);
            m_stageVisibleAreaIndicatorShape =
                std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(visibleAreaIndicatorVertices),
                    visibleAreaIndicatorIndices,
                    XMFLOAT3(DirectX::Colors::LightSlateGray),
                    m_stationaryFrameOfReference->CoordinateSystem);
            m_sceneController->AddSceneObject(m_stageVisibleAreaIndicatorShape);
        }
    }
}
```

<span data-ttu-id="c0967-150">以顺时针顺序提供定义舞台边界的顶点集。</span><span class="sxs-lookup"><span data-stu-id="c0967-150">The set of vertices that define the stage boundary are provided in clockwise order.</span></span> <span data-ttu-id="c0967-151">当用户使用 Windows Mixed Reality shell 时，它们会在边界处绘制隔离区，但你可能需要为自己的目的 triangularize 不可区域。</span><span class="sxs-lookup"><span data-stu-id="c0967-151">The Windows Mixed Reality shell draws a fence at the boundary when the user approaches it, but you may want to triangularize the walkable area for your own purposes.</span></span> <span data-ttu-id="c0967-152">以下算法可用于 triangularize 阶段。</span><span class="sxs-lookup"><span data-stu-id="c0967-152">The following algorithm can be used to triangularize the stage.</span></span>


<span data-ttu-id="c0967-153">**空间阶段 triangularization** 的代码</span><span class="sxs-lookup"><span data-stu-id="c0967-153">Code for **Spatial stage triangularization**</span></span>

```
std::vector<unsigned short> SpatialStageManager::TriangulatePoints(std::vector<float3> const& vertices)
{
    size_t const& vertexCount = vertices.size();

    // Segments of the shape are removed as they are triangularized.
    std::vector<bool> vertexRemoved;
    vertexRemoved.resize(vertexCount, false);
    unsigned int vertexRemovedCount = 0;

    // Indices are used to define triangles.
    std::vector<unsigned short> indices;

    // Decompose into convex segments.
    unsigned short currentVertex = 0;
    while (vertexRemovedCount < (vertexCount - 2))
    {
        // Get next triangle:
        // Start with the current vertex.
        unsigned short index1 = currentVertex;

        // Get the next available vertex.
        unsigned short index2 = index1 + 1;

        // This cycles to the next available index.
        auto CycleIndex = [=](unsigned short indexToCycle, unsigned short stopIndex)
        {
            // Make sure the index does not exceed bounds.
            if (indexToCycle >= unsigned short(vertexCount))
            {
                indexToCycle -= unsigned short(vertexCount);
            }

            while (vertexRemoved[indexToCycle])
            {
                // If the vertex is removed, go to the next available one.
                ++indexToCycle;

                // Make sure the index does not exceed bounds.
                if (indexToCycle >= unsigned short(vertexCount))
                {
                    indexToCycle -= unsigned short(vertexCount);
                }

                // Prevent cycling all the way around.
                // Should not be needed, as we limit with the vertex count.
                if (indexToCycle == stopIndex)
                {
                    break;
                }
            }

            return indexToCycle;
        };
        index2 = CycleIndex(index2, index1);

        // Get the next available vertex after that.
        unsigned short index3 = index2 + 1;
        index3 = CycleIndex(index3, index1);

        // Vertices that may define a triangle inside the 2D shape.
        auto& v1 = vertices[index1];
        auto& v2 = vertices[index2];
        auto& v3 = vertices[index3];

        // If the projection of the first segment (in clockwise order) onto the second segment is 
        // positive, we know that the clockwise angle is less than 180 degrees, which tells us 
        // that the triangle formed by the two segments is contained within the bounding shape.
        auto v2ToV1 = v1 - v2;
        auto v2ToV3 = v3 - v2;
        float3 normalToV2ToV3 = { -v2ToV3.z, 0.f, v2ToV3.x };
        float projectionOntoNormal = dot(v2ToV1, normalToV2ToV3);
        if (projectionOntoNormal >= 0)
        {
            // Triangle is contained within the 2D shape.

            // Remove peak vertex from the list.
            vertexRemoved[index2] = true;
            ++vertexRemovedCount;

            // Create the triangle.
            indices.push_back(index1);
            indices.push_back(index2);
            indices.push_back(index3);

            // Continue on to the next outer triangle.
            currentVertex = index3;
        }
        else
        {
            // Triangle is a cavity in the 2D shape.
            // The next triangle starts at the inside corner.
            currentVertex = index2;
        }
    }

    indices.shrink_to_fit();
    return indices;
}
```

## <a name="place-holograms-in-the-world-using-a-stationary-frame-of-reference"></a><span data-ttu-id="c0967-154">使用固定的参考框架在世界中放置全息影像</span><span class="sxs-lookup"><span data-stu-id="c0967-154">Place holograms in the world using a stationary frame of reference</span></span>

<span data-ttu-id="c0967-155">[SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx)类表示一个引用框架，该框架在用户四处移动时相对于用户的环境[保持静止](../../design/coordinate-systems.md#stationary-frame-of-reference)。</span><span class="sxs-lookup"><span data-stu-id="c0967-155">The [SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx) class represents a frame of reference that [remains stationary](../../design/coordinate-systems.md#stationary-frame-of-reference) relative to the user's surroundings as the user moves around.</span></span> <span data-ttu-id="c0967-156">这一帧参考用于使坐标在设备附近保持稳定。</span><span class="sxs-lookup"><span data-stu-id="c0967-156">This frame of reference prioritizes keeping coordinates stable near the device.</span></span> <span data-ttu-id="c0967-157">SpatialStationaryFrameOfReference 的一项关键用途是在渲染全息影像时充当渲染引擎内的基础世界坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-157">One key use of a SpatialStationaryFrameOfReference is to act as the underlying world coordinate system within a rendering engine when rendering holograms.</span></span>

<span data-ttu-id="c0967-158">若要获取 SpatialStationaryFrameOfReference，请使用 [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) 类并调用 [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0967-158">To get a SpatialStationaryFrameOfReference, use the [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) class and call [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx).</span></span>

<span data-ttu-id="c0967-159">从 Windows 全息应用模板代码：</span><span class="sxs-lookup"><span data-stu-id="c0967-159">From the Windows Holographic app template code:</span></span>

```
           // The simplest way to render world-locked holograms is to create a stationary reference frame
           // when the app is launched. This is roughly analogous to creating a "world" coordinate system
           // with the origin placed at the device's position as the app is launched.
           referenceFrame = locator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```
* <span data-ttu-id="c0967-160">固定参考帧旨在提供相对于总体空间的最佳位置。</span><span class="sxs-lookup"><span data-stu-id="c0967-160">Stationary reference frames are designed to provide a best-fit position relative to the overall space.</span></span> <span data-ttu-id="c0967-161">该引用帧中的各个位置都允许略微偏移。</span><span class="sxs-lookup"><span data-stu-id="c0967-161">Individual positions within that reference frame are allowed to drift slightly.</span></span> <span data-ttu-id="c0967-162">这是正常现象，因为设备会了解有关环境的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0967-162">This is normal as the device learns more about the environment.</span></span>
* <span data-ttu-id="c0967-163">需要精确放置单独的全息影像时，应使用 SpatialAnchor 将各个全息图锚定到现实世界中的某个位置-例如，用户指示特别感兴趣的点。</span><span class="sxs-lookup"><span data-stu-id="c0967-163">When precise placement of individual holograms is required, a SpatialAnchor should be used to anchor the individual hologram to a position in the real world - for example, a point the user indicates to be of special interest.</span></span> <span data-ttu-id="c0967-164">定位点位置不会偏移，但可以更正。定位点将使用更正后在下一帧中开始的更正位置。</span><span class="sxs-lookup"><span data-stu-id="c0967-164">Anchor positions don't drift, but can be corrected; the anchor will use the corrected position starting in the next frame after the correction has occurred.</span></span>

## <a name="place-holograms-in-the-world-using-spatial-anchors"></a><span data-ttu-id="c0967-165">使用空间锚点将全息影像置于世界中</span><span class="sxs-lookup"><span data-stu-id="c0967-165">Place holograms in the world using spatial anchors</span></span>

<span data-ttu-id="c0967-166">[空间锚点](../../design/coordinate-systems.md#spatial-anchors) 是在真实世界的特定位置放置全息影像的绝佳方式，系统可确保锚点在一段时间内保持不变。</span><span class="sxs-lookup"><span data-stu-id="c0967-166">[Spatial anchors](../../design/coordinate-systems.md#spatial-anchors) are a great way to place holograms at a specific place in the real world, with the system ensuring the anchor stays in place over time.</span></span> <span data-ttu-id="c0967-167">本主题说明如何创建和使用定位点，以及如何使用定位点数据。</span><span class="sxs-lookup"><span data-stu-id="c0967-167">This topic explains how to create and use an anchor, and how to work with anchor data.</span></span>

<span data-ttu-id="c0967-168">你可以在所选的 SpatialCoordinateSystem 内的任何位置和方向上创建 SpatialAnchor。</span><span class="sxs-lookup"><span data-stu-id="c0967-168">You can create a SpatialAnchor at any position and orientation within the SpatialCoordinateSystem of your choosing.</span></span> <span data-ttu-id="c0967-169">设备现在必须能够找到该坐标系，而且系统不得达到其空间锚定的限制。</span><span class="sxs-lookup"><span data-stu-id="c0967-169">The device must be able to locate that coordinate system at the moment, and the system must not have reached its limit of spatial anchors.</span></span>

<span data-ttu-id="c0967-170">定义后，SpatialAnchor 的坐标系统将不断调整，以保持其初始位置的精确位置和方向。</span><span class="sxs-lookup"><span data-stu-id="c0967-170">Once defined, the coordinate system of a SpatialAnchor adjusts continually to keep the precise position and orientation of its initial location.</span></span> <span data-ttu-id="c0967-171">然后，你可以使用此 SpatialAnchor 来呈现在该确切位置的用户环境中显示为固定的全息影像。</span><span class="sxs-lookup"><span data-stu-id="c0967-171">You can then use this SpatialAnchor to render holograms that will appear fixed in the user's surroundings at that exact location.</span></span>

<span data-ttu-id="c0967-172">调整锚点的调整效果将随着锚点增加的距离而放大。</span><span class="sxs-lookup"><span data-stu-id="c0967-172">The effects of the adjustments that keep the anchor in place are magnified as distance from the anchor increases.</span></span> <span data-ttu-id="c0967-173">应避免相对于该定位点的源中超过3米的定位点呈现内容。</span><span class="sxs-lookup"><span data-stu-id="c0967-173">You should avoid rendering content relative to an anchor that is more than about 3 meters from that anchor's origin.</span></span>

<span data-ttu-id="c0967-174">[坐标系](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx)属性获取一个坐标系统，该系统允许你相对于定位点放置内容，并在设备调整定位点的确切位置时应用缓动。</span><span class="sxs-lookup"><span data-stu-id="c0967-174">The [CoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx) property gets a coordinate system that lets you place content relative to the anchor, with easing applied when the device adjusts the anchor's precise location.</span></span>

<span data-ttu-id="c0967-175">使用 [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) 属性和相应的 [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) 事件自行管理这些调整。</span><span class="sxs-lookup"><span data-stu-id="c0967-175">Use the [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) property and the corresponding [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) event to manage these adjustments yourself.</span></span>

### <a name="persist-and-share-spatial-anchors"></a><span data-ttu-id="c0967-176">保留并共享空间锚</span><span class="sxs-lookup"><span data-stu-id="c0967-176">Persist and share spatial anchors</span></span>

<span data-ttu-id="c0967-177">你可以使用 [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) 类在本地保留 SpatialAnchor，然后在同一 HoloLens 设备上的未来应用会话中恢复它。</span><span class="sxs-lookup"><span data-stu-id="c0967-177">You can persist a SpatialAnchor locally using the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) class and then get it back in a future app session on the same HoloLens device.</span></span>

<span data-ttu-id="c0967-178">通过使用 <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空间锚点</a>，你可以从本地 SpatialAnchor 创建持久的云锚点，你的应用可以在多个 HoloLens、IOS 和 Android 设备上找到它。</span><span class="sxs-lookup"><span data-stu-id="c0967-178">By using <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a>, you can create a durable cloud anchor from a local SpatialAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="c0967-179">通过在多个设备之间共享公用空间定位点，每个用户都可以在同一物理位置实时查看相对于该锚点呈现的内容。</span><span class="sxs-lookup"><span data-stu-id="c0967-179">By sharing a common spatial anchor across multiple devices, each user can see content rendered relative to that anchor in the same physical location in real time.</span></span> 

<span data-ttu-id="c0967-180">你还可以将 <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空间锚点</a> 用于每个 HoloLens、IOS 和 Android 设备上的异步全息影像。</span><span class="sxs-lookup"><span data-stu-id="c0967-180">You can also use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> for asynchronous hologram persistence across HoloLens, iOS, and Android devices.</span></span>  <span data-ttu-id="c0967-181">通过共享持久云空间锚点，多个设备可以在一段时间内观察到相同的持久全息图，即使这些设备同时不存在。</span><span class="sxs-lookup"><span data-stu-id="c0967-181">By sharing a durable cloud spatial anchor, multiple devices can observe the same persisted hologram over time, even if those devices aren't present together at the same time.</span></span>

<span data-ttu-id="c0967-182">若要开始在 HoloLens 应用中构建共享体验，请尝试5分钟的 <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">Azure 空间锚快速入门</a>。</span><span class="sxs-lookup"><span data-stu-id="c0967-182">To get started building shared experiences in your HoloLens app, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">Azure Spatial Anchors HoloLens quickstart</a>.</span></span>

<span data-ttu-id="c0967-183">启动并运行 Azure 空间锚点后，可以 <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">在 HoloLens 上创建和查找锚</a>。</span><span class="sxs-lookup"><span data-stu-id="c0967-183">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">create and locate anchors on HoloLens</a>.</span></span>  <span data-ttu-id="c0967-184">演练也适用于 <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android 和 iOS</a> ，使你能够在所有设备上共享相同的定位标记。</span><span class="sxs-lookup"><span data-stu-id="c0967-184">Walkthroughs are available for <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android and iOS</a> as well, enabling you to share the same anchors on all devices.</span></span>

### <a name="create-spatialanchors-for-holographic-content"></a><span data-ttu-id="c0967-185">为全息内容创建 SpatialAnchors</span><span class="sxs-lookup"><span data-stu-id="c0967-185">Create SpatialAnchors for holographic content</span></span>

<span data-ttu-id="c0967-186">对于此代码示例，我们修改了 Windows 全息应用程序模板，在检测到 **按下** 的手势时创建定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-186">For this code sample, we modified the Windows Holographic app template to create anchors when the **Pressed** gesture is detected.</span></span> <span data-ttu-id="c0967-187">然后，在呈现过程中将多维数据集放在定位点上。</span><span class="sxs-lookup"><span data-stu-id="c0967-187">The cube is then placed at the anchor during the render pass.</span></span>

<span data-ttu-id="c0967-188">由于 helper 类支持多个定位点，因此，我们可以将所需数量的多维数据集置于此代码示例中！</span><span class="sxs-lookup"><span data-stu-id="c0967-188">Since multiple anchors are supported by the helper class, we can place as many cubes as we want to use this code sample!</span></span>

> [!NOTE]
> <span data-ttu-id="c0967-189">定位点的 Id 是你在应用中控制的内容。</span><span class="sxs-lookup"><span data-stu-id="c0967-189">The IDs for anchors are something you control in your app.</span></span> <span data-ttu-id="c0967-190">在此示例中，我们创建了一个命名方案，该方案基于当前存储在应用程序的定位点集合中的定位点数。</span><span class="sxs-lookup"><span data-stu-id="c0967-190">In this example, we have created a naming scheme that is sequential based on the number of anchors currently stored in the app's collection of anchors.</span></span>

```
   // Check for new input state since the last frame.
   SpatialInteractionSourceState^ pointerState = m_spatialInputHandler->CheckForInput();
   if (pointerState != nullptr)
   {
       // Try to get the pointer pose relative to the SpatialStationaryReferenceFrame.
       SpatialPointerPose^ pointerPose = pointerState->TryGetPointerPose(currentCoordinateSystem);
       if (pointerPose != nullptr)
       {
           // When a Pressed gesture is detected, the anchor will be created two meters in front of the user.

           // Get the gaze direction relative to the given coordinate system.
           const float3 headPosition = pointerPose->Head->Position;
           const float3 headDirection = pointerPose->Head->ForwardDirection;

           // The anchor position in the StationaryReferenceFrame.
           static const float distanceFromUser = 2.0f; // meters
           const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * headDirection);

           // Create the anchor at position.
           SpatialAnchor^ anchor = SpatialAnchor::TryCreateRelativeTo(currentCoordinateSystem, gazeAtTwoMeters);

           if ((anchor != nullptr) && (m_spatialAnchorHelper != nullptr))
           {
               // In this example, we store the anchor in an IMap.
               auto anchorMap = m_spatialAnchorHelper->GetAnchorMap();

               // Create an identifier for the anchor.
               String^ id = ref new String(L"HolographicSpatialAnchorStoreSample_Anchor") + anchorMap->Size;

               anchorMap->Insert(id->ToString(), anchor);
           }
       }
   }
```

### <a name="asynchronously-load-and-cache-the-spatialanchorstore"></a><span data-ttu-id="c0967-191">异步加载和缓存，SpatialAnchorStore</span><span class="sxs-lookup"><span data-stu-id="c0967-191">Asynchronously load, and cache, the SpatialAnchorStore</span></span>

<span data-ttu-id="c0967-192">我们来看一下如何编写有助于处理此持久性的 SampleSpatialAnchorHelper 类，其中包括：</span><span class="sxs-lookup"><span data-stu-id="c0967-192">Let's see how to write a SampleSpatialAnchorHelper class that helps handle this persistence, including:</span></span>
* <span data-ttu-id="c0967-193">存储内存中定位点的集合，由 Platform：： String 键进行索引。</span><span class="sxs-lookup"><span data-stu-id="c0967-193">Storing a collection of in-memory anchors, indexed by a Platform::String key.</span></span>
* <span data-ttu-id="c0967-194">从系统的 SpatialAnchorStore 加载定位点，这与本地内存中集合保持分离。</span><span class="sxs-lookup"><span data-stu-id="c0967-194">Loading anchors from the system's SpatialAnchorStore, which is kept separate from the local in-memory collection.</span></span>
* <span data-ttu-id="c0967-195">当应用选择执行此操作时，将本地内存中集合的定位点保存到 SpatialAnchorStore。</span><span class="sxs-lookup"><span data-stu-id="c0967-195">Saving the local in-memory collection of anchors to the SpatialAnchorStore when the app chooses to do so.</span></span>

<span data-ttu-id="c0967-196">下面介绍了如何将 [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) 对象保存在 [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx)中。</span><span class="sxs-lookup"><span data-stu-id="c0967-196">Here's how to save [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) objects in the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span></span>

<span data-ttu-id="c0967-197">类启动时，会异步请求 SpatialAnchorStore。</span><span class="sxs-lookup"><span data-stu-id="c0967-197">When the class starts up, we request the SpatialAnchorStore asynchronously.</span></span> <span data-ttu-id="c0967-198">这涉及到 API 加载锚定存储时的系统 i/o，此 API 是异步的，因此 i/o 是非阻塞的。</span><span class="sxs-lookup"><span data-stu-id="c0967-198">This involves system I/O as the API loads the anchor store, and this API is made asynchronous so that the I/O is non-blocking.</span></span>

```
   // Request the spatial anchor store, which is the WinRT object that will accept the imported anchor data.
   return create_task(SpatialAnchorManager::RequestStoreAsync())
       .then([](task<SpatialAnchorStore^> previousTask)
   {
       std::shared_ptr<SampleSpatialAnchorHelper> newHelper = nullptr;

       try
       {
           SpatialAnchorStore^ anchorStore = previousTask.get();

           // Once the SpatialAnchorStore has been loaded by the system, we can create our helper class.

           // Using "new" to access private constructor
           newHelper = std::shared_ptr<SampleSpatialAnchorHelper>(new SampleSpatialAnchorHelper(anchorStore));

           // Now we can load anchors from the store.
           newHelper->LoadFromAnchorStore();
       }
       catch (Exception^ exception)
       {
           PrintWstringToDebugConsole(
               std::wstring(L"Exception while loading the anchor store: ") +
               exception->Message->Data() +
               L"\n"
               );
       }

       // Return the initialized class instance.
       return newHelper;
   });
```

<span data-ttu-id="c0967-199">系统会提供一个 SpatialAnchorStore，可用于保存锚。</span><span class="sxs-lookup"><span data-stu-id="c0967-199">You'll be given a SpatialAnchorStore that you can use to save the anchors.</span></span> <span data-ttu-id="c0967-200">这是将字符串键值与 SpatialAnchors 的数据值相关联的 IMapView。</span><span class="sxs-lookup"><span data-stu-id="c0967-200">This is an IMapView that associates key values that are Strings, with data values that are SpatialAnchors.</span></span> <span data-ttu-id="c0967-201">在我们的示例代码中，我们将其存储在私有类成员变量中，该变量可通过我们的帮助程序类的公共函数访问。</span><span class="sxs-lookup"><span data-stu-id="c0967-201">In our sample code, we store this in a private class member variable that is accessible through a public function of our helper class.</span></span>

```
   SampleSpatialAnchorHelper::SampleSpatialAnchorHelper(SpatialAnchorStore^ anchorStore)
   {
       m_anchorStore = anchorStore;
       m_anchorMap = ref new Platform::Collections::Map<String^, SpatialAnchor^>();
   }
```

>[!NOTE]
><span data-ttu-id="c0967-202">别忘了挂钩暂停/恢复事件，保存并加载定位点存储。</span><span class="sxs-lookup"><span data-stu-id="c0967-202">Don't forget to hook up the suspend/resume events to save and load the anchor store.</span></span>

```
   void HolographicSpatialAnchorStoreSampleMain::SaveAppState()
   {
       // For example, store information in the SpatialAnchorStore.
       if (m_spatialAnchorHelper != nullptr)
       {
           m_spatialAnchorHelper->TrySaveToAnchorStore();
       }
   }
```

```
   void HolographicSpatialAnchorStoreSampleMain::LoadAppState()
   {
       // For example, load information from the SpatialAnchorStore.
       LoadAnchorStore();
   }
```

### <a name="save-content-to-the-anchor-store"></a><span data-ttu-id="c0967-203">将内容保存到定位点存储</span><span class="sxs-lookup"><span data-stu-id="c0967-203">Save content to the anchor store</span></span>

<span data-ttu-id="c0967-204">当系统挂起应用时，需要将空间锚点保存到锚存储。</span><span class="sxs-lookup"><span data-stu-id="c0967-204">When the system suspends your app, you need to save your spatial anchors to the anchor store.</span></span> <span data-ttu-id="c0967-205">你还可以选择在其他时间将定位点保存到定位点存储区，就像你在应用的实现时所需要的那样。</span><span class="sxs-lookup"><span data-stu-id="c0967-205">You may also choose to save anchors to the anchor store at other times, as you find to be necessary for your app's implementation.</span></span>

<span data-ttu-id="c0967-206">准备尝试将内存中的定位标记保存到 SpatialAnchorStore 时，可以循环遍历集合并尝试保存每个定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-206">When you're ready to try saving the in-memory anchors to the SpatialAnchorStore, you can loop through your collection and try to save each one.</span></span>

```
   // TrySaveToAnchorStore: Stores all anchors from memory into the app's anchor store.
   //
   // For each anchor in memory, this function tries to store it in the app's AnchorStore. The operation will fail if
   // the anchor store already has an anchor by that name.
   //
   bool SampleSpatialAnchorHelper::TrySaveToAnchorStore()
   {
       // This function returns true if all the anchors in the in-memory collection are saved to the anchor
       // store. If zero anchors are in the in-memory collection, we will still return true because the
       // condition has been met.
       bool success = true;

       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           for each (auto& pair in m_anchorMap)
           {
               auto const& id = pair->Key;
               auto const& anchor = pair->Value;

               // Try to save the anchors.
               if (!m_anchorStore->TrySave(id, anchor))
               {
                   // This may indicate the anchor ID is taken, or the anchor limit is reached for the app.
                   success=false;
               }
           }
       }

       return success;
   }
```

### <a name="load-content-from-the-anchor-store-when-the-app-resumes"></a><span data-ttu-id="c0967-207">在应用恢复时从定位点存储加载内容</span><span class="sxs-lookup"><span data-stu-id="c0967-207">Load content from the anchor store when the app resumes</span></span>

<span data-ttu-id="c0967-208">你可以还原 AnchorStore 中保存的定位点，方法是在你的应用程序恢复或随时恢复时将其从定位点存储区的 IMapView 传输到你自己的内存中数据库。</span><span class="sxs-lookup"><span data-stu-id="c0967-208">You can restore saved anchors in the AnchorStore by transferring them from the anchor store's IMapView to your own in-memory database of SpatialAnchors when your app resumes or at any time.</span></span>

<span data-ttu-id="c0967-209">若要从 SpatialAnchorStore 还原定位点，请将你感兴趣的每个定位点还原到自己的内存中集合。</span><span class="sxs-lookup"><span data-stu-id="c0967-209">To restore anchors from the SpatialAnchorStore, restore each one that you're interested in to your own in-memory collection.</span></span>

<span data-ttu-id="c0967-210">需要 SpatialAnchors 的内存中数据库，才能将字符串与所创建的 SpatialAnchors 相关联。</span><span class="sxs-lookup"><span data-stu-id="c0967-210">You need your own in-memory database of SpatialAnchors to associate Strings with the SpatialAnchors that you create.</span></span> <span data-ttu-id="c0967-211">在我们的示例代码中，我们选择使用 Windows：： Foundation：：集合：： IMap 来存储定位点，这使得为 SpatialAnchorStore 使用相同的密钥和数据值变得简单。</span><span class="sxs-lookup"><span data-stu-id="c0967-211">In our sample code, we choose to use a Windows::Foundation::Collections::IMap to store the anchors, which makes it easy to use the same key and data value for the SpatialAnchorStore.</span></span>

```
   // This is an in-memory anchor list that is separate from the anchor store.
   // These anchors may be used, reasoned about, and so on before committing the collection to the store.
   Windows::Foundation::Collections::IMap<Platform::String^, Windows::Perception::Spatial::SpatialAnchor^>^ m_anchorMap;
```

>[!NOTE]
><span data-ttu-id="c0967-212">可能无法立即定位还原的定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-212">An anchor that is restored might not be locatable right away.</span></span> <span data-ttu-id="c0967-213">例如，它可能是位于单独房间或不同建筑物中的定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-213">For example, it might be an anchor in a separate room or in a different building altogether.</span></span> <span data-ttu-id="c0967-214">在使用从 AnchorStore 检索到的定位点之前应对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="c0967-214">Anchors retrieved from the AnchorStore should be tested for locatability before using them.</span></span>

<br>

>[!NOTE]
><span data-ttu-id="c0967-215">在此示例代码中，我们将从 AnchorStore 检索所有定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-215">In this example code, we retrieve all anchors from the AnchorStore.</span></span> <span data-ttu-id="c0967-216">这不是必需的;您的应用程序也可以选择使用对您的实现有意义的字符串键值，并选择某个定位点。</span><span class="sxs-lookup"><span data-stu-id="c0967-216">This is not a requirement; your app could just as well pick and choose a certain subset of anchors by using String key values that are meaningful to your implementation.</span></span>

```
   // LoadFromAnchorStore: Loads all anchors from the app's anchor store into memory.
   //
   // The anchors are stored in memory using an IMap, which stores anchors using a string identifier. Any string can be used as
   // the identifier; it can have meaning to the app, such as "Game_Leve1_CouchAnchor," or it can be a GUID that is generated
   // by the app.
   //
   void SampleSpatialAnchorHelper::LoadFromAnchorStore()
   {
       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           // Get all saved anchors.
           auto anchorMapView = m_anchorStore->GetAllSavedAnchors();
           for each (auto const& pair in anchorMapView)
           {
               auto const& id = pair->Key;
               auto const& anchor = pair->Value;
               m_anchorMap->Insert(id, anchor);
           }
       }
   }
```

### <a name="clear-the-anchor-store-when-needed"></a><span data-ttu-id="c0967-217">如果需要，请清除锚定存储</span><span class="sxs-lookup"><span data-stu-id="c0967-217">Clear the anchor store, when needed</span></span>

<span data-ttu-id="c0967-218">有时，您需要清除应用状态并写入新数据。</span><span class="sxs-lookup"><span data-stu-id="c0967-218">Sometimes, you need to clear app state and write new data.</span></span> <span data-ttu-id="c0967-219">下面是如何通过 [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx)执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="c0967-219">Here's how you do that with the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span></span>

<span data-ttu-id="c0967-220">使用我们的帮助器类，几乎不需要包装 Clear 函数。</span><span class="sxs-lookup"><span data-stu-id="c0967-220">Using our helper class, it's almost unnecessary to wrap the Clear function.</span></span> <span data-ttu-id="c0967-221">我们选择在示例实现中执行此操作，因为我们的帮助器类被赋予了拥有 SpatialAnchorStore 实例的责任。</span><span class="sxs-lookup"><span data-stu-id="c0967-221">We choose to do so in our sample implementation, because our helper class is given the responsibility of owning the SpatialAnchorStore instance.</span></span>

```
   // ClearAnchorStore: Clears the AnchorStore for the app.
   //
   // This function clears the AnchorStore. It has no effect on the anchors stored in memory.
   //
   void SampleSpatialAnchorHelper::ClearAnchorStore()
   {
       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           // Clear all anchors from the store.
           m_anchorStore->Clear();
       }
   }
```

### <a name="example-relating-anchor-coordinate-systems-to-stationary-reference-frame-coordinate-systems"></a><span data-ttu-id="c0967-222">示例：将定位坐标系与固定引用帧坐标系统相关联</span><span class="sxs-lookup"><span data-stu-id="c0967-222">Example: Relating anchor coordinate systems to stationary reference frame coordinate systems</span></span>

<span data-ttu-id="c0967-223">假设你有一个定位点，并且想要将定位点坐标系统中的某些内容关联到其他内容所使用的 SpatialStationaryReferenceFrame。</span><span class="sxs-lookup"><span data-stu-id="c0967-223">Let's say you have an anchor, and you want to relate something in your anchor's coordinate system to the SpatialStationaryReferenceFrame you’re already using for your other content.</span></span> <span data-ttu-id="c0967-224">您可以使用 [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) 从定位点的坐标系统获取转换为固定参考帧的转换：</span><span class="sxs-lookup"><span data-stu-id="c0967-224">You can use [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) to get a transform from the anchor’s coordinate system to that of the stationary reference frame:</span></span>

```
   // In this code snippet, someAnchor is a SpatialAnchor^ that has been initialized and is valid in the current environment.
   float4x4 anchorSpaceToCurrentCoordinateSystem;
   SpatialCoordinateSystem^ anchorSpace = someAnchor->CoordinateSystem;
   const auto tryTransform = anchorSpace->TryGetTransformTo(currentCoordinateSystem);
   if (tryTransform != nullptr)
   {
       anchorSpaceToCurrentCoordinateSystem = tryTransform->Value;
   }
```

<span data-ttu-id="c0967-225">此过程可通过两种方式来实现：</span><span class="sxs-lookup"><span data-stu-id="c0967-225">This process is useful to you in two ways:</span></span>
1. <span data-ttu-id="c0967-226">它告诉你是否可以彼此理解两个引用框架，以及</span><span class="sxs-lookup"><span data-stu-id="c0967-226">It tells you if the two reference frames can be understood relative to one another, and;</span></span>
2. <span data-ttu-id="c0967-227">如果是这样，它将提供一个转换，以便直接从一个坐标系转换到另一个坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-227">If so, it provides you a transform to go directly from one coordinate system to the other.</span></span>

<span data-ttu-id="c0967-228">使用此信息，您可以了解两个引用帧之间对象之间的空间关系。</span><span class="sxs-lookup"><span data-stu-id="c0967-228">With this information, you have an understanding of the spatial relation between objects between the two reference frames.</span></span>

<span data-ttu-id="c0967-229">对于呈现，通常可以根据对象的原始参考框架或锚点对它们进行分组，从而获得更好的结果。</span><span class="sxs-lookup"><span data-stu-id="c0967-229">For rendering, you can often obtain better results by grouping objects according to their original reference frame or anchor.</span></span> <span data-ttu-id="c0967-230">为每个组执行单独的绘图处理。</span><span class="sxs-lookup"><span data-stu-id="c0967-230">Perform a separate drawing pass for each group.</span></span> <span data-ttu-id="c0967-231">对于具有最初使用同一坐标系统创建的模型转换的对象，视图矩阵更准确。</span><span class="sxs-lookup"><span data-stu-id="c0967-231">The view matrices are more accurate for objects with model transforms that are created initially using the same coordinate system.</span></span>

## <a name="create-holograms-using-a-device-attached-frame-of-reference"></a><span data-ttu-id="c0967-232">使用设备附加的参考框架创建全息影像</span><span class="sxs-lookup"><span data-stu-id="c0967-232">Create holograms using a device-attached frame of reference</span></span>

<span data-ttu-id="c0967-233">有时，你想要呈现已 [附加](../../design/coordinate-systems.md#attached-frame-of-reference) 到设备位置的全息影像，例如，当设备只能确定其方向而不能确定其在空间中的位置时，包含调试信息或信息性消息的面板。</span><span class="sxs-lookup"><span data-stu-id="c0967-233">There are times when you want to render a hologram that [remains attached](../../design/coordinate-systems.md#attached-frame-of-reference) to the device's location, for example a panel with debugging information or an informational message when the device is only able to determine its orientation and not its position in space.</span></span> <span data-ttu-id="c0967-234">为此，我们使用附加的参考框架。</span><span class="sxs-lookup"><span data-stu-id="c0967-234">To accomplish this, we use an attached frame of reference.</span></span>

<span data-ttu-id="c0967-235">SpatialLocatorAttachedFrameOfReference 类定义了相对于设备而不是实际的坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-235">The SpatialLocatorAttachedFrameOfReference class defines coordinate systems, which are relative to the device rather than to the real-world.</span></span> <span data-ttu-id="c0967-236">此框架的固定标题相对于用户在创建引用框架时面向的方向的用户环境。</span><span class="sxs-lookup"><span data-stu-id="c0967-236">This frame has a fixed heading relative to the user's surroundings that points in the direction the user was facing when the reference frame was created.</span></span> <span data-ttu-id="c0967-237">接下来，这一帧参考中的所有方向都是相对于该固定标题的，即使用户要旋转设备也是如此。</span><span class="sxs-lookup"><span data-stu-id="c0967-237">From then on, all orientations in this frame of reference are relative to that fixed heading, even as the user rotates the device.</span></span>

<span data-ttu-id="c0967-238">对于 HoloLens，此帧坐标系统的原点位于用户头部的旋转中心，因此其位置不受 head 旋转的影响。</span><span class="sxs-lookup"><span data-stu-id="c0967-238">For HoloLens, the origin of this frame's coordinate system is located at the center of rotation of the user's head, so that its position is not affected by head rotation.</span></span> <span data-ttu-id="c0967-239">您的应用程序可以指定与此点相对的偏移量，以将全息影像置于用户的前端。</span><span class="sxs-lookup"><span data-stu-id="c0967-239">Your app can specify an offset relative to this point to position holograms in front of the user.</span></span>

<span data-ttu-id="c0967-240">若要获取 SpatialLocatorAttachedFrameOfReference，请使用 SpatialLocator 类并调用 CreateAttachedFrameOfReferenceAtCurrentHeading。</span><span class="sxs-lookup"><span data-stu-id="c0967-240">To get a SpatialLocatorAttachedFrameOfReference, use the SpatialLocator class and call CreateAttachedFrameOfReferenceAtCurrentHeading.</span></span>

<span data-ttu-id="c0967-241">这适用于整个范围的 Windows Mixed Reality 设备。</span><span class="sxs-lookup"><span data-stu-id="c0967-241">This applies to the entire range of Windows Mixed Reality devices.</span></span>

### <a name="use-a-reference-frame-attached-to-the-device"></a><span data-ttu-id="c0967-242">使用附加到设备的引用框架</span><span class="sxs-lookup"><span data-stu-id="c0967-242">Use a reference frame attached to the device</span></span>

<span data-ttu-id="c0967-243">这些部分讨论了在 Windows 全息应用程序模板中所做的更改，以使用此 API 启用设备附加的引用框架。</span><span class="sxs-lookup"><span data-stu-id="c0967-243">These sections talk about what we changed in the Windows Holographic app template to enable a device-attached frame of reference using this API.</span></span> <span data-ttu-id="c0967-244">此 "附加" 的全息图将与固定或定位全息影像一起工作，并且在设备暂时无法找到其在世界各地的位置时也可能会用到它。</span><span class="sxs-lookup"><span data-stu-id="c0967-244">This "attached" hologram will work alongside stationary or anchored holograms, and may also be used when the device is temporarily unable to find its position in the world.</span></span>

<span data-ttu-id="c0967-245">首先，我们将模板更改为存储 SpatialLocatorAttachedFrameOfReference 而不是 SpatialStationaryFrameOfReference：</span><span class="sxs-lookup"><span data-stu-id="c0967-245">First, we changed the template to store a SpatialLocatorAttachedFrameOfReference instead of a SpatialStationaryFrameOfReference:</span></span>

<span data-ttu-id="c0967-246">从 **HolographicTagAlongSampleMain**：</span><span class="sxs-lookup"><span data-stu-id="c0967-246">From **HolographicTagAlongSampleMain.h**:</span></span>

```
   // A reference frame attached to the holographic camera.
   Windows::Perception::Spatial::SpatialLocatorAttachedFrameOfReference^   m_referenceFrame;
```

<span data-ttu-id="c0967-247">从 **HolographicTagAlongSampleMain**：</span><span class="sxs-lookup"><span data-stu-id="c0967-247">From **HolographicTagAlongSampleMain.cpp**:</span></span>

```
   // In this example, we create a reference frame attached to the device.
   m_referenceFrame = m_locator->CreateAttachedFrameOfReferenceAtCurrentHeading();
```

<span data-ttu-id="c0967-248">在更新过程中，我们会在从帧预测获得的时间戳处获取坐标系统。</span><span class="sxs-lookup"><span data-stu-id="c0967-248">During the update, we now obtain the coordinate system at the time stamp obtained from with the frame prediction.</span></span>

```
   // Next, we get a coordinate system from the attached frame of reference that is
   // associated with the current frame. Later, this coordinate system is used for
   // for creating the stereo view matrices when rendering the sample content.
   SpatialCoordinateSystem^ currentCoordinateSystem =
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp);
```

### <a name="get-a-spatial-pointer-pose-and-follow-the-users-gaze"></a><span data-ttu-id="c0967-249">获取空间指针姿势，并遵循用户的注视</span><span class="sxs-lookup"><span data-stu-id="c0967-249">Get a spatial pointer pose, and follow the user's Gaze</span></span>

<span data-ttu-id="c0967-250">我们希望我们的示例全息图跟随用户的 [注视](../../design/gaze-and-commit.md)，这与全息 shell 可以遵循用户的注视方式类似。</span><span class="sxs-lookup"><span data-stu-id="c0967-250">We want our example hologram to follow the user's [gaze](../../design/gaze-and-commit.md), similar to how the holographic shell can follow the user's gaze.</span></span> <span data-ttu-id="c0967-251">为此，我们需要从相同的时间戳中获取 SpatialPointerPose。</span><span class="sxs-lookup"><span data-stu-id="c0967-251">For this, we need to get the SpatialPointerPose from the same time stamp.</span></span>

```
SpatialPointerPose^ pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
```

<span data-ttu-id="c0967-252">此 SpatialPointerPose 包含根据 [用户的当前标题](gaze-in-directx.md)放置全息影像所需的信息。</span><span class="sxs-lookup"><span data-stu-id="c0967-252">This SpatialPointerPose has the information needed to position the hologram according to the [user's current heading](gaze-in-directx.md).</span></span>

<span data-ttu-id="c0967-253">为了用户舒适，我们使用线性内插 ( "lerp" ) 在一段时间内使更改位置平滑。</span><span class="sxs-lookup"><span data-stu-id="c0967-253">For user comfort, we use linear interpolation ("lerp") to smooth the change in position over a period of time.</span></span> <span data-ttu-id="c0967-254">这比将全息图锁定到其注视的用户更适合。</span><span class="sxs-lookup"><span data-stu-id="c0967-254">This is more comfortable for the user than locking the hologram to their gaze.</span></span> <span data-ttu-id="c0967-255">Lerping 的标记，还可以通过抑制移动来使全息影像稳定。</span><span class="sxs-lookup"><span data-stu-id="c0967-255">Lerping the tag-along hologram's position also allows us to stabilize the hologram by dampening the movement.</span></span> <span data-ttu-id="c0967-256">如果未执行此抑制，用户将看到全息影像抖动，因为通常会将其视为让的用户。</span><span class="sxs-lookup"><span data-stu-id="c0967-256">If we didn't do this dampening, the user would see the hologram jitter because of what are normally considered to be imperceptible movements of the user's head.</span></span>

<span data-ttu-id="c0967-257">From **StationaryQuadRenderer：:P ositionhologram**：</span><span class="sxs-lookup"><span data-stu-id="c0967-257">From **StationaryQuadRenderer::PositionHologram**:</span></span>

```
   const float& dtime = static_cast<float>(timer.GetElapsedSeconds());

   if (pointerPose != nullptr)
   {
       // Get the gaze direction relative to the given coordinate system.
       const float3 headPosition  = pointerPose->Head->Position;
       const float3 headDirection = pointerPose->Head->ForwardDirection;

       // The tag-along hologram follows a point 2.0m in front of the user's gaze direction.
       static const float distanceFromUser = 2.0f; // meters
       const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * headDirection);

       // Lerp the position, to keep the hologram comfortably stable.
       auto lerpedPosition = lerp(m_position, gazeAtTwoMeters, dtime * c_lerpRate);

       // This will be used as the translation component of the hologram's
       // model transform.
       SetPosition(lerpedPosition);
   }
```

>[!NOTE]
><span data-ttu-id="c0967-258">对于调试面板，您可以选择将全息图从一边重定位到一边，使其不会妨碍您的视图。</span><span class="sxs-lookup"><span data-stu-id="c0967-258">In the case of a debugging panel, you might choose to reposition the hologram off to the side a little so that it doesn't obstruct your view.</span></span> <span data-ttu-id="c0967-259">下面是有关如何执行此操作的示例。</span><span class="sxs-lookup"><span data-stu-id="c0967-259">Here's an example of how you might do that.</span></span>

<span data-ttu-id="c0967-260">对于 **StationaryQuadRenderer：:P ositionhologram**：</span><span class="sxs-lookup"><span data-stu-id="c0967-260">For **StationaryQuadRenderer::PositionHologram**:</span></span>

```
       // If you're making a debug view, you might not want the tag-along to be directly in the
       // center of your field of view. Use this code to position the hologram to the right of
       // the user's gaze direction.
       /*
       const float3 offset = float3(0.13f, 0.0f, 0.f);
       static const float distanceFromUser = 2.2f; // meters
       const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * (headDirection + offset));
       */
```

### <a name="rotate-the-hologram-to-face-the-camera"></a><span data-ttu-id="c0967-261">旋转全息图以面对相机</span><span class="sxs-lookup"><span data-stu-id="c0967-261">Rotate the hologram to face the camera</span></span>

<span data-ttu-id="c0967-262">不能定位全息图（在本例中为四部分），还必须旋转对象，使其面向用户。</span><span class="sxs-lookup"><span data-stu-id="c0967-262">It isn't enough to position the hologram, which in this case is a quad; we must also rotate the object to face the user.</span></span> <span data-ttu-id="c0967-263">这种旋转发生在世界空间中，因为这种类型的 billboarding 允许全息图保留在用户的环境中。</span><span class="sxs-lookup"><span data-stu-id="c0967-263">This rotation occurs in world space, because this type of billboarding allows the hologram to remain a part of the user's environment.</span></span> <span data-ttu-id="c0967-264">由于全息图锁定为显示方向，因此，billboarding 不是很舒适：在这种情况下，你还必须在左视图和右视图矩阵之间进行插值，才能获得不会干扰立体声呈现的视图空间布告栏转换。</span><span class="sxs-lookup"><span data-stu-id="c0967-264">View-space billboarding isn't as comfortable because the hologram becomes locked to the display orientation; in that case, you would also have to interpolate between the left and right view matrices to acquire a view-space billboard transform that doesn't disrupt stereo rendering.</span></span> <span data-ttu-id="c0967-265">在这里，我们将旋转 X 和 Z 轴以面对用户。</span><span class="sxs-lookup"><span data-stu-id="c0967-265">Here, we rotate on the X and Z axes to face the user.</span></span>

<span data-ttu-id="c0967-266">From **StationaryQuadRenderer：： Update**：</span><span class="sxs-lookup"><span data-stu-id="c0967-266">From **StationaryQuadRenderer::Update**:</span></span>

```
   // Seconds elapsed since previous frame.
   const float& dTime = static_cast<float>(timer.GetElapsedSeconds());

   // Create a direction normal from the hologram's position to the origin of person space.
   // This is the z-axis rotation.
   XMVECTOR facingNormal = XMVector3Normalize(-XMLoadFloat3(&m_position));

   // Rotate the x-axis around the y-axis.
   // This is a 90-degree angle from the normal, in the xz-plane.
   // This is the x-axis rotation.
   XMVECTOR xAxisRotation = XMVector3Normalize(XMVectorSet(XMVectorGetZ(facingNormal), 0.f, -XMVectorGetX(facingNormal), 0.f));

   // Create a third normal to satisfy the conditions of a rotation matrix.
   // The cross product  of the other two normals is at a 90-degree angle to
   // both normals. (Normalize the cross product to avoid floating-point math
   // errors.)
   // Note how the cross product will never be a zero-matrix because the two normals
   // are always at a 90-degree angle from one another.
   XMVECTOR yAxisRotation = XMVector3Normalize(XMVector3Cross(facingNormal, xAxisRotation));

   // Construct the 4x4 rotation matrix.

   // Rotate the quad to face the user.
   XMMATRIX rotationMatrix = XMMATRIX(
       xAxisRotation,
       yAxisRotation,
       facingNormal,
       XMVectorSet(0.f, 0.f, 0.f, 1.f)
       );

   // Position the quad.
   const XMMATRIX modelTranslation = XMMatrixTranslationFromVector(XMLoadFloat3(&m_position));

   // The view and projection matrices are provided by the system; they are associated
   // with holographic cameras, and updated on a per-camera basis.
   // Here, we provide the model transform for the sample hologram. The model transform
   // matrix is transposed to prepare it for the shader.
   XMStoreFloat4x4(&m_modelConstantBufferData.model, XMMatrixTranspose(rotationMatrix * modelTranslation));
```

### <a name="render-the-attached-hologram"></a><span data-ttu-id="c0967-267">呈现附加全息图</span><span class="sxs-lookup"><span data-stu-id="c0967-267">Render the attached hologram</span></span>

<span data-ttu-id="c0967-268">在此示例中，我们还会选择在 SpatialLocatorAttachedReferenceFrame 的坐标系统中呈现全息影像，这是我们放置全息图的位置。</span><span class="sxs-lookup"><span data-stu-id="c0967-268">For this example, we also choose to render the hologram in the coordinate system of the SpatialLocatorAttachedReferenceFrame, which is where we positioned the hologram.</span></span> <span data-ttu-id="c0967-269"> (如果我们决定使用另一个坐标系统进行呈现，则需要从设备附加的参考框架的坐标系统到该坐标系统获取转换。 ) </span><span class="sxs-lookup"><span data-stu-id="c0967-269">(If we had decided to render using another coordinate system, we would need to acquire a transform from the device-attached reference frame's coordinate system to that coordinate system.)</span></span>

<span data-ttu-id="c0967-270">From **HolographicTagAlongSampleMain：： Render**：</span><span class="sxs-lookup"><span data-stu-id="c0967-270">From **HolographicTagAlongSampleMain::Render**:</span></span>

```
   // The view and projection matrices for each holographic camera will change
   // every frame. This function refreshes the data in the constant buffer for
   // the holographic camera indicated by cameraPose.
   pCameraResources->UpdateViewProjectionBuffer(
       m_deviceResources,
       cameraPose,
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp)
       );
```

<span data-ttu-id="c0967-271">就这么简单！</span><span class="sxs-lookup"><span data-stu-id="c0967-271">That's it!</span></span> <span data-ttu-id="c0967-272">现在，全息图将 "跟踪" 在用户看看方向上为2米的位置。</span><span class="sxs-lookup"><span data-stu-id="c0967-272">The hologram will now "chase" a position that is 2 meters in front of the user's gaze direction.</span></span>

>[!NOTE]
><span data-ttu-id="c0967-273">此示例还会加载其他内容-请参阅 StationaryQuadRenderer。</span><span class="sxs-lookup"><span data-stu-id="c0967-273">This example also loads additional content - see StationaryQuadRenderer.cpp.</span></span>

## <a name="handling-tracking-loss"></a><span data-ttu-id="c0967-274">处理跟踪丢失</span><span class="sxs-lookup"><span data-stu-id="c0967-274">Handling tracking loss</span></span>

<span data-ttu-id="c0967-275">当设备在世界各地找不到自己时，应用程序会遇到 "跟踪丢失" 的情况。</span><span class="sxs-lookup"><span data-stu-id="c0967-275">When the device can't locate itself in the world, the app experiences "tracking loss".</span></span> <span data-ttu-id="c0967-276">Windows Mixed Reality 应用应能够应对位置跟踪系统的此类中断。</span><span class="sxs-lookup"><span data-stu-id="c0967-276">Windows Mixed Reality apps should be able to handle such disruptions to the positional tracking system.</span></span> <span data-ttu-id="c0967-277">通过使用默认 SpatialLocator 上的 LocatabilityChanged 事件，可以观察到这些中断，并创建响应。</span><span class="sxs-lookup"><span data-stu-id="c0967-277">These disruptions can be observed, and responses created, by using the LocatabilityChanged event on the default SpatialLocator.</span></span>

<span data-ttu-id="c0967-278">From **AppMain：： SetHolographicSpace：**</span><span class="sxs-lookup"><span data-stu-id="c0967-278">From **AppMain::SetHolographicSpace:**</span></span>

```
   // Be able to respond to changes in the positional tracking state.
   m_locatabilityChangedToken =
       m_locator->LocatabilityChanged +=
           ref new Windows::Foundation::TypedEventHandler<SpatialLocator^, Object^>(
               std::bind(&HolographicApp1Main::OnLocatabilityChanged, this, _1, _2)
               );
```

<span data-ttu-id="c0967-279">当你的应用收到 LocatabilityChanged 事件时，它可以根据需要更改行为。</span><span class="sxs-lookup"><span data-stu-id="c0967-279">When your app receives a LocatabilityChanged event, it can change behavior as needed.</span></span> <span data-ttu-id="c0967-280">例如，在 PositionalTrackingInhibited 状态下，你的应用程序可以暂停正常操作，并呈现显示一条警告消息的 [标记](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) 。</span><span class="sxs-lookup"><span data-stu-id="c0967-280">For example, in the PositionalTrackingInhibited state, your app can pause normal operation and render a [tag-along hologram](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) that displays a warning message.</span></span>

<span data-ttu-id="c0967-281">Windows 全息应用程序模板附带了一个已为你创建的 LocatabilityChanged 处理程序。</span><span class="sxs-lookup"><span data-stu-id="c0967-281">The Windows Holographic app template comes with a LocatabilityChanged handler already created for you.</span></span> <span data-ttu-id="c0967-282">默认情况下，当位置跟踪不可用时，它将在调试控制台中显示警告。</span><span class="sxs-lookup"><span data-stu-id="c0967-282">By default, it displays a warning in the debug console when positional tracking is unavailable.</span></span> <span data-ttu-id="c0967-283">可以向此处理程序添加代码，以根据需要从应用程序中提供响应。</span><span class="sxs-lookup"><span data-stu-id="c0967-283">You can add code to this handler to provide a response as needed from your app.</span></span>

<span data-ttu-id="c0967-284">从 **AppMain：**</span><span class="sxs-lookup"><span data-stu-id="c0967-284">From **AppMain.cpp:**</span></span>

```
   void HolographicApp1Main::OnLocatabilityChanged(SpatialLocator^ sender, Object^ args)
   {
       switch (sender->Locatability)
       {
       case SpatialLocatability::Unavailable:
           // Holograms cannot be rendered.
           {
               String^ message = L"Warning! Positional tracking is " +
                                           sender->Locatability.ToString() + L".\n";
               OutputDebugStringW(message->Data());
           }
           break;

       // In the following three cases, it is still possible to place holograms using a
       // SpatialLocatorAttachedFrameOfReference.
       case SpatialLocatability::PositionalTrackingActivating:
           // The system is preparing to use positional tracking.

       case SpatialLocatability::OrientationOnly:
           // Positional tracking has not been activated.

       case SpatialLocatability::PositionalTrackingInhibited:
           // Positional tracking is temporarily inhibited. User action may be required
           // in order to restore positional tracking.
           break;

       case SpatialLocatability::PositionalTrackingActive:
           // Positional tracking is active. World-locked content can be rendered.
           break;
       }
   }
```

## <a name="spatial-mapping"></a><span data-ttu-id="c0967-285">空间映射</span><span class="sxs-lookup"><span data-stu-id="c0967-285">Spatial mapping</span></span>

<span data-ttu-id="c0967-286">[空间映射](spatial-mapping-in-directx.md)api 使用坐标系统获取 surface 网格的模型转换。</span><span class="sxs-lookup"><span data-stu-id="c0967-286">The [spatial mapping](spatial-mapping-in-directx.md) APIs make use of coordinate systems to get model transforms for surface meshes.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0967-287">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c0967-287">See also</span></span>
* [<span data-ttu-id="c0967-288">坐标系统</span><span class="sxs-lookup"><span data-stu-id="c0967-288">Coordinate systems</span></span>](../../design/coordinate-systems.md)
* [<span data-ttu-id="c0967-289">空间定位点</span><span class="sxs-lookup"><span data-stu-id="c0967-289">Spatial anchors</span></span>](../../design/spatial-anchors.md)
* <span data-ttu-id="c0967-290"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure 空间定位点</a></span><span class="sxs-lookup"><span data-stu-id="c0967-290"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* [<span data-ttu-id="c0967-291">DirectX 中的头部和眼部凝视</span><span class="sxs-lookup"><span data-stu-id="c0967-291">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="c0967-292">DirectX 中的手和运动控制器</span><span class="sxs-lookup"><span data-stu-id="c0967-292">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="c0967-293">DirectX 中的空间映射</span><span class="sxs-lookup"><span data-stu-id="c0967-293">Spatial mapping in DirectX</span></span>](spatial-mapping-in-directx.md)
