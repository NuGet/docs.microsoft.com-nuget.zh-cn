---
title: NuGet 2.9-RC 发行说明
description: NuGet 2.9 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780323"
---
# <a name="nuget-29-rc-release-notes"></a>NuGet 2.9-RC 发行说明

[NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md)  | [NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 在9月10日发布2015，作为 Visual Studio 2012 和2013的 2.8.7 VSIX 更新。

### <a name="updates-in-this-release"></a>此版本中的更新

* 现在，如果其包含的文档格式不正确，则跳过处理包 `.nuspec` - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* 更正了针对 Unix/Linux 方案的 \r\n multipartwebrequest 处理- [776](https://github.com/NuGet/Home/issues/776)
* 更正了与 Visual Studio 2013 社区版中的生成事件的集成- [1180](https://github.com/NuGet/Home/issues/1180)


此版本中的修补程序的完整列表可在 GitHub 上的[2.8.8 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)中找到
