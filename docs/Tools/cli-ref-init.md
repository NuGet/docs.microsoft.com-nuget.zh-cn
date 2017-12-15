---
title: "NuGet CLI init 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Nuget.exe init 命令参考"
keywords: "nuget init 引用，init 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="05f98-104">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="05f98-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="05f98-105">**适用于：** ，创建包&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="05f98-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="05f98-106">将所有包从平面文件夹都复制到目标文件夹使用层次结构布局，按照所述的[将命令添加](#add)上面。</span><span class="sxs-lookup"><span data-stu-id="05f98-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="05f98-107">即，使用`init`相当于使用`add`命令上每个包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="05f98-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="05f98-108">与`add`，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。</span><span class="sxs-lookup"><span data-stu-id="05f98-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="05f98-109">用法</span><span class="sxs-lookup"><span data-stu-id="05f98-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="05f98-110">其中`<source>`是包含包的文件夹和`<destination>`是本地文件夹或包将复制到其中的 UNC 路径名。</span><span class="sxs-lookup"><span data-stu-id="05f98-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="05f98-111">选项</span><span class="sxs-lookup"><span data-stu-id="05f98-111">Options</span></span>

| <span data-ttu-id="05f98-112">选项</span><span class="sxs-lookup"><span data-stu-id="05f98-112">Option</span></span> | <span data-ttu-id="05f98-113">描述</span><span class="sxs-lookup"><span data-stu-id="05f98-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05f98-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="05f98-114">ConfigFile</span></span> | <span data-ttu-id="05f98-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="05f98-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="05f98-116">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="05f98-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="05f98-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="05f98-117">ForceEnglishOutput</span></span> | <span data-ttu-id="05f98-118">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="05f98-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="05f98-119">Expand</span><span class="sxs-lookup"><span data-stu-id="05f98-119">Expand</span></span> | <span data-ttu-id="05f98-120">将所有文件都添加到包源，则添加每个包中与相同`-Expand`与`add`命令。</span><span class="sxs-lookup"><span data-stu-id="05f98-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="05f98-121">帮助</span><span class="sxs-lookup"><span data-stu-id="05f98-121">Help</span></span> | <span data-ttu-id="05f98-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="05f98-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="05f98-123">非交互式</span><span class="sxs-lookup"><span data-stu-id="05f98-123">NonInteractive</span></span> | <span data-ttu-id="05f98-124">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="05f98-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="05f98-125">详细级别</span><span class="sxs-lookup"><span data-stu-id="05f98-125">Verbosity</span></span> | <span data-ttu-id="05f98-126">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="05f98-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="05f98-127">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="05f98-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="05f98-128">示例</span><span class="sxs-lookup"><span data-stu-id="05f98-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
