---
title: NuGet 包获取 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中获取包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842507"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="41e9e-103">Get-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="41e9e-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="41e9e-104">*本主题介绍中的命令[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell Get-package 命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="41e9e-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="41e9e-105">检索安装在本地存储库中的包的列表，列出了与-ListAvailable 开关一起使用时的包源中可用的包或列出与-更新开关一起使用时可用的更新。</span><span class="sxs-lookup"><span data-stu-id="41e9e-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="41e9e-106">语法</span><span class="sxs-lookup"><span data-stu-id="41e9e-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="41e9e-107">不带任何参数，`Get-Package`显示的默认项目中安装的包的列表。</span><span class="sxs-lookup"><span data-stu-id="41e9e-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="41e9e-108">参数</span><span class="sxs-lookup"><span data-stu-id="41e9e-108">Parameters</span></span>

| <span data-ttu-id="41e9e-109">参数</span><span class="sxs-lookup"><span data-stu-id="41e9e-109">Parameter</span></span> | <span data-ttu-id="41e9e-110">描述</span><span class="sxs-lookup"><span data-stu-id="41e9e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41e9e-111">Source</span><span class="sxs-lookup"><span data-stu-id="41e9e-111">Source</span></span> | <span data-ttu-id="41e9e-112">包的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="41e9e-112">The URL or folder path for the package .</span></span> <span data-ttu-id="41e9e-113">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="41e9e-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="41e9e-114">如果省略，`Get-Package`搜索当前所选的包源。</span><span class="sxs-lookup"><span data-stu-id="41e9e-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="41e9e-115">与-ListAvailable，一起使用时默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="41e9e-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="41e9e-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="41e9e-116">ListAvailable</span></span> | <span data-ttu-id="41e9e-117">列出了默认值为 nuget.org 的包源中可用的包。除非另有指定的 PageSize 和/或-第一个显示默认值为 50 的包。</span><span class="sxs-lookup"><span data-stu-id="41e9e-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="41e9e-118">更新</span><span class="sxs-lookup"><span data-stu-id="41e9e-118">Updates</span></span> | <span data-ttu-id="41e9e-119">列出包源中有可用更新的包。</span><span class="sxs-lookup"><span data-stu-id="41e9e-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="41e9e-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="41e9e-120">ProjectName</span></span> | <span data-ttu-id="41e9e-121">获取已安装的包的项目。</span><span class="sxs-lookup"><span data-stu-id="41e9e-121">The project from which to get installed packages.</span></span> <span data-ttu-id="41e9e-122">如果省略，则返回安装整个解决方案的项目。</span><span class="sxs-lookup"><span data-stu-id="41e9e-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="41e9e-123">筛选器</span><span class="sxs-lookup"><span data-stu-id="41e9e-123">Filter</span></span> | <span data-ttu-id="41e9e-124">用来将其应用到包 ID、 说明和标记来缩小包列表的筛选器字符串。</span><span class="sxs-lookup"><span data-stu-id="41e9e-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="41e9e-125">第一个</span><span class="sxs-lookup"><span data-stu-id="41e9e-125">First</span></span> | <span data-ttu-id="41e9e-126">若要从列表开头返回的包数。</span><span class="sxs-lookup"><span data-stu-id="41e9e-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="41e9e-127">如果未指定，默认为 50。</span><span class="sxs-lookup"><span data-stu-id="41e9e-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="41e9e-128">Skip</span><span class="sxs-lookup"><span data-stu-id="41e9e-128">Skip</span></span> | <span data-ttu-id="41e9e-129">省略了第一个&lt;int&gt;显示的列表中的包。</span><span class="sxs-lookup"><span data-stu-id="41e9e-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="41e9e-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="41e9e-130">AllVersions</span></span> | <span data-ttu-id="41e9e-131">显示所有可用版本的每个包而不是仅最新版本。</span><span class="sxs-lookup"><span data-stu-id="41e9e-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="41e9e-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="41e9e-132">IncludePrerelease</span></span> | <span data-ttu-id="41e9e-133">在结果中包括预发行包。</span><span class="sxs-lookup"><span data-stu-id="41e9e-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="41e9e-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="41e9e-134">PageSize</span></span> | <span data-ttu-id="41e9e-135">*（3.0 +)* 与一起使用时-ListAvailable （必需），包的数量以列出提供提示以继续之前。</span><span class="sxs-lookup"><span data-stu-id="41e9e-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="41e9e-136">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="41e9e-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="41e9e-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="41e9e-137">Common Parameters</span></span>

<span data-ttu-id="41e9e-138">`Get-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="41e9e-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="41e9e-139">示例</span><span class="sxs-lookup"><span data-stu-id="41e9e-139">Examples</span></span>

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
