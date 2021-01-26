---
title: NuGet 3.1 发行说明
description: NuGet 3.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776537"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 发行说明

[NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)  | [NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)

NuGet 3.1 已于年7月27日发布2015，作为 Visual Studio 2015 通用 Windows 平台 SDK 的捆绑扩展。 我们使用 Windows 平台 SDK 交付了此版本，以便 Windows 开发体验能够利用之前已启动的 NuGet 跨平台工作。 此 NuGet 扩展版本仅适用于 Visual Studio 2015。

我们建议那些有权访问 Visual Studio 库的开发人员更新到可用的最新版本，因为我们始终发布包含 bug 修复和新功能的更新。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 扩展

此版本中的问题和功能在 GitHub 上标记为 ["3.1 RTM UWP 可传递支持" 里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  ，在3.1 版本中关闭了67问题。

### <a name="new-features"></a>新功能

* `project.json` 支持 Windows UWP 和 ASP.NET 5 支持
* 可传递包安装

这些功能的说明和定义可在文档中的其他位置找到。

### <a name="deprecated"></a>已放弃

以下功能不再适用于 Visual Studio 2015：

* 解决方案级包无法再安装

以下功能不再适用于 Visual Studio 2015 和使用该规范的项目 `project.json`

* `install.ps1` 和 `uninstall.ps1` -包安装、还原、更新和卸载过程中将忽略这些脚本
* 将忽略配置转换
* 内容将携带，但不会复制到项目中。
    * 团队正在努力重新实现此功能，请按照以下主题中的讨论和进度进行操作： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知问题

此版本提供了许多已知问题。

* 安装 Windows 10 SDK 的3.1 版本将会降级之前安装的任何版本的 NuGet 扩展

## <a name="nuget-command-line"></a>NuGet 命令行

NuGet 命令行可执行文件已更新并移至新的可分发位置，因此可以继续使用 nuget.exe 的历史版本。  你可以在以下位置下载适用于 Windows 的 3.1 beta 版本的 nuget.exe： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的可分发位置位于 dist.nuget.org 主机上，其文件夹结构遵循以下模板：

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>新功能

* nuget.exe 可以还原包并将其安装到使用文件的项目中 `project.json` 。
* nuget.exe 可以连接到并使用 NuGet v3 协议，网址为： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知问题 ##

1.    无法对文件执行 pack `project.json` - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono- [1059](https://github.com/NuGet/Home/issues/1059)不支持
3.    未本地化- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)
4.    未签名，就像现有的 http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
