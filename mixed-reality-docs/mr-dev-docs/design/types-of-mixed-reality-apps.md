---
title: 混合现实应用的类型
description: 开发 Windows Mixed Reality 应用的优势之一在于，平台可以从完全沉浸的虚拟环境中支持的一系列经验，通过用户的当前 environmentl 进行分层分层。
author: rwinj
ms.author: willyang
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality，设计，应用模式，混合现实耳机，windows Mixed Reality 耳机，虚拟现实耳机，HoloLens
ms.openlocfilehash: 17ae6b2ec8d9c67d2b6f0114535fc25c1cb487b2
ms.sourcegitcommit: 4f3ef057a285be2e260615e5d6c41f00d15d08f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94703213"
---
# <a name="types-of-mixed-reality-apps"></a>混合现实应用的类型

为 Windows Mixed Reality 开发应用程序的一个优点是，该平台可以支持多种体验。 从完全沉浸式的虚拟环境到用户当前环境中的光线信息分层，Windows Mixed Reality 提供了一组强大的工具，可将任何体验引入到生活中。 对于应用程序制造商来说，在开发过程的早期了解其体验的位置，这一点非常重要。 此决定最终会影响应用设计的构成和开发的技术路径。

## <a name="enhanced-environment-apps-hololens-only"></a>增强的环境应用 (仅 HoloLens) 

混合现实可为用户带来价值的最强大的方式之一是，方便在用户的当前环境中放置数字信息或内容。 这是一个增强的环境应用。 此方法对于以下情况很常见：真实环境中数字内容的上下文放置非常重要，并且/或在其体验过程中使用户的实际环境 "存在" 成为关键。 这种方法还可让用户轻松地从实际任务移动到数字任务并轻松地进行操作，借此获得更多的信任，以保证用户看到的混合现实应用真正成为其环境的一部分。

![增强的环境应用](images/enhancedenvironmentapps-640px.jpg)<br>
*增强的环境应用*

**示例使用**
* 混合现实记事本样式应用，允许用户创建笔记并将其放置在其环境中
* 将混合现实电视应用置于舒适的位置以供观看
* 放置在厨房岛之上的混合现实烹饪应用，可帮助你进行烹饪任务
* 一种混合现实应用，为用户提供 "x 光愿景 (" 的感觉，这就是一个 holographically，它放在上并模拟真实世界对象，同时允许用户查看) 
* 混合现实批注放置在工厂中，用于为辅助角色指定必要的信息
* 办公空间中混合现实 wayfinding
* 混合现实 tabletop 体验 (即板游戏样式体验) 
* 混合现实通信应用，如 Skype

## <a name="blended-environment-apps"></a>混合环境应用

由于 Windows Mixed Reality 能够识别和映射用户的环境，因此它能够创建可完全叠加在用户空间上的数字层。 精简层会考虑用户环境的形状和边界，但是应用程序可能会选择转换最适合从而深入了解应用程序中用户的某些元素。 这称为混合环境应用。 与增强的环境应用不同，混合环境应用程序可能只关心环境，以最好地使用其构成来鼓励特定的用户行为 (例如鼓励移动或浏览) ，或通过将元素替换为厨房， (厨房计数器几乎 skinned 显示不同的平铺) 模式。 这种类型的体验甚至可能会将元素转换为完全不同的对象，但仍会将对象的大致尺寸保留为其基本 (厨房岛会转换为犯罪 thriller 游戏) 的转储程序。

![混合环境应用](images/blendedenvironmentapps-640px.jpg)<br>
*混合环境应用*

**示例使用**
* 混合现实内部设计应用，可使用不同的颜色和模式绘制墙壁、countertops 或地面
* 一种混合现实应用，允许汽车设计器将新的设计迭代置于现有汽车顶层的即将到来的汽车刷新之上
* 床已 "覆盖"，由儿童游戏中的混合现实水果支架替换
* 在犯罪 thriller 游戏中，桌面被 "覆盖" 并替换为混合现实转储程序
* 使用大致相同的形状和尺寸 "覆盖" 了悬挂灯笼并将其替换为 signpost
* 一种应用，它允许用户在其真实或沉浸式世界中冲击孔洞，这会显示神奇世界

## <a name="immersive-environment-apps"></a>沉浸式环境应用

沉浸式环境应用以完全更改用户世界的环境为中心，并可将其置于不同的时间和空间。 这些环境看起来非常真实，只是在应用程序创建者的想象中仅限制了 thrilling 体验。 与混合环境应用不同，一旦 Windows Mixed Reality 标识用户的空间，沉浸式环境应用可能会完全忽略用户的当前环境，并将其替换为自己的整个股票。 这些体验还可能会完全分离时间和空间，这意味着用户可以通过沉浸式体验来浏览罗马的 实际环境的上下文对于沉浸式环境应用可能并不重要。

![沉浸式环境应用](images/windows-mixed-reality-640px.jpg)<br>
*沉浸式环境应用*

**示例使用**
* 一个沉浸式应用，使用户能够浏览与他们自己的 (完全分离的空间，例如，演练著名大楼、博物馆、流行城) 
* 一种沉浸式应用程序，用于协调用户的事件或方案 (即工作或性能) 

## <a name="see-also"></a>另请参阅
* [开发概述](../develop/development.md)
* [应用模型](app-model.md)
* [应用视图](app-views.md)
