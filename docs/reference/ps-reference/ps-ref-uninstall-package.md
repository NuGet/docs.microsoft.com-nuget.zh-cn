---
title: NuGet 卸载-包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "卸载-包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327274"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="541ba-103">Uninstall-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="541ba-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="541ba-104">*本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 卸载包" 命令, 请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="541ba-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="541ba-105">从项目中删除包, 并可以选择删除其依赖项。</span><span class="sxs-lookup"><span data-stu-id="541ba-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="541ba-106">如果其他包依赖于此包, 则该命令将失败, 除非指定了-Force 选项。</span><span class="sxs-lookup"><span data-stu-id="541ba-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="541ba-107">语法</span><span class="sxs-lookup"><span data-stu-id="541ba-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="541ba-108">如果其他包依赖于此包, 则该命令将失败, 除非指定了-Force 选项。</span><span class="sxs-lookup"><span data-stu-id="541ba-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="541ba-109">参数</span><span class="sxs-lookup"><span data-stu-id="541ba-109">Parameters</span></span>

| <span data-ttu-id="541ba-110">参数</span><span class="sxs-lookup"><span data-stu-id="541ba-110">Parameter</span></span> | <span data-ttu-id="541ba-111">描述</span><span class="sxs-lookup"><span data-stu-id="541ba-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="541ba-112">Id</span><span class="sxs-lookup"><span data-stu-id="541ba-112">Id</span></span> | <span data-ttu-id="541ba-113">请求要卸载的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="541ba-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="541ba-114">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="541ba-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="541ba-115">Version</span><span class="sxs-lookup"><span data-stu-id="541ba-115">Version</span></span> | <span data-ttu-id="541ba-116">要卸载的包的版本, 默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="541ba-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="541ba-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="541ba-117">RemoveDependencies</span></span> | <span data-ttu-id="541ba-118">卸载包及其未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="541ba-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="541ba-119">也就是说, 如果任何依赖项具有依赖于它的其他包, 则会跳过它。</span><span class="sxs-lookup"><span data-stu-id="541ba-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="541ba-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="541ba-120">ProjectName</span></span> | <span data-ttu-id="541ba-121">要从中卸载包的项目, 默认为默认项目。</span><span class="sxs-lookup"><span data-stu-id="541ba-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="541ba-122">团队</span><span class="sxs-lookup"><span data-stu-id="541ba-122">Force</span></span> | <span data-ttu-id="541ba-123">强制卸载包, 即使其他程序包依赖于它。</span><span class="sxs-lookup"><span data-stu-id="541ba-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="541ba-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="541ba-124">WhatIf</span></span> | <span data-ttu-id="541ba-125">显示运行命令时将发生的情况, 但不实际执行卸载。</span><span class="sxs-lookup"><span data-stu-id="541ba-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="541ba-126">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="541ba-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="541ba-127">通用参数</span><span class="sxs-lookup"><span data-stu-id="541ba-127">Common Parameters</span></span>

<span data-ttu-id="541ba-128">`Uninstall-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="541ba-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="541ba-129">示例</span><span class="sxs-lookup"><span data-stu-id="541ba-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
