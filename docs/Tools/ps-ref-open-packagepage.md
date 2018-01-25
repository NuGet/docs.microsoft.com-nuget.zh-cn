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
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>打开 PackagePage （Visual Studio 中的包管理器控制台）

*在 3.0 +; 中已过时仅在内可用[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*

将启动默认浏览器中使用项目、 许可证或指定包的报告滥用行为 URL。

## <a name="syntax"></a>语法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | 所需的程序包的包 ID。 -Id 开关本身是可选的。 |
| 版本 | 默认为最新版本的包版本。 |
| 源 | 包源，默认设置为源下拉列表中的选定源。 |
| 许可证 | 打开浏览器向包的许可证 URL。 如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。 |
| ReportAbuse | 打开浏览器向包的报告滥用行为 URL。 如果-许可证和-ReportAbuse 均未指定，浏览器将打开包的项目 URL。 |
| PassThru | 显示的 URL;使用-WhatIf 禁止显示打开浏览器。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Open-PackagePage`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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