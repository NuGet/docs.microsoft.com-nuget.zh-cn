---
title: NuGet Get-Project PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 GetProject PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777474"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="6804d-103">在 Visual Studio 中 Get-Project (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="6804d-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6804d-104">*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="6804d-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6804d-105">显示有关默认项目或指定项目的信息。</span><span class="sxs-lookup"><span data-stu-id="6804d-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="6804d-106">`Get-Project` 专门返回对 Visual Studio DTE (开发工具环境的引用，) 项目的对象。</span><span class="sxs-lookup"><span data-stu-id="6804d-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="6804d-107">语法</span><span class="sxs-lookup"><span data-stu-id="6804d-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6804d-108">参数</span><span class="sxs-lookup"><span data-stu-id="6804d-108">Parameters</span></span>

| <span data-ttu-id="6804d-109">参数</span><span class="sxs-lookup"><span data-stu-id="6804d-109">Parameter</span></span> | <span data-ttu-id="6804d-110">说明</span><span class="sxs-lookup"><span data-stu-id="6804d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6804d-111">名称</span><span class="sxs-lookup"><span data-stu-id="6804d-111">Name</span></span> | <span data-ttu-id="6804d-112">指定要显示的项目，默认为在包管理器控制台中选择的默认项目。</span><span class="sxs-lookup"><span data-stu-id="6804d-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="6804d-113">-Name 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="6804d-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="6804d-114">全部</span><span class="sxs-lookup"><span data-stu-id="6804d-114">All</span></span> | <span data-ttu-id="6804d-115">显示解决方案中每个项目的信息;项目的顺序不确定。</span><span class="sxs-lookup"><span data-stu-id="6804d-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="6804d-116">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="6804d-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6804d-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="6804d-117">Common Parameters</span></span>

<span data-ttu-id="6804d-118">`Get-Project` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="6804d-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6804d-119">示例</span><span class="sxs-lookup"><span data-stu-id="6804d-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```