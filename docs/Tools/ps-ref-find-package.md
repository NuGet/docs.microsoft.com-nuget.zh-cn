---
title: "NuGet Find-package PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: "Visual Studio 中的 NuGet 包管理器控制台中查找包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，查找包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b6af6098da9c00e47b81ac9ec37bd5210a99a9fe
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>查找包 （在 Visual Studio 中的包管理器控制台）

*版本 3.0 +;本主题介绍中的命令[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell 查找包命令，请参阅[PowerShell PackageManagement 引用](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6)。*

从包源中获取具有指定 ID 或关键字的远程程序包集。

## <a name="syntax"></a>语法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id&lt;关键字&gt; | （必需）搜索包源时要使用的关键字。 使用-ExactMatch 返回其包 ID 和匹配关键字这些包。 如果给不出任何关键字，则`Find-Package`返回第一次-指定下载或数量的前 20 个包的列表。 注意，-Id 是可选的并且不执行任何操作。 |
| 源 | 要搜索的程序包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Find-Package`搜索当前选定的程序包源。 |
| AllVersions | 显示每个包而不是仅最新版本的所有可用的版本。 |
| First | 要从列表中; 的开头返回的程序包数默认值为 20。 |
| Skip | 省略第一个&lt;int&gt;从列表中显示的包。  |
| IncludePrerelease | 在结果中包含预发行程序包。 |
| ExactMatch | 指定要使用&lt;关键字&gt;作为区分大小写的包 id。 |
| StartWith | 返回包的包 ID 开头&lt;关键字&gt;。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Find-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
