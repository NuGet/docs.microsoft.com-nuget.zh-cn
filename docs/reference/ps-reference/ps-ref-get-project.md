---
title: NuGet 获取项目 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 GetProject PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327354"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a13be-103">Get-Project （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="a13be-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a13be-104">*仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*</span><span class="sxs-lookup"><span data-stu-id="a13be-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a13be-105">显示有关默认项目或指定项目的信息。</span><span class="sxs-lookup"><span data-stu-id="a13be-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="a13be-106">`Get-Project`特别返回对项目的 Visual Studio DTE (开发工具环境) 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="a13be-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a13be-107">语法</span><span class="sxs-lookup"><span data-stu-id="a13be-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a13be-108">参数</span><span class="sxs-lookup"><span data-stu-id="a13be-108">Parameters</span></span>

| <span data-ttu-id="a13be-109">参数</span><span class="sxs-lookup"><span data-stu-id="a13be-109">Parameter</span></span> | <span data-ttu-id="a13be-110">描述</span><span class="sxs-lookup"><span data-stu-id="a13be-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a13be-111">名称</span><span class="sxs-lookup"><span data-stu-id="a13be-111">Name</span></span> | <span data-ttu-id="a13be-112">指定要显示的项目, 默认为在包管理器控制台中选择的默认项目。</span><span class="sxs-lookup"><span data-stu-id="a13be-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a13be-113">-Name 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="a13be-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a13be-114">全部</span><span class="sxs-lookup"><span data-stu-id="a13be-114">All</span></span> | <span data-ttu-id="a13be-115">显示解决方案中每个项目的信息;项目的顺序不确定。</span><span class="sxs-lookup"><span data-stu-id="a13be-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a13be-116">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="a13be-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a13be-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="a13be-117">Common Parameters</span></span>

<span data-ttu-id="a13be-118">`Get-Project`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="a13be-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a13be-119">示例</span><span class="sxs-lookup"><span data-stu-id="a13be-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```