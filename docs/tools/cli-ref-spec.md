---
title: NuGet CLI spec 命令
description: Nuget.exe spec 命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794146"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="0f3fd-103">spec 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0f3fd-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="0f3fd-104">**适用于：** 创建包&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="0f3fd-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0f3fd-105">生成`.nuspec`新包文件。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="0f3fd-106">如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建已标记化`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="0f3fd-107">有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0f3fd-108">用法</span><span class="sxs-lookup"><span data-stu-id="0f3fd-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="0f3fd-109">其中`<packageID>`是一个可选包标识符，以将保存在`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="0f3fd-110">选项</span><span class="sxs-lookup"><span data-stu-id="0f3fd-110">Options</span></span>

| <span data-ttu-id="0f3fd-111">选项</span><span class="sxs-lookup"><span data-stu-id="0f3fd-111">Option</span></span> | <span data-ttu-id="0f3fd-112">描述</span><span class="sxs-lookup"><span data-stu-id="0f3fd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f3fd-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="0f3fd-113">AssemblyPath</span></span> | <span data-ttu-id="0f3fd-114">指定要用于元数据的程序集的路径。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="0f3fd-115">强制</span><span class="sxs-lookup"><span data-stu-id="0f3fd-115">Force</span></span> | <span data-ttu-id="0f3fd-116">将覆盖任何现有`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="0f3fd-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0f3fd-117">ForceEnglishOutput</span></span> | <span data-ttu-id="0f3fd-118">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0f3fd-119">帮助</span><span class="sxs-lookup"><span data-stu-id="0f3fd-119">Help</span></span> | <span data-ttu-id="0f3fd-120">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="0f3fd-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0f3fd-121">NonInteractive</span></span> | <span data-ttu-id="0f3fd-122">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0f3fd-123">详细级别</span><span class="sxs-lookup"><span data-stu-id="0f3fd-123">Verbosity</span></span> | <span data-ttu-id="0f3fd-124">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="0f3fd-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0f3fd-125">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0f3fd-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0f3fd-126">示例</span><span class="sxs-lookup"><span data-stu-id="0f3fd-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
