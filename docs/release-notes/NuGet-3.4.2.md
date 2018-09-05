---
title: NuGet 3.4.2 发行说明
description: NuGet 3.4.2 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549146"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 发行说明

[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 已于 2016 年 4 月 8，若要解决几个在 3.4 和 3.4.1 中发现的问题，发布版本。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 现已推出

您可以下载 release candidate 的 nuget.exe 3.4.2[此处](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和改进

* 我们显著改进性能的特定方案中，其中有深入的依赖项关系图的包上的更新需要花费很长时间，挂起 Visual Studio 中的更新。
* nuget 还原，而无需网络流量是 2.5 倍 – Visual Studio 中更快 3 倍。
* 除了此更改后，我们已解决了问题，我们已达到网络，两次时 VS UI 中提取更新计数。 这是部分负责方面具有丰富经验 3.4/3.4.1 某些超时问题客户。
* 添加了的对 no_proxy 设置

## <a name="fixes"></a>修补程序

* 修复了其中 nuget.org 源中缺少 NuGet 设置或配置更新到 3.4.1 后。
* 修复了在何处对 FindPackagesById 3.4.1 中的大小写更改断开 Artifactory。
* 更正了 FIPS 使用 nuget.exe 的 NuGet 还原导致失败的问题。
* 浏览具有无效的图标 URL 源时，修复了故障。
* 修复了与合并版本和所有源中的条目的问题。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>上面 3.4.2 中的已知问题 Windows x86 命令行 (版本 RC)

将早期的下一步一周前我们碰到 RTM 修复这些问题。

*  如果解决方案文件放置在与项目文件的较低的文件夹层次结构中，对解决方案运行 nuget 还原将失败。
*  使用 V2 源的包上运行 nuget delete 命令将失败。 改为使用 V3 源。


有关此版本中的修补程序和改进的完整列表，请参阅问题列表[此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。