---
title: "NuGet CLI 局部变量命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Nuget.exe 局部变量命令参考"
keywords: "nuget 局部变量引用，局部变量命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="487b9-104">局部变量命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="487b9-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="487b9-105">**适用于：**打包消耗&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="487b9-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="487b9-106">清除或列出本地 NuGet 资源，如 http 请求缓存、 包缓存和计算机范围全局包文件夹。</span><span class="sxs-lookup"><span data-stu-id="487b9-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="487b9-107">`locals`命令还可以用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="487b9-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="487b9-108">有关详细信息，请参阅[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)。</span><span class="sxs-lookup"><span data-stu-id="487b9-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="487b9-109">用法</span><span class="sxs-lookup"><span data-stu-id="487b9-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="487b9-110">其中`<cache>`是之一`all`， `http-cache`， `packages-cache`， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="487b9-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="487b9-111">选项</span><span class="sxs-lookup"><span data-stu-id="487b9-111">Options</span></span>

| <span data-ttu-id="487b9-112">选项</span><span class="sxs-lookup"><span data-stu-id="487b9-112">Option</span></span> | <span data-ttu-id="487b9-113">描述</span><span class="sxs-lookup"><span data-stu-id="487b9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="487b9-114">清除</span><span class="sxs-lookup"><span data-stu-id="487b9-114">Clear</span></span> | <span data-ttu-id="487b9-115">清除指定的缓存。</span><span class="sxs-lookup"><span data-stu-id="487b9-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="487b9-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="487b9-116">ConfigFile</span></span> | <span data-ttu-id="487b9-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="487b9-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="487b9-118">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="487b9-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="487b9-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="487b9-119">ForceEnglishOutput</span></span> | <span data-ttu-id="487b9-120">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="487b9-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="487b9-121">帮助</span><span class="sxs-lookup"><span data-stu-id="487b9-121">Help</span></span> | <span data-ttu-id="487b9-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="487b9-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="487b9-123">列表</span><span class="sxs-lookup"><span data-stu-id="487b9-123">List</span></span> | <span data-ttu-id="487b9-124">列出指定的缓存的位置或一起使用时的所有缓存的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="487b9-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="487b9-125">非交互式</span><span class="sxs-lookup"><span data-stu-id="487b9-125">NonInteractive</span></span> | <span data-ttu-id="487b9-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="487b9-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="487b9-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="487b9-127">Verbosity</span></span> | <span data-ttu-id="487b9-128">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="487b9-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="487b9-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="487b9-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="487b9-130">示例</span><span class="sxs-lookup"><span data-stu-id="487b9-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```
