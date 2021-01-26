---
title: NuGet Register-TabExpansion PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Register-TabExpansion PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777462"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="91f11-103">在 Visual Studio 中 Register-TabExpansion (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="91f11-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="91f11-104">*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="91f11-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="91f11-105">为指定命令的参数注册选项卡扩展，以便在输入命令时使用 Tab 键时，展开的值将显示为相关参数的可用选项。</span><span class="sxs-lookup"><span data-stu-id="91f11-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="91f11-106">将覆盖此命令的任何以前的扩展。</span><span class="sxs-lookup"><span data-stu-id="91f11-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="91f11-107">语法</span><span class="sxs-lookup"><span data-stu-id="91f11-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="91f11-108">参数</span><span class="sxs-lookup"><span data-stu-id="91f11-108">Parameters</span></span>

| <span data-ttu-id="91f11-109">参数</span><span class="sxs-lookup"><span data-stu-id="91f11-109">Parameter</span></span> | <span data-ttu-id="91f11-110">说明</span><span class="sxs-lookup"><span data-stu-id="91f11-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91f11-111">名称</span><span class="sxs-lookup"><span data-stu-id="91f11-111">Name</span></span> | <span data-ttu-id="91f11-112"> (要求) 要注册扩展的命令。</span><span class="sxs-lookup"><span data-stu-id="91f11-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="91f11-113">-Name 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="91f11-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="91f11-114">定义</span><span class="sxs-lookup"><span data-stu-id="91f11-114">Definition</span></span> | <span data-ttu-id="91f11-115"> (必需) 一个对象，该对象描述语法中的参数， `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 其中 `<parameter>` 是要修改的参数的名称，每个参数都 `<value>` 提供特定的扩展。</span><span class="sxs-lookup"><span data-stu-id="91f11-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="91f11-116">同时接受单引号和双引号。</span><span class="sxs-lookup"><span data-stu-id="91f11-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="91f11-117">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="91f11-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="91f11-118">通用参数</span><span class="sxs-lookup"><span data-stu-id="91f11-118">Common Parameters</span></span>

<span data-ttu-id="91f11-119">`Register-TabExpansion` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="91f11-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="91f11-120">示例</span><span class="sxs-lookup"><span data-stu-id="91f11-120">Examples</span></span>

<span data-ttu-id="91f11-121">假设解决方案包含三个项目名称但是、实用工具和 SpecialParser。</span><span class="sxs-lookup"><span data-stu-id="91f11-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="91f11-122">开发人员经常在 `Update-Package` 每个项目中的不同时间使用命令。</span><span class="sxs-lookup"><span data-stu-id="91f11-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="91f11-123">她发现，使用该命令为 `Update-Package` 参数提供自动完成扩展是非常方便的 `-ProjectName` ，因此她每次都不需要键入项目名称。</span><span class="sxs-lookup"><span data-stu-id="91f11-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="91f11-124">然后，下面的命令将这三个项目名称注册为参数的扩展 `-ProjectName` ：</span><span class="sxs-lookup"><span data-stu-id="91f11-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="91f11-125">然后，开发人员可以键入 `Update-Package -ProjectName ` ，按 tab，并查看作为自动完成选项提供的扩展：</span><span class="sxs-lookup"><span data-stu-id="91f11-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用 Register-TabExpansion 的示例](media/Register-TabExpansion-Example.png)