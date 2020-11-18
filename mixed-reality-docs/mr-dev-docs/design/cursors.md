---
title: 游标
description: 对于目标向量，光标或指示器可为用户提供持续的反馈，以了解 HoloLens 对其意图的了解情况。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens (第一代) ，HoloLens 2，Mixed Reality，光标，目标，注视，手势，混合现实耳机，windows Mixed Reality 耳机，虚拟现实耳机，HoloLens，MRTK，混合现实工具包，射线，输入
ms.openlocfilehash: db895c7aad177d7ddd2eb371392812b1d7e4d039
ms.sourcegitcommit: 4f3ef057a285be2e260615e5d6c41f00d15d08f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94702643"
---
# <a name="cursors"></a>游标

![游标](images/UX_Hero_Cursor.jpg)

当前目标向量的光标或指示器可为用户提供持续的反馈，以了解头戴显示在该时间的位置。 光标允许用户了解其当前目标点，并作为反馈来指示哪个区域、全息图或点将响应输入。 它是设备理解用户关注 (的数字表示形式，但这可能不同于确定其意图) 的任何内容。

游标提供的反馈为用户提供预测系统响应方式的能力，使用该信号作为反馈来更好地传达设备对设备的意图，并最终更有把握其交互。

有三种类型的游标： **手指、光线** 和 **打印头**。 这些指针在 HoloLens、HoloLens 2 和沉浸式耳机上使用不同的输入情态。 下面是针对每种类型的耳机和交互模型使用哪种类型的游标的指导。 在混合现实工具包中 (MRTK) ，我们已创建了拖放游标模块，以帮助你生成正确的指针体验。


## <a name="device-support"></a>设备支持

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>功能</strong></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens（第 1 代）</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="../discover/immersive-headset-hardware-details.md"><strong>沉浸式头戴显示设备</strong></a></td>
    </tr>
     <tr>
        <td>手指光标</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
     <tr>
        <td>Ray 光标</td>
        <td>❌</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>打印头光标</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="finger-cursor"></a>手指光标
Finger 游标仅在 HoloLens 2 上可用，以增强 "[直接操作](direct-manipulation.md)" 交互模式。 为了更好地了解手指的位置，我们将环附加到了两个食指的提示。 环形大小基于手指与 UI 图面的接近度， (手指越接近，环形) 越小，当手指与 UI 联系时，它将缩小为点形状。 <br>

![手指光标](images/finger-cursor.png)<br>
**Finger cursor 1 的视觉反馈状态** ：环形收缩为点。 2：环形与图面对齐。 3：环与 finger 矢量垂直。 4：无环。

## <a name="ray-cursor"></a>Ray 光标
Ray 光标连接到最靠近的光线的末尾，以允许对不是手接触的对象进行操作。 在沉浸式耳机中，从运动控制器开始，并以点光标结束。 在 HoloLens 2 中，我们充分利用了这些运动控制器光线的心理模型，并利用了源自不要和 end 的环形光标（与直接操作中使用的 finger 光标一致）。 <br>
:::row:::
    :::column:::
        ![Ray cursor 控制器](images/ray-cursor-controller.png)<br>
        **运动控制器的光线光标**<br>
    :::column-end:::
    :::column:::
        ![Ray 光标手](images/ray-cursor-hand.png)<br>
        **免提的光线光标**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="head-gaze-cursor"></a>打印头光标
打印头光标是一个点，用于连接到使用点的位置和旋转点的不可见的端面向量。 若要执行操作，请将指针光标与各种提交输入（如分流、语音命令、停留和按钮按下）配对。 在 HoloLens 2 中，打印头最好与任何不是分流的提交输入配对，因为这会在空中分流和远手光线之间发生交互冲突。 <br>
:::row:::
    :::column:::
        ![打印头的光标手](images/head-gaze-cursor-hand.png)<br>
        **带有手动手势的打印头**<br>
    :::column-end:::
    :::column:::
        ![打印头光标声音](images/head-gaze-cursor-voice.png)<br>
        **带有声音命令的头盔光标**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="cursor-customization-recommendations"></a>游标自定义建议
如果要自定义游标反馈行为和外观，以下是一些设计建议：

### <a name="cursor-scale"></a>游标刻度
* 光标不应大于可用目标，从而使用户可以轻松地与内容交互并查看内容。
* 根据您创建的体验，在用户看起来时缩放光标也是一个重要的考虑因素。 例如，当用户看到你的体验时，游标不应太小，因此不会丢失。
* 缩放光标时，请考虑将软动画应用到它，因为它会进行缩放以使其成为一种有机感觉。
* 避免阻碍内容。 全息影像使体验更加容易，并且光标不应从它们中消失。

### <a name="directionless-cursor-shape"></a>Directionless 光标形状
* 尽管没有一个右光标形状，但建议使用 directionless 形状（如圆环图）。 在某些方向上指向 (例如，传统的箭头光标) 的游标可能会使用户感到困惑。
* 当使用游标向用户传达交互指令时，会出现这种情况的例外情况。 例如，在混合现实操作系统中缩放全息影像时，光标暂时会包括一些箭头，指导用户如何移动其手来缩放全息影像。

### <a name="look-and-feel"></a>外观
* 环形或圆环图游标适用于许多应用程序。
* 选择最能代表您正在创建的体验的颜色和形状。
* 游标特别容易出现 [颜色分离](../develop/platform-capabilities-and-apis/hologram-stability.md#color-separation)。
* 具有均衡不透明度的小游标将使其具有信息性，而无需占据视觉层次结构。
* 请 cognizant 在游标后面使用阴影或突出显示，因为它们可能会妨碍内容和对任务的注意力。
* 光标应与应用中的表面对齐并进行分配，这会使用户感觉到系统可以看到的位置，但系统也知道其周围的位置。 例如，在混合现实操作系统中，光标与用户世界的表面保持一致，即使用户没有直接在全息图上查看，也可以感觉到世界认知。
* 当光标位于接近邻近的位置时，会将光标锁定到交互式元素，从而有助于提高用户在执行选择操作时与该元素进行交互的置信度。

### <a name="visual-cues"></a>视觉提示
* 如果你的体验侧重于单个全息图，则当你看起来远离该全息图时，光标应该只与全息图和改变形状对齐。 这可以向用户传达全息影像是可操作的，并且可以与之进行交互。
* 如果你的应用程序使用空间映射，则光标可能会对齐并向其看到的每个表面显示。 这会向 HoloLens 和你的应用程序可以看到其空间的用户提供反馈。 这就是一个事实，那就是全息影像非常真实，并可帮助您弥补现实和虚拟之间的差距。
* 在视图中没有全息影像或曲面时，了解光标应执行的操作。 将其放置在用户前面预先确定的距离上是一种选择。

### <a name="possible-actions"></a>可能的操作
* 光标可由不同的图标表示，以传达全息图可以执行的可能操作，例如缩放或旋转。
* 仅在游标中添加了其他内容时，才添加其他信息。 否则，用户可能不会注意到状态发生更改，也可能会使光标混淆。

### <a name="input-state"></a>输入状态
* 可以使用光标显示用户的输入状态或意向。 例如，我们可以显示一个图标，告诉用户系统看到其手状态，并且应用程序知道他们已准备好采取措施。
* 还可以使用光标向用户显示系统通过暂时颜色改动听到的声音命令

* 可以通过不同的方式实现以下游标状态。 您可以通过对游标（如状态机）进行建模来实现这些不同的状态。 例如：
    * 空闲状态是显示默认光标的位置。
    * "就绪" 状态为 "已检测到用户" 就绪位置。
    * 交互状态是用户执行特定交互时的状态。
    * 当你传达可以在全息图上执行的可能操作时，可能的操作状态或悬停状态。

您还可以以外观方式实现这些状态，以便在检测到不同的状态时可以显示不同的图稿资产。

<br>

---


## <a name="going-cursor-free"></a>转到 "无游标"
如果浸入式是体验的关键组件，并且在通过通和手势 (指向交互时，建议不使用游标进行设计，) 不需要很高的精度。 通过向用户提供对系统的理解并帮助他们自信地将其意图传达给系统的方式，系统仍必须满足游标通常满足的需求。 这可以通过其他明显的状态更改实现。

<br>

---

## <a name="cursor-in-mrtk-mixed-reality-toolkit-for-unity"></a>MRTK 中的光标 (混合现实工具包) 适用于 Unity
默认情况下， [MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)提供与 shell 的系统游标具有相同可视状态的 Prefab ([DefaultCursor) prefab。](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Cursors) 它分配在 MRTK 的输入配置文件的“指针”下。 您可以根据自己的经验来替换/自定义此光标。 对于目视跟踪输入经验，MRTK 还提供了 EyeGazeCursor，它具有微妙的视觉对象来最大程度地减少干扰。

* [MRTK - 指针配置文件](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html#pointer-configuration)
* [MRTK - 输入系统](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)
* [MRTK - 指针](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html)


---

## <a name="see-also"></a>另请参阅
* [笔势](gaze-and-commit.md#composite-gestures)
* [头部凝视并提交](gaze-and-commit.md)
