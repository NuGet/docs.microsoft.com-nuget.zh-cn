---
title: NuGet CLI 初始化命令
description: Nuget.exe init 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327774"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="d9d0c-103">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d9d0c-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="d9d0c-104">**适用于:** 创建&bullet;包的**支持版本:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="d9d0c-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d9d0c-105">使用 "[添加" 命令](cli-ref-add.md)所述的分层布局, 将平面文件夹中的所有包复制到目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="d9d0c-106">也就是说, 使用`init`等效于对文件夹中的`add`每个包使用命令。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="d9d0c-107">对于`add`, 目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库, 如 nuget.org 或专用服务器。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="d9d0c-108">用法</span><span class="sxs-lookup"><span data-stu-id="d9d0c-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="d9d0c-109">其中`<source>` , 是包含包的文件夹`<destination>` , 是要将包复制到的本地文件夹或 UNC 路径名。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="d9d0c-110">选项</span><span class="sxs-lookup"><span data-stu-id="d9d0c-110">Options</span></span>

| <span data-ttu-id="d9d0c-111">选项</span><span class="sxs-lookup"><span data-stu-id="d9d0c-111">Option</span></span> | <span data-ttu-id="d9d0c-112">描述</span><span class="sxs-lookup"><span data-stu-id="d9d0c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9d0c-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d9d0c-113">ConfigFile</span></span> | <span data-ttu-id="d9d0c-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d9d0c-115">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d9d0c-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d9d0c-116">ForceEnglishOutput</span></span> | <span data-ttu-id="d9d0c-117">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d9d0c-118">Expand</span><span class="sxs-lookup"><span data-stu-id="d9d0c-118">Expand</span></span> | <span data-ttu-id="d9d0c-119">添加添加到包源的每个包中的所有文件;`-Expand` 与`add`命令相同。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="d9d0c-120">Help</span><span class="sxs-lookup"><span data-stu-id="d9d0c-120">Help</span></span> | <span data-ttu-id="d9d0c-121">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d9d0c-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d9d0c-122">NonInteractive</span></span> | <span data-ttu-id="d9d0c-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d9d0c-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d9d0c-124">Verbosity</span></span> | <span data-ttu-id="d9d0c-125">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="d9d0c-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d9d0c-126">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d9d0c-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d9d0c-127">示例</span><span class="sxs-lookup"><span data-stu-id="d9d0c-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
