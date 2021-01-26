---
title: NuGet CLI delete 命令
description: nuget.exe delete 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775950"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="c07bf-103"> (NuGet CLI) 删除命令</span><span class="sxs-lookup"><span data-stu-id="c07bf-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="c07bf-104">**适用于：** 包发布 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="c07bf-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c07bf-105">从包源中删除或取消列出包。</span><span class="sxs-lookup"><span data-stu-id="c07bf-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="c07bf-106">对于 nuget.org，delete 命令 [取消列出包](../../nuget-org/policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="c07bf-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c07bf-107">使用情况</span><span class="sxs-lookup"><span data-stu-id="c07bf-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="c07bf-108">where `<packageID>` 和 `<packageVersion>` 确定要删除或取消列出的确切包。</span><span class="sxs-lookup"><span data-stu-id="c07bf-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="c07bf-109">具体的行为取决于源。</span><span class="sxs-lookup"><span data-stu-id="c07bf-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="c07bf-110">例如，对于本地文件夹，将删除包;对于 nuget.org，包未列出。</span><span class="sxs-lookup"><span data-stu-id="c07bf-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="c07bf-111">选项</span><span class="sxs-lookup"><span data-stu-id="c07bf-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="c07bf-112">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="c07bf-112">The API key for the target repository.</span></span> <span data-ttu-id="c07bf-113">如果不存在，则使用配置文件中指定的一个。</span><span class="sxs-lookup"><span data-stu-id="c07bf-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c07bf-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c07bf-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c07bf-115">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="c07bf-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c07bf-116">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="c07bf-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c07bf-117">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="c07bf-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c07bf-118">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="c07bf-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="c07bf-119">删除时不提示。</span><span class="sxs-lookup"><span data-stu-id="c07bf-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="c07bf-120">**`-NoServiceEndpoint`** 不会将 "api/v2/包" 追加到源 URL。</span><span class="sxs-lookup"><span data-stu-id="c07bf-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="c07bf-121">指定服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="c07bf-121">Specifies the server URL.</span></span> <span data-ttu-id="c07bf-122">Nuget.org 的 URL 是 `https://api.nuget.org/v3/index.json` 。</span><span class="sxs-lookup"><span data-stu-id="c07bf-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c07bf-123">对于专用源，请替换主机名，例如， *% hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="c07bf-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c07bf-124">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="c07bf-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c07bf-125">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c07bf-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c07bf-126">示例</span><span class="sxs-lookup"><span data-stu-id="c07bf-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
