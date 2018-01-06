---
title: "NuGet Find-package PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: "Visual Studio 中的 NuGet 包管理器控制台中查找包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，查找包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb55cc71e0d4b8eee28b232e64d2cc42364fc153
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="85374-104">查找包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="85374-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="85374-105">*版本 3.0 +;本主题介绍中的命令[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell 查找包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="85374-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="85374-106">从包源中获取具有指定 ID 或关键字的远程程序包集。</span><span class="sxs-lookup"><span data-stu-id="85374-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="85374-107">语法</span><span class="sxs-lookup"><span data-stu-id="85374-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="85374-108">参数</span><span class="sxs-lookup"><span data-stu-id="85374-108">Parameters</span></span>

| <span data-ttu-id="85374-109">参数</span><span class="sxs-lookup"><span data-stu-id="85374-109">Parameter</span></span> | <span data-ttu-id="85374-110">描述</span><span class="sxs-lookup"><span data-stu-id="85374-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85374-111">Id&lt;关键字&gt;</span><span class="sxs-lookup"><span data-stu-id="85374-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="85374-112">（必需）搜索包源时要使用的关键字。</span><span class="sxs-lookup"><span data-stu-id="85374-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="85374-113">使用-ExactMatch 返回其包 ID 和匹配关键字这些包。</span><span class="sxs-lookup"><span data-stu-id="85374-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="85374-114">如果给不出任何关键字，则`Find-Package`返回第一次-指定下载或数量的前 20 个包的列表。</span><span class="sxs-lookup"><span data-stu-id="85374-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="85374-115">注意，-Id 是可选的并且不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="85374-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="85374-116">源</span><span class="sxs-lookup"><span data-stu-id="85374-116">Source</span></span> | <span data-ttu-id="85374-117">要搜索的程序包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="85374-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="85374-118">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="85374-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="85374-119">如果省略，`Find-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="85374-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="85374-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="85374-120">AllVersions</span></span> | <span data-ttu-id="85374-121">显示每个包而不是仅最新版本的所有可用的版本。</span><span class="sxs-lookup"><span data-stu-id="85374-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="85374-122">First</span><span class="sxs-lookup"><span data-stu-id="85374-122">First</span></span> | <span data-ttu-id="85374-123">要从列表中; 的开头返回的程序包数默认值为 20。</span><span class="sxs-lookup"><span data-stu-id="85374-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="85374-124">Skip</span><span class="sxs-lookup"><span data-stu-id="85374-124">Skip</span></span> | <span data-ttu-id="85374-125">省略第一个&lt;int&gt;从列表中显示的包。</span><span class="sxs-lookup"><span data-stu-id="85374-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="85374-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="85374-126">IncludePrerelease</span></span> | <span data-ttu-id="85374-127">在结果中包含预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="85374-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="85374-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="85374-128">ExactMatch</span></span> | <span data-ttu-id="85374-129">指定要使用&lt;关键字&gt;作为区分大小写的包 id。</span><span class="sxs-lookup"><span data-stu-id="85374-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="85374-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="85374-130">StartWith</span></span> | <span data-ttu-id="85374-131">返回包的包 ID 开头&lt;关键字&gt;。</span><span class="sxs-lookup"><span data-stu-id="85374-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="85374-132">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="85374-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="85374-133">通用参数</span><span class="sxs-lookup"><span data-stu-id="85374-133">Common Parameters</span></span>

<span data-ttu-id="85374-134">`Find-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="85374-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="85374-135">示例</span><span class="sxs-lookup"><span data-stu-id="85374-135">Examples</span></span>

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
