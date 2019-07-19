---
title: NuGet 跨平台身份验证插件
description: Nuget、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平台身份验证插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317283"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="c0f8a-103">NuGet 跨平台身份验证插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="c0f8a-104">在版本 4.8 + 中, 所有 NuGet 客户端 (Nuget.exe、Visual Studio、dotnet 和 Msbuild.exe) 都可以使用在[NuGet 跨平台插件](NuGet-Cross-Platform-Plugins.md)模型之上构建的身份验证插件。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="c0f8a-105">Dotnet 中的身份验证</span><span class="sxs-lookup"><span data-stu-id="c0f8a-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="c0f8a-106">默认情况下, Visual Studio 和 Nuget.exe 是交互式的。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="c0f8a-107">Nuget.exe 包含用于使其成为[非交互式](../nuget-exe-CLI-Reference.md)的开关。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-107">NuGet.exe contains a switch to make it [non interactive](../nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="c0f8a-108">此外, Nuget.exe 和 Visual Studio 插件会提示用户输入。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="c0f8a-109">在 dotnet 中没有提示, 默认值为非交互式。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="c0f8a-110">Dotnet 中的身份验证机制是设备流。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="c0f8a-111">如果 "还原" 或 "添加包" 操作以交互方式运行, 则在命令行上将会阻止操作并向用户提供如何完成身份验证的说明。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="c0f8a-112">用户完成身份验证后, 操作将继续。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="c0f8a-113">若要使操作具有交互性, 应通过`--interactive`一个。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="c0f8a-114">目前只有显式`dotnet restore`和`dotnet add package`命令支持交互式切换。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="c0f8a-115">`dotnet build` 和`dotnet publish`上没有交互式开关。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="c0f8a-116">MSBuild 中的身份验证</span><span class="sxs-lookup"><span data-stu-id="c0f8a-116">Authentication in MSBuild</span></span>

<span data-ttu-id="c0f8a-117">与 dotnet 类似, Msbuild.exe 默认情况下不交互, msbuild.exe 身份验证机制是设备流。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="c0f8a-118">若要允许还原暂停并等待身份验证, 请调用 restore with `msbuild -t:restore -p:NuGetInteractive="true"`。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-118">To allow the restore to pause and wait for authentication, call restore with `msbuild -t:restore -p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="c0f8a-119">创建跨平台身份验证插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="c0f8a-120">可以在[Microsoft 凭据提供程序插件](https://github.com/Microsoft/artifacts-credprovider)中找到示例实现。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="c0f8a-121">插件必须符合 NuGet 客户端工具所规定的安全要求, 这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="c0f8a-122">作为身份验证插件的插件所需的最低版本为*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="c0f8a-123">NuGet 将通过插件执行握手, 并查询支持的操作声明。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="c0f8a-124">有关特定消息的详细信息, 请参阅 NuGet 跨平台插件[协议消息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="c0f8a-125">NuGet 会将日志级别设置为 "可用", 并向该插件提供代理信息。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="c0f8a-126">仅在 NuGet 将日志级别设置为插件后, 才可以接受日志记录到 NuGet 控制台。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="c0f8a-127">.NET Framework 插件身份验证行为</span><span class="sxs-lookup"><span data-stu-id="c0f8a-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="c0f8a-128">在 .NET Framework 中, 允许插件以对话框的形式提示用户输入。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="c0f8a-129">.NET Core 插件身份验证行为</span><span class="sxs-lookup"><span data-stu-id="c0f8a-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="c0f8a-130">在 .NET Core 中, 无法显示对话框。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="c0f8a-131">插件应该使用设备流进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="c0f8a-132">该插件可以向 NuGet 发送日志消息, 并向用户发送说明。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="c0f8a-133">请注意, 在日志级别设置为插件后, 日志记录可用。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="c0f8a-134">NuGet 不会从命令行获取任何交互式输入。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="c0f8a-135">当客户端使用获取身份验证凭据调用插件时, 插件需要符合交互交换机, 并遵循对话开关。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="c0f8a-136">下表总结了插件对于所有组合的行为方式。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="c0f8a-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="c0f8a-137">IsNonInteractive</span></span> | <span data-ttu-id="c0f8a-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="c0f8a-138">CanShowDialog</span></span> | <span data-ttu-id="c0f8a-139">插件行为</span><span class="sxs-lookup"><span data-stu-id="c0f8a-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="c0f8a-140">true</span><span class="sxs-lookup"><span data-stu-id="c0f8a-140">true</span></span> | <span data-ttu-id="c0f8a-141">true</span><span class="sxs-lookup"><span data-stu-id="c0f8a-141">true</span></span> | <span data-ttu-id="c0f8a-142">IsNonInteractive 开关优先于对话框开关。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="c0f8a-143">不允许插件弹出对话框。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="c0f8a-144">此组合仅对 .NET Framework 插件有效</span><span class="sxs-lookup"><span data-stu-id="c0f8a-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="c0f8a-145">true</span><span class="sxs-lookup"><span data-stu-id="c0f8a-145">true</span></span> | <span data-ttu-id="c0f8a-146">False</span><span class="sxs-lookup"><span data-stu-id="c0f8a-146">false</span></span> | <span data-ttu-id="c0f8a-147">IsNonInteractive 开关优先于对话框开关。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="c0f8a-148">不允许插件阻止。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="c0f8a-149">此组合仅适用于 .NET Core 插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="c0f8a-150">False</span><span class="sxs-lookup"><span data-stu-id="c0f8a-150">false</span></span> | <span data-ttu-id="c0f8a-151">true</span><span class="sxs-lookup"><span data-stu-id="c0f8a-151">true</span></span> | <span data-ttu-id="c0f8a-152">插件应该会显示一个对话框。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-152">The plugin should show a dialog.</span></span> <span data-ttu-id="c0f8a-153">此组合仅对 .NET Framework 插件有效</span><span class="sxs-lookup"><span data-stu-id="c0f8a-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="c0f8a-154">False</span><span class="sxs-lookup"><span data-stu-id="c0f8a-154">false</span></span> | <span data-ttu-id="c0f8a-155">False</span><span class="sxs-lookup"><span data-stu-id="c0f8a-155">false</span></span> | <span data-ttu-id="c0f8a-156">插件应/不能显示对话框。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="c0f8a-157">该插件应该使用设备流通过日志记录指令消息进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="c0f8a-158">此组合仅适用于 .NET Core 插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="c0f8a-159">请参阅以下规范, 然后再编写插件。</span><span class="sxs-lookup"><span data-stu-id="c0f8a-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="c0f8a-160">NuGet 包下载插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="c0f8a-161">NuGet 跨 x-plat 身份验证插件</span><span class="sxs-lookup"><span data-stu-id="c0f8a-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
