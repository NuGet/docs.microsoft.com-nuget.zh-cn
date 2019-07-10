---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427112"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>阐释

随着[许可证表达式](../reference/nuspec.md#license)的引入，出现了一种需求，即需要提供可靠的服务，为单个许可证标识符、异常标识符或许可证表达式提供参考文本。
此服务的另一个要求是具有稳定的 URL 架构，该架构不易受链接失效的影响，因此我们可以安全地使用它来为旧客户端提供后向兼容性。

Licenses.nuget.org 满足这一要求。 Nuget.org 使用它为使用许可证表达式指定其许可证的包提供许可证文本引用。 `nuget pack` 或与其他[客户端工具](../install-nuget-client-tools.md)打包，将 [`licenseUrl`](../reference/nuspec.md#licenseurl) 元素设置为指向 licenses.nuget.org，以提供与不支持 `license` 元素的旧客户端的后向兼容性。

## <a name="protocol"></a>协议

Licenses.nuget.org 旨在供浏览器中的人查看，不提供机器可读响应。
必须使用 HTTPS 协议，并且期望以某种方式构造请求。 它仅支持 `GET` 请求。
它接受许可证表达式或许可异常标识符作为输入，方法如下所述。 请注意，许可表达式的所有元素都区分大小写，因此对 licenses.nuget.org 的所有输入也区分大小写。

### <a name="license-expressions"></a>许可证表达式

#### <a name="request"></a>请求

许可表达式（包括普通情况下，由单个许可证组成的表达式）必须是 [URL 编码](https://tools.ietf.org/html/rfc3986#section-2.1)的，并在 licenses.nuget.org 的请求中用作路径。

| 许可证表达式 | 要使用的 URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| （LGPL 2.0 仅限使用 FLTK-exception 或 Apache-2.0+） | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

该服务仅支持 nuget.org 接受的许可证标识符和许可证异常标识符。包含不受支持的许可证标识符或许可证异常标识符或不符合许可证表达式语法的所有许可证表达式都视为无效。

#### <a name="response"></a>响应

Licenses.nuget.org 响应包含有效许可证表达式的请求，其中包含 HTTP 200 状态代码和包含许可证表达式描述的网页：

* 如果提供的许可证表达式包含单个许可证标识符，则返回包含该许可证引用文本的网页；
* 如果提供的许可证表达式是复合许可证表达式，则返回包含许可证表达式的网页，其中包含指向各个许可证或许可证异常引用的链接。

任何包含无效许可证表达式的请求都会产生 HTTP 404 响应。

### <a name="license-exceptions"></a>许可证异常

#### <a name="request"></a>请求

许可证异常标识符必须经过 URL 编码，并在对 licenses.nuget.org 的请求中用作路径。在单个请求中只能提供单个许可证异常标识符。 URL 的路径部分中除了许可证异常标识符外，不能出现任何其他字符。

| 许可证异常标识符 | 要使用的 URL |
|:---|:---|
|FLTK 异常            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl 异常 | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>响应

Licenses.nuget.org 响应具有已知许可证异常标识符且具有 HTTP 200 响应的请求以及包含指定许可证异常的引用文本的网页。

任何包含不受支持的许可证异常标识符的请求都会产生 HTTP 404 响应。