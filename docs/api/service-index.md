---
title: 服务索引，NuGet API
description: 服务索引是 NuGet HTTP API 的入口点，并枚举服务器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545252"
---
# <a name="service-index"></a>服务索引

服务索引是一个 JSON 文档是 NuGet 包源的入口点，并允许客户端实现，若要了解包源的功能。 服务索引是一个具有两个必需属性的 JSON 对象： `version` （服务索引的架构版本） 和`resources`（终结点或功能的包源）。

nuget.org 的服务索引位于`https://api.nuget.org/v3/index.json`。

## <a name="versioning"></a>版本管理

`version`值是 SemVer 2.0.0 版本解析，因此字符串指示服务索引的架构版本。 API 要求的版本字符串有主版本号的`3`。 服务索引架构做出非重大更改后，会增加版本字符串的次要版本。

服务索引的每个资源是版本控制独立于服务索引的架构版本。

当前架构版本是`3.0.0`。 `3.0.0`版本在功能上等效于较旧`3.0.0-beta.1`版本但只是首选，因为它更清楚地传达稳定、 定义架构。

## <a name="http-methods"></a>HTTP 方法

服务索引是使用 HTTP 方法可以访问`GET`和`HEAD`。

## <a name="resources"></a>资源

`resources`属性包含此包源支持的资源数组。

### <a name="resource"></a>资源

资源是中的对象`resources`数组。 它表示包源的版本控制功能。 每个资源有以下属性：

name          | 类型   | 必需 | 说明
------------- | ------ | -------- | -----
@id           | 字符串 | 是      | 资源的 URL
@type         | 字符串 | 是      | 一个字符串常数，表示资源类型
注释       | 字符串 | 否       | 资源的人工可读说明

`@id`是 URL 必须是绝对路径，并且必须具有 HTTP 或 HTTPS 架构。

`@type`用于标识要与资源交互时使用的特定协议。 资源类型是不透明的字符串，但通常采用格式：

    {RESOURCE_NAME}/{RESOURCE_VERSION}

客户端应进行硬编码`@type`他们了解并查找包源的服务索引中的值。 确切`@type`枚举中列出的单个资源引用文档上目前所用的值[API 概述](overview.md#resources-and-schema)。

本文档中，为不同的资源有关的文档将实质上是按分组`{RESOURCE_NAME}`它类似于按方案进行分组的服务索引中找到。 

没有任何要求每个资源具有一个唯一`@id`或`@type`。 负责要确定哪些资源通过另一个首选的客户端实现。 一个可能的实现是相同或兼容的资源`@type`可以以轮循机制方式发生连接故障或服务器错误时使用。

### <a name="sample-request"></a>示例请求

获取 https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [service-index.json](./_data/service-index.json)]
