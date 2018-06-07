---
title: NuGet CLI 推送命令
description: Nuget.exe 推送命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817186"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="86bb7-103">推送命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="86bb7-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="86bb7-104">**适用于：** 包发布&bullet;**受支持的版本：** 所有; 4.1.0+ nuget.org 的必要条件</span><span class="sxs-lookup"><span data-stu-id="86bb7-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="86bb7-105">若要将包推送到 nuget.org 必须使用 nuget.exe v4.1.0 +，并实现所需[NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="86bb7-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="86bb7-106">推送到包源的包，将其发布。</span><span class="sxs-lookup"><span data-stu-id="86bb7-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="86bb7-107">NuGet 的默认配置通过加载获取`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然后加载任何`Nuget.Config`或`.nuget\Nuget.Config`文件从驱动器的根目录开始和结束当前目录中 (请参阅[配置NuGet 行为](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="86bb7-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="86bb7-108">用法</span><span class="sxs-lookup"><span data-stu-id="86bb7-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="86bb7-109">其中`<packagePath>`标识要将推送到服务器的包。</span><span class="sxs-lookup"><span data-stu-id="86bb7-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="86bb7-110">选项</span><span class="sxs-lookup"><span data-stu-id="86bb7-110">Options</span></span>

| <span data-ttu-id="86bb7-111">选项</span><span class="sxs-lookup"><span data-stu-id="86bb7-111">Option</span></span> | <span data-ttu-id="86bb7-112">描述</span><span class="sxs-lookup"><span data-stu-id="86bb7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86bb7-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="86bb7-113">ApiKey</span></span> | <span data-ttu-id="86bb7-114">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="86bb7-114">The API key for the target repository.</span></span> <span data-ttu-id="86bb7-115">如果不存在，则使用在配置文件中指定。</span><span class="sxs-lookup"><span data-stu-id="86bb7-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="86bb7-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="86bb7-116">ConfigFile</span></span> | <span data-ttu-id="86bb7-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="86bb7-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="86bb7-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="86bb7-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="86bb7-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="86bb7-119">DisableBuffering</span></span> | <span data-ttu-id="86bb7-120">禁用时将推送到的 http （s） 服务器以减少内存使用情况进行缓冲。</span><span class="sxs-lookup"><span data-stu-id="86bb7-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="86bb7-121">注意： 当使用此选项时，集成的 Windows 身份验证可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="86bb7-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="86bb7-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="86bb7-122">ForceEnglishOutput</span></span> | <span data-ttu-id="86bb7-123">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="86bb7-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="86bb7-124">帮助</span><span class="sxs-lookup"><span data-stu-id="86bb7-124">Help</span></span> | <span data-ttu-id="86bb7-125">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="86bb7-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="86bb7-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="86bb7-126">NonInteractive</span></span> | <span data-ttu-id="86bb7-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="86bb7-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="86bb7-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="86bb7-128">NoSymbols</span></span> | <span data-ttu-id="86bb7-129">*（3.5 +)* 如果符号包存在，它将不会推送到符号服务器。</span><span class="sxs-lookup"><span data-stu-id="86bb7-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="86bb7-130">源</span><span class="sxs-lookup"><span data-stu-id="86bb7-130">Source</span></span> | <span data-ttu-id="86bb7-131">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="86bb7-131">Specifies the server URL.</span></span> <span data-ttu-id="86bb7-132">NuGet 标识的 UNC 或本地文件夹源，并只需将复制文件而不是将它使用 HTTP 推送。</span><span class="sxs-lookup"><span data-stu-id="86bb7-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="86bb7-133">此外，从开始 NuGet 上面 3.4.2，这是强制参数除非`NuGet.Config`文件指定*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="86bb7-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="86bb7-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="86bb7-134">SymbolSource</span></span> | <span data-ttu-id="86bb7-135">*（3.5 +)* 指定符号服务器 URL; 推送到 nuget.org 时使用 nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="86bb7-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="86bb7-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="86bb7-136">SymbolApiKey</span></span> | <span data-ttu-id="86bb7-137">*（3.5 +)* 中指定的 URL 指定的 API 密钥`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="86bb7-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="86bb7-138">超时</span><span class="sxs-lookup"><span data-stu-id="86bb7-138">Timeout</span></span> | <span data-ttu-id="86bb7-139">指定超时，以秒为单位，以便将推送到服务器。</span><span class="sxs-lookup"><span data-stu-id="86bb7-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="86bb7-140">默认值为 300 秒 （5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="86bb7-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="86bb7-141">详细级别</span><span class="sxs-lookup"><span data-stu-id="86bb7-141">Verbosity</span></span> | <span data-ttu-id="86bb7-142">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="86bb7-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="86bb7-143">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="86bb7-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="86bb7-144">示例</span><span class="sxs-lookup"><span data-stu-id="86bb7-144">Examples</span></span>

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
