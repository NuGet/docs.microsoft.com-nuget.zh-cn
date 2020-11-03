---
title: NuGet Find-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Find-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 267dd3eb501cae6e419386a5ca5e0c1ab659f807
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238083"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ece7a-103">在 Visual Studio 中 Find-Package (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="ece7a-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ece7a-104">*版本 3.0 +;本主题介绍 Windows 上 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内的命令。有关通用 PowerShell Find-Package 命令，请参阅 [PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="ece7a-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ece7a-105">从包源中获取具有指定 ID 或关键字的一组远程包。</span><span class="sxs-lookup"><span data-stu-id="ece7a-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="ece7a-106">语法</span><span class="sxs-lookup"><span data-stu-id="ece7a-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ece7a-107">parameters</span><span class="sxs-lookup"><span data-stu-id="ece7a-107">Parameters</span></span>

| <span data-ttu-id="ece7a-108">参数</span><span class="sxs-lookup"><span data-stu-id="ece7a-108">Parameter</span></span> | <span data-ttu-id="ece7a-109">说明</span><span class="sxs-lookup"><span data-stu-id="ece7a-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ece7a-110">Id &lt; 关键字&gt;</span><span class="sxs-lookup"><span data-stu-id="ece7a-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="ece7a-111"> (需要在搜索包源时使用) 关键字。</span><span class="sxs-lookup"><span data-stu-id="ece7a-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="ece7a-112">使用-ExactMatch 仅返回其包 ID 与关键字匹配的那些包。</span><span class="sxs-lookup"><span data-stu-id="ece7a-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="ece7a-113">如果未提供任何关键字，则 `Find-Package` 返回按下载项列出的前20个包的列表，或由-First 指定的数字。</span><span class="sxs-lookup"><span data-stu-id="ece7a-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="ece7a-114">请注意，-Id 是可选的，而不是操作。</span><span class="sxs-lookup"><span data-stu-id="ece7a-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="ece7a-115">源</span><span class="sxs-lookup"><span data-stu-id="ece7a-115">Source</span></span> | <span data-ttu-id="ece7a-116">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="ece7a-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ece7a-117">本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="ece7a-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ece7a-118">如果省略，则 `Find-Package` 搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="ece7a-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ece7a-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ece7a-119">AllVersions</span></span> | <span data-ttu-id="ece7a-120">显示每个包的所有可用版本，而不是仅显示最新版本。</span><span class="sxs-lookup"><span data-stu-id="ece7a-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="ece7a-121">First</span><span class="sxs-lookup"><span data-stu-id="ece7a-121">First</span></span> | <span data-ttu-id="ece7a-122">要从列表开头返回的包数;默认值为20。</span><span class="sxs-lookup"><span data-stu-id="ece7a-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="ece7a-123">跳过</span><span class="sxs-lookup"><span data-stu-id="ece7a-123">Skip</span></span> | <span data-ttu-id="ece7a-124">省略 &lt; &gt; 所显示列表中的第一个 int 包。</span><span class="sxs-lookup"><span data-stu-id="ece7a-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="ece7a-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ece7a-125">IncludePrerelease</span></span> | <span data-ttu-id="ece7a-126">在结果中包括预发布包。</span><span class="sxs-lookup"><span data-stu-id="ece7a-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="ece7a-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="ece7a-127">ExactMatch</span></span> | <span data-ttu-id="ece7a-128">指定使用 &lt; 关键字 &gt; 作为区分大小写的包 ID。</span><span class="sxs-lookup"><span data-stu-id="ece7a-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="ece7a-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="ece7a-129">StartWith</span></span> | <span data-ttu-id="ece7a-130">返回包 ID 以关键字开头的 &lt; 包 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="ece7a-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="ece7a-131">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="ece7a-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ece7a-132">通用参数</span><span class="sxs-lookup"><span data-stu-id="ece7a-132">Common Parameters</span></span>

<span data-ttu-id="ece7a-133">`Find-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="ece7a-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ece7a-134">示例</span><span class="sxs-lookup"><span data-stu-id="ece7a-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```