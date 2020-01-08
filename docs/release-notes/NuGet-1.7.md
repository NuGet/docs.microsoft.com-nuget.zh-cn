---
title: NuGet 1.7 发行说明
description: NuGet 1.7 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383314"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 发行说明

[Nuget 1.6 发行说明](../release-notes/nuget-1.6.md) | [Nuget 1.8 发行说明](../release-notes/nuget-1.8.md)

NuGet 1.7 于年4月 4 2012 日发布。

## <a name="known-installation-issue"></a>已知安装问题
如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。

解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。  有关更多信息，请参见<https://support.microsoft.com/kb/2581019>。

注意：如果 Visual Studio 不允许你卸载扩展（"卸载" 按钮已禁用），则可能需要使用 "以管理员身份运行" 重启 Visual Studio。

## <a name="features"></a>特征

### <a name="support-opening-readmetxt-file-after-installation"></a>支持在安装后打开 readme.txt 文件
1\.7 中的新增内容，如果你的包在包的根目录中包含一个 `readme.txt` 文件，则在安装完包之后，NuGet 将自动打开此文件。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在 "管理 NuGet 包" 对话框中显示预发行包
"管理 NuGet 包" 对话框现在包含一个下拉列表，其中提供了显示预发行包的选项。

![显示预发行包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>缺少包文件时显示 "包还原" 按钮
打开 "程序包管理器控制台" 或 "管理器 NuGet 包" 对话框时，NuGet 将检查当前解决方案是否已启用包还原模式，以及 `packages` 文件夹中是否缺少任何包文件。 如果满足这两个条件，NuGet 会通知你，并显示一个便利的 "还原" 按钮。 单击此按钮将触发 NuGet 以还原所有缺少的包。

![对话框上的 "包还原" 按钮](./media/packagerestore-dialog.png)

![控制台上的 "包还原" 按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>添加解决方案级包 .config 文件
在 NuGet 的早期版本中，每个项目都有一个 `packages.config` 文件，该文件跟踪在该项目中安装的 NuGet 包。 不过，解决方案级别没有类似的文件来跟踪解决方案级包。 因此，无法还原解决方案级包。
此功能现已在 NuGet 1.7 中实现。 解决方案级 `packages.config` 文件位于解决方案根下的 `.nuget` 文件夹下，并且将仅存储解决方案级包。

### <a name="remove-new-package-command"></a>删除新包命令
由于使用率低，已删除新包命令。 建议开发人员使用 nuget.exe 或方便的 NuGet 包资源管理器来创建包。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.7 在包还原工作流和网络/源代码管理方案周围修复了很多 bug。

有关 NuGet 1.7 中已修复的工作项的完整列表，请查看[此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
