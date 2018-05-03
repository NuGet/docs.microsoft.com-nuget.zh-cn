---
title: NuGet 同步包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中同步包 PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>同步包 （在 Visual Studio 中的包管理器控制台）

*版本 3.0 +;仅在内可用[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*

获取从安装包的版本指定 （或默认值） 项目，并同步到解决方案中项目的其余部分的版本。

## <a name="syntax"></a>语法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要同步的包标识符。-Id 开关本身是可选的。 |
| IgnoreDependencies | 安装仅此包不及其依赖项。 |
| ProjectName | 要同步包从，默认为默认项目的项目。 |
| 版本 | 若要同步，包的版本默认为当前安装的版本。 |
| 源 | 要搜索的程序包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Sync-Package`搜索当前选定的程序包源。 |
| IncludePrerelease | 在同步中包括预发行程序包。 |
| FileConflictAction | 当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。 可能的值为*覆盖，忽略，无、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 版本的依赖项包若要使用，可以是下列项之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</li><li>*最高*（默认值为更新包不带任何参数）： 最高的版本</li></ul>你可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。 |
| WhatIf | 显示不实际执行同步运行命令时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Sync-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
