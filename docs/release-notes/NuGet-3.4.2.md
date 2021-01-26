---
title: NuGet 3.4.2 发行说明
description: NuGet 3.4.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780251"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 发行说明

[NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)  | [NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 于2016年4月8日发布，以解决3.4 和3.4.1 版本中标识的多个问题。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 现已推出

可在 [此处](https://dist.nuget.org/index.html)下载 nuget.exe 3.4.2 的候选发布版本。

## <a name="updates-and-improvements"></a>更新和改进

* 在特定方案中，我们大大提高了更新的性能，在此方案中，具有深层依赖项关系图的包上的更新花了很长时间并挂起了 Visual Studio。
* 不带网络流量的 nuget 还原在 Visual Studio 中速度为 2.5 x –3倍。
* 除了此更改之外，我们还修复了一个问题，即在 VS UI 中提取更新计数时，我们将网络命中了两次。 这部分负责在 3.4/3.4.1 中遇到的客户遇到一些超时问题。
* 添加了 no_proxy 设置支持

## <a name="fixes"></a>修复项

* 修复了更新到3.4.1 后，NuGet 设置或配置中缺少 nuget.org 源的问题。
* 修复了3.4.1 中断 Artifactory 时，大小写更改为 FindPackagesById 的问题。
* 更正了导致 NuGet 还原失败的 FIPS 的问题，nuget.exe。
* 修复了浏览具有无效图标 URL 的源时出现的故障。
* 修复了合并版本和条目来自 "所有源" 的问题。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 Windows x86 命令行 (RC 中的已知问题) 

这些问题将在第一周的第一周提前修复，然后再进行 RTM。

*  如果解决方案文件位于低于项目文件的文件夹层次结构中，则在解决方案上运行 nuget 还原将会失败。
*  使用 V2 馈送对包运行 nuget delete 命令将失败。 请改用 V3 馈送。


有关此版本中的修复和改进的完整列表，请查看 [此处](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)的问题列表。