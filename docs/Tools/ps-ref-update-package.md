---
title: "NuGet 更新包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "在 Visual Studio 中的 NuGet 包管理器控制台中的更新包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，更新包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="56e0c-104">更新包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="56e0c-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="56e0c-105">*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="56e0c-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="56e0c-106">更新到较新版本的包和其依赖项或在项目中，所有包。</span><span class="sxs-lookup"><span data-stu-id="56e0c-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="56e0c-107">语法</span><span class="sxs-lookup"><span data-stu-id="56e0c-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="56e0c-108">在 NuGet 2.8 +`Update-Package`可用来将你的项目中的现有包降级。</span><span class="sxs-lookup"><span data-stu-id="56e0c-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="56e0c-109">例如，如果你有 Microsoft.AspNet.MVC 5.1.0-rc1 安装，以下命令会将它降级到 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="56e0c-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="56e0c-110">参数</span><span class="sxs-lookup"><span data-stu-id="56e0c-110">Parameters</span></span>

|  <span data-ttu-id="56e0c-111">参数</span><span class="sxs-lookup"><span data-stu-id="56e0c-111">Parameter</span></span> | <span data-ttu-id="56e0c-112">描述</span><span class="sxs-lookup"><span data-stu-id="56e0c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="56e0c-113">Id</span><span class="sxs-lookup"><span data-stu-id="56e0c-113">Id</span></span> | <span data-ttu-id="56e0c-114">要更新的包标识符。</span><span class="sxs-lookup"><span data-stu-id="56e0c-114">The identifier of the package to update.</span></span> <span data-ttu-id="56e0c-115">如果省略，则更新所有包。</span><span class="sxs-lookup"><span data-stu-id="56e0c-115">If omitted, updates all packages.</span></span> <span data-ttu-id="56e0c-116">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="56e0c-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="56e0c-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="56e0c-117">IgnoreDependencies</span></span> | <span data-ttu-id="56e0c-118">跳过更新包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="56e0c-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="56e0c-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="56e0c-119">ProjectName</span></span> | <span data-ttu-id="56e0c-120">项目包含要更新的包，将使用默认值的所有项目的名称。</span><span class="sxs-lookup"><span data-stu-id="56e0c-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="56e0c-121">版本</span><span class="sxs-lookup"><span data-stu-id="56e0c-121">Version</span></span> | <span data-ttu-id="56e0c-122">要用于升级，默认为最新版本的版本。</span><span class="sxs-lookup"><span data-stu-id="56e0c-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="56e0c-123">NuGet 3.0 + 中的版本值必须是之一*最低、 最高、 HighestMinor*，或*HighestPatch* （等效于-安全）。</span><span class="sxs-lookup"><span data-stu-id="56e0c-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="56e0c-124">安全</span><span class="sxs-lookup"><span data-stu-id="56e0c-124">Safe</span></span> | <span data-ttu-id="56e0c-125">将使用相同的主要和次要版本与当前安装的包的唯一版本升级的约束。</span><span class="sxs-lookup"><span data-stu-id="56e0c-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="56e0c-126">源</span><span class="sxs-lookup"><span data-stu-id="56e0c-126">Source</span></span> | <span data-ttu-id="56e0c-127">要搜索的程序包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="56e0c-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="56e0c-128">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="56e0c-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="56e0c-129">如果省略，`Uninstall-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="56e0c-129">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="56e0c-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="56e0c-130">IncludePrerelease</span></span> | <span data-ttu-id="56e0c-131">包括预发行程序包更新。</span><span class="sxs-lookup"><span data-stu-id="56e0c-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="56e0c-132">重新安装</span><span class="sxs-lookup"><span data-stu-id="56e0c-132">Reinstall</span></span> | <span data-ttu-id="56e0c-133">Resintalls 使用其当前安装的版本包。</span><span class="sxs-lookup"><span data-stu-id="56e0c-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="56e0c-134">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="56e0c-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="56e0c-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="56e0c-135">FileConflictAction</span></span> | <span data-ttu-id="56e0c-136">当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。</span><span class="sxs-lookup"><span data-stu-id="56e0c-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="56e0c-137">可能的值为*覆盖，忽略，无、 OverwriteAll*，和*IgnoreAll* （3.0 +）。</span><span class="sxs-lookup"><span data-stu-id="56e0c-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="56e0c-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="56e0c-138">DependencyVersion</span></span> | <span data-ttu-id="56e0c-139">版本的依赖项包若要使用，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="56e0c-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="56e0c-140">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="56e0c-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="56e0c-141">*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="56e0c-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="56e0c-142">*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="56e0c-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="56e0c-143">*最高*（默认值为更新包不带任何参数）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="56e0c-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="56e0c-144">你可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="56e0c-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="56e0c-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="56e0c-145">ToHighestPatch</span></span> | <span data-ttu-id="56e0c-146">将仅使用相同的次要版本与当前安装的包的版本升级的约束。</span><span class="sxs-lookup"><span data-stu-id="56e0c-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="56e0c-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="56e0c-147">ToHighestMinor</span></span> | <span data-ttu-id="56e0c-148">将仅使用相同的主要版本与当前安装的包的版本升级的约束。</span><span class="sxs-lookup"><span data-stu-id="56e0c-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="56e0c-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="56e0c-149">WhatIf</span></span> | <span data-ttu-id="56e0c-150">显示不实际执行更新运行命令时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="56e0c-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="56e0c-151">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="56e0c-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="56e0c-152">通用参数</span><span class="sxs-lookup"><span data-stu-id="56e0c-152">Common Parameters</span></span>

<span data-ttu-id="56e0c-153">`Update-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="56e0c-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="56e0c-154">示例</span><span class="sxs-lookup"><span data-stu-id="56e0c-154">Examples</span></span>

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