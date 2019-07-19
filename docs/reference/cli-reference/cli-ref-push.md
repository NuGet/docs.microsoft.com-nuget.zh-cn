---
title: NuGet CLI push 命令
description: 针对 nuget.exe push 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327624"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="f9a3b-103">push 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f9a3b-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="f9a3b-104">**适用于:** 包发布&bullet; **支持的版本:** 全部; 4.1.0 + 必需的 nuget.org</span><span class="sxs-lookup"><span data-stu-id="f9a3b-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="f9a3b-105">若要将包推送到 nuget.org, 必须使用 4.1.0 +, 后者实现所需的[nuget 协议](../../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="f9a3b-106">将包推送到包源并发布包。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="f9a3b-107">NuGet 的默认配置是通过`%AppData%\NuGet\NuGet.Config`加载 (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux `Nuget.Config` ) `.nuget\Nuget.Config` , 然后从驱动器的根目录启动并在当前目录中结束 (请参阅[常用 NuGet配置](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="f9a3b-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="f9a3b-108">用法</span><span class="sxs-lookup"><span data-stu-id="f9a3b-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="f9a3b-109">其中`<packagePath>`标识要推送到服务器的包。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="f9a3b-110">选项</span><span class="sxs-lookup"><span data-stu-id="f9a3b-110">Options</span></span>

| <span data-ttu-id="f9a3b-111">选项</span><span class="sxs-lookup"><span data-stu-id="f9a3b-111">Option</span></span> | <span data-ttu-id="f9a3b-112">描述</span><span class="sxs-lookup"><span data-stu-id="f9a3b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9a3b-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="f9a3b-113">ApiKey</span></span> | <span data-ttu-id="f9a3b-114">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-114">The API key for the target repository.</span></span> <span data-ttu-id="f9a3b-115">如果不存在, 则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f9a3b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f9a3b-116">ConfigFile</span></span> | <span data-ttu-id="f9a3b-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f9a3b-118">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f9a3b-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="f9a3b-119">DisableBuffering</span></span> | <span data-ttu-id="f9a3b-120">在推送到 HTTP (s) 服务器时禁用缓冲, 以减少内存使用量。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="f9a3b-121">注意: 使用此选项时, 集成的 Windows 身份验证可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="f9a3b-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f9a3b-122">ForceEnglishOutput</span></span> | <span data-ttu-id="f9a3b-123">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f9a3b-124">Help</span><span class="sxs-lookup"><span data-stu-id="f9a3b-124">Help</span></span> | <span data-ttu-id="f9a3b-125">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="f9a3b-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f9a3b-126">NonInteractive</span></span> | <span data-ttu-id="f9a3b-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f9a3b-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="f9a3b-128">NoSymbols</span></span> | <span data-ttu-id="f9a3b-129">*(3.5 +)* 如果符号包存在, 则不会将其推送到符号服务器。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="f9a3b-130">Source</span><span class="sxs-lookup"><span data-stu-id="f9a3b-130">Source</span></span> | <span data-ttu-id="f9a3b-131">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-131">Specifies the server URL.</span></span> <span data-ttu-id="f9a3b-132">NuGet 标识 UNC 或本地文件夹源, 只是复制该文件, 而不是使用 HTTP 推送它。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="f9a3b-133">此外, 从 NuGet 3.4.2 开始, 这是必需的参数, 除非`NuGet.Config`该文件指定了*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="f9a3b-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="f9a3b-134">SkipDuplicate</span></span> | <span data-ttu-id="f9a3b-135">*(5.1 +)* 如果包和版本已存在, 则跳过它, 并继续执行推送中的下一个包 (如果有)。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="f9a3b-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="f9a3b-136">SymbolSource</span></span> | <span data-ttu-id="f9a3b-137">*(3.5 +)* 指定符号服务器 URL;推送到 nuget.org 时使用 nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="f9a3b-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="f9a3b-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="f9a3b-138">SymbolApiKey</span></span> | <span data-ttu-id="f9a3b-139">*(3.5 +)* 为中`-SymbolSource`指定的 URL 指定 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="f9a3b-140">Timeout</span><span class="sxs-lookup"><span data-stu-id="f9a3b-140">Timeout</span></span> | <span data-ttu-id="f9a3b-141">指定推送到服务器的超时值 (以秒为单位)。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="f9a3b-142">默认值为300秒 (5 分钟)。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="f9a3b-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f9a3b-143">Verbosity</span></span> | <span data-ttu-id="f9a3b-144">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f9a3b-145">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f9a3b-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f9a3b-146">示例</span><span class="sxs-lookup"><span data-stu-id="f9a3b-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
