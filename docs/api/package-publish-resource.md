---
title: 推送和删除的 NuGet API
description: 发布服务允许客户端将新包发布和取消列出或删除现有的包。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547516"
---
# <a name="push-and-delete"></a><span data-ttu-id="df258-103">推送和删除</span><span class="sxs-lookup"><span data-stu-id="df258-103">Push and Delete</span></span>

<span data-ttu-id="df258-104">可以推送、 删除 （或取消列出，具体取决于服务器实现），并重新列出包使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="df258-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="df258-105">这些操作所基于的中断`PackagePublish`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="df258-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="df258-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="df258-106">Versioning</span></span>

<span data-ttu-id="df258-107">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="df258-107">The following `@type` value is used:</span></span>

<span data-ttu-id="df258-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="df258-108">@type value</span></span>          | <span data-ttu-id="df258-109">说明</span><span class="sxs-lookup"><span data-stu-id="df258-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="df258-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="df258-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="df258-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="df258-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="df258-112">基 URL</span><span class="sxs-lookup"><span data-stu-id="df258-112">Base URL</span></span>

<span data-ttu-id="df258-113">以下 Api 的基 URL 是的值`@id`的属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="df258-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="df258-114">以下文档中，使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="df258-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="df258-115">请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="df258-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="df258-116">请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。</span><span class="sxs-lookup"><span data-stu-id="df258-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="df258-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="df258-117">HTTP methods</span></span>

<span data-ttu-id="df258-118">`PUT`，`POST`和`DELETE`此资源支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="df258-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="df258-119">有关每个终结点上支持哪些方法，请参阅下面。</span><span class="sxs-lookup"><span data-stu-id="df258-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="df258-120">将包推送</span><span class="sxs-lookup"><span data-stu-id="df258-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="df258-121">nuget.org 已[其他要求](NuGet-Protocols.md)与推送终结点进行交互。</span><span class="sxs-lookup"><span data-stu-id="df258-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="df258-122">nuget.org 支持推送新的包使用以下 API。</span><span class="sxs-lookup"><span data-stu-id="df258-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="df258-123">如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。</span><span class="sxs-lookup"><span data-stu-id="df258-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="df258-124">其他包源可能支持替换现有的包。</span><span class="sxs-lookup"><span data-stu-id="df258-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="df258-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="df258-125">Request parameters</span></span>

<span data-ttu-id="df258-126">name</span><span class="sxs-lookup"><span data-stu-id="df258-126">Name</span></span>           | <span data-ttu-id="df258-127">内</span><span class="sxs-lookup"><span data-stu-id="df258-127">In</span></span>     | <span data-ttu-id="df258-128">类型</span><span class="sxs-lookup"><span data-stu-id="df258-128">Type</span></span>   | <span data-ttu-id="df258-129">必需</span><span class="sxs-lookup"><span data-stu-id="df258-129">Required</span></span> | <span data-ttu-id="df258-130">说明</span><span class="sxs-lookup"><span data-stu-id="df258-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="df258-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="df258-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="df258-132">Header</span><span class="sxs-lookup"><span data-stu-id="df258-132">Header</span></span> | <span data-ttu-id="df258-133">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-133">string</span></span> | <span data-ttu-id="df258-134">是</span><span class="sxs-lookup"><span data-stu-id="df258-134">yes</span></span>      | <span data-ttu-id="df258-135">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="df258-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="df258-136">API 密钥是从包源获得由用户和配置到客户端不透明的字符串。</span><span class="sxs-lookup"><span data-stu-id="df258-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="df258-137">强制要求任何特定字符串格式，但 API 密钥的长度不应超过合理的大小，为 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="df258-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="df258-138">请求正文</span><span class="sxs-lookup"><span data-stu-id="df258-138">Request body</span></span>

<span data-ttu-id="df258-139">请求正文必须采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="df258-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="df258-140">多部分窗体数据</span><span class="sxs-lookup"><span data-stu-id="df258-140">Multipart form data</span></span>

<span data-ttu-id="df258-141">请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是推送.nupkg 的原始字节。</span><span class="sxs-lookup"><span data-stu-id="df258-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="df258-142">多部分正文中后面的项将被忽略。</span><span class="sxs-lookup"><span data-stu-id="df258-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="df258-143">将忽略的文件的名称或任何其他标头的多部分项。</span><span class="sxs-lookup"><span data-stu-id="df258-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="df258-144">响应</span><span class="sxs-lookup"><span data-stu-id="df258-144">Response</span></span>

<span data-ttu-id="df258-145">状态代码</span><span class="sxs-lookup"><span data-stu-id="df258-145">Status Code</span></span> | <span data-ttu-id="df258-146">含义</span><span class="sxs-lookup"><span data-stu-id="df258-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="df258-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="df258-147">201, 202</span></span>    | <span data-ttu-id="df258-148">已成功推送包</span><span class="sxs-lookup"><span data-stu-id="df258-148">The package was successfully pushed</span></span>
<span data-ttu-id="df258-149">400</span><span class="sxs-lookup"><span data-stu-id="df258-149">400</span></span>         | <span data-ttu-id="df258-150">提供的包无效</span><span class="sxs-lookup"><span data-stu-id="df258-150">The provided package is invalid</span></span>
<span data-ttu-id="df258-151">409</span><span class="sxs-lookup"><span data-stu-id="df258-151">409</span></span>         | <span data-ttu-id="df258-152">已存在具有提供的 ID 和版本的包</span><span class="sxs-lookup"><span data-stu-id="df258-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="df258-153">服务器实现上成功状态代码返回成功推送包时存在差异。</span><span class="sxs-lookup"><span data-stu-id="df258-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="df258-154">删除包</span><span class="sxs-lookup"><span data-stu-id="df258-154">Delete a package</span></span>

<span data-ttu-id="df258-155">nuget.org 将解释为包删除请求的"取消列出"。</span><span class="sxs-lookup"><span data-stu-id="df258-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="df258-156">这意味着包仍可用于包的现有使用者，但包不会再出现在搜索结果中或 web 界面中。</span><span class="sxs-lookup"><span data-stu-id="df258-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="df258-157">有关这种做法的详细信息，请参阅[删除包](../policies/deleting-packages.md)策略。</span><span class="sxs-lookup"><span data-stu-id="df258-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="df258-158">其他服务器实现可以自由地解释为硬删除此信号，软删除，或取消列出。</span><span class="sxs-lookup"><span data-stu-id="df258-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="df258-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持处理此请求作为未列出或硬删除基于配置选项。</span><span class="sxs-lookup"><span data-stu-id="df258-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="df258-160">请求参数</span><span class="sxs-lookup"><span data-stu-id="df258-160">Request parameters</span></span>

<span data-ttu-id="df258-161">name</span><span class="sxs-lookup"><span data-stu-id="df258-161">Name</span></span>           | <span data-ttu-id="df258-162">内</span><span class="sxs-lookup"><span data-stu-id="df258-162">In</span></span>     | <span data-ttu-id="df258-163">类型</span><span class="sxs-lookup"><span data-stu-id="df258-163">Type</span></span>   | <span data-ttu-id="df258-164">必需</span><span class="sxs-lookup"><span data-stu-id="df258-164">Required</span></span> | <span data-ttu-id="df258-165">说明</span><span class="sxs-lookup"><span data-stu-id="df258-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="df258-166">Id</span><span class="sxs-lookup"><span data-stu-id="df258-166">ID</span></span>             | <span data-ttu-id="df258-167">URL</span><span class="sxs-lookup"><span data-stu-id="df258-167">URL</span></span>    | <span data-ttu-id="df258-168">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-168">string</span></span> | <span data-ttu-id="df258-169">是</span><span class="sxs-lookup"><span data-stu-id="df258-169">yes</span></span>      | <span data-ttu-id="df258-170">要删除的包 ID</span><span class="sxs-lookup"><span data-stu-id="df258-170">The ID of the package to delete</span></span>
<span data-ttu-id="df258-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="df258-171">VERSION</span></span>        | <span data-ttu-id="df258-172">URL</span><span class="sxs-lookup"><span data-stu-id="df258-172">URL</span></span>    | <span data-ttu-id="df258-173">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-173">string</span></span> | <span data-ttu-id="df258-174">是</span><span class="sxs-lookup"><span data-stu-id="df258-174">yes</span></span>      | <span data-ttu-id="df258-175">要删除的包的版本</span><span class="sxs-lookup"><span data-stu-id="df258-175">The version of the package to delete</span></span>
<span data-ttu-id="df258-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="df258-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="df258-177">Header</span><span class="sxs-lookup"><span data-stu-id="df258-177">Header</span></span> | <span data-ttu-id="df258-178">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-178">string</span></span> | <span data-ttu-id="df258-179">是</span><span class="sxs-lookup"><span data-stu-id="df258-179">yes</span></span>      | <span data-ttu-id="df258-180">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="df258-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="df258-181">响应</span><span class="sxs-lookup"><span data-stu-id="df258-181">Response</span></span>

<span data-ttu-id="df258-182">状态代码</span><span class="sxs-lookup"><span data-stu-id="df258-182">Status Code</span></span> | <span data-ttu-id="df258-183">含义</span><span class="sxs-lookup"><span data-stu-id="df258-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="df258-184">204</span><span class="sxs-lookup"><span data-stu-id="df258-184">204</span></span>         | <span data-ttu-id="df258-185">删除此包，</span><span class="sxs-lookup"><span data-stu-id="df258-185">The package was deleted</span></span>
<span data-ttu-id="df258-186">404</span><span class="sxs-lookup"><span data-stu-id="df258-186">404</span></span>         | <span data-ttu-id="df258-187">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="df258-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="df258-188">重新列出包</span><span class="sxs-lookup"><span data-stu-id="df258-188">Relist a package</span></span>

<span data-ttu-id="df258-189">如果某个包未列出，则就可以使该包在使用"重新列出"终结点的搜索结果中再次可见。</span><span class="sxs-lookup"><span data-stu-id="df258-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="df258-190">此终结点有形状[删除 （取消列出） 终结点](#delete-a-package)但使用`POST`HTTP 方法，而不是`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="df258-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="df258-191">如果包已列出，请求仍会成功。</span><span class="sxs-lookup"><span data-stu-id="df258-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="df258-192">请求参数</span><span class="sxs-lookup"><span data-stu-id="df258-192">Request parameters</span></span>

<span data-ttu-id="df258-193">name</span><span class="sxs-lookup"><span data-stu-id="df258-193">Name</span></span>           | <span data-ttu-id="df258-194">内</span><span class="sxs-lookup"><span data-stu-id="df258-194">In</span></span>     | <span data-ttu-id="df258-195">类型</span><span class="sxs-lookup"><span data-stu-id="df258-195">Type</span></span>   | <span data-ttu-id="df258-196">必需</span><span class="sxs-lookup"><span data-stu-id="df258-196">Required</span></span> | <span data-ttu-id="df258-197">说明</span><span class="sxs-lookup"><span data-stu-id="df258-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="df258-198">Id</span><span class="sxs-lookup"><span data-stu-id="df258-198">ID</span></span>             | <span data-ttu-id="df258-199">URL</span><span class="sxs-lookup"><span data-stu-id="df258-199">URL</span></span>    | <span data-ttu-id="df258-200">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-200">string</span></span> | <span data-ttu-id="df258-201">是</span><span class="sxs-lookup"><span data-stu-id="df258-201">yes</span></span>      | <span data-ttu-id="df258-202">重新列出包的 ID</span><span class="sxs-lookup"><span data-stu-id="df258-202">The ID of the package to relist</span></span>
<span data-ttu-id="df258-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="df258-203">VERSION</span></span>        | <span data-ttu-id="df258-204">URL</span><span class="sxs-lookup"><span data-stu-id="df258-204">URL</span></span>    | <span data-ttu-id="df258-205">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-205">string</span></span> | <span data-ttu-id="df258-206">是</span><span class="sxs-lookup"><span data-stu-id="df258-206">yes</span></span>      | <span data-ttu-id="df258-207">重新列出包的版本</span><span class="sxs-lookup"><span data-stu-id="df258-207">The version of the package to relist</span></span>
<span data-ttu-id="df258-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="df258-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="df258-209">Header</span><span class="sxs-lookup"><span data-stu-id="df258-209">Header</span></span> | <span data-ttu-id="df258-210">字符串</span><span class="sxs-lookup"><span data-stu-id="df258-210">string</span></span> | <span data-ttu-id="df258-211">是</span><span class="sxs-lookup"><span data-stu-id="df258-211">yes</span></span>      | <span data-ttu-id="df258-212">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="df258-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="df258-213">响应</span><span class="sxs-lookup"><span data-stu-id="df258-213">Response</span></span>

<span data-ttu-id="df258-214">状态代码</span><span class="sxs-lookup"><span data-stu-id="df258-214">Status Code</span></span> | <span data-ttu-id="df258-215">含义</span><span class="sxs-lookup"><span data-stu-id="df258-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="df258-216">200</span><span class="sxs-lookup"><span data-stu-id="df258-216">200</span></span>         | <span data-ttu-id="df258-217">现在，该包列</span><span class="sxs-lookup"><span data-stu-id="df258-217">The package is now listed</span></span>
<span data-ttu-id="df258-218">404</span><span class="sxs-lookup"><span data-stu-id="df258-218">404</span></span>         | <span data-ttu-id="df258-219">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="df258-219">No package with the provided `ID` and `VERSION` exists</span></span>
