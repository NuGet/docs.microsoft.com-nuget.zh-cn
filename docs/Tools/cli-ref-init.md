---
title: NuGet CLI init 命令
description: Nuget.exe init 命令参考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f5e819d014637d1ebb0403d9d838f9362efb20f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="93d16-103">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93d16-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="93d16-104">**适用于：** ，创建包&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="93d16-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="93d16-105">将所有包从平面文件夹都复制到目标文件夹使用层次结构布局，按照所述的[将命令添加](cli-ref-add.md)。</span><span class="sxs-lookup"><span data-stu-id="93d16-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="93d16-106">即，使用`init`相当于使用`add`命令上每个包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="93d16-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="93d16-107">与`add`，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。</span><span class="sxs-lookup"><span data-stu-id="93d16-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="93d16-108">用法</span><span class="sxs-lookup"><span data-stu-id="93d16-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="93d16-109">其中`<source>`是包含包的文件夹和`<destination>`是本地文件夹或包复制到其中的 UNC 路径名。</span><span class="sxs-lookup"><span data-stu-id="93d16-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="93d16-110">选项</span><span class="sxs-lookup"><span data-stu-id="93d16-110">Options</span></span>

| <span data-ttu-id="93d16-111">选项</span><span class="sxs-lookup"><span data-stu-id="93d16-111">Option</span></span> | <span data-ttu-id="93d16-112">描述</span><span class="sxs-lookup"><span data-stu-id="93d16-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93d16-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="93d16-113">ConfigFile</span></span> | <span data-ttu-id="93d16-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="93d16-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="93d16-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="93d16-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="93d16-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="93d16-116">ForceEnglishOutput</span></span> | <span data-ttu-id="93d16-117">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="93d16-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="93d16-118">Expand</span><span class="sxs-lookup"><span data-stu-id="93d16-118">Expand</span></span> | <span data-ttu-id="93d16-119">将所有文件都添加到包源，则添加每个包中与相同`-Expand`与`add`命令。</span><span class="sxs-lookup"><span data-stu-id="93d16-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="93d16-120">帮助</span><span class="sxs-lookup"><span data-stu-id="93d16-120">Help</span></span> | <span data-ttu-id="93d16-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="93d16-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="93d16-122">非交互式</span><span class="sxs-lookup"><span data-stu-id="93d16-122">NonInteractive</span></span> | <span data-ttu-id="93d16-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="93d16-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="93d16-124">详细级别</span><span class="sxs-lookup"><span data-stu-id="93d16-124">Verbosity</span></span> | <span data-ttu-id="93d16-125">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="93d16-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="93d16-126">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="93d16-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="93d16-127">示例</span><span class="sxs-lookup"><span data-stu-id="93d16-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
