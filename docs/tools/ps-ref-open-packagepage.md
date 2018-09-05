---
title: NuGet 打开 PackagePage PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中打开 PackagePage PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547163"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="e6427-103">Open-PackagePage （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="e6427-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e6427-104">*在 3.0 + 中; 已弃用仅在内可用[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="e6427-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e6427-105">将启动默认浏览器与项目、 许可证或指定包的报告滥用 URL。</span><span class="sxs-lookup"><span data-stu-id="e6427-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6427-106">语法</span><span class="sxs-lookup"><span data-stu-id="e6427-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e6427-107">参数</span><span class="sxs-lookup"><span data-stu-id="e6427-107">Parameters</span></span>

| <span data-ttu-id="e6427-108">参数</span><span class="sxs-lookup"><span data-stu-id="e6427-108">Parameter</span></span> | <span data-ttu-id="e6427-109">描述</span><span class="sxs-lookup"><span data-stu-id="e6427-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6427-110">Id</span><span class="sxs-lookup"><span data-stu-id="e6427-110">Id</span></span> | <span data-ttu-id="e6427-111">所需包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="e6427-111">The package ID of the desired package.</span></span> <span data-ttu-id="e6427-112">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="e6427-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e6427-113">版本</span><span class="sxs-lookup"><span data-stu-id="e6427-113">Version</span></span> | <span data-ttu-id="e6427-114">默认为最新版本的包的版本。</span><span class="sxs-lookup"><span data-stu-id="e6427-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="e6427-115">源</span><span class="sxs-lookup"><span data-stu-id="e6427-115">Source</span></span> | <span data-ttu-id="e6427-116">包源，默认设置为源下拉列表中选定的源。</span><span class="sxs-lookup"><span data-stu-id="e6427-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="e6427-117">许可证</span><span class="sxs-lookup"><span data-stu-id="e6427-117">License</span></span> | <span data-ttu-id="e6427-118">包的许可证 URL 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="e6427-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="e6427-119">如果-许可证和-ReportAbuse 均未指定，在浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="e6427-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e6427-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="e6427-120">ReportAbuse</span></span> | <span data-ttu-id="e6427-121">包的报告滥用 URL 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="e6427-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="e6427-122">如果-许可证和-ReportAbuse 均未指定，在浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="e6427-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e6427-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="e6427-123">PassThru</span></span> | <span data-ttu-id="e6427-124">显示的 URL;使用-WhatIf 若要禁止显示打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="e6427-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="e6427-125">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="e6427-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e6427-126">通用参数</span><span class="sxs-lookup"><span data-stu-id="e6427-126">Common Parameters</span></span>

<span data-ttu-id="e6427-127">`Open-PackagePage` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e6427-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e6427-128">示例</span><span class="sxs-lookup"><span data-stu-id="e6427-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```