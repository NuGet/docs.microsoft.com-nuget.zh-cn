---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383964"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="3f75e-103">setapikey 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="3f75e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="3f75e-104">**适用于：** 包使用情况、发布 &bullet;**支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="3f75e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3f75e-105">将给定服务器 URL 的 API 密钥保存到 `NuGet.Config`，以便不需要为后续命令输入该 URL。</span><span class="sxs-lookup"><span data-stu-id="3f75e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3f75e-106">用量</span><span class="sxs-lookup"><span data-stu-id="3f75e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="3f75e-107">其中 `<source>` 标识服务器，`<key>` 是要保存的密钥或密码。</span><span class="sxs-lookup"><span data-stu-id="3f75e-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="3f75e-108">如果省略 `<source>`，则采用 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="3f75e-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="3f75e-109">API 密钥不用于通过专用源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3f75e-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="3f75e-110">请参阅[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，管理凭据以便通过源进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3f75e-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="3f75e-111">选项</span><span class="sxs-lookup"><span data-stu-id="3f75e-111">Options</span></span>

| <span data-ttu-id="3f75e-112">选项</span><span class="sxs-lookup"><span data-stu-id="3f75e-112">Option</span></span> | <span data-ttu-id="3f75e-113">描述</span><span class="sxs-lookup"><span data-stu-id="3f75e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f75e-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3f75e-114">ConfigFile</span></span> | <span data-ttu-id="3f75e-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="3f75e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3f75e-116">如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="3f75e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3f75e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3f75e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="3f75e-118">*（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="3f75e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3f75e-119">帮助</span><span class="sxs-lookup"><span data-stu-id="3f75e-119">Help</span></span> | <span data-ttu-id="3f75e-120">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="3f75e-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="3f75e-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3f75e-121">NonInteractive</span></span> | <span data-ttu-id="3f75e-122">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="3f75e-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3f75e-123">详细级别</span><span class="sxs-lookup"><span data-stu-id="3f75e-123">Verbosity</span></span> | <span data-ttu-id="3f75e-124">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="3f75e-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3f75e-125">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3f75e-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3f75e-126">示例</span><span class="sxs-lookup"><span data-stu-id="3f75e-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
