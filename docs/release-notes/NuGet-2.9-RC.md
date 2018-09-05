---
title: NuGet 2.9 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.9 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548319"
---
# <a name="nuget-29-rc-release-notes"></a>NuGet 2.9 RC 发行说明

[NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 已于 2015 年 9 月 10 日发布作为到 2.8.7 更新 VSIX 中的进行 Visual Studio 2012 和 2013年。

### <a name="updates-in-this-release"></a>此版本中的更新

* 现在跳过处理包，如果其包含`.nuspec`文档的格式不正确- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* 更正的 Unix/Linux 方案-\r\n multipartwebrequest 处理[776](https://github.com/NuGet/Home/issues/776)
* 更正了与 Visual Studio 2013 Community edition-中的生成事件的集成[1180年](https://github.com/NuGet/Home/issues/1180)


在此版本中的修补程序的完整列表可在 GitHub 上的[2.8.8 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
