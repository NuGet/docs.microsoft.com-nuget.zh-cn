---
title: "NuGet Get 项目 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio 中的 NuGet 包管理器控制台中 GetProject PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，Get 项目"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb98498d6cc6245c9e22b00eada097b816160aea
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a5bc8-104">Get 项目 （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="a5bc8-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a5bc8-105">*仅在内可用[NuGet 程序包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="a5bc8-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a5bc8-106">显示的默认值或指定的项目的信息。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="a5bc8-107">`Get-Project`具体而言返回项目的 Visual Studio DTE （开发工具环境） 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5bc8-108">语法</span><span class="sxs-lookup"><span data-stu-id="a5bc8-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a5bc8-109">参数</span><span class="sxs-lookup"><span data-stu-id="a5bc8-109">Parameters</span></span>

| <span data-ttu-id="a5bc8-110">参数</span><span class="sxs-lookup"><span data-stu-id="a5bc8-110">Parameter</span></span> | <span data-ttu-id="a5bc8-111">描述</span><span class="sxs-lookup"><span data-stu-id="a5bc8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5bc8-112">name</span><span class="sxs-lookup"><span data-stu-id="a5bc8-112">Name</span></span> | <span data-ttu-id="a5bc8-113">指定的项目以显示，默认为程序包管理器控制台中选定的默认项目。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a5bc8-114">-名称开关是可选本身。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a5bc8-115">全部</span><span class="sxs-lookup"><span data-stu-id="a5bc8-115">All</span></span> | <span data-ttu-id="a5bc8-116">显示解决方案; 中的每个项目的信息项目的顺序是不确定的。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a5bc8-117">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a5bc8-118">通用参数</span><span class="sxs-lookup"><span data-stu-id="a5bc8-118">Common Parameters</span></span>

<span data-ttu-id="a5bc8-119">`Get-Project`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="a5bc8-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a5bc8-120">示例</span><span class="sxs-lookup"><span data-stu-id="a5bc8-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```