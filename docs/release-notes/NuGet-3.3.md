---
title: NuGet 3.3 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.3 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546642"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 发行说明

[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 已于 2015 年 11 月 30 日与大量用户界面更新和命令行功能，以及一系列有用的 NuGet 客户端的修补程序的发布。

## <a name="new-features"></a>新增功能

* 已引入，允许 NuGet 命令行客户端能够无缝使用已经过身份验证源的凭据提供程序。 [说明如何安装 Visual Studio Team Services 凭据提供程序](../api/nuget-exe-credential-providers.md)和配置 NuGet 客户端使用它位于 NuGet 文档。

## <a name="new-user-interface-features"></a>新用户界面功能

* 单独的浏览、 已安装，且更新可用的选项卡
* 更新可用徽章，指示有可用更新的包的数目
* 包在包列表中，指明是否安装包徽章或有可用更新
* 下载计数和作者添加到包列表
* 最高可用的版本编号和在包列表中的当前安装的版本编号
* 操作按钮，以允许快速安装、 更新和卸载从包列表
* 包详细信息面板上更清晰的操作按钮
* 在包详细信息面板上的包更新日期
* 合并在解决方案视图的面板
* 项目和解决方案视图上已安装的版本号的可排序网格

## <a name="new-command-line-features"></a>命令行的新功能

在此版本中我们引入了`add`并`init`命令来初始化基于文件夹的存储库中所述[nuget.exe 参考](../tools/nuget-exe-cli-reference.md)。 存储库构造和维护与此文件夹结构，将[提供了显著的性能好处](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我们的博客上所述。

## <a name="contentfiles"></a>ContentFiles

中现在支持内容`project.json`托管的新项目`contentFiles`文件夹并`.nuspec``contentFiles`元素表示法。  此内容可以更直接地指定由包的作者与项目系统之间的交互。  详细了解如何配置中的 contentFiles`.nuspec`中可以找到文档[.nuspec 引用](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 局部变量缓存管理

NuGet 命令行已更新以包括有关如何管理工作站上的本地缓存信息。  中提供了有关局部变量命令的详细信息[NuGet 命令行参考](../tools/cli-ref-locals.md)。

## <a name="fixed-issues"></a>已解决的问题

**值得注意的问题**

* 用于还原的 NuGet 命令行还原的支持打包在一起 Mono 的上一个解决方案文件[1543年](https://github.com/NuGet/Home/issues/1543)

可以在 GitHub 上找到 3.3 版本中已解决的问题的完整列表[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。

在中记录的 3.3 的命令行版本中修复的问题列表[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。

## <a name="known-issues"></a>已知问题

我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)