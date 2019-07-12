---
title: NuGet 包同步 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中同步包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842253"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package （Visual Studio 中的程序包管理器控制台）

*版本 3.0 + 中;仅在内可用[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

获取从已安装包的版本指定 （或默认值） 项目，并同步到解决方案中项目的其余部分的版本。

## <a name="syntax"></a>语法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要同步的包的标识符。-Id 开关本身是可选的。 |
| IgnoreDependencies | 安装此包仅不及其依赖项。 |
| ProjectName | 要同步中，默认值为默认项目的包的项目。 |
| Version | 要同步的包的版本默认为当前安装的版本。 |
| Source | 要搜索的包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Sync-Package`搜索当前所选的包源。 |
| IncludePrerelease | 在同步中包括预发行包。 |
| FileConflictAction | 当要求您覆盖或忽略现有的项目所引用的文件时要执行的操作。 可能的值为*覆盖、 忽略、 None、 OverwriteAll*，并 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 版本的依赖项包使用，可以是以下值之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</li><li>*最高*（默认值为更新包不带任何参数）： 最高版本</li></ul>您可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。 |
| WhatIf | 显示运行该命令而无需实际执行同步时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Sync-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
