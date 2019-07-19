---
title: NuGet 注册-Tabexpansion 控制 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 Tabexpansion 控制 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327294"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Tabexpansion 控制 (Visual Studio 中的包管理器控制台)

*仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*

为指定命令的参数注册选项卡扩展, 以便在输入命令时使用 Tab 键时, 展开的值将显示为相关参数的可用选项。 将覆盖此命令的任何以前的扩展。

## <a name="syntax"></a>语法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| 名称 | 请求要向其注册扩展的命令。 -Name 开关本身是可选的。 |
| 定义 | 请求一个对象, 该对象描述语法`@{'<parameter>' = {'<value1>', '<value2>', ...}}`中的参数, 其中`<parameter>`是要修改的参数的名称`<value>` , 每个参数都提供特定的扩展。 同时接受单引号和双引号。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Register-TabExpansion`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

假设解决方案包含三个项目名称但是、实用工具和 SpecialParser。 开发人员经常在每`Update-Package`个项目中的不同时间使用命令。 她发现, 使用`Update-Package`该命令为`-ProjectName`参数提供自动完成扩展是非常方便的, 因此她每次都不需要键入项目名称。 

然后, 下面的命令将这三个项目名称注册为`-ProjectName`参数的扩展:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

然后, 开发人员可以`Update-Package -ProjectName `键入, 按 tab, 并查看作为自动完成选项提供的扩展:

![使用 Tabexpansion 控制的示例](media/Register-TabExpansion-Example.png)
