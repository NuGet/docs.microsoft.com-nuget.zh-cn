---
title: NuGet PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中提供的 PowerShell 命令的完整引用。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327924"
---
# <a name="powershell-reference"></a>PowerShell 参考

程序包管理器控制台在 Windows 上的 Visual Studio 中提供了一个 PowerShell 接口, 可通过下面列出的特定命令与 NuGet 交互。 (目前, 控制台目前不可用于 Visual Studio for Mac。)有关使用控制台的指南, 请参阅[使用程序包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md)主题。

> [!Tip]
> 所有 PowerShell 命令仅与包消耗相关。 除了包还可以是其他包的使用者以外, 没有任何 PowerShell 命令都与创建和发布包相关。

> [!Important]
> 此处列出的命令特定于 Visual Studio 中的包管理器控制台, 不同于常规 PowerShell 环境中提供的[包管理模块命令](/powershell/module/packagemanagement/?view=powershell-6)。 具体而言, 每个环境都有一些命令, 这些命令在其他环境中不可用, 并且其特定参数的名称相同的命令也可能不同。 使用 Visual Studio 中的包管理控制台时, 适用于本主题中所述的命令和参数。

| 常见命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | 将包及其依赖项安装到项目中。 | 全部 |
| [Update-Package](ps-reference/ps-ref-update-package.md) | 更新包及其依赖项或项目中的所有包。 | 全部 |
| [Find-Package](ps-reference/ps-ref-find-package.md) | 使用包 ID 或关键字搜索包源。 | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | 检索本地存储库中安装的包的列表, 或列出包源中可用的包。 | 全部 |

| 辅助命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | 检查项目的输出路径中的所有程序集, 并将绑定重定向`app.config`添加`web.config`到或 (如果需要)。 | 全部 |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 显示有关默认项目或指定项目的信息。 | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。 | 3\.0 + 中弃用 |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | 为命令的参数注册选项卡展开, 使你可以为常用参数值创建自定义扩展。 | 全部 |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 获取指定项目中已安装包的版本, 并将该版本同步到解决方案中项目的其余部分。 | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | 从项目中删除包, 并可以选择删除其依赖项。 | 全部 |

若要获取有关控制台中任何这些命令的完整详细信息, 只需运行以下命令名称:

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

有关详细信息, 请参阅 PowerShell 文档中的[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) 。
