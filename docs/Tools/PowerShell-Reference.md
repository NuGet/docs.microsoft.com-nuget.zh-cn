---
title: "NuGet PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "对 Visual Studio 中的 NuGet 包管理器控制台中可用的 PowerShell 命令的完整引用。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64450a8bcca7f6028d4ce389d51ac35e9209cfae
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="powershell-reference"></a>PowerShell 参考

程序包管理器控制台提供下面的 PowerShell 接口，以特定的命令通过 NuGet 进行交互的 Windows 上的 Visual Studio 中列出。 （控制台不是在 Visual Studio for mac。 目前可用的）有关如何使用控制台的指南，请参阅[程序包管理器控制台](../tools/package-manager-console.md)主题。

> [!Tip]
> 仅与包消耗相关的所有 PowerShell 命令。 任何 PowerShell 命令不与创建和发布除外的包的范围内包也可以是其他包的使用者。

> [!Important]
> 此处列出的命令是特定于 Visual Studio 中的包管理器控制台，区别[软件包管理模块命令](/powershell/module/packagemanagement/?view=powershell-6)常规 PowerShell 环境中提供。 具体而言，每个环境包含在另一个中, 不可用的命令，并具有相同名称的命令也可能在特定自变量而异。 当使用 Visual Studio 中的包管理控制台，将应用的命令和参数中存在本文所述。

| 常见的命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | 在项目中安装包和其依赖项。 | 全部 |
| [Update-Package](ps-ref-update-package.md) | 更新包和其依赖项或在项目中的所有包。 | 全部 |
| [Find-Package](ps-ref-find-package.md) | 搜索包源使用的包 ID 或关键字。 | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 检索安装在本地存储库，包的列表或列出从包源提供的程序包。 | 全部 |

| 辅助命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | 检查项目输出路径中的所有程序集并将添加绑定重定向到`app.config`或`web.config`在必要时。 | 全部 |
| [Get-Project](ps-ref-get-project.md) | 显示的默认值或指定的项目的信息。 | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | 将启动默认浏览器中使用项目、 许可证或指定包的报告滥用行为 URL。 | 在 3.0 + 弃用 |
| [注册 TabExpansion](ps-ref-register-tabexpansion.md) | 注册一个命令，使你可以创建自定义的扩展的常用的参数值的参数选项卡扩展。 | 全部 |
| [Sync-Package](ps-ref-sync-package.md) | 安装从包的版本的 get 指定项目和同步到解决方案中项目的其余部分的版本。 | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 从项目中，有选择性地删除其依赖项中删除包。 | 全部 |

有关完整的详细帮助其中任何命令，在控制台中，只需运行命令中的名称与以下：

```ps
Get-Help <command> -full
```

所有程序包管理器控制台命令都支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):

- 调试
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 详细
- WarningAction
- WarningVariable

有关详细信息，请参阅[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216)中的 PowerShell 文档。
