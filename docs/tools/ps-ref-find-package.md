---
title: NuGet 找到的包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中找到的包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550973"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="39002-103">Find-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="39002-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="39002-104">*版本 3.0 + 中;本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 找到的包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="39002-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="39002-105">包源中获取具有指定 ID 或关键字远程包的集。</span><span class="sxs-lookup"><span data-stu-id="39002-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="39002-106">语法</span><span class="sxs-lookup"><span data-stu-id="39002-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="39002-107">参数</span><span class="sxs-lookup"><span data-stu-id="39002-107">Parameters</span></span>

| <span data-ttu-id="39002-108">参数</span><span class="sxs-lookup"><span data-stu-id="39002-108">Parameter</span></span> | <span data-ttu-id="39002-109">描述</span><span class="sxs-lookup"><span data-stu-id="39002-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39002-110">Id&lt;关键字&gt;</span><span class="sxs-lookup"><span data-stu-id="39002-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="39002-111">（必需）搜索包源时要使用的关键字。</span><span class="sxs-lookup"><span data-stu-id="39002-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="39002-112">使用-ExactMatch 返回关键字匹配的包 ID 这些包。</span><span class="sxs-lookup"><span data-stu-id="39002-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="39002-113">如果不给定了任何关键字，`Find-Package`返回首次为-指定数或下载的前 20 个包的列表。</span><span class="sxs-lookup"><span data-stu-id="39002-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="39002-114">请注意，-Id 是可选的执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="39002-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="39002-115">源</span><span class="sxs-lookup"><span data-stu-id="39002-115">Source</span></span> | <span data-ttu-id="39002-116">要搜索的包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="39002-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="39002-117">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="39002-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="39002-118">如果省略，`Find-Package`搜索当前所选的包源。</span><span class="sxs-lookup"><span data-stu-id="39002-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="39002-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="39002-119">AllVersions</span></span> | <span data-ttu-id="39002-120">显示所有可用版本的每个包而不是仅最新版本。</span><span class="sxs-lookup"><span data-stu-id="39002-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="39002-121">First</span><span class="sxs-lookup"><span data-stu-id="39002-121">First</span></span> | <span data-ttu-id="39002-122">若要从列表中; 开头返回的包数默认值为 20。</span><span class="sxs-lookup"><span data-stu-id="39002-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="39002-123">Skip</span><span class="sxs-lookup"><span data-stu-id="39002-123">Skip</span></span> | <span data-ttu-id="39002-124">省略了第一个&lt;int&gt;显示的列表中的包。</span><span class="sxs-lookup"><span data-stu-id="39002-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="39002-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="39002-125">IncludePrerelease</span></span> | <span data-ttu-id="39002-126">在结果中包括预发行包。</span><span class="sxs-lookup"><span data-stu-id="39002-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="39002-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="39002-127">ExactMatch</span></span> | <span data-ttu-id="39002-128">指定要使用&lt;关键字&gt;作为一个区分大小写的包 id。</span><span class="sxs-lookup"><span data-stu-id="39002-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="39002-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="39002-129">StartWith</span></span> | <span data-ttu-id="39002-130">返回包的包 ID 开头&lt;关键字&gt;。</span><span class="sxs-lookup"><span data-stu-id="39002-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="39002-131">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="39002-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="39002-132">通用参数</span><span class="sxs-lookup"><span data-stu-id="39002-132">Common Parameters</span></span>

<span data-ttu-id="39002-133">`Find-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="39002-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="39002-134">示例</span><span class="sxs-lookup"><span data-stu-id="39002-134">Examples</span></span>

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
