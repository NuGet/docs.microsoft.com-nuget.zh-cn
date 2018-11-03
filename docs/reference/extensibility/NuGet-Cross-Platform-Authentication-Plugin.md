---
title: NuGet 跨平台身份验证插件
description: NuGet 的 NuGet.exe、 dotnet.exe、 msbuild.exe 和 Visual Studio 跨平台身份验证插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: d80339eb81ade1cf2c323a604cc4fac06dcb1012
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981049"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="80fb4-103">NuGet 跨平台身份验证插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="80fb4-104">在版本 4.8 +，客户端 (NuGet.exe，Visual Studio、 dotnet.exe 和 MSBuild.exe) 可使用身份验证插件构建的所有 NuGet[跨平台插件 NuGet](NuGet-Cross-Platform-Plugins.md)模型。</span><span class="sxs-lookup"><span data-stu-id="80fb4-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="80fb4-105">Dotnet.exe 中的身份验证</span><span class="sxs-lookup"><span data-stu-id="80fb4-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="80fb4-106">Visual Studio 和 NuGet.exe 是交互式的默认情况下。</span><span class="sxs-lookup"><span data-stu-id="80fb4-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="80fb4-107">NuGet.exe 包含一个开关，它使得[非交互式](../../tools/nuget-exe-CLI-Reference.md)。</span><span class="sxs-lookup"><span data-stu-id="80fb4-107">NuGet.exe contains a switch to make it [non interactive](../../tools/nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="80fb4-108">此外，NuGet.exe 和 Visual Studio 插件提示用户输入。</span><span class="sxs-lookup"><span data-stu-id="80fb4-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="80fb4-109">Dotnet.exe 中没有任何提示，默认值为非交互式。</span><span class="sxs-lookup"><span data-stu-id="80fb4-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="80fb4-110">Dotnet.exe 中的身份验证机制是设备流。</span><span class="sxs-lookup"><span data-stu-id="80fb4-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="80fb4-111">当还原或添加操作块和用户如何向完成身份验证将提供命令行的说明，以交互方式运行包操作。</span><span class="sxs-lookup"><span data-stu-id="80fb4-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="80fb4-112">当用户完成身份验证将继续操作。</span><span class="sxs-lookup"><span data-stu-id="80fb4-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="80fb4-113">若要使该操作具有交互性，一个应传递`--interactive`。</span><span class="sxs-lookup"><span data-stu-id="80fb4-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="80fb4-114">当前仅显式`dotnet restore`和`dotnet add package`命令支持交互式切换。</span><span class="sxs-lookup"><span data-stu-id="80fb4-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="80fb4-115">在没有交互式开关`dotnet build`和`dotnet publish`。</span><span class="sxs-lookup"><span data-stu-id="80fb4-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="80fb4-116">在 MSBuild 中的身份验证</span><span class="sxs-lookup"><span data-stu-id="80fb4-116">Authentication in MSBuild</span></span>

<span data-ttu-id="80fb4-117">类似于 dotnet.exe，MSBuild.exe 默认为非交互式 MSBuild.exe 身份验证机制是设备流。</span><span class="sxs-lookup"><span data-stu-id="80fb4-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="80fb4-118">若要允许还原后，若要暂停并等待身份验证，请调用使用还原`msbuild /t:restore /p:NuGetInteractive="true"`。</span><span class="sxs-lookup"><span data-stu-id="80fb4-118">To allow the restore to pause and wait for authentication, call restore with `msbuild /t:restore /p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="80fb4-119">创建跨平台身份验证插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="80fb4-120">示例实现可在[Microsoft 凭据提供程序插件](https://github.com/Microsoft/artifacts-credprovider)。</span><span class="sxs-lookup"><span data-stu-id="80fb4-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="80fb4-121">它是非常重要的插件，符合所提出的 NuGet 客户端工具的安全要求。</span><span class="sxs-lookup"><span data-stu-id="80fb4-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="80fb4-122">所需的最低版本为插件以进行身份验证插件*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="80fb4-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="80fb4-123">NuGet 将执行与插件和查询握手的受支持的操作声明。</span><span class="sxs-lookup"><span data-stu-id="80fb4-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="80fb4-124">跨平台插件 NuGet，请参阅[协议消息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)有关特定消息的详细信息。</span><span class="sxs-lookup"><span data-stu-id="80fb4-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="80fb4-125">NuGet 会将日志级别设置和代理服务器信息提供给插件时适用。</span><span class="sxs-lookup"><span data-stu-id="80fb4-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="80fb4-126">记录到 NuGet 控制台可接受后才 NuGet 已将日志级别设置为该插件。</span><span class="sxs-lookup"><span data-stu-id="80fb4-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="80fb4-127">.NET framework 插件的身份验证行为</span><span class="sxs-lookup"><span data-stu-id="80fb4-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="80fb4-128">在.NET Framework 中，插件可以提示用户提供输入，在对话框的窗体中。</span><span class="sxs-lookup"><span data-stu-id="80fb4-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="80fb4-129">.NET core 插件的身份验证行为</span><span class="sxs-lookup"><span data-stu-id="80fb4-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="80fb4-130">在.NET Core 中，不能显示一个对话框。</span><span class="sxs-lookup"><span data-stu-id="80fb4-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="80fb4-131">插件应使用设备流身份验证。</span><span class="sxs-lookup"><span data-stu-id="80fb4-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="80fb4-132">该插件可将日志消息发送到 NuGet，向用户说明。</span><span class="sxs-lookup"><span data-stu-id="80fb4-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="80fb4-133">请注意，日志记录可用后的日志级别已设置为该插件。</span><span class="sxs-lookup"><span data-stu-id="80fb4-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="80fb4-134">NuGet 不会从命令行的任何交互式输入。</span><span class="sxs-lookup"><span data-stu-id="80fb4-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="80fb4-135">当客户端调用时获得获取身份验证凭据的插件时，插件需要符合交互性开关并遵循对话框开关。</span><span class="sxs-lookup"><span data-stu-id="80fb4-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="80fb4-136">下表总结了该插件的所有组合的行为方式。</span><span class="sxs-lookup"><span data-stu-id="80fb4-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="80fb4-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="80fb4-137">IsNonInteractive</span></span> | <span data-ttu-id="80fb4-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="80fb4-138">CanShowDialog</span></span> | <span data-ttu-id="80fb4-139">插件行为</span><span class="sxs-lookup"><span data-stu-id="80fb4-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="80fb4-140">true</span><span class="sxs-lookup"><span data-stu-id="80fb4-140">true</span></span> | <span data-ttu-id="80fb4-141">true</span><span class="sxs-lookup"><span data-stu-id="80fb4-141">true</span></span> | <span data-ttu-id="80fb4-142">IsNonInteractive 开关将优先于对话框开关。</span><span class="sxs-lookup"><span data-stu-id="80fb4-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="80fb4-143">该插件不能弹出一个对话框。</span><span class="sxs-lookup"><span data-stu-id="80fb4-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="80fb4-144">此组合所适用的.NET Framework 插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="80fb4-145">true</span><span class="sxs-lookup"><span data-stu-id="80fb4-145">true</span></span> | <span data-ttu-id="80fb4-146">False</span><span class="sxs-lookup"><span data-stu-id="80fb4-146">false</span></span> | <span data-ttu-id="80fb4-147">IsNonInteractive 开关将优先于对话框开关。</span><span class="sxs-lookup"><span data-stu-id="80fb4-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="80fb4-148">该插件不能阻止。</span><span class="sxs-lookup"><span data-stu-id="80fb4-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="80fb4-149">这种组合时才有效.NET 核心插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="80fb4-150">False</span><span class="sxs-lookup"><span data-stu-id="80fb4-150">false</span></span> | <span data-ttu-id="80fb4-151">true</span><span class="sxs-lookup"><span data-stu-id="80fb4-151">true</span></span> | <span data-ttu-id="80fb4-152">插件应显示一个对话框。</span><span class="sxs-lookup"><span data-stu-id="80fb4-152">The plugin should show a dialog.</span></span> <span data-ttu-id="80fb4-153">此组合所适用的.NET Framework 插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="80fb4-154">False</span><span class="sxs-lookup"><span data-stu-id="80fb4-154">false</span></span> | <span data-ttu-id="80fb4-155">False</span><span class="sxs-lookup"><span data-stu-id="80fb4-155">false</span></span> | <span data-ttu-id="80fb4-156">插件应可以显示一个对话框。</span><span class="sxs-lookup"><span data-stu-id="80fb4-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="80fb4-157">插件应使用设备流的日志记录通过记录器的指令消息进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="80fb4-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="80fb4-158">这种组合时才有效.NET 核心插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="80fb4-159">请参阅以下规范在编写一个插件之前。</span><span class="sxs-lookup"><span data-stu-id="80fb4-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="80fb4-160">NuGet 包下载插件</span><span class="sxs-lookup"><span data-stu-id="80fb4-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="80fb4-161">跨平台身份验证插件的 NuGet</span><span class="sxs-lookup"><span data-stu-id="80fb4-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
