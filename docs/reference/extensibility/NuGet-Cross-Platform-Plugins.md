---
title: NuGet 跨平台插件
description: Nuget、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平台插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428383"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="bb8c7-103">NuGet 跨平台插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="bb8c7-104">已添加 NuGet 4.8 + 跨平台插件支持。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="bb8c7-105">这是通过生成新的插件扩展性模型实现的，该模型必须符合一组严格的操作规则。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="bb8c7-106">这些插件是独立的可执行文件（.NET Core world 中的 runnables），NuGet 客户端在单独的进程中启动。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="bb8c7-107">这是一次真正的写入，可在任何位置运行插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="bb8c7-108">它将适用于所有 NuGet 客户端工具。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="bb8c7-109">插件可以是 .NET Framework （Nuget.exe、Msbuild.exe 和 Visual Studio），也可以是 .NET Core （dotnet）。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="bb8c7-110">定义 NuGet 客户端与插件之间的版本控制通信协议。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="bb8c7-111">在启动握手期间，2个进程会协商协议版本。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="bb8c7-112">为了涵盖所有 NuGet 客户端工具方案，同时需要 .NET Framework 和 .NET Core 插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="bb8c7-113">下面介绍插件的客户端/框架组合。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="bb8c7-114">客户端工具</span><span class="sxs-lookup"><span data-stu-id="bb8c7-114">Client tool</span></span>  | <span data-ttu-id="bb8c7-115">框架</span><span class="sxs-lookup"><span data-stu-id="bb8c7-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="bb8c7-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb8c7-116">Visual Studio</span></span> | <span data-ttu-id="bb8c7-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb8c7-117">.NET Framework</span></span> |
| <span data-ttu-id="bb8c7-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="bb8c7-118">dotnet.exe</span></span> | <span data-ttu-id="bb8c7-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="bb8c7-119">.NET Core</span></span> |
| <span data-ttu-id="bb8c7-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bb8c7-120">NuGet.exe</span></span> | <span data-ttu-id="bb8c7-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb8c7-121">.NET Framework</span></span> |
| <span data-ttu-id="bb8c7-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="bb8c7-122">MSBuild.exe</span></span> | <span data-ttu-id="bb8c7-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb8c7-123">.NET Framework</span></span> |
| <span data-ttu-id="bb8c7-124">Mono 上的 Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bb8c7-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="bb8c7-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb8c7-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="bb8c7-126">工作原理</span><span class="sxs-lookup"><span data-stu-id="bb8c7-126">How does it work</span></span>

<span data-ttu-id="bb8c7-127">高级别工作流的描述如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="bb8c7-128">NuGet 发现可用插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="bb8c7-129">如果适用，NuGet 将按优先级顺序循环访问插件，并逐个启动插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="bb8c7-130">NuGet 将使用第一个可为请求服务的插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="bb8c7-131">插件不再需要时将关闭。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="bb8c7-132">一般插件要求</span><span class="sxs-lookup"><span data-stu-id="bb8c7-132">General plugin requirements</span></span>

<span data-ttu-id="bb8c7-133">当前协议版本为*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="bb8c7-134">在此版本下，要求如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="bb8c7-135">具有有效的受信任 Authenticode 签名程序集，将在 Windows 和 Mono 上运行。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="bb8c7-136">尚无对 Linux 和 Mac 上运行的程序集的特殊信任要求。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="bb8c7-137">相关问题</span><span class="sxs-lookup"><span data-stu-id="bb8c7-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="bb8c7-138">支持在 NuGet 客户端工具的当前安全上下文下进行无状态启动。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="bb8c7-139">例如，NuGet 客户端工具不会在稍后所述的插件协议之外执行提升或其他初始化。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="bb8c7-140">除非显式指定，否则为非交互式。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="bb8c7-141">遵循协商插件协议版本。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="bb8c7-142">在合理的时间段内响应所有请求。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="bb8c7-143">处理任何正在进行的操作的取消请求。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="bb8c7-144">以下规范更详细地介绍了技术规范：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="bb8c7-145">NuGet 包下载插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="bb8c7-146">NuGet 跨 x-plat 身份验证插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="bb8c7-147">客户端-插件交互</span><span class="sxs-lookup"><span data-stu-id="bb8c7-147">Client - Plugin interaction</span></span>

<span data-ttu-id="bb8c7-148">NuGet 客户端工具和插件通过标准流（stdin、stdout、stderr）与 JSON 通信。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="bb8c7-149">所有数据必须采用 UTF-8 编码。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="bb8c7-150">插件用参数 "-插件" 启动。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="bb8c7-151">如果用户在没有此参数的情况下直接启动了插件可执行文件，则该插件可以提供信息性消息，而不是等待协议握手。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="bb8c7-152">协议握手超时值为5秒。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="bb8c7-153">插件应尽可能简短地在中完成设置。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="bb8c7-154">NuGet 客户端工具将通过传入 NuGet 源的服务索引来查询插件支持的操作。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="bb8c7-155">插件可以使用服务索引来检查是否存在受支持的服务类型。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="bb8c7-156">NuGet 客户端工具与插件之间的通信是双向的。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="bb8c7-157">每个请求的超时为5秒。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="bb8c7-158">如果操作需要更长的时间，则应发送进度消息，以防止请求超时。1分钟处于非活动状态后，插件将被视为空闲状态并关闭。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="bb8c7-159">插件安装和发现</span><span class="sxs-lookup"><span data-stu-id="bb8c7-159">Plugin installation and discovery</span></span>

<span data-ttu-id="bb8c7-160">插件将通过基于约定的目录结构来发现。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="bb8c7-161">CI/CD 方案和超级用户可以使用环境变量来重写此行为。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="bb8c7-162">使用环境变量时，只允许使用绝对路径。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="bb8c7-163">请注意，`NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 仅适用于 5.3 + 版本的 NuGet 工具和更高版本。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="bb8c7-164">`NUGET_NETFX_PLUGIN_PATHS`-定义将由基于 .NET Framework 的工具（Nuget.exe/Msbuild.exe/Visual Studio）使用的插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="bb8c7-165">优先于 `NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="bb8c7-166">（仅 NuGet 版本 5.3 +）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="bb8c7-167">`NUGET_NETCORE_PLUGIN_PATHS`-定义将由基于 .NET Core 的工具（dotnet）使用的插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="bb8c7-168">优先于 `NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="bb8c7-169">（仅 NuGet 版本 5.3 +）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="bb8c7-170">`NUGET_PLUGIN_PATHS`-定义将用于 NuGet 进程的插件，保留优先级。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="bb8c7-171">如果设置了此环境变量，它将覆盖基于约定的发现。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="bb8c7-172">如果指定了任何一个框架特定的变量，则忽略。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="bb8c7-173">用户-位置，`%UserProfile%/.nuget/plugins`中的 NuGet 主页位置。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="bb8c7-174">此位置不能被重写。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-174">This location cannot be overriden.</span></span> <span data-ttu-id="bb8c7-175">.NET Core 和 .NET Framework 插件将使用不同的根目录。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="bb8c7-176">框架</span><span class="sxs-lookup"><span data-stu-id="bb8c7-176">Framework</span></span> | <span data-ttu-id="bb8c7-177">根发现位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="bb8c7-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="bb8c7-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="bb8c7-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bb8c7-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="bb8c7-180">每个插件都应安装在其自己的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="bb8c7-181">插件入口点将是已安装文件夹的名称，其扩展名为 .NET Core，.exe 扩展名用于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="bb8c7-182">当前没有用于安装插件的用户情景。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="bb8c7-183">只需将所需文件移动到预定位置即可。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="bb8c7-184">支持的操作</span><span class="sxs-lookup"><span data-stu-id="bb8c7-184">Supported operations</span></span>

<span data-ttu-id="bb8c7-185">新的插件协议支持两个操作。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="bb8c7-186">操作名称</span><span class="sxs-lookup"><span data-stu-id="bb8c7-186">Operation name</span></span> | <span data-ttu-id="bb8c7-187">最低协议版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-187">Minimum protocol version</span></span> | <span data-ttu-id="bb8c7-188">最小 NuGet 客户端版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="bb8c7-189">下载包</span><span class="sxs-lookup"><span data-stu-id="bb8c7-189">Download Package</span></span> | <span data-ttu-id="bb8c7-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="bb8c7-190">1.0.0</span></span> | <span data-ttu-id="bb8c7-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="bb8c7-191">4.3.0</span></span> |
| [<span data-ttu-id="bb8c7-192">身份验证</span><span class="sxs-lookup"><span data-stu-id="bb8c7-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="bb8c7-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="bb8c7-193">2.0.0</span></span> | <span data-ttu-id="bb8c7-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="bb8c7-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="bb8c7-195">在正确的运行时下运行插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="bb8c7-196">对于 dotnet 方案中的 NuGet，插件需要能够在 dotnet 的特定运行时执行。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="bb8c7-197">它在插件提供程序和使用者上，以确保使用兼容的 dotnet/插件组合。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="bb8c7-198">用户位置插件可能会出现问题，例如，2.0 运行时下的 dotnet 尝试使用为2.1 运行时编写的插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="bb8c7-199">功能缓存</span><span class="sxs-lookup"><span data-stu-id="bb8c7-199">Capabilities caching</span></span>

<span data-ttu-id="bb8c7-200">插件的安全验证和实例化成本高昂。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="bb8c7-201">类似于身份验证操作，下载操作的执行频率更高，但平均 NuGet 用户只可能具有身份验证插件。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="bb8c7-202">为了改进体验，NuGet 将缓存给定请求的操作声明。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="bb8c7-203">此缓存是每个插件，其中插件键是插件路径，此功能缓存的过期时间为30天。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="bb8c7-204">缓存位于 `%LocalAppData%/NuGet/plugins-cache` 中，并通过环境变量 `NUGET_PLUGINS_CACHE_PATH`进行重写。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="bb8c7-205">若要清除此[缓存](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，可以运行带有 `plugins-cache` 选项的局部变量命令。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="bb8c7-206">现在，`all` 局部变量 "选项也将删除插件缓存。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="bb8c7-207">协议消息索引</span><span class="sxs-lookup"><span data-stu-id="bb8c7-207">Protocol messages index</span></span>

<span data-ttu-id="bb8c7-208">协议版本*1.0.0*消息：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="bb8c7-209">关闭</span><span class="sxs-lookup"><span data-stu-id="bb8c7-209">Close</span></span>
    * <span data-ttu-id="bb8c7-210">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-211">请求不包含有效负载</span><span class="sxs-lookup"><span data-stu-id="bb8c7-211">The request will contain no payload</span></span>
    * <span data-ttu-id="bb8c7-212">不需要响应。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-212">No response is expected.</span></span>  <span data-ttu-id="bb8c7-213">适当的响应是为了使插件进程及时退出。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="bb8c7-214">复制包中的文件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-214">Copy files in package</span></span>
    * <span data-ttu-id="bb8c7-215">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-216">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-216">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-217">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-217">the package ID and version</span></span>
        * <span data-ttu-id="bb8c7-218">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-218">the package source repository location</span></span>
        * <span data-ttu-id="bb8c7-219">目标目录路径</span><span class="sxs-lookup"><span data-stu-id="bb8c7-219">destination directory path</span></span>
        * <span data-ttu-id="bb8c7-220">包中要复制到目标目录路径的文件的可枚举</span><span class="sxs-lookup"><span data-stu-id="bb8c7-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="bb8c7-221">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-221">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-222">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-223">如果操作成功，则为目标目录中复制的文件的完整路径的可枚举</span><span class="sxs-lookup"><span data-stu-id="bb8c7-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="bb8c7-224">复制包文件（. nupkg）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="bb8c7-225">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-226">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-226">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-227">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-227">the package ID and version</span></span>
        * <span data-ttu-id="bb8c7-228">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-228">the package source repository location</span></span>
        * <span data-ttu-id="bb8c7-229">目标文件路径</span><span class="sxs-lookup"><span data-stu-id="bb8c7-229">the destination file path</span></span>
    * <span data-ttu-id="bb8c7-230">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-230">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-231">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="bb8c7-232">获取凭据</span><span class="sxs-lookup"><span data-stu-id="bb8c7-232">Get credentials</span></span>
    * <span data-ttu-id="bb8c7-233">请求方向：插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="bb8c7-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="bb8c7-234">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-234">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-235">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-235">the package source repository location</span></span>
        * <span data-ttu-id="bb8c7-236">使用当前凭据从包源存储库获取的 HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="bb8c7-237">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-237">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-238">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-239">用户名（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-239">a username, if available</span></span>
        * <span data-ttu-id="bb8c7-240">密码（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-240">a password, if available</span></span>

5.  <span data-ttu-id="bb8c7-241">获取包中的文件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-241">Get files in package</span></span>
    * <span data-ttu-id="bb8c7-242">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-243">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-243">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-244">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-244">the package ID and version</span></span>
        * <span data-ttu-id="bb8c7-245">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-245">the package source repository location</span></span>
    * <span data-ttu-id="bb8c7-246">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-246">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-247">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-248">如果操作成功，则为包中的文件路径的可枚举</span><span class="sxs-lookup"><span data-stu-id="bb8c7-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="bb8c7-249">获取操作声明</span><span class="sxs-lookup"><span data-stu-id="bb8c7-249">Get operation claims</span></span> 
    * <span data-ttu-id="bb8c7-250">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-251">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-251">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-252">包源的服务索引 json</span><span class="sxs-lookup"><span data-stu-id="bb8c7-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="bb8c7-253">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-253">the package source repository location</span></span>
    * <span data-ttu-id="bb8c7-254">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-254">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-255">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-256">如果操作成功，则为支持的操作（如包下载）的可枚举。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="bb8c7-257">如果插件不支持包源，则该插件必须返回一组支持操作的空集。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="bb8c7-258">此消息已在版本*2.0.0*中更新。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="bb8c7-259">它在客户端上，用于保留向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="bb8c7-260">获取包哈希</span><span class="sxs-lookup"><span data-stu-id="bb8c7-260">Get package hash</span></span>
    * <span data-ttu-id="bb8c7-261">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-262">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-262">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-263">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-263">the package ID and version</span></span>
        * <span data-ttu-id="bb8c7-264">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-264">the package source repository location</span></span>
        * <span data-ttu-id="bb8c7-265">哈希算法</span><span class="sxs-lookup"><span data-stu-id="bb8c7-265">the hash algorithm</span></span>
    * <span data-ttu-id="bb8c7-266">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-266">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-267">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-268">如果操作成功，则使用所请求的哈希算法的包文件哈希</span><span class="sxs-lookup"><span data-stu-id="bb8c7-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="bb8c7-269">获取包的版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-269">Get package versions</span></span>
    * <span data-ttu-id="bb8c7-270">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-271">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-271">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-272">包 ID</span><span class="sxs-lookup"><span data-stu-id="bb8c7-272">the package ID</span></span>
        * <span data-ttu-id="bb8c7-273">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-273">the package source repository location</span></span>
    * <span data-ttu-id="bb8c7-274">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-274">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-275">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-276">如果操作成功，则为包版本的可枚举</span><span class="sxs-lookup"><span data-stu-id="bb8c7-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="bb8c7-277">获取服务索引</span><span class="sxs-lookup"><span data-stu-id="bb8c7-277">Get service index</span></span>
    * <span data-ttu-id="bb8c7-278">请求方向：插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="bb8c7-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="bb8c7-279">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-279">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-280">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-280">the package source repository location</span></span>
    * <span data-ttu-id="bb8c7-281">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-281">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-282">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-283">如果操作成功，则为服务索引</span><span class="sxs-lookup"><span data-stu-id="bb8c7-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="bb8c7-284">握手</span><span class="sxs-lookup"><span data-stu-id="bb8c7-284">Handshake</span></span>
     * <span data-ttu-id="bb8c7-285">请求方向： NuGet < > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="bb8c7-286">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-286">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-287">当前插件协议版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="bb8c7-288">支持的最低插件协议版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="bb8c7-289">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-289">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-290">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="bb8c7-291">如果操作成功，则协商协议版本。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="bb8c7-292">失败将导致插件终止。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="bb8c7-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="bb8c7-293">Initialize</span></span>
     * <span data-ttu-id="bb8c7-294">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="bb8c7-295">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-295">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-296">NuGet 客户端工具版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="bb8c7-297">NuGet 客户端工具的有效语言。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="bb8c7-298">如果使用，此操作将考虑 ForceEnglishOutput 设置。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="bb8c7-299">默认请求超时值，它取代协议默认值。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="bb8c7-300">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-300">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-301">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="bb8c7-302">失败将导致插件终止。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="bb8c7-303">日志</span><span class="sxs-lookup"><span data-stu-id="bb8c7-303">Log</span></span>
     * <span data-ttu-id="bb8c7-304">请求方向：插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="bb8c7-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="bb8c7-305">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-305">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-306">请求的日志级别</span><span class="sxs-lookup"><span data-stu-id="bb8c7-306">the log level for the request</span></span>
         * <span data-ttu-id="bb8c7-307">要记录的消息</span><span class="sxs-lookup"><span data-stu-id="bb8c7-307">a message to log</span></span>
     * <span data-ttu-id="bb8c7-308">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-308">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-309">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="bb8c7-310">监视 NuGet 进程退出</span><span class="sxs-lookup"><span data-stu-id="bb8c7-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="bb8c7-311">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="bb8c7-312">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-312">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-313">NuGet 进程 ID</span><span class="sxs-lookup"><span data-stu-id="bb8c7-313">the NuGet process ID</span></span>
     * <span data-ttu-id="bb8c7-314">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-314">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-315">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="bb8c7-316">预提取包</span><span class="sxs-lookup"><span data-stu-id="bb8c7-316">Prefetch package</span></span>
     * <span data-ttu-id="bb8c7-317">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="bb8c7-318">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-318">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-319">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="bb8c7-319">the package ID and version</span></span>
         * <span data-ttu-id="bb8c7-320">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-320">the package source repository location</span></span>
     * <span data-ttu-id="bb8c7-321">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-321">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-322">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="bb8c7-323">设置凭据</span><span class="sxs-lookup"><span data-stu-id="bb8c7-323">Set credentials</span></span>
     * <span data-ttu-id="bb8c7-324">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="bb8c7-325">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-325">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-326">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-326">the package source repository location</span></span>
         * <span data-ttu-id="bb8c7-327">最后一个已知包源用户名（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="bb8c7-328">最后一个已知包源密码（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="bb8c7-329">最后一个已知代理用户名（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="bb8c7-330">最后一个已知代理密码（如果可用）</span><span class="sxs-lookup"><span data-stu-id="bb8c7-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="bb8c7-331">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-331">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-332">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="bb8c7-333">设置日志级别</span><span class="sxs-lookup"><span data-stu-id="bb8c7-333">Set log level</span></span>
     * <span data-ttu-id="bb8c7-334">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="bb8c7-335">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-335">The request will contain:</span></span>
         * <span data-ttu-id="bb8c7-336">默认日志级别</span><span class="sxs-lookup"><span data-stu-id="bb8c7-336">the default log level</span></span>
     * <span data-ttu-id="bb8c7-337">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-337">A response will contain:</span></span>
         * <span data-ttu-id="bb8c7-338">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="bb8c7-339">协议版本*2.0.0*消息</span><span class="sxs-lookup"><span data-stu-id="bb8c7-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="bb8c7-340">获取操作声明</span><span class="sxs-lookup"><span data-stu-id="bb8c7-340">Get Operation Claims</span></span>

* <span data-ttu-id="bb8c7-341">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="bb8c7-342">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-342">The request will contain:</span></span>
        * <span data-ttu-id="bb8c7-343">包源的服务索引 json</span><span class="sxs-lookup"><span data-stu-id="bb8c7-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="bb8c7-344">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="bb8c7-344">the package source repository location</span></span>
    * <span data-ttu-id="bb8c7-345">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-345">A response will contain:</span></span>
        * <span data-ttu-id="bb8c7-346">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="bb8c7-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="bb8c7-347">如果操作成功，则为支持的操作的可枚举。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="bb8c7-348">如果插件不支持包源，则该插件必须返回一组支持操作的空集。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="bb8c7-349">如果服务索引和包源为 null，则该插件可以通过身份验证进行应答。</span><span class="sxs-lookup"><span data-stu-id="bb8c7-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="bb8c7-350">获取身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="bb8c7-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="bb8c7-351">请求方向： NuGet > 插件</span><span class="sxs-lookup"><span data-stu-id="bb8c7-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="bb8c7-352">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="bb8c7-352">The request will contain:</span></span>
    * <span data-ttu-id="bb8c7-353">URI</span><span class="sxs-lookup"><span data-stu-id="bb8c7-353">Uri</span></span>
    * <span data-ttu-id="bb8c7-354">isRetry</span><span class="sxs-lookup"><span data-stu-id="bb8c7-354">isRetry</span></span>
    * <span data-ttu-id="bb8c7-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bb8c7-355">NonInteractive</span></span>
    * <span data-ttu-id="bb8c7-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="bb8c7-356">CanShowDialog</span></span>
* <span data-ttu-id="bb8c7-357">响应将包含</span><span class="sxs-lookup"><span data-stu-id="bb8c7-357">A response will contain</span></span>
    * <span data-ttu-id="bb8c7-358">用户名</span><span class="sxs-lookup"><span data-stu-id="bb8c7-358">Username</span></span>
    * <span data-ttu-id="bb8c7-359">Password</span><span class="sxs-lookup"><span data-stu-id="bb8c7-359">Password</span></span>
    * <span data-ttu-id="bb8c7-360">Message</span><span class="sxs-lookup"><span data-stu-id="bb8c7-360">Message</span></span>
    * <span data-ttu-id="bb8c7-361">身份验证类型列表</span><span class="sxs-lookup"><span data-stu-id="bb8c7-361">List of Auth Types</span></span>
    * <span data-ttu-id="bb8c7-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="bb8c7-362">MessageResponseCode</span></span>
