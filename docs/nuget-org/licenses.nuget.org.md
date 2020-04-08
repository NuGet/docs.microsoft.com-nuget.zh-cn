---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427112"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="2213a-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="2213a-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="2213a-103">阐释</span><span class="sxs-lookup"><span data-stu-id="2213a-103">Rationale</span></span>

<span data-ttu-id="2213a-104">随着[许可证表达式](../reference/nuspec.md#license)的引入，出现了一种需求，即需要提供可靠的服务，为单个许可证标识符、异常标识符或许可证表达式提供参考文本。</span><span class="sxs-lookup"><span data-stu-id="2213a-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="2213a-105">此服务的另一个要求是具有稳定的 URL 架构，该架构不易受链接失效的影响，因此我们可以安全地使用它来为旧客户端提供后向兼容性。</span><span class="sxs-lookup"><span data-stu-id="2213a-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="2213a-106">Licenses.nuget.org 满足这一要求。</span><span class="sxs-lookup"><span data-stu-id="2213a-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="2213a-107">Nuget.org 使用它为使用许可证表达式指定其许可证的包提供许可证文本引用。</span><span class="sxs-lookup"><span data-stu-id="2213a-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="2213a-108">`nuget pack` 或与其他[客户端工具](../install-nuget-client-tools.md)打包，将 [`licenseUrl`](../reference/nuspec.md#licenseurl) 元素设置为指向 licenses.nuget.org，以提供与不支持 `license` 元素的旧客户端的后向兼容性。</span><span class="sxs-lookup"><span data-stu-id="2213a-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="2213a-109">协议</span><span class="sxs-lookup"><span data-stu-id="2213a-109">Protocol</span></span>

<span data-ttu-id="2213a-110">Licenses.nuget.org 旨在供浏览器中的人查看，不提供机器可读响应。</span><span class="sxs-lookup"><span data-stu-id="2213a-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="2213a-111">必须使用 HTTPS 协议，并且期望以某种方式构造请求。</span><span class="sxs-lookup"><span data-stu-id="2213a-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="2213a-112">它仅支持 `GET` 请求。</span><span class="sxs-lookup"><span data-stu-id="2213a-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="2213a-113">它接受许可证表达式或许可异常标识符作为输入，方法如下所述。</span><span class="sxs-lookup"><span data-stu-id="2213a-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="2213a-114">请注意，许可表达式的所有元素都区分大小写，因此对 licenses.nuget.org 的所有输入也区分大小写。</span><span class="sxs-lookup"><span data-stu-id="2213a-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="2213a-115">许可证表达式</span><span class="sxs-lookup"><span data-stu-id="2213a-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="2213a-116">请求</span><span class="sxs-lookup"><span data-stu-id="2213a-116">Request</span></span>

<span data-ttu-id="2213a-117">许可表达式（包括普通情况下，由单个许可证组成的表达式）必须是 [URL 编码](https://tools.ietf.org/html/rfc3986#section-2.1)的，并在 licenses.nuget.org 的请求中用作路径。</span><span class="sxs-lookup"><span data-stu-id="2213a-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="2213a-118">许可证表达式</span><span class="sxs-lookup"><span data-stu-id="2213a-118">License expression</span></span> | <span data-ttu-id="2213a-119">要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="2213a-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="2213a-120">MIT</span><span class="sxs-lookup"><span data-stu-id="2213a-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="2213a-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="2213a-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="2213a-122">（LGPL 2.0 仅限使用 FLTK-exception 或 Apache-2.0+）</span><span class="sxs-lookup"><span data-stu-id="2213a-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="2213a-123">该服务仅支持 nuget.org 接受的许可证标识符和许可证异常标识符。包含不受支持的许可证标识符或许可证异常标识符或不符合许可证表达式语法的所有许可证表达式都视为无效。</span><span class="sxs-lookup"><span data-stu-id="2213a-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="2213a-124">响应</span><span class="sxs-lookup"><span data-stu-id="2213a-124">Response</span></span>

<span data-ttu-id="2213a-125">Licenses.nuget.org 响应包含有效许可证表达式的请求，其中包含 HTTP 200 状态代码和包含许可证表达式描述的网页：</span><span class="sxs-lookup"><span data-stu-id="2213a-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="2213a-126">如果提供的许可证表达式包含单个许可证标识符，则返回包含该许可证引用文本的网页；</span><span class="sxs-lookup"><span data-stu-id="2213a-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="2213a-127">如果提供的许可证表达式是复合许可证表达式，则返回包含许可证表达式的网页，其中包含指向各个许可证或许可证异常引用的链接。</span><span class="sxs-lookup"><span data-stu-id="2213a-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="2213a-128">任何包含无效许可证表达式的请求都会产生 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="2213a-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="2213a-129">许可证异常</span><span class="sxs-lookup"><span data-stu-id="2213a-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="2213a-130">请求</span><span class="sxs-lookup"><span data-stu-id="2213a-130">Request</span></span>

<span data-ttu-id="2213a-131">许可证异常标识符必须经过 URL 编码，并在对 licenses.nuget.org 的请求中用作路径。在单个请求中只能提供单个许可证异常标识符。</span><span class="sxs-lookup"><span data-stu-id="2213a-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="2213a-132">URL 的路径部分中除了许可证异常标识符外，不能出现任何其他字符。</span><span class="sxs-lookup"><span data-stu-id="2213a-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="2213a-133">许可证异常标识符</span><span class="sxs-lookup"><span data-stu-id="2213a-133">License exception identifier</span></span> | <span data-ttu-id="2213a-134">要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="2213a-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="2213a-135">FLTK 异常</span><span class="sxs-lookup"><span data-stu-id="2213a-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="2213a-136">openvpn-openssl 异常</span><span class="sxs-lookup"><span data-stu-id="2213a-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="2213a-137">响应</span><span class="sxs-lookup"><span data-stu-id="2213a-137">Response</span></span>

<span data-ttu-id="2213a-138">Licenses.nuget.org 响应具有已知许可证异常标识符且具有 HTTP 200 响应的请求以及包含指定许可证异常的引用文本的网页。</span><span class="sxs-lookup"><span data-stu-id="2213a-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="2213a-139">任何包含不受支持的许可证异常标识符的请求都会产生 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="2213a-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>