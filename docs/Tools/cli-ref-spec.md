---
title: "NuGet CLI 规范命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe spec 命令参考"
keywords: "nuget 规范引用、 spec 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a44ba-104">spec 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a44ba-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a44ba-105">**适用于：** ，创建包&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="a44ba-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a44ba-106">生成`.nuspec`新包的文件。</span><span class="sxs-lookup"><span data-stu-id="a44ba-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a44ba-107">如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建标记`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="a44ba-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a44ba-108">有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ba-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a44ba-109">用法</span><span class="sxs-lookup"><span data-stu-id="a44ba-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a44ba-110">其中`<packageID>`是一个可选软件包的标识符以保存`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="a44ba-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a44ba-111">选项</span><span class="sxs-lookup"><span data-stu-id="a44ba-111">Options</span></span>

| <span data-ttu-id="a44ba-112">选项</span><span class="sxs-lookup"><span data-stu-id="a44ba-112">Option</span></span> | <span data-ttu-id="a44ba-113">描述</span><span class="sxs-lookup"><span data-stu-id="a44ba-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a44ba-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a44ba-114">AssemblyPath</span></span> | <span data-ttu-id="a44ba-115">指定要对元数据使用的程序集的路径。</span><span class="sxs-lookup"><span data-stu-id="a44ba-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a44ba-116">强制</span><span class="sxs-lookup"><span data-stu-id="a44ba-116">Force</span></span> | <span data-ttu-id="a44ba-117">将覆盖任何现有`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="a44ba-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a44ba-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a44ba-118">ForceEnglishOutput</span></span> | <span data-ttu-id="a44ba-119">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="a44ba-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a44ba-120">帮助</span><span class="sxs-lookup"><span data-stu-id="a44ba-120">Help</span></span> | <span data-ttu-id="a44ba-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="a44ba-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a44ba-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a44ba-122">NonInteractive</span></span> | <span data-ttu-id="a44ba-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="a44ba-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a44ba-124">详细级别</span><span class="sxs-lookup"><span data-stu-id="a44ba-124">Verbosity</span></span> | <span data-ttu-id="a44ba-125">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="a44ba-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a44ba-126">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a44ba-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a44ba-127">示例</span><span class="sxs-lookup"><span data-stu-id="a44ba-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
