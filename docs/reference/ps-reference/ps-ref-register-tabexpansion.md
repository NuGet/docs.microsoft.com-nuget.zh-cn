---
title: NuGet 注册-Tabexpansion 控制 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 Tabexpansion 控制 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327294"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="e4673-103">Tabexpansion 控制 (Visual Studio 中的包管理器控制台)</span><span class="sxs-lookup"><span data-stu-id="e4673-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e4673-104">*仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*</span><span class="sxs-lookup"><span data-stu-id="e4673-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e4673-105">为指定命令的参数注册选项卡扩展, 以便在输入命令时使用 Tab 键时, 展开的值将显示为相关参数的可用选项。</span><span class="sxs-lookup"><span data-stu-id="e4673-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="e4673-106">将覆盖此命令的任何以前的扩展。</span><span class="sxs-lookup"><span data-stu-id="e4673-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="e4673-107">语法</span><span class="sxs-lookup"><span data-stu-id="e4673-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e4673-108">参数</span><span class="sxs-lookup"><span data-stu-id="e4673-108">Parameters</span></span>

| <span data-ttu-id="e4673-109">参数</span><span class="sxs-lookup"><span data-stu-id="e4673-109">Parameter</span></span> | <span data-ttu-id="e4673-110">描述</span><span class="sxs-lookup"><span data-stu-id="e4673-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4673-111">名称</span><span class="sxs-lookup"><span data-stu-id="e4673-111">Name</span></span> | <span data-ttu-id="e4673-112">请求要向其注册扩展的命令。</span><span class="sxs-lookup"><span data-stu-id="e4673-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="e4673-113">-Name 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="e4673-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="e4673-114">定义</span><span class="sxs-lookup"><span data-stu-id="e4673-114">Definition</span></span> | <span data-ttu-id="e4673-115">请求一个对象, 该对象描述语法`@{'<parameter>' = {'<value1>', '<value2>', ...}}`中的参数, 其中`<parameter>`是要修改的参数的名称`<value>` , 每个参数都提供特定的扩展。</span><span class="sxs-lookup"><span data-stu-id="e4673-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="e4673-116">同时接受单引号和双引号。</span><span class="sxs-lookup"><span data-stu-id="e4673-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="e4673-117">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="e4673-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e4673-118">通用参数</span><span class="sxs-lookup"><span data-stu-id="e4673-118">Common Parameters</span></span>

<span data-ttu-id="e4673-119">`Register-TabExpansion`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e4673-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e4673-120">示例</span><span class="sxs-lookup"><span data-stu-id="e4673-120">Examples</span></span>

<span data-ttu-id="e4673-121">假设解决方案包含三个项目名称但是、实用工具和 SpecialParser。</span><span class="sxs-lookup"><span data-stu-id="e4673-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="e4673-122">开发人员经常在每`Update-Package`个项目中的不同时间使用命令。</span><span class="sxs-lookup"><span data-stu-id="e4673-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="e4673-123">她发现, 使用`Update-Package`该命令为`-ProjectName`参数提供自动完成扩展是非常方便的, 因此她每次都不需要键入项目名称。</span><span class="sxs-lookup"><span data-stu-id="e4673-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="e4673-124">然后, 下面的命令将这三个项目名称注册为`-ProjectName`参数的扩展:</span><span class="sxs-lookup"><span data-stu-id="e4673-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="e4673-125">然后, 开发人员可以`Update-Package -ProjectName `键入, 按 tab, 并查看作为自动完成选项提供的扩展:</span><span class="sxs-lookup"><span data-stu-id="e4673-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用 Tabexpansion 控制的示例](media/Register-TabExpansion-Example.png)
