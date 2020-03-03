---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231222"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="71b4f-103">setapikey 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="71b4f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="71b4f-104">**适用于：** 包使用情况、发布 &bullet;**支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="71b4f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="71b4f-105">将给定服务器 URL 的 API 密钥保存到 `NuGet.Config`，以便不需要为后续命令输入该 URL。</span><span class="sxs-lookup"><span data-stu-id="71b4f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="71b4f-106">使用情况</span><span class="sxs-lookup"><span data-stu-id="71b4f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="71b4f-107">其中 `<source>` 标识服务器，`<key>` 是要保存的密钥。</span><span class="sxs-lookup"><span data-stu-id="71b4f-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="71b4f-108">如果省略 `<source>`，则采用 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="71b4f-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="71b4f-109">API 密钥不用于通过专用源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="71b4f-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="71b4f-110">请参阅[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，管理凭据以便通过源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="71b4f-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="71b4f-111">可以从单个 NuGet 服务器获取 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="71b4f-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="71b4f-112">若要创建和管理 nuget.org 的 APIKeys，请参阅[发布 api 密钥](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="71b4f-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="71b4f-113">选项</span><span class="sxs-lookup"><span data-stu-id="71b4f-113">Options</span></span>

| <span data-ttu-id="71b4f-114">选项</span><span class="sxs-lookup"><span data-stu-id="71b4f-114">Option</span></span> | <span data-ttu-id="71b4f-115">说明</span><span class="sxs-lookup"><span data-stu-id="71b4f-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71b4f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="71b4f-116">ConfigFile</span></span> | <span data-ttu-id="71b4f-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="71b4f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="71b4f-118">如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="71b4f-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="71b4f-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="71b4f-119">ForceEnglishOutput</span></span> | <span data-ttu-id="71b4f-120">*（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="71b4f-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="71b4f-121">帮助</span><span class="sxs-lookup"><span data-stu-id="71b4f-121">Help</span></span> | <span data-ttu-id="71b4f-122">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="71b4f-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="71b4f-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="71b4f-123">NonInteractive</span></span> | <span data-ttu-id="71b4f-124">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="71b4f-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="71b4f-125">详细程度</span><span class="sxs-lookup"><span data-stu-id="71b4f-125">Verbosity</span></span> | <span data-ttu-id="71b4f-126">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="71b4f-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="71b4f-127">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="71b4f-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="71b4f-128">示例</span><span class="sxs-lookup"><span data-stu-id="71b4f-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
