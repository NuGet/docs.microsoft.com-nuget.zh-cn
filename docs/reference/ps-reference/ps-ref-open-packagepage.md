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
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Open-PackagePage (程序包管理器控制台) 

*3.0 + 中弃用仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*

用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。

## <a name="syntax"></a>语法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 说明 |
| --- | --- |
| ID | 所需包的包 ID。 -Id 开关本身是可选的。 |
| 版本 | 包的版本，默认为最新版本。 |
| Source | 包源，默认为 "源" 下拉选项中的所选源。 |
| 许可证 | 打开浏览器，直至包的许可证 URL。 如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。 |
| ReportAbuse | 打开浏览器，指向包的 "报告滥用 URL"。 如果未指定-License 和-ReportAbuse，则浏览器将打开包的项目 URL。 |
| PassThru | 显示 URL;使用 with-WhatIf 来禁止打开浏览器。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Open-PackagePage` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

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