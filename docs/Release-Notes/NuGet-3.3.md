---
title: NuGet 3.3 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.3 的发行说明。
keywords: NuGet 3.3 发行说明，bug 修复的已知问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 发行说明

[NuGet 3.2.1 发行说明](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 已释放 2015 年 11 月 30 日与大量的用户界面更新和命令行功能，以及有用修复 NuGet 客户端的集合。

## <a name="new-features"></a>新增功能

* 已引入，允许 NuGet 命令行客户端能够无缝配合使用经过身份验证的源的凭据提供程序。 [说明如何安装 Visual Studio Team Services 凭据提供程序](../api/nuget-exe-credential-providers.md)和配置 NuGet 客户端使用它位于 NuGet Docs。

## <a name="new-user-interface-features"></a>新的用户界面功能

* 浏览、 已安装，和更新可用的单独选项卡
* 更新可用徽章，该值指示具有可用的更新的程序包数
* 在包列表中以指示是否将包安装到或有一个更新的包徽章
* 下载计数和作者添加到包列表
* 最高可用的版本编号和包列表上的当前安装的版本编号
* 操作按钮，以允许快速安装、 更新和卸载从包列表
* 包详细信息面板上的清楚地了解操作按钮
* 包详细信息面板上的包更新日期
* 合并解决方案视图中的面板
* 可排序网格的项目和安装的版本号，在解决方案视图

## <a name="new-command-line-features"></a>新的命令行功能

在此版本中，我们将介绍`add`和`init`命令来初始化基于文件夹的存储库中所述[nuget.exe 引用](../tools/nuget-exe-cli-reference.md)。 存储库构造并维护与此文件夹结构将[提供显著的性能优势](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我们的博客上所述。

## <a name="contentfiles"></a>ContentFiles

中现在支持内容`project.json`托管通过新的项目`contentFiles`文件夹和`.nuspec``contentFiles`元素表示法。  与项目系统的交互的包作者可以更直接指定此内容。  有关如何配置中的文件的详细信息`.nuspec`在找不到文档[.nuspec 引用](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 局部变量缓存管理

NuGet 命令行已更新以包括有关如何管理工作站上的本地缓存的信息。  中提供了有关局部变量命令的详细信息[NuGet 命令行参考](../tools/cli-ref-locals.md)。

## <a name="fixed-issues"></a>已解决的问题

**值得注意的问题**

* NuGet 命令行对还原的还原的支持包解决方案上具有文件 Mono- [1543年](https://github.com/NuGet/Home/issues/1543)

在 3.3 版本中已解决的问题的完整列表可以在 GitHub 上找到[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。

在 3.3 命令行版本中修复的问题的列表中记录[3.3 命令行里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。

## <a name="known-issues"></a>已知问题

我们将继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)