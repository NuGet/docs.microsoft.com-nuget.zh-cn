---
title: NuGet CLI init 命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe init 命令参考
keywords: nuget init 引用，init 命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="4b28e-104">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4b28e-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="4b28e-105">**适用于：** ，创建包&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="4b28e-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="4b28e-106">将所有包从平面文件夹都复制到目标文件夹使用层次结构布局，按照所述的[将命令添加](cli-ref-add.md)。</span><span class="sxs-lookup"><span data-stu-id="4b28e-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="4b28e-107">即，使用`init`相当于使用`add`命令上每个包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4b28e-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="4b28e-108">与`add`，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。</span><span class="sxs-lookup"><span data-stu-id="4b28e-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="4b28e-109">用法</span><span class="sxs-lookup"><span data-stu-id="4b28e-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="4b28e-110">其中`<source>`是包含包的文件夹和`<destination>`是本地文件夹或包复制到其中的 UNC 路径名。</span><span class="sxs-lookup"><span data-stu-id="4b28e-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="4b28e-111">选项</span><span class="sxs-lookup"><span data-stu-id="4b28e-111">Options</span></span>

| <span data-ttu-id="4b28e-112">选项</span><span class="sxs-lookup"><span data-stu-id="4b28e-112">Option</span></span> | <span data-ttu-id="4b28e-113">描述</span><span class="sxs-lookup"><span data-stu-id="4b28e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b28e-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4b28e-114">ConfigFile</span></span> | <span data-ttu-id="4b28e-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4b28e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4b28e-116">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="4b28e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4b28e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4b28e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="4b28e-118">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="4b28e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4b28e-119">Expand</span><span class="sxs-lookup"><span data-stu-id="4b28e-119">Expand</span></span> | <span data-ttu-id="4b28e-120">将所有文件都添加到包源，则添加每个包中与相同`-Expand`与`add`命令。</span><span class="sxs-lookup"><span data-stu-id="4b28e-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="4b28e-121">帮助</span><span class="sxs-lookup"><span data-stu-id="4b28e-121">Help</span></span> | <span data-ttu-id="4b28e-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="4b28e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="4b28e-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4b28e-123">NonInteractive</span></span> | <span data-ttu-id="4b28e-124">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="4b28e-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4b28e-125">详细级别</span><span class="sxs-lookup"><span data-stu-id="4b28e-125">Verbosity</span></span> | <span data-ttu-id="4b28e-126">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="4b28e-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4b28e-127">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4b28e-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4b28e-128">示例</span><span class="sxs-lookup"><span data-stu-id="4b28e-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
