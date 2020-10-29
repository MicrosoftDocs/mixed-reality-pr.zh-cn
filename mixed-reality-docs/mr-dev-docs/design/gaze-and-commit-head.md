---
title: 头部凝视和提交
description: 头部凝视和提交输入模型概述
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: 混合现实, 凝视, 设定凝视目标, 交互, 设计
ms.openlocfilehash: 76223dd375e76d943183bc745792e2cb9d3d0601
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91677399"
---
# <a name="head-gaze-and-commit"></a>头部凝视和提交
" [注视](gaze-and-commit.md)" 和 "提交" 输入 _模型是一_ 种特殊情况，它涉及到对象的方向为 "向前" (head 方向) ，然后使用辅助输入（例如，手势分流或语音命令 "Select"）来定位对象。 

## <a name="device-support"></a>设备支持

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>输入模型</strong></td>
        <td><a href="../hololens-hardware-details.md"><strong>HoloLens（第 1 代）</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="../discover/immersive-headset-hardware-details.md"><strong>沉浸式头戴显示设备</strong></a></td>
    </tr>
     <tr>
        <td>头部凝视和提交</td>
        <td>✔️ 推荐</td>
        <td>✔️推荐（第三个选择 - <a href="interaction-fundamentals.md">查看其他选项</a>）</td>
        <td>➕ 备用选项</td>
    </tr>
</table>

---

## <a name="target-sizing-and-feedback"></a>目标大小调整和反馈
一直看着打印头向量，使其可用于精细定位，但通常最适用于毛目标-获取稍大的目标。 在大多数情况下，最小目标大小为1到1.5 度允许成功的用户操作，尽管目标为3度，但通常可以提高速度。 请注意，即使对于 3D 元素，用户设定为目标的尺寸实际上也是 2D 区域，3D 元素的投影即是可设定为目标的区域。 提供一些突出的提示，指出某个元素处于 "活动" 状态， (用户为该元素设定目标) 特别有用。 这可能包括处理方式（如可见的 "悬停" 效果、音频突出显示或单击），或通过元素清晰显示光标。

![2 米远处的最佳目标大小](images/gazetargeting-size-1000px.jpg)<br>
*2 米远处的最佳目标大小*

<br>

![突出显示凝视目标对象的示例](images/gazetargeting-highlighting-940px.jpg)<br>
*突出显示凝视目标对象的示例*

## <a name="target-placement"></a>目标位置
用户经常找不到在其视图字段中定位很高或极低的 UI 元素，这就是他们对其主要关注点的关注点（大约在眼睛上）。 将大多数目标放在视平线位置附近的某个合理范围内可能有所帮助。 考虑到用户在任何时候都倾向于关注一个相对较小的可视区域（注意力视锥大约为 10 度），通过将 UI 元素分组到在概念上相关的位置，可以在用户的视线通过某个区域时利用各项目之间的注意力链锁作用。 在设计 UI 时，请注意 HoloLens 和沉浸式头戴显示设备之间视野的巨大差异。

![在 Galaxy Explorer 中使用分组 UI 元素简化凝视目标设定的示例](images/gazetargeting-grouping-1000px.jpg)<br>
*在 Galaxy Explorer 中使用分组 UI 元素简化凝视目标设定的示例*

## <a name="improving-targeting-behaviors"></a>改进目标设定行为
如果可将用户意向定位到 (或大致接近) ，则在交互时接受接近的未命中尝试，就像它们的目标是正确的一样。 下面是一些可在混合现实体验中结合使用的成功方法：

### <a name="head-gaze-stabilization-gravity-wells"></a>头部凝视防抖动（“重力井”）
这应该是最多或全部开启。 此方法可删除用户在查找和讲话行为上可能具有的移动的自然头和抖动。

### <a name="closest-link-algorithms"></a>最邻近链接算法
这些方法在交互内容稀少的区域效果最好。 如果很有可能确定用户尝试与之交互的概率很高，则可以通过假定某些级别来补充其目标功能。

### <a name="backdating-and-postdating-actions"></a>Backdating 和 postdating 操作
此机制非常适合需要快速完成的任务。 当用户通过一系列的目标和激活设法使其来实现速度提高时，采用某种目的是非常有用的，并允许缺少 50 (的步骤处理用户在) 之前或之后稍微突出的目标，而不是在早期测试生效之前/之后发生。

### <a name="smoothing"></a>平滑处理
此机制对于路径移动非常有用，因为自然移动特征会降低轻微的抖动和 wobble。 对路径运动进行平滑处理时，按移动的大小和距离而不是一段时间来平滑。

### <a name="magnetism"></a>磁吸
此机制可被视为最近的链接算法的更通用版本，即根据目标绘制游标，或者只是直观或不增加 hitboxes，因为用户通过使用一些交互式布局了解来更好地利用用户意图来实现目标。 这对于小型目标尤其有用。

### <a name="focus-stickiness"></a>焦点粘性
在确定要将焦点放到哪些附近的交互式元素时，焦点将为当前聚焦的元素提供偏移。 当在两个元素之间的中间点处浮动时，这有助于减少不稳定的焦点切换行为。


## <a name="see-also"></a>请参阅
* [基于眼睛的交互](eye-gaze-interaction.md)
* [凝视和停留](gaze-and-dwell.md)
* [手 - 直接操作](direct-manipulation.md)
* [手 - 手势](gaze-and-commit.md#composite-gestures)
* [手 - 指向并提交](point-and-commit.md)
* [本能交互](interaction-fundamentals.md)
* [语音输入](voice-input.md)



