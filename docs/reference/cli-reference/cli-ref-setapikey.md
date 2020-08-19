---
title: NuGet CLI setapikey 命令
description: nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622806"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="b7e3d-103"> (NuGet CLI) 的 setapikey 命令</span><span class="sxs-lookup"><span data-stu-id="b7e3d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="b7e3d-104">**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="b7e3d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b7e3d-105">将给定服务器 URL 的 API 密钥保存到 `NuGet.Config` ，以便不需要为后续命令输入该 URL。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b7e3d-106">使用情况</span><span class="sxs-lookup"><span data-stu-id="b7e3d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="b7e3d-107">其中 `<source>` 标识服务器， `<key>` 是要保存的密钥。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="b7e3d-108">如果 `<source>` 省略，则假定为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="b7e3d-109">API 密钥不用于通过专用源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="b7e3d-110">请参阅[ `nuget sources` 命令](../cli-reference/cli-ref-sources.md)，管理凭据以便通过源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="b7e3d-111">可以从单个 NuGet 服务器获取 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="b7e3d-112">若要创建和管理 nuget.org 的 APIKeys，请参阅 [获取 api 密钥](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="b7e3d-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="b7e3d-113">选项</span><span class="sxs-lookup"><span data-stu-id="b7e3d-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b7e3d-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b7e3d-115">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b7e3d-116">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b7e3d-117">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b7e3d-118">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="b7e3d-119">API 密钥有效的服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b7e3d-120">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="b7e3d-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="b7e3d-121">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b7e3d-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b7e3d-122">示例</span><span class="sxs-lookup"><span data-stu-id="b7e3d-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
