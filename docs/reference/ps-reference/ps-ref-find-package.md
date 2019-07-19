---
title: NuGet 查找包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "查找包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327384"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package （Visual Studio 中的程序包管理器控制台）

*版本 3.0 +;本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 查找包" 命令, 请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*

从包源中获取具有指定 ID 或关键字的一组远程包。

## <a name="syntax"></a>语法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id &lt;关键字&gt; | 请求搜索包源时要使用的关键字。 使用-ExactMatch 仅返回其包 ID 与关键字匹配的那些包。 如果未提供任何关键字, `Find-Package`则返回按下载项列出的前20个包的列表, 或由-First 指定的数字。 请注意,-Id 是可选的, 而不是操作。 |
| Source | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径, 也可以是相对于当前文件夹的路径。 如果省略, `Find-Package`则搜索当前选定的包源。 |
| AllVersions | 显示每个包的所有可用版本, 而不是仅显示最新版本。 |
| 第一个 | 要从列表开头返回的包数;默认值为20。 |
| Skip | 省略所显示&lt;列表&gt;中的第一个 int 包。  |
| IncludePrerelease | 在结果中包括预发布包。 |
| ExactMatch | 指定使用&lt;关键字&gt;作为区分大小写的包 ID。 |
| StartWith | 返回包 ID 以关键字&lt;&gt;开头的包。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Find-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
