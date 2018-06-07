---
title: NuGet CLI 规范命令
description: Nuget.exe spec 命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817081"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="252c3-103">spec 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="252c3-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="252c3-104">**适用于：** ，创建包&bullet;**受支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="252c3-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="252c3-105">生成`.nuspec`新包的文件。</span><span class="sxs-lookup"><span data-stu-id="252c3-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="252c3-106">如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建标记`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="252c3-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="252c3-107">有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="252c3-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="252c3-108">用法</span><span class="sxs-lookup"><span data-stu-id="252c3-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="252c3-109">其中`<packageID>`是一个可选软件包的标识符以保存`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="252c3-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="252c3-110">选项</span><span class="sxs-lookup"><span data-stu-id="252c3-110">Options</span></span>

| <span data-ttu-id="252c3-111">选项</span><span class="sxs-lookup"><span data-stu-id="252c3-111">Option</span></span> | <span data-ttu-id="252c3-112">描述</span><span class="sxs-lookup"><span data-stu-id="252c3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="252c3-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="252c3-113">AssemblyPath</span></span> | <span data-ttu-id="252c3-114">指定要对元数据使用的程序集的路径。</span><span class="sxs-lookup"><span data-stu-id="252c3-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="252c3-115">强制</span><span class="sxs-lookup"><span data-stu-id="252c3-115">Force</span></span> | <span data-ttu-id="252c3-116">将覆盖任何现有`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="252c3-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="252c3-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="252c3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="252c3-118">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="252c3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="252c3-119">帮助</span><span class="sxs-lookup"><span data-stu-id="252c3-119">Help</span></span> | <span data-ttu-id="252c3-120">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="252c3-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="252c3-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="252c3-121">NonInteractive</span></span> | <span data-ttu-id="252c3-122">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="252c3-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="252c3-123">详细级别</span><span class="sxs-lookup"><span data-stu-id="252c3-123">Verbosity</span></span> | <span data-ttu-id="252c3-124">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="252c3-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="252c3-125">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="252c3-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="252c3-126">示例</span><span class="sxs-lookup"><span data-stu-id="252c3-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
