---
title: "NuGet 卸载包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Visual Studio 中的 NuGet 包管理器控制台中卸载程序包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，卸载包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9255e-104">卸载程序包 （在 Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="9255e-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9255e-105">*本主题介绍中的命令[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell 卸载程序包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="9255e-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="9255e-106">从项目中，有选择性地删除其依赖项中删除包。</span><span class="sxs-lookup"><span data-stu-id="9255e-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="9255e-107">如果其他程序包依赖于此包，该命令将失败，除非指定选项 – Force。</span><span class="sxs-lookup"><span data-stu-id="9255e-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="9255e-108">语法</span><span class="sxs-lookup"><span data-stu-id="9255e-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9255e-109">如果其他程序包依赖于此包，该命令将失败，除非指定选项 – Force。</span><span class="sxs-lookup"><span data-stu-id="9255e-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="9255e-110">参数</span><span class="sxs-lookup"><span data-stu-id="9255e-110">Parameters</span></span>

| <span data-ttu-id="9255e-111">参数</span><span class="sxs-lookup"><span data-stu-id="9255e-111">Parameter</span></span> | <span data-ttu-id="9255e-112">描述</span><span class="sxs-lookup"><span data-stu-id="9255e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9255e-113">Id</span><span class="sxs-lookup"><span data-stu-id="9255e-113">Id</span></span> | <span data-ttu-id="9255e-114">（必需）要卸载的程序包的标识符。</span><span class="sxs-lookup"><span data-stu-id="9255e-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="9255e-115">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="9255e-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9255e-116">版本</span><span class="sxs-lookup"><span data-stu-id="9255e-116">Version</span></span> | <span data-ttu-id="9255e-117">若要卸载，包的版本默认为当前安装的版本。</span><span class="sxs-lookup"><span data-stu-id="9255e-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="9255e-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="9255e-118">RemoveDependencies</span></span> | <span data-ttu-id="9255e-119">卸载程序包及其未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="9255e-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="9255e-120">也就是说，如果任何依赖关系没有依赖于它的另一个包，它会跳过。</span><span class="sxs-lookup"><span data-stu-id="9255e-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="9255e-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="9255e-121">ProjectName</span></span> | <span data-ttu-id="9255e-122">要从中卸载程序包，对默认项目默认项目。</span><span class="sxs-lookup"><span data-stu-id="9255e-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="9255e-123">强制</span><span class="sxs-lookup"><span data-stu-id="9255e-123">Force</span></span> | <span data-ttu-id="9255e-124">强制包要卸载，即使其他程序包依赖于它。</span><span class="sxs-lookup"><span data-stu-id="9255e-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="9255e-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="9255e-125">WhatIf</span></span> | <span data-ttu-id="9255e-126">显示运行命令而不实际执行卸载时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="9255e-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="9255e-127">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="9255e-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9255e-128">通用参数</span><span class="sxs-lookup"><span data-stu-id="9255e-128">Common Parameters</span></span>

<span data-ttu-id="9255e-129">`Uninstall-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="9255e-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9255e-130">示例</span><span class="sxs-lookup"><span data-stu-id="9255e-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
