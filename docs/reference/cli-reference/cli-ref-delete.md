---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327834"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="8023b-103">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8023b-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="8023b-104">**适用于:** 包发布&bullet; **支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="8023b-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8023b-105">从包源中删除或取消列出包。</span><span class="sxs-lookup"><span data-stu-id="8023b-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="8023b-106">对于 nuget.org, delete 命令[取消列出包](../../nuget-org/policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8023b-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8023b-107">用法</span><span class="sxs-lookup"><span data-stu-id="8023b-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="8023b-108">where `<packageID>` 和`<packageVersion>`确定要删除或取消列出的确切包。</span><span class="sxs-lookup"><span data-stu-id="8023b-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="8023b-109">具体的行为取决于源。</span><span class="sxs-lookup"><span data-stu-id="8023b-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="8023b-110">例如, 对于本地文件夹, 将删除包;对于 nuget.org, 包未列出。</span><span class="sxs-lookup"><span data-stu-id="8023b-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="8023b-111">选项</span><span class="sxs-lookup"><span data-stu-id="8023b-111">Options</span></span>

| <span data-ttu-id="8023b-112">选项</span><span class="sxs-lookup"><span data-stu-id="8023b-112">Option</span></span> | <span data-ttu-id="8023b-113">描述</span><span class="sxs-lookup"><span data-stu-id="8023b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8023b-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8023b-114">ApiKey</span></span> | <span data-ttu-id="8023b-115">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="8023b-115">The API key for the target repository.</span></span> <span data-ttu-id="8023b-116">如果不存在, 则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="8023b-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="8023b-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8023b-117">ConfigFile</span></span> | <span data-ttu-id="8023b-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="8023b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8023b-119">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="8023b-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8023b-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8023b-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8023b-121">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="8023b-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8023b-122">Help</span><span class="sxs-lookup"><span data-stu-id="8023b-122">Help</span></span> | <span data-ttu-id="8023b-123">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="8023b-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8023b-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8023b-124">NonInteractive</span></span> | <span data-ttu-id="8023b-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="8023b-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8023b-126">Source</span><span class="sxs-lookup"><span data-stu-id="8023b-126">Source</span></span> | <span data-ttu-id="8023b-127">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="8023b-127">Specifies the server URL.</span></span> <span data-ttu-id="8023b-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="8023b-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8023b-129">对于专用源, 请替换主机名, 例如, *% hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="8023b-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="8023b-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8023b-130">Verbosity</span></span> | <span data-ttu-id="8023b-131">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="8023b-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8023b-132">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8023b-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8023b-133">示例</span><span class="sxs-lookup"><span data-stu-id="8023b-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
