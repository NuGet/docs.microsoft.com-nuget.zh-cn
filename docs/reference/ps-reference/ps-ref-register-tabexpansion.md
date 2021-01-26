---
title: NuGet Register-TabExpansion PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Register-TabExpansion PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777462"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Register-TabExpansion (程序包管理器控制台) 

*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*

为指定命令的参数注册选项卡扩展，以便在输入命令时使用 Tab 键时，展开的值将显示为相关参数的可用选项。 将覆盖此命令的任何以前的扩展。

## <a name="syntax"></a>语法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 说明 |
| --- | --- |
| 名称 |  (要求) 要注册扩展的命令。 -Name 开关本身是可选的。 |
| 定义 |  (必需) 一个对象，该对象描述语法中的参数， `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 其中 `<parameter>` 是要修改的参数的名称，每个参数都 `<value>` 提供特定的扩展。 同时接受单引号和双引号。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Register-TabExpansion` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

假设解决方案包含三个项目名称但是、实用工具和 SpecialParser。 开发人员经常在 `Update-Package` 每个项目中的不同时间使用命令。 她发现，使用该命令为 `Update-Package` 参数提供自动完成扩展是非常方便的 `-ProjectName` ，因此她每次都不需要键入项目名称。 

然后，下面的命令将这三个项目名称注册为参数的扩展 `-ProjectName` ：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

然后，开发人员可以键入 `Update-Package -ProjectName ` ，按 tab，并查看作为自动完成选项提供的扩展：

![使用 Register-TabExpansion 的示例](media/Register-TabExpansion-Example.png)