---
title: 立体渲染
description: 容量耗尽映像包含丰富的信息，这些信息具有不透明度和颜色在整个卷中，无法轻松地表示为表面。 了解如何在 Windows Mixed Reality 内有效呈现容量耗尽映像。
author: kevinkennedy
ms.author: kkennedy
ms.date: 03/21/2018
ms.topic: article
keywords: 容量耗尽映像，卷渲染，性能，混合现实
ms.openlocfilehash: 6dbb49c31761d4b7b9da5060d15763c3925be754
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91676987"
---
# <a name="volume-rendering"></a><span data-ttu-id="e90ca-105">立体渲染</span><span class="sxs-lookup"><span data-stu-id="e90ca-105">Volume rendering</span></span>

<span data-ttu-id="e90ca-106">对于医学 MRI 或工程量，请参阅 [维基百科上的卷渲染](https://en.wikipedia.org/wiki/Volume_rendering)。</span><span class="sxs-lookup"><span data-stu-id="e90ca-106">For medical MRI or engineering volumes, see [Volume Rendering on Wikipedia](https://en.wikipedia.org/wiki/Volume_rendering).</span></span> <span data-ttu-id="e90ca-107">这些 "容量耗尽 images" 包含丰富的信息，其中包含在整个卷中不透明度和颜色的颜色，无法轻松地表示为表面（如 [多边形网格](https://en.wikipedia.org/wiki/Polygon_mesh)）。</span><span class="sxs-lookup"><span data-stu-id="e90ca-107">These 'volumetric images' contain rich information with opacity and color throughout the volume that cannot be easily expressed as surfaces such as [polygonal meshes](https://en.wikipedia.org/wiki/Polygon_mesh).</span></span>

<span data-ttu-id="e90ca-108">用于提高性能的关键解决方案</span><span class="sxs-lookup"><span data-stu-id="e90ca-108">Key solutions to improve performance</span></span>
1. <span data-ttu-id="e90ca-109">糟糕：简单的方法：显示整个卷，通常运行速度太慢</span><span class="sxs-lookup"><span data-stu-id="e90ca-109">BAD: Naïve Approach: Show Whole Volume, generally runs too slowly</span></span>
2. <span data-ttu-id="e90ca-110">好：切削平面：仅显示卷的单个扇区</span><span class="sxs-lookup"><span data-stu-id="e90ca-110">GOOD: Cutting Plane: Show only a single slice of the volume</span></span>
3. <span data-ttu-id="e90ca-111">好：削减子卷：仅显示卷的几个层</span><span class="sxs-lookup"><span data-stu-id="e90ca-111">GOOD: Cutting Sub-Volume: Show only a few layers of the volume</span></span>
4. <span data-ttu-id="e90ca-112">好：降低了卷渲染的分辨率 (参阅 "混合分辨率场景渲染" ) </span><span class="sxs-lookup"><span data-stu-id="e90ca-112">GOOD: Lower the resolution of the volume rendering (see 'Mixed Resolution Scene Rendering')</span></span>

<span data-ttu-id="e90ca-113">只有一定数量的信息可从应用程序传输到屏幕上的任何特定帧（这是总内存带宽）。</span><span class="sxs-lookup"><span data-stu-id="e90ca-113">There is only a certain amount of information that can be transferred from the application to the screen in any particular frame, which is the total memory bandwidth.</span></span> <span data-ttu-id="e90ca-114">此外，转换该数据以进行演示需要的任何处理 (或 "底纹" ) 需要时间。</span><span class="sxs-lookup"><span data-stu-id="e90ca-114">Also, any processing (or 'shading') required to transform that data for presentation requires time.</span></span> <span data-ttu-id="e90ca-115">执行卷渲染时的主要注意事项如下：</span><span class="sxs-lookup"><span data-stu-id="e90ca-115">The primary considerations when doing volume rendering are as such:</span></span>
* <span data-ttu-id="e90ca-116">屏幕宽度 \* 屏幕高度 \* 屏幕上的屏幕计数 \* 每帧的总容量-每帧样本数</span><span class="sxs-lookup"><span data-stu-id="e90ca-116">Screen-Width \* Screen-Height \* Screen-Count \* Volume-Layers-On-That-Pixel = Total-Volume-Samples-Per-Frame</span></span>
* <span data-ttu-id="e90ca-117">1028 \* 720 \* 2 \* 256 = 378961920 (100% )  (全速卷：样本太多) </span><span class="sxs-lookup"><span data-stu-id="e90ca-117">1028 \* 720 \* 2 \* 256 = 378961920 (100%) (full res volume: too many samples)</span></span>
* <span data-ttu-id="e90ca-118">1028 \* 720 \* 2 \* 1 = 1480320 (完全) 的 0.3% (瘦切片：1个像素采样，能顺利运行) </span><span class="sxs-lookup"><span data-stu-id="e90ca-118">1028 \* 720 \* 2 \* 1 = 1480320 (0.3% of full) (thin slice: 1 sample per pixel, runs smoothly)</span></span>
* <span data-ttu-id="e90ca-119">1028 \* 720 \* 2 \* 10 = 14803200 (完整) 的 3.9% (子卷切片：每个像素10个样本，以相当平滑的形式运行，以三维形式显示) </span><span class="sxs-lookup"><span data-stu-id="e90ca-119">1028 \* 720 \* 2 \* 10 = 14803200 (3.9% of full) (sub-volume slice: 10 samples per pixel, runs fairly smoothly, looks 3d)</span></span>
* <span data-ttu-id="e90ca-120">200 \* 200 \* 2 \* 256 = 20480000 (完全) 的 5% (减小分辨率量：更少的像素，整卷，看上去是三维但有点模糊) </span><span class="sxs-lookup"><span data-stu-id="e90ca-120">200 \* 200 \* 2 \* 256 = 20480000 (5% of full) (lower res volume: fewer pixels, full volume, looks 3d but a bit blurry)</span></span>

## <a name="representing-3d-textures"></a><span data-ttu-id="e90ca-121">表示三维纹理</span><span class="sxs-lookup"><span data-stu-id="e90ca-121">Representing 3D Textures</span></span>

<span data-ttu-id="e90ca-122">在 CPU 上：</span><span class="sxs-lookup"><span data-stu-id="e90ca-122">On the CPU:</span></span>

```
public struct Int3 { public int X, Y, Z; /* ... */ }
 public class VolumeHeader  {
   public readonly Int3 Size;
   public VolumeHeader(Int3 size) { this.Size = size;  }
   public int CubicToLinearIndex(Int3 index) {
     return index.X + (index.Y * (Size.X)) + (index.Z * (Size.X * Size.Y));
   }
   public Int3 LinearToCubicIndex(int linearIndex)
   {
     return new Int3((linearIndex / 1) % Size.X,
       (linearIndex / Size.X) % Size.Y,
       (linearIndex / (Size.X * Size.Y)) % Size.Z);
   }
   /* ... */
 }
 public class VolumeBuffer<T> {
   public readonly VolumeHeader Header;
   public readonly T[] DataArray;
   public T GetVoxel(Int3 pos)        {
     return this.DataArray[this.Header.CubicToLinearIndex(pos)];
   }
   public void SetVoxel(Int3 pos, T val)        {
     this.DataArray[this.Header.CubicToLinearIndex(pos)] = val;
   }
   public T this[Int3 pos] {
     get { return this.GetVoxel(pos); }
     set { this.SetVoxel(pos, value); }
   }
   /* ... */
 }
```

<span data-ttu-id="e90ca-123">在 GPU 上：</span><span class="sxs-lookup"><span data-stu-id="e90ca-123">On the GPU:</span></span>

```
float3 _VolBufferSize;
 int3 UnitVolumeToIntVolume(float3 coord) {
   return (int3)( coord * _VolBufferSize.xyz );
 }
 int IntVolumeToLinearIndex(int3 coord, int3 size) {
   return coord.x + ( coord.y * size.x ) + ( coord.z * ( size.x * size.y ) );
 }
 uniform StructuredBuffer<float> _VolBuffer;
 float SampleVol(float3 coord3 ) {
   int3 intIndex3 = UnitVolumeToIntVolume( coord3 );
   int index1D = IntVolumeToLinearIndex( intIndex3, _VolBufferSize.xyz);
   return __VolBuffer[index1D];
 }
```

## <a name="shading-and-gradients"></a><span data-ttu-id="e90ca-124">底纹和渐变</span><span class="sxs-lookup"><span data-stu-id="e90ca-124">Shading and Gradients</span></span>

<span data-ttu-id="e90ca-125">如何对音量（如 MRI）进行着色，以便进行有用的可视化。</span><span class="sxs-lookup"><span data-stu-id="e90ca-125">How to shade a volume, such as MRI, for useful visualization.</span></span> <span data-ttu-id="e90ca-126">主要方法是将 "强度" 窗口 (要在其中查看亮度的最小值和最大) ，只需将其缩放到该空间即可查看黑色和白色强度。</span><span class="sxs-lookup"><span data-stu-id="e90ca-126">The primary method is to have an 'intensity window' (a min and max) that you want to see intensities within, and simply scale into that space to see the black and white intensity.</span></span> <span data-ttu-id="e90ca-127">然后，可以将 "颜色斜坡" 应用于该范围内的值，并将其存储为纹理，以便强度密度的不同部分可以着色不同的颜色：</span><span class="sxs-lookup"><span data-stu-id="e90ca-127">A 'color ramp' can then be applied to the values within that range, and stored as a texture, so that different parts of the intensity spectrum can be shaded different colors:</span></span>

```
float4 ShadeVol( float intensity ) {
   float unitIntensity = saturate( intensity - IntensityMin / ( IntensityMax - IntensityMin ) );
   // Simple two point black and white intensity:
   color.rgba = unitIntensity;
   // Color ramp method:
   color.rgba = tex2d( ColorRampTexture, float2( unitIntensity, 0 ) );
```

<span data-ttu-id="e90ca-128">在许多应用程序中，我们都将原始强度值和 "分段索引" (用于细分外观和骨骼等不同部分;这些段通常由专家在) 专用工具中创建。</span><span class="sxs-lookup"><span data-stu-id="e90ca-128">In many of our applications, we store in our volume both a raw intensity value and a 'segmentation index' (to segment different parts such as skin and bone; these segments are generally created by experts in dedicated tools).</span></span> <span data-ttu-id="e90ca-129">这可以与上述方法结合使用，为每个段索引放置不同的颜色，甚至不同的颜色斜坡：</span><span class="sxs-lookup"><span data-stu-id="e90ca-129">This can be combined with the approach above to put a different color, or even different color ramp for each segment index:</span></span>

```
// Change color to match segment index (fade each segment towards black):
 color.rgb = SegmentColors[ segment_index ] * color.a; // brighter alpha gives brighter color
```

## <a name="volume-slicing-in-a-shader"></a><span data-ttu-id="e90ca-130">着色器中的卷切片</span><span class="sxs-lookup"><span data-stu-id="e90ca-130">Volume Slicing in a Shader</span></span>

<span data-ttu-id="e90ca-131">第一步是创建一个可在卷上移动的 "切片平面"、"切分它" 以及每个点的扫描值。</span><span class="sxs-lookup"><span data-stu-id="e90ca-131">A great first step is to create a "slicing plane" that can move through the volume, 'slicing it', and how the scan values at each point.</span></span> <span data-ttu-id="e90ca-132">这假设有一个 "VolumeSpace" 多维数据集，该多维数据集表示卷在世界空间中的位置，可用作放置点的参考：</span><span class="sxs-lookup"><span data-stu-id="e90ca-132">This assumes that there is a 'VolumeSpace' cube, which represents where the volume is in world space, that can be used as a reference for placing the points:</span></span>

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos, 1));
```

```
// In the pixel shader:
 float4 color = ShadeVol( SampleVol( volSpace ) );
```

## <a name="volume-tracing-in-shaders"></a><span data-ttu-id="e90ca-133">着色中的卷跟踪</span><span class="sxs-lookup"><span data-stu-id="e90ca-133">Volume Tracing in Shaders</span></span>

<span data-ttu-id="e90ca-134">如何使用 GPU 执行子卷跟踪 (会经历几个 voxels 深度，然后将数据从后到前一层) ：</span><span class="sxs-lookup"><span data-stu-id="e90ca-134">How to use the GPU to do sub-volume tracing (walks a few voxels deep, then layers on the data from back to front):</span></span>

```
float4 AlphaBlend(float4 dst, float4 src) {
   float4 res = (src * src.a) + (dst - dst * src.a);
   res.a = src.a + (dst.a - dst.a*src.a);
   return res;
 }
 float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 0.15; // depth in volume space, customize!!!
   float numLoops = 10; // can be 400 on nice PC
   float4 curColor = float4(0, 0, 0, 0);
   // Figure out front and back volume coords to walk through:
   float3 frontCoord = objPosStart;
   float3 backCoord = frontPos + (normalize(cameraPosVolSpace - objPosStart) * maxDepth);
   float3 stepCoord = (frontCoord - backCoord) / numLoops;
   float3 curCoord = backCoord;
   // Add per-pixel random offset, avoids layer aliasing:
   curCoord += stepCoord * RandomFromPositionFast(objPosStart);
   // Walk from back to front (to make front appear in-front of back):
   for (float i = 0; i < numLoops; i++) {
     float intensity = SampleVol(curCoord);
     float4 shaded = ShadeVol(intensity);
     curColor = AlphaBlend(curColor, shaded);
     curCoord += stepCoord;
   }
   return curColor;
 }
```

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos.xyz, 1));
 float4 cameraInVolSpace = mul(_WorldToVolume, float4(_WorldSpaceCameraPos.xyz, 1));
```

```
// In the pixel shader:
 float4 color = volTraceSubVolume( volSpace, cameraInVolSpace );
```

## <a name="whole-volume-rendering"></a><span data-ttu-id="e90ca-135">整个卷渲染</span><span class="sxs-lookup"><span data-stu-id="e90ca-135">Whole Volume Rendering</span></span>

<span data-ttu-id="e90ca-136">修改上述子卷代码后，我们将获得：</span><span class="sxs-lookup"><span data-stu-id="e90ca-136">Modifying the sub-volume code above, we get:</span></span>

```
float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 1.73; // sqrt(3), max distance from point on cube to any other point on cube
   int maxSamples = 400; // just in case, keep this value within bounds
   // not shown: trim front and back positions to both be within the cube
   int distanceInVoxels = length(UnitVolumeToIntVolume(frontPos - backPos)); // measure distance in voxels
   int numLoops = min( distanceInVoxels, maxSamples ); // put a min on the voxels to sample
```

## <a name="mixed-resolution-scene-rendering"></a><span data-ttu-id="e90ca-137">混合分辨率场景呈现</span><span class="sxs-lookup"><span data-stu-id="e90ca-137">Mixed Resolution Scene Rendering</span></span>

<span data-ttu-id="e90ca-138">如何以低分辨率渲染场景的一部分并将其放回原位：</span><span class="sxs-lookup"><span data-stu-id="e90ca-138">How to render a part of the scene with a low resolution and put it back in place:</span></span>
1. <span data-ttu-id="e90ca-139">设置两个离线相机，每个屏幕上都有一个用于更新每个帧的</span><span class="sxs-lookup"><span data-stu-id="e90ca-139">Setup two off-screen cameras, one to follow each eye that update each frame</span></span>
2. <span data-ttu-id="e90ca-140">设置两个低分辨率呈现目标 (例如200x200 大小每个照相机所呈现到的) </span><span class="sxs-lookup"><span data-stu-id="e90ca-140">Setup two low-resolution render targets (i.e. 200x200 each) that the cameras render into</span></span>
3. <span data-ttu-id="e90ca-141">设置在用户前移动的四个</span><span class="sxs-lookup"><span data-stu-id="e90ca-141">Setup a quad that moves in front of the user</span></span>

<span data-ttu-id="e90ca-142">每个帧：</span><span class="sxs-lookup"><span data-stu-id="e90ca-142">Each Frame:</span></span>
1. <span data-ttu-id="e90ca-143">在低分辨率 (卷数据、昂贵着色器等）中绘制每个眼睛的渲染目标 ) </span><span class="sxs-lookup"><span data-stu-id="e90ca-143">Draw the render targets for each eye at low-resolution (volume data, expensive shaders, etc.)</span></span>
2. <span data-ttu-id="e90ca-144">通常将场景绘制为 (网格、UI 等的完整分辨率 ) </span><span class="sxs-lookup"><span data-stu-id="e90ca-144">Draw the scene normally as full resolution (meshes, UI, etc.)</span></span>
3. <span data-ttu-id="e90ca-145">在用户前、场景上绘制四核，并将低分辨率呈现到</span><span class="sxs-lookup"><span data-stu-id="e90ca-145">Draw a quad in front of the user, over the scene, and project the low-res renders onto that</span></span>
4. <span data-ttu-id="e90ca-146">结果：包含低分辨率但高密度卷数据的完整分辨率元素的直观组合</span><span class="sxs-lookup"><span data-stu-id="e90ca-146">Result: visual combination of full-resolution elements with low-resolution but high-density volume data</span></span>
