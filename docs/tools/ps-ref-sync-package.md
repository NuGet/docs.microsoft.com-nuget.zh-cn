---
title: NuGet 包同步 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中同步包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547989"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="111e7-103">Sync-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="111e7-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="111e7-104">*版本 3.0 + 中;仅在内可用[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="111e7-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="111e7-105">获取从已安装包的版本指定 （或默认值） 项目，并同步到解决方案中项目的其余部分的版本。</span><span class="sxs-lookup"><span data-stu-id="111e7-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="111e7-106">语法</span><span class="sxs-lookup"><span data-stu-id="111e7-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="111e7-107">参数</span><span class="sxs-lookup"><span data-stu-id="111e7-107">Parameters</span></span>

| <span data-ttu-id="111e7-108">参数</span><span class="sxs-lookup"><span data-stu-id="111e7-108">Parameter</span></span> | <span data-ttu-id="111e7-109">描述</span><span class="sxs-lookup"><span data-stu-id="111e7-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="111e7-110">Id</span><span class="sxs-lookup"><span data-stu-id="111e7-110">Id</span></span> | <span data-ttu-id="111e7-111">（必需）要同步的包的标识符。-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="111e7-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="111e7-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="111e7-112">IgnoreDependencies</span></span> | <span data-ttu-id="111e7-113">安装此包仅不及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="111e7-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="111e7-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="111e7-114">ProjectName</span></span> | <span data-ttu-id="111e7-115">要同步中，默认值为默认项目的包的项目。</span><span class="sxs-lookup"><span data-stu-id="111e7-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="111e7-116">版本</span><span class="sxs-lookup"><span data-stu-id="111e7-116">Version</span></span> | <span data-ttu-id="111e7-117">要同步的包的版本默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="111e7-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="111e7-118">源</span><span class="sxs-lookup"><span data-stu-id="111e7-118">Source</span></span> | <span data-ttu-id="111e7-119">要搜索的包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="111e7-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="111e7-120">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="111e7-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="111e7-121">如果省略，`Sync-Package`搜索当前所选的包源。</span><span class="sxs-lookup"><span data-stu-id="111e7-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="111e7-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="111e7-122">IncludePrerelease</span></span> | <span data-ttu-id="111e7-123">在同步中包括预发行包。</span><span class="sxs-lookup"><span data-stu-id="111e7-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="111e7-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="111e7-124">FileConflictAction</span></span> | <span data-ttu-id="111e7-125">当要求您覆盖或忽略现有的项目所引用的文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="111e7-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="111e7-126">可能的值为*覆盖、 忽略、 None、 OverwriteAll*，并 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="111e7-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="111e7-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="111e7-127">DependencyVersion</span></span> | <span data-ttu-id="111e7-128">版本的依赖项包使用，可以是以下值之一：</span><span class="sxs-lookup"><span data-stu-id="111e7-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="111e7-129">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="111e7-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="111e7-130">*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="111e7-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="111e7-131">*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="111e7-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="111e7-132">*最高*（默认值为更新包不带任何参数）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="111e7-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="111e7-133">您可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="111e7-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="111e7-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="111e7-134">WhatIf</span></span> | <span data-ttu-id="111e7-135">显示运行该命令而无需实际执行同步时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="111e7-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="111e7-136">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="111e7-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="111e7-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="111e7-137">Common Parameters</span></span>

<span data-ttu-id="111e7-138">`Sync-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="111e7-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="111e7-139">示例</span><span class="sxs-lookup"><span data-stu-id="111e7-139">Examples</span></span>

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
