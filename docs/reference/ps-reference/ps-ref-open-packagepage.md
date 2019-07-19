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
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage （Visual Studio 中的程序包管理器控制台）

*3.0 + 中弃用仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*

用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。

## <a name="syntax"></a>语法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | 所需包的包 ID。 -Id 开关本身是可选的。 |
| Version | 包的版本, 默认为最新版本。 |
| Source | 包源, 默认为 "源" 下拉选项中的所选源。 |
| 许可证 | 打开浏览器, 直至包的许可证 URL。 如果未指定-License 和-ReportAbuse, 则浏览器将打开包的项目 URL。 |
| ReportAbuse | 打开浏览器, 指向包的 "报告滥用 URL"。 如果未指定-License 和-ReportAbuse, 则浏览器将打开包的项目 URL。 |
| PassThru | 显示 URL;使用 with-WhatIf 来禁止打开浏览器。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Open-PackagePage`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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