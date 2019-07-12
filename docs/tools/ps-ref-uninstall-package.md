---
title: NuGet 卸载包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中卸载程序包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842471"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7729c-103">Uninstall-Package （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="7729c-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7729c-104">*本主题介绍中的命令[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 卸载程序包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="7729c-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7729c-105">从项目中，有选择性地删除其依赖项中删除包。</span><span class="sxs-lookup"><span data-stu-id="7729c-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="7729c-106">如果其他程序包依赖于此包，该命令将失败，除非选项指定了 – Force。</span><span class="sxs-lookup"><span data-stu-id="7729c-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="7729c-107">语法</span><span class="sxs-lookup"><span data-stu-id="7729c-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7729c-108">如果其他程序包依赖于此包，该命令将失败，除非选项指定了 – Force。</span><span class="sxs-lookup"><span data-stu-id="7729c-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="7729c-109">参数</span><span class="sxs-lookup"><span data-stu-id="7729c-109">Parameters</span></span>

| <span data-ttu-id="7729c-110">参数</span><span class="sxs-lookup"><span data-stu-id="7729c-110">Parameter</span></span> | <span data-ttu-id="7729c-111">描述</span><span class="sxs-lookup"><span data-stu-id="7729c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7729c-112">Id</span><span class="sxs-lookup"><span data-stu-id="7729c-112">Id</span></span> | <span data-ttu-id="7729c-113">（必需）要卸载的包的标识符。</span><span class="sxs-lookup"><span data-stu-id="7729c-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="7729c-114">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="7729c-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7729c-115">Version</span><span class="sxs-lookup"><span data-stu-id="7729c-115">Version</span></span> | <span data-ttu-id="7729c-116">若要卸载，包的版本默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="7729c-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7729c-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="7729c-117">RemoveDependencies</span></span> | <span data-ttu-id="7729c-118">卸载程序包及其未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="7729c-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="7729c-119">也就是说，如果任何依赖项具有依赖于它的另一个包，它会跳过。</span><span class="sxs-lookup"><span data-stu-id="7729c-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="7729c-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7729c-120">ProjectName</span></span> | <span data-ttu-id="7729c-121">要从中卸载程序包，默认值为默认项目项目。</span><span class="sxs-lookup"><span data-stu-id="7729c-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7729c-122">强制</span><span class="sxs-lookup"><span data-stu-id="7729c-122">Force</span></span> | <span data-ttu-id="7729c-123">即使其他程序包依赖于它强制要卸载的包。</span><span class="sxs-lookup"><span data-stu-id="7729c-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="7729c-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7729c-124">WhatIf</span></span> | <span data-ttu-id="7729c-125">显示无需实际执行卸载运行命令时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="7729c-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="7729c-126">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="7729c-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7729c-127">通用参数</span><span class="sxs-lookup"><span data-stu-id="7729c-127">Common Parameters</span></span>

<span data-ttu-id="7729c-128">`Uninstall-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="7729c-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7729c-129">示例</span><span class="sxs-lookup"><span data-stu-id="7729c-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
