---
title: NuGet CLI 规范命令
description: Nuget.exe 规范命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327564"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="0eb3d-103">spec 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0eb3d-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="0eb3d-104">**适用于:** 创建&bullet;包的**支持版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="0eb3d-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0eb3d-105">为新包生成文件。`.nuspec`</span><span class="sxs-lookup"><span data-stu-id="0eb3d-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="0eb3d-106">如果在与项目文件相同的文件夹中运行 (`.csproj`、 `.vbproj`、 `.fsproj`), `spec`则将创建`.nuspec`一个标记化文件。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="0eb3d-107">有关其他信息, 请参阅[创建包](../../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0eb3d-108">用法</span><span class="sxs-lookup"><span data-stu-id="0eb3d-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="0eb3d-109">其中`<packageID>`是要保存到`.nuspec`文件中的可选包标识符。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="0eb3d-110">选项</span><span class="sxs-lookup"><span data-stu-id="0eb3d-110">Options</span></span>

| <span data-ttu-id="0eb3d-111">选项</span><span class="sxs-lookup"><span data-stu-id="0eb3d-111">Option</span></span> | <span data-ttu-id="0eb3d-112">描述</span><span class="sxs-lookup"><span data-stu-id="0eb3d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0eb3d-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="0eb3d-113">AssemblyPath</span></span> | <span data-ttu-id="0eb3d-114">指定要用于元数据的程序集的路径。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="0eb3d-115">团队</span><span class="sxs-lookup"><span data-stu-id="0eb3d-115">Force</span></span> | <span data-ttu-id="0eb3d-116">覆盖任何现有`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="0eb3d-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0eb3d-117">ForceEnglishOutput</span></span> | <span data-ttu-id="0eb3d-118">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0eb3d-119">Help</span><span class="sxs-lookup"><span data-stu-id="0eb3d-119">Help</span></span> | <span data-ttu-id="0eb3d-120">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="0eb3d-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0eb3d-121">NonInteractive</span></span> | <span data-ttu-id="0eb3d-122">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0eb3d-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0eb3d-123">Verbosity</span></span> | <span data-ttu-id="0eb3d-124">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="0eb3d-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0eb3d-125">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0eb3d-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0eb3d-126">示例</span><span class="sxs-lookup"><span data-stu-id="0eb3d-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
