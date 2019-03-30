---
title: 包详细信息 URL 模板，NuGet API
description: 包详细信息 URL 模板允许客户端 web 链接到更多包详细信息及其用户界面中显示
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638068"
---
# <a name="package-details-url-template"></a><span data-ttu-id="2b636-103">包详细信息 URL 模板</span><span class="sxs-lookup"><span data-stu-id="2b636-103">Package details URL template</span></span>

<span data-ttu-id="2b636-104">就可以生成用户可以用来查看其 web 浏览器中的更多包详细信息的 URL 的客户端。</span><span class="sxs-lookup"><span data-stu-id="2b636-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="2b636-105">当包源想要显示的 NuGet 客户端应用程序的显示范围内可能容纳不下的包有关的其他信息时，这很有用。</span><span class="sxs-lookup"><span data-stu-id="2b636-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="2b636-106">用于生成此 URL 使用的资源是`PackageDetailsUriTemplate`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2b636-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2b636-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="2b636-107">Versioning</span></span>

<span data-ttu-id="2b636-108">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="2b636-108">The following `@type` values are used:</span></span>

<span data-ttu-id="2b636-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="2b636-109">@type value</span></span>                     | <span data-ttu-id="2b636-110">说明</span><span class="sxs-lookup"><span data-stu-id="2b636-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="2b636-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="2b636-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="2b636-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="2b636-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="2b636-113">URL 模板</span><span class="sxs-lookup"><span data-stu-id="2b636-113">URL template</span></span>

<span data-ttu-id="2b636-114">以下 API 的 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="2b636-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2b636-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2b636-115">HTTP methods</span></span>

<span data-ttu-id="2b636-116">尽管客户端不应代表用户向包的详细信息 URL 发出请求，但应支持 web 页`GET`方法，以允许单击的 URL 来轻松地在 web 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="2b636-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="2b636-117">构造的 URL</span><span class="sxs-lookup"><span data-stu-id="2b636-117">Construct the URL</span></span>

<span data-ttu-id="2b636-118">提供了已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="2b636-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="2b636-119">客户端实现应显示此构造的 URL （或可单击的链接） 向允许其用户若要打开 web 浏览器的 url，若要了解有关包的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2b636-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="2b636-120">包详细信息页的内容取决于服务器实现。</span><span class="sxs-lookup"><span data-stu-id="2b636-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="2b636-121">该 URL 必须是绝对 URL，该方案 （协议） 必须是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="2b636-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="2b636-122">值`@id`索引服务中是一个包含任何以下占位符令牌的 URL 字符串：</span><span class="sxs-lookup"><span data-stu-id="2b636-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="2b636-123">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="2b636-123">URL placeholders</span></span>

<span data-ttu-id="2b636-124">名称</span><span class="sxs-lookup"><span data-stu-id="2b636-124">Name</span></span>        | <span data-ttu-id="2b636-125">类型</span><span class="sxs-lookup"><span data-stu-id="2b636-125">Type</span></span>    | <span data-ttu-id="2b636-126">必需</span><span class="sxs-lookup"><span data-stu-id="2b636-126">Required</span></span> | <span data-ttu-id="2b636-127">说明</span><span class="sxs-lookup"><span data-stu-id="2b636-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="2b636-128">string</span><span class="sxs-lookup"><span data-stu-id="2b636-128">string</span></span>  | <span data-ttu-id="2b636-129">否</span><span class="sxs-lookup"><span data-stu-id="2b636-129">no</span></span>       | <span data-ttu-id="2b636-130">要获取的详细信息的包 ID</span><span class="sxs-lookup"><span data-stu-id="2b636-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="2b636-131">string</span><span class="sxs-lookup"><span data-stu-id="2b636-131">string</span></span>  | <span data-ttu-id="2b636-132">否</span><span class="sxs-lookup"><span data-stu-id="2b636-132">no</span></span>       | <span data-ttu-id="2b636-133">要获取的详细信息的包版本</span><span class="sxs-lookup"><span data-stu-id="2b636-133">The package version to get details for</span></span>

<span data-ttu-id="2b636-134">服务器应接受`{id}`和`{version}`任何大小写的值。</span><span class="sxs-lookup"><span data-stu-id="2b636-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="2b636-135">此外，服务器不应为版本是否为敏感[规范化](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2b636-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="2b636-136">换而言之，应接受服务器还接受非规范化的版本。</span><span class="sxs-lookup"><span data-stu-id="2b636-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="2b636-137">例如，nuget.org 的包的详细信息模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b636-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="2b636-138">如果客户端实现需要为 NuGet.Versioning 4.3.0 显示包详细信息的链接，它将产生以下 URL 并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="2b636-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
