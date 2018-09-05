---
title: NuGet CLI 局部变量命令
description: Nuget.exe 局部变量命令参考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545023"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="cb7a3-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cb7a3-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="cb7a3-104">**适用于：** 打包消耗&bullet;**支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cb7a3-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="cb7a3-105">清除或列出本地 NuGet 资源，例如*http 缓存*，*全局包*文件夹和临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="cb7a3-106">`locals`命令还可用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="cb7a3-107">有关详细信息，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cb7a3-108">用法</span><span class="sxs-lookup"><span data-stu-id="cb7a3-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="cb7a3-109">其中`<folder>`是之一`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`， `temp` *（3.4 +）*，和`plugins-cache` *（4.8 +）*。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="cb7a3-110">选项</span><span class="sxs-lookup"><span data-stu-id="cb7a3-110">Options</span></span>

| <span data-ttu-id="cb7a3-111">选项</span><span class="sxs-lookup"><span data-stu-id="cb7a3-111">Option</span></span> | <span data-ttu-id="cb7a3-112">描述</span><span class="sxs-lookup"><span data-stu-id="cb7a3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb7a3-113">清除</span><span class="sxs-lookup"><span data-stu-id="cb7a3-113">Clear</span></span> | <span data-ttu-id="cb7a3-114">清除指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="cb7a3-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cb7a3-115">ConfigFile</span></span> | <span data-ttu-id="cb7a3-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb7a3-117">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cb7a3-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cb7a3-118">ForceEnglishOutput</span></span> | <span data-ttu-id="cb7a3-119">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cb7a3-120">帮助</span><span class="sxs-lookup"><span data-stu-id="cb7a3-120">Help</span></span> | <span data-ttu-id="cb7a3-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="cb7a3-122">列表</span><span class="sxs-lookup"><span data-stu-id="cb7a3-122">List</span></span> | <span data-ttu-id="cb7a3-123">列出在指定的文件夹的位置或与一起使用时的所有文件夹的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="cb7a3-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cb7a3-124">NonInteractive</span></span> | <span data-ttu-id="cb7a3-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cb7a3-126">详细级别</span><span class="sxs-lookup"><span data-stu-id="cb7a3-126">Verbosity</span></span> | <span data-ttu-id="cb7a3-127">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cb7a3-128">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cb7a3-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cb7a3-129">示例</span><span class="sxs-lookup"><span data-stu-id="cb7a3-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="cb7a3-130">有关其他示例，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="cb7a3-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
