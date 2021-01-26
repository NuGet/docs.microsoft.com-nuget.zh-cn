---
title: NuGet Get-Project PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 GetProject PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777474"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Get-Project (程序包管理器控制台) 

*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*

显示有关默认项目或指定项目的信息。 `Get-Project` 专门返回对 Visual Studio DTE (开发工具环境的引用，) 项目的对象。

## <a name="syntax"></a>语法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 说明 |
| --- | --- |
| 名称 | 指定要显示的项目，默认为在包管理器控制台中选择的默认项目。 -Name 开关本身是可选的。 |
| 全部 | 显示解决方案中每个项目的信息;项目的顺序不确定。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Get-Project` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```