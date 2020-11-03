---
title: NuGet Sync-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Sync-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238044"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5d9ab-103">在 Visual Studio 中 Sync-Package (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="5d9ab-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5d9ab-104">*版本 3.0 +;仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="5d9ab-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5d9ab-105">从指定 (或默认) 项目中获取已安装包的版本，并将该版本同步到解决方案中项目的其余部分。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="5d9ab-106">语法</span><span class="sxs-lookup"><span data-stu-id="5d9ab-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5d9ab-107">parameters</span><span class="sxs-lookup"><span data-stu-id="5d9ab-107">Parameters</span></span>

| <span data-ttu-id="5d9ab-108">参数</span><span class="sxs-lookup"><span data-stu-id="5d9ab-108">Parameter</span></span> | <span data-ttu-id="5d9ab-109">说明</span><span class="sxs-lookup"><span data-stu-id="5d9ab-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d9ab-110">ID</span><span class="sxs-lookup"><span data-stu-id="5d9ab-110">Id</span></span> | <span data-ttu-id="5d9ab-111">需要 () 要同步的包的标识符。-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5d9ab-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5d9ab-112">IgnoreDependencies</span></span> | <span data-ttu-id="5d9ab-113">仅安装此程序包，而不安装其依赖项。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="5d9ab-114">项目名称</span><span class="sxs-lookup"><span data-stu-id="5d9ab-114">ProjectName</span></span> | <span data-ttu-id="5d9ab-115">要从中同步包的项目，默认为默认项目。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="5d9ab-116">版本</span><span class="sxs-lookup"><span data-stu-id="5d9ab-116">Version</span></span> | <span data-ttu-id="5d9ab-117">要同步的包版本，默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="5d9ab-118">源</span><span class="sxs-lookup"><span data-stu-id="5d9ab-118">Source</span></span> | <span data-ttu-id="5d9ab-119">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5d9ab-120">本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5d9ab-121">如果省略，则 `Sync-Package` 搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5d9ab-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5d9ab-122">IncludePrerelease</span></span> | <span data-ttu-id="5d9ab-123">包括同步中的预发行包。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="5d9ab-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5d9ab-124">FileConflictAction</span></span> | <span data-ttu-id="5d9ab-125">当要求覆盖或忽略项目引用的现有文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5d9ab-126">可能的值包括 *Overwrite、Ignore、None、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="5d9ab-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5d9ab-127">DependencyVersion</span></span> | <span data-ttu-id="5d9ab-128">要使用的依赖项包的版本，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="5d9ab-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5d9ab-129">*最低* (默认) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="5d9ab-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5d9ab-130">*HighestPatch* ：最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="5d9ab-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5d9ab-131">*HighestMinor* ：最小主要版本号最高的版本，最高修补程序</span><span class="sxs-lookup"><span data-stu-id="5d9ab-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5d9ab-132">不带参数的 Update-Package 的 *最高* (默认值) ：最高版本</span><span class="sxs-lookup"><span data-stu-id="5d9ab-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5d9ab-133">您可以使用文件中的设置设置默认值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5d9ab-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5d9ab-134">WhatIf</span></span> | <span data-ttu-id="5d9ab-135">显示运行命令时，不实际执行同步的情况。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="5d9ab-136">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5d9ab-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="5d9ab-137">Common Parameters</span></span>

<span data-ttu-id="5d9ab-138">`Sync-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="5d9ab-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5d9ab-139">示例</span><span class="sxs-lookup"><span data-stu-id="5d9ab-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```