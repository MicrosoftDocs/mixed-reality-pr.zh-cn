---
title: 使用 Unity IL2CPP 进行托管调试
description: 本文介绍如何在 Unity IL2CPP UWP 项目上运行托管调试器。
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: unity，visual studio，调试，il2cpp，HoloLens，混合现实耳机，windows mixed reality 耳机，虚拟现实耳机，UWP
ms.openlocfilehash: 96a2c21fc6f8b2bdab199e65c9b1a31ffb6e029b
ms.sourcegitcommit: dd13a32a5bb90bd53eeeea8214cd5384d7b9ef76
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94678586"
---
# <a name="managed-debugging-with-unity-il2cpp"></a>使用 Unity IL2CPP 进行托管调试

按照以下步骤将托管调试器附加到 Unity IL2CPP UWP 生成。 本指南最初为 HoloLens 和 HoloLens 2 开发。

1. 需要在支持 [多播](https://en.wikipedia.org/wiki/Multicast)的网络上使用。
1. 确保 **InternetClientServer** 和 **PRIVATENETWORKCLIENTSERVER** 已在 UWP 发布设置功能下的 Unity 中签入。

    ![UWP 发布设置功能](images/il2cpp-debugging-capabilities.png)

1. 配置 Unity UWP 生成设置：
    - 开发生成
    - 脚本调试
    - 等待托管调试器 (可选) 

    ![UWP 生成设置](images/il2cpp-debugging-build.png)

1. 在 Unity 中构建。
1. 生成 Visual Studio 解决方案并将其部署到设备。 你应以 " **调试** " 或 " **发布** " 配置进行构建。 **主** 配置将禁用 Unity 探查器，并可防止优化调试。 （可选）在解决方案的 appxmanifest.xml 中的功能列表中验证 **Internet (客户端 & 服务器)** 和 **专用网络 (客户端 & 服务器)** 。
1. 在设备上启动应用。 确保你的设备已连接到与你的电脑相同的网络。
1. 请确保设备 **未** 通过 USB 连接到你的电脑。
1. 当你在 Unity 中双击脚本时，请使用创建的 Visual Studio 解决方案，你可以在其中查看和编辑 c # 脚本。
1. 调试-> 附加 Unity 调试器。

    ![附加 Unity 调试器](images/il2cpp-debugging-attach.png)

1. 在列表中选择你的设备，然后单击 "确定" 以附加。

    ![设备列表](images/il2cpp-debugging-machines.png)
