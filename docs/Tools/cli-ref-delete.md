---
title: "NuGet CLI 删除命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete 命令的引用"
keywords: "nuget 删除引用，则删除包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="3a47e-104">删除命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3a47e-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="3a47e-105">**适用于：**包发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="3a47e-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3a47e-106">删除或 unlists 从包源的包。</span><span class="sxs-lookup"><span data-stu-id="3a47e-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="3a47e-107">有关 nuget.org，delete 命令[unlists 包](../policies/Deleting-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="3a47e-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3a47e-108">用法</span><span class="sxs-lookup"><span data-stu-id="3a47e-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="3a47e-109">其中`<packageID>`和`<packageVersion>`标识要删除或不列出的确切包。</span><span class="sxs-lookup"><span data-stu-id="3a47e-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="3a47e-110">具体的行为取决于源。</span><span class="sxs-lookup"><span data-stu-id="3a47e-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="3a47e-111">对于本地文件夹，例如，则删除此包;未列出 nuget.org 包为。</span><span class="sxs-lookup"><span data-stu-id="3a47e-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="3a47e-112">选项</span><span class="sxs-lookup"><span data-stu-id="3a47e-112">Options</span></span>

| <span data-ttu-id="3a47e-113">选项</span><span class="sxs-lookup"><span data-stu-id="3a47e-113">Option</span></span> | <span data-ttu-id="3a47e-114">描述</span><span class="sxs-lookup"><span data-stu-id="3a47e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a47e-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3a47e-115">ApiKey</span></span> | <span data-ttu-id="3a47e-116">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="3a47e-116">The API key for the target repository.</span></span> <span data-ttu-id="3a47e-117">如果不存在，请在指定某一*%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="3a47e-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3a47e-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3a47e-118">ConfigFile</span></span> | <span data-ttu-id="3a47e-119">*（2.5 +)* NuGet 要应用的配置文件。</span><span class="sxs-lookup"><span data-stu-id="3a47e-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="3a47e-120">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="3a47e-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3a47e-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3a47e-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3a47e-122">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="3a47e-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3a47e-123">帮助</span><span class="sxs-lookup"><span data-stu-id="3a47e-123">Help</span></span> | <span data-ttu-id="3a47e-124">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="3a47e-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3a47e-125">非交互式</span><span class="sxs-lookup"><span data-stu-id="3a47e-125">NonInteractive</span></span> | <span data-ttu-id="3a47e-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="3a47e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3a47e-127">源</span><span class="sxs-lookup"><span data-stu-id="3a47e-127">Source</span></span> | <span data-ttu-id="3a47e-128">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="3a47e-128">Specifies the server URL.</span></span> <span data-ttu-id="3a47e-129">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="3a47e-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="3a47e-130">对于专用源，用替换主机名，例如， *%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="3a47e-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="3a47e-131">详细级别</span><span class="sxs-lookup"><span data-stu-id="3a47e-131">Verbosity</span></span> | <span data-ttu-id="3a47e-132">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="3a47e-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="3a47e-133">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3a47e-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3a47e-134">示例</span><span class="sxs-lookup"><span data-stu-id="3a47e-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
