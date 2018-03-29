---
title: NuGet CLI setapikey 命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe setapikey 命令参考
keywords: nuget setapikey 引用，setapikey 命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="e7c9a-104">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e7c9a-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="e7c9a-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="e7c9a-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e7c9a-106">将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e7c9a-107">用法</span><span class="sxs-lookup"><span data-stu-id="e7c9a-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="e7c9a-108">其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="e7c9a-109">如果`<source>`是省略，则假定 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="e7c9a-110">选项</span><span class="sxs-lookup"><span data-stu-id="e7c9a-110">Options</span></span>

| <span data-ttu-id="e7c9a-111">选项</span><span class="sxs-lookup"><span data-stu-id="e7c9a-111">Option</span></span> | <span data-ttu-id="e7c9a-112">描述</span><span class="sxs-lookup"><span data-stu-id="e7c9a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7c9a-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e7c9a-113">ConfigFile</span></span> | <span data-ttu-id="e7c9a-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e7c9a-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e7c9a-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e7c9a-116">ForceEnglishOutput</span></span> | <span data-ttu-id="e7c9a-117">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e7c9a-118">帮助</span><span class="sxs-lookup"><span data-stu-id="e7c9a-118">Help</span></span> | <span data-ttu-id="e7c9a-119">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="e7c9a-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e7c9a-120">NonInteractive</span></span> | <span data-ttu-id="e7c9a-121">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e7c9a-122">详细级别</span><span class="sxs-lookup"><span data-stu-id="e7c9a-122">Verbosity</span></span> | <span data-ttu-id="e7c9a-123">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="e7c9a-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e7c9a-124">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e7c9a-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e7c9a-125">示例</span><span class="sxs-lookup"><span data-stu-id="e7c9a-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
