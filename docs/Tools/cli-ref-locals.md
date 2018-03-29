---
title: NuGet CLI 局部变量命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 局部变量命令参考
keywords: nuget 局部变量引用，局部变量命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="ad15b-104">局部变量命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ad15b-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="ad15b-105">**适用于：**打包消耗&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ad15b-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ad15b-106">清除或列出本地 NuGet 资源例如*http 缓存*，*全局包*文件夹和临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad15b-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="ad15b-107">`locals`命令还可以用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="ad15b-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="ad15b-108">有关详细信息，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="ad15b-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ad15b-109">用法</span><span class="sxs-lookup"><span data-stu-id="ad15b-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="ad15b-110">其中`<folder>`是之一`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="ad15b-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="ad15b-111">选项</span><span class="sxs-lookup"><span data-stu-id="ad15b-111">Options</span></span>

| <span data-ttu-id="ad15b-112">选项</span><span class="sxs-lookup"><span data-stu-id="ad15b-112">Option</span></span> | <span data-ttu-id="ad15b-113">描述</span><span class="sxs-lookup"><span data-stu-id="ad15b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad15b-114">清除</span><span class="sxs-lookup"><span data-stu-id="ad15b-114">Clear</span></span> | <span data-ttu-id="ad15b-115">清除指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad15b-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="ad15b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ad15b-116">ConfigFile</span></span> | <span data-ttu-id="ad15b-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ad15b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ad15b-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="ad15b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ad15b-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ad15b-119">ForceEnglishOutput</span></span> | <span data-ttu-id="ad15b-120">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="ad15b-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ad15b-121">帮助</span><span class="sxs-lookup"><span data-stu-id="ad15b-121">Help</span></span> | <span data-ttu-id="ad15b-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="ad15b-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ad15b-123">列表</span><span class="sxs-lookup"><span data-stu-id="ad15b-123">List</span></span> | <span data-ttu-id="ad15b-124">列出指定的文件夹的位置或一起使用时的所有文件夹的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="ad15b-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="ad15b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ad15b-125">NonInteractive</span></span> | <span data-ttu-id="ad15b-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="ad15b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ad15b-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="ad15b-127">Verbosity</span></span> | <span data-ttu-id="ad15b-128">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="ad15b-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ad15b-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad15b-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ad15b-130">示例</span><span class="sxs-lookup"><span data-stu-id="ad15b-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="ad15b-131">有关其他示例，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="ad15b-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
