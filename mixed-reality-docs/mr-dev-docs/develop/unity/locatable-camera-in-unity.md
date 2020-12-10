---
title: Unity 中的可定位相机
description: 了解如何捕获照片到文件或 Texture2D，如何捕获照片并与原始字节交互，以及如何捕获视频。
author: wguyman
ms.author: wguyman
ms.date: 03/21/2018
ms.topic: article
keywords: 照片，视频，hololens，照相机，unity，定位，PVC，照片视频摄像机，混合现实耳机，windows mixed reality 耳机，虚拟现实耳机，网络摄像机，照片捕获，视频捕获
ms.openlocfilehash: 125521206421acbcc4c9ad6e5fb371314ddb48f2
ms.sourcegitcommit: 87b54c75044f433cfadda68ca71c1165608e2f4b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97010098"
---
# <a name="locatable-camera-in-unity"></a><span data-ttu-id="98eec-104">Unity 中的可定位相机</span><span class="sxs-lookup"><span data-stu-id="98eec-104">Locatable camera in Unity</span></span>

## <a name="enabling-the-capability-for-photo-video-camera"></a><span data-ttu-id="98eec-105">启用相片视频相机功能</span><span class="sxs-lookup"><span data-stu-id="98eec-105">Enabling the capability for Photo Video Camera</span></span>

<span data-ttu-id="98eec-106">必须为应用声明 "网络摄像机" 功能，才能使用 [相机](../platform-capabilities-and-apis/locatable-camera.md)。</span><span class="sxs-lookup"><span data-stu-id="98eec-106">The "WebCam" capability must be declared for an app to use the [camera](../platform-capabilities-and-apis/locatable-camera.md).</span></span>
1. <span data-ttu-id="98eec-107">在 Unity 编辑器中，导航到 "编辑 > 项目设置 > Player" 页，转到 "播放机" 设置。</span><span class="sxs-lookup"><span data-stu-id="98eec-107">In the Unity Editor, go to the player settings by navigating to the "Edit > Project Settings > Player" page</span></span>
2. <span data-ttu-id="98eec-108">选择 "Windows 应用商店" 选项卡</span><span class="sxs-lookup"><span data-stu-id="98eec-108">Select the "Windows Store" tab</span></span>
3. <span data-ttu-id="98eec-109">在 "发布设置 > 功能" 部分中，检查 **网络摄像机** 和 **麦克风** 功能</span><span class="sxs-lookup"><span data-stu-id="98eec-109">In the "Publishing Settings > Capabilities" section, check the **WebCam** and **Microphone** capabilities</span></span>

<span data-ttu-id="98eec-110">照相机一次只能出现一次操作。</span><span class="sxs-lookup"><span data-stu-id="98eec-110">Only a single operation can occur with the camera at a time.</span></span> <span data-ttu-id="98eec-111">你可以检查相机目前处于的模式中是否包含 UnityEngine。</span><span class="sxs-lookup"><span data-stu-id="98eec-111">You can check with mode the camera is currently in with UnityEngine.XR.WSA.WebCam.Mode.</span></span> <span data-ttu-id="98eec-112">可用模式有照片、视频或无。</span><span class="sxs-lookup"><span data-stu-id="98eec-112">Available modes are photo, video, or none.</span></span>

## <a name="photo-capture"></a><span data-ttu-id="98eec-113">照片捕获</span><span class="sxs-lookup"><span data-stu-id="98eec-113">Photo Capture</span></span>

<span data-ttu-id="98eec-114">**命名空间：** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="98eec-114">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="98eec-115">**类型：** *PhotoCapture*</span><span class="sxs-lookup"><span data-stu-id="98eec-115">**Type:** *PhotoCapture*</span></span>

<span data-ttu-id="98eec-116">*PhotoCapture* 类型允许你使用照片摄像机拍摄照片。</span><span class="sxs-lookup"><span data-stu-id="98eec-116">The *PhotoCapture* type allows you to take still photographs with the Photo Video Camera.</span></span> <span data-ttu-id="98eec-117">使用 *PhotoCapture* 拍摄照片的一般模式如下所示：</span><span class="sxs-lookup"><span data-stu-id="98eec-117">The general pattern for using *PhotoCapture* to take a photo is as follows:</span></span>
1. <span data-ttu-id="98eec-118">创建 *PhotoCapture* 对象</span><span class="sxs-lookup"><span data-stu-id="98eec-118">Create a *PhotoCapture* object</span></span>
2. <span data-ttu-id="98eec-119">使用所需的设置创建 *CameraParameters* 对象</span><span class="sxs-lookup"><span data-stu-id="98eec-119">Create a *CameraParameters* object with the settings you want</span></span>
3. <span data-ttu-id="98eec-120">通过 *StartPhotoModeAsync* 启动照片模式</span><span class="sxs-lookup"><span data-stu-id="98eec-120">Start Photo Mode via *StartPhotoModeAsync*</span></span>
4. <span data-ttu-id="98eec-121">拍摄所需照片</span><span class="sxs-lookup"><span data-stu-id="98eec-121">Take the photo you want</span></span>
    * <span data-ttu-id="98eec-122"> (可选) 与该图片交互</span><span class="sxs-lookup"><span data-stu-id="98eec-122">(optional) Interact with that picture</span></span>
5. <span data-ttu-id="98eec-123">停止照片模式并清理资源</span><span class="sxs-lookup"><span data-stu-id="98eec-123">Stop Photo Mode and clean up resources</span></span>

### <a name="common-set-up-for-photocapture"></a><span data-ttu-id="98eec-124">通用设置 PhotoCapture</span><span class="sxs-lookup"><span data-stu-id="98eec-124">Common Set Up for PhotoCapture</span></span>

<span data-ttu-id="98eec-125">对于所有这三个用途，请从上述前三个步骤开始</span><span class="sxs-lookup"><span data-stu-id="98eec-125">For all three uses, start with the same first three steps above</span></span>

<span data-ttu-id="98eec-126">首先创建 *PhotoCapture* 对象</span><span class="sxs-lookup"><span data-stu-id="98eec-126">Start by creating a *PhotoCapture* object</span></span>

```cs
PhotoCapture photoCaptureObject = null;
   void Start()
   {
       PhotoCapture.CreateAsync(false, OnPhotoCaptureCreated);
   }
```

<span data-ttu-id="98eec-127">接下来，存储对象、设置参数和启动照片模式</span><span class="sxs-lookup"><span data-stu-id="98eec-127">Next, store your object, set your parameters, and start Photo Mode</span></span>

```cs
void OnPhotoCaptureCreated(PhotoCapture captureObject)
   {
       photoCaptureObject = captureObject;

       Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();

       CameraParameters c = new CameraParameters();
       c.hologramOpacity = 0.0f;
       c.cameraResolutionWidth = cameraResolution.width;
       c.cameraResolutionHeight = cameraResolution.height;
       c.pixelFormat = CapturePixelFormat.BGRA32;

       captureObject.StartPhotoModeAsync(c, false, OnPhotoModeStarted);
   }
```

<span data-ttu-id="98eec-128">最后，你还将使用此处提供的相同清理代码</span><span class="sxs-lookup"><span data-stu-id="98eec-128">In the end, you'll also use the same clean-up code presented here</span></span>

```cs
void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
   {
       photoCaptureObject.Dispose();
       photoCaptureObject = null;
   }
```

<span data-ttu-id="98eec-129">完成这些步骤后，你可以选择要捕获哪种类型的照片。</span><span class="sxs-lookup"><span data-stu-id="98eec-129">After these steps, you can choose which type of photo to capture.</span></span>

### <a name="capture-a-photo-to-a-file"></a><span data-ttu-id="98eec-130">将照片捕获到文件</span><span class="sxs-lookup"><span data-stu-id="98eec-130">Capture a Photo to a File</span></span>

<span data-ttu-id="98eec-131">最简单的操作是将照片直接捕获到文件中。</span><span class="sxs-lookup"><span data-stu-id="98eec-131">The simplest operation is to capture a photo directly to a file.</span></span> <span data-ttu-id="98eec-132">照片可以保存为 JPG 或 PNG。</span><span class="sxs-lookup"><span data-stu-id="98eec-132">The photo can be saved as a JPG or a PNG.</span></span>

<span data-ttu-id="98eec-133">如果已成功启动照片模式，拍摄照片并将其存储在磁盘上</span><span class="sxs-lookup"><span data-stu-id="98eec-133">If you successfully started photo mode, take a photo and store it on disk</span></span>

```cs
private void OnPhotoModeStarted(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           string filename = string.Format(@"CapturedImage{0}_n.jpg", Time.time);
           string filePath = System.IO.Path.Combine(Application.persistentDataPath, filename);

           photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);
       }
       else
       {
           Debug.LogError("Unable to start photo mode!");
       }
   }
```

<span data-ttu-id="98eec-134">将照片捕获到磁盘后，退出照片模式，然后清理对象</span><span class="sxs-lookup"><span data-stu-id="98eec-134">After capturing the photo to disk, exit photo mode and then clean up your objects</span></span>

```cs
void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           Debug.Log("Saved Photo to disk!");
           photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
       }
       else
       {
           Debug.Log("Failed to save Photo to disk");
       }
   }
```

### <a name="capture-a-photo-to-a-texture2d"></a><span data-ttu-id="98eec-135">将照片捕获到 Texture2D</span><span class="sxs-lookup"><span data-stu-id="98eec-135">Capture a Photo to a Texture2D</span></span>

<span data-ttu-id="98eec-136">将数据捕获到 Texture2D 时，该过程类似于捕获到磁盘。</span><span class="sxs-lookup"><span data-stu-id="98eec-136">When capturing data to a Texture2D, the process is similar to capturing to disk.</span></span>

<span data-ttu-id="98eec-137">按照上面的设置过程进行操作。</span><span class="sxs-lookup"><span data-stu-id="98eec-137">Follow the setup process above.</span></span>

<span data-ttu-id="98eec-138">在 *OnPhotoModeStarted* 中，将帧捕获到内存。</span><span class="sxs-lookup"><span data-stu-id="98eec-138">In *OnPhotoModeStarted*, capture a frame to memory.</span></span>

```cs
private void OnPhotoModeStarted(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           photoCaptureObject.TakePhotoAsync(OnCapturedPhotoToMemory);
       }
       else
       {
           Debug.LogError("Unable to start photo mode!");
       }
   }
```

<span data-ttu-id="98eec-139">然后，将结果应用到纹理，并使用上面的常见清理代码。</span><span class="sxs-lookup"><span data-stu-id="98eec-139">You'll then apply your result to a texture and use the common clean-up code above.</span></span>

```cs
void OnCapturedPhotoToMemory(PhotoCapture.PhotoCaptureResult result, PhotoCaptureFrame photoCaptureFrame)
   {
       if (result.success)
       {
           // Create our Texture2D for use and set the correct resolution
           Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();
           Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);
           // Copy the raw image data into our target texture
           photoCaptureFrame.UploadImageDataToTexture(targetTexture);
           // Do as we wish with the texture such as apply it to a material, etc.
       }
       // Clean up
       photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
   }
```

### <a name="capture-a-photo-and-interact-with-the-raw-bytes"></a><span data-ttu-id="98eec-140">捕获照片并与原始字节交互</span><span class="sxs-lookup"><span data-stu-id="98eec-140">Capture a Photo and Interact with the Raw bytes</span></span>

<span data-ttu-id="98eec-141">若要与内存中帧的原始字节交互，请按照与在 Texture2D 中捕获 *照片时相同* 的设置步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="98eec-141">To interact with the raw bytes of an in memory frame, follow the same setup steps as above and *OnPhotoModeStarted* as in capturing a photo to a Texture2D.</span></span> <span data-ttu-id="98eec-142">不同之处在于，可在 *OnCapturedPhotoToMemory* 中获取原始字节并与其进行交互。</span><span class="sxs-lookup"><span data-stu-id="98eec-142">The difference is in *OnCapturedPhotoToMemory* where you can get the raw bytes and interact with them.</span></span>

<span data-ttu-id="98eec-143">在此示例中，你将创建 *一个 <Color> 列表*，通过 SetPixels 将其进一步处理或应用于纹理 *( # B1*</span><span class="sxs-lookup"><span data-stu-id="98eec-143">In this example, you'll create a *List<Color>* to be further processed or applied to a texture via *SetPixels()*</span></span>

```cs
void OnCapturedPhotoToMemory(PhotoCapture.PhotoCaptureResult result, PhotoCaptureFrame photoCaptureFrame)
   {
       if (result.success)
       {
           List<byte> imageBufferList = new List<byte>();
           // Copy the raw IMFMediaBuffer data into our empty byte list.
           photoCaptureFrame.CopyRawImageDataIntoBuffer(imageBufferList);

           // In this example, we captured the image using the BGRA32 format.
           // So our stride will be 4 since we have a byte for each rgba channel.
           // The raw image data will also be flipped so we access our pixel data
           // in the reverse order.
           int stride = 4;
           float denominator = 1.0f / 255.0f;
           List<Color> colorArray = new List<Color>();
           for (int i = imageBufferList.Count - 1; i >= 0; i -= stride)
           {
               float a = (int)(imageBufferList[i - 0]) * denominator;
               float r = (int)(imageBufferList[i - 1]) * denominator;
               float g = (int)(imageBufferList[i - 2]) * denominator;
               float b = (int)(imageBufferList[i - 3]) * denominator;

               colorArray.Add(new Color(r, g, b, a));
           }
           // Now we could do something with the array such as texture.SetPixels() or run image processing on the list
       }
       photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
   }
```

## <a name="video-capture"></a><span data-ttu-id="98eec-144">视频捕获</span><span class="sxs-lookup"><span data-stu-id="98eec-144">Video Capture</span></span>

<span data-ttu-id="98eec-145">**命名空间：** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="98eec-145">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="98eec-146">**类型：** *VideoCapture*</span><span class="sxs-lookup"><span data-stu-id="98eec-146">**Type:** *VideoCapture*</span></span>

<span data-ttu-id="98eec-147">*VideoCapture* 函数类似于 *PhotoCapture*。</span><span class="sxs-lookup"><span data-stu-id="98eec-147">*VideoCapture* functions similarly to *PhotoCapture*.</span></span> <span data-ttu-id="98eec-148">唯一的两个不同之处在于，每秒必须指定帧数 (FPS) 值，并且只能将磁盘直接保存为..。</span><span class="sxs-lookup"><span data-stu-id="98eec-148">The only two differences are that you must specify a Frames Per Second (FPS) value and you can only save directly to disk as a .mp4 file.</span></span> <span data-ttu-id="98eec-149">使用 *VideoCapture* 的步骤如下所示：</span><span class="sxs-lookup"><span data-stu-id="98eec-149">The steps to use *VideoCapture* are as follows:</span></span>
1. <span data-ttu-id="98eec-150">创建 *VideoCapture* 对象</span><span class="sxs-lookup"><span data-stu-id="98eec-150">Create a *VideoCapture* object</span></span>
2. <span data-ttu-id="98eec-151">使用所需的设置创建 *CameraParameters* 对象</span><span class="sxs-lookup"><span data-stu-id="98eec-151">Create a *CameraParameters* object with the settings you want</span></span>
3. <span data-ttu-id="98eec-152">通过 *StartVideoModeAsync* 启动视频模式</span><span class="sxs-lookup"><span data-stu-id="98eec-152">Start Video Mode via *StartVideoModeAsync*</span></span>
4. <span data-ttu-id="98eec-153">开始录制视频</span><span class="sxs-lookup"><span data-stu-id="98eec-153">Start recording video</span></span>
5. <span data-ttu-id="98eec-154">停止录制视频</span><span class="sxs-lookup"><span data-stu-id="98eec-154">Stop recording video</span></span>
6. <span data-ttu-id="98eec-155">停止视频模式并清理资源</span><span class="sxs-lookup"><span data-stu-id="98eec-155">Stop Video Mode and clean up resources</span></span>

<span data-ttu-id="98eec-156">首先，创建 *VideoCapture* 对象 *VideoCapture m_VideoCapture = null;*</span><span class="sxs-lookup"><span data-stu-id="98eec-156">Start by creating our *VideoCapture* object *VideoCapture m_VideoCapture = null;*</span></span>

```cs
void Start ()
   {
       VideoCapture.CreateAsync(false, OnVideoCaptureCreated);
   }
```

<span data-ttu-id="98eec-157">接下来，设置要用于记录和启动的参数。</span><span class="sxs-lookup"><span data-stu-id="98eec-157">Next, set up the parameters you'll want for the recording and start.</span></span>

```cs
void OnVideoCaptureCreated (VideoCapture videoCapture)
   {
       if (videoCapture != null)
       {
           m_VideoCapture = videoCapture;

           Resolution cameraResolution = VideoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();
           float cameraFramerate = VideoCapture.GetSupportedFrameRatesForResolution(cameraResolution).OrderByDescending((fps) => fps).First();

           CameraParameters cameraParameters = new CameraParameters();
           cameraParameters.hologramOpacity = 0.0f;
           cameraParameters.frameRate = cameraFramerate;
           cameraParameters.cameraResolutionWidth = cameraResolution.width;
           cameraParameters.cameraResolutionHeight = cameraResolution.height;
           cameraParameters.pixelFormat = CapturePixelFormat.BGRA32;

           m_VideoCapture.StartVideoModeAsync(cameraParameters,
                                               VideoCapture.AudioState.None,
                                               OnStartedVideoCaptureMode);
       }
       else
       {
           Debug.LogError("Failed to create VideoCapture Instance!");
       }
   }
```

<span data-ttu-id="98eec-158">启动后，开始记录</span><span class="sxs-lookup"><span data-stu-id="98eec-158">Once started, begin the recording</span></span>

```cs
void OnStartedVideoCaptureMode(VideoCapture.VideoCaptureResult result)
   {
       if (result.success)
       {
           string filename = string.Format("MyVideo_{0}.mp4", Time.time);
           string filepath = System.IO.Path.Combine(Application.persistentDataPath, filename);

           m_VideoCapture.StartRecordingAsync(filepath, OnStartedRecordingVideo);
       }
   }
```

<span data-ttu-id="98eec-159">记录开始后，你可以更新你的 UI 或行为以启用停止。</span><span class="sxs-lookup"><span data-stu-id="98eec-159">After recording has started, you could update your UI or behaviors to enable stopping.</span></span> <span data-ttu-id="98eec-160">在这里，你只需记录。</span><span class="sxs-lookup"><span data-stu-id="98eec-160">Here you just log.</span></span>

```cs
void OnStartedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Started Recording Video!");
       // We will stop the video from recording via other input such as a timer or a tap, etc.
   }
```

<span data-ttu-id="98eec-161">稍后，你将需要使用计时器或用户输入来停止记录，例如。</span><span class="sxs-lookup"><span data-stu-id="98eec-161">At a later point, you'll want to stop the recording using a timer or user input, for instance.</span></span>

```cs
// The user has indicated to stop recording
   void StopRecordingVideo()
   {
       m_VideoCapture.StopRecordingAsync(OnStoppedRecordingVideo);
   }
```

<span data-ttu-id="98eec-162">录制停止后，停止视频模式并清理资源。</span><span class="sxs-lookup"><span data-stu-id="98eec-162">Once the recording has stopped, stop video mode and clean up your resources.</span></span>

```cs
void OnStoppedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Stopped Recording Video!");
       m_VideoCapture.StopVideoModeAsync(OnStoppedVideoCaptureMode);
   }

   void OnStoppedVideoCaptureMode(VideoCapture.VideoCaptureResult result)
   {
       m_VideoCapture.Dispose();
       m_VideoCapture = null;
   }
```

## <a name="troubleshooting"></a><span data-ttu-id="98eec-163">疑难解答</span><span class="sxs-lookup"><span data-stu-id="98eec-163">Troubleshooting</span></span>
* <span data-ttu-id="98eec-164">无可用解决方案</span><span class="sxs-lookup"><span data-stu-id="98eec-164">No resolutions are available</span></span>
    * <span data-ttu-id="98eec-165">确保在项目中指定了 **网络摄像机** 功能。</span><span class="sxs-lookup"><span data-stu-id="98eec-165">Ensure the **WebCam** capability is specified in your project.</span></span>

## <a name="next-development-checkpoint"></a><span data-ttu-id="98eec-166">下一个开发检查点</span><span class="sxs-lookup"><span data-stu-id="98eec-166">Next Development Checkpoint</span></span>

<span data-ttu-id="98eec-167">如果遵循我们所说的 Unity 开发检查点旅程，就是探索混合现实平台功能和 Api。</span><span class="sxs-lookup"><span data-stu-id="98eec-167">If you're following the Unity development checkpoint journey we've laid out, you're in the midst of exploring the Mixed Reality platform capabilities and APIs.</span></span> <span data-ttu-id="98eec-168">从这里，你可以继续学习下一主题：</span><span class="sxs-lookup"><span data-stu-id="98eec-168">From here, you can continue to the next topic:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98eec-169">焦点</span><span class="sxs-lookup"><span data-stu-id="98eec-169">Focus point</span></span>](focus-point-in-unity.md)

<span data-ttu-id="98eec-170">或直接跳到在设备或模拟器上部署应用：</span><span class="sxs-lookup"><span data-stu-id="98eec-170">Or jump directly to deploying your app on a device or emulator:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98eec-171">部署到 HoloLens 或 Windows Mixed Reality 沉浸式耳机</span><span class="sxs-lookup"><span data-stu-id="98eec-171">Deploy to HoloLens or Windows Mixed Reality immersive headsets</span></span>](../platform-capabilities-and-apis/using-visual-studio.md)

<span data-ttu-id="98eec-172">你可以随时返回到 [Unity 开发检查点](unity-development-overview.md#3-platform-capabilities-and-apis)。</span><span class="sxs-lookup"><span data-stu-id="98eec-172">You can always go back to the [Unity development checkpoints](unity-development-overview.md#3-platform-capabilities-and-apis) at any time.</span></span>

## <a name="see-also"></a><span data-ttu-id="98eec-173">另请参阅</span><span class="sxs-lookup"><span data-stu-id="98eec-173">See Also</span></span>
* [<span data-ttu-id="98eec-174">可定位相机</span><span class="sxs-lookup"><span data-stu-id="98eec-174">Locatable camera</span></span>](../platform-capab ilities-and-apis/locatable-camera.md)
