---
title: "NuGet 3.2.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "发行说明，了解 NuGet 3.2.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.2.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 发行说明

[NuGet 3.2 发行说明](../release-notes/nuget-3.2.md) | [NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)

NuGet 3.2.1 为命令行发布于 2015 年 10 月 12 日有少量的优化和 3.2 版本的修补程序，并且可从[dist.nuget.org](http://dist.nuget.org/index.html)。

## <a name="improvements"></a>改进

* NuGet 现在使用配置文件的原始大小写与`NuGet.Config`。  这是区分大小写的操作系统上重要[1427年](https://github.com/NuGet/Home/issues/1427)
* NuGet 还原现在将忽略 dnx 项目 (`*.xproj`) 应处理与`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)
* 使用时优化网络利用率`index.json`和包注册数据[1426年](https://github.com/NuGet/Home/issues/1426)
* 处理，与 v2 服务更加稳定可靠的改进的资源下载[1448年](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修补程序

* NuGet 更新是否能够正确更新`.csproj` / `.vcxproj`引用[1483年](https://github.com/NuGet/Home/issues/1483)
* 现在防止本地.nuget 文件夹时 SpecialFolders.UserProfile 找不到创建[1531年](https://github.com/NuGet/Home/issues/1531)
* 改进的在本地缓存中下载过程中损坏的包的处理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)

处理命令行和 Visual Studio 扩展可以在 NuGet GitHub 中找到有关问题的完整列表[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>已知问题

我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)