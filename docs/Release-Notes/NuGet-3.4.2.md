---
title: NuGet 上面 3.4.2 发行说明
description: 发行说明，了解 NuGet 上面 3.4.2 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-342-release-notes"></a>NuGet 上面 3.4.2 发行说明

[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)

NuGet 上面 3.4.2 已于 2016 年 4 月 8，以解决在 3.4 和 3.4.1 中识别的几个问题发布版本。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 上面 3.4.2 RC 现已推出

你可以下载 nuget.exe 上面 3.4.2 的候选发布版[此处](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和改进

* 我们显著改进性能的特定方案中，其中上有深入的依赖项关系图的包的更新所花很长时间，挂起 Visual Studio 中的更新。
* 而不会网络流量的 nuget 还原是 2.5 x-Visual Studio 中更快的 3 x。
* 除了此更改后，我们已解决问题，我们已达到网络，两次时提取更新计数的 VS UI。 这是部分负责 3.4/3.4.1 方面具有丰富经验某些超时问题客户。
* 添加了对 no_proxy 设置支持

## <a name="fixes"></a>修补程序

* 修复了问题 nuget.org 源所在 NuGet 的设置或配置中缺少更新到 3.4.1 后。
* 修复了问题中 3.4.1 FindPackagesById 大小写更改将 Artifactory 处中断。
* 更正 FIPS NuGet 还原与 nuget.exe 导致失败的问题。
* 浏览具有无效的图标 URL 源时，请修复崩溃。
* 修复了与合并版本和从 '所有资源' 的项的问题。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>上面 3.4.2 中的已知问题 Windows x86 命令行 (版本 RC)

将早期下周我们命中 RTM 之前修复这些问题。

*  如果解决方案文件放置在与项目文件的较低的文件夹层次结构，正在运行的解决方案的 nuget 还原将失败。
*  在包使用 V2 源上运行 nuget delete 命令将失败。 请改用 V3 源。


有关此版本中的修补程序和改进的完整列表，请参阅的问题列表[此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。