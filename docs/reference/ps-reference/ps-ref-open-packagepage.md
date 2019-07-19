---
title: NuGet PackagePage PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 PackagePage PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327374"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d5a8e-103">Open-PackagePage （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="d5a8e-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d5a8e-104">*3.0 + 中弃用仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*</span><span class="sxs-lookup"><span data-stu-id="d5a8e-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d5a8e-105">用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d5a8e-106">语法</span><span class="sxs-lookup"><span data-stu-id="d5a8e-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d5a8e-107">参数</span><span class="sxs-lookup"><span data-stu-id="d5a8e-107">Parameters</span></span>

| <span data-ttu-id="d5a8e-108">参数</span><span class="sxs-lookup"><span data-stu-id="d5a8e-108">Parameter</span></span> | <span data-ttu-id="d5a8e-109">描述</span><span class="sxs-lookup"><span data-stu-id="d5a8e-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5a8e-110">Id</span><span class="sxs-lookup"><span data-stu-id="d5a8e-110">Id</span></span> | <span data-ttu-id="d5a8e-111">所需包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-111">The package ID of the desired package.</span></span> <span data-ttu-id="d5a8e-112">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d5a8e-113">Version</span><span class="sxs-lookup"><span data-stu-id="d5a8e-113">Version</span></span> | <span data-ttu-id="d5a8e-114">包的版本, 默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d5a8e-115">Source</span><span class="sxs-lookup"><span data-stu-id="d5a8e-115">Source</span></span> | <span data-ttu-id="d5a8e-116">包源, 默认为 "源" 下拉选项中的所选源。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d5a8e-117">许可证</span><span class="sxs-lookup"><span data-stu-id="d5a8e-117">License</span></span> | <span data-ttu-id="d5a8e-118">打开浏览器, 直至包的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d5a8e-119">如果未指定-License 和-ReportAbuse, 则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d5a8e-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d5a8e-120">ReportAbuse</span></span> | <span data-ttu-id="d5a8e-121">打开浏览器, 指向包的 "报告滥用 URL"。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d5a8e-122">如果未指定-License 和-ReportAbuse, 则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d5a8e-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="d5a8e-123">PassThru</span></span> | <span data-ttu-id="d5a8e-124">显示 URL;使用 with-WhatIf 来禁止打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d5a8e-125">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d5a8e-126">通用参数</span><span class="sxs-lookup"><span data-stu-id="d5a8e-126">Common Parameters</span></span>

<span data-ttu-id="d5a8e-127">`Open-PackagePage`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="d5a8e-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d5a8e-128">示例</span><span class="sxs-lookup"><span data-stu-id="d5a8e-128">Examples</span></span>

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