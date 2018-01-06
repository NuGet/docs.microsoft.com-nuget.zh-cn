---
title: "NuGet 2.2 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.2 的发行说明。"
keywords: "NuGet 2.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1f6080e01777431c4dfb2278db167bd3bc9a67ea
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 发行说明

[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)

NuGet 2.2 已于 2012 年 12 月 12 日发布。

## <a name="visual-studio-quick-launch"></a>Visual Studio 快速启动
已添加到 Visual Studio 2012 中的新功能之一是[快速启动对话框](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。 NuGet 2.2 扩展此对话框中，使其能够与在快速启动中输入搜索词初始化包管理器对话框。 例如，现在在快速启动中输入 jquery 将包括在结果中要搜索匹配 jquery 的 NuGet 包的选项。

![NuGet 在 Visual Studio 快速启动](./media/quick-launch.png)

选择此选项将启动长期 jquery 的标准 NuGet 包管理器搜索体验。

![预填充的 NuGet 包管理器对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>指定有关包内容的整个文件夹
NuGet 2.2 现在允许你指定中的整个文件夹`<file>`元素`.nuspec`要包含该文件夹的内容的所有文件。 例如，以下将导致所有脚本在包的脚本文件夹中以包安装到项目时添加到 contents\scripts 文件夹。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新 6/24/16： 安装包时，将忽略空文件夹中的"内容"文件夹。**

## <a name="known-issues"></a>已知问题

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>使用包管理器控制台时，软件包安装失败，对于 F # 项目
当尝试将 NuGet 包安装到 F # 项目使用包管理器控制台，则会引发 InvalidOperationException。 我们正在积极处理与 F # 团队以解决此问题，但在此期间，解决方法是将 NuGet 包安装到 F # 项目中的 NuGet 包管理器对话框而不是控制台通过。 [CodePlex 上提供了详细信息](http://nuget.codeplex.com/workitem/2873)。


## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2 包括许多的 bug 修补程序。 有关工作的完整列表项固定在 NuGet 2.2 中请视图[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
