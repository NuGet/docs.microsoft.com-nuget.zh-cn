---
title: "推送和删除，NuGet API |Microsoft 文档"
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
description: "发布服务允许客户端发布新的包以及不列出或删除现有包。"
keywords: "NuGet API 推送包 NuGet API 删除包、 NuGet API 不列出包，NuGet API 上载包、 NuGet API 创建包"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="21a75-104">推送和删除</span><span class="sxs-lookup"><span data-stu-id="21a75-104">Push and Delete</span></span>

<span data-ttu-id="21a75-105">可以推送、 删除 （或不列出，具体取决于服务器实现），和 relist 使用 NuGet V3 API 的包。</span><span class="sxs-lookup"><span data-stu-id="21a75-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="21a75-106">这些操作基于注销`PackagePublish`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="21a75-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="21a75-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="21a75-107">Versioning</span></span>

<span data-ttu-id="21a75-108">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="21a75-108">The following `@type` value is used:</span></span>

<span data-ttu-id="21a75-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="21a75-109">@type value</span></span>          | <span data-ttu-id="21a75-110">说明</span><span class="sxs-lookup"><span data-stu-id="21a75-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="21a75-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="21a75-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="21a75-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="21a75-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="21a75-113">基 URL</span><span class="sxs-lookup"><span data-stu-id="21a75-113">Base URL</span></span>

<span data-ttu-id="21a75-114">以下 Api 的基 URL 是值`@id`属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="21a75-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="21a75-115">下面的文档中，使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="21a75-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="21a75-116">请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="21a75-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="21a75-117">请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。</span><span class="sxs-lookup"><span data-stu-id="21a75-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="21a75-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="21a75-118">HTTP methods</span></span>

<span data-ttu-id="21a75-119">`PUT`，`POST`和`DELETE`此资源支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="21a75-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="21a75-120">有关每个终结点支持的方法，请参阅下面。</span><span class="sxs-lookup"><span data-stu-id="21a75-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="21a75-121">推送包</span><span class="sxs-lookup"><span data-stu-id="21a75-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="21a75-122">nuget.org 具有[其他要求](NuGet-Protocols.md)与推送终结点进行交互。</span><span class="sxs-lookup"><span data-stu-id="21a75-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="21a75-123">nuget.org 支持使用以下 API 的推送新包。</span><span class="sxs-lookup"><span data-stu-id="21a75-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="21a75-124">如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。</span><span class="sxs-lookup"><span data-stu-id="21a75-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="21a75-125">其他包源可能支持替换现有包。</span><span class="sxs-lookup"><span data-stu-id="21a75-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="21a75-126">请求参数</span><span class="sxs-lookup"><span data-stu-id="21a75-126">Request parameters</span></span>

<span data-ttu-id="21a75-127">name</span><span class="sxs-lookup"><span data-stu-id="21a75-127">Name</span></span>           | <span data-ttu-id="21a75-128">内</span><span class="sxs-lookup"><span data-stu-id="21a75-128">In</span></span>     | <span data-ttu-id="21a75-129">类型</span><span class="sxs-lookup"><span data-stu-id="21a75-129">Type</span></span>   | <span data-ttu-id="21a75-130">必需</span><span class="sxs-lookup"><span data-stu-id="21a75-130">Required</span></span> | <span data-ttu-id="21a75-131">说明</span><span class="sxs-lookup"><span data-stu-id="21a75-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="21a75-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="21a75-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="21a75-133">Header</span><span class="sxs-lookup"><span data-stu-id="21a75-133">Header</span></span> | <span data-ttu-id="21a75-134">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-134">string</span></span> | <span data-ttu-id="21a75-135">是</span><span class="sxs-lookup"><span data-stu-id="21a75-135">yes</span></span>      | <span data-ttu-id="21a75-136">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="21a75-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="21a75-137">API 密钥是由用户从包源收到以及配置到客户端不透明的字符串。</span><span class="sxs-lookup"><span data-stu-id="21a75-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="21a75-138">没有特定字符串格式都将托管，但 API 密钥的长度不应超过合理的大小为 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="21a75-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="21a75-139">请求正文</span><span class="sxs-lookup"><span data-stu-id="21a75-139">Request body</span></span>

<span data-ttu-id="21a75-140">请求正文必须采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="21a75-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="21a75-141">多部分窗体数据</span><span class="sxs-lookup"><span data-stu-id="21a75-141">Multipart form data</span></span>

<span data-ttu-id="21a75-142">请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是被按.nupkg 的原始字节。</span><span class="sxs-lookup"><span data-stu-id="21a75-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="21a75-143">多部分正文中的后续项将被忽略。</span><span class="sxs-lookup"><span data-stu-id="21a75-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="21a75-144">忽略的文件名称或任何其他标头的多部分项。</span><span class="sxs-lookup"><span data-stu-id="21a75-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="21a75-145">响应</span><span class="sxs-lookup"><span data-stu-id="21a75-145">Response</span></span>

<span data-ttu-id="21a75-146">状态代码</span><span class="sxs-lookup"><span data-stu-id="21a75-146">Status Code</span></span> | <span data-ttu-id="21a75-147">含义</span><span class="sxs-lookup"><span data-stu-id="21a75-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="21a75-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="21a75-148">201, 202</span></span>    | <span data-ttu-id="21a75-149">成功推送包</span><span class="sxs-lookup"><span data-stu-id="21a75-149">The package was successfully pushed</span></span>
<span data-ttu-id="21a75-150">400</span><span class="sxs-lookup"><span data-stu-id="21a75-150">400</span></span>         | <span data-ttu-id="21a75-151">提供的包无效</span><span class="sxs-lookup"><span data-stu-id="21a75-151">The provided package is invalid</span></span>
<span data-ttu-id="21a75-152">409</span><span class="sxs-lookup"><span data-stu-id="21a75-152">409</span></span>         | <span data-ttu-id="21a75-153">具有提供的 ID 和版本的包已存在</span><span class="sxs-lookup"><span data-stu-id="21a75-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="21a75-154">服务器实现上成功状态代码返回成功推送包时存在差异。</span><span class="sxs-lookup"><span data-stu-id="21a75-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="21a75-155">删除包</span><span class="sxs-lookup"><span data-stu-id="21a75-155">Delete a package</span></span>

<span data-ttu-id="21a75-156">nuget.org 解释为包删除请求的"不列出"。</span><span class="sxs-lookup"><span data-stu-id="21a75-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="21a75-157">这意味着包仍可用于现有的包的使用者，但包不会再出现在搜索结果中或在 web 界面。</span><span class="sxs-lookup"><span data-stu-id="21a75-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="21a75-158">有关这种做法的详细信息，请参阅[删除包](../policies/deleting-packages.md)策略。</span><span class="sxs-lookup"><span data-stu-id="21a75-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="21a75-159">其他服务器实现可以自由地解释为硬删除此信号、 软删除，或不列出。</span><span class="sxs-lookup"><span data-stu-id="21a75-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="21a75-160">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持为 unlist 或硬删除基于配置选项处理此请求。</span><span class="sxs-lookup"><span data-stu-id="21a75-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="21a75-161">请求参数</span><span class="sxs-lookup"><span data-stu-id="21a75-161">Request parameters</span></span>

<span data-ttu-id="21a75-162">name</span><span class="sxs-lookup"><span data-stu-id="21a75-162">Name</span></span>           | <span data-ttu-id="21a75-163">内</span><span class="sxs-lookup"><span data-stu-id="21a75-163">In</span></span>     | <span data-ttu-id="21a75-164">类型</span><span class="sxs-lookup"><span data-stu-id="21a75-164">Type</span></span>   | <span data-ttu-id="21a75-165">必需</span><span class="sxs-lookup"><span data-stu-id="21a75-165">Required</span></span> | <span data-ttu-id="21a75-166">说明</span><span class="sxs-lookup"><span data-stu-id="21a75-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="21a75-167">Id</span><span class="sxs-lookup"><span data-stu-id="21a75-167">ID</span></span>             | <span data-ttu-id="21a75-168">URL</span><span class="sxs-lookup"><span data-stu-id="21a75-168">URL</span></span>    | <span data-ttu-id="21a75-169">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-169">string</span></span> | <span data-ttu-id="21a75-170">是</span><span class="sxs-lookup"><span data-stu-id="21a75-170">yes</span></span>      | <span data-ttu-id="21a75-171">要删除的包 ID</span><span class="sxs-lookup"><span data-stu-id="21a75-171">The ID of the package to delete</span></span>
<span data-ttu-id="21a75-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="21a75-172">VERSION</span></span>        | <span data-ttu-id="21a75-173">URL</span><span class="sxs-lookup"><span data-stu-id="21a75-173">URL</span></span>    | <span data-ttu-id="21a75-174">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-174">string</span></span> | <span data-ttu-id="21a75-175">是</span><span class="sxs-lookup"><span data-stu-id="21a75-175">yes</span></span>      | <span data-ttu-id="21a75-176">要删除的包的版本</span><span class="sxs-lookup"><span data-stu-id="21a75-176">The version of the package to delete</span></span>
<span data-ttu-id="21a75-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="21a75-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="21a75-178">Header</span><span class="sxs-lookup"><span data-stu-id="21a75-178">Header</span></span> | <span data-ttu-id="21a75-179">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-179">string</span></span> | <span data-ttu-id="21a75-180">是</span><span class="sxs-lookup"><span data-stu-id="21a75-180">yes</span></span>      | <span data-ttu-id="21a75-181">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="21a75-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="21a75-182">响应</span><span class="sxs-lookup"><span data-stu-id="21a75-182">Response</span></span>

<span data-ttu-id="21a75-183">状态代码</span><span class="sxs-lookup"><span data-stu-id="21a75-183">Status Code</span></span> | <span data-ttu-id="21a75-184">含义</span><span class="sxs-lookup"><span data-stu-id="21a75-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="21a75-185">204</span><span class="sxs-lookup"><span data-stu-id="21a75-185">204</span></span>         | <span data-ttu-id="21a75-186">删除此包，</span><span class="sxs-lookup"><span data-stu-id="21a75-186">The package was deleted</span></span>
<span data-ttu-id="21a75-187">404</span><span class="sxs-lookup"><span data-stu-id="21a75-187">404</span></span>         | <span data-ttu-id="21a75-188">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="21a75-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="21a75-189">Relist 包</span><span class="sxs-lookup"><span data-stu-id="21a75-189">Relist a package</span></span>

<span data-ttu-id="21a75-190">如果某个包未列出，则可以使该包在使用"relist"终结点的搜索结果中再次可见。</span><span class="sxs-lookup"><span data-stu-id="21a75-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="21a75-191">此终结点都具有相同形式[删除 （不列出） 终结点](#delete-a-package)但使用`POST`HTTP 方法，而不是`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="21a75-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="21a75-192">如果包已列出，请求仍会成功。</span><span class="sxs-lookup"><span data-stu-id="21a75-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="21a75-193">请求参数</span><span class="sxs-lookup"><span data-stu-id="21a75-193">Request parameters</span></span>

<span data-ttu-id="21a75-194">name</span><span class="sxs-lookup"><span data-stu-id="21a75-194">Name</span></span>           | <span data-ttu-id="21a75-195">内</span><span class="sxs-lookup"><span data-stu-id="21a75-195">In</span></span>     | <span data-ttu-id="21a75-196">类型</span><span class="sxs-lookup"><span data-stu-id="21a75-196">Type</span></span>   | <span data-ttu-id="21a75-197">必需</span><span class="sxs-lookup"><span data-stu-id="21a75-197">Required</span></span> | <span data-ttu-id="21a75-198">说明</span><span class="sxs-lookup"><span data-stu-id="21a75-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="21a75-199">Id</span><span class="sxs-lookup"><span data-stu-id="21a75-199">ID</span></span>             | <span data-ttu-id="21a75-200">URL</span><span class="sxs-lookup"><span data-stu-id="21a75-200">URL</span></span>    | <span data-ttu-id="21a75-201">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-201">string</span></span> | <span data-ttu-id="21a75-202">是</span><span class="sxs-lookup"><span data-stu-id="21a75-202">yes</span></span>      | <span data-ttu-id="21a75-203">要 relist 包的 ID</span><span class="sxs-lookup"><span data-stu-id="21a75-203">The ID of the package to relist</span></span>
<span data-ttu-id="21a75-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="21a75-204">VERSION</span></span>        | <span data-ttu-id="21a75-205">URL</span><span class="sxs-lookup"><span data-stu-id="21a75-205">URL</span></span>    | <span data-ttu-id="21a75-206">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-206">string</span></span> | <span data-ttu-id="21a75-207">是</span><span class="sxs-lookup"><span data-stu-id="21a75-207">yes</span></span>      | <span data-ttu-id="21a75-208">要 relist 的包的版本</span><span class="sxs-lookup"><span data-stu-id="21a75-208">The version of the package to relist</span></span>
<span data-ttu-id="21a75-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="21a75-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="21a75-210">Header</span><span class="sxs-lookup"><span data-stu-id="21a75-210">Header</span></span> | <span data-ttu-id="21a75-211">字符串</span><span class="sxs-lookup"><span data-stu-id="21a75-211">string</span></span> | <span data-ttu-id="21a75-212">是</span><span class="sxs-lookup"><span data-stu-id="21a75-212">yes</span></span>      | <span data-ttu-id="21a75-213">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="21a75-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="21a75-214">响应</span><span class="sxs-lookup"><span data-stu-id="21a75-214">Response</span></span>

<span data-ttu-id="21a75-215">状态代码</span><span class="sxs-lookup"><span data-stu-id="21a75-215">Status Code</span></span> | <span data-ttu-id="21a75-216">含义</span><span class="sxs-lookup"><span data-stu-id="21a75-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="21a75-217">200</span><span class="sxs-lookup"><span data-stu-id="21a75-217">200</span></span>         | <span data-ttu-id="21a75-218">包现在列出</span><span class="sxs-lookup"><span data-stu-id="21a75-218">The package is now listed</span></span>
<span data-ttu-id="21a75-219">404</span><span class="sxs-lookup"><span data-stu-id="21a75-219">404</span></span>         | <span data-ttu-id="21a75-220">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="21a75-220">No package with the provided `ID` and `VERSION` exists</span></span>
