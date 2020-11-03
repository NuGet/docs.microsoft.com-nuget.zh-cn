---
title: NuGet Uninstall-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Uninstall-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237122"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4924e-103">在 Visual Studio 中 Uninstall-Package (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="4924e-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4924e-104">*本主题介绍 Windows 上 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内的命令。有关通用 PowerShell Uninstall-Package 命令，请参阅 [PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="4924e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4924e-105">从项目中删除包，并可以选择删除其依赖项。</span><span class="sxs-lookup"><span data-stu-id="4924e-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="4924e-106">如果其他程序包依赖于该程序包，则除非指定了 –Force 选项，否则此命令将失败。</span><span class="sxs-lookup"><span data-stu-id="4924e-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="4924e-107">语法</span><span class="sxs-lookup"><span data-stu-id="4924e-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4924e-108">如果其他程序包依赖于该程序包，则除非指定了 –Force 选项，否则此命令将失败。</span><span class="sxs-lookup"><span data-stu-id="4924e-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="4924e-109">parameters</span><span class="sxs-lookup"><span data-stu-id="4924e-109">Parameters</span></span>

| <span data-ttu-id="4924e-110">参数</span><span class="sxs-lookup"><span data-stu-id="4924e-110">Parameter</span></span> | <span data-ttu-id="4924e-111">说明</span><span class="sxs-lookup"><span data-stu-id="4924e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4924e-112">ID</span><span class="sxs-lookup"><span data-stu-id="4924e-112">Id</span></span> | <span data-ttu-id="4924e-113">需要 () 要卸载的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="4924e-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="4924e-114">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="4924e-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4924e-115">版本</span><span class="sxs-lookup"><span data-stu-id="4924e-115">Version</span></span> | <span data-ttu-id="4924e-116">要卸载的包的版本，默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="4924e-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4924e-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="4924e-117">RemoveDependencies</span></span> | <span data-ttu-id="4924e-118">卸载包及其未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4924e-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="4924e-119">也就是说，如果任何依赖项具有依赖于它的其他包，则会跳过它。</span><span class="sxs-lookup"><span data-stu-id="4924e-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="4924e-120">项目名称</span><span class="sxs-lookup"><span data-stu-id="4924e-120">ProjectName</span></span> | <span data-ttu-id="4924e-121">要从中卸载包的项目，默认为默认项目。</span><span class="sxs-lookup"><span data-stu-id="4924e-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="4924e-122">Force</span><span class="sxs-lookup"><span data-stu-id="4924e-122">Force</span></span> | <span data-ttu-id="4924e-123">强制卸载包，即使其他程序包依赖于它。</span><span class="sxs-lookup"><span data-stu-id="4924e-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="4924e-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4924e-124">WhatIf</span></span> | <span data-ttu-id="4924e-125">显示运行命令时将发生的情况，但不实际执行卸载。</span><span class="sxs-lookup"><span data-stu-id="4924e-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="4924e-126">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="4924e-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4924e-127">通用参数</span><span class="sxs-lookup"><span data-stu-id="4924e-127">Common Parameters</span></span>

<span data-ttu-id="4924e-128">`Uninstall-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4924e-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4924e-129">示例</span><span class="sxs-lookup"><span data-stu-id="4924e-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```