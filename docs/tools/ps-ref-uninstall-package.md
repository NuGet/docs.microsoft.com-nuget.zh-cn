---
title: NuGet 卸载包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中卸载程序包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551638"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package （Visual Studio 中的程序包管理器控制台）

*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 卸载程序包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

从项目中，有选择性地删除其依赖项中删除包。 如果其他程序包依赖于此包，该命令将失败，除非选项指定了 – Force。

## <a name="syntax"></a>语法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

如果其他程序包依赖于此包，该命令将失败，除非选项指定了 – Force。

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要卸载的包的标识符。 -Id 开关本身是可选的。 |
| 版本 | 若要卸载，包的版本默认为当前安装的版本。 |
| RemoveDependencies | 卸载程序包及其未使用的依赖项。 也就是说，如果任何依赖项具有依赖于它的另一个包，它会跳过。 |
| ProjectName | 要从中卸载程序包，默认值为默认项目项目。 |
| 强制 | 即使其他程序包依赖于它强制要卸载的包。 |
| WhatIf | 显示无需实际执行卸载运行命令时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Uninstall-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
