---
title: 推送和删除的 NuGet API
description: 发布服务允许客户端将新包发布和取消列出或删除现有的包。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426725"
---
# <a name="push-and-delete"></a>推送和删除

可以推送、 删除 （或取消列出，具体取决于服务器实现），并重新列出包使用 NuGet V3 API。 这些操作所基于的中断`PackagePublish`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值          | 说明
-------------------- | -----
PackagePublish/2.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是的值`@id`的属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。 以下文档中，使用 nuget.org 的 URL。 请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。

请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。

## <a name="http-methods"></a>HTTP 方法

`PUT`，`POST`和`DELETE`此资源支持 HTTP 方法。 有关每个终结点上支持哪些方法，请参阅下面。

## <a name="push-a-package"></a>将包推送

> [!Note]
> nuget.org 已[其他要求](NuGet-Protocols.md)与推送终结点进行交互。

nuget.org 支持推送新的包使用以下 API。 如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。 其他包源可能支持替换现有的包。

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

API 密钥是从包源获得由用户和配置到客户端不透明的字符串。 强制要求任何特定字符串格式，但 API 密钥的长度不应超过合理的大小，为 HTTP 标头值。

### <a name="request-body"></a>请求正文

请求正文必须采用以下形式：

#### <a name="multipart-form-data"></a>多部分窗体数据

请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是推送.nupkg 的原始字节。 多部分正文中后面的项将被忽略。 将忽略的文件的名称或任何其他标头的多部分项。

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
201, 202    | 已成功推送包
400         | 提供的包无效
409         | 已存在具有提供的 ID 和版本的包

服务器实现上成功状态代码返回成功推送包时存在差异。

## <a name="delete-a-package"></a>删除包

nuget.org 将解释为包删除请求的"取消列出"。 这意味着包仍可用于包的现有使用者，但包不会再出现在搜索结果中或 web 界面中。 有关这种做法的详细信息，请参阅[删除包](../nuget-org/policies/deleting-packages.md)策略。 其他服务器实现可以自由地解释为硬删除此信号，软删除，或取消列出。 例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持处理此请求作为未列出或硬删除基于配置选项。

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
Id             | URL    | string | 是      | 要删除的包 ID
VERSION        | URL    | string | 是      | 要删除的包的版本
X-NuGet-ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
204         | 删除此包，
404         | 利用所提供的任何包`ID`和`VERSION`存在

## <a name="relist-a-package"></a>重新列出包

如果某个包未列出，则就可以使该包在使用"重新列出"终结点的搜索结果中再次可见。 此终结点有形状[删除 （取消列出） 终结点](#delete-a-package)但使用`POST`HTTP 方法，而不是`DELETE`方法。

如果包已列出，请求仍会成功。

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
Id             | URL    | string | 是      | 重新列出包的 ID
VERSION        | URL    | string | 是      | 重新列出包的版本
X-NuGet-ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
200         | 现在，该包列
404         | 利用所提供的任何包`ID`和`VERSION`存在
