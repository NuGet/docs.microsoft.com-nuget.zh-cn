---
title: NuGet 同步包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中同步包 PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="affb8-103">Sync-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="affb8-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="affb8-104">*版本 3.0 +;仅在内可用[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="affb8-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="affb8-105">获取从安装包的版本指定 （或默认值） 项目，并同步到解决方案中项目的其余部分的版本。</span><span class="sxs-lookup"><span data-stu-id="affb8-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="affb8-106">语法</span><span class="sxs-lookup"><span data-stu-id="affb8-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="affb8-107">参数</span><span class="sxs-lookup"><span data-stu-id="affb8-107">Parameters</span></span>

| <span data-ttu-id="affb8-108">参数</span><span class="sxs-lookup"><span data-stu-id="affb8-108">Parameter</span></span> | <span data-ttu-id="affb8-109">描述</span><span class="sxs-lookup"><span data-stu-id="affb8-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="affb8-110">Id</span><span class="sxs-lookup"><span data-stu-id="affb8-110">Id</span></span> | <span data-ttu-id="affb8-111">（必需）要同步的包标识符。-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="affb8-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="affb8-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="affb8-112">IgnoreDependencies</span></span> | <span data-ttu-id="affb8-113">安装仅此包不及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="affb8-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="affb8-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="affb8-114">ProjectName</span></span> | <span data-ttu-id="affb8-115">要同步包从，默认为默认项目的项目。</span><span class="sxs-lookup"><span data-stu-id="affb8-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="affb8-116">版本</span><span class="sxs-lookup"><span data-stu-id="affb8-116">Version</span></span> | <span data-ttu-id="affb8-117">若要同步，包的版本默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="affb8-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="affb8-118">源</span><span class="sxs-lookup"><span data-stu-id="affb8-118">Source</span></span> | <span data-ttu-id="affb8-119">要搜索的程序包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="affb8-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="affb8-120">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="affb8-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="affb8-121">如果省略，`Sync-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="affb8-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="affb8-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="affb8-122">IncludePrerelease</span></span> | <span data-ttu-id="affb8-123">在同步中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="affb8-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="affb8-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="affb8-124">FileConflictAction</span></span> | <span data-ttu-id="affb8-125">当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。</span><span class="sxs-lookup"><span data-stu-id="affb8-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="affb8-126">可能的值为*覆盖，忽略，无、 OverwriteAll*，和 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="affb8-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="affb8-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="affb8-127">DependencyVersion</span></span> | <span data-ttu-id="affb8-128">版本的依赖项包若要使用，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="affb8-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="affb8-129">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="affb8-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="affb8-130">*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="affb8-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="affb8-131">*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="affb8-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="affb8-132">*最高*（默认值为更新包不带任何参数）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="affb8-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="affb8-133">你可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="affb8-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="affb8-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="affb8-134">WhatIf</span></span> | <span data-ttu-id="affb8-135">显示不实际执行同步运行命令时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="affb8-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="affb8-136">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="affb8-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="affb8-137">通用参数</span><span class="sxs-lookup"><span data-stu-id="affb8-137">Common Parameters</span></span>

<span data-ttu-id="affb8-138">`Sync-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="affb8-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="affb8-139">示例</span><span class="sxs-lookup"><span data-stu-id="affb8-139">Examples</span></span>

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
