---
title: "NuGet 打开 PackagePage PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio 中的 NuGet 包管理器控制台中打开 PackagePage PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，打开 PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cc645d9a2779fd6b1b329e9aac4777d50f75d16
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="32d6a-104">打开 PackagePage （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="32d6a-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="32d6a-105">*在 3.0 +; 中已过时仅在内可用[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="32d6a-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="32d6a-106">将启动默认浏览器中使用项目、 许可证或指定包的报告滥用行为 URL。</span><span class="sxs-lookup"><span data-stu-id="32d6a-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="32d6a-107">语法</span><span class="sxs-lookup"><span data-stu-id="32d6a-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="32d6a-108">参数</span><span class="sxs-lookup"><span data-stu-id="32d6a-108">Parameters</span></span>

| <span data-ttu-id="32d6a-109">参数</span><span class="sxs-lookup"><span data-stu-id="32d6a-109">Parameter</span></span> | <span data-ttu-id="32d6a-110">描述</span><span class="sxs-lookup"><span data-stu-id="32d6a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32d6a-111">Id</span><span class="sxs-lookup"><span data-stu-id="32d6a-111">Id</span></span> | <span data-ttu-id="32d6a-112">所需的程序包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="32d6a-112">The package ID of the desired package.</span></span> <span data-ttu-id="32d6a-113">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="32d6a-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="32d6a-114">版本</span><span class="sxs-lookup"><span data-stu-id="32d6a-114">Version</span></span> | <span data-ttu-id="32d6a-115">默认为最新版本的包版本。</span><span class="sxs-lookup"><span data-stu-id="32d6a-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="32d6a-116">源</span><span class="sxs-lookup"><span data-stu-id="32d6a-116">Source</span></span> | <span data-ttu-id="32d6a-117">包源，默认设置为源下拉列表中的选定源。</span><span class="sxs-lookup"><span data-stu-id="32d6a-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="32d6a-118">许可证</span><span class="sxs-lookup"><span data-stu-id="32d6a-118">License</span></span> | <span data-ttu-id="32d6a-119">打开浏览器向包的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="32d6a-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="32d6a-120">如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="32d6a-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="32d6a-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="32d6a-121">ReportAbuse</span></span> | <span data-ttu-id="32d6a-122">打开浏览器向包的报告滥用行为 URL。</span><span class="sxs-lookup"><span data-stu-id="32d6a-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="32d6a-123">如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="32d6a-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="32d6a-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="32d6a-124">PassThru</span></span> | <span data-ttu-id="32d6a-125">显示的 URL;使用-WhatIf 禁止显示打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="32d6a-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="32d6a-126">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="32d6a-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="32d6a-127">通用参数</span><span class="sxs-lookup"><span data-stu-id="32d6a-127">Common Parameters</span></span>

<span data-ttu-id="32d6a-128">`Open-PackagePage` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="32d6a-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="32d6a-129">示例</span><span class="sxs-lookup"><span data-stu-id="32d6a-129">Examples</span></span>

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