---
title: NuGet Open-PackagePage PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Open-PackagePage PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238057"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="86b7c-103">在 Visual Studio 中 Open-PackagePage (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="86b7c-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="86b7c-104">*3.0 + 中弃用仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="86b7c-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="86b7c-105">用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="86b7c-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="86b7c-106">语法</span><span class="sxs-lookup"><span data-stu-id="86b7c-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="86b7c-107">parameters</span><span class="sxs-lookup"><span data-stu-id="86b7c-107">Parameters</span></span>

| <span data-ttu-id="86b7c-108">参数</span><span class="sxs-lookup"><span data-stu-id="86b7c-108">Parameter</span></span> | <span data-ttu-id="86b7c-109">说明</span><span class="sxs-lookup"><span data-stu-id="86b7c-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86b7c-110">ID</span><span class="sxs-lookup"><span data-stu-id="86b7c-110">Id</span></span> | <span data-ttu-id="86b7c-111">所需包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="86b7c-111">The package ID of the desired package.</span></span> <span data-ttu-id="86b7c-112">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="86b7c-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="86b7c-113">版本</span><span class="sxs-lookup"><span data-stu-id="86b7c-113">Version</span></span> | <span data-ttu-id="86b7c-114">包的版本，默认为最新版本。</span><span class="sxs-lookup"><span data-stu-id="86b7c-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="86b7c-115">源</span><span class="sxs-lookup"><span data-stu-id="86b7c-115">Source</span></span> | <span data-ttu-id="86b7c-116">包源，默认为 "源" 下拉选项中的所选源。</span><span class="sxs-lookup"><span data-stu-id="86b7c-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="86b7c-117">许可证</span><span class="sxs-lookup"><span data-stu-id="86b7c-117">License</span></span> | <span data-ttu-id="86b7c-118">打开浏览器，直至包的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="86b7c-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="86b7c-119">如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="86b7c-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="86b7c-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="86b7c-120">ReportAbuse</span></span> | <span data-ttu-id="86b7c-121">打开浏览器，指向包的 "报告滥用 URL"。</span><span class="sxs-lookup"><span data-stu-id="86b7c-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="86b7c-122">如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="86b7c-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="86b7c-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="86b7c-123">PassThru</span></span> | <span data-ttu-id="86b7c-124">显示 URL;使用 with-WhatIf 来禁止打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="86b7c-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="86b7c-125">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="86b7c-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="86b7c-126">通用参数</span><span class="sxs-lookup"><span data-stu-id="86b7c-126">Common Parameters</span></span>

<span data-ttu-id="86b7c-127">`Open-PackagePage` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="86b7c-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="86b7c-128">示例</span><span class="sxs-lookup"><span data-stu-id="86b7c-128">Examples</span></span>

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