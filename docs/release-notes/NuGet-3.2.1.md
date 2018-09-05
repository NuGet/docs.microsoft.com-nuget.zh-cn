---
title: NuGet 3.2.1 发行说明
description: NuGet 3.2.1 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548185"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 发行说明

[NuGet 3.2 发行说明](../release-notes/nuget-3.2.md) | [NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)

有关命令行中的 NuGet 3.2.1 已于 2015 年 10 月 12 日发布了几个优化和 3.2 版本的修补程序，可从[dist.nuget.org](http://dist.nuget.org/index.html)。

## <a name="improvements"></a>改进

* NuGet 现在使用配置文件时使用的原始大小写`NuGet.Config`。  这一点在区分大小写的操作系统上[1427年](https://github.com/NuGet/Home/issues/1427)
* NuGet 还原现在将忽略 dnx 项目 (`*.xproj`) 应具有处理`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)
* 使用时，优化网络利用率`index.json`并将其打包注册数据[1426年](https://github.com/NuGet/Home/issues/1426)
* 处理，与 v2 服务更加稳定可靠的改进的资源下载[1448年](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修补程序

* NuGet 更新是否能够正确更新`.csproj` / `.vcxproj`引用[1483年](https://github.com/NuGet/Home/issues/1483)
* 现在阻止本地.nuget 文件夹时 SpecialFolders.UserProfile 找不到创建[1531年](https://github.com/NuGet/Home/issues/1531)
* 改进了在下载过程中损坏的包在本地缓存中的处理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)

可以在 NuGet GitHub 中找到的命令行和 Visual Studio 扩展已解决的问题的完整列表[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>已知问题

我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)