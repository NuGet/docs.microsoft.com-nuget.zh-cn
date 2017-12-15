---
title: "NuGet 1.7 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df7becc6-993d-4d06-8495-a0c26748bdfa
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.7 的发行说明。"
keywords: "NuGet 1.7 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 420b40576cb3862f0e4406966f9ccca9fd1f39a1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 版的发行说明

[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md) | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)

NuGet 1.7 已于 2012 年 4 月 4 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。

解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。  请参阅[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)有关详细信息。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>支持在安装后打开 readme.txt 文件
如果你的包包括在 1.7，新`readme.txt`根目录下的包，NuGet 的文件将自动打开此文件后它已完成安装你的包。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在管理 NuGet 包对话框中显示预发行程序包
管理 NuGet 包对话框现在包括一个下拉列表，它提供选项，可以显示预发行程序包。

![显示预发行程序包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>缺少包文件时显示程序包还原按钮
当你打开程序包管理器控制台或管理器 NuGet 包对话框，NuGet 将检查当前解决方案已启用的程序包还原模式并且任何包文件中缺少`packages`文件夹。 如果满足这两个条件，NuGet 将通知你，将显示一个方便的还原按钮。 单击此按钮将触发 NuGet 还原所有缺少的程序包。

![在对话框的包还原按钮](./media/packagerestore-dialog.png)

![在控制台上的包还原按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>添加解决方案级 packages.config 文件
在以前版本的 NuGet 中，每个项目有`packages.config`文件来跟踪哪些 NuGet 包安装在该项目。 但是，没有类似文件可以在解决方案级别来跟踪解决方案级包。 因此，没有方法来还原解决方案级程序包。
在 NuGet 1.7 中现在实现此功能。 解决方案级`packages.config`文件放置在`.nuget`下解决方案文件夹的根，并将存储解决方案仅级包。

### <a name="remove-new-package-command"></a>删除新建包命令
由于使用率低，新建包命令已被删除。 建议开发人员使用 nuget.exe 或方便 NuGet 包资源管理器来创建包。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.7 已修复 bug 的程序包还原工作流和网络/源控制方案都很多。

有关工作的完整列表项固定在 NuGet 1.7，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
