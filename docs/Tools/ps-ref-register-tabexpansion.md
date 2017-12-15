---
title: "NuGet 注册 TabExpansion PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8314ec69-ee8c-4933-84ef-e6d8a412d268
description: "Visual Studio 中的 NuGet 包管理器控制台中注册 TabExpansion PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，注册 TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 498b8638c81b800e5f20f7604b36e6af76da0283
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="4d33e-104">注册 TabExpansion （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="4d33e-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4d33e-105">*仅在内可用[NuGet 程序包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="4d33e-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4d33e-106">注册指定的命令的参数选项卡扩展，以便使用时选项卡上，输入命令时，扩展的值显示为相关参数的可用选项。</span><span class="sxs-lookup"><span data-stu-id="4d33e-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="4d33e-107">将覆盖任何以前扩展命令。</span><span class="sxs-lookup"><span data-stu-id="4d33e-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d33e-108">语法</span><span class="sxs-lookup"><span data-stu-id="4d33e-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4d33e-109">参数</span><span class="sxs-lookup"><span data-stu-id="4d33e-109">Parameters</span></span>

| <span data-ttu-id="4d33e-110">参数</span><span class="sxs-lookup"><span data-stu-id="4d33e-110">Parameter</span></span> | <span data-ttu-id="4d33e-111">描述</span><span class="sxs-lookup"><span data-stu-id="4d33e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d33e-112">名称</span><span class="sxs-lookup"><span data-stu-id="4d33e-112">Name</span></span> | <span data-ttu-id="4d33e-113">（必需）要注册扩展到该命令。</span><span class="sxs-lookup"><span data-stu-id="4d33e-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="4d33e-114">-Name 是可选的交换机本身。</span><span class="sxs-lookup"><span data-stu-id="4d33e-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="4d33e-115">定义</span><span class="sxs-lookup"><span data-stu-id="4d33e-115">Definition</span></span> | <span data-ttu-id="4d33e-116">（必需）描述在语法中的自变量的对象`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的参数和每个名称`<value>`提供特定的扩展。</span><span class="sxs-lookup"><span data-stu-id="4d33e-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="4d33e-117">接受单引号和双引号。</span><span class="sxs-lookup"><span data-stu-id="4d33e-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="4d33e-118">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="4d33e-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4d33e-119">通用参数</span><span class="sxs-lookup"><span data-stu-id="4d33e-119">Common Parameters</span></span>

<span data-ttu-id="4d33e-120">`Register-TabExpansion`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4d33e-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4d33e-121">示例</span><span class="sxs-lookup"><span data-stu-id="4d33e-121">Examples</span></span>

<span data-ttu-id="4d33e-122">请考虑一个包含三个项目名称 EventManager、 实用程序和 SpecialParser 解决方案。</span><span class="sxs-lookup"><span data-stu-id="4d33e-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="4d33e-123">开发人员经常使用`Update-Package`命令在不同时间与每个这些项目。</span><span class="sxs-lookup"><span data-stu-id="4d33e-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="4d33e-124">她发现方便具有`Update-Package`命令提供的自动完成扩展`-ProjectName`自变量，因此她不需要键入项目名称出每个时间。</span><span class="sxs-lookup"><span data-stu-id="4d33e-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="4d33e-125">以下命令，然后，将这些三个项目名称注册为扩展的`-ProjectName`参数：</span><span class="sxs-lookup"><span data-stu-id="4d33e-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="4d33e-126">开发人员然后可以键入`Update-Package -ProjectName `、 按 tab 键，以及查看作为自动完成选项提供的扩展：</span><span class="sxs-lookup"><span data-stu-id="4d33e-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用注册 TabExpansion 的示例](media/Register-TabExpansion-Example.png)
