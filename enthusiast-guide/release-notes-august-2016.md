---
title: 发行说明 - 2016 年 8 月
description: 对于秋季2016，请随时了解适用于 Windows 10 周年发行说明的最新版本。
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens，发行说明，os，平台，功能，商业套件
ms.openlocfilehash: c70da10043cfbcfa88105635f2467c8feaadbedf
ms.sourcegitcommit: d3a3b4f13b3728cfdd4d43035c806c0791d3f2fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "98581646"
---
# <a name="release-notes---august-2016"></a><span data-ttu-id="c7c34-104">发行说明 - 2016 年 8 月</span><span class="sxs-lookup"><span data-stu-id="c7c34-104">Release notes - August 2016</span></span>

<span data-ttu-id="c7c34-105">HoloLens 团队正在侦听来自 Windows 预览体验计划中的开发人员的反馈，以确定工作优先级。</span><span class="sxs-lookup"><span data-stu-id="c7c34-105">The HoloLens team is listening to feedback from developers in the Windows Insider Program to prioritize our work.</span></span> <span data-ttu-id="c7c34-106">通过反馈中心、[开发人员论坛](https://forums.hololens.com) [ @HoloLens 和 Twitter](https://twitter.com/hololens)继续向[我们提供反馈](/windows/mixed-reality/give-us-feedback)。</span><span class="sxs-lookup"><span data-stu-id="c7c34-106">Continue to [give us feedback](/windows/mixed-reality/give-us-feedback) through the Feedback Hub, the [developer forums](https://forums.hololens.com) and [Twitter via @HoloLens](https://twitter.com/hololens).</span></span> <span data-ttu-id="c7c34-107">由于 Windows 10 涵盖周年周年更新，因此 HoloLens 团队很乐意更好地提高全息体验。</span><span class="sxs-lookup"><span data-stu-id="c7c34-107">As Windows 10 embraces the Anniversary Update, the HoloLens team is happy to deliver further improve to the holographic experience.</span></span> <span data-ttu-id="c7c34-108">在此更新中，我们侧重于主要修补程序、改进功能和引入企业请求的功能，并在 Microsoft HoloLens 商业套件中提供。</span><span class="sxs-lookup"><span data-stu-id="c7c34-108">In this update, we focused on major fixes, improvements, and introducing features requested by businesses and available in the Microsoft HoloLens Commercial Suite.</span></span>

<span data-ttu-id="c7c34-109">**最新版本：** Windows 全息8月2016更新 (**10.0.14393.0**、Windows 10 周年) </span><span class="sxs-lookup"><span data-stu-id="c7c34-109">**Latest release:** Windows Holographic August 2016 Update (**10.0.14393.0**, Windows 10 Anniversary Release)</span></span>

>[!VIDEO https://www.youtube.com/embed/tNd0e2CiAkE]

<span data-ttu-id="c7c34-110">若要 [更新到当前版本](/windows/mixed-reality/updating-hololens)，请打开 " *设置* " 应用，中转到 " *更新 & 安全性*"，然后选择 " *检查更新* " 按钮。</span><span class="sxs-lookup"><span data-stu-id="c7c34-110">To [update to the current release](/windows/mixed-reality/updating-hololens), open the *Settings* app, go to *Update & Security*, then select the *Check for updates* button.</span></span>

## <a name="new-features"></a><span data-ttu-id="c7c34-111">新增功能</span><span class="sxs-lookup"><span data-stu-id="c7c34-111">New features</span></span>

<span data-ttu-id="c7c34-112">**附加到进程调试** HoloLens 现在支持附加到进程调试。</span><span class="sxs-lookup"><span data-stu-id="c7c34-112">**Attach To Process Debugging** HoloLens now supports attach-to-process debugging.</span></span> <span data-ttu-id="c7c34-113">你可以使用 Visual Studio 2015 Update 3 连接到 HoloLens 上正在运行的应用程序并 [开始对其进行调试](/windows/mixed-reality/develop/platform-capabilities-and-apis/using-visual-studio#debugging-an-installed-or-running-app)。</span><span class="sxs-lookup"><span data-stu-id="c7c34-113">You can use Visual Studio 2015 Update 3 to connect to a running app on a HoloLens and [start debugging it](/windows/mixed-reality/develop/platform-capabilities-and-apis/using-visual-studio#debugging-an-installed-or-running-app).</span></span> <span data-ttu-id="c7c34-114">这无需从 Visual Studio 项目中进行部署。</span><span class="sxs-lookup"><span data-stu-id="c7c34-114">This works without the need to deploy from a Visual Studio project.</span></span>

<span data-ttu-id="c7c34-115">**已更新 HoloLens 模拟器** 我们还发布了 HoloLens 模拟器的更新版本。</span><span class="sxs-lookup"><span data-stu-id="c7c34-115">**Updated HoloLens Emulator** We've also released an updated version of the HoloLens Emulator.</span></span>

<span data-ttu-id="c7c34-116">**游戏板支持** 你现在可以将蓝牙 gamepads 与 HoloLens 配对并使用！</span><span class="sxs-lookup"><span data-stu-id="c7c34-116">**Gamepad Support** You can now pair and use Bluetooth gamepads with HoloLens!</span></span> <span data-ttu-id="c7c34-117">新发布的 Xbox 无线控制器具有蓝牙功能，可用于播放你最喜欢的启用游戏程序的游戏和应用程序。</span><span class="sxs-lookup"><span data-stu-id="c7c34-117">The newly released Xbox Wireless Controller S features Bluetooth capabilities and can be used to play your favorite gamepad-enabled games and apps.</span></span> <span data-ttu-id="c7c34-118">必须先应用 [控制器更新](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) ，然后才能使用 HoloLens 连接 Xbox 无线控制器。</span><span class="sxs-lookup"><span data-stu-id="c7c34-118">A [controller update](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) must be applied before you can connect the Xbox Wireless Controller S with HoloLens.</span></span> <span data-ttu-id="c7c34-119">[XInput](/windows/win32/xinput/xinput-game-controller-apis-portal)和[Windows 工作输入](/uwp/api/Windows.Gaming.Input)Api 支持 Xbox 无线控制器。</span><span class="sxs-lookup"><span data-stu-id="c7c34-119">The Xbox Wireless Controller S is supported by [XInput](/windows/win32/xinput/xinput-game-controller-apis-portal) and [Windows.Gaming.Input](/uwp/api/Windows.Gaming.Input) APIs.</span></span> <span data-ttu-id="c7c34-120">可以通过 [Windows. 游戏输入](/uwp/api/Windows.Gaming.Input) API 访问更多的蓝牙控制器模型。</span><span class="sxs-lookup"><span data-stu-id="c7c34-120">You can access more Bluetooth controllers models through the [Windows.Gaming.Input](/uwp/api/Windows.Gaming.Input) API.</span></span>

## <a name="improvements-and-fixes"></a><span data-ttu-id="c7c34-121">改进和修复</span><span class="sxs-lookup"><span data-stu-id="c7c34-121">Improvements and fixes</span></span>

<span data-ttu-id="c7c34-122">我们与 Windows 10 周年更新的其余部分保持同步，因此除了 HoloLens 特定的修补程序，你还可以从 Windows 更新中获得所有性能，以提高平台的可靠性和性能。</span><span class="sxs-lookup"><span data-stu-id="c7c34-122">We're in sync with the rest of the Windows 10 Anniversary update, so in addition to the HoloLens specific fixes, you're also receiving all the goodness from the Windows update to increase platform reliability and performance.</span></span> <span data-ttu-id="c7c34-123">你的反馈非常重视，并优先于版本中的修补程序。</span><span class="sxs-lookup"><span data-stu-id="c7c34-123">Your feedback is highly valued and prioritized for fixes in the release.</span></span>

<span data-ttu-id="c7c34-124">我们改进了以下体验：</span><span class="sxs-lookup"><span data-stu-id="c7c34-124">We've improved the following experiences:</span></span>
* <span data-ttu-id="c7c34-125">登录体验。</span><span class="sxs-lookup"><span data-stu-id="c7c34-125">log in experiences.</span></span>
* <span data-ttu-id="c7c34-126">工作区加入。</span><span class="sxs-lookup"><span data-stu-id="c7c34-126">workplaces join.</span></span>
* <span data-ttu-id="c7c34-127">设备电源状态转换的能源效率。</span><span class="sxs-lookup"><span data-stu-id="c7c34-127">power efficiency for device power state transitions.</span></span>
* <span data-ttu-id="c7c34-128">混合现实捕获的稳定性。</span><span class="sxs-lookup"><span data-stu-id="c7c34-128">stability with Mixed Reality Captures.</span></span>
* <span data-ttu-id="c7c34-129">蓝牙连接的可靠性</span><span class="sxs-lookup"><span data-stu-id="c7c34-129">reliability for Bluetooth connectivity</span></span>
* <span data-ttu-id="c7c34-130">多应用场景中的全息影像持久性。</span><span class="sxs-lookup"><span data-stu-id="c7c34-130">hologram persistence in multi app scenario.</span></span>

<span data-ttu-id="c7c34-131">我们修复了以下问题：</span><span class="sxs-lookup"><span data-stu-id="c7c34-131">We've fixed the following issues:</span></span>
* <span data-ttu-id="c7c34-132">Visual Studio 探查器和图形调试器无法连接。</span><span class="sxs-lookup"><span data-stu-id="c7c34-132">the Visual Studio profilers and graphics debugger fail to connect.</span></span>
* <span data-ttu-id="c7c34-133">照片 & 文档不会显示在设备门户的文件资源管理器中。</span><span class="sxs-lookup"><span data-stu-id="c7c34-133">photos & documents don't show up in the file explorer in the device portal.</span></span>
* <span data-ttu-id="c7c34-134">当光标位于调整模式下时，应用程序栏可以闪烁。</span><span class="sxs-lookup"><span data-stu-id="c7c34-134">the App Bar can flash when the cursor is placed above it while in Adjust mode.</span></span>
* <span data-ttu-id="c7c34-135">处于调整模式时，眼睛点光标将在一段时间内更改为4箭头光标。</span><span class="sxs-lookup"><span data-stu-id="c7c34-135">When in Adjust mode, the eye gaze dot cursor will change to the 4-arrow cursor sometime more slowly.</span></span>
* <span data-ttu-id="c7c34-136">"你好 Cortana 播放音乐" 不启动 Groove。</span><span class="sxs-lookup"><span data-stu-id="c7c34-136">"Hey Cortana play music" doesn't launch Groove.</span></span>
* <span data-ttu-id="c7c34-137">在上一次更新后，说 "回家 Home" 不会正确显示 pin 面板。</span><span class="sxs-lookup"><span data-stu-id="c7c34-137">after the previous update, saying "Go Home" doesn't display the pins panel correctly.</span></span>

## <a name="introducing-microsoft-hololens-commercial-suite"></a><span data-ttu-id="c7c34-138">Microsoft HoloLens 商用套件简介</span><span class="sxs-lookup"><span data-stu-id="c7c34-138">Introducing Microsoft HoloLens Commercial Suite</span></span>

<span data-ttu-id="c7c34-139">Microsoft HoloLens 商用套件已准备好进行企业部署。</span><span class="sxs-lookup"><span data-stu-id="c7c34-139">The Microsoft HoloLens Commercial Suite is ready for enterprise deployment.</span></span> <span data-ttu-id="c7c34-140">我们已从早期企业合作伙伴添加了多个高请求 [商业功能](/windows/mixed-reality/commercial-features) 。</span><span class="sxs-lookup"><span data-stu-id="c7c34-140">We've added several highly requested [commercial features](/windows/mixed-reality/commercial-features) from our early business partners.</span></span>

<span data-ttu-id="c7c34-141">请与当地 Microsoft 帐户经理联系以购买 Microsoft HoloLens 商用套件。</span><span class="sxs-lookup"><span data-stu-id="c7c34-141">Contact your local Microsoft account manager to purchase the Microsoft HoloLens Commercial Suite.</span></span>

### <a name="key-commercial-features"></a><span data-ttu-id="c7c34-142">主要商业功能</span><span class="sxs-lookup"><span data-stu-id="c7c34-142">Key Commercial Features</span></span> 

* <span data-ttu-id="c7c34-143">**展台模式。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-143">**Kiosk mode.**</span></span> <span data-ttu-id="c7c34-144">使用 HoloLens 展台模式，你可以限制要运行哪些应用来启用演示或展示体验。</span><span class="sxs-lookup"><span data-stu-id="c7c34-144">With HoloLens kiosk mode, you can limit which apps to run to enable demo or showcase experiences.</span></span><br>
  <span data-ttu-id="c7c34-145">![通过展台模式，HoloLens 直接启动到所选的应用。](images/201608-kioskmode-400px.png)</span><span class="sxs-lookup"><span data-stu-id="c7c34-145">![With kiosk mode, HoloLens launches directly into the app of your choice.](images/201608-kioskmode-400px.png)</span></span>
* <span data-ttu-id="c7c34-146">**针对 HoloLens (MDM) 的移动设备管理。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-146">**Mobile Device Management (MDM) for HoloLens.**</span></span> <span data-ttu-id="c7c34-147">你的 IT 部门可以使用 Microsoft Intune 的解决方案同时管理多个 HoloLens 设备。</span><span class="sxs-lookup"><span data-stu-id="c7c34-147">Your IT department can manage multiple HoloLens devices simultaneously using solutions like Microsoft Intune.</span></span> <span data-ttu-id="c7c34-148">你可以管理设置，选择要安装的应用，并设置根据你的组织的需要定制的安全配置。</span><span class="sxs-lookup"><span data-stu-id="c7c34-148">You can manage settings, select apps to install and set security configurations tailored to your organization's need.</span></span><br>
  <span data-ttu-id="c7c34-149">![HoloLens 版移动设备管理提供跨多个设备的企业级设备管理。](images/201608-enterprisemanagement-400px.png)</span><span class="sxs-lookup"><span data-stu-id="c7c34-149">![Mobile Device Management on HoloLens provides enterprise grade device management across multiple devices.](images/201608-enterprisemanagement-400px.png)</span></span>
* <span data-ttu-id="c7c34-150">**适用于企业的 Windows 更新。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-150">**Windows Update for Business.**</span></span> <span data-ttu-id="c7c34-151">受控操作系统更新到设备和支持长期服务分支。</span><span class="sxs-lookup"><span data-stu-id="c7c34-151">Controlled operating system updates to devices and support for long-term servicing branch.</span></span>
* <span data-ttu-id="c7c34-152">**数据安全性。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-152">**Data security.**</span></span> <span data-ttu-id="c7c34-153">BitLocker 数据加密在 HoloLens 上启用，以提供与任何其他 Windows 设备相同级别的安全保护。</span><span class="sxs-lookup"><span data-stu-id="c7c34-153">BitLocker data encryption is enabled on HoloLens to provide the same level of security protection as any other Windows device.</span></span>
* <span data-ttu-id="c7c34-154">**工作访问。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-154">**Work access.**</span></span> <span data-ttu-id="c7c34-155">你的组织中的任何人都可以通过 HoloLens 上的虚拟专用网络远程连接到公司网络。</span><span class="sxs-lookup"><span data-stu-id="c7c34-155">Anyone in your organization can remotely connect to the corporate network through virtual private network on a HoloLens.</span></span> <span data-ttu-id="c7c34-156">HoloLens 还可以访问需要凭据 Wi-Fi 网络。</span><span class="sxs-lookup"><span data-stu-id="c7c34-156">HoloLens can also access Wi-Fi networks that require credentials.</span></span>
* <span data-ttu-id="c7c34-157">**适用于企业的 Microsoft Store。**</span><span class="sxs-lookup"><span data-stu-id="c7c34-157">**Microsoft Store for Business.**</span></span> <span data-ttu-id="c7c34-158">你的 IT 部门还可以设置企业专用商店，只包含适用于你的特定 HoloLens 用途的公司应用。</span><span class="sxs-lookup"><span data-stu-id="c7c34-158">Your IT department can also set up an enterprise private store, containing only your company’s apps for your specific HoloLens usage.</span></span> <span data-ttu-id="c7c34-159">将企业软件安全地分发到选定的企业用户组。</span><span class="sxs-lookup"><span data-stu-id="c7c34-159">Securely distribute your enterprise software to selected group of enterprise users.</span></span>

### <a name="development-edition-vs-commercial-suite"></a><span data-ttu-id="c7c34-160">开发版与商业套件</span><span class="sxs-lookup"><span data-stu-id="c7c34-160">Development Edition vs. Commercial Suite</span></span>

<table>
<tr>
<th><span data-ttu-id="c7c34-161">功能</span><span class="sxs-lookup"><span data-stu-id="c7c34-161">Features</span></span></th><th><span data-ttu-id="c7c34-162">Development Edition</span><span class="sxs-lookup"><span data-stu-id="c7c34-162">Development Edition</span></span></th><th><span data-ttu-id="c7c34-163">商业套件</span><span class="sxs-lookup"><span data-stu-id="c7c34-163">Commercial Suite</span></span></th>
</tr><tr>
<td><span data-ttu-id="c7c34-164">Bitlocker) 的设备加密 (</span><span class="sxs-lookup"><span data-stu-id="c7c34-164">Device Encryption (Bitlocker)</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-165">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-165">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-166">虚拟专用网络 (VPN)</span><span class="sxs-lookup"><span data-stu-id="c7c34-166">Virtual Private Network (VPN)</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-167">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-167">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-168"><a href="/windows/mixed-reality/develop/platform-capabilities-and-apis/using-the-windows-device-portal#kiosk-mode">展台模式</a></span><span class="sxs-lookup"><span data-stu-id="c7c34-168"><a href="/windows/mixed-reality/develop/platform-capabilities-and-apis/using-the-windows-device-portal#kiosk-mode">Kiosk mode</a></span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-169">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-169">✔️</span></span></td>
</tr><tr>
<th colspan="3" style="text-align: left;"> <span data-ttu-id="c7c34-170">管理和部署</span><span class="sxs-lookup"><span data-stu-id="c7c34-170">Management and deployment</span></span></th>
</tr><tr>
<td><span data-ttu-id="c7c34-171">移动设备管理 (MDM)</span><span class="sxs-lookup"><span data-stu-id="c7c34-171">Mobile Device Management (MDM)</span></span></td><td style="text-align: center;"></td><td style="text-align: center;"><span data-ttu-id="c7c34-172">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-172">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-173">阻止取消注册的功能</span><span class="sxs-lookup"><span data-stu-id="c7c34-173">Ability to block unenrollment</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-174">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-174">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-175">基于证书的企业 Wi-Fi 访问</span><span class="sxs-lookup"><span data-stu-id="c7c34-175">Cert Based Corporate Wi-Fi Access</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-176">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-176">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-177"> (使用者 Microsoft Store) </span><span class="sxs-lookup"><span data-stu-id="c7c34-177">Microsoft Store (Consumer)</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-178">使用者</span><span class="sxs-lookup"><span data-stu-id="c7c34-178">Consumer</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-179">通过 MDM 筛选</span><span class="sxs-lookup"><span data-stu-id="c7c34-179">Filtering via MDM</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-180"><a href="/microsoft-store/working-with-line-of-business-apps">业务商店门户</a></span><span class="sxs-lookup"><span data-stu-id="c7c34-180"><a href="/microsoft-store/working-with-line-of-business-apps">Business Store Portal</a></span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-181">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-181">✔️</span></span></td>
</tr><tr>
<th colspan="3" style="text-align: left;"> <span data-ttu-id="c7c34-182">安全性和标识</span><span class="sxs-lookup"><span data-stu-id="c7c34-182">Security and Identity</span></span></th>
</tr><tr>
<td><span data-ttu-id="c7c34-183">利用 Azure Active Directory (AAD) 登录</span><span class="sxs-lookup"><span data-stu-id="c7c34-183">Log in with Azure Active Directory (AAD)</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-184">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-184">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-185">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-185">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-186">用 Microsoft 帐户登录 (MSA) </span><span class="sxs-lookup"><span data-stu-id="c7c34-186">Log in with Microsoft Account (MSA)</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-187">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-187">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-188">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-188">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-189">带有 PIN 解锁的下一代凭据</span><span class="sxs-lookup"><span data-stu-id="c7c34-189">Next Generation Credentials with PIN unlock</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-190">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-190">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-191">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-191">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-192"><a href="/windows-hardware/design/device-experiences/oem-secure-boot">安全启动</a></span><span class="sxs-lookup"><span data-stu-id="c7c34-192"><a href="/windows-hardware/design/device-experiences/oem-secure-boot">Secure boot</a></span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-193">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-193">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-194">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-194">✔️</span></span></td>
</tr><tr>
<th colspan="3" style="text-align: left;"> <span data-ttu-id="c7c34-195">服务和支持</span><span class="sxs-lookup"><span data-stu-id="c7c34-195">Servicing and Support</span></span></th>
</tr><tr>
<td><span data-ttu-id="c7c34-196">自动系统更新到达时自动更新</span><span class="sxs-lookup"><span data-stu-id="c7c34-196">Automatic system updates as they arrive</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-197">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-197">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="c7c34-198">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-198">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-199"><a href="/windows/deployment/update/waas-manage-updates-wufb">Windows Update for Business</a></span><span class="sxs-lookup"><span data-stu-id="c7c34-199"><a href="/windows/deployment/update/waas-manage-updates-wufb">Windows Update for Business</a></span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-200">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-200">✔️</span></span></td>
</tr><tr>
<td><span data-ttu-id="c7c34-201">Long Term Servicing Branch</span><span class="sxs-lookup"><span data-stu-id="c7c34-201">Long-term servicing branch</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="c7c34-202">✔️</span><span class="sxs-lookup"><span data-stu-id="c7c34-202">✔️</span></span></td>
</tr>
</table>

## <a name="prior-release-notes"></a><span data-ttu-id="c7c34-203">以前的发行说明</span><span class="sxs-lookup"><span data-stu-id="c7c34-203">Prior release notes</span></span>
* [<span data-ttu-id="c7c34-204">发行说明 - 2016 年 5 月</span><span class="sxs-lookup"><span data-stu-id="c7c34-204">Release notes - May 2016</span></span>](release-notes-may-2016.md)
* [<span data-ttu-id="c7c34-205">发行说明 - 2016 年 3 月</span><span class="sxs-lookup"><span data-stu-id="c7c34-205">Release notes - March 2016</span></span>](release-notes-march-2016.md)

## <a name="see-also"></a><span data-ttu-id="c7c34-206">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c7c34-206">See also</span></span>
* [<span data-ttu-id="c7c34-207">HoloLens 已知问题</span><span class="sxs-lookup"><span data-stu-id="c7c34-207">HoloLens known issues</span></span>](/windows/mixed-reality/hololens-known-issues)
* [<span data-ttu-id="c7c34-208">商业功能</span><span class="sxs-lookup"><span data-stu-id="c7c34-208">Commercial features</span></span>](/windows/mixed-reality/commercial-features)
* [<span data-ttu-id="c7c34-209">安装工具</span><span class="sxs-lookup"><span data-stu-id="c7c34-209">Install the tools</span></span>](/windows/mixed-reality/develop/install-the-tools)
* [<span data-ttu-id="c7c34-210">使用 HoloLens 仿真器</span><span class="sxs-lookup"><span data-stu-id="c7c34-210">Using the HoloLens emulator</span></span>](/windows/mixed-reality/develop/platform-capabilities-and-apis/using-the-hololens-emulator)