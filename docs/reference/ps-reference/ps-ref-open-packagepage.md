---
title: NuGet Open-PackagePage PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Open-PackagePage PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780407"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="4cd15-103">在 Visual Studio 中 Open-PackagePage (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="4cd15-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4cd15-104">*3.0 + 中弃用仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="4cd15-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4cd15-105">用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="4cd15-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="4cd15-106">语法</span><span class="sxs-lookup"><span data-stu-id="4cd15-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4cd15-107">参数</span><span class="sxs-lookup"><span data-stu-id="4cd15-107">Parameters</span></span>

| <span data-ttu-id="4cd15-108">参数</span><span class="sxs-lookup"><span data-stu-id="4cd15-108">Parameter</span></span> | <span data-ttu-id="4cd15-109">说明</span><span class="sxs-lookup"><span data-stu-id="4cd15-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4cd15-110">ID</span><span class="sxs-lookup"><span data-stu-id="4cd15-110">Id</span></span> | <span data-ttu-id="4cd15-111">所需包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="4cd15-111">The package ID of the desired package.</span></span> <span data-ttu-id="4cd15-112">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="4cd15-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4cd15-113">版本</span><span class="sxs-lookup"><span data-stu-id="4cd15-113">Version</span></span> | <span data-ttu-id="4cd15-114">包的版本，默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="4cd15-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="4cd15-115">Source</span><span class="sxs-lookup"><span data-stu-id="4cd15-115">Source</span></span> | <span data-ttu-id="4cd15-116">包源，默认为 "源" 下拉选项中的所选源。</span><span class="sxs-lookup"><span data-stu-id="4cd15-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="4cd15-117">许可证</span><span class="sxs-lookup"><span data-stu-id="4cd15-117">License</span></span> | <span data-ttu-id="4cd15-118">打开浏览器，直至包的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd15-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="4cd15-119">如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd15-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="4cd15-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="4cd15-120">ReportAbuse</span></span> | <span data-ttu-id="4cd15-121">打开浏览器，指向包的 "报告滥用 URL"。</span><span class="sxs-lookup"><span data-stu-id="4cd15-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="4cd15-122">如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd15-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="4cd15-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="4cd15-123">PassThru</span></span> | <span data-ttu-id="4cd15-124">显示 URL;使用 with-WhatIf 来禁止打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="4cd15-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="4cd15-125">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="4cd15-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4cd15-126">通用参数</span><span class="sxs-lookup"><span data-stu-id="4cd15-126">Common Parameters</span></span>

<span data-ttu-id="4cd15-127">`Open-PackagePage` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4cd15-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4cd15-128">示例</span><span class="sxs-lookup"><span data-stu-id="4cd15-128">Examples</span></span>

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