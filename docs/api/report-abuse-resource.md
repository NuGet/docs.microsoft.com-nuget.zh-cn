---
title: 报表滥用 URL 模板，NuGet API
description: "\"报表滥用 URL\" 模板允许客户端在其用户界面中显示 \"报告滥用\" 链接。"
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775225"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="0ea3c-103">报告滥用 URL 模板</span><span class="sxs-lookup"><span data-stu-id="0ea3c-103">Report abuse URL template</span></span>

<span data-ttu-id="0ea3c-104">客户端可能会生成一个 URL，用户可以使用该 URL 报告有关特定包的滥用。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="0ea3c-105">当包源要启用所有客户端体验 (甚至第三方) 将滥用报表委托给包源时，此方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="0ea3c-106">用于生成此 URL 的资源是 `ReportAbuseUriTemplate` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0ea3c-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="0ea3c-107">Versioning</span></span>

<span data-ttu-id="0ea3c-108">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="0ea3c-108">The following `@type` values are used:</span></span>

<span data-ttu-id="0ea3c-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="0ea3c-109">@type value</span></span>                       | <span data-ttu-id="0ea3c-110">说明</span><span class="sxs-lookup"><span data-stu-id="0ea3c-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="0ea3c-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="0ea3c-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="0ea3c-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="0ea3c-112">The initial release</span></span>
<span data-ttu-id="0ea3c-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="0ea3c-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="0ea3c-114">别名 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="0ea3c-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="0ea3c-115">URL 模板</span><span class="sxs-lookup"><span data-stu-id="0ea3c-115">URL template</span></span>

<span data-ttu-id="0ea3c-116">以下 API 的 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0ea3c-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0ea3c-117">HTTP methods</span></span>

<span data-ttu-id="0ea3c-118">尽管客户端不打算代表用户向报表滥用 URL 发出请求，但网页应支持方法，以便 `GET` 在 web 浏览器中轻松地打开已单击的 url。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="0ea3c-119">构造 URL</span><span class="sxs-lookup"><span data-stu-id="0ea3c-119">Construct the URL</span></span>

<span data-ttu-id="0ea3c-120">给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="0ea3c-121">客户端实现应显示此构造的 URL (或可单击的链接，) 用户允许用户在 URL 中打开 web 浏览器，并进行任何必要的滥用报告。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="0ea3c-122">滥用报表窗体的实现由服务器实现确定。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="0ea3c-123">的值 `@id` 是包含以下任何占位符标记的 URL 字符串：</span><span class="sxs-lookup"><span data-stu-id="0ea3c-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="0ea3c-124">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="0ea3c-124">URL placeholders</span></span>

<span data-ttu-id="0ea3c-125">名称</span><span class="sxs-lookup"><span data-stu-id="0ea3c-125">Name</span></span>        | <span data-ttu-id="0ea3c-126">类型</span><span class="sxs-lookup"><span data-stu-id="0ea3c-126">Type</span></span>    | <span data-ttu-id="0ea3c-127">必须</span><span class="sxs-lookup"><span data-stu-id="0ea3c-127">Required</span></span> | <span data-ttu-id="0ea3c-128">注释</span><span class="sxs-lookup"><span data-stu-id="0ea3c-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="0ea3c-129">string</span><span class="sxs-lookup"><span data-stu-id="0ea3c-129">string</span></span>  | <span data-ttu-id="0ea3c-130">否</span><span class="sxs-lookup"><span data-stu-id="0ea3c-130">no</span></span>       | <span data-ttu-id="0ea3c-131">要为其报告滥用行为的包 ID</span><span class="sxs-lookup"><span data-stu-id="0ea3c-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="0ea3c-132">string</span><span class="sxs-lookup"><span data-stu-id="0ea3c-132">string</span></span>  | <span data-ttu-id="0ea3c-133">否</span><span class="sxs-lookup"><span data-stu-id="0ea3c-133">no</span></span>       | <span data-ttu-id="0ea3c-134">要为其报告滥用行为的包版本</span><span class="sxs-lookup"><span data-stu-id="0ea3c-134">The package version to report abuse for</span></span>

<span data-ttu-id="0ea3c-135">`{id}` `{version}` 服务器实现解释的和值必须区分大小写，而不区分版本是否规范化。</span><span class="sxs-lookup"><span data-stu-id="0ea3c-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="0ea3c-136">例如，nuget.exe 的报表滥用模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="0ea3c-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="0ea3c-137">如果客户端实现需要显示4.3.0 的报表滥用窗体的链接，它将生成以下 URL，并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="0ea3c-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
