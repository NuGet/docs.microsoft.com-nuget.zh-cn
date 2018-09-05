---
title: 跨平台插件的 NuGet
description: NuGet 的 NuGet.exe、 dotnet.exe、 msbuild.exe 和 Visual Studio 跨平台插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548201"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="4c12f-103">跨平台插件的 NuGet</span><span class="sxs-lookup"><span data-stu-id="4c12f-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="4c12f-104">在 NuGet 4.8 + 中添加了对跨平台插件的支持。</span><span class="sxs-lookup"><span data-stu-id="4c12f-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="4c12f-105">这是通过生成新的插件可扩展性模型，必须符合一组严格的规则的操作的使用来实现。</span><span class="sxs-lookup"><span data-stu-id="4c12f-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="4c12f-106">插件是自包含的可执行文件 （可运行对象在.NET Core 世界中），NuGet 客户端在一个单独的进程中启动。</span><span class="sxs-lookup"><span data-stu-id="4c12f-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="4c12f-107">这是 true 一次编写，随处运行插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="4c12f-108">它会使用所有 NuGet 客户端工具。</span><span class="sxs-lookup"><span data-stu-id="4c12f-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="4c12f-109">插件可以是.NET Framework （NuGet.exe、 MSBuild.exe 和 Visual Studio） 或.NET Core (dotnet.exe)。</span><span class="sxs-lookup"><span data-stu-id="4c12f-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="4c12f-110">NuGet 客户端和插件之间的版本控制的通信协议定义。</span><span class="sxs-lookup"><span data-stu-id="4c12f-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="4c12f-111">启动握手期间 2 进程协商的协议版本。</span><span class="sxs-lookup"><span data-stu-id="4c12f-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="4c12f-112">要覆盖所有 NuGet 客户端工具方案，其中一个需要.NET Framework 和.NET 核心插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="4c12f-113">下面介绍了插件的客户端/框架组合。</span><span class="sxs-lookup"><span data-stu-id="4c12f-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="4c12f-114">客户端工具</span><span class="sxs-lookup"><span data-stu-id="4c12f-114">Client tool</span></span>  | <span data-ttu-id="4c12f-115">框架</span><span class="sxs-lookup"><span data-stu-id="4c12f-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="4c12f-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4c12f-116">Visual Studio</span></span> | <span data-ttu-id="4c12f-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c12f-117">.NET Framework</span></span> |
| <span data-ttu-id="4c12f-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="4c12f-118">dotnet.exe</span></span> | <span data-ttu-id="4c12f-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4c12f-119">.NET Core</span></span> |
| <span data-ttu-id="4c12f-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="4c12f-120">NuGet.exe</span></span> | <span data-ttu-id="4c12f-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c12f-121">.NET Framework</span></span> |
| <span data-ttu-id="4c12f-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="4c12f-122">MSBuild.exe</span></span> | <span data-ttu-id="4c12f-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c12f-123">.NET Framework</span></span> |
| <span data-ttu-id="4c12f-124">Mono 上的 NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="4c12f-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="4c12f-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c12f-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="4c12f-126">它是如何工作的</span><span class="sxs-lookup"><span data-stu-id="4c12f-126">How does it work</span></span>

<span data-ttu-id="4c12f-127">高级工作流如下所述：</span><span class="sxs-lookup"><span data-stu-id="4c12f-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="4c12f-128">NuGet 发现可用插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="4c12f-129">如果适用，NuGet 将循环访问的优先级顺序并开始逐个进行中的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="4c12f-130">NuGet 将使用第一个插件，可以处理该请求。</span><span class="sxs-lookup"><span data-stu-id="4c12f-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="4c12f-131">在不再需要时，将关闭插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="4c12f-132">常规插件要求</span><span class="sxs-lookup"><span data-stu-id="4c12f-132">General plugin requirements</span></span>

<span data-ttu-id="4c12f-133">当前的协议版本是*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="4c12f-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="4c12f-134">在此版本中，要求如下所示：</span><span class="sxs-lookup"><span data-stu-id="4c12f-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="4c12f-135">具有有效的、 受信任的验证码签名程序集将在 Windows 和 Mono 上运行。</span><span class="sxs-lookup"><span data-stu-id="4c12f-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="4c12f-136">没有任何特殊信任要求尚未运行 Linux 和 Mac 上的程序集。</span><span class="sxs-lookup"><span data-stu-id="4c12f-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="4c12f-137">相关的问题</span><span class="sxs-lookup"><span data-stu-id="4c12f-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="4c12f-138">支持的 NuGet 客户端工具的当前安全上下文的无状态启动。</span><span class="sxs-lookup"><span data-stu-id="4c12f-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="4c12f-139">例如，NuGet 客户端工具将执行提升或更高版本所述的插件协议之外的其他初始化。</span><span class="sxs-lookup"><span data-stu-id="4c12f-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="4c12f-140">除非显式指定，则为非交互式。</span><span class="sxs-lookup"><span data-stu-id="4c12f-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="4c12f-141">遵守协商的插件协议版本。</span><span class="sxs-lookup"><span data-stu-id="4c12f-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="4c12f-142">在合理时间段内响应的所有请求。</span><span class="sxs-lookup"><span data-stu-id="4c12f-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="4c12f-143">接受任何正在进行中操作的取消请求。</span><span class="sxs-lookup"><span data-stu-id="4c12f-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="4c12f-144">技术规范都进行了以下规范中的更多详细信息：</span><span class="sxs-lookup"><span data-stu-id="4c12f-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="4c12f-145">NuGet 包下载插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="4c12f-146">跨平台身份验证插件的 NuGet</span><span class="sxs-lookup"><span data-stu-id="4c12f-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="4c12f-147">客户端-插件交互</span><span class="sxs-lookup"><span data-stu-id="4c12f-147">Client - Plugin interaction</span></span>

<span data-ttu-id="4c12f-148">NuGet 客户端工具和插件通过进行通信使用 JSON 标准流 （stdin、 stdout、 stderr）。</span><span class="sxs-lookup"><span data-stu-id="4c12f-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="4c12f-149">所有数据必须都是 utf-8 编码。</span><span class="sxs-lookup"><span data-stu-id="4c12f-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="4c12f-150">插件启动具有参数"的插件"。</span><span class="sxs-lookup"><span data-stu-id="4c12f-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="4c12f-151">如果用户直接启动可执行文件而不使用此参数的插件，该插件可以提供信息性消息而不是等待协议握手。</span><span class="sxs-lookup"><span data-stu-id="4c12f-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="4c12f-152">协议握手超时值为 5 秒。</span><span class="sxs-lookup"><span data-stu-id="4c12f-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="4c12f-153">插件应完成作为缺乏尽可能的金额中设置。</span><span class="sxs-lookup"><span data-stu-id="4c12f-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="4c12f-154">NuGet 客户端工具将通过传入的 NuGet 源的服务索引查询插件的支持的操作。</span><span class="sxs-lookup"><span data-stu-id="4c12f-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="4c12f-155">插件可能使用的服务索引检查支持的服务类型存在。</span><span class="sxs-lookup"><span data-stu-id="4c12f-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="4c12f-156">NuGet 客户端工具和插件之间的通信是双向的。</span><span class="sxs-lookup"><span data-stu-id="4c12f-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="4c12f-157">每个请求已超时设置为 5 秒。</span><span class="sxs-lookup"><span data-stu-id="4c12f-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="4c12f-158">如果需要更长时间操作都认为各自的进程应发送进度消息以防止请求超时。处于非活动状态的 1 分钟之后插件被视为空闲和关闭的情况下。</span><span class="sxs-lookup"><span data-stu-id="4c12f-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="4c12f-159">插件安装和发现</span><span class="sxs-lookup"><span data-stu-id="4c12f-159">Plugin installation and discovery</span></span>

<span data-ttu-id="4c12f-160">插件会发现通过基于约定的目录结构。</span><span class="sxs-lookup"><span data-stu-id="4c12f-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="4c12f-161">CI/CD 方案和高级用户可以使用环境变量重写的行为。</span><span class="sxs-lookup"><span data-stu-id="4c12f-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="4c12f-162">`NUGET_PLUGIN_PATHS` -定义将用于该 NuGet 过程中，保留的优先级的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="4c12f-163">如果设置此环境变量，它将替代约定，其发现。</span><span class="sxs-lookup"><span data-stu-id="4c12f-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="4c12f-164">用户位置、 中的 NuGet 主页位置`%UserProfile%/.nuget/plugins`。</span><span class="sxs-lookup"><span data-stu-id="4c12f-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="4c12f-165">此位置不能重写。</span><span class="sxs-lookup"><span data-stu-id="4c12f-165">This location cannot be overriden.</span></span> <span data-ttu-id="4c12f-166">不同的根目录将用于.NET Core 和.NET Framework 的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="4c12f-167">框架</span><span class="sxs-lookup"><span data-stu-id="4c12f-167">Framework</span></span> | <span data-ttu-id="4c12f-168">根发现位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="4c12f-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4c12f-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="4c12f-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c12f-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="4c12f-171">应在其自己的文件夹中安装的每个插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="4c12f-172">插件的入口点将是使用.NET Core 的.dll 扩展和.exe 适用于.NET Framework 的扩展的安装文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="4c12f-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="4c12f-173">目前存在的插件安装没有用户情景。</span><span class="sxs-lookup"><span data-stu-id="4c12f-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="4c12f-174">它是将所需的文件移动到预先确定的位置一样简单。</span><span class="sxs-lookup"><span data-stu-id="4c12f-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="4c12f-175">支持的操作</span><span class="sxs-lookup"><span data-stu-id="4c12f-175">Supported operations</span></span>

<span data-ttu-id="4c12f-176">在新的插件协议下支持两个操作。</span><span class="sxs-lookup"><span data-stu-id="4c12f-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="4c12f-177">操作名称</span><span class="sxs-lookup"><span data-stu-id="4c12f-177">Operation name</span></span> | <span data-ttu-id="4c12f-178">最低协议版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-178">Minimum protocol version</span></span> | <span data-ttu-id="4c12f-179">最低 NuGet 客户端版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="4c12f-180">下载包</span><span class="sxs-lookup"><span data-stu-id="4c12f-180">Download Package</span></span> | <span data-ttu-id="4c12f-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4c12f-181">1.0.0</span></span> | <span data-ttu-id="4c12f-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="4c12f-182">4.3.0</span></span> |
| [<span data-ttu-id="4c12f-183">身份验证</span><span class="sxs-lookup"><span data-stu-id="4c12f-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="4c12f-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="4c12f-184">2.0.0</span></span> | <span data-ttu-id="4c12f-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="4c12f-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="4c12f-186">运行插件下正确运行时</span><span class="sxs-lookup"><span data-stu-id="4c12f-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="4c12f-187">适用于 NuGet dotnet.exe 方案中，插件需要能够执行的 dotnet.exe 该特定运行时。</span><span class="sxs-lookup"><span data-stu-id="4c12f-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="4c12f-188">它是插件提供商和使用者，以确保兼容 dotnet.exe/plugin 结合使用。</span><span class="sxs-lookup"><span data-stu-id="4c12f-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="4c12f-189">使用用户位置插件时例如时出现潜在问题，dotnet.exe 下 2.0 运行时尝试使用针对 2.1 运行时编写的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="4c12f-190">缓存的功能</span><span class="sxs-lookup"><span data-stu-id="4c12f-190">Capabilities caching</span></span>

<span data-ttu-id="4c12f-191">安全验证和实例化的插件是代价高昂。</span><span class="sxs-lookup"><span data-stu-id="4c12f-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="4c12f-192">但是一般 NuGet 用户才可能具有一个身份验证插件，下载操作比身份验证操作，更频繁地发生。</span><span class="sxs-lookup"><span data-stu-id="4c12f-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="4c12f-193">若要改进的体验，NuGet 将缓存给定请求的操作声明。</span><span class="sxs-lookup"><span data-stu-id="4c12f-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="4c12f-194">此缓存是每个插件使用的插件路径中，插件键，此功能缓存的到期时间为 30 天。</span><span class="sxs-lookup"><span data-stu-id="4c12f-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="4c12f-195">缓存位于`%LocalAppData%/NuGet/plugins-cache`和环境变量替代`NUGET_PLUGINS_CACHE_PATH`。</span><span class="sxs-lookup"><span data-stu-id="4c12f-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="4c12f-196">若要清除这[缓存](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，其中一个可以运行局部变量命令和`plugins-cache`选项。</span><span class="sxs-lookup"><span data-stu-id="4c12f-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="4c12f-197">`all`局部变量选项也会立即删除插件缓存。</span><span class="sxs-lookup"><span data-stu-id="4c12f-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="4c12f-198">协议消息索引</span><span class="sxs-lookup"><span data-stu-id="4c12f-198">Protocol messages index</span></span>

<span data-ttu-id="4c12f-199">协议版本*1.0.0*消息：</span><span class="sxs-lookup"><span data-stu-id="4c12f-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="4c12f-200">关闭</span><span class="sxs-lookup"><span data-stu-id="4c12f-200">Close</span></span>
    * <span data-ttu-id="4c12f-201">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-202">该请求将包含无有效负载</span><span class="sxs-lookup"><span data-stu-id="4c12f-202">The request will contain no payload</span></span>
    * <span data-ttu-id="4c12f-203">预期无响应。</span><span class="sxs-lookup"><span data-stu-id="4c12f-203">No response is expected.</span></span>  <span data-ttu-id="4c12f-204">正确的响应是插件进程立即退出。</span><span class="sxs-lookup"><span data-stu-id="4c12f-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="4c12f-205">将包中复制文件</span><span class="sxs-lookup"><span data-stu-id="4c12f-205">Copy files in package</span></span>
    * <span data-ttu-id="4c12f-206">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-207">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-207">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-208">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-208">the package ID and version</span></span>
        * <span data-ttu-id="4c12f-209">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-209">the package source repository location</span></span>
        * <span data-ttu-id="4c12f-210">目标目录路径</span><span class="sxs-lookup"><span data-stu-id="4c12f-210">destination directory path</span></span>
        * <span data-ttu-id="4c12f-211">可枚举的包复制到目标目录路径中的文件</span><span class="sxs-lookup"><span data-stu-id="4c12f-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="4c12f-212">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-212">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-213">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-214">如果操作成功的目标目录中复制文件的完整路径的可枚举值</span><span class="sxs-lookup"><span data-stu-id="4c12f-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="4c12f-215">将包文件 (.nupkg) 复制</span><span class="sxs-lookup"><span data-stu-id="4c12f-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="4c12f-216">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-217">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-217">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-218">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-218">the package ID and version</span></span>
        * <span data-ttu-id="4c12f-219">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-219">the package source repository location</span></span>
        * <span data-ttu-id="4c12f-220">目标文件路径</span><span class="sxs-lookup"><span data-stu-id="4c12f-220">the destination file path</span></span>
    * <span data-ttu-id="4c12f-221">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-221">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-222">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="4c12f-223">获取凭据</span><span class="sxs-lookup"><span data-stu-id="4c12f-223">Get credentials</span></span>
    * <span data-ttu-id="4c12f-224">请求方向： 插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="4c12f-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="4c12f-225">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-225">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-226">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-226">the package source repository location</span></span>
        * <span data-ttu-id="4c12f-227">从包源存储库使用当前凭据获取 HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="4c12f-228">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-228">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-229">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-230">用户名，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-230">a username, if available</span></span>
        * <span data-ttu-id="4c12f-231">密码，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-231">a password, if available</span></span>

5.  <span data-ttu-id="4c12f-232">获取包中的文件</span><span class="sxs-lookup"><span data-stu-id="4c12f-232">Get files in package</span></span>
    * <span data-ttu-id="4c12f-233">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-234">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-234">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-235">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-235">the package ID and version</span></span>
        * <span data-ttu-id="4c12f-236">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-236">the package source repository location</span></span>
    * <span data-ttu-id="4c12f-237">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-237">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-238">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-239">如果操作已成功在包中的文件路径的可枚举值</span><span class="sxs-lookup"><span data-stu-id="4c12f-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="4c12f-240">获取操作声明</span><span class="sxs-lookup"><span data-stu-id="4c12f-240">Get operation claims</span></span> 
    * <span data-ttu-id="4c12f-241">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-242">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-242">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-243">包源服务 index.json</span><span class="sxs-lookup"><span data-stu-id="4c12f-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="4c12f-244">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-244">the package source repository location</span></span>
    * <span data-ttu-id="4c12f-245">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-245">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-246">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-247">可枚举的支持的操作 (例如： 包下载) 如果操作成功。</span><span class="sxs-lookup"><span data-stu-id="4c12f-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="4c12f-248">如果提供的插件不支持包源，该插件必须返回空集支持的操作。</span><span class="sxs-lookup"><span data-stu-id="4c12f-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="4c12f-249">此消息已更新版本中*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="4c12f-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="4c12f-250">它是在客户端可以保持向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="4c12f-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="4c12f-251">获取包哈希</span><span class="sxs-lookup"><span data-stu-id="4c12f-251">Get package hash</span></span>
    * <span data-ttu-id="4c12f-252">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-253">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-253">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-254">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-254">the package ID and version</span></span>
        * <span data-ttu-id="4c12f-255">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-255">the package source repository location</span></span>
        * <span data-ttu-id="4c12f-256">哈希算法</span><span class="sxs-lookup"><span data-stu-id="4c12f-256">the hash algorithm</span></span>
    * <span data-ttu-id="4c12f-257">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-257">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-258">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-259">包文件哈希使用请求的哈希算法，如果操作成功</span><span class="sxs-lookup"><span data-stu-id="4c12f-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="4c12f-260">获取包的版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-260">Get package versions</span></span>
    * <span data-ttu-id="4c12f-261">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-262">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-262">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-263">包 ID</span><span class="sxs-lookup"><span data-stu-id="4c12f-263">the package ID</span></span>
        * <span data-ttu-id="4c12f-264">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-264">the package source repository location</span></span>
    * <span data-ttu-id="4c12f-265">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-265">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-266">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-267">可枚举的包版本，如果操作成功</span><span class="sxs-lookup"><span data-stu-id="4c12f-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="4c12f-268">获取服务索引</span><span class="sxs-lookup"><span data-stu-id="4c12f-268">Get service index</span></span>
    * <span data-ttu-id="4c12f-269">请求方向： 插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="4c12f-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="4c12f-270">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-270">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-271">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-271">the package source repository location</span></span>
    * <span data-ttu-id="4c12f-272">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-272">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-273">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-274">服务索引，如果操作成功</span><span class="sxs-lookup"><span data-stu-id="4c12f-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="4c12f-275">握手</span><span class="sxs-lookup"><span data-stu-id="4c12f-275">Handshake</span></span>
     * <span data-ttu-id="4c12f-276">请求方向： NuGet <>-插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="4c12f-277">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-277">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-278">当前的插件协议版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="4c12f-279">支持的最低插件协议版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="4c12f-280">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-280">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-281">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="4c12f-282">如果操作成功协商的协议的版本。</span><span class="sxs-lookup"><span data-stu-id="4c12f-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="4c12f-283">失败将导致终止的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="4c12f-284">初始化</span><span class="sxs-lookup"><span data-stu-id="4c12f-284">Initialize</span></span>
     * <span data-ttu-id="4c12f-285">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4c12f-286">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-286">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-287">NuGet 客户端工具版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="4c12f-288">NuGet 客户端工具有效语言。</span><span class="sxs-lookup"><span data-stu-id="4c12f-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="4c12f-289">这将考虑 ForceEnglishOutput 设置中，如果使用。</span><span class="sxs-lookup"><span data-stu-id="4c12f-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="4c12f-290">默认请求超时，取代了协议的默认值。</span><span class="sxs-lookup"><span data-stu-id="4c12f-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="4c12f-291">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-291">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-292">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="4c12f-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="4c12f-293">失败将导致终止的插件。</span><span class="sxs-lookup"><span data-stu-id="4c12f-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="4c12f-294">日志</span><span class="sxs-lookup"><span data-stu-id="4c12f-294">Log</span></span>
     * <span data-ttu-id="4c12f-295">请求方向： 插件-> NuGet</span><span class="sxs-lookup"><span data-stu-id="4c12f-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="4c12f-296">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-296">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-297">请求日志级别</span><span class="sxs-lookup"><span data-stu-id="4c12f-297">the log level for the request</span></span>
         * <span data-ttu-id="4c12f-298">要记录的消息</span><span class="sxs-lookup"><span data-stu-id="4c12f-298">a message to log</span></span>
     * <span data-ttu-id="4c12f-299">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-299">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-300">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="4c12f-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="4c12f-301">监视 NuGet 进程退出</span><span class="sxs-lookup"><span data-stu-id="4c12f-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="4c12f-302">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4c12f-303">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-303">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-304">NuGet 进程 ID</span><span class="sxs-lookup"><span data-stu-id="4c12f-304">the NuGet process ID</span></span>
     * <span data-ttu-id="4c12f-305">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-305">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-306">指示操作结果的响应代码。</span><span class="sxs-lookup"><span data-stu-id="4c12f-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="4c12f-307">预提取的包</span><span class="sxs-lookup"><span data-stu-id="4c12f-307">Prefetch package</span></span>
     * <span data-ttu-id="4c12f-308">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4c12f-309">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-309">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-310">包 ID 和版本</span><span class="sxs-lookup"><span data-stu-id="4c12f-310">the package ID and version</span></span>
         * <span data-ttu-id="4c12f-311">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-311">the package source repository location</span></span>
     * <span data-ttu-id="4c12f-312">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-312">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-313">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="4c12f-314">设置凭据</span><span class="sxs-lookup"><span data-stu-id="4c12f-314">Set credentials</span></span>
     * <span data-ttu-id="4c12f-315">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4c12f-316">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-316">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-317">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-317">the package source repository location</span></span>
         * <span data-ttu-id="4c12f-318">最后一个已知的包源用户名，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="4c12f-319">最后一个已知的包源密码，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="4c12f-320">最后一个已知的代理用户名，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="4c12f-321">最后一个已知的代理密码，如果可用</span><span class="sxs-lookup"><span data-stu-id="4c12f-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="4c12f-322">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-322">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-323">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="4c12f-324">将日志级别设置</span><span class="sxs-lookup"><span data-stu-id="4c12f-324">Set log level</span></span>
     * <span data-ttu-id="4c12f-325">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4c12f-326">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-326">The request will contain:</span></span>
         * <span data-ttu-id="4c12f-327">默认日志级别</span><span class="sxs-lookup"><span data-stu-id="4c12f-327">the default log level</span></span>
     * <span data-ttu-id="4c12f-328">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-328">A response will contain:</span></span>
         * <span data-ttu-id="4c12f-329">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="4c12f-330">协议版本*2.0.0*消息</span><span class="sxs-lookup"><span data-stu-id="4c12f-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="4c12f-331">获取操作声明</span><span class="sxs-lookup"><span data-stu-id="4c12f-331">Get Operation Claims</span></span>

* <span data-ttu-id="4c12f-332">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4c12f-333">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-333">The request will contain:</span></span>
        * <span data-ttu-id="4c12f-334">包源服务 index.json</span><span class="sxs-lookup"><span data-stu-id="4c12f-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="4c12f-335">包源存储库位置</span><span class="sxs-lookup"><span data-stu-id="4c12f-335">the package source repository location</span></span>
    * <span data-ttu-id="4c12f-336">响应将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-336">A response will contain:</span></span>
        * <span data-ttu-id="4c12f-337">指示操作结果的响应代码</span><span class="sxs-lookup"><span data-stu-id="4c12f-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4c12f-338">可枚举的支持的操作如果操作成功。</span><span class="sxs-lookup"><span data-stu-id="4c12f-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="4c12f-339">如果提供的插件不支持包源，该插件必须返回空集支持的操作。</span><span class="sxs-lookup"><span data-stu-id="4c12f-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="4c12f-340">如果服务索引和包源为 null，则该插件可以回答与身份验证。</span><span class="sxs-lookup"><span data-stu-id="4c12f-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="4c12f-341">获取身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="4c12f-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="4c12f-342">请求方向： NuGet-> 插件</span><span class="sxs-lookup"><span data-stu-id="4c12f-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="4c12f-343">该请求将包含：</span><span class="sxs-lookup"><span data-stu-id="4c12f-343">The request will contain:</span></span>
    * <span data-ttu-id="4c12f-344">URI</span><span class="sxs-lookup"><span data-stu-id="4c12f-344">Uri</span></span>
    * <span data-ttu-id="4c12f-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="4c12f-345">isRetry</span></span>
    * <span data-ttu-id="4c12f-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4c12f-346">NonInteractive</span></span>
    * <span data-ttu-id="4c12f-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="4c12f-347">CanShowDialog</span></span>
* <span data-ttu-id="4c12f-348">响应将包含</span><span class="sxs-lookup"><span data-stu-id="4c12f-348">A response will contain</span></span>
    * <span data-ttu-id="4c12f-349">用户名</span><span class="sxs-lookup"><span data-stu-id="4c12f-349">Username</span></span>
    * <span data-ttu-id="4c12f-350">Password</span><span class="sxs-lookup"><span data-stu-id="4c12f-350">Password</span></span>
    * <span data-ttu-id="4c12f-351">消息</span><span class="sxs-lookup"><span data-stu-id="4c12f-351">Message</span></span>
    * <span data-ttu-id="4c12f-352">身份验证类型的列表</span><span class="sxs-lookup"><span data-stu-id="4c12f-352">List of Auth Types</span></span>
    * <span data-ttu-id="4c12f-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="4c12f-353">MessageResponseCode</span></span>