---
title: 获取项目的 NuGet PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中的 GetProject PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842279"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project （Visual Studio 中的程序包管理器控制台）

*仅在内可用[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

显示默认值或指定的项目有关的信息。 `Get-Project` 专门返回到项目的 Visual Studio DTE （开发工具环境） 对象的引用。

## <a name="syntax"></a>语法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| 名称 | 指定要显示，项目默认设置为在包管理器控制台中选择的默认项目。 -名称开关是可选本身。 |
| 全部 | 在解决方案中; 每个项目的显示信息项目的顺序是不确定的。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Get-Project` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```