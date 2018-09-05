---
title: NuGet 1.7 版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.7 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551462"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 版发行说明

[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md) | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)

NuGet 1.7 已于 2012 年 4 月 4 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。

解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。  有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>安装后打开 readme.txt 文件的支持
中的新增功能 1.7，如果您的包包括`readme.txt`NuGet 包的根目录处文件将自动打开此文件之后它已完成安装您的包。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在管理 NuGet 包对话框中显示预发行包
管理 NuGet 包对话框中现在包含一个下拉列表，其中提供了选项，以显示预发行包。

![显示预发行包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>缺少包文件时显示包还原按钮
当打开包管理器控制台或管理器 NuGet 包对话框时，NuGet 将检查当前解决方案已启用包还原模式下，如果任何包文件中缺少`packages`文件夹。 如果满足这两个条件，NuGet 会通知你，将显示一个方便访问的还原按钮。 单击此按钮会触发 NuGet 还原缺少的所有包。

![在对话框中的包还原按钮](./media/packagerestore-dialog.png)

![在控制台上的包还原按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>添加解决方案级 packages.config 文件
在以前版本的 NuGet，每个项目具有`packages.config`文件，它将跟踪该项目中安装了哪些 NuGet 程序包。 但是，没有类似文件在解决方案级别来跟踪解决方案级别包。 因此，没有方法来还原解决方案级别包。
在 NuGet 1.7 中现在实现此功能。 解决方案级`packages.config`文件将位于下`.nuget`解决方案下的文件夹根，并将存储仅解决方案级别包。

### <a name="remove-new-package-command"></a>删除新建包命令
由于低使用率，已删除新建程序包命令。 开发人员建议使用 nuget.exe 或方便 NuGet 包资源管理器来创建包。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.7 已修复的包还原工作流和网络/源代码管理方案方面的许多缺陷。

有关完整列表的工作项中已修复 NuGet 1.7，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
