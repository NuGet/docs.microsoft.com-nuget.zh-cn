---
title: 报告滥用 URL 模板，NuGet API
description: 报告滥用 URL 模板允许客户端在其 UI 中显示的报告滥用行为链接。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549334"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="a4b1f-103">报告滥用 URL 模板</span><span class="sxs-lookup"><span data-stu-id="a4b1f-103">Report abuse URL template</span></span>

<span data-ttu-id="a4b1f-104">就可以生成可由用户报告滥用行为有关特定包的 URL 的客户端。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="a4b1f-105">当包源想要启用所有客户端体验 （甚至是第三方） 委派对包源的滥用报告时，这很有用。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="a4b1f-106">用于生成此 URL 使用的资源是`ReportAbuseUriTemplate`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a4b1f-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="a4b1f-107">Versioning</span></span>

<span data-ttu-id="a4b1f-108">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="a4b1f-108">The following `@type` values are used:</span></span>

<span data-ttu-id="a4b1f-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="a4b1f-109">@type value</span></span>                       | <span data-ttu-id="a4b1f-110">说明</span><span class="sxs-lookup"><span data-stu-id="a4b1f-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="a4b1f-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="a4b1f-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="a4b1f-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="a4b1f-112">The initial release</span></span>
<span data-ttu-id="a4b1f-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="a4b1f-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="a4b1f-114">别名 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="a4b1f-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="a4b1f-115">URL 模板</span><span class="sxs-lookup"><span data-stu-id="a4b1f-115">URL template</span></span>

<span data-ttu-id="a4b1f-116">以下 API 的 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a4b1f-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="a4b1f-117">HTTP methods</span></span>

<span data-ttu-id="a4b1f-118">尽管客户端不应代表用户向报告滥用 URL 发出请求，但应支持 web 页`GET`方法，以允许单击的 URL 来轻松地在 web 浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="a4b1f-119">构造的 URL</span><span class="sxs-lookup"><span data-stu-id="a4b1f-119">Construct the URL</span></span>

<span data-ttu-id="a4b1f-120">提供了已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="a4b1f-121">客户端实现应显示给用户允许应用来打开 web 浏览器到 URL 并进行任何必要的滥用报告此构造的 URL （或可单击的链接）。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="a4b1f-122">滥用报告表单的实现取决于服务器实现。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="a4b1f-123">值`@id`是 URL 的字符串包含任何以下占位符标记：</span><span class="sxs-lookup"><span data-stu-id="a4b1f-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="a4b1f-124">URL 占位符</span><span class="sxs-lookup"><span data-stu-id="a4b1f-124">URL placeholders</span></span>

<span data-ttu-id="a4b1f-125">name</span><span class="sxs-lookup"><span data-stu-id="a4b1f-125">Name</span></span>        | <span data-ttu-id="a4b1f-126">类型</span><span class="sxs-lookup"><span data-stu-id="a4b1f-126">Type</span></span>    | <span data-ttu-id="a4b1f-127">必需</span><span class="sxs-lookup"><span data-stu-id="a4b1f-127">Required</span></span> | <span data-ttu-id="a4b1f-128">说明</span><span class="sxs-lookup"><span data-stu-id="a4b1f-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="a4b1f-129">字符串</span><span class="sxs-lookup"><span data-stu-id="a4b1f-129">string</span></span>  | <span data-ttu-id="a4b1f-130">否</span><span class="sxs-lookup"><span data-stu-id="a4b1f-130">no</span></span>       | <span data-ttu-id="a4b1f-131">将包 ID 与举报违规帖子</span><span class="sxs-lookup"><span data-stu-id="a4b1f-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="a4b1f-132">字符串</span><span class="sxs-lookup"><span data-stu-id="a4b1f-132">string</span></span>  | <span data-ttu-id="a4b1f-133">否</span><span class="sxs-lookup"><span data-stu-id="a4b1f-133">no</span></span>       | <span data-ttu-id="a4b1f-134">将包版本到举报违规帖子</span><span class="sxs-lookup"><span data-stu-id="a4b1f-134">The package version to report abuse for</span></span>

<span data-ttu-id="a4b1f-135">`{id}`和`{version}`解释服务器实现的值必须是不区分大小写和不敏感到是否规范化版本。</span><span class="sxs-lookup"><span data-stu-id="a4b1f-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="a4b1f-136">例如，nuget.org 的报告滥用行为模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4b1f-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="a4b1f-137">如果需要有关 NuGet.Versioning 4.3.0 报告滥用行为窗体显示的链接的客户端实现，它将产生以下 URL 并将其提供给用户：</span><span class="sxs-lookup"><span data-stu-id="a4b1f-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
