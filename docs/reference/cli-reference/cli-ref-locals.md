---
title: NuGet CLI 局部变量命令
description: Nuget.exe 局部变量命令的参考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327804"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="7b5b5-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7b5b5-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="7b5b5-104">**适用于:** 包&bullet;使用**受支持的版本:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="7b5b5-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7b5b5-105">清除或列出本地 NuGet 资源, 例如*http 缓存*、*全局包*文件夹和临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="7b5b5-106">`locals`命令也可用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="7b5b5-107">有关详细信息, 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7b5b5-108">用法</span><span class="sxs-lookup"><span data-stu-id="7b5b5-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="7b5b5-109">其中`<folder>` `all`, 是`plugins-cache` 、 `global-packages` `temp`    、(3.5 及更早版本)、、(3.4 +) 和 (4.8 +) 之一。 `packages-cache` `http-cache`</span><span class="sxs-lookup"><span data-stu-id="7b5b5-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="7b5b5-110">选项</span><span class="sxs-lookup"><span data-stu-id="7b5b5-110">Options</span></span>

| <span data-ttu-id="7b5b5-111">选项</span><span class="sxs-lookup"><span data-stu-id="7b5b5-111">Option</span></span> | <span data-ttu-id="7b5b5-112">描述</span><span class="sxs-lookup"><span data-stu-id="7b5b5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b5b5-113">清除</span><span class="sxs-lookup"><span data-stu-id="7b5b5-113">Clear</span></span> | <span data-ttu-id="7b5b5-114">清除指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="7b5b5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7b5b5-115">ConfigFile</span></span> | <span data-ttu-id="7b5b5-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7b5b5-117">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7b5b5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7b5b5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="7b5b5-119">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7b5b5-120">Help</span><span class="sxs-lookup"><span data-stu-id="7b5b5-120">Help</span></span> | <span data-ttu-id="7b5b5-121">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7b5b5-122">列表</span><span class="sxs-lookup"><span data-stu-id="7b5b5-122">List</span></span> | <span data-ttu-id="7b5b5-123">列出指定文件夹的位置或所有文件夹在与*all*一起使用时的位置。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="7b5b5-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7b5b5-124">NonInteractive</span></span> | <span data-ttu-id="7b5b5-125">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7b5b5-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7b5b5-126">Verbosity</span></span> | <span data-ttu-id="7b5b5-127">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7b5b5-128">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7b5b5-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7b5b5-129">示例</span><span class="sxs-lookup"><span data-stu-id="7b5b5-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="7b5b5-130">有关其他示例, 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7b5b5-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
