---
title: 服务索引，NuGet API
description: 服务索引是 NuGet HTTP API 的入口点，可枚举服务器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775361"
---
# <a name="service-index"></a>服务索引

服务索引是一个 JSON 文档，它是 NuGet 包源的入口点，并允许客户端实现发现包源的功能。 服务索引是一个具有两个必需属性的 JSON 对象： `version` (服务索引的架构版本) 并 `resources`  (包源) 的终结点或功能。

nuget.exe 的服务索引位于 `https://api.nuget.org/v3/index.json` 。

## <a name="versioning"></a>版本控制

`version`该值是一个 SemVer 2.0.0 不可解析版本字符串，它指示服务索引的架构版本。 API 规定版本字符串具有的主要版本号 `3` 。 由于对服务索引架构进行了非重大更改，将增加版本字符串的次要版本。

服务索引中的每个资源独立于服务索引架构版本进行了版本控制。

当前架构版本为 `3.0.0` 。 `3.0.0`版本在功能上等同于旧 `3.0.0-beta.1` 版本，但应首选此版本，因为它更清晰地传达稳定定义的架构。

## <a name="http-methods"></a>HTTP 方法

可以使用 HTTP 方法和访问服务索引 `GET` `HEAD` 。

## <a name="resources"></a>资源

`resources`属性包含此包源支持的资源的数组。

### <a name="resource"></a>资源

资源是数组中的对象 `resources` 。 它表示包源的版本控制功能。 资源具有以下属性：

名称          | 类型   | 必须 | 注释
------------- | ------ | -------- | -----
@id           | string | 是      | 资源的 URL
@type         | string | 是      | 表示资源类型的字符串常数
comment       | string | 否       | 用户可读的资源说明

`@id`是一个必须为绝对的 URL，并且必须具有 HTTP 或 HTTPS 架构。

`@type`用于标识与资源交互时要使用的特定协议。 资源的类型是不透明的字符串，但通常采用以下格式：

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

客户端应对它们理解的值进行硬编码 `@type` ，并在包源的服务索引中查找这些值。 `@type`当前使用的确切值基于[API 概述](overview.md#resources-and-schema)中列出的各个资源引用文档进行枚举。

对于本文档，有关不同资源的文档实质上是按 `{RESOURCE_NAME}` 服务索引中找到的，这类似于按方案分组。 

不要求每个资源都具有唯一的 `@id` 或 `@type` 。 由客户端实现确定要优先于另一种资源。 一个可能的实现是在 `@type` 出现连接故障或服务器错误的情况下，可以使用相同或兼容的资源。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [service-index.json](./_data/service-index.json)]
