---
title: NuGet 3.3 发行说明
description: NuGet 3.3 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776509"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 发行说明

[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md)  | [NuGet 3.4-RC 发行说明](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 于2015年11月30日发布，具有大量用户界面更新和命令行功能，以及对 NuGet 客户端的有用修补程序的集合。

## <a name="new-features"></a>新功能

* 引入了凭据提供程序，使 NuGet 命令行客户端能够与经过身份验证的源无缝协作。 NuGet 文档中提供了有关[如何安装 Visual Studio Team Services 凭据提供程序以及如何](../reference/extensibility/nuget-exe-credential-providers.md)配置 nuget 客户端以使用该提供程序的说明。

## <a name="new-user-interface-features"></a>新的用户界面功能

* 单独的浏览、已安装和更新可用选项卡
* 更新可用徽章，指示包含可用更新的包数
* 包列表中的包徽章，用来指示包是否已安装或是否有可用更新
* 添加到包列表的下载计数和作者
* 包列表中可用的最高版本号和当前安装的版本号
* 允许从包列表快速安装、更新和卸载的操作按钮
* 包详细信息面板中更清晰的操作按钮
* 包更新日期包详细信息面板
* 解决方案视图中的合并面板
* 项目的可排序网格和解决方案视图上安装的版本号

## <a name="new-command-line-features"></a>新的命令行功能

在此版本中，我们引入了 `add` 和 `init` 命令以初始化基于文件夹的存储库，如 [nuget.exe 参考](../reference/nuget-exe-cli-reference.md)中所述。 通过此文件夹结构构造和维护的存储库将 [提供重要的性能优势](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) ，如博客中所述。

## <a name="contentfiles"></a>ContentFiles

在托管项目中， `project.json` 通过新 `contentFiles` 文件夹和 `.nuspec` `contentFiles` 元素表示法现在支持内容。  包作者可以更直接指定此内容以与项目系统交互。  有关如何在文档中配置 contentFiles 的详细信息， `.nuspec` 请参阅 [nuspec 引用](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 局部变量缓存管理

NuGet 命令行已更新，以包括有关如何管理工作站上的本地缓存的信息。  [NuGet 命令行参考](../reference/cli-reference/cli-ref-locals.md)中提供了有关局部变量命令的详细信息。

## <a name="fixed-issues"></a>已解决的问题

**值得注意的问题**

* NuGet 命令行已还原对在 Mono 上使用解决方案文件还原包的支持- [1543](https://github.com/NuGet/Home/issues/1543)

3.3 版本中解决的问题的完整列表可在 GitHub 上的 [3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。

3.3 命令行版本中修复的问题列表记录在 [3.3 Command-Line 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。

## <a name="known-issues"></a>已知问题

我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)