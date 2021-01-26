---
title: 推送和删除，NuGet API
description: 发布服务允许客户端发布新包，并取消列出或删除现有包。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773920"
---
# <a name="push-and-delete"></a><span data-ttu-id="9ddad-103">推送和删除</span><span class="sxs-lookup"><span data-stu-id="9ddad-103">Push and Delete</span></span>

<span data-ttu-id="9ddad-104">使用 NuGet V3 API，可以推送、删除 (或取消列出，具体取决于服务器实现) 和重新列出包。</span><span class="sxs-lookup"><span data-stu-id="9ddad-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="9ddad-105">这些操作基于 `PackagePublish` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="9ddad-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9ddad-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="9ddad-106">Versioning</span></span>

<span data-ttu-id="9ddad-107">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="9ddad-107">The following `@type` value is used:</span></span>

<span data-ttu-id="9ddad-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="9ddad-108">@type value</span></span>          | <span data-ttu-id="9ddad-109">说明</span><span class="sxs-lookup"><span data-stu-id="9ddad-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="9ddad-110">PackagePublish/2.0。0</span><span class="sxs-lookup"><span data-stu-id="9ddad-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="9ddad-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="9ddad-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9ddad-112">基 URL</span><span class="sxs-lookup"><span data-stu-id="9ddad-112">Base URL</span></span>

<span data-ttu-id="9ddad-113">以下 Api 的基 URL 是 `@id` `PackagePublish/2.0.0` 包源的 [服务索引](service-index.md)中资源的属性的值。</span><span class="sxs-lookup"><span data-stu-id="9ddad-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="9ddad-114">对于以下文档，使用 nuget 的 URL。</span><span class="sxs-lookup"><span data-stu-id="9ddad-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="9ddad-115">请考虑 `https://www.nuget.org/api/v2/package` `@id` 在服务索引中找到的值的占位符。</span><span class="sxs-lookup"><span data-stu-id="9ddad-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="9ddad-116">请注意，此 URL 指向与旧版 V2 推送终结点相同的位置，因为协议是相同的。</span><span class="sxs-lookup"><span data-stu-id="9ddad-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9ddad-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="9ddad-117">HTTP methods</span></span>

<span data-ttu-id="9ddad-118">`PUT` `POST` `DELETE` 此资源支持、和 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="9ddad-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="9ddad-119">对于每个终结点支持的方法，请参阅下面的。</span><span class="sxs-lookup"><span data-stu-id="9ddad-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="9ddad-120">推送包</span><span class="sxs-lookup"><span data-stu-id="9ddad-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="9ddad-121">nuget.org 具有与推送终结点交互的 [其他要求](NuGet-Protocols.md) 。</span><span class="sxs-lookup"><span data-stu-id="9ddad-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="9ddad-122">nuget.org 支持使用以下 API 推送新包。</span><span class="sxs-lookup"><span data-stu-id="9ddad-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="9ddad-123">如果已存在具有提供的 ID 和版本的包，则 nuget.org 将拒绝推送。</span><span class="sxs-lookup"><span data-stu-id="9ddad-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="9ddad-124">其他包源可能支持替换现有包。</span><span class="sxs-lookup"><span data-stu-id="9ddad-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="9ddad-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="9ddad-125">Request parameters</span></span>

<span data-ttu-id="9ddad-126">名称</span><span class="sxs-lookup"><span data-stu-id="9ddad-126">Name</span></span>           | <span data-ttu-id="9ddad-127">In</span><span class="sxs-lookup"><span data-stu-id="9ddad-127">In</span></span>     | <span data-ttu-id="9ddad-128">类型</span><span class="sxs-lookup"><span data-stu-id="9ddad-128">Type</span></span>   | <span data-ttu-id="9ddad-129">必须</span><span class="sxs-lookup"><span data-stu-id="9ddad-129">Required</span></span> | <span data-ttu-id="9ddad-130">注释</span><span class="sxs-lookup"><span data-stu-id="9ddad-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9ddad-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9ddad-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9ddad-132">标头</span><span class="sxs-lookup"><span data-stu-id="9ddad-132">Header</span></span> | <span data-ttu-id="9ddad-133">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-133">string</span></span> | <span data-ttu-id="9ddad-134">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-134">yes</span></span>      | <span data-ttu-id="9ddad-135">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9ddad-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="9ddad-136">API 密钥是用户从包源中获得的不透明字符串，配置到客户端。</span><span class="sxs-lookup"><span data-stu-id="9ddad-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="9ddad-137">不会强制执行任何特定的字符串格式，但 API 密钥的长度不应超过 HTTP 标头值的合理大小。</span><span class="sxs-lookup"><span data-stu-id="9ddad-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="9ddad-138">请求正文</span><span class="sxs-lookup"><span data-stu-id="9ddad-138">Request body</span></span>

<span data-ttu-id="9ddad-139">请求正文必须采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="9ddad-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="9ddad-140">多部分表单数据</span><span class="sxs-lookup"><span data-stu-id="9ddad-140">Multipart form data</span></span>

<span data-ttu-id="9ddad-141">请求标头 `Content-Type` 为 `multipart/form-data` ，而请求正文中的第一项是所推送的 nupkg 的原始字节。</span><span class="sxs-lookup"><span data-stu-id="9ddad-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="9ddad-142">多部分正文中的后续项将被忽略。</span><span class="sxs-lookup"><span data-stu-id="9ddad-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="9ddad-143">将忽略多部分项目的文件名或任何其他标头。</span><span class="sxs-lookup"><span data-stu-id="9ddad-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="9ddad-144">响应</span><span class="sxs-lookup"><span data-stu-id="9ddad-144">Response</span></span>

<span data-ttu-id="9ddad-145">状态代码</span><span class="sxs-lookup"><span data-stu-id="9ddad-145">Status Code</span></span> | <span data-ttu-id="9ddad-146">含义</span><span class="sxs-lookup"><span data-stu-id="9ddad-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="9ddad-147">201、202</span><span class="sxs-lookup"><span data-stu-id="9ddad-147">201, 202</span></span>    | <span data-ttu-id="9ddad-148">已成功推送包</span><span class="sxs-lookup"><span data-stu-id="9ddad-148">The package was successfully pushed</span></span>
<span data-ttu-id="9ddad-149">400</span><span class="sxs-lookup"><span data-stu-id="9ddad-149">400</span></span>         | <span data-ttu-id="9ddad-150">提供的包无效</span><span class="sxs-lookup"><span data-stu-id="9ddad-150">The provided package is invalid</span></span>
<span data-ttu-id="9ddad-151">409</span><span class="sxs-lookup"><span data-stu-id="9ddad-151">409</span></span>         | <span data-ttu-id="9ddad-152">具有提供的 ID 和版本的包已存在</span><span class="sxs-lookup"><span data-stu-id="9ddad-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="9ddad-153">服务器实现不同于成功推送包时返回的成功状态代码。</span><span class="sxs-lookup"><span data-stu-id="9ddad-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="9ddad-154">删除包</span><span class="sxs-lookup"><span data-stu-id="9ddad-154">Delete a package</span></span>

<span data-ttu-id="9ddad-155">nuget.org 将包删除请求解释为 "取消列出"。</span><span class="sxs-lookup"><span data-stu-id="9ddad-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="9ddad-156">这意味着包对于包的现有使用者仍可用，但包不再显示在搜索结果或 web 界面中。</span><span class="sxs-lookup"><span data-stu-id="9ddad-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="9ddad-157">有关此操作的详细信息，请参阅 [已删除的包](../nuget-org/policies/deleting-packages.md) 策略。</span><span class="sxs-lookup"><span data-stu-id="9ddad-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="9ddad-158">其他服务器实现可随意将此信号解释为硬删除、软删除或取消列出。</span><span class="sxs-lookup"><span data-stu-id="9ddad-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="9ddad-159">例如， [NuGet. server](https://www.nuget.org/packages/NuGet.Server) (服务器实现仅支持旧版 V2 API) 支持将此请求作为基于配置选项的取消列出或硬删除进行处理。</span><span class="sxs-lookup"><span data-stu-id="9ddad-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9ddad-160">请求参数</span><span class="sxs-lookup"><span data-stu-id="9ddad-160">Request parameters</span></span>

<span data-ttu-id="9ddad-161">名称</span><span class="sxs-lookup"><span data-stu-id="9ddad-161">Name</span></span>           | <span data-ttu-id="9ddad-162">In</span><span class="sxs-lookup"><span data-stu-id="9ddad-162">In</span></span>     | <span data-ttu-id="9ddad-163">类型</span><span class="sxs-lookup"><span data-stu-id="9ddad-163">Type</span></span>   | <span data-ttu-id="9ddad-164">必须</span><span class="sxs-lookup"><span data-stu-id="9ddad-164">Required</span></span> | <span data-ttu-id="9ddad-165">注释</span><span class="sxs-lookup"><span data-stu-id="9ddad-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9ddad-166">ID</span><span class="sxs-lookup"><span data-stu-id="9ddad-166">ID</span></span>             | <span data-ttu-id="9ddad-167">URL</span><span class="sxs-lookup"><span data-stu-id="9ddad-167">URL</span></span>    | <span data-ttu-id="9ddad-168">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-168">string</span></span> | <span data-ttu-id="9ddad-169">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-169">yes</span></span>      | <span data-ttu-id="9ddad-170">要删除的包的 ID</span><span class="sxs-lookup"><span data-stu-id="9ddad-170">The ID of the package to delete</span></span>
<span data-ttu-id="9ddad-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="9ddad-171">VERSION</span></span>        | <span data-ttu-id="9ddad-172">URL</span><span class="sxs-lookup"><span data-stu-id="9ddad-172">URL</span></span>    | <span data-ttu-id="9ddad-173">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-173">string</span></span> | <span data-ttu-id="9ddad-174">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-174">yes</span></span>      | <span data-ttu-id="9ddad-175">要删除的包的版本</span><span class="sxs-lookup"><span data-stu-id="9ddad-175">The version of the package to delete</span></span>
<span data-ttu-id="9ddad-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9ddad-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9ddad-177">标头</span><span class="sxs-lookup"><span data-stu-id="9ddad-177">Header</span></span> | <span data-ttu-id="9ddad-178">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-178">string</span></span> | <span data-ttu-id="9ddad-179">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-179">yes</span></span>      | <span data-ttu-id="9ddad-180">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9ddad-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9ddad-181">响应</span><span class="sxs-lookup"><span data-stu-id="9ddad-181">Response</span></span>

<span data-ttu-id="9ddad-182">状态代码</span><span class="sxs-lookup"><span data-stu-id="9ddad-182">Status Code</span></span> | <span data-ttu-id="9ddad-183">含义</span><span class="sxs-lookup"><span data-stu-id="9ddad-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="9ddad-184">204</span><span class="sxs-lookup"><span data-stu-id="9ddad-184">204</span></span>         | <span data-ttu-id="9ddad-185">已删除包</span><span class="sxs-lookup"><span data-stu-id="9ddad-185">The package was deleted</span></span>
<span data-ttu-id="9ddad-186">404</span><span class="sxs-lookup"><span data-stu-id="9ddad-186">404</span></span>         | <span data-ttu-id="9ddad-187">未提供 `ID` 和存在具有的 `VERSION` 包</span><span class="sxs-lookup"><span data-stu-id="9ddad-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="9ddad-188">重新列出包</span><span class="sxs-lookup"><span data-stu-id="9ddad-188">Relist a package</span></span>

<span data-ttu-id="9ddad-189">如果未列出某个包，则可以使用 "重新列出" 终结点将该包再次显示在搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="9ddad-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="9ddad-190">此终结点与 [delete (取消列出) 终结点](#delete-a-package) 具有相同的形状，但使用 `POST` HTTP 方法而不是 `DELETE` 方法。</span><span class="sxs-lookup"><span data-stu-id="9ddad-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="9ddad-191">如果包已列出，请求仍会成功。</span><span class="sxs-lookup"><span data-stu-id="9ddad-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9ddad-192">请求参数</span><span class="sxs-lookup"><span data-stu-id="9ddad-192">Request parameters</span></span>

<span data-ttu-id="9ddad-193">名称</span><span class="sxs-lookup"><span data-stu-id="9ddad-193">Name</span></span>           | <span data-ttu-id="9ddad-194">In</span><span class="sxs-lookup"><span data-stu-id="9ddad-194">In</span></span>     | <span data-ttu-id="9ddad-195">类型</span><span class="sxs-lookup"><span data-stu-id="9ddad-195">Type</span></span>   | <span data-ttu-id="9ddad-196">必须</span><span class="sxs-lookup"><span data-stu-id="9ddad-196">Required</span></span> | <span data-ttu-id="9ddad-197">注释</span><span class="sxs-lookup"><span data-stu-id="9ddad-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9ddad-198">ID</span><span class="sxs-lookup"><span data-stu-id="9ddad-198">ID</span></span>             | <span data-ttu-id="9ddad-199">URL</span><span class="sxs-lookup"><span data-stu-id="9ddad-199">URL</span></span>    | <span data-ttu-id="9ddad-200">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-200">string</span></span> | <span data-ttu-id="9ddad-201">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-201">yes</span></span>      | <span data-ttu-id="9ddad-202">要重新列出的包的 ID</span><span class="sxs-lookup"><span data-stu-id="9ddad-202">The ID of the package to relist</span></span>
<span data-ttu-id="9ddad-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="9ddad-203">VERSION</span></span>        | <span data-ttu-id="9ddad-204">URL</span><span class="sxs-lookup"><span data-stu-id="9ddad-204">URL</span></span>    | <span data-ttu-id="9ddad-205">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-205">string</span></span> | <span data-ttu-id="9ddad-206">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-206">yes</span></span>      | <span data-ttu-id="9ddad-207">要重新列出的包的版本</span><span class="sxs-lookup"><span data-stu-id="9ddad-207">The version of the package to relist</span></span>
<span data-ttu-id="9ddad-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9ddad-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9ddad-209">标头</span><span class="sxs-lookup"><span data-stu-id="9ddad-209">Header</span></span> | <span data-ttu-id="9ddad-210">string</span><span class="sxs-lookup"><span data-stu-id="9ddad-210">string</span></span> | <span data-ttu-id="9ddad-211">是</span><span class="sxs-lookup"><span data-stu-id="9ddad-211">yes</span></span>      | <span data-ttu-id="9ddad-212">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9ddad-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9ddad-213">响应</span><span class="sxs-lookup"><span data-stu-id="9ddad-213">Response</span></span>

<span data-ttu-id="9ddad-214">状态代码</span><span class="sxs-lookup"><span data-stu-id="9ddad-214">Status Code</span></span> | <span data-ttu-id="9ddad-215">含义</span><span class="sxs-lookup"><span data-stu-id="9ddad-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="9ddad-216">200</span><span class="sxs-lookup"><span data-stu-id="9ddad-216">200</span></span>         | <span data-ttu-id="9ddad-217">现在会列出此包</span><span class="sxs-lookup"><span data-stu-id="9ddad-217">The package is now listed</span></span>
<span data-ttu-id="9ddad-218">404</span><span class="sxs-lookup"><span data-stu-id="9ddad-218">404</span></span>         | <span data-ttu-id="9ddad-219">未提供 `ID` 和存在具有的 `VERSION` 包</span><span class="sxs-lookup"><span data-stu-id="9ddad-219">No package with the provided `ID` and `VERSION` exists</span></span>
