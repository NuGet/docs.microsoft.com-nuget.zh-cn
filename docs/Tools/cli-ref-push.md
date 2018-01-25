---
title: "NuGet CLI 推送命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 推送命令参考"
keywords: "nuget 推送引用，推送命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 50883bc85ab96cba54fb4ce0bd344e8148c4fab1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="fbf90-104">推送命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fbf90-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="fbf90-105">**适用于：**包发布&bullet;**受支持的版本：**所有; 4.1.0+ nuget.org 的必要条件</span><span class="sxs-lookup"><span data-stu-id="fbf90-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="fbf90-106">若要将包推送到 nuget.org 必须使用 nuget.exe v4.1.0 +，并实现所需[NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="fbf90-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="fbf90-107">推送到包源的包，将其发布。</span><span class="sxs-lookup"><span data-stu-id="fbf90-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="fbf90-108">NuGet 的默认配置通过加载获取`%AppData%\NuGet\NuGet.Config`，然后加载任何`Nuget.Config`或`.nuget\Nuget.Config`文件从驱动器的根目录开始和结束当前目录中 (请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="fbf90-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="fbf90-109">用法</span><span class="sxs-lookup"><span data-stu-id="fbf90-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="fbf90-110">其中`<packagePath>`标识要将推送到服务器的包。</span><span class="sxs-lookup"><span data-stu-id="fbf90-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="fbf90-111">选项</span><span class="sxs-lookup"><span data-stu-id="fbf90-111">Options</span></span>

| <span data-ttu-id="fbf90-112">选项</span><span class="sxs-lookup"><span data-stu-id="fbf90-112">Option</span></span> | <span data-ttu-id="fbf90-113">描述</span><span class="sxs-lookup"><span data-stu-id="fbf90-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fbf90-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="fbf90-114">ApiKey</span></span> | <span data-ttu-id="fbf90-115">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="fbf90-115">The API key for the target repository.</span></span> <span data-ttu-id="fbf90-116">如果不存在，请在指定某一*%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="fbf90-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fbf90-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fbf90-117">ConfigFile</span></span> | <span data-ttu-id="fbf90-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="fbf90-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fbf90-119">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="fbf90-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fbf90-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="fbf90-120">DisableBuffering</span></span> | <span data-ttu-id="fbf90-121">禁用时将推送到的 http （s） 服务器以减少内存使用情况进行缓冲。</span><span class="sxs-lookup"><span data-stu-id="fbf90-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="fbf90-122">注意： 当使用此选项时，集成的 Windows 身份验证可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="fbf90-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="fbf90-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fbf90-123">ForceEnglishOutput</span></span> | <span data-ttu-id="fbf90-124">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="fbf90-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fbf90-125">帮助</span><span class="sxs-lookup"><span data-stu-id="fbf90-125">Help</span></span> | <span data-ttu-id="fbf90-126">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="fbf90-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="fbf90-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fbf90-127">NonInteractive</span></span> | <span data-ttu-id="fbf90-128">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="fbf90-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fbf90-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="fbf90-129">NoSymbols</span></span> | <span data-ttu-id="fbf90-130">*（3.5 +)*如果符号包存在，它将不会推送到符号服务器。</span><span class="sxs-lookup"><span data-stu-id="fbf90-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="fbf90-131">源</span><span class="sxs-lookup"><span data-stu-id="fbf90-131">Source</span></span> | <span data-ttu-id="fbf90-132">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="fbf90-132">Specifies the server URL.</span></span> <span data-ttu-id="fbf90-133">NuGet 标识的 UNC 或本地文件夹源，并只需将复制文件而不是将它使用 HTTP 推送。</span><span class="sxs-lookup"><span data-stu-id="fbf90-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="fbf90-134">此外，从开始 NuGet 上面 3.4.2，这是强制参数除非`NuGet.Config`文件指定*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../Consume-Packages/Configuring-NuGet-Behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="fbf90-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="fbf90-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="fbf90-135">SymbolSource</span></span> | <span data-ttu-id="fbf90-136">*（3.5 +)*指定符号服务器 URL; 推送到 nuget.org 时使用 nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="fbf90-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="fbf90-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="fbf90-137">SymbolApiKey</span></span> | <span data-ttu-id="fbf90-138">*（3.5 +)*中指定的 URL 指定的 API 密钥`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="fbf90-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="fbf90-139">超时</span><span class="sxs-lookup"><span data-stu-id="fbf90-139">Timeout</span></span> | <span data-ttu-id="fbf90-140">指定超时，以秒为单位，以便将推送到服务器。</span><span class="sxs-lookup"><span data-stu-id="fbf90-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="fbf90-141">默认值为 300 秒 （5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="fbf90-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="fbf90-142">详细级别</span><span class="sxs-lookup"><span data-stu-id="fbf90-142">Verbosity</span></span> | <span data-ttu-id="fbf90-143">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="fbf90-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fbf90-144">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fbf90-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fbf90-145">示例</span><span class="sxs-lookup"><span data-stu-id="fbf90-145">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
