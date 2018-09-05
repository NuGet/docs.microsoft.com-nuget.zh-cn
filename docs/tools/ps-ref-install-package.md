---
title: NuGet 安装包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中安装包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546021"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="10bb4-103">Install-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="10bb4-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="10bb4-104">*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 安装包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="10bb4-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="10bb4-105">将包及其依赖项安装到项目。</span><span class="sxs-lookup"><span data-stu-id="10bb4-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="10bb4-106">语法</span><span class="sxs-lookup"><span data-stu-id="10bb4-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="10bb4-107">在 NuGet 2.8 +`Install-Package`将你的项目中的现有包降级。</span><span class="sxs-lookup"><span data-stu-id="10bb4-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="10bb4-108">例如，如果必须安装 Microsoft.AspNet.MVC 5.1.0-rc1，以下命令将降级到 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="10bb4-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="10bb4-109">参数</span><span class="sxs-lookup"><span data-stu-id="10bb4-109">Parameters</span></span>

| <span data-ttu-id="10bb4-110">参数</span><span class="sxs-lookup"><span data-stu-id="10bb4-110">Parameter</span></span> | <span data-ttu-id="10bb4-111">描述</span><span class="sxs-lookup"><span data-stu-id="10bb4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10bb4-112">Id</span><span class="sxs-lookup"><span data-stu-id="10bb4-112">Id</span></span> | <span data-ttu-id="10bb4-113">（必需）要安装的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="10bb4-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="10bb4-114">(*3.0 +*) 的路径或 URL 的标识符可以是`packages.config`文件或`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="10bb4-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="10bb4-115">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="10bb4-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="10bb4-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="10bb4-116">IgnoreDependencies</span></span> | <span data-ttu-id="10bb4-117">安装此包仅不及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="10bb4-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="10bb4-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="10bb4-118">ProjectName</span></span> | <span data-ttu-id="10bb4-119">要在其中安装包，默认值为默认项目项目。</span><span class="sxs-lookup"><span data-stu-id="10bb4-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="10bb4-120">源</span><span class="sxs-lookup"><span data-stu-id="10bb4-120">Source</span></span> | <span data-ttu-id="10bb4-121">要搜索的包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="10bb4-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="10bb4-122">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="10bb4-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="10bb4-123">如果省略，`Install-Package`搜索当前所选的包源。</span><span class="sxs-lookup"><span data-stu-id="10bb4-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="10bb4-124">版本</span><span class="sxs-lookup"><span data-stu-id="10bb4-124">Version</span></span> | <span data-ttu-id="10bb4-125">若要安装，包的版本默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="10bb4-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="10bb4-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="10bb4-126">IncludePrerelease</span></span> | <span data-ttu-id="10bb4-127">考虑安装的预发行包。</span><span class="sxs-lookup"><span data-stu-id="10bb4-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="10bb4-128">如果省略，则被视为仅稳定的包。</span><span class="sxs-lookup"><span data-stu-id="10bb4-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="10bb4-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="10bb4-129">FileConflictAction</span></span> | <span data-ttu-id="10bb4-130">当要求您覆盖或忽略现有的项目所引用的文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="10bb4-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="10bb4-131">可能的值为*覆盖、 忽略、 None、 OverwriteAll*，并 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="10bb4-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="10bb4-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="10bb4-132">DependencyVersion</span></span> | <span data-ttu-id="10bb4-133">版本的依赖项包使用，可以是以下值之一：</span><span class="sxs-lookup"><span data-stu-id="10bb4-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="10bb4-134">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="10bb4-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="10bb4-135">*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="10bb4-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="10bb4-136">*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="10bb4-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="10bb4-137">*最高*（默认值为更新包不带任何参数）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="10bb4-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="10bb4-138">您可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="10bb4-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="10bb4-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="10bb4-139">WhatIf</span></span> | <span data-ttu-id="10bb4-140">显示运行该命令而不实际执行安装时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="10bb4-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="10bb4-141">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="10bb4-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="10bb4-142">通用参数</span><span class="sxs-lookup"><span data-stu-id="10bb4-142">Common Parameters</span></span>

<span data-ttu-id="10bb4-143">`Install-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="10bb4-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="10bb4-144">示例</span><span class="sxs-lookup"><span data-stu-id="10bb4-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
