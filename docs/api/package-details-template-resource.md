---
title: 包详细信息 URL 模板, NuGet API
description: "\"包详细信息 URL\" 模板允许客户端在其 UI 中显示指向更多包详细信息的 web 链接"
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488167"
---
# <a name="package-details-url-template"></a><span data-ttu-id="89b1c-103">包详细信息 URL 模板</span><span class="sxs-lookup"><span data-stu-id="89b1c-103">Package details URL template</span></span>

<span data-ttu-id="89b1c-104">客户端可能会生成一个 URL, 用户可以使用该 URL 在其 web 浏览器中查看更多包详细信息。</span><span class="sxs-lookup"><span data-stu-id="89b1c-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="89b1c-105">当包源要显示与 NuGet 客户端应用程序所显示的范围不匹配的包的其他信息时, 这非常有用。</span><span class="sxs-lookup"><span data-stu-id="89b1c-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="89b1c-106">用于生成此 URL 的资源是在`PackageDetailsUriTemplate` [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="89b1c-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="89b1c-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="89b1c-107">Versioning</span></span>

<span data-ttu-id="89b1c-108">使用以下`@type`值:</span><span class="sxs-lookup"><span data-stu-id="89b1c-108">The following `@type` values are used:</span></span>

<span data-ttu-id="89b1c-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="89b1c-109">@type value</span></span>                     | <span data-ttu-id="89b1c-110">说明</span><span class="sxs-lookup"><span data-stu-id="89b1c-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="89b1c-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="89b1c-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="89b1c-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="89b1c-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="89b1c-113">URL 模板</span><span class="sxs-lookup"><span data-stu-id="89b1c-113">URL template</span></span>

<span data-ttu-id="89b1c-114">以下 API 的 URL 是与上述某个资源`@id` `@type`值关联的属性的值。</span><span class="sxs-lookup"><span data-stu-id="89b1c-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="89b1c-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="89b1c-115">HTTP methods</span></span>

<span data-ttu-id="89b1c-116">尽管客户端不打算代表用户向包详细信息 URL 发出请求, 但网页应支持`GET`方法, 以便在 web 浏览器中轻松地打开已单击的 url。</span><span class="sxs-lookup"><span data-stu-id="89b1c-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="89b1c-117">构造 URL</span><span class="sxs-lookup"><span data-stu-id="89b1c-117">Construct the URL</span></span>

<span data-ttu-id="89b1c-118">给定已知的包 ID 和版本, 客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="89b1c-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="89b1c-119">客户端实现应向用户显示此构造的 URL (或可单击的链接), 以允许用户通过 web 浏览器打开 URL 并了解有关包的详细信息。</span><span class="sxs-lookup"><span data-stu-id="89b1c-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="89b1c-120">包详细信息页的内容由服务器实现确定。</span><span class="sxs-lookup"><span data-stu-id="89b1c-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="89b1c-121">URL 必须是绝对 URL, 方案 (协议) 必须为 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="89b1c-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="89b1c-122">服务索引中的`@id`值是包含以下任何占位符标记的 URL 字符串:</span><span class="sxs-lookup"><span data-stu-id="89b1c-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="89b1c-123">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="89b1c-123">URL placeholders</span></span>

<span data-ttu-id="89b1c-124">name</span><span class="sxs-lookup"><span data-stu-id="89b1c-124">Name</span></span>        | <span data-ttu-id="89b1c-125">类型</span><span class="sxs-lookup"><span data-stu-id="89b1c-125">Type</span></span>    | <span data-ttu-id="89b1c-126">必填</span><span class="sxs-lookup"><span data-stu-id="89b1c-126">Required</span></span> | <span data-ttu-id="89b1c-127">说明</span><span class="sxs-lookup"><span data-stu-id="89b1c-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="89b1c-128">string</span><span class="sxs-lookup"><span data-stu-id="89b1c-128">string</span></span>  | <span data-ttu-id="89b1c-129">否</span><span class="sxs-lookup"><span data-stu-id="89b1c-129">no</span></span>       | <span data-ttu-id="89b1c-130">要获取其详细信息的包 ID</span><span class="sxs-lookup"><span data-stu-id="89b1c-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="89b1c-131">string</span><span class="sxs-lookup"><span data-stu-id="89b1c-131">string</span></span>  | <span data-ttu-id="89b1c-132">否</span><span class="sxs-lookup"><span data-stu-id="89b1c-132">no</span></span>       | <span data-ttu-id="89b1c-133">要获取其详细信息的包版本</span><span class="sxs-lookup"><span data-stu-id="89b1c-133">The package version to get details for</span></span>

<span data-ttu-id="89b1c-134">服务器应接受`{id}`任何大小`{version}`写形式的和值。</span><span class="sxs-lookup"><span data-stu-id="89b1c-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="89b1c-135">此外, 服务器不应对版本是否[规范化](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers)敏感。</span><span class="sxs-lookup"><span data-stu-id="89b1c-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="89b1c-136">换句话说, 服务器还应接受非标准化版本。</span><span class="sxs-lookup"><span data-stu-id="89b1c-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="89b1c-137">例如, nuget 的包详细信息模板如下所示:</span><span class="sxs-lookup"><span data-stu-id="89b1c-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="89b1c-138">如果客户端实现需要显示4.3.0 的包详细信息的链接, 它将生成以下 URL, 并将其提供给用户:</span><span class="sxs-lookup"><span data-stu-id="89b1c-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
