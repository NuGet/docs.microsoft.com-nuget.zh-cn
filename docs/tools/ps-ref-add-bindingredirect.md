---
title: NuGet 添加 BindingRedirect PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect （Visual Studio 中的程序包管理器控制台）

*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*

检查项目输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。 安装程序包时，将自动运行此命令。

绑定重定向和为何使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。

## <a name="syntax"></a>语法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| ProjectName | （必需）要向其中添加绑定重定向项目。 -ProjectName 交换机本身是可选的。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```