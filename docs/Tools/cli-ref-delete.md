---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的引用
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="00615-103">删除命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="00615-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="00615-104">**适用于：**包发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="00615-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="00615-105">删除或 unlists 从包源的包。</span><span class="sxs-lookup"><span data-stu-id="00615-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="00615-106">有关 nuget.org，delete 命令[unlists 包](../policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="00615-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="00615-107">用法</span><span class="sxs-lookup"><span data-stu-id="00615-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="00615-108">其中`<packageID>`和`<packageVersion>`标识要删除或不列出的确切包。</span><span class="sxs-lookup"><span data-stu-id="00615-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="00615-109">具体的行为取决于源。</span><span class="sxs-lookup"><span data-stu-id="00615-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="00615-110">对于本地文件夹，例如，则删除此包;未列出 nuget.org 包为。</span><span class="sxs-lookup"><span data-stu-id="00615-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="00615-111">选项</span><span class="sxs-lookup"><span data-stu-id="00615-111">Options</span></span>

| <span data-ttu-id="00615-112">选项</span><span class="sxs-lookup"><span data-stu-id="00615-112">Option</span></span> | <span data-ttu-id="00615-113">描述</span><span class="sxs-lookup"><span data-stu-id="00615-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00615-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="00615-114">ApiKey</span></span> | <span data-ttu-id="00615-115">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="00615-115">The API key for the target repository.</span></span> <span data-ttu-id="00615-116">如果不存在，则使用在配置文件中指定。</span><span class="sxs-lookup"><span data-stu-id="00615-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="00615-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="00615-117">ConfigFile</span></span> | <span data-ttu-id="00615-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="00615-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="00615-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="00615-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="00615-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="00615-120">ForceEnglishOutput</span></span> | <span data-ttu-id="00615-121">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="00615-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="00615-122">帮助</span><span class="sxs-lookup"><span data-stu-id="00615-122">Help</span></span> | <span data-ttu-id="00615-123">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="00615-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="00615-124">非交互式</span><span class="sxs-lookup"><span data-stu-id="00615-124">NonInteractive</span></span> | <span data-ttu-id="00615-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="00615-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="00615-126">源</span><span class="sxs-lookup"><span data-stu-id="00615-126">Source</span></span> | <span data-ttu-id="00615-127">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="00615-127">Specifies the server URL.</span></span> <span data-ttu-id="00615-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="00615-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="00615-129">对于专用源，用替换主机名，例如， *%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="00615-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="00615-130">详细级别</span><span class="sxs-lookup"><span data-stu-id="00615-130">Verbosity</span></span> | <span data-ttu-id="00615-131">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="00615-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="00615-132">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="00615-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="00615-133">示例</span><span class="sxs-lookup"><span data-stu-id="00615-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
