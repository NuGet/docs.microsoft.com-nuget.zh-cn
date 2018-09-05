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
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage （Visual Studio 中的程序包管理器控制台）

*在 3.0 + 中; 已弃用仅在内可用[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

将启动默认浏览器与项目、 许可证或指定包的报告滥用 URL。

## <a name="syntax"></a>语法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | 所需包的包 ID。 -Id 开关本身是可选的。 |
| 版本 | 默认为最新版本的包的版本。 |
| 源 | 包源，默认设置为源下拉列表中选定的源。 |
| 许可证 | 包的许可证 URL 浏览器中打开。 如果-许可证和-ReportAbuse 均未指定，在浏览器将打开包的项目 URL。 |
| ReportAbuse | 包的报告滥用 URL 浏览器中打开。 如果-许可证和-ReportAbuse 均未指定，在浏览器将打开包的项目 URL。 |
| PassThru | 显示的 URL;使用-WhatIf 若要禁止显示打开浏览器。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Open-PackagePage` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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