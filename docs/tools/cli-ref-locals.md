---
title: NuGet CLI 局部变量命令
description: Nuget.exe 局部变量命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818196"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c202b-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c202b-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c202b-104">**适用于：** 打包消耗&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c202b-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c202b-105">清除或列出本地 NuGet 资源例如*http 缓存*，*全局包*文件夹和临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="c202b-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="c202b-106">`locals`命令还可以用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="c202b-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c202b-107">有关详细信息，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c202b-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c202b-108">用法</span><span class="sxs-lookup"><span data-stu-id="c202b-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="c202b-109">其中`<folder>`是之一`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="c202b-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c202b-110">选项</span><span class="sxs-lookup"><span data-stu-id="c202b-110">Options</span></span>

| <span data-ttu-id="c202b-111">选项</span><span class="sxs-lookup"><span data-stu-id="c202b-111">Option</span></span> | <span data-ttu-id="c202b-112">描述</span><span class="sxs-lookup"><span data-stu-id="c202b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c202b-113">清除</span><span class="sxs-lookup"><span data-stu-id="c202b-113">Clear</span></span> | <span data-ttu-id="c202b-114">清除指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c202b-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="c202b-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c202b-115">ConfigFile</span></span> | <span data-ttu-id="c202b-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c202b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c202b-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="c202b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c202b-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c202b-118">ForceEnglishOutput</span></span> | <span data-ttu-id="c202b-119">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="c202b-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c202b-120">帮助</span><span class="sxs-lookup"><span data-stu-id="c202b-120">Help</span></span> | <span data-ttu-id="c202b-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c202b-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="c202b-122">列表</span><span class="sxs-lookup"><span data-stu-id="c202b-122">List</span></span> | <span data-ttu-id="c202b-123">列出指定的文件夹的位置或一起使用时的所有文件夹的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="c202b-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="c202b-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c202b-124">NonInteractive</span></span> | <span data-ttu-id="c202b-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="c202b-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c202b-126">详细级别</span><span class="sxs-lookup"><span data-stu-id="c202b-126">Verbosity</span></span> | <span data-ttu-id="c202b-127">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="c202b-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c202b-128">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c202b-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c202b-129">示例</span><span class="sxs-lookup"><span data-stu-id="c202b-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="c202b-130">有关其他示例，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c202b-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
