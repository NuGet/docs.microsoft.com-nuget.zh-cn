---
title: NuGet 添加 BindingRedirect PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551652"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect （Visual Studio 中的程序包管理器控制台）

*仅在内可用[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

检查项目的输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。 安装包时，将自动运行此命令。

有关绑定的绑定重定向以及为什么使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。

## <a name="syntax"></a>语法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| ProjectName | （必需）要将绑定重定向添加到项目。 -ProjectName 开关本身是可选的。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```