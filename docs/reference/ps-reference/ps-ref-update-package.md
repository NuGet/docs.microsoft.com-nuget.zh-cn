---
title: NuGet Update-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Update-Package PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777378"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="69e62-103">在 Visual Studio 中 Update-Package (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="69e62-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="69e62-104">*仅在 Windows 上的 Visual Studio 中的 [NuGet 包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="69e62-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="69e62-105">将包及其依赖项或项目中的所有包更新到较新的版本。</span><span class="sxs-lookup"><span data-stu-id="69e62-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="69e62-106">语法</span><span class="sxs-lookup"><span data-stu-id="69e62-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="69e62-107">在 NuGet 2.8 + 中， `Update-Package` 可以使用来降级项目中的现有包。</span><span class="sxs-lookup"><span data-stu-id="69e62-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="69e62-108">例如，如果安装了 5.1.0-rc1，以下命令会将其降级到5.0.0：</span><span class="sxs-lookup"><span data-stu-id="69e62-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="69e62-109">参数</span><span class="sxs-lookup"><span data-stu-id="69e62-109">Parameters</span></span>

|  <span data-ttu-id="69e62-110">参数</span><span class="sxs-lookup"><span data-stu-id="69e62-110">Parameter</span></span> | <span data-ttu-id="69e62-111">说明</span><span class="sxs-lookup"><span data-stu-id="69e62-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69e62-112">ID</span><span class="sxs-lookup"><span data-stu-id="69e62-112">Id</span></span> | <span data-ttu-id="69e62-113">要更新的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="69e62-113">The identifier of the package to update.</span></span> <span data-ttu-id="69e62-114">如果省略，则更新所有包。</span><span class="sxs-lookup"><span data-stu-id="69e62-114">If omitted, updates all packages.</span></span> <span data-ttu-id="69e62-115">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="69e62-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="69e62-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="69e62-116">IgnoreDependencies</span></span> | <span data-ttu-id="69e62-117">跳过更新包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="69e62-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="69e62-118">项目名称</span><span class="sxs-lookup"><span data-stu-id="69e62-118">ProjectName</span></span> | <span data-ttu-id="69e62-119">包含要更新的包的项目的名称，默认为 "所有项目"。</span><span class="sxs-lookup"><span data-stu-id="69e62-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="69e62-120">版本</span><span class="sxs-lookup"><span data-stu-id="69e62-120">Version</span></span> | <span data-ttu-id="69e62-121">要用于升级的版本，默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="69e62-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="69e62-122">在 NuGet 3.0 + 中，版本值必须是 *最小、最高、HighestMinor* 或 *HighestPatch* (等效于-Safe) 。</span><span class="sxs-lookup"><span data-stu-id="69e62-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="69e62-123">Safe</span><span class="sxs-lookup"><span data-stu-id="69e62-123">Safe</span></span> | <span data-ttu-id="69e62-124">仅将升级限制为与当前安装的包具有相同的主版本和次版本的版本。</span><span class="sxs-lookup"><span data-stu-id="69e62-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="69e62-125">Source</span><span class="sxs-lookup"><span data-stu-id="69e62-125">Source</span></span> | <span data-ttu-id="69e62-126">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="69e62-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="69e62-127">本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="69e62-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="69e62-128">如果省略，则 `Update-Package` 搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="69e62-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="69e62-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="69e62-129">IncludePrerelease</span></span> | <span data-ttu-id="69e62-130">包含更新的预发布包。</span><span class="sxs-lookup"><span data-stu-id="69e62-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="69e62-131">重新安装</span><span class="sxs-lookup"><span data-stu-id="69e62-131">Reinstall</span></span> | <span data-ttu-id="69e62-132">使用当前安装的版本 Resintalls 包。</span><span class="sxs-lookup"><span data-stu-id="69e62-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="69e62-133">请参阅[重新安装和更新包](../../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="69e62-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="69e62-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="69e62-134">FileConflictAction</span></span> | <span data-ttu-id="69e62-135">当要求覆盖或忽略项目引用的现有文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="69e62-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="69e62-136">可能的值包括 *Overwrite、Ignore、None、OverwriteAll* 和 *IgnoreAll* (3.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="69e62-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="69e62-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="69e62-137">DependencyVersion</span></span> | <span data-ttu-id="69e62-138">要使用的依赖项包的版本，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="69e62-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="69e62-139">*最低* (默认) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="69e62-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="69e62-140">*HighestPatch*：最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="69e62-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="69e62-141">*HighestMinor*：最小主要版本号最高的版本，最高修补程序</span><span class="sxs-lookup"><span data-stu-id="69e62-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="69e62-142">不带参数的 Update-Package 的 *最高* (默认值) ：最高版本</span><span class="sxs-lookup"><span data-stu-id="69e62-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="69e62-143">您可以使用文件中的设置设置默认值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="69e62-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="69e62-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="69e62-144">ToHighestPatch</span></span> | <span data-ttu-id="69e62-145">等效于-Safe。</span><span class="sxs-lookup"><span data-stu-id="69e62-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="69e62-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="69e62-146">ToHighestMinor</span></span> | <span data-ttu-id="69e62-147">仅将升级限制为版本与当前安装的包相同的版本。</span><span class="sxs-lookup"><span data-stu-id="69e62-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="69e62-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="69e62-148">WhatIf</span></span> | <span data-ttu-id="69e62-149">显示运行命令时，不实际执行更新的情况。</span><span class="sxs-lookup"><span data-stu-id="69e62-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="69e62-150">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="69e62-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="69e62-151">通用参数</span><span class="sxs-lookup"><span data-stu-id="69e62-151">Common Parameters</span></span>

<span data-ttu-id="69e62-152">`Update-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="69e62-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="69e62-153">示例</span><span class="sxs-lookup"><span data-stu-id="69e62-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
