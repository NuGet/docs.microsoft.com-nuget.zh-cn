---
title: NuGet 安装包 PowerShell 参考 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 在 Visual Studio 中的 NuGet 包管理器控制台的安装包 PowerShell 命令参考。
keywords: NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，安装包
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="fc09c-104">安装包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="fc09c-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fc09c-105">*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell Install-package 命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="fc09c-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="fc09c-106">到项目中安装包及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="fc09c-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="fc09c-107">语法</span><span class="sxs-lookup"><span data-stu-id="fc09c-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="fc09c-108">在 NuGet 2.8 +`Install-Package`将你的项目中的现有包降级。</span><span class="sxs-lookup"><span data-stu-id="fc09c-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="fc09c-109">例如，如果你有 Microsoft.AspNet.MVC 5.1.0-rc1 安装，以下命令会将它降级到 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="fc09c-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="fc09c-110">参数</span><span class="sxs-lookup"><span data-stu-id="fc09c-110">Parameters</span></span>

| <span data-ttu-id="fc09c-111">参数</span><span class="sxs-lookup"><span data-stu-id="fc09c-111">Parameter</span></span> | <span data-ttu-id="fc09c-112">描述</span><span class="sxs-lookup"><span data-stu-id="fc09c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc09c-113">Id</span><span class="sxs-lookup"><span data-stu-id="fc09c-113">Id</span></span> | <span data-ttu-id="fc09c-114">（必需）要安装的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="fc09c-114">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="fc09c-115">(*3.0 +*) 路径或 URL，该标识符可以是`packages.config`文件或`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="fc09c-115">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="fc09c-116">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="fc09c-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fc09c-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="fc09c-117">IgnoreDependencies</span></span> | <span data-ttu-id="fc09c-118">安装仅此包不及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="fc09c-118">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="fc09c-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fc09c-119">ProjectName</span></span> | <span data-ttu-id="fc09c-120">要安装包，默认为默认项目到项目。</span><span class="sxs-lookup"><span data-stu-id="fc09c-120">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="fc09c-121">源</span><span class="sxs-lookup"><span data-stu-id="fc09c-121">Source</span></span> | <span data-ttu-id="fc09c-122">要搜索的程序包源 URL 或文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="fc09c-122">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="fc09c-123">本地文件夹路径可以是绝对的或相对于当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="fc09c-123">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="fc09c-124">如果省略，`Install-Package`搜索当前选定的程序包源。</span><span class="sxs-lookup"><span data-stu-id="fc09c-124">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="fc09c-125">版本</span><span class="sxs-lookup"><span data-stu-id="fc09c-125">Version</span></span> | <span data-ttu-id="fc09c-126">若要安装，包的版本默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="fc09c-126">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="fc09c-127">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="fc09c-127">IncludePrerelease</span></span> | <span data-ttu-id="fc09c-128">将安装的预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="fc09c-128">Considers prerelease packages for the install.</span></span> <span data-ttu-id="fc09c-129">如果省略，则考虑仅稳定的程序包。</span><span class="sxs-lookup"><span data-stu-id="fc09c-129">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="fc09c-130">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="fc09c-130">FileConflictAction</span></span> | <span data-ttu-id="fc09c-131">当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。</span><span class="sxs-lookup"><span data-stu-id="fc09c-131">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="fc09c-132">可能的值为*覆盖，忽略，无、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="fc09c-132">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="fc09c-133">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="fc09c-133">DependencyVersion</span></span> | <span data-ttu-id="fc09c-134">版本的依赖项包若要使用，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="fc09c-134">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="fc09c-135">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="fc09c-135">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="fc09c-136">*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="fc09c-136">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="fc09c-137">*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="fc09c-137">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="fc09c-138">*最高*（默认值为更新包不带任何参数）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="fc09c-138">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="fc09c-139">你可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="fc09c-139">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="fc09c-140">WhatIf</span><span class="sxs-lookup"><span data-stu-id="fc09c-140">WhatIf</span></span> | <span data-ttu-id="fc09c-141">显示运行命令而不实际执行安装时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="fc09c-141">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="fc09c-142">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="fc09c-142">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fc09c-143">通用参数</span><span class="sxs-lookup"><span data-stu-id="fc09c-143">Common Parameters</span></span>

<span data-ttu-id="fc09c-144">`Install-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="fc09c-144">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fc09c-145">示例</span><span class="sxs-lookup"><span data-stu-id="fc09c-145">Examples</span></span>

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
