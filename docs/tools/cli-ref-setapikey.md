---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817679"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="237e7-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="237e7-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="237e7-104">**适用于：** 包消耗、 发布&bullet;**受支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="237e7-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="237e7-105">将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。</span><span class="sxs-lookup"><span data-stu-id="237e7-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="237e7-106">用法</span><span class="sxs-lookup"><span data-stu-id="237e7-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="237e7-107">其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。</span><span class="sxs-lookup"><span data-stu-id="237e7-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="237e7-108">如果`<source>`是省略，则假定 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="237e7-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="237e7-109">选项</span><span class="sxs-lookup"><span data-stu-id="237e7-109">Options</span></span>

| <span data-ttu-id="237e7-110">选项</span><span class="sxs-lookup"><span data-stu-id="237e7-110">Option</span></span> | <span data-ttu-id="237e7-111">描述</span><span class="sxs-lookup"><span data-stu-id="237e7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="237e7-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="237e7-112">ConfigFile</span></span> | <span data-ttu-id="237e7-113">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="237e7-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="237e7-114">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="237e7-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="237e7-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="237e7-115">ForceEnglishOutput</span></span> | <span data-ttu-id="237e7-116">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="237e7-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="237e7-117">帮助</span><span class="sxs-lookup"><span data-stu-id="237e7-117">Help</span></span> | <span data-ttu-id="237e7-118">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="237e7-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="237e7-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="237e7-119">NonInteractive</span></span> | <span data-ttu-id="237e7-120">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="237e7-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="237e7-121">详细级别</span><span class="sxs-lookup"><span data-stu-id="237e7-121">Verbosity</span></span> | <span data-ttu-id="237e7-122">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="237e7-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="237e7-123">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="237e7-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="237e7-124">示例</span><span class="sxs-lookup"><span data-stu-id="237e7-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
