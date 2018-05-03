---
title: NuGet 注册 TabExpansion PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中注册 TabExpansion PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="e3b49-103">注册 TabExpansion （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="e3b49-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e3b49-104">*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="e3b49-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e3b49-105">注册指定的命令的参数选项卡扩展，以便使用时选项卡上，输入命令时，扩展的值显示为相关参数的可用选项。</span><span class="sxs-lookup"><span data-stu-id="e3b49-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="e3b49-106">将覆盖任何以前扩展命令。</span><span class="sxs-lookup"><span data-stu-id="e3b49-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="e3b49-107">语法</span><span class="sxs-lookup"><span data-stu-id="e3b49-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e3b49-108">参数</span><span class="sxs-lookup"><span data-stu-id="e3b49-108">Parameters</span></span>

| <span data-ttu-id="e3b49-109">参数</span><span class="sxs-lookup"><span data-stu-id="e3b49-109">Parameter</span></span> | <span data-ttu-id="e3b49-110">描述</span><span class="sxs-lookup"><span data-stu-id="e3b49-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3b49-111">名称</span><span class="sxs-lookup"><span data-stu-id="e3b49-111">Name</span></span> | <span data-ttu-id="e3b49-112">（必需）要注册扩展到该命令。</span><span class="sxs-lookup"><span data-stu-id="e3b49-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="e3b49-113">-Name 是可选的交换机本身。</span><span class="sxs-lookup"><span data-stu-id="e3b49-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="e3b49-114">定义</span><span class="sxs-lookup"><span data-stu-id="e3b49-114">Definition</span></span> | <span data-ttu-id="e3b49-115">（必需）描述在语法中的自变量的对象`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的参数和每个名称`<value>`提供特定的扩展。</span><span class="sxs-lookup"><span data-stu-id="e3b49-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="e3b49-116">接受单引号和双引号。</span><span class="sxs-lookup"><span data-stu-id="e3b49-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="e3b49-117">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="e3b49-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e3b49-118">通用参数</span><span class="sxs-lookup"><span data-stu-id="e3b49-118">Common Parameters</span></span>

<span data-ttu-id="e3b49-119">`Register-TabExpansion` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e3b49-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e3b49-120">示例</span><span class="sxs-lookup"><span data-stu-id="e3b49-120">Examples</span></span>

<span data-ttu-id="e3b49-121">请考虑一个包含三个项目名称 EventManager、 实用程序和 SpecialParser 解决方案。</span><span class="sxs-lookup"><span data-stu-id="e3b49-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="e3b49-122">开发人员经常使用`Update-Package`命令在不同时间与每个这些项目。</span><span class="sxs-lookup"><span data-stu-id="e3b49-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="e3b49-123">她发现方便具有`Update-Package`命令提供的自动完成扩展`-ProjectName`自变量，因此她不需要键入项目名称出每个时间。</span><span class="sxs-lookup"><span data-stu-id="e3b49-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="e3b49-124">以下命令，然后，将这些三个项目名称注册为扩展的`-ProjectName`参数：</span><span class="sxs-lookup"><span data-stu-id="e3b49-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="e3b49-125">开发人员然后可以键入`Update-Package -ProjectName `、 按 tab 键，以及查看作为自动完成选项提供的扩展：</span><span class="sxs-lookup"><span data-stu-id="e3b49-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用注册 TabExpansion 的示例](media/Register-TabExpansion-Example.png)
