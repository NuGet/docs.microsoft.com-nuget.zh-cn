---
title: NuGet 3.1 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.1 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545342"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 发行说明

[NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)

NuGet 3.1 2015 年 7 月 27 日作为发布对通用 Windows 平台 SDK 的捆绑扩展插件用于 Visual Studio 2015。 我们提供了此版本中的使用 Windows 平台 SDK，以便 Windows 开发体验无法利用以前已经开始的 NuGet 跨平台工作。 此 NuGet 扩展版本才可用于 Visual Studio 2015。

我们建议有权访问不可用，因为我们始终要发布包含 bug 修复和新功能更新的最新版本的 Visual Studio 库更新这些开发人员。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 扩展

问题和在此版本中的功能标记使用 GitHub 上["3.1 RTM UWP 可传递支持"里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)总的来说，我们已关闭的 67 3.1 发行版中的问题。

### <a name="new-features"></a>新增功能

* `project.json` 支持 Windows UWP 和 ASP.NET 5 支持
* 可传递的包安装

说明和定义的这些功能可以将其他位置的文档中找到。

### <a name="deprecated"></a>不推荐使用

以下功能将不再可用于 Visual Studio 2015:

* 不能再将解决方案级别包安装

以下功能将不再适用于 Visual Studio 2015 和使用的项目`project.json`规范

* `install.ps1` 和`uninstall.ps1`-这些脚本将包安装过程中忽略、 还原、 更新和卸载
* 配置转换将被忽略
* 将执行，但不是复制到项目的内容。
    * 团队正在努力重新实现此功能、 关注讨论和在进度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知问题

没有随此版本的已知问题的数量。

* 版本与 Windows 10 SDK 的版本 3.1 安装将以前安装的 NuGet 任何的扩展版本降级

## <a name="nuget-command-line"></a>NuGet 命令行

NuGet 命令行可执行文件已更新，并且移动到新的可分发位置，以便历史版本的 nuget.exe 继续可用。  可以为 Windows 在下载 nuget.exe 3.1 beta 的版本： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的可分发位置位于在 dist.nuget.org 主机上，遵循此模板的文件夹结构：

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新增功能

* nuget.exe 可以恢复，并将包安装到使用的项目`project.json`文件。
* nuget.exe 可以连接到并使用在 NuGet v3 协议： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知问题 ##

1.    无法执行包针对`project.json`文件- [928](https://github.com/NuGet/Home/issues/928)
2.    不支持 Mono- [1059年](https://github.com/NuGet/Home/issues/1059)
3.    未本地化- [1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)
4.    未签名，就像现有 http://nuget.org/nuget.exe  -  [1073年](https://github.com/NuGet/Home/issues/1073)
