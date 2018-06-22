---
title: NuGet 2.9 RC 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.9 RC 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819370"
---
# <a name="nuget-29-rc-release-notes"></a>NuGet 2.9 RC 发行说明

[NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 发布于 2015 年 9 月 10 日为 2.8.7 的更新 Visual Studio 2012 和 2013 VSIX。

### <a name="updates-in-this-release"></a>在此版本的更新

* 现在跳过处理包，如果其包含`.nuspec`文档格式不正确- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* 更正的 Unix/Linux 方案-\r\n multipartwebrequest 处理[776](https://github.com/NuGet/Home/issues/776)
* 更正与在 Visual Studio 2013 Community 版本-生成事件的集成[1180年](https://github.com/NuGet/Home/issues/1180)


在此版本的修补程序的完整列表可以在 GitHub 上找到[2.8.8 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
