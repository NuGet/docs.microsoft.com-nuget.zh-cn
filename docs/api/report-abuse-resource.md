---
title: 报告滥用行为 URL 模板，NuGet API
description: 报告滥用行为 URL 模板允许客户端在其用户界面中显示的报告滥用行为链接。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818462"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="b4ecd-103">报告滥用行为 URL 模板</span><span class="sxs-lookup"><span data-stu-id="b4ecd-103">Report abuse URL template</span></span>

<span data-ttu-id="b4ecd-104">它是客户端来生成可由用户有关特定包报告滥用行为的 URL。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="b4ecd-105">当包源想要启用所有客户端的体验，（甚至是第三方） 以委托到包源的滥用行为报表，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="b4ecd-106">用于提取包内容的资源是`ReportAbuseUriTemplate`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b4ecd-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="b4ecd-107">Versioning</span></span>

<span data-ttu-id="b4ecd-108">以下`@type`将使用值：</span><span class="sxs-lookup"><span data-stu-id="b4ecd-108">The following `@type` values are used:</span></span>

<span data-ttu-id="b4ecd-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="b4ecd-109">@type value</span></span>                       | <span data-ttu-id="b4ecd-110">说明</span><span class="sxs-lookup"><span data-stu-id="b4ecd-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="b4ecd-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="b4ecd-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="b4ecd-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="b4ecd-112">The initial release</span></span>
<span data-ttu-id="b4ecd-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="b4ecd-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="b4ecd-114">别名 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="b4ecd-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="b4ecd-115">URL 模板</span><span class="sxs-lookup"><span data-stu-id="b4ecd-115">URL template</span></span>

<span data-ttu-id="b4ecd-116">以下 API 的 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b4ecd-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="b4ecd-117">HTTP methods</span></span>

<span data-ttu-id="b4ecd-118">尽管客户端不打算代表用户对报表滥用行为 URL 发出请求，但应支持网页`GET`方法，以便允许一个被单击的 URL，以轻松地在 web 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="b4ecd-119">构造 URL</span><span class="sxs-lookup"><span data-stu-id="b4ecd-119">Construct the URL</span></span>

<span data-ttu-id="b4ecd-120">给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="b4ecd-121">客户端实现应给此用户，从而允许它们以打开 web 浏览器的 url 并进行任何必要的滥用行为报表显示此构造的 URL （或可单击的链接）。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="b4ecd-122">由服务器实现确定滥用行为报表窗体的实现。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="b4ecd-123">值`@id`是一个包含任何以下占位符令牌的 URL 字符串：</span><span class="sxs-lookup"><span data-stu-id="b4ecd-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="b4ecd-124">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="b4ecd-124">URL placeholders</span></span>

<span data-ttu-id="b4ecd-125">名称</span><span class="sxs-lookup"><span data-stu-id="b4ecd-125">Name</span></span>        | <span data-ttu-id="b4ecd-126">类型</span><span class="sxs-lookup"><span data-stu-id="b4ecd-126">Type</span></span>    | <span data-ttu-id="b4ecd-127">必需</span><span class="sxs-lookup"><span data-stu-id="b4ecd-127">Required</span></span> | <span data-ttu-id="b4ecd-128">说明</span><span class="sxs-lookup"><span data-stu-id="b4ecd-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="b4ecd-129">字符串</span><span class="sxs-lookup"><span data-stu-id="b4ecd-129">string</span></span>  | <span data-ttu-id="b4ecd-130">否</span><span class="sxs-lookup"><span data-stu-id="b4ecd-130">no</span></span>       | <span data-ttu-id="b4ecd-131">将包 ID 与报表有关的滥用行为</span><span class="sxs-lookup"><span data-stu-id="b4ecd-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="b4ecd-132">字符串</span><span class="sxs-lookup"><span data-stu-id="b4ecd-132">string</span></span>  | <span data-ttu-id="b4ecd-133">否</span><span class="sxs-lookup"><span data-stu-id="b4ecd-133">no</span></span>       | <span data-ttu-id="b4ecd-134">包版本到有关报告滥用行为</span><span class="sxs-lookup"><span data-stu-id="b4ecd-134">The package version to report abuse for</span></span>

<span data-ttu-id="b4ecd-135">`{id}`和`{version}`由服务器实施解释的值必须是区分大小写和对版本进行了规范化是否不敏感。</span><span class="sxs-lookup"><span data-stu-id="b4ecd-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="b4ecd-136">例如，nuget.org 的报告滥用行为模板类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4ecd-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="b4ecd-137">如果客户端实现需要为 NuGet.Versioning 4.3.0 到报告滥用行为窗体中显示一个链接，它将产生以下 URL 并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="b4ecd-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
