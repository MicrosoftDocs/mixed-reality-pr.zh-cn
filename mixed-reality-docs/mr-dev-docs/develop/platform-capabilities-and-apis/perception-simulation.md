---
title: 感知模拟
description: 使用感知模拟库自动完成沉浸式应用程序模拟输入的指南
author: pbarnettms
ms.author: pbarnett
ms.date: 05/12/2020
ms.topic: article
keywords: HoloLens，模拟，测试
ms.openlocfilehash: 64028c3a1ad58cecfebc93aee325b73c3a6a649a
ms.sourcegitcommit: c41372e0c6ca265f599bff309390982642d628b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97530394"
---
# <a name="perception-simulation"></a>感知模拟

是否要为应用生成自动测试？ 是否希望你的测试超出组件级别的单元测试，并真正运用端到端应用？ 感知模拟是你要查找的内容。 感知模拟库将人类和世界输入数据发送到你的应用，因此你可以自动执行测试。 例如，可以模拟查找特定的可重复位置的人工输入，然后使用笔势或运动控制器。

感知模拟可以将此类模拟输入发送到物理 HoloLens，HoloLens 模拟器 (第一代) 、HoloLens 2 模拟器或安装有混合现实门户的 PC。 感知模拟会绕过混合现实设备上的实时传感器，并将模拟输入发送到设备上运行的应用程序。 应用程序通过它们始终使用的相同 Api 来接收这些输入事件，无法判断运行与感知模拟之间的差异。 认知模拟是将模拟输入发送到 HoloLens 虚拟机所使用的一种技术。

若要开始在代码中使用模拟，请首先创建 IPerceptionSimulationManager 对象。 在该对象中，可以发出命令来控制模拟 "人体" 的属性，包括头位置、手形位置和手势。 还可以启用和操作运动控制器。

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a>设置用于感知模拟的 Visual Studio 项目
1. 在开发电脑上[安装 HoloLens 模拟器](../install-the-tools.md)。 模拟器包含用于感知模拟的库。
2. 创建新的 Visual Studio c # 桌面项目 (控制台项目非常适合) 入门。
3. 将以下二进制文件添加到项目中，作为 (项目->添加 >引用 ... ) 中的引用。可以在% ProgramFiles (x86) % \ Microsoft XDE \\ () 版本中找到它们，例如，为 HoloLens 2 模拟器% **ProgramFiles (x86) % \ microsoft XDE \\ 10.0.18362.0** 。   (注意：尽管二进制文件是 HoloLens 2 模拟器的一部分，但它们也适用于桌面上的 Windows Mixed Reality。 ) 。 用于感知模拟的 PerceptionSimulationManager.Interop.dll 托管 c # 包装。
    b. 用于设置到 HoloLens 或仿真程序的 web 套接字通信通道的 PerceptionSimulationRest.dll 库。
    c. 用于模拟 SimulationStream.Interop.dll 共享的类型。
4. 将实现二进制 PerceptionSimulationManager.dll 添加到项目 a。 首先将它作为二进制添加到项目 (项目->添加 >的现有项 ... ) 。将其保存为链接，使其不会将其复制到项目源文件夹。 ![将 PerceptionSimulationManager.dll 作为链接 b 添加到项目 ](images/saveaslink.png) 。 然后，确保它在生成时复制到输出文件夹。 这位于二进制文件的属性表中。 ![将 PerceptionSimulationManager.dll 标记为复制到输出目录](images/copyalways.png)
5. 将活动解决方案平台设置为 x64。   (使用 Configuration Manager 为 x64 创建平台项（如果尚不存在）。 ) 

## <a name="creating-an-iperceptionsimulation-manager-object"></a>创建 IPerceptionSimulation Manager 对象

若要控制模拟，你将对从 IPerceptionSimulationManager 对象检索到的对象进行更新。 第一步是获取该对象，并将其连接到目标设备或仿真程序。 可以通过单击[工具栏](using-the-hololens-emulator.md)中的 "设备门户" 按钮来获取仿真程序的 IP 地址。

![打开设备门户图标 ](images/emulator-deviceportal.png) **打开设备门户**：在模拟器中打开用于 HoloLens OS 的 Windows 设备门户。  对于 Windows Mixed Reality，可以在 "设置" 应用程序中的 "更新 & 安全性" 下检索此项，然后在 "启用设备门户" 下的 "连接使用：" 部分中的 "开发人员"。  请务必记下 IP 地址和端口。

首先，调用 RestSimulationStreamSink 来获取 RestSimulationStreamSink 对象。 这是你将通过 http 连接控制的目标设备或仿真程序。 命令将传递到设备或模拟器上运行的 [Windows 设备门户](using-the-windows-device-portal.md) 并进行处理。 创建对象需要四个参数：
* Uri uri-目标设备的 IP 地址 (例如，" https://123.123.123.123 " 或 " https://123.123.123.123:50080 " ) 
* 系统 NetworkCredential 凭据-用于在目标设备或模拟器上连接到 [Windows 设备门户](using-the-windows-device-portal.md) 的用户名/密码。 如果是通过其本地地址连接到模拟器 (例如，168。*.*.* ) 在同一台计算机上，将接受任何凭据。
* 布尔标准-对于普通优先级为 True，低优先级为 false。 通常，你需要将此值设置为 *true* ，以便测试方案允许你的测试进行控制。  仿真程序和 Windows Mixed Reality 模拟使用低优先级连接。  如果你的测试也使用低优先级连接，则最新建立的连接将处于控制之下。
* CancellationToken 标记-用于取消异步操作的标记。

其次，你将创建 IPerceptionSimulationManager。 这是用于控制模拟的对象。 还必须在异步方法中完成此操作。

## <a name="control-the-simulated-human"></a>控制模拟的人工

IPerceptionSimulationManager 具有返回 ISimulatedHuman 对象的人属性。 若要控制模拟人力，请对此对象执行操作。 例如：

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a>基本示例 c # 控制台应用程序

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Task.Run(async () =>
            {
                RestSimulationStreamSink sink = null;
                CancellationToken token = new System.Threading.CancellationToken();

                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }

                // Always close the sink to return control to the previous application.
                if (sink != null)
                {
                    await sink.Close(token);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();
        }
    }
}
```

## <a name="extended-sample-c-console-application"></a>扩展的示例 c # 控制台应用程序

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            RestSimulationStreamSink sink = null;
            CancellationToken token = new System.Threading.CancellationToken();

            Task.Run(async () =>
            {
                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);

                    // Now, we'll simulate a sequence of actions.
                    // Sleeps in-between each action give time to the system
                    // to be able to properly react.
                    // This is just an example. A proper automated test should verify
                    // that the app has behaved correctly
                    // before proceeding to the next step, instead of using Sleeps.

                    // Activate the right hand
                    manager.Human.RightHand.Activated = true;

                    // Simulate Bloom gesture, which should cause Shell to disappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... this time, Shell should reappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate a Head rotation down around the X axis
                    // This should cause gaze to aim about the center of the screen
                    manager.Human.Head.Rotate(new Rotation3(0.04f, 0.0f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a finger press & release
                    // Should cause a tap on the center tile, thus launching it
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate a second finger press & release
                    // Should activate the app that was launched when the center tile was clicked
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(5000);

                    // Simulate a Head rotation towards the upper right corner
                    manager.Human.Head.Rotate(new Rotation3(-0.14f, 0.17f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a third finger press & release
                    // Should press the Remove button on the app
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... bringing the Shell back once more
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();

            // Always close the sink to return control to the previous application.
            if (sink != null)
            {
                sink.Close(token);
            }
        }
    }
}
```

## <a name="note-on-6-dof-controllers"></a>DOF 控制器上的注意事项

在模拟 DOF 控制器上调用方法的任何属性之前，必须激活控制器。  如果不这样做，将导致异常。  从 Windows 10 可能2019更新开始，可以通过将 ISimulatedSixDofController 对象的 Status 属性设置为 SimulatedSixDofControllerStatus，来安装和激活模拟的 DOF 控制器。
在 Windows 10 2018 10 月版更新及更早版本中，必须先通过调用 \Windows\System32 文件夹中的 PerceptionSimulationDevice 工具单独安装模拟的 DOF 控制器。  此工具的用法如下所示：


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

例如

```
    PerceptionSimulationDevice.exe i 6dof 1
```

支持的操作包括：
* i = 安装
* q = 查询
* r = 删除

支持的实例包括：
* 1 = 左 6-DOF 控制器
* 2 = 右 6-DOF 控制器

该进程的退出代码将指示成功 (零返回值) 或 (非零返回值) 。  当使用 "q" 操作来查询控制器是否已安装时，如果未安装控制器，则返回值将为零 (0) 如果控制器已安装，则返回 (1) 。

在 Windows 10 2018 10 月更新版或更早版本上删除控制器时，请先通过 API 将其状态设置为 Off，然后调用 PerceptionSimulationDevice 工具。

必须以管理员身份运行此工具。




## <a name="api-reference"></a>API 参考

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a>PerceptionSimulation. SimulatedDeviceType

描述模拟设备类型

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

**PerceptionSimulation. SimulatedDeviceType. 引用**

虚构引用设备，PerceptionSimulationManager 的默认值

### <a name="microsoftperceptionsimulationheadtrackermode"></a>PerceptionSimulation. HeadTrackerMode

描述 head 跟踪器模式

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

**PerceptionSimulation. HeadTrackerMode**

默认标题跟踪。 这意味着系统可能会根据运行时条件选择最佳的标题跟踪模式。

**PerceptionSimulation. HeadTrackerMode**

仅定向到头跟踪。 这意味着跟踪的位置可能不可靠，并且某些依赖于头位置的功能可能不可用。

**PerceptionSimulation. HeadTrackerMode. 位置**

位置标题跟踪。 这意味着跟踪的头位置和方向都是可靠的

### <a name="microsoftperceptionsimulationsimulatedgesture"></a>PerceptionSimulation. SimulatedGesture

描述模拟手势

```
public enum SimulatedGesture
{
    None = 0,
    FingerPressed = 1,
    FingerReleased = 2,
    Home = 4,
    Max = Home
}
```

**PerceptionSimulation. SimulatedGesture**

用于指示没有笔势的 sentinel 值。

**PerceptionSimulation. SimulatedGesture. FingerPressed**

手指按下的手势。

**PerceptionSimulation. SimulatedGesture. FingerReleased**

用手指释放的手势。

**PerceptionSimulation. SimulatedGesture**

Home/system 手势。

**PerceptionSimulation. SimulatedGesture. Max**

最大有效手势。

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a>PerceptionSimulation. SimulatedSixDofControllerStatus

模拟 6 DOF 控制器的可能状态。

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

**PerceptionSimulation. SimulatedSixDofControllerStatus。**

6-DOF 控制器已关闭。

**PerceptionSimulation. SimulatedSixDofControllerStatus。**

6-DOF 控制器已打开并进行跟踪。

**PerceptionSimulation. SimulatedSixDofControllerStatus. TrackingLost**

6-DOF 控制器已打开，但无法跟踪。

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a>PerceptionSimulation. SimulatedSixDofControllerButton

模拟 6 DOF 控制器上支持的按钮。

```
public enum SimulatedSixDofControllerButton
{
    None = 0,
    Home = 1,
    Menu = 2,
    Grip = 4,
    TouchpadPress = 8,
    Select = 16,
    TouchpadTouch = 32,
    Thumbstick = 64,
    Max = Thumbstick
}
```

**PerceptionSimulation. SimulatedSixDofControllerButton**

用于指示没有按钮的 sentinel 值。

**PerceptionSimulation. SimulatedSixDofControllerButton**

"主页" 按钮处于按下状态。

**PerceptionSimulation. SimulatedSixDofControllerButton**

按下菜单按钮。

**PerceptionSimulation. SimulatedSixDofControllerButton**

按下 "手柄" 按钮。

**PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadPress**

触摸板已按下。

**PerceptionSimulation. SimulatedSixDofControllerButton. Select**

按 "选择" 按钮。

**PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadTouch**

触摸板接触。

**PerceptionSimulation. SimulatedSixDofControllerButton**

已按下操纵杆。

**PerceptionSimulation. SimulatedSixDofControllerButton. Max**

"最大有效" 按钮。


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a>PerceptionSimulation. SimulatedEyesCalibrationState

模拟眼睛的校准状态

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

**PerceptionSimulation. SimulatedEyesCalibrationState. 不可用**

眼睛校准不可用。

**PerceptionSimulation. SimulatedEyesCalibrationState。**

眼睛已经校准。  这是默认值。

**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**

正在校准眼睛。

**PerceptionSimulation. SimulatedEyesCalibrationState. UserCalibrationNeeded**

需要校准眼睛。

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a>PerceptionSimulation. SimulatedHandJointTrackingAccuracy

手的接点的跟踪准确性。

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

**PerceptionSimulation. SimulatedHandJointTrackingAccuracy. 不可用**

不会跟踪接头。

**PerceptionSimulation. SimulatedHandJointTrackingAccuracy**

将推断联合位置。

**PerceptionSimulation. SimulatedHandJointTrackingAccuracy。**

将完全跟踪联合。

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a>PerceptionSimulation. SimulatedHandPose

手的接点的跟踪准确性。

```
public enum SimulatedHandPose
{
    Closed = 0,
    Open = 1,
    Point = 2,
    Pinch = 3,
    Max = Pinch
}
```

**PerceptionSimulation. SimulatedHandPose. 关闭**

手的 finger 接头被配置为反映闭合的姿势。

**PerceptionSimulation. SimulatedHandPose。**

触接头的配置以反映开放姿势。

**PerceptionSimulation. SimulatedHandPose. 点**

触接头的配置以反映一个指示。

**PerceptionSimulation. SimulatedHandPose**

触接头的配置以反映收缩的姿势。

**PerceptionSimulation. SimulatedHandPose. Max**

SimulatedHandPose 的最大有效值。


### <a name="microsoftperceptionsimulationplaybackstate"></a>PerceptionSimulation. PlaybackState

描述播放的状态。

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

**PerceptionSimulation. PlaybackState. 已停止**

录制当前已停止，可供播放。

**PerceptionSimulation. PlaybackState**

当前正在播放记录。

**PerceptionSimulation. PlaybackState. 暂停**

当前已暂停录制。

**PerceptionSimulation. PlaybackState. 结束**

记录已结束。

### <a name="microsoftperceptionsimulationvector3"></a>PerceptionSimulation. System.numerics.vector2

介绍三个组件向量，它可能在三维空间中描述点或向量。

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

**PerceptionSimulation. System.numerics.vector2. X**

向量的 X 分量。

**PerceptionSimulation. System.numerics.vector2**

向量的 Y 分量。

**PerceptionSimulation. System.numerics.vector2. Z**

向量的 Z 分量。

**PerceptionSimulation (系统) 的 #ctor： single、system.object**

构造一个新的 System.numerics.vector2。

参数
* x-向量的 x 分量。
* y-向量的 y 分量。
* z-矢量的 z 分量。

### <a name="microsoftperceptionsimulationrotation3"></a>PerceptionSimulation. Rotation3

介绍三个组件旋转。

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

**PerceptionSimulation. Rotation3**

旋转的螺距分量，围绕 X 轴向下旋转。

**PerceptionSimulation. Rotation3. 偏航**

旋转的偏航组件，绕 Y 轴旋转。

**PerceptionSimulation. Rotation3**

围绕 Z 轴旋转的滚动部分。

**PerceptionSimulation (系统) 的 #ctor： single、system.object**

构造一个新的 Rotation3。

参数
* 螺距-旋转的螺距部分。
* 偏航-旋转的偏航组件。
* 滚动-旋转的滚动组件。

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a>PerceptionSimulation. SimulatedHandJointConfiguration

描述模拟手上的接点配置。

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

**PerceptionSimulation. SimulatedHandJointConfiguration. 位置**

接点的位置。

**PerceptionSimulation. SimulatedHandJointConfiguration**

接点的旋转。

**PerceptionSimulation. SimulatedHandJointConfiguration. TrackingAccuracy**

联合的跟踪准确性。


### <a name="microsoftperceptionsimulationfrustum"></a>PerceptionSimulation

描述通常由相机使用的视图（如）。

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

**PerceptionSimulation。**

在锥上包含的最小距离。

**PerceptionSimulation. Far**

在锥中包含的最大距离。

**PerceptionSimulation. FieldOfView**

以弧度表示的（以弧度表示）的水平字段 (小于 PI) 。

**PerceptionSimulation. AspectRatio**

视图的水平字段与视图的垂直字段的比率。

### <a name="microsoftperceptionsimulationsimulateddisplayconfiguration"></a>PerceptionSimulation. SimulatedDisplayConfiguration

描述模拟耳机显示的配置。

```
public struct SimulatedDisplayConfiguration
{
    public Vector3 LeftEyePosition;
    public Rotation3 LeftEyeRotation;
    public Vector3 RightEyePosition;
    public Rotation3 RightEyeRotation;
    public float Ipd;
    public bool ApplyEyeTransforms;
    public bool ApplyIpd;
}
```

**PerceptionSimulation. SimulatedDisplayConfiguration. LeftEyePosition**

从头部中心到左边的转换是为了实现立体声渲染。

**PerceptionSimulation. SimulatedDisplayConfiguration. LeftEyeRotation**

用于立体声呈现的左侧方式的旋转。

**PerceptionSimulation. SimulatedDisplayConfiguration. RightEyePosition**

从头部中心到正确眼睛的转换是为了实现立体声渲染。

**PerceptionSimulation. SimulatedDisplayConfiguration. RightEyeRotation**

为了实现立体声渲染，正确的眼睛旋转。

**PerceptionSimulation. SimulatedDisplayConfiguration**

系统报告的 Ipd 值用于立体声渲染。

**PerceptionSimulation. SimulatedDisplayConfiguration. ApplyEyeTransforms**

为左和右眼转换提供的值是否应视为有效且应用于正在运行的系统。

**PerceptionSimulation. SimulatedDisplayConfiguration. ApplyIpd**

为 Ipd 提供的值是否应视为有效，并将其应用于正在运行的系统。


### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a>PerceptionSimulation. IPerceptionSimulationManager

用于生成用于控制设备的数据包的根。

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

**PerceptionSimulation. IPerceptionSimulationManager. 设备**

检索用于解释模拟人类和模拟世界的模拟设备对象。

**PerceptionSimulation. IPerceptionSimulationManager**

检索控制模拟人的对象。

**PerceptionSimulation. IPerceptionSimulationManager**

将模拟重置为其默认状态。

### <a name="microsoftperceptionsimulationisimulateddevice"></a>PerceptionSimulation. ISimulatedDevice

描述设备的接口，该设备解释模拟世界和模拟人类

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

**PerceptionSimulation. ISimulatedDevice. HeadTracker**

从模拟设备检索 Head 跟踪器。

**PerceptionSimulation. ISimulatedDevice. HandTracker**

从模拟设备检索手动跟踪器。

**PerceptionSimulation. ISimulatedDevice. SetSimulatedDeviceType (PerceptionSimulation)**

设置模拟设备的属性，使其与所提供的设备类型相匹配。

参数
* 类型-新类型的模拟设备

### <a name="microsoftperceptionsimulationisimulateddevice2"></a>PerceptionSimulation. ISimulatedDevice2

可以通过将 ISimulatedDevice 转换为 ISimulatedDevice2 提供其他属性

```
public interface ISimulatedDevice2
{
    bool IsUserPresent { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    SimulatedDisplayConfiguration DisplayConfiguration { get; set; }

};
```

**PerceptionSimulation. ISimulatedDevice2. IsUserPresent**

检索或设置模拟人力是否正在积极地戴上耳机。

**PerceptionSimulation. ISimulatedDevice2. DisplayConfiguration**

检索或设置模拟的显示的属性。

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a>PerceptionSimulation. ISimulatedHeadTracker

描述模拟设备的部分的接口，该部分跟踪模拟人的头。

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

**PerceptionSimulation. ISimulatedHeadTracker. HeadTrackerMode**

检索和设置当前 head 跟踪器模式。

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a>PerceptionSimulation. ISimulatedHandTracker

描述模拟设备的部分的接口，该部分跟踪模拟人的手

```
public interface ISimulatedHandTracker
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    float Pitch { get; set; }
    bool FrustumIgnored { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    Frustum Frustum { get; set; }
}
```

**PerceptionSimulation. ISimulatedHandTracker. WorldPosition**

检索与世界相关的节点的位置（以米为单位）。

**PerceptionSimulation. ISimulatedHandTracker. 位置**

检索和设置模拟手型跟踪器的位置（相对于打印头的中心）。

**PerceptionSimulation. ISimulatedHandTracker**

检索和设置模拟手型跟踪器的下间距。

**PerceptionSimulation. ISimulatedHandTracker. FrustumIgnored**

检索和设置是否忽略模拟手动跟踪器的 "截锥"。 如果忽略，则这两个指针始终可见。 当未被忽略时 (默认) 只是在 "手形跟踪器" 中的

**PerceptionSimulation. ISimulatedHandTracker**

检索和设置用来确定是否对模拟手型跟踪器可见的被截锥属性。

### <a name="microsoftperceptionsimulationisimulatedhuman"></a>PerceptionSimulation. ISimulatedHuman

用于控制模拟人的顶级接口。

```
public interface ISimulatedHuman 
{
    Vector3 WorldPosition { get; set; }
    float Direction { get; set; }
    float Height { get; set; }
    ISimulatedHand LeftHand { get; }
    ISimulatedHand RightHand { get; }
    ISimulatedHead Head { get; }s
    void Move(Vector3 translation);
    void Rotate(float radians);
}
```

**PerceptionSimulation. ISimulatedHuman. WorldPosition**

检索和设置与世界相关的节点的位置（以米为单位）。 此位置对应于人脚的中心点。

**PerceptionSimulation. ISimulatedHuman。**

检索和设置模拟人脸在世界中的方向。 0弧度朝下 Z 轴向下。 正弧度围绕 Y 轴顺时针旋转。

**PerceptionSimulation. ISimulatedHuman**

检索和设置模拟人的高度（以米为单位）。

**PerceptionSimulation. ISimulatedHuman. LeftHand**

检索模拟人的左侧。

**PerceptionSimulation. ISimulatedHuman. RightHand**

检索模拟人的右边。

**PerceptionSimulation. ISimulatedHuman**

检索模拟人的 head。

**PerceptionSimulation (System.numerics.vector2) （ISimulatedHuman）**

以米为单位移动模拟人工相对于其当前位置的位置。

参数
* 平移-要移动的转换，相对于当前位置。

**PerceptionSimulation () 中的 ISimulatedHuman**

围绕 Y 轴顺时针旋转模拟人工相对于其当前方向

参数
* radians-绕 Y 轴旋转的量。

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a>PerceptionSimulation. ISimulatedHuman2

可以通过将 ISimulatedHuman 转换为 ISimulatedHuman2 提供其他属性

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

**PerceptionSimulation. ISimulatedHuman2. LeftController**

检索左 6-DOF 控制器。

**PerceptionSimulation. ISimulatedHuman2. RightController**

检索正确的 DOF 控制器。


### <a name="microsoftperceptionsimulationisimulatedhand"></a>PerceptionSimulation. ISimulatedHand

描述模拟人类

```
public interface ISimulatedHand
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    bool Activated { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    bool Visible { [return: MarshalAs(UnmanagedType.Bool)] get; }
    void EnsureVisible();
    void Move(Vector3 translation);
    void PerformGesture(SimulatedGesture gesture);
}
```

**PerceptionSimulation. ISimulatedHand. WorldPosition**

检索与世界相关的节点的位置（以米为单位）。

**PerceptionSimulation. ISimulatedHand. 位置**

检索和设置模拟手型相对于人类的位置（以米为单位）。

**PerceptionSimulation. ISimulatedHand. 已激活**

检索和设置当前是否已激活该手型。

**PerceptionSimulation. ISimulatedHand。**

检索当前是否对 SimulatedDevice (可见，即，该手形是否位于 HandTracker) 检测到的位置。

**PerceptionSimulation. ISimulatedHand. Ensurevisible\**

移动手使其对 SimulatedDevice 可见。

**PerceptionSimulation (System.numerics.vector2) （ISimulatedHand）**

以米为单位移动模拟手型相对于其当前位置的位置。

参数
* 翻译-模拟手的平移量。

**PerceptionSimulation. ISimulatedHand. PerformGesture (PerceptionSimulation)**

使用模拟手执行手势。  只有在启用了该功能的情况，系统才会检测到它。

参数
* 手势-要执行的手势。

### <a name="microsoftperceptionsimulationisimulatedhand2"></a>PerceptionSimulation. ISimulatedHand2

可以通过将 ISimulatedHand 转换为 ISimulatedHand2 来获取其他属性。
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

**PerceptionSimulation. ISimulatedHand2**

检索或设置模拟手的旋转。  正弧度沿轴旋转时顺时针旋转。

### <a name="microsoftperceptionsimulationisimulatedhand3"></a>PerceptionSimulation. ISimulatedHand3

可以通过将 ISimulatedHand 转换为 ISimulatedHand3 提供其他属性
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

**PerceptionSimulation. ISimulatedHand3. GetJointConfiguration**

获取指定的联合的联合配置。

**PerceptionSimulation. ISimulatedHand3. SetJointConfiguration**

设置指定的联合的联合配置。

**PerceptionSimulation. ISimulatedHand3. SetHandPose**

使用可选的动画标志将手设置为已知姿势。  注意：动画效果不会立即反映其最终的联合配置。


### <a name="microsoftperceptionsimulationisimulatedhead"></a>PerceptionSimulation. ISimulatedHead

描述模拟人的头的接口。

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

**PerceptionSimulation. ISimulatedHead. WorldPosition**

检索与世界相关的节点的位置（以米为单位）。

**PerceptionSimulation. ISimulatedHead**

检索模拟头部的旋转。 正弧度沿轴旋转时顺时针旋转。

**PerceptionSimulation. ISimulatedHead**

检索模拟头直径。 此值用于确定 head 中心 (旋转点) 。

**PerceptionSimulation (Rotation3) （ISimulatedHead）**

相对于当前旋转旋转模拟头。 正弧度沿轴旋转时顺时针旋转。

参数
* 旋转-要旋转的量。

### <a name="microsoftperceptionsimulationisimulatedhead2"></a>PerceptionSimulation. ISimulatedHead2

可以通过将 ISimulatedHead 转换为 ISimulatedHead2 提供其他属性

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

**PerceptionSimulation. ISimulatedHead2**

检索模拟人的眼睛。

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a>PerceptionSimulation. ISimulatedSixDofController

描述与模拟人类关联的 6 DOF 控制器的接口。

```
public interface ISimulatedSixDofController
{
    Vector3 WorldPosition { get; }
    SimulatedSixDofControllerStatus Status { get; set; }
    Vector3 Position { get; }
    Rotation3 Orientation { get; set; }
    void Move(Vector3 translation);
    void PressButton(SimulatedSixDofControllerButton button);
    void ReleaseButton(SimulatedSixDofControllerButton button);
    void GetTouchpadPosition(out float x, out float y);
    void SetTouchpadPosition(float x, float y);
}
```

**PerceptionSimulation. ISimulatedSixDofController. WorldPosition**

检索与世界相关的节点的位置（以米为单位）。

**PerceptionSimulation. ISimulatedSixDofController**

检索或设置控制器的当前状态。  在移动、旋转或按下按钮的任何调用都将成功之前，控制器状态必须设置为 Off 以外的值。

**PerceptionSimulation. ISimulatedSixDofController. 位置**

检索或设置模拟控制器相对于人类的位置（以米为单位）。

**PerceptionSimulation. ISimulatedSixDofController**

检索或设置模拟控制器的方向。

**PerceptionSimulation (System.numerics.vector2) （ISimulatedSixDofController）**

移动模拟控制器相对于其当前位置的位置（以米为单位）。

参数
* 翻译-模拟控制器的平移量。

**PerceptionSimulation. ISimulatedSixDofController. PressButton (SimulatedSixDofControllerButton)**

按模拟控制器上的按钮。  仅当控制器已启用时，系统才会检测到该控制器。

参数
* 按钮-要按下的按钮。

**PerceptionSimulation. ISimulatedSixDofController. ReleaseButton (SimulatedSixDofControllerButton)**

释放模拟控制器上的按钮。  仅当控制器已启用时，系统才会检测到该控制器。

参数
* 按钮-要释放的按钮。

**PerceptionSimulation. ISimulatedSixDofController. GetTouchpadPosition (out、out float)**

获取模拟手指在模拟控制器的触摸板上的位置。

参数
* x-手指的水平位置。
* y-手指的垂直位置。

**SetTouchpadPosition (float，float)**

设置模拟手指在模拟控制器的触摸板上的位置。

参数
* x-手指的水平位置。
* y-手指的垂直位置。

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a>PerceptionSimulation. ISimulatedSixDofController2

可以通过将 ISimulatedSixDofController 转换为 ISimulatedSixDofController2 来提供其他属性和方法。

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

**PerceptionSimulation. ISimulatedSixDofController2. GetThumbstickPosition (out、out float)**

获取模拟操纵杆在模拟控制器上的位置。

参数
* x-操纵杆的水平位置。
* y-操纵杆的垂直位置。

**SetThumbstickPosition (float，float)**

设置模拟操纵杆在模拟控制器上的位置。

参数
* x-操纵杆的水平位置。
* y-操纵杆的垂直位置。

**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**

检索或设置模拟控制器的电池电量级别。  该值必须大于0.0 且小于或等于100.0。


### <a name="microsoftperceptionsimulationisimulatedeyes"></a>PerceptionSimulation. ISimulatedEyes

描述模拟人力的眼睛的接口。

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

**PerceptionSimulation. ISimulatedEyes**

检索模拟眼睛的旋转。 正弧度沿轴旋转时顺时针旋转。

**PerceptionSimulation (Rotation3) （ISimulatedEyes）**

相对于当前旋转旋转模拟眼睛。 正弧度沿轴旋转时顺时针旋转。

参数
* 旋转-要旋转的量。

**PerceptionSimulation. ISimulatedEyes. CalibrationState**

检索或设置模拟眼睛的校准状态。

**PerceptionSimulation. ISimulatedEyes. WorldPosition**

检索与世界相关的节点的位置（以米为单位）。


### <a name="microsoftperceptionsimulationisimulationrecording"></a>PerceptionSimulation. ISimulationRecording

用于与为播放加载的单个录制交互的接口。

```
public interface ISimulationRecording
{
    StreamDataTypes DataTypes { get; }
    PlaybackState State { get; }
    void Play();
    void Pause();
    void Seek(UInt64 ticks);
    void Stop();
};
```

**PerceptionSimulation. ISimulationRecording**

检索记录中数据类型的列表。

**PerceptionSimulation. ISimulationRecording**

检索当前记录的状态。

**PerceptionSimulation. ISimulationRecording**

开始播放。 如果记录已暂停，播放将从暂停位置恢复;如果停止，则将从开始处开始播放。 如果已播放，则忽略此调用。

**PerceptionSimulation. ISimulationRecording. 暂停**

暂停播放当前位置。 如果记录已停止，则调用将被忽略。

**PerceptionSimulation () 中的 ISimulationRecording**

将记录查找到指定时间 (以 100-纳秒为间隔，从开始) 到该位置暂停。 如果该时间超出了记录的结束时间，则会在最后一帧暂停该时间。

参数
* 计时周期-要查找的时间。

**PerceptionSimulation. ISimulationRecording. Stop**

停止播放并将位置重置为开始位置。

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a>PerceptionSimulation. ISimulationRecordingCallback

用于在播放期间接收状态更改的接口。

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

**PerceptionSimulation. ISimulationRecordingCallback. PlaybackStateChanged (PerceptionSimulation)**

当 ISimulationRecording 的播放状态发生更改时调用。

参数
* newState-记录的新状态。

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a>PerceptionSimulation. PerceptionSimulationManager

用于创建感知模拟对象的根对象。

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

**PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationManager (PerceptionSimulation)**

针对生成模拟包并将其传送到所提供接收器的对象创建。

参数
* sink-接收所有生成的数据包的接收器。

返回值

创建的管理器。

**PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationRecording ()**

创建接收器，将所有接收的数据包存储在文件中的指定路径。

参数
* path-要创建的文件的路径。

返回值

创建的接收器。

**PerceptionSimulation) LoadPerceptionSimulationRecording (PerceptionSimulation.. ISimulationStreamSinkFactory**

从指定的文件加载记录。

参数
* path-要加载的文件的路径。
* 工厂-记录用于在需要时创建 ISimulationStreamSink 的工厂。

返回值

加载的记录。

**LoadPerceptionSimulationRecording (PerceptionSimulation，PerceptionSimulation) ISimulationStreamSinkFactory，PerceptionSimulation，ISimulationRecordingCallback。的**

从指定的文件加载记录。

参数
* path-要加载的文件的路径。
* 工厂-记录用于在需要时创建 ISimulationStreamSink 的工厂。
* callback-回调，用于接收 regrading 记录状态的更新。

返回值

加载的记录。

### <a name="microsoftperceptionsimulationstreamdatatypes"></a>PerceptionSimulation. StreamDataTypes

描述不同类型的流数据。

```
public enum StreamDataTypes
{
    None = 0x00,
    Head = 0x01,
    Hands = 0x02,
    SpatialMapping = 0x08,
    Calibration = 0x10,
    Environment = 0x20,
    SixDofControllers = 0x40,
    Eyes = 0x80,
    DisplayConfiguration = 0x100
    All = None | Head | Hands | SpatialMapping | Calibration | Environment | SixDofControllers | Eyes | DisplayConfiguration
}
```

**PerceptionSimulation. StreamDataTypes**

用于指示没有流数据类型的 sentinel 值。

**PerceptionSimulation. StreamDataTypes**

数据流的位置和方向。

**PerceptionSimulation. StreamDataTypes**

用于指针位置和手势的数据流。

**PerceptionSimulation. StreamDataTypes. SpatialMapping**

环境的空间映射的数据流。

**PerceptionSimulation. StreamDataTypes**

用于校准设备的数据流。 只有远程模式下的系统才会接受校准数据包。

**PerceptionSimulation. StreamDataTypes**

设备环境的数据流。

**PerceptionSimulation. StreamDataTypes. SixDofControllers**

运动控制器的数据流。

**PerceptionSimulation. StreamDataTypes**

具有模拟人力的眼睛的数据流。

**PerceptionSimulation. StreamDataTypes. DisplayConfiguration**

具有设备显示配置的数据流。

**PerceptionSimulation. StreamDataTypes。**

用于指示所有记录的数据类型的 sentinel 值。

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a>PerceptionSimulation. ISimulationStreamSink

从模拟流接收数据包的对象。

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

**OnPacketReceived (uint length，byte [] packet)**

接收单个数据包，该数据包在内部键入并进行版本控制。

参数
* length-数据包的长度。
* 数据包-包的数据。

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a>PerceptionSimulation. ISimulationStreamSinkFactory

用于创建 ISimulationStreamSink 的对象。

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

**PerceptionSimulation. ISimulationStreamSinkFactory. CreateSimulationStreamSink ( # B1**

创建 ISimulationStreamSink 的单个实例。

返回值

创建的接收器。
