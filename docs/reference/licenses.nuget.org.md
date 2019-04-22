---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921554"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>阐释

通过引入[许可证表达式](nuspec.md#license)，一项要求出现了用来将提供单个许可证标识符、 异常标识符或许可证表达式引用文本的可靠服务。
此服务的一个额外的要求是具有稳定的 URL 架构，不是易受链接 rot，以便我们可以安全地用于较旧的客户端提供向后兼容性。

Licenses.nuget.org 可满足该角色。 Nuget.org 使用它来为包指定其许可证的使用许可证表达式提供许可证文本引用。 `nuget pack` 或与其他包装[客户端工具](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)设置[ `licenseUrl` ](nuspec.md#licenseurl)元素以指向 licenses.nuget.org 以提供向后兼容性与旧版客户端不支持的`license`元素。

## <a name="protocol"></a>协议

Licenses.nuget.org 用于查看他们的浏览器中的人员，提供没有机器可读的响应。
必须使用 HTTPS 协议，并且请求要求以特定方式构造。 它仅支持`GET`请求。
它接受许可证表达式或许可证异常标识符作为输入下面指定的方式。 请注意，许可证表达式的所有元素都均区分大小写，因此所有输入 licenses.nuget.org 都也区分大小写。

### <a name="license-expressions"></a>许可证表达式

#### <a name="request"></a>请求

许可证 （包括普通的情况下，当表达式包含的单个许可证） 的表达式必须为[URL 编码](https://tools.ietf.org/html/rfc3986#section-2.1)，用作对 licenses.nuget.org 的请求中的路径。

| 许可证表达式 | 若要使用的 URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL 2.0-仅限使用 FLTK 异常或 Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

该服务仅支持许可证标识符和接受的 nuget.org 的许可证异常标识符。所有许可证表达式包含不受支持的许可证标识符或许可证异常标识符或不符合许可证表达式语法将被都视为无效。

#### <a name="response"></a>响应

Licenses.nuget.org 响应请求包含有效的许可证与 HTTP 200 状态代码和网页包含说明的许可证表达式的表达式：

* 如果提供许可证的表达式，包含单个许可证标识符，其中包含该许可证引用文本; 返回 web 页
* 如果提供许可证表达式是复合许可证表达式，包含与单个许可证或许可证异常引用的链接许可证表达式返回 web 页。

包含 HTTP 404 响应中的某个许可证无效表达式结果的任何请求。

### <a name="license-exceptions"></a>许可证异常

#### <a name="request"></a>请求

许可证异常标识符必须是 URL 编码并将其用作到 licenses.nuget.org 请求中的路径。仅单个许可证异常标识符可以在单个请求中提供。 除了许可异常标识符没有其他字符可能在 URL 的路径部分中提供。

| 许可证异常标识符 | 若要使用的 URL |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>响应

Licenses.nuget.org 响应 HTTP 200 响应进行回应包含指定的许可证异常的引用文本的网页的已知的许可证异常标识符的请求。

包含不受支持的许可证异常标识符的任何请求会导致 HTTP 404 响应。