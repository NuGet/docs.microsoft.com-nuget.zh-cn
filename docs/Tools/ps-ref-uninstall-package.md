---
title: "NuGet 卸载包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio 中的 NuGet 包管理器控制台中卸载程序包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，卸载包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8c1690e0ddda6ad88e045a2097d65d135e233d2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>卸载程序包 （在 Visual Studio 中的包管理器控制台）

*本主题介绍中的命令[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell 卸载程序包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

从项目中，有选择性地删除其依赖项中删除包。 如果其他程序包依赖于此包，该命令将失败，除非指定选项 – Force。

## <a name="syntax"></a>语法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

如果其他程序包依赖于此包，该命令将失败，除非指定选项 – Force。

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要卸载的程序包的标识符。 -Id 开关本身是可选的。 |
| 版本 | 若要卸载，包的版本默认为当前安装的版本。 |
| RemoveDependencies | 卸载程序包及其未使用的依赖项。 也就是说，如果任何依赖关系没有依赖于它的另一个包，它会跳过。 |
| ProjectName | 要从中卸载程序包，对默认项目默认项目。 |
| 强制 | 强制包要卸载，即使其他程序包依赖于它。 |
| WhatIf | 显示运行命令而不实际执行卸载时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Uninstall-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
