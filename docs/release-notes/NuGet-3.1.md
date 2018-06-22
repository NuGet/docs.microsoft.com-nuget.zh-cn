---
title: NuGet 3.1 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.1 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820856"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 发行说明

[NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)

NuGet 3.1 发布于 2015 年 7 月 27 日为通用 Windows 平台 SDK 的捆绑扩展 for Visual Studio 2015。 我们提供与 Windows 平台 SDK 的此版本，以便 Windows 开发体验可能会利用以前已经开始的 NuGet 跨平台工作。 此 NuGet 扩展版本仅可用于 Visual Studio 2015。

我们建议这些开发人员有权访问不可用，因为我们始终要发布 bug 修补程序和新功能的更新的最新版本的 Visual Studio 库更新。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 扩展

问题和此版本中的功能标记与 GitHub 上["3.1 RTM UWP 可传递支持"里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)，总共我们关闭 3.1 版本中的 67 问题。

### <a name="new-features"></a>新增功能

* `project.json` 支持针对 Windows UWP 和 ASP.NET 5 支持
* 可传递的包安装

说明和定义这些功能可以找到其他地方文档中。

### <a name="deprecated"></a>不推荐使用

以下功能将不再可用于 Visual Studio 2015:

* 解决方案级别程序包可以不再进行安装

以下功能将不再可用于 Visual Studio 2015 和使用的项目`project.json`规范

* `install.ps1` 和`uninstall.ps1`-这些脚本将包安装过程中忽略、 还原、 更新和卸载
* 将忽略配置转换
* 内容将执行，但不是复制到项目。
    * 团队正致力于重新实现此功能，请按照讨论和在进度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知问题

没有大量的时候附带此版本的已知问题。

* 使用 Windows 10 SDK 的 3.1 版本的安装将将以前已安装的 NuGet 任何的扩展版本降级

## <a name="nuget-command-line"></a>NuGet 命令行

NuGet 命令行可执行文件已更新，并移动到新的可分发位置，以便 nuget.exe 的历史版本可以继续将变得可。  你可以为在 Windows 上下载 nuget.exe 的 3.1 beta 版本： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的可分发位置位于在 dist.nuget.org 主机上，遵循此模板的文件夹结构：

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新增功能

* nuget.exe 可以恢复，并将包安装到使用的项目`project.json`文件。
* nuget.exe 可以连接到和使用 NuGet v3 协议： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知问题 ##

1.    无法执行包针对`project.json`文件- [928](https://github.com/NuGet/Home/issues/928)
2.    不支持 Mono- [1059年](https://github.com/NuGet/Home/issues/1059)
3.    未本地化的[1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)
4.    未签名，就像现有http://nuget.org/nuget.exe- [1073年](https://github.com/NuGet/Home/issues/1073)
