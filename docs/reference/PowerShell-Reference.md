---
title: NuGet PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中提供的 PowerShell 命令的完整引用。
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 98bea8a225f4864953f898ef57b26e9093f7c2e9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779363"
---
# <a name="powershell-reference"></a>PowerShell 参考

程序包管理器控制台在 Windows 上的 Visual Studio 中提供了一个 PowerShell 接口，可通过下面列出的特定命令与 NuGet 交互。  (控制台目前在 Visual Studio for Mac 中不可用。 ) 有关使用控制台的指南，请参阅 [使用程序包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md) 主题。

> [!Tip]
> 所有 PowerShell 命令仅与包消耗相关。 除了包还可以是其他包的使用者以外，没有任何 PowerShell 命令都与创建和发布包相关。

> [!Important]
> 此处列出的命令特定于 Visual Studio 中的包管理器控制台，它不同于常规 PowerShell 环境中提供的[包管理模块命令](/powershell/module/packagemanagement/?view=powershell-6)。 具体而言，每个环境都有一些命令，这些命令在其他环境中不可用，而具有相同名称的命令在其特定参数中也可能不同。 使用 Visual Studio 中的包管理控制台时，本主题中所述的命令和参数适用。

| 常见命令 | 说明 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | 将程序包及其依赖项安装到项目中。 | 全部 |
| [Update-Package](ps-reference/ps-ref-update-package.md) | 更新包及其依赖项或项目中的所有包。 | 全部 |
| [Find-Package](ps-reference/ps-ref-find-package.md) | 使用包 ID 或关键字搜索包源。 | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | 检索本地存储库中安装的包的列表，或列出包源中可用的包。 | 全部 |

| 辅助命令 | 说明 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | 检查项目的输出路径中的所有程序集，并将绑定重定向添加到 `app.config` 或 `web.config` （如果需要）。 | 全部 |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 显示有关默认项目或指定项目的信息。 | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。 | 3.0 + 中弃用 |
| [注册-Tabexpansion 控制](ps-reference/ps-ref-register-tabexpansion.md) | 为命令的参数注册选项卡展开，使你可以为常用参数值创建自定义扩展。 | 全部 |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 获取指定项目中已安装包的版本，并将该版本同步到解决方案中项目的其余部分。 | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | 从项目中删除包，并可以选择删除其依赖项。 | 全部 |

若要获取有关控制台中任何这些命令的完整详细信息，只需运行以下命令名称：

```ps
Get-Help <command> -full
```

所有程序包管理器控制台命令都支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：

- 调试
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 详细
- WarningAction
- WarningVariable

有关详细信息，请参阅 PowerShell 文档中的 [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) 。