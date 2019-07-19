---
title: NuGet 安装包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的安装包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327334"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="575cf-103">Install-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="575cf-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="575cf-104">*本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 安装包" 命令, 请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="575cf-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="575cf-105">将包及其依赖项安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="575cf-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="575cf-106">语法</span><span class="sxs-lookup"><span data-stu-id="575cf-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="575cf-107">在 NuGet 2.8 + 中`Install-Package` , 可以降级项目中的现有包。</span><span class="sxs-lookup"><span data-stu-id="575cf-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="575cf-108">例如, 如果安装了 5.1.0-rc1, 以下命令会将其降级到 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="575cf-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="575cf-109">参数</span><span class="sxs-lookup"><span data-stu-id="575cf-109">Parameters</span></span>

| <span data-ttu-id="575cf-110">参数</span><span class="sxs-lookup"><span data-stu-id="575cf-110">Parameter</span></span> | <span data-ttu-id="575cf-111">描述</span><span class="sxs-lookup"><span data-stu-id="575cf-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="575cf-112">Id</span><span class="sxs-lookup"><span data-stu-id="575cf-112">Id</span></span> | <span data-ttu-id="575cf-113">请求要安装的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="575cf-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="575cf-114">(*3.0 +* )标识符可以是`packages.config`文件`.nupkg`或文件的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="575cf-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="575cf-115">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="575cf-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="575cf-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="575cf-116">IgnoreDependencies</span></span> | <span data-ttu-id="575cf-117">仅安装此程序包, 而不安装其依赖项。</span><span class="sxs-lookup"><span data-stu-id="575cf-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="575cf-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="575cf-118">ProjectName</span></span> | <span data-ttu-id="575cf-119">要在其中安装包的项目, 默认为默认项目。</span><span class="sxs-lookup"><span data-stu-id="575cf-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="575cf-120">Source</span><span class="sxs-lookup"><span data-stu-id="575cf-120">Source</span></span> | <span data-ttu-id="575cf-121">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="575cf-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="575cf-122">本地文件夹路径可以是绝对路径, 也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="575cf-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="575cf-123">如果省略, `Install-Package`则搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="575cf-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="575cf-124">Version</span><span class="sxs-lookup"><span data-stu-id="575cf-124">Version</span></span> | <span data-ttu-id="575cf-125">要安装的包的版本, 默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="575cf-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="575cf-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="575cf-126">IncludePrerelease</span></span> | <span data-ttu-id="575cf-127">考虑安装的预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="575cf-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="575cf-128">如果省略, 则只考虑稳定的包。</span><span class="sxs-lookup"><span data-stu-id="575cf-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="575cf-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="575cf-129">FileConflictAction</span></span> | <span data-ttu-id="575cf-130">当要求覆盖或忽略项目引用的现有文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="575cf-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="575cf-131">可能的值包括*Overwrite、Ignore、None、OverwriteAll*和 *(3.0 +)* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="575cf-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="575cf-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="575cf-132">DependencyVersion</span></span> | <span data-ttu-id="575cf-133">要使用的依赖项包的版本, 可以是下列项之一:</span><span class="sxs-lookup"><span data-stu-id="575cf-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="575cf-134">*最低*(默认值): 最低版本</span><span class="sxs-lookup"><span data-stu-id="575cf-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="575cf-135">*HighestPatch*: 最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="575cf-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="575cf-136">*HighestMinor*: 最小主要版本号最高的版本, 最高修补程序</span><span class="sxs-lookup"><span data-stu-id="575cf-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="575cf-137">*最高*(不带参数的更新包的默认值): 最高版本</span><span class="sxs-lookup"><span data-stu-id="575cf-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="575cf-138">您可以使用[`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config`文件中的设置设置默认值。</span><span class="sxs-lookup"><span data-stu-id="575cf-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="575cf-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="575cf-139">WhatIf</span></span> | <span data-ttu-id="575cf-140">显示运行命令时, 如果不实际执行安装, 会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="575cf-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="575cf-141">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="575cf-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="575cf-142">通用参数</span><span class="sxs-lookup"><span data-stu-id="575cf-142">Common Parameters</span></span>

<span data-ttu-id="575cf-143">`Install-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="575cf-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="575cf-144">示例</span><span class="sxs-lookup"><span data-stu-id="575cf-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
