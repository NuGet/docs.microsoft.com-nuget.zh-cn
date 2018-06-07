---
title: NuGet Get 项目 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 GetProject PowerShell 命令参考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817751"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="5da3b-103">Get-Project （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="5da3b-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5da3b-104">*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="5da3b-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5da3b-105">显示的默认值或指定的项目的信息。</span><span class="sxs-lookup"><span data-stu-id="5da3b-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="5da3b-106">`Get-Project` 具体而言返回项目的 Visual Studio DTE （开发工具环境） 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="5da3b-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="5da3b-107">语法</span><span class="sxs-lookup"><span data-stu-id="5da3b-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5da3b-108">参数</span><span class="sxs-lookup"><span data-stu-id="5da3b-108">Parameters</span></span>

| <span data-ttu-id="5da3b-109">参数</span><span class="sxs-lookup"><span data-stu-id="5da3b-109">Parameter</span></span> | <span data-ttu-id="5da3b-110">描述</span><span class="sxs-lookup"><span data-stu-id="5da3b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5da3b-111">name</span><span class="sxs-lookup"><span data-stu-id="5da3b-111">Name</span></span> | <span data-ttu-id="5da3b-112">指定的项目以显示，默认为程序包管理器控制台中选定的默认项目。</span><span class="sxs-lookup"><span data-stu-id="5da3b-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="5da3b-113">-名称开关是可选本身。</span><span class="sxs-lookup"><span data-stu-id="5da3b-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="5da3b-114">全部</span><span class="sxs-lookup"><span data-stu-id="5da3b-114">All</span></span> | <span data-ttu-id="5da3b-115">显示解决方案; 中的每个项目的信息项目的顺序是不确定的。</span><span class="sxs-lookup"><span data-stu-id="5da3b-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="5da3b-116">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="5da3b-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5da3b-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="5da3b-117">Common Parameters</span></span>

<span data-ttu-id="5da3b-118">`Get-Project` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="5da3b-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5da3b-119">示例</span><span class="sxs-lookup"><span data-stu-id="5da3b-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```