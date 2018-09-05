---
title: NuGet 2.2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545987"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 发行说明

[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)

NuGet 2.2 已于 2012 年 12 月 12 日发布。

## <a name="visual-studio-quick-launch"></a>Visual Studio 快速启动
在 Visual Studio 2012 中已添加的新功能之一是[快速启动对话框](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。 NuGet 2.2 扩展了此对话框中，使其能够与在快速启动栏中输入的搜索条件初始化包管理器对话框。 例如，现在在快速启动中输入 jquery 将包括在结果中搜索匹配 jquery NuGet 包的选项。

![Visual Studio 快速启动中的 NuGet](./media/quick-launch.png)

选择此选项将启动术语 jquery 的标准 NuGet 包管理器搜索的体验。

![预填充的 NuGet 包管理器对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>指定包内容的整个文件夹
NuGet 2.2 现在允许你指定的整个文件夹中`<file>`元素的`.nuspec`文件来包含所有该文件夹的内容。 例如，以下将导致所有脚本要添加到 contents\scripts 文件夹中，当包安装到项目的包的脚本文件夹中。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新 6/24/16： 安装包时，"内容"文件夹中的空文件夹将被忽略。**

## <a name="known-issues"></a>已知问题

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>使用包管理器控制台时，软件包安装失败的 F # 项目
当尝试将 NuGet 程序包安装到 F # 项目使用包管理器控制台时，将引发 InvalidOperationException。 我们正在积极与 F # 团队来解决此问题，但在此期间，解决方法是将 NuGet 包安装到 F # 项目的 NuGet 包管理器对话框而不是在控制台通过。 [CodePlex 上提供了详细信息](http://nuget.codeplex.com/workitem/2873)。


## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2 包括许多 bug 修复。 有关工作的完整列表项中已修复 NuGet 2.2，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
