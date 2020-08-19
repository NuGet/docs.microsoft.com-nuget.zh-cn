---
title: NuGet CLI push 命令
description: nuget.exe push 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622840"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="78aab-103"> (NuGet CLI 的推送命令) </span><span class="sxs-lookup"><span data-stu-id="78aab-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="78aab-104">**适用于：** 包发布 &bullet; **支持的版本：** 全部; 4.1.0 + 必需的 nuget.org</span><span class="sxs-lookup"><span data-stu-id="78aab-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="78aab-105">若要将包推送到 nuget.org，必须使用 nuget.exe v 4.1.0 + 来实现所需的 [nuget 协议](../../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="78aab-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="78aab-106">将包推送到包源并发布包。</span><span class="sxs-lookup"><span data-stu-id="78aab-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="78aab-107">通过加载 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ，然后加载 `Nuget.Config` `.nuget\Nuget.Config` 从驱动器的根目录开始并在当前目录中结束的任何或文件，将获取 NuGet 的默认配置 (参见 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)) </span><span class="sxs-lookup"><span data-stu-id="78aab-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="78aab-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="78aab-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="78aab-109">其中 `<packagePath>` 标识要推送到服务器的包。</span><span class="sxs-lookup"><span data-stu-id="78aab-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="78aab-110">选项</span><span class="sxs-lookup"><span data-stu-id="78aab-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="78aab-111">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="78aab-111">The API key for the target repository.</span></span> <span data-ttu-id="78aab-112">如果不存在，则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="78aab-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="78aab-113">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="78aab-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="78aab-114">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="78aab-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="78aab-115">当推送到 HTTP (s) 服务器来减少内存使用情况时，将禁用缓冲。</span><span class="sxs-lookup"><span data-stu-id="78aab-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="78aab-116">注意：使用此选项时，集成的 Windows 身份验证可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="78aab-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="78aab-117">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="78aab-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="78aab-118">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="78aab-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="78aab-119">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="78aab-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="78aab-120">不追加 `api/v2/packages` 到源 URL。</span><span class="sxs-lookup"><span data-stu-id="78aab-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="78aab-121">\* (3.5 +) \* 如果符号包存在，则不会将其推送到符号服务器。</span><span class="sxs-lookup"><span data-stu-id="78aab-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="78aab-122">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="78aab-122">Specifies the server URL.</span></span> <span data-ttu-id="78aab-123">NuGet 标识 UNC 或本地文件夹源，只是复制该文件，而不是使用 HTTP 推送它。</span><span class="sxs-lookup"><span data-stu-id="78aab-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="78aab-124">此外，从 NuGet 3.4.2 开始，这是必需的参数，除非该 `NuGet.Config` 文件指定了 *DefaultPushSource* 值 (请参阅 [配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)) 。</span><span class="sxs-lookup"><span data-stu-id="78aab-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="78aab-125">\* (5.1 +) \* 如果包和版本已存在，则跳过它，并继续执行推送中的下一个包（如果有）。</span><span class="sxs-lookup"><span data-stu-id="78aab-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="78aab-126">\* (3.5 +) \* 指定符号服务器 URL;推送到 nuget.org 时使用 nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="78aab-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="78aab-127">\* (3.5 +) \* 为中指定的 URL 指定 API 密钥 `-SymbolSource` 。</span><span class="sxs-lookup"><span data-stu-id="78aab-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="78aab-128">指定推送到服务器的超时值（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="78aab-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="78aab-129">默认值为 300 秒（5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="78aab-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="78aab-130">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="78aab-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="78aab-131">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="78aab-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="78aab-132">示例</span><span class="sxs-lookup"><span data-stu-id="78aab-132">Examples</span></span>

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
