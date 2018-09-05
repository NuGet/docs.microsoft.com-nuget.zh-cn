---
title: NuGet 更新包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中的更新包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546071"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="49b97-103">Update-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="49b97-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="49b97-104">*仅在内可用[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="49b97-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="49b97-105">更新到较新版本的包和依赖项或在项目中，所有包。</span><span class="sxs-lookup"><span data-stu-id="49b97-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="49b97-106">语法</span><span class="sxs-lookup"><span data-stu-id="49b97-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="49b97-107">在 NuGet 2.8 +`Update-Package`可用于将你的项目中的现有包降级。</span><span class="sxs-lookup"><span data-stu-id="49b97-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="49b97-108">例如，如果必须安装 Microsoft.AspNet.MVC 5.1.0-rc1，以下命令将降级到 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="49b97-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="49b97-109">参数</span><span class="sxs-lookup"><span data-stu-id="49b97-109">Parameters</span></span>

|  <span data-ttu-id="49b97-110">参数</span><span class="sxs-lookup"><span data-stu-id="49b97-110">Parameter</span></span> | <span data-ttu-id="49b97-111">描述</span><span class="sxs-lookup"><span data-stu-id="49b97-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49b97-112">Id</span><span class="sxs-lookup"><span data-stu-id="49b97-112">Id</span></span> | <span data-ttu-id="49b97-113">要更新的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="49b97-113">The identifier of the package to update.</span></span> <span data-ttu-id="49b97-114">如果省略，将更新所有包。</span><span class="sxs-lookup"><span data-stu-id="49b97-114">If omitted, updates all packages.</span></span> <span data-ttu-id="49b97-115">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="49b97-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="49b97-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="49b97-116">IgnoreDependencies</span></span> | <span data-ttu-id="49b97-117">跳过更新包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="49b97-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="49b97-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="49b97-118">ProjectName</span></span> | <span data-ttu-id="49b97-119">包含要更新的包，默认值为所有项目的项目的名称。</span><span class="sxs-lookup"><span data-stu-id="49b97-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="49b97-120">版本</span><span class="sxs-lookup"><span data-stu-id="49b97-120">Version</span></span> | <span data-ttu-id="49b97-121">要用于升级，默认为最新版本的版本。</span><span class="sxs-lookup"><span data-stu-id="49b97-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="49b97-122">在 NuGet 3.0 + 中，版本值必须是之一*最低、 最高、 HighestMinor*，或*HighestPatch* （相当于-安全）。</span><span class="sxs-lookup"><span data-stu-id="49b97-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="49b97-123">安全</span><span class="sxs-lookup"><span data-stu-id="49b97-123">Safe</span></span> | <span data-ttu-id="49b97-124">限制升级到使用相同的主要和次要版本与当前安装的包的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="49b97-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="49b97-125">源</span><span class="sxs-lookup"><span data-stu-id="49b97-125">Source</span></span> | <span data-ttu-id="49b97-126">要搜索的包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="49b97-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="49b97-127">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="49b97-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="49b97-128">如果省略，`Update-Package`搜索当前所选的包源。</span><span class="sxs-lookup"><span data-stu-id="49b97-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="49b97-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="49b97-129">IncludePrerelease</span></span> | <span data-ttu-id="49b97-130">包括预发行包的更新。</span><span class="sxs-lookup"><span data-stu-id="49b97-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="49b97-131">重新安装</span><span class="sxs-lookup"><span data-stu-id="49b97-131">Reinstall</span></span> | <span data-ttu-id="49b97-132">Resintalls 包使用其当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="49b97-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="49b97-133">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="49b97-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="49b97-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="49b97-134">FileConflictAction</span></span> | <span data-ttu-id="49b97-135">当要求您覆盖或忽略现有的项目所引用的文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="49b97-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="49b97-136">可能的值为*覆盖、 忽略、 None、 OverwriteAll*，并*IgnoreAll* （3.0 +）。</span><span class="sxs-lookup"><span data-stu-id="49b97-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="49b97-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="49b97-137">DependencyVersion</span></span> | <span data-ttu-id="49b97-138">版本的依赖项包使用，可以是以下值之一：</span><span class="sxs-lookup"><span data-stu-id="49b97-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="49b97-139">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="49b97-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="49b97-140">*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="49b97-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="49b97-141">*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="49b97-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="49b97-142">*最高*（默认值为更新包不带任何参数）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="49b97-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="49b97-143">您可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="49b97-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="49b97-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="49b97-144">ToHighestPatch</span></span> | <span data-ttu-id="49b97-145">限制为仅使用相同的次要版本与当前安装的包的版本升级。</span><span class="sxs-lookup"><span data-stu-id="49b97-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="49b97-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="49b97-146">ToHighestMinor</span></span> | <span data-ttu-id="49b97-147">限制为仅使用相同的主版本与当前安装的包的版本升级。</span><span class="sxs-lookup"><span data-stu-id="49b97-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="49b97-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="49b97-148">WhatIf</span></span> | <span data-ttu-id="49b97-149">显示无需实际执行更新运行命令时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="49b97-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="49b97-150">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="49b97-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="49b97-151">通用参数</span><span class="sxs-lookup"><span data-stu-id="49b97-151">Common Parameters</span></span>

<span data-ttu-id="49b97-152">`Update-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="49b97-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="49b97-153">示例</span><span class="sxs-lookup"><span data-stu-id="49b97-153">Examples</span></span>

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
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
