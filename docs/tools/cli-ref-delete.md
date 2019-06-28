---
title: NuGet CLI 删除命令
description: Nuget.exe delete 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426110"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="1f9fc-103">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1f9fc-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="1f9fc-104">**适用于：** 包发布&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="1f9fc-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1f9fc-105">删除或取消列出包从包源。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="1f9fc-106">对于 nuget.org，删除命令[取消列出包](../nuget-org/policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1f9fc-107">用法</span><span class="sxs-lookup"><span data-stu-id="1f9fc-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="1f9fc-108">其中`<packageID>`和`<packageVersion>`标识要删除或取消列出的确切包。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="1f9fc-109">确切行为取决于源。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="1f9fc-110">对于本地文件夹，例如，删除的包;对于 nuget.org 包是未列出。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="1f9fc-111">选项</span><span class="sxs-lookup"><span data-stu-id="1f9fc-111">Options</span></span>

| <span data-ttu-id="1f9fc-112">选项</span><span class="sxs-lookup"><span data-stu-id="1f9fc-112">Option</span></span> | <span data-ttu-id="1f9fc-113">描述</span><span class="sxs-lookup"><span data-stu-id="1f9fc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f9fc-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="1f9fc-114">ApiKey</span></span> | <span data-ttu-id="1f9fc-115">目标存储库 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-115">The API key for the target repository.</span></span> <span data-ttu-id="1f9fc-116">如果不存在，则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="1f9fc-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f9fc-117">ConfigFile</span></span> | <span data-ttu-id="1f9fc-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f9fc-119">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f9fc-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f9fc-120">ForceEnglishOutput</span></span> | <span data-ttu-id="1f9fc-121">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f9fc-122">Help</span><span class="sxs-lookup"><span data-stu-id="1f9fc-122">Help</span></span> | <span data-ttu-id="1f9fc-123">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f9fc-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f9fc-124">NonInteractive</span></span> | <span data-ttu-id="1f9fc-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f9fc-126">Source</span><span class="sxs-lookup"><span data-stu-id="1f9fc-126">Source</span></span> | <span data-ttu-id="1f9fc-127">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-127">Specifies the server URL.</span></span> <span data-ttu-id="1f9fc-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="1f9fc-129">对于专用源，例如，替换主机名 *%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="1f9fc-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1f9fc-130">Verbosity</span></span> | <span data-ttu-id="1f9fc-131">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="1f9fc-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1f9fc-132">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1f9fc-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1f9fc-133">示例</span><span class="sxs-lookup"><span data-stu-id="1f9fc-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
