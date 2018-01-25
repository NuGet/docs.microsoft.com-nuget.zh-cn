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
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="e0086-104">打开 PackagePage （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="e0086-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e0086-105">*在 3.0 +; 中已过时仅在内可用[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="e0086-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e0086-106">将启动默认浏览器中使用项目、 许可证或指定包的报告滥用行为 URL。</span><span class="sxs-lookup"><span data-stu-id="e0086-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="e0086-107">语法</span><span class="sxs-lookup"><span data-stu-id="e0086-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e0086-108">参数</span><span class="sxs-lookup"><span data-stu-id="e0086-108">Parameters</span></span>

| <span data-ttu-id="e0086-109">参数</span><span class="sxs-lookup"><span data-stu-id="e0086-109">Parameter</span></span> | <span data-ttu-id="e0086-110">描述</span><span class="sxs-lookup"><span data-stu-id="e0086-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e0086-111">Id</span><span class="sxs-lookup"><span data-stu-id="e0086-111">Id</span></span> | <span data-ttu-id="e0086-112">所需的程序包的包 ID。</span><span class="sxs-lookup"><span data-stu-id="e0086-112">The package ID of the desired package.</span></span> <span data-ttu-id="e0086-113">-Id 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="e0086-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e0086-114">版本</span><span class="sxs-lookup"><span data-stu-id="e0086-114">Version</span></span> | <span data-ttu-id="e0086-115">默认为最新版本的包版本。</span><span class="sxs-lookup"><span data-stu-id="e0086-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="e0086-116">源</span><span class="sxs-lookup"><span data-stu-id="e0086-116">Source</span></span> | <span data-ttu-id="e0086-117">包源，默认设置为源下拉列表中的选定源。</span><span class="sxs-lookup"><span data-stu-id="e0086-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="e0086-118">许可证</span><span class="sxs-lookup"><span data-stu-id="e0086-118">License</span></span> | <span data-ttu-id="e0086-119">打开浏览器向包的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="e0086-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="e0086-120">如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="e0086-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e0086-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="e0086-121">ReportAbuse</span></span> | <span data-ttu-id="e0086-122">打开浏览器向包的报告滥用行为 URL。</span><span class="sxs-lookup"><span data-stu-id="e0086-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="e0086-123">如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="e0086-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e0086-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="e0086-124">PassThru</span></span> | <span data-ttu-id="e0086-125">显示的 URL;使用-WhatIf 禁止显示打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="e0086-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="e0086-126">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="e0086-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e0086-127">通用参数</span><span class="sxs-lookup"><span data-stu-id="e0086-127">Common Parameters</span></span>

<span data-ttu-id="e0086-128">`Open-PackagePage`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e0086-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e0086-129">示例</span><span class="sxs-lookup"><span data-stu-id="e0086-129">Examples</span></span>

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