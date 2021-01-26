---
title: NuGet 1.7 发行说明
description: NuGet 1.7 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777068"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 发行说明

[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)  | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)

NuGet 1.7 于年4月 4 2012 日发布。

## <a name="known-installation-issue"></a>已知安装问题
如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。

解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。  有关更多信息，请参见<https://support.microsoft.com/kb/2581019>。

注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>支持在安装后打开 readme.txt 文件
1.7 中的新增内容，如果你 `readme.txt` 的包在包的根目录中包含一个文件，则在安装完包之后，NuGet 将自动打开此文件。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在 "管理 NuGet 包" 对话框中显示预发行包
"管理 NuGet 包" 对话框现在包含一个下拉列表，其中提供了显示预发行包的选项。

![显示预发行包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>缺少包文件时显示 "包还原" 按钮
打开 "程序包管理器控制台" 或 "管理器 NuGet 包" 对话框时，NuGet 将检查当前解决方案是否已启用包还原模式，以及文件夹中是否缺少任何包文件 `packages` 。 如果满足这两个条件，NuGet 会通知你，并显示一个便利的 "还原" 按钮。 单击此按钮将触发 NuGet 以还原所有缺少的包。

![对话框上的 "包还原" 按钮](./media/packagerestore-dialog.png)

![控制台上的 "包还原" 按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>添加解决方案级 packages.config 文件
在 NuGet 的早期版本中，每个项目都有一个 `packages.config` 文件，该文件跟踪在该项目中安装的 NuGet 包。 不过，解决方案级别没有类似的文件来跟踪解决方案级包。 因此，无法还原解决方案级包。
此功能现已在 NuGet 1.7 中实现。 解决方案级文件位于 `packages.config` `.nuget` 解决方案根下的文件夹下，并且将仅存储解决方案级包。

### <a name="remove-new-package-command"></a>删除 New-Package 命令
由于使用率低，已删除 New-Package 命令。 建议开发人员使用 nuget.exe 或便捷的 NuGet 包资源管理器来创建包。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.7 在包还原工作流和网络/源代码管理方案周围修复了很多 bug。

有关 NuGet 1.7 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
