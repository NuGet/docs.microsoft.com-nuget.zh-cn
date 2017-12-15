---
title: "报告滥用行为 URL 模板，NuGet API |Microsoft 文档"
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
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "报告滥用行为 URL 模板允许客户端在其用户界面中显示的报告滥用行为链接。"
keywords: "NuGet API 报告滥用行为、 NuGet API 文件合规、 NuGet.org 报表 URL 模板"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="0dcd5-104">报告滥用行为 URL 模板</span><span class="sxs-lookup"><span data-stu-id="0dcd5-104">Report Abuse URL Template</span></span>

<span data-ttu-id="0dcd5-105">它是客户端来生成可由用户有关特定包报告滥用行为的 URL。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="0dcd5-106">当包源想要启用所有客户端的体验，（甚至是第三方） 以委托到包源的滥用行为报表，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="0dcd5-107">用于提取包内容的资源是`ReportAbuseUriTemplate`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0dcd5-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="0dcd5-108">Versioning</span></span>

<span data-ttu-id="0dcd5-109">以下`@type`将使用值：</span><span class="sxs-lookup"><span data-stu-id="0dcd5-109">The following `@type` values are used:</span></span>

<span data-ttu-id="0dcd5-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="0dcd5-110">@type value</span></span>                       | <span data-ttu-id="0dcd5-111">说明</span><span class="sxs-lookup"><span data-stu-id="0dcd5-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="0dcd5-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="0dcd5-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="0dcd5-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="0dcd5-113">The initial release</span></span>
<span data-ttu-id="0dcd5-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="0dcd5-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="0dcd5-115">别名`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="0dcd5-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="0dcd5-116">URL 模板</span><span class="sxs-lookup"><span data-stu-id="0dcd5-116">URL template</span></span>

<span data-ttu-id="0dcd5-117">以下 API 的 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0dcd5-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0dcd5-118">HTTP methods</span></span>

<span data-ttu-id="0dcd5-119">尽管客户端不打算代表用户对报表滥用行为 URL 发出请求，但应支持网页`GET`方法，以便允许一个被单击的 URL，以轻松地在 web 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="0dcd5-120">构造 URL</span><span class="sxs-lookup"><span data-stu-id="0dcd5-120">Construct the URL</span></span>

<span data-ttu-id="0dcd5-121">给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="0dcd5-122">客户端实现应给此用户，从而允许它们以打开 web 浏览器的 url 并进行任何必要的滥用行为报表显示此构造的 URL （或可单击的链接）。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="0dcd5-123">由服务器实现确定滥用行为报表窗体的实现。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="0dcd5-124">值`@id`是一个包含任何以下占位符令牌的 URL 字符串：</span><span class="sxs-lookup"><span data-stu-id="0dcd5-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="0dcd5-125">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="0dcd5-125">URL placeholders</span></span>

<span data-ttu-id="0dcd5-126">名称</span><span class="sxs-lookup"><span data-stu-id="0dcd5-126">Name</span></span>        | <span data-ttu-id="0dcd5-127">类型</span><span class="sxs-lookup"><span data-stu-id="0dcd5-127">Type</span></span>    | <span data-ttu-id="0dcd5-128">必需</span><span class="sxs-lookup"><span data-stu-id="0dcd5-128">Required</span></span> | <span data-ttu-id="0dcd5-129">说明</span><span class="sxs-lookup"><span data-stu-id="0dcd5-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="0dcd5-130">string</span><span class="sxs-lookup"><span data-stu-id="0dcd5-130">string</span></span>  | <span data-ttu-id="0dcd5-131">no</span><span class="sxs-lookup"><span data-stu-id="0dcd5-131">no</span></span>       | <span data-ttu-id="0dcd5-132">将包 ID 与报表有关的滥用行为</span><span class="sxs-lookup"><span data-stu-id="0dcd5-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="0dcd5-133">string</span><span class="sxs-lookup"><span data-stu-id="0dcd5-133">string</span></span>  | <span data-ttu-id="0dcd5-134">no</span><span class="sxs-lookup"><span data-stu-id="0dcd5-134">no</span></span>       | <span data-ttu-id="0dcd5-135">包版本到有关报告滥用行为</span><span class="sxs-lookup"><span data-stu-id="0dcd5-135">The package version to report abuse for</span></span>

<span data-ttu-id="0dcd5-136">`{id}`和`{version}`由服务器实施解释的值必须是区分大小 insenstive 和对版本进行了规范化是否不敏感。</span><span class="sxs-lookup"><span data-stu-id="0dcd5-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="0dcd5-137">例如，nuget.org 的报告滥用行为模板类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="0dcd5-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="0dcd5-138">如果客户端实现需要为 NuGet.Versioning 4.3.0 到报告滥用行为窗体中显示一个链接，它将产生以下 URL 并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="0dcd5-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```