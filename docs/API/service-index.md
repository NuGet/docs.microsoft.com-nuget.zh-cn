---
title: "服务索引、 NuGet API |Microsoft 文档"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f6d6cf2-53fb-417a-b1d8-e0ac591c1699
description: "服务索引是 NuGet HTTP API 的入口点，并枚举服务器的功能。"
keywords: "NuGet API 入口点，NuGetA PI 终结点发现"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 0c43a09d8564964bd0140b9ac5deb9d3063e4dc5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="service-index"></a>服务索引

服务索引是一个 JSON 文档，是 NuGet 程序包源的入口点，并允许一个客户端实现，以发现包源的功能。 服务索引是具有两个必需属性的 JSON 对象： `version` （服务索引的架构版本） 和`resources`（终结点或功能的包源）。

nuget.org 的服务索引的位置如下：
```
https://api.nuget.org/v3/index.json
```

## <a name="versioning"></a>版本管理

`version`值是 SemVer 2.0.0 解析，因此版本字符串，它指示服务索引的架构版本。
API 规定的版本字符串有的一个主要版本号`3`。 对服务索引架构进行非重大更改时，将增加的版本字符串的次要版本。

服务索引中的每个资源是版本控制独立于服务索引架构版本。

当前架构版本是`3.0.0-beta.1`。

## <a name="http-methods"></a>HTTP 方法

服务索引是使用 HTTP 方法可以访问`GET`和`HEAD`。

## <a name="resources"></a>资源

`resources`属性包含此包源所支持的资源的数组。

### <a name="resource"></a>资源

资源是中的对象`resources`数组。 它表示包源已进行版本管理功能。 资源具有以下属性：

名称          | 类型   | 必需 | 说明
------------- | ------ | -------- | -----
@id           | string | 是      | 资源的 URL
@type         | string | 是      | 一个字符串常量，代表资源类型
注释       | string | no       | 资源的人工可读说明

`@id`是 URL 必须是绝对路径，必须具有 HTTP 或 HTTPS 的架构。

`@type`用于标识要使用与资源交互时的特定协议。 资源的类型是不透明的字符串，但通常采用格式：

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

客户端预期硬编码到`@type`它们了解并查找包源的服务索引中的值。 准确`@type`当今使用的值枚举中列出的单个资源引用文档[API 概述](overview.md#resources-and-schema)。

本文档中，为不同的资源有关的文档都实质上是将按`{RESOURCE_NAME}`类似于按方案分组服务索引中找到。 

不存在的每个资源具有一个唯一的要求`@id`或`@type`。 负责要确定哪些资源较另一种首选的客户端实现。 一个可能的实现是相同或兼容的资源`@type`可在发生连接故障或服务器错误一种轮循机制的方式。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [service-index.json](./_data/service-index.json)]
