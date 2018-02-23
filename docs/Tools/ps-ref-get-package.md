---
title: "NuGet Get 包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "在 Visual Studio 中的 NuGet 包管理器控制台中的 Get 包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，Get 包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 01a874ce9ae59dcaeb696a45f23cc5e9f2cfa251
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="237b2-104">获取包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="237b2-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="237b2-105">*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell Get 包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="237b2-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="237b2-106">检索包安装在本地存储库的列表，列出从包源与-ListAvailable 开关一起使用时可用的包或列出可用的更新与-更新开关一起使用时。</span><span class="sxs-lookup"><span data-stu-id="237b2-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="237b2-107">语法</span><span class="sxs-lookup"><span data-stu-id="237b2-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="237b2-108">不带任何参数，`Get-Package`显示的默认项目中安装的程序包的列表。</span><span class="sxs-lookup"><span data-stu-id="237b2-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="237b2-109">参数</span><span class="sxs-lookup"><span data-stu-id="237b2-109">Parameters</span></span>

| <span data-ttu-id="237b2-110">参数</span><span class="sxs-lookup"><span data-stu-id="237b2-110">Parameter</span></span> | <span data-ttu-id="237b2-111">描述</span><span class="sxs-lookup"><span data-stu-id="237b2-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="237b2-112">源</span><span class="sxs-lookup"><span data-stu-id="237b2-112">Source</span></span> | <span data-ttu-id="237b2-113">包的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="237b2-113">The URL or folder path for the package .</span></span> <span data-ttu-id="237b2-114">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="237b2-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="237b2-115">如果省略，`Get-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="237b2-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="237b2-116">如果与-ListAvailable 一起，默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="237b2-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="237b2-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="237b2-117">ListAvailable</span></span> | <span data-ttu-id="237b2-118">列出从包源，默认为 nuget.org 可用的包。除非指定的 PageSize 和/或-第一个，则显示默认值为 50 的包。</span><span class="sxs-lookup"><span data-stu-id="237b2-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="237b2-119">更新</span><span class="sxs-lookup"><span data-stu-id="237b2-119">Updates</span></span> | <span data-ttu-id="237b2-120">列出程序包源中具有更新的包。</span><span class="sxs-lookup"><span data-stu-id="237b2-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="237b2-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="237b2-121">ProjectName</span></span> | <span data-ttu-id="237b2-122">从中获取已安装的软件包项目。</span><span class="sxs-lookup"><span data-stu-id="237b2-122">The project from which to get installed packages.</span></span> <span data-ttu-id="237b2-123">如果省略，则返回安装整个解决方案的项目。</span><span class="sxs-lookup"><span data-stu-id="237b2-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="237b2-124">筛选器</span><span class="sxs-lookup"><span data-stu-id="237b2-124">Filter</span></span> | <span data-ttu-id="237b2-125">用于通过将其应用到包 ID、 说明和标记缩小的包列表的筛选器字符串。</span><span class="sxs-lookup"><span data-stu-id="237b2-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="237b2-126">First</span><span class="sxs-lookup"><span data-stu-id="237b2-126">First</span></span> | <span data-ttu-id="237b2-127">要从列表的开头返回的程序包数。</span><span class="sxs-lookup"><span data-stu-id="237b2-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="237b2-128">如果未指定，默认为 50。</span><span class="sxs-lookup"><span data-stu-id="237b2-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="237b2-129">Skip</span><span class="sxs-lookup"><span data-stu-id="237b2-129">Skip</span></span> | <span data-ttu-id="237b2-130">省略第一个&lt;int&gt;从列表中显示的包。</span><span class="sxs-lookup"><span data-stu-id="237b2-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="237b2-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="237b2-131">AllVersions</span></span> | <span data-ttu-id="237b2-132">显示每个包而不是仅最新版本的所有可用的版本。</span><span class="sxs-lookup"><span data-stu-id="237b2-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="237b2-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="237b2-133">IncludePrerelease</span></span> | <span data-ttu-id="237b2-134">在结果中包含预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="237b2-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="237b2-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="237b2-135">PageSize</span></span> | <span data-ttu-id="237b2-136">*（3.0 +)*时与-ListAvailable 一起 （必需） 的包的数量来授予提示是否继续前列表。</span><span class="sxs-lookup"><span data-stu-id="237b2-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="237b2-137">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="237b2-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="237b2-138">通用参数</span><span class="sxs-lookup"><span data-stu-id="237b2-138">Common Parameters</span></span>

<span data-ttu-id="237b2-139">`Get-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="237b2-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="237b2-140">示例</span><span class="sxs-lookup"><span data-stu-id="237b2-140">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
