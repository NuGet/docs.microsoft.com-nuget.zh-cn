---
title: NuGet 获取包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "获取包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327344"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="74a3b-103">Get-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="74a3b-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="74a3b-104">*本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 获取包" 命令, 请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="74a3b-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="74a3b-105">检索本地存储库中安装的包的列表, 列出包源中与-ListAvailable 开关一起使用时可用的包, 或在与-Update 开关一起使用时列出可用的更新。</span><span class="sxs-lookup"><span data-stu-id="74a3b-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="74a3b-106">语法</span><span class="sxs-lookup"><span data-stu-id="74a3b-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="74a3b-107">在没有参数的`Get-Package`情况下, 将显示默认项目中安装的包的列表。</span><span class="sxs-lookup"><span data-stu-id="74a3b-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="74a3b-108">参数</span><span class="sxs-lookup"><span data-stu-id="74a3b-108">Parameters</span></span>

| <span data-ttu-id="74a3b-109">参数</span><span class="sxs-lookup"><span data-stu-id="74a3b-109">Parameter</span></span> | <span data-ttu-id="74a3b-110">描述</span><span class="sxs-lookup"><span data-stu-id="74a3b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74a3b-111">Source</span><span class="sxs-lookup"><span data-stu-id="74a3b-111">Source</span></span> | <span data-ttu-id="74a3b-112">包的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="74a3b-112">The URL or folder path for the package .</span></span> <span data-ttu-id="74a3b-113">本地文件夹路径可以是绝对路径, 也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="74a3b-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="74a3b-114">如果省略, `Get-Package`则搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="74a3b-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="74a3b-115">当与-ListAvailable 一起使用时, 默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="74a3b-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="74a3b-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="74a3b-116">ListAvailable</span></span> | <span data-ttu-id="74a3b-117">列出包源中可用的包, 默认为 nuget.org。显示默认的50包, 除非指定了-PageSize 和/或-First。</span><span class="sxs-lookup"><span data-stu-id="74a3b-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="74a3b-118">更新</span><span class="sxs-lookup"><span data-stu-id="74a3b-118">Updates</span></span> | <span data-ttu-id="74a3b-119">列出具有包源中可用更新的包。</span><span class="sxs-lookup"><span data-stu-id="74a3b-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="74a3b-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="74a3b-120">ProjectName</span></span> | <span data-ttu-id="74a3b-121">要从中获取已安装包的项目。</span><span class="sxs-lookup"><span data-stu-id="74a3b-121">The project from which to get installed packages.</span></span> <span data-ttu-id="74a3b-122">如果省略, 则返回整个解决方案的已安装项目。</span><span class="sxs-lookup"><span data-stu-id="74a3b-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="74a3b-123">筛选器</span><span class="sxs-lookup"><span data-stu-id="74a3b-123">Filter</span></span> | <span data-ttu-id="74a3b-124">一个筛选器字符串, 用于通过将包列表应用到包 ID、说明和标记来缩小包列表范围。</span><span class="sxs-lookup"><span data-stu-id="74a3b-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="74a3b-125">第一个</span><span class="sxs-lookup"><span data-stu-id="74a3b-125">First</span></span> | <span data-ttu-id="74a3b-126">要从列表开头返回的程序包数。</span><span class="sxs-lookup"><span data-stu-id="74a3b-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="74a3b-127">如果未指定, 则默认为50。</span><span class="sxs-lookup"><span data-stu-id="74a3b-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="74a3b-128">Skip</span><span class="sxs-lookup"><span data-stu-id="74a3b-128">Skip</span></span> | <span data-ttu-id="74a3b-129">省略所显示&lt;列表&gt;中的第一个 int 包。</span><span class="sxs-lookup"><span data-stu-id="74a3b-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="74a3b-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="74a3b-130">AllVersions</span></span> | <span data-ttu-id="74a3b-131">显示每个包的所有可用版本, 而不是仅显示最新版本。</span><span class="sxs-lookup"><span data-stu-id="74a3b-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="74a3b-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="74a3b-132">IncludePrerelease</span></span> | <span data-ttu-id="74a3b-133">在结果中包括预发布包。</span><span class="sxs-lookup"><span data-stu-id="74a3b-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="74a3b-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="74a3b-134">PageSize</span></span> | <span data-ttu-id="74a3b-135">*(3.0 +)* 当与-ListAvailable (必需) 一起使用时, 会在提示继续操作之前列出要列出的包数。</span><span class="sxs-lookup"><span data-stu-id="74a3b-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="74a3b-136">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="74a3b-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="74a3b-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="74a3b-137">Common Parameters</span></span>

<span data-ttu-id="74a3b-138">`Get-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="74a3b-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="74a3b-139">示例</span><span class="sxs-lookup"><span data-stu-id="74a3b-139">Examples</span></span>

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
