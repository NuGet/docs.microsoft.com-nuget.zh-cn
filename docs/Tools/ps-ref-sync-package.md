---
title: "NuGet 同步包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio 中的 NuGet 包管理器控制台中同步包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，同步包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ff30b-104">同步包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="ff30b-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ff30b-105">*版本 3.0 +;仅在内可用[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="ff30b-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ff30b-106">获取从安装包的版本指定 （或默认值） 项目，并同步到解决方案中项目的其余部分的版本。</span><span class="sxs-lookup"><span data-stu-id="ff30b-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="ff30b-107">语法</span><span class="sxs-lookup"><span data-stu-id="ff30b-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ff30b-108">参数</span><span class="sxs-lookup"><span data-stu-id="ff30b-108">Parameters</span></span>

| <span data-ttu-id="ff30b-109">参数</span><span class="sxs-lookup"><span data-stu-id="ff30b-109">Parameter</span></span> | <span data-ttu-id="ff30b-110">描述</span><span class="sxs-lookup"><span data-stu-id="ff30b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff30b-111">Id</span><span class="sxs-lookup"><span data-stu-id="ff30b-111">Id</span></span> | <span data-ttu-id="ff30b-112">（必需）要同步的包标识符。-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="ff30b-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ff30b-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="ff30b-113">IgnoreDependencies</span></span> | <span data-ttu-id="ff30b-114">安装仅此包不及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="ff30b-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="ff30b-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ff30b-115">ProjectName</span></span> | <span data-ttu-id="ff30b-116">要同步包从，默认为默认项目的项目。</span><span class="sxs-lookup"><span data-stu-id="ff30b-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="ff30b-117">版本</span><span class="sxs-lookup"><span data-stu-id="ff30b-117">Version</span></span> | <span data-ttu-id="ff30b-118">若要同步，包的版本默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="ff30b-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ff30b-119">源</span><span class="sxs-lookup"><span data-stu-id="ff30b-119">Source</span></span> | <span data-ttu-id="ff30b-120">要搜索的程序包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="ff30b-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ff30b-121">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="ff30b-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ff30b-122">如果省略，`Sync-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="ff30b-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ff30b-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ff30b-123">IncludePrerelease</span></span> | <span data-ttu-id="ff30b-124">在同步中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="ff30b-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="ff30b-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ff30b-125">FileConflictAction</span></span> | <span data-ttu-id="ff30b-126">当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。</span><span class="sxs-lookup"><span data-stu-id="ff30b-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ff30b-127">可能的值为*覆盖，忽略，无、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="ff30b-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="ff30b-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ff30b-128">DependencyVersion</span></span> | <span data-ttu-id="ff30b-129">版本的依赖项包若要使用，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="ff30b-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ff30b-130">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="ff30b-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ff30b-131">*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="ff30b-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ff30b-132">*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="ff30b-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ff30b-133">*最高*（默认值为更新包不带任何参数）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="ff30b-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="ff30b-134">你可以设置默认值使用[ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="ff30b-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="ff30b-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ff30b-135">WhatIf</span></span> | <span data-ttu-id="ff30b-136">显示不实际执行同步运行命令时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="ff30b-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="ff30b-137">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="ff30b-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ff30b-138">通用参数</span><span class="sxs-lookup"><span data-stu-id="ff30b-138">Common Parameters</span></span>

<span data-ttu-id="ff30b-139">`Sync-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="ff30b-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ff30b-140">示例</span><span class="sxs-lookup"><span data-stu-id="ff30b-140">Examples</span></span>

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
