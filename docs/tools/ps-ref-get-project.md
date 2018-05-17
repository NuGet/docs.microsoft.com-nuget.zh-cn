---
title: NuGet Get 项目 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 GetProject PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project （Visual Studio 中的程序包管理器控制台）

*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*

显示的默认值或指定的项目的信息。 `Get-Project` 具体而言返回项目的 Visual Studio DTE （开发工具环境） 对象的引用。

## <a name="syntax"></a>语法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| 名称 | 指定的项目以显示，默认为程序包管理器控制台中选定的默认项目。 -名称开关是可选本身。 |
| 全部 | 显示解决方案; 中的每个项目的信息项目的顺序是不确定的。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Get-Project` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```