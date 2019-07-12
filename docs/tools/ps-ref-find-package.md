---
title: NuGet 找到的包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中找到的包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842525"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package （Visual Studio 中的程序包管理器控制台）

*版本 3.0 + 中;本主题介绍中的命令[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 找到的包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

包源中获取具有指定 ID 或关键字远程包的集。

## <a name="syntax"></a>语法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id&lt;关键字&gt; | （必需）搜索包源时要使用的关键字。 使用-ExactMatch 返回关键字匹配的包 ID 这些包。 如果不给定了任何关键字，`Find-Package`返回首次为-指定数或下载的前 20 个包的列表。 请注意，-Id 是可选的执行任何操作。 |
| Source | 要搜索的包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Find-Package`搜索当前所选的包源。 |
| AllVersions | 显示所有可用版本的每个包而不是仅最新版本。 |
| 第一个 | 若要从列表中; 开头返回的包数默认值为 20。 |
| Skip | 省略了第一个&lt;int&gt;显示的列表中的包。  |
| IncludePrerelease | 在结果中包括预发行包。 |
| ExactMatch | 指定要使用&lt;关键字&gt;作为一个区分大小写的包 id。 |
| StartWith | 返回包的包 ID 开头&lt;关键字&gt;。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Find-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。

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
