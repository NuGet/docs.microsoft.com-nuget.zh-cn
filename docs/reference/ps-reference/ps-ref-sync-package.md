---
title: NuGet 同步-包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的同步包 PowerShell 命令引用。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327304"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ea7d3-103">Sync-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="ea7d3-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ea7d3-104">*版本 3.0 +;仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*</span><span class="sxs-lookup"><span data-stu-id="ea7d3-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ea7d3-105">从指定的 (或默认的) 项目获取已安装包的版本, 并将该版本同步到解决方案中项目的其余部分。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="ea7d3-106">语法</span><span class="sxs-lookup"><span data-stu-id="ea7d3-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ea7d3-107">参数</span><span class="sxs-lookup"><span data-stu-id="ea7d3-107">Parameters</span></span>

| <span data-ttu-id="ea7d3-108">参数</span><span class="sxs-lookup"><span data-stu-id="ea7d3-108">Parameter</span></span> | <span data-ttu-id="ea7d3-109">描述</span><span class="sxs-lookup"><span data-stu-id="ea7d3-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea7d3-110">Id</span><span class="sxs-lookup"><span data-stu-id="ea7d3-110">Id</span></span> | <span data-ttu-id="ea7d3-111">请求要同步的包的标识符。-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ea7d3-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="ea7d3-112">IgnoreDependencies</span></span> | <span data-ttu-id="ea7d3-113">仅安装此程序包, 而不安装其依赖项。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="ea7d3-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ea7d3-114">ProjectName</span></span> | <span data-ttu-id="ea7d3-115">要从中同步包的项目, 默认为默认项目。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="ea7d3-116">Version</span><span class="sxs-lookup"><span data-stu-id="ea7d3-116">Version</span></span> | <span data-ttu-id="ea7d3-117">要同步的包版本, 默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ea7d3-118">Source</span><span class="sxs-lookup"><span data-stu-id="ea7d3-118">Source</span></span> | <span data-ttu-id="ea7d3-119">要搜索的包源的 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ea7d3-120">本地文件夹路径可以是绝对路径, 也可以是相对于当前文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ea7d3-121">如果省略, `Sync-Package`则搜索当前选定的包源。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ea7d3-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ea7d3-122">IncludePrerelease</span></span> | <span data-ttu-id="ea7d3-123">包括同步中的预发行包。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="ea7d3-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ea7d3-124">FileConflictAction</span></span> | <span data-ttu-id="ea7d3-125">当要求覆盖或忽略项目引用的现有文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ea7d3-126">可能的值包括*Overwrite、Ignore、None、OverwriteAll*和 *(3.0 +)* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="ea7d3-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ea7d3-127">DependencyVersion</span></span> | <span data-ttu-id="ea7d3-128">要使用的依赖项包的版本, 可以是下列项之一:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ea7d3-129">*最低*(默认值): 最低版本</span><span class="sxs-lookup"><span data-stu-id="ea7d3-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ea7d3-130">*HighestPatch*: 最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="ea7d3-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ea7d3-131">*HighestMinor*: 最小主要版本号最高的版本, 最高修补程序</span><span class="sxs-lookup"><span data-stu-id="ea7d3-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ea7d3-132">*最高*(不带参数的更新包的默认值): 最高版本</span><span class="sxs-lookup"><span data-stu-id="ea7d3-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="ea7d3-133">您可以使用[`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config`文件中的设置设置默认值。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="ea7d3-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ea7d3-134">WhatIf</span></span> | <span data-ttu-id="ea7d3-135">显示运行命令时, 不实际执行同步的情况。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="ea7d3-136">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ea7d3-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="ea7d3-137">Common Parameters</span></span>

<span data-ttu-id="ea7d3-138">`Sync-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="ea7d3-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ea7d3-139">示例</span><span class="sxs-lookup"><span data-stu-id="ea7d3-139">Examples</span></span>

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
