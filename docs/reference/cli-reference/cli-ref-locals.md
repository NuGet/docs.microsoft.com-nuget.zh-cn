---
title: NuGet CLI 局部变量命令
description: nuget.exe 局部变量命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779205"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="51014-103"> (NuGet CLI 的局部变量命令) </span><span class="sxs-lookup"><span data-stu-id="51014-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="51014-104">**适用于：** 包使用 &bullet; **受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="51014-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="51014-105">清除或列出本地 NuGet 资源，例如 *http 缓存*、 *全局包* 文件夹和临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="51014-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="51014-106">`locals`命令也可用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="51014-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="51014-107">有关详细信息，请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="51014-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="51014-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="51014-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="51014-109">其中 `<folder>` `all` ，是、 `http-cache` 、 `packages-cache` *(3.5 及更低版本)*、 `global-packages` `temp` *(3.4 +)* 和 `plugins-cache` *(4.8 +)*。</span><span class="sxs-lookup"><span data-stu-id="51014-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="51014-110">选项</span><span class="sxs-lookup"><span data-stu-id="51014-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="51014-111">清除指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="51014-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="51014-112">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="51014-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="51014-113">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="51014-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="51014-114">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="51014-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="51014-115">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="51014-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="51014-116">列出指定文件夹的位置或所有文件夹在与 *all* 一起使用时的位置。</span><span class="sxs-lookup"><span data-stu-id="51014-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="51014-117">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="51014-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="51014-118">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="51014-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="51014-119">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="51014-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="51014-120">示例</span><span class="sxs-lookup"><span data-stu-id="51014-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="51014-121">有关其他示例，请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="51014-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
