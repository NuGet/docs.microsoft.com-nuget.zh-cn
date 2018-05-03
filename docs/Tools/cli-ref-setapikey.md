---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令参考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 968e22f32e51659590a6fe1e881bf5a9792a1331
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="37a19-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="37a19-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="37a19-104">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="37a19-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="37a19-105">将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。</span><span class="sxs-lookup"><span data-stu-id="37a19-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="37a19-106">用法</span><span class="sxs-lookup"><span data-stu-id="37a19-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="37a19-107">其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。</span><span class="sxs-lookup"><span data-stu-id="37a19-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="37a19-108">如果`<source>`是省略，则假定 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="37a19-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="37a19-109">选项</span><span class="sxs-lookup"><span data-stu-id="37a19-109">Options</span></span>

| <span data-ttu-id="37a19-110">选项</span><span class="sxs-lookup"><span data-stu-id="37a19-110">Option</span></span> | <span data-ttu-id="37a19-111">描述</span><span class="sxs-lookup"><span data-stu-id="37a19-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="37a19-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="37a19-112">ConfigFile</span></span> | <span data-ttu-id="37a19-113">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="37a19-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="37a19-114">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="37a19-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="37a19-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="37a19-115">ForceEnglishOutput</span></span> | <span data-ttu-id="37a19-116">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="37a19-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="37a19-117">帮助</span><span class="sxs-lookup"><span data-stu-id="37a19-117">Help</span></span> | <span data-ttu-id="37a19-118">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="37a19-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="37a19-119">非交互式</span><span class="sxs-lookup"><span data-stu-id="37a19-119">NonInteractive</span></span> | <span data-ttu-id="37a19-120">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="37a19-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="37a19-121">详细级别</span><span class="sxs-lookup"><span data-stu-id="37a19-121">Verbosity</span></span> | <span data-ttu-id="37a19-122">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="37a19-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="37a19-123">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="37a19-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="37a19-124">示例</span><span class="sxs-lookup"><span data-stu-id="37a19-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
