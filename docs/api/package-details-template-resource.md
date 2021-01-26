---
title: 包详细信息 URL 模板，NuGet API
description: "\"包详细信息 URL\" 模板允许客户端在其 UI 中显示指向更多包详细信息的 web 链接"
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773951"
---
# <a name="package-details-url-template"></a><span data-ttu-id="e7dca-103">包详细信息 URL 模板</span><span class="sxs-lookup"><span data-stu-id="e7dca-103">Package details URL template</span></span>

<span data-ttu-id="e7dca-104">客户端可能会生成一个 URL，用户可以使用该 URL 在其 web 浏览器中查看更多包详细信息。</span><span class="sxs-lookup"><span data-stu-id="e7dca-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="e7dca-105">当包源要显示与 NuGet 客户端应用程序所显示的范围不匹配的包的其他信息时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="e7dca-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="e7dca-106">用于生成此 URL 的资源是 `PackageDetailsUriTemplate` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="e7dca-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e7dca-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="e7dca-107">Versioning</span></span>

<span data-ttu-id="e7dca-108">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="e7dca-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e7dca-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="e7dca-109">@type value</span></span>                     | <span data-ttu-id="e7dca-110">说明</span><span class="sxs-lookup"><span data-stu-id="e7dca-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="e7dca-111">PackageDetailsUriTemplate/5.1。0</span><span class="sxs-lookup"><span data-stu-id="e7dca-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="e7dca-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="e7dca-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="e7dca-113">URL 模板</span><span class="sxs-lookup"><span data-stu-id="e7dca-113">URL template</span></span>

<span data-ttu-id="e7dca-114">以下 API 的 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="e7dca-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e7dca-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="e7dca-115">HTTP methods</span></span>

<span data-ttu-id="e7dca-116">尽管客户端不打算代表用户向包详细信息 URL 发出请求，但网页应支持方法，以便 `GET` 在 web 浏览器中轻松地打开已单击的 url。</span><span class="sxs-lookup"><span data-stu-id="e7dca-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e7dca-117">构造 URL</span><span class="sxs-lookup"><span data-stu-id="e7dca-117">Construct the URL</span></span>

<span data-ttu-id="e7dca-118">给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="e7dca-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e7dca-119">客户端实现应显示此构造的 URL (或可单击的链接) 用户允许用户在 URL 中打开 web 浏览器并了解有关包的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e7dca-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="e7dca-120">包详细信息页的内容由服务器实现确定。</span><span class="sxs-lookup"><span data-stu-id="e7dca-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="e7dca-121">URL 必须是绝对 URL，并且 (协议) 的方案必须为 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="e7dca-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="e7dca-122">`@id`服务索引中的值是包含以下任何占位符标记的 URL 字符串：</span><span class="sxs-lookup"><span data-stu-id="e7dca-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e7dca-123">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="e7dca-123">URL placeholders</span></span>

<span data-ttu-id="e7dca-124">名称</span><span class="sxs-lookup"><span data-stu-id="e7dca-124">Name</span></span>        | <span data-ttu-id="e7dca-125">类型</span><span class="sxs-lookup"><span data-stu-id="e7dca-125">Type</span></span>    | <span data-ttu-id="e7dca-126">必须</span><span class="sxs-lookup"><span data-stu-id="e7dca-126">Required</span></span> | <span data-ttu-id="e7dca-127">注释</span><span class="sxs-lookup"><span data-stu-id="e7dca-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e7dca-128">string</span><span class="sxs-lookup"><span data-stu-id="e7dca-128">string</span></span>  | <span data-ttu-id="e7dca-129">否</span><span class="sxs-lookup"><span data-stu-id="e7dca-129">no</span></span>       | <span data-ttu-id="e7dca-130">要获取其详细信息的包 ID</span><span class="sxs-lookup"><span data-stu-id="e7dca-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="e7dca-131">string</span><span class="sxs-lookup"><span data-stu-id="e7dca-131">string</span></span>  | <span data-ttu-id="e7dca-132">否</span><span class="sxs-lookup"><span data-stu-id="e7dca-132">no</span></span>       | <span data-ttu-id="e7dca-133">要获取其详细信息的包版本</span><span class="sxs-lookup"><span data-stu-id="e7dca-133">The package version to get details for</span></span>

<span data-ttu-id="e7dca-134">服务器应接受 `{id}` `{version}` 任何大小写形式的和值。</span><span class="sxs-lookup"><span data-stu-id="e7dca-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="e7dca-135">此外，服务器不应对版本是否 [规范化](../concepts/package-versioning.md#normalized-version-numbers)敏感。</span><span class="sxs-lookup"><span data-stu-id="e7dca-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e7dca-136">换句话说，服务器还应接受非标准化版本。</span><span class="sxs-lookup"><span data-stu-id="e7dca-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="e7dca-137">例如，nuget 的包详细信息模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="e7dca-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="e7dca-138">如果客户端实现需要显示4.3.0 的包详细信息的链接，它将生成以下 URL，并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="e7dca-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
