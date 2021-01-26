---
title: NuGet Get-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Get-Package PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777491"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a45ff-103">在 Visual Studio 中 Get-Package (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="a45ff-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a45ff-104">*本主题介绍 Windows 上 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内的命令。有关通用 PowerShell Get-Package 命令，请参阅 [PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="a45ff-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="a45ff-105">检索本地存储库中安装的包的列表，列出包源中与-ListAvailable 开关一起使用时可用的包，或在与-Update 开关一起使用时列出可用的更新。</span><span class="sxs-lookup"><span data-stu-id="a45ff-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="a45ff-106">语法</span><span class="sxs-lookup"><span data-stu-id="a45ff-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="a45ff-107">在没有参数的情况下，将 `Get-Package` 显示默认项目中安装的包的列表。</span><span class="sxs-lookup"><span data-stu-id="a45ff-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="a45ff-108">参数</span><span class="sxs-lookup"><span data-stu-id="a45ff-108">Parameters</span></span>

| <span data-ttu-id="a45ff-109">参数</span><span class="sxs-lookup"><span data-stu-id="a45ff-109">Parameter</span></span> | <span data-ttu-id="a45ff-110">说明</span><span class="sxs-lookup"><span data-stu-id="a45ff-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a45ff-111">Source</span><span class="sxs-lookup"><span data-stu-id="a45ff-111">Source</span></span> | <span data-ttu-id="a45ff-112">包的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="a45ff-112">The URL or folder path for the package .</span></span> <span data-ttu-id="a45ff-113">本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="a45ff-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a45ff-114">如果省略，则 `Get-Package` 搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="a45ff-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="a45ff-115">当与-ListAvailable 一起使用时，默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="a45ff-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="a45ff-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="a45ff-116">ListAvailable</span></span> | <span data-ttu-id="a45ff-117">列出包源中可用的包，默认为 nuget.org。显示默认的50包，除非指定了-PageSize 和/或-First。</span><span class="sxs-lookup"><span data-stu-id="a45ff-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="a45ff-118">更新</span><span class="sxs-lookup"><span data-stu-id="a45ff-118">Updates</span></span> | <span data-ttu-id="a45ff-119">列出具有包源中可用更新的包。</span><span class="sxs-lookup"><span data-stu-id="a45ff-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="a45ff-120">项目名称</span><span class="sxs-lookup"><span data-stu-id="a45ff-120">ProjectName</span></span> | <span data-ttu-id="a45ff-121">要从中获取已安装包的项目。</span><span class="sxs-lookup"><span data-stu-id="a45ff-121">The project from which to get installed packages.</span></span> <span data-ttu-id="a45ff-122">如果省略，则返回整个解决方案的已安装项目。</span><span class="sxs-lookup"><span data-stu-id="a45ff-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="a45ff-123">筛选器</span><span class="sxs-lookup"><span data-stu-id="a45ff-123">Filter</span></span> | <span data-ttu-id="a45ff-124">一个筛选器字符串，用于通过将包列表应用到包 ID、说明和标记来缩小包列表范围。</span><span class="sxs-lookup"><span data-stu-id="a45ff-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="a45ff-125">First</span><span class="sxs-lookup"><span data-stu-id="a45ff-125">First</span></span> | <span data-ttu-id="a45ff-126">要从列表开头返回的程序包数。</span><span class="sxs-lookup"><span data-stu-id="a45ff-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="a45ff-127">如果未指定，则默认为50。</span><span class="sxs-lookup"><span data-stu-id="a45ff-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="a45ff-128">跳过</span><span class="sxs-lookup"><span data-stu-id="a45ff-128">Skip</span></span> | <span data-ttu-id="a45ff-129">省略 &lt; &gt; 所显示列表中的第一个 int 包。</span><span class="sxs-lookup"><span data-stu-id="a45ff-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="a45ff-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a45ff-130">AllVersions</span></span> | <span data-ttu-id="a45ff-131">显示每个包的所有可用版本，而不是仅显示最新版本。</span><span class="sxs-lookup"><span data-stu-id="a45ff-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="a45ff-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="a45ff-132">IncludePrerelease</span></span> | <span data-ttu-id="a45ff-133">在结果中包括预发布包。</span><span class="sxs-lookup"><span data-stu-id="a45ff-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="a45ff-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="a45ff-134">PageSize</span></span> | <span data-ttu-id="a45ff-135">*(3.0 +)* 当与-ListAvailable 一起使用时 (需要) ，并在提示继续操作之前列出要列出的包数。</span><span class="sxs-lookup"><span data-stu-id="a45ff-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="a45ff-136">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="a45ff-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a45ff-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="a45ff-137">Common Parameters</span></span>

<span data-ttu-id="a45ff-138">`Get-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="a45ff-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a45ff-139">示例</span><span class="sxs-lookup"><span data-stu-id="a45ff-139">Examples</span></span>

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