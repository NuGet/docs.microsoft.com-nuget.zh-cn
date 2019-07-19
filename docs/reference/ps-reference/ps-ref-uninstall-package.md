---
title: NuGet 卸载-包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "卸载-包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327274"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package （Visual Studio 中的程序包管理器控制台）

*本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 卸载包" 命令, 请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*

从项目中删除包, 并可以选择删除其依赖项。 如果其他包依赖于此包, 则该命令将失败, 除非指定了-Force 选项。

## <a name="syntax"></a>语法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

如果其他包依赖于此包, 则该命令将失败, 除非指定了-Force 选项。

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | 请求要卸载的包的标识符。 -Id 开关本身是可选的。 |
| Version | 要卸载的包的版本, 默认为当前安装的版本。 |
| RemoveDependencies | 卸载包及其未使用的依赖项。 也就是说, 如果任何依赖项具有依赖于它的其他包, 则会跳过它。 |
| ProjectName | 要从中卸载包的项目, 默认为默认项目。 |
| 团队 | 强制卸载包, 即使其他程序包依赖于它。 |
| WhatIf | 显示运行命令时将发生的情况, 但不实际执行卸载。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Uninstall-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
