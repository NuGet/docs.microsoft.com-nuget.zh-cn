---
title: NuGet 2.2 发行说明
description: NuGet 2.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780430"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 发行说明

[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)  | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)

NuGet 2.2 于2012年12月12日发布。

## <a name="visual-studio-quick-launch"></a>Visual Studio 快速启动
Visual Studio 2012 中新增的一项功能是 " [快速启动" 对话框](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。 NuGet 2.2 扩展了此对话框，使其能够通过 "快速启动" 中输入的搜索词初始化 "包管理器" 对话框。 例如，在 "快速启动" 中输入 "jquery" 现在会在结果中包含一个选项，用于搜索匹配 "jquery" 的 NuGet 包。

![Visual Studio 快速启动中的 NuGet](./media/quick-launch.png)

选择此选项将启动术语 "jquery" 的标准 NuGet 包管理器搜索体验。

![预填充的 "NuGet 包管理器" 对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>为包内容指定整个文件夹
NuGet 2.2 现在允许在文件的元素中指定整个文件夹， `<file>` `.nuspec` 以包含该文件夹的所有内容。 例如，当包安装到项目中时，以下将导致程序包的 scripts 文件夹中的所有脚本都添加到 contents\scripts 文件夹中。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新6/24/16：安装包时忽略 "content" 文件夹中的空文件夹。**

## <a name="known-issues"></a>已知问题

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>使用包管理器控制台时，F # 项目的包安装失败
尝试使用 package manager console 将 NuGet 包安装到 F # 项目时，将引发 InvalidOperationException。 我们正在积极地与 F # 团队合作解决此问题，但在这种情况下，解决方法是通过 NuGet 的包管理器对话框而不是控制台将 NuGet 包安装到 F # 项目。 有关[详细信息，请访问 CodePlex](http://nuget.codeplex.com/workitem/2873)。


## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2 包含多个 bug 修复。 有关 NuGet 2.2 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
