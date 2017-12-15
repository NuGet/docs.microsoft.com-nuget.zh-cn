---
title: "推送和删除，NuGet API |Microsoft 文档"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "发布服务允许客户端发布新的包以及不列出或删除现有包。"
keywords: "NuGet API 推送包 NuGet API 删除包、 NuGet API 不列出包，NuGet API 上载包、 NuGet API 创建包"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a>推送和删除

可以推送和删除 （或不列出，具体取决于服务器实现） 包使用 NuGet V3 API。
这两种操作基于注销`PackagePublish`资源位于[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值          | 说明
-------------------- | -----
PackagePublish/2.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是值`@id`属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。 下面的文档中，使用 nuget.org 的 URL。 请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。

请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。

## <a name="http-methods"></a>HTTP 方法

`PUT`和`DELETE`此资源支持 HTTP 方法。 有关每个终结点支持的方法，请参阅下面。

## <a name="push-a-package"></a>推送包

nuget.org 支持使用以下 API 的推送新包。 如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。 其他包源可能支持替换现有包。

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
X NuGet ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

API 密钥是由用户从包源收到以及配置到客户端不透明的字符串。 没有特定字符串格式都将托管，但 API 密钥的长度不应超过合理的大小为 HTTP 标头值。

### <a name="request-body"></a>请求正文

请求正文必须采用以下形式：

#### <a name="multipart-form-data"></a>多部分窗体数据

请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是被按.nupkg 的原始字节。 多部分正文中的后续项将被忽略。 忽略的文件名称或任何其他标头的多部分项。

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
201, 202    | 成功推送包
400         | 提供的包无效
409         | 具有提供的 ID 和版本的包已存在

服务器实现上成功状态代码返回成功推送包时存在差异。

## <a name="delete-a-package"></a>删除包

nuget.org 解释为包删除请求的"不列出"。 这意味着包仍可用于现有的包的使用者，但包不会再出现在搜索结果中或在 web 界面。 有关这种做法的详细信息，请参阅[删除包](../policies/deleting-packages.md)策略。 其他服务器实现可以自由地解释为硬删除此信号、 软删除，或不列出。 例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持为 unlist 或硬删除基于配置选项处理此请求。

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
Id             | URL    | string | 是      | 要删除的包 ID
VERSION        | URL    | string | 是      | 要删除的包的版本
X NuGet ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
204         | 删除此包，
404         | 利用所提供的任何包`ID`和`VERSION`存在
