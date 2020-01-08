---
title: NuGet 查找包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "查找包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384628"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="61539-103">Find-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="61539-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="61539-104">*版本 3.0 +;本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 查找包" 命令，请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="61539-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="61539-105">从包源中获取具有指定 ID 或关键字的一组远程包。</span><span class="sxs-lookup"><span data-stu-id="61539-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="61539-106">语法</span><span class="sxs-lookup"><span data-stu-id="61539-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="61539-107">参数</span><span class="sxs-lookup"><span data-stu-id="61539-107">Parameters</span></span>

| <span data-ttu-id="61539-108">参数</span><span class="sxs-lookup"><span data-stu-id="61539-108">Parameter</span></span> | <span data-ttu-id="61539-109">描述</span><span class="sxs-lookup"><span data-stu-id="61539-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61539-110">Id &lt;关键字&gt;</span><span class="sxs-lookup"><span data-stu-id="61539-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="61539-111">请求搜索包源时要使用的关键字。</span><span class="sxs-lookup"><span data-stu-id="61539-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="61539-112">使用-ExactMatch 仅返回其包 ID 与关键字匹配的那些包。</span><span class="sxs-lookup"><span data-stu-id="61539-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="61539-113">如果未提供任何关键字，`Find-Package` 将返回前20个包的列表（通过下载）或由-First 指定的数字。</span><span class="sxs-lookup"><span data-stu-id="61539-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="61539-114">请注意，-Id 是可选的，而不是操作。</span><span class="sxs-lookup"><span data-stu-id="61539-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="61539-115">Source</span><span class="sxs-lookup"><span data-stu-id="61539-115">Source</span></span> | <span data-ttu-id="61539-116">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="61539-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="61539-117">本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="61539-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="61539-118">如果省略，则 `Find-Package` 搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="61539-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="61539-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="61539-119">AllVersions</span></span> | <span data-ttu-id="61539-120">显示每个包的所有可用版本，而不是仅显示最新版本。</span><span class="sxs-lookup"><span data-stu-id="61539-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="61539-121">First</span><span class="sxs-lookup"><span data-stu-id="61539-121">First</span></span> | <span data-ttu-id="61539-122">要从列表开头返回的包数;默认值为20。</span><span class="sxs-lookup"><span data-stu-id="61539-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="61539-123">Skip</span><span class="sxs-lookup"><span data-stu-id="61539-123">Skip</span></span> | <span data-ttu-id="61539-124">省略所显示列表中的第一个 &lt;int&gt; 包。</span><span class="sxs-lookup"><span data-stu-id="61539-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="61539-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="61539-125">IncludePrerelease</span></span> | <span data-ttu-id="61539-126">在结果中包括预发布包。</span><span class="sxs-lookup"><span data-stu-id="61539-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="61539-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="61539-127">ExactMatch</span></span> | <span data-ttu-id="61539-128">指定为使用 &lt;关键字&gt; 为区分大小写的包 ID。</span><span class="sxs-lookup"><span data-stu-id="61539-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="61539-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="61539-129">StartWith</span></span> | <span data-ttu-id="61539-130">返回包 ID 以 &lt;关键字开头&gt;的包。</span><span class="sxs-lookup"><span data-stu-id="61539-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="61539-131">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="61539-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="61539-132">通用参数</span><span class="sxs-lookup"><span data-stu-id="61539-132">Common Parameters</span></span>

<span data-ttu-id="61539-133">`Find-Package` 支持以下[常见的 PowerShell 参数](https://go.microsoft.com/fwlink/?LinkID=113216)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="61539-133">`Find-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="61539-134">示例</span><span class="sxs-lookup"><span data-stu-id="61539-134">Examples</span></span>

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
