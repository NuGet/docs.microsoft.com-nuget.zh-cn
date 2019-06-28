---
title: NuGet PowerShell 参考
description: 对 Visual Studio 中的 NuGet 包管理器控制台中可用的 PowerShell 命令的完整引用。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426127"
---
# <a name="powershell-reference"></a>PowerShell 参考

包管理器控制台提供了下面列出与 NuGet 交互通过特定命令的 Windows 上的 Visual Studio 中的 PowerShell 接口。 （在控制台不是在 Visual Studio for mac 中目前可用的）使用控制台的指南，请参阅[安装和管理包使用 PowerShell](../tools/package-manager-console.md)主题。

> [!Tip]
> 所有 PowerShell 命令仅都与包使用。 任何 PowerShell 命令不与创建和发布包除外的范围内包也可以是其他包的使用者。

> [!Important]
> 此处列出的命令特定于 Visual Studio 中的包管理器控制台，并且不同于[包管理的模块命令](/powershell/module/packagemanagement/?view=powershell-6)常规的 PowerShell 环境中提供。 具体而言，每个环境包含在另一个中, 不可用的命令，并具有相同名称的命令在其特定的参数也可能存在差异。 当在 Visual Studio 中使用包管理控制台，命令和本主题中所述的自变量应用。

| 常用命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | 将包及其依赖项安装到项目。 | 全部 |
| [Update-Package](ps-ref-update-package.md) | 更新包和及其依赖项或在项目中的所有包。 | 全部 |
| [Find-Package](ps-ref-find-package.md) | 搜索使用的包 ID 或关键字的包源。 | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 检索安装在本地存储库中的包的列表，或列出的包源中可用的包。 | 全部 |

| 辅助命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | 检查项目的输出路径中的所有程序集并将添加到绑定重定向`app.config`或`web.config`在必要时。 | 全部 |
| [Get-Project](ps-ref-get-project.md) | 显示默认值或指定的项目有关的信息。 | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | 将启动默认浏览器与项目、 许可证或指定包的报告滥用 URL。 | 3\.0 + 中不推荐使用 |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | 注册命令，它允许您创建自定义的扩展的常用参数值的参数的选项卡扩展。 | 全部 |
| [Sync-Package](ps-ref-sync-package.md) | 获取安装的版本的包从指定项目并同步到解决方案中项目的其余部分的版本。 | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 从项目中，有选择性地删除其依赖项中删除包。 | 全部 |

有关完整的详细帮助其中任何命令，在控制台中，只需运行以下命令使用相关的命令名：

```ps
Get-Help <command> -full
```

包管理器控制台的所有命令都支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):

- 调试
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 详细
- WarningAction
- WarningVariable

有关详细信息，请参阅[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 文档中。
