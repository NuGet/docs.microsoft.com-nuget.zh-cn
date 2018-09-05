---
title: NuGet CLI 推送命令
description: Nuget.exe push 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548338"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="8f36e-103">push 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8f36e-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="8f36e-104">**适用于：** 包发布&bullet;**支持的版本：** 所有; 所需的 nuget.org 4.1.0 +</span><span class="sxs-lookup"><span data-stu-id="8f36e-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="8f36e-105">若要将包推送到 nuget.org，必须使用 nuget.exe v4.1.0 +，该实现所需[NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="8f36e-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="8f36e-106">将包推送到包源并将其发布。</span><span class="sxs-lookup"><span data-stu-id="8f36e-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="8f36e-107">NuGet 的默认配置通过加载`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然后加载任何`Nuget.Config`或`.nuget\Nuget.Config`文件从驱动器的根目录开始和结束当前目录中 (请参阅[配置NuGet 行为](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="8f36e-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="8f36e-108">用法</span><span class="sxs-lookup"><span data-stu-id="8f36e-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="8f36e-109">其中`<packagePath>`标识要推送到服务器的包。</span><span class="sxs-lookup"><span data-stu-id="8f36e-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="8f36e-110">选项</span><span class="sxs-lookup"><span data-stu-id="8f36e-110">Options</span></span>

| <span data-ttu-id="8f36e-111">选项</span><span class="sxs-lookup"><span data-stu-id="8f36e-111">Option</span></span> | <span data-ttu-id="8f36e-112">描述</span><span class="sxs-lookup"><span data-stu-id="8f36e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f36e-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8f36e-113">ApiKey</span></span> | <span data-ttu-id="8f36e-114">目标存储库 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="8f36e-114">The API key for the target repository.</span></span> <span data-ttu-id="8f36e-115">如果不存在，则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="8f36e-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="8f36e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8f36e-116">ConfigFile</span></span> | <span data-ttu-id="8f36e-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="8f36e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8f36e-118">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="8f36e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8f36e-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="8f36e-119">DisableBuffering</span></span> | <span data-ttu-id="8f36e-120">禁用缓冲时推送到 http （s） 服务器以减少内存使用情况。</span><span class="sxs-lookup"><span data-stu-id="8f36e-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="8f36e-121">注意： 使用此选项时，集成的 Windows 身份验证可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="8f36e-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="8f36e-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8f36e-122">ForceEnglishOutput</span></span> | <span data-ttu-id="8f36e-123">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="8f36e-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8f36e-124">帮助</span><span class="sxs-lookup"><span data-stu-id="8f36e-124">Help</span></span> | <span data-ttu-id="8f36e-125">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="8f36e-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="8f36e-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8f36e-126">NonInteractive</span></span> | <span data-ttu-id="8f36e-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="8f36e-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8f36e-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="8f36e-128">NoSymbols</span></span> | <span data-ttu-id="8f36e-129">*（3.5 +)* 如果符号包存在，它将不会推送到符号服务器。</span><span class="sxs-lookup"><span data-stu-id="8f36e-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="8f36e-130">源</span><span class="sxs-lookup"><span data-stu-id="8f36e-130">Source</span></span> | <span data-ttu-id="8f36e-131">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="8f36e-131">Specifies the server URL.</span></span> <span data-ttu-id="8f36e-132">NuGet 标识的 UNC 或本地文件夹源，并只需将复制的文件而非推送它使用 HTTP。</span><span class="sxs-lookup"><span data-stu-id="8f36e-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="8f36e-133">此外，从 NuGet 3.4.2 开始，这是一个必需参数除非`NuGet.Config`文件指定*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="8f36e-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="8f36e-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="8f36e-134">SymbolSource</span></span> | <span data-ttu-id="8f36e-135">*（3.5 +)* Nuget.smbsrc.net 使用推送到 nuget.org 时; 指定符号服务器 URL</span><span class="sxs-lookup"><span data-stu-id="8f36e-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="8f36e-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="8f36e-136">SymbolApiKey</span></span> | <span data-ttu-id="8f36e-137">*（3.5 +)* 为 URL 指定在指定的 API 密钥`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="8f36e-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="8f36e-138">超时</span><span class="sxs-lookup"><span data-stu-id="8f36e-138">Timeout</span></span> | <span data-ttu-id="8f36e-139">指定的超时，以秒为单位，以便将推送到服务器。</span><span class="sxs-lookup"><span data-stu-id="8f36e-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="8f36e-140">默认值为 300 秒 （5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="8f36e-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="8f36e-141">详细级别</span><span class="sxs-lookup"><span data-stu-id="8f36e-141">Verbosity</span></span> | <span data-ttu-id="8f36e-142">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="8f36e-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8f36e-143">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8f36e-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f36e-144">示例</span><span class="sxs-lookup"><span data-stu-id="8f36e-144">Examples</span></span>

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
