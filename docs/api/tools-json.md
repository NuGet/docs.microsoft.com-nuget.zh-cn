---
title: 用于发现 nuget.exe 版本的 tools.js
description: 的端点
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773812"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>用于发现 nuget.exe 版本的 tools.js

如今，有几种方法可以以可脚本方式在计算机上获取最新版本的 nuget.exe。 例如，可以从 nuget.org 下载并提取 [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) 包。这会带来一些复杂性，因为它要求您已经为) nuget.exe (， `nuget.exe install` 或者必须使用基本的解压缩工具来解压缩 nupkg，并在内部查找二进制文件。

如果你已经有 nuget.exe，则还可以使用 `nuget.exe update -self` ，但这也需要具有 nuget.exe 的现有副本。 此方法还会更新到最新版本。 它不允许使用特定版本。

`tools.json`终结点可用于解决启动问题，并提供对所下载 nuget.exe 版本的控制。 这可以用于 CI/CD 环境或自定义脚本，以发现和下载 nuget.exe 的任何发行版本。

`tools.json`可以使用未经身份验证的 HTTP 请求获取终结点 (例如， `Invoke-WebRequest` 在 PowerShell 中或 `wget`) 中。 使用 JSON 反序列化程序可以对其进行分析，后续 nuget.exe 还可以使用未经身份验证的 HTTP 请求获取下载 Url。

可以使用方法获取终结点 `GET` ：

```
GET https://dist.nuget.org/tools.json
```

此处提供终结点的 [JSON 架构](https://json-schema.org/) ：

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>响应

响应是一个 JSON 文档，其中包含所有 nuget.exe 的可用版本。

根 JSON 对象具有以下属性：

名称      | 类型             | 必须
--------- | ---------------- | --------
nuget.exe | 对象数组 | 是

数组中的每个对象 `nuget.exe` 具有以下属性：

名称     | 类型   | 必须 | 注释
-------- | ------ | -------- | -----
版本  | string | 是      | SemVer 2.0.0 字符串
url      | string | 是      | 下载此版本的 nuget.exe 的绝对 URL
阶段 (stage)    | string | 是      | 枚举字符串
上载 | string | 是      | 可用版本的大约 ISO 8601 时间戳

数组中的项将按降序、SemVer 2.0.0 顺序排序。 这一保证旨在降低对最高版本号感兴趣的客户端的负担。 但这意味着列表不按时间顺序进行排序。 例如，如果在较高的主要版本之前的日期提供较低的主要版本，则此服务版本将不会显示在列表的顶部。 如果需要由 *时间戳* 发布的最新版本，只需按字符串对数组进行排序即可 `uploaded` 。 这 `uploaded` 是因为时间戳采用 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 格式，可以使用字典排序 (例如，简单的字符串排序) 。

`stage`属性指示此版本工具的审查。 

阶段              | 含义
------------------ | ------
EarlyAccessPreview | 在 [下载](https://www.nuget.org/downloads) 网页上还不可见，应由合作伙伴验证
Released（已释放）           | 在下载站点上可用，但尚不建议用于跨范围使用
ReleasedAndBlessed | 在下载站点提供，建议用于使用

使用最新的建议版本的一种简单方法是采用列表中具有值的第一个版本 `stage` `ReleasedAndBlessed` 。 这是因为版本按 SemVer 2.0.0 顺序排序。

`NuGet.CommandLine`Nuget.org 上的包通常仅更新了 `ReleasedAndBlessed` 版本。

### <a name="sample-request"></a>示例请求

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [tools-json.json](./_data/tools-json.json)]
