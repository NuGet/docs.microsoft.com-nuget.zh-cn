---
title: NuGet Add-BindingRedirect PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Add-BindingRedirect PowerShell 命令参考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777616"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Add-BindingRedirect (程序包管理器控制台) 

*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*

检查项目的输出路径中的所有程序集，并在必要时向应用程序或 web 配置文件添加绑定重定向。 安装包时，会自动运行此命令。

> [!NOTE]
> 这仅适用于使用 packages.config 文件的方案。 有关详细信息，请参阅 [NuGet packages.config 文件引用](~/reference/packages-config.md)。

有关绑定重定向及其使用原因的详细信息，请参阅 .NET 文档中的 [重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions) 。

## <a name="syntax"></a>语法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 说明 |
| --- | --- |
| 项目名称 | 需要 () 项目添加绑定重定向。 -项目开关本身是可选的。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Add-BindingRedirect` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```