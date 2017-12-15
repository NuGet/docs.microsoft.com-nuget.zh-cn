---
title: "NuGet CLI setapikey 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Nuget.exe setapikey 命令参考"
keywords: "nuget setapikey 引用，setapikey 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="41eb7-104">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="41eb7-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="41eb7-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="41eb7-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="41eb7-106">将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。</span><span class="sxs-lookup"><span data-stu-id="41eb7-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="41eb7-107">用法</span><span class="sxs-lookup"><span data-stu-id="41eb7-107">Usage</span></span>

```
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="41eb7-108">其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。</span><span class="sxs-lookup"><span data-stu-id="41eb7-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="41eb7-109">如果`<source>`是省略，则假定 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="41eb7-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="41eb7-110">选项</span><span class="sxs-lookup"><span data-stu-id="41eb7-110">Options</span></span>

| <span data-ttu-id="41eb7-111">选项</span><span class="sxs-lookup"><span data-stu-id="41eb7-111">Option</span></span> | <span data-ttu-id="41eb7-112">描述</span><span class="sxs-lookup"><span data-stu-id="41eb7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41eb7-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="41eb7-113">ConfigFile</span></span> | <span data-ttu-id="41eb7-114">*（2.5 +)* NuGet 要修改的配置文件。</span><span class="sxs-lookup"><span data-stu-id="41eb7-114">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="41eb7-115">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="41eb7-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="41eb7-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="41eb7-116">ForceEnglishOutput</span></span> | <span data-ttu-id="41eb7-117">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="41eb7-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="41eb7-118">帮助</span><span class="sxs-lookup"><span data-stu-id="41eb7-118">Help</span></span> | <span data-ttu-id="41eb7-119">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="41eb7-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="41eb7-120">非交互式</span><span class="sxs-lookup"><span data-stu-id="41eb7-120">NonInteractive</span></span> | <span data-ttu-id="41eb7-121">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="41eb7-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="41eb7-122">详细级别</span><span class="sxs-lookup"><span data-stu-id="41eb7-122">Verbosity</span></span> | <span data-ttu-id="41eb7-123">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="41eb7-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="41eb7-124">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="41eb7-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="41eb7-125">示例</span><span class="sxs-lookup"><span data-stu-id="41eb7-125">Examples</span></span>

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
