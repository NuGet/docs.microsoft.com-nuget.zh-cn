---
title: NuGet 3.4.4 发行说明
description: NuGet 3.4.4 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780231"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 发行说明

[NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md)  | [NuGet 3.5-测试版发行说明](../release-notes/nuget-3.5-Beta.md)

此版本的主要重点是对3.4.3 版本 nuget.exe 的质量进行了改进，同时对 Visual Studio 扩展进行了一些修补。

可在 [此处](https://dist.nuget.org/index.html)下载 VSIX 和 nuget.exe。

## <a name="344-rtm-2016-05-19"></a>[3.4.4](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19) 

[完整 Changelog](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>更改

- 包改进：对封装符号、封装方式 `project.json` 和[ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)进行了改进
- 在 update 命令中查找项目失败时显示异常 [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- `.nuspec` `project.json` 当打包[ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)时，从输入中读取包类型
- 创建 NuGet。共享不是项目。 [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- 使用推送超时作为 HTTP 响应超时[ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- 使用未来时间的包文件的时间不会超过[ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- `NuGet.Core.dll`将版本更新为2.12.0 以修复 XML 问题[ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- 支持。/NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- 显示错误还原（不含 `project.json` 或 `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) ）
- 当所需版本不同时修复依赖项版本[ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)