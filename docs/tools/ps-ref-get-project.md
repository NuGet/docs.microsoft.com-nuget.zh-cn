---
title: 获取项目的 NuGet PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中的 GetProject PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842279"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3355-103">Get-Project （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="f3355-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3355-104">*仅在内可用[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="f3355-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f3355-105">显示默认值或指定的项目有关的信息。</span><span class="sxs-lookup"><span data-stu-id="f3355-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="f3355-106">`Get-Project` 专门返回到项目的 Visual Studio DTE （开发工具环境） 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="f3355-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3355-107">语法</span><span class="sxs-lookup"><span data-stu-id="f3355-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f3355-108">参数</span><span class="sxs-lookup"><span data-stu-id="f3355-108">Parameters</span></span>

| <span data-ttu-id="f3355-109">参数</span><span class="sxs-lookup"><span data-stu-id="f3355-109">Parameter</span></span> | <span data-ttu-id="f3355-110">描述</span><span class="sxs-lookup"><span data-stu-id="f3355-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3355-111">名称</span><span class="sxs-lookup"><span data-stu-id="f3355-111">Name</span></span> | <span data-ttu-id="f3355-112">指定要显示，项目默认设置为在包管理器控制台中选择的默认项目。</span><span class="sxs-lookup"><span data-stu-id="f3355-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="f3355-113">-名称开关是可选本身。</span><span class="sxs-lookup"><span data-stu-id="f3355-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="f3355-114">全部</span><span class="sxs-lookup"><span data-stu-id="f3355-114">All</span></span> | <span data-ttu-id="f3355-115">在解决方案中; 每个项目的显示信息项目的顺序是不确定的。</span><span class="sxs-lookup"><span data-stu-id="f3355-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="f3355-116">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="f3355-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3355-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="f3355-117">Common Parameters</span></span>

<span data-ttu-id="f3355-118">`Get-Project` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="f3355-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3355-119">示例</span><span class="sxs-lookup"><span data-stu-id="f3355-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```