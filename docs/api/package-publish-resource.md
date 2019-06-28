---
title: 推送和删除的 NuGet API
description: 发布服务允许客户端将新包发布和取消列出或删除现有的包。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426725"
---
# <a name="push-and-delete"></a><span data-ttu-id="47650-103">推送和删除</span><span class="sxs-lookup"><span data-stu-id="47650-103">Push and Delete</span></span>

<span data-ttu-id="47650-104">可以推送、 删除 （或取消列出，具体取决于服务器实现），并重新列出包使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="47650-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="47650-105">这些操作所基于的中断`PackagePublish`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="47650-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="47650-106">版本管理</span><span class="sxs-lookup"><span data-stu-id="47650-106">Versioning</span></span>

<span data-ttu-id="47650-107">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="47650-107">The following `@type` value is used:</span></span>

<span data-ttu-id="47650-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="47650-108">@type value</span></span>          | <span data-ttu-id="47650-109">说明</span><span class="sxs-lookup"><span data-stu-id="47650-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="47650-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="47650-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="47650-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="47650-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="47650-112">基 URL</span><span class="sxs-lookup"><span data-stu-id="47650-112">Base URL</span></span>

<span data-ttu-id="47650-113">以下 Api 的基 URL 是的值`@id`的属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="47650-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="47650-114">以下文档中，使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="47650-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="47650-115">请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="47650-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="47650-116">请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。</span><span class="sxs-lookup"><span data-stu-id="47650-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="47650-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="47650-117">HTTP methods</span></span>

<span data-ttu-id="47650-118">`PUT`，`POST`和`DELETE`此资源支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="47650-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="47650-119">有关每个终结点上支持哪些方法，请参阅下面。</span><span class="sxs-lookup"><span data-stu-id="47650-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="47650-120">将包推送</span><span class="sxs-lookup"><span data-stu-id="47650-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="47650-121">nuget.org 已[其他要求](NuGet-Protocols.md)与推送终结点进行交互。</span><span class="sxs-lookup"><span data-stu-id="47650-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="47650-122">nuget.org 支持推送新的包使用以下 API。</span><span class="sxs-lookup"><span data-stu-id="47650-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="47650-123">如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。</span><span class="sxs-lookup"><span data-stu-id="47650-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="47650-124">其他包源可能支持替换现有的包。</span><span class="sxs-lookup"><span data-stu-id="47650-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="47650-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="47650-125">Request parameters</span></span>

<span data-ttu-id="47650-126">名称</span><span class="sxs-lookup"><span data-stu-id="47650-126">Name</span></span>           | <span data-ttu-id="47650-127">内</span><span class="sxs-lookup"><span data-stu-id="47650-127">In</span></span>     | <span data-ttu-id="47650-128">类型</span><span class="sxs-lookup"><span data-stu-id="47650-128">Type</span></span>   | <span data-ttu-id="47650-129">必需</span><span class="sxs-lookup"><span data-stu-id="47650-129">Required</span></span> | <span data-ttu-id="47650-130">说明</span><span class="sxs-lookup"><span data-stu-id="47650-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="47650-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="47650-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="47650-132">Header</span><span class="sxs-lookup"><span data-stu-id="47650-132">Header</span></span> | <span data-ttu-id="47650-133">string</span><span class="sxs-lookup"><span data-stu-id="47650-133">string</span></span> | <span data-ttu-id="47650-134">是</span><span class="sxs-lookup"><span data-stu-id="47650-134">yes</span></span>      | <span data-ttu-id="47650-135">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="47650-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="47650-136">API 密钥是从包源获得由用户和配置到客户端不透明的字符串。</span><span class="sxs-lookup"><span data-stu-id="47650-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="47650-137">强制要求任何特定字符串格式，但 API 密钥的长度不应超过合理的大小，为 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="47650-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="47650-138">请求正文</span><span class="sxs-lookup"><span data-stu-id="47650-138">Request body</span></span>

<span data-ttu-id="47650-139">请求正文必须采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="47650-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="47650-140">多部分窗体数据</span><span class="sxs-lookup"><span data-stu-id="47650-140">Multipart form data</span></span>

<span data-ttu-id="47650-141">请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是推送.nupkg 的原始字节。</span><span class="sxs-lookup"><span data-stu-id="47650-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="47650-142">多部分正文中后面的项将被忽略。</span><span class="sxs-lookup"><span data-stu-id="47650-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="47650-143">将忽略的文件的名称或任何其他标头的多部分项。</span><span class="sxs-lookup"><span data-stu-id="47650-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="47650-144">响应</span><span class="sxs-lookup"><span data-stu-id="47650-144">Response</span></span>

<span data-ttu-id="47650-145">状态代码</span><span class="sxs-lookup"><span data-stu-id="47650-145">Status Code</span></span> | <span data-ttu-id="47650-146">含义</span><span class="sxs-lookup"><span data-stu-id="47650-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="47650-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="47650-147">201, 202</span></span>    | <span data-ttu-id="47650-148">已成功推送包</span><span class="sxs-lookup"><span data-stu-id="47650-148">The package was successfully pushed</span></span>
<span data-ttu-id="47650-149">400</span><span class="sxs-lookup"><span data-stu-id="47650-149">400</span></span>         | <span data-ttu-id="47650-150">提供的包无效</span><span class="sxs-lookup"><span data-stu-id="47650-150">The provided package is invalid</span></span>
<span data-ttu-id="47650-151">409</span><span class="sxs-lookup"><span data-stu-id="47650-151">409</span></span>         | <span data-ttu-id="47650-152">已存在具有提供的 ID 和版本的包</span><span class="sxs-lookup"><span data-stu-id="47650-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="47650-153">服务器实现上成功状态代码返回成功推送包时存在差异。</span><span class="sxs-lookup"><span data-stu-id="47650-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="47650-154">删除包</span><span class="sxs-lookup"><span data-stu-id="47650-154">Delete a package</span></span>

<span data-ttu-id="47650-155">nuget.org 将解释为包删除请求的"取消列出"。</span><span class="sxs-lookup"><span data-stu-id="47650-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="47650-156">这意味着包仍可用于包的现有使用者，但包不会再出现在搜索结果中或 web 界面中。</span><span class="sxs-lookup"><span data-stu-id="47650-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="47650-157">有关这种做法的详细信息，请参阅[删除包](../nuget-org/policies/deleting-packages.md)策略。</span><span class="sxs-lookup"><span data-stu-id="47650-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="47650-158">其他服务器实现可以自由地解释为硬删除此信号，软删除，或取消列出。</span><span class="sxs-lookup"><span data-stu-id="47650-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="47650-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持处理此请求作为未列出或硬删除基于配置选项。</span><span class="sxs-lookup"><span data-stu-id="47650-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="47650-160">请求参数</span><span class="sxs-lookup"><span data-stu-id="47650-160">Request parameters</span></span>

<span data-ttu-id="47650-161">名称</span><span class="sxs-lookup"><span data-stu-id="47650-161">Name</span></span>           | <span data-ttu-id="47650-162">内</span><span class="sxs-lookup"><span data-stu-id="47650-162">In</span></span>     | <span data-ttu-id="47650-163">类型</span><span class="sxs-lookup"><span data-stu-id="47650-163">Type</span></span>   | <span data-ttu-id="47650-164">必需</span><span class="sxs-lookup"><span data-stu-id="47650-164">Required</span></span> | <span data-ttu-id="47650-165">说明</span><span class="sxs-lookup"><span data-stu-id="47650-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="47650-166">Id</span><span class="sxs-lookup"><span data-stu-id="47650-166">ID</span></span>             | <span data-ttu-id="47650-167">URL</span><span class="sxs-lookup"><span data-stu-id="47650-167">URL</span></span>    | <span data-ttu-id="47650-168">string</span><span class="sxs-lookup"><span data-stu-id="47650-168">string</span></span> | <span data-ttu-id="47650-169">是</span><span class="sxs-lookup"><span data-stu-id="47650-169">yes</span></span>      | <span data-ttu-id="47650-170">要删除的包 ID</span><span class="sxs-lookup"><span data-stu-id="47650-170">The ID of the package to delete</span></span>
<span data-ttu-id="47650-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="47650-171">VERSION</span></span>        | <span data-ttu-id="47650-172">URL</span><span class="sxs-lookup"><span data-stu-id="47650-172">URL</span></span>    | <span data-ttu-id="47650-173">string</span><span class="sxs-lookup"><span data-stu-id="47650-173">string</span></span> | <span data-ttu-id="47650-174">是</span><span class="sxs-lookup"><span data-stu-id="47650-174">yes</span></span>      | <span data-ttu-id="47650-175">要删除的包的版本</span><span class="sxs-lookup"><span data-stu-id="47650-175">The version of the package to delete</span></span>
<span data-ttu-id="47650-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="47650-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="47650-177">Header</span><span class="sxs-lookup"><span data-stu-id="47650-177">Header</span></span> | <span data-ttu-id="47650-178">string</span><span class="sxs-lookup"><span data-stu-id="47650-178">string</span></span> | <span data-ttu-id="47650-179">是</span><span class="sxs-lookup"><span data-stu-id="47650-179">yes</span></span>      | <span data-ttu-id="47650-180">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="47650-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="47650-181">响应</span><span class="sxs-lookup"><span data-stu-id="47650-181">Response</span></span>

<span data-ttu-id="47650-182">状态代码</span><span class="sxs-lookup"><span data-stu-id="47650-182">Status Code</span></span> | <span data-ttu-id="47650-183">含义</span><span class="sxs-lookup"><span data-stu-id="47650-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="47650-184">204</span><span class="sxs-lookup"><span data-stu-id="47650-184">204</span></span>         | <span data-ttu-id="47650-185">删除此包，</span><span class="sxs-lookup"><span data-stu-id="47650-185">The package was deleted</span></span>
<span data-ttu-id="47650-186">404</span><span class="sxs-lookup"><span data-stu-id="47650-186">404</span></span>         | <span data-ttu-id="47650-187">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="47650-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="47650-188">重新列出包</span><span class="sxs-lookup"><span data-stu-id="47650-188">Relist a package</span></span>

<span data-ttu-id="47650-189">如果某个包未列出，则就可以使该包在使用"重新列出"终结点的搜索结果中再次可见。</span><span class="sxs-lookup"><span data-stu-id="47650-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="47650-190">此终结点有形状[删除 （取消列出） 终结点](#delete-a-package)但使用`POST`HTTP 方法，而不是`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="47650-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="47650-191">如果包已列出，请求仍会成功。</span><span class="sxs-lookup"><span data-stu-id="47650-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="47650-192">请求参数</span><span class="sxs-lookup"><span data-stu-id="47650-192">Request parameters</span></span>

<span data-ttu-id="47650-193">名称</span><span class="sxs-lookup"><span data-stu-id="47650-193">Name</span></span>           | <span data-ttu-id="47650-194">内</span><span class="sxs-lookup"><span data-stu-id="47650-194">In</span></span>     | <span data-ttu-id="47650-195">类型</span><span class="sxs-lookup"><span data-stu-id="47650-195">Type</span></span>   | <span data-ttu-id="47650-196">必需</span><span class="sxs-lookup"><span data-stu-id="47650-196">Required</span></span> | <span data-ttu-id="47650-197">说明</span><span class="sxs-lookup"><span data-stu-id="47650-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="47650-198">Id</span><span class="sxs-lookup"><span data-stu-id="47650-198">ID</span></span>             | <span data-ttu-id="47650-199">URL</span><span class="sxs-lookup"><span data-stu-id="47650-199">URL</span></span>    | <span data-ttu-id="47650-200">string</span><span class="sxs-lookup"><span data-stu-id="47650-200">string</span></span> | <span data-ttu-id="47650-201">是</span><span class="sxs-lookup"><span data-stu-id="47650-201">yes</span></span>      | <span data-ttu-id="47650-202">重新列出包的 ID</span><span class="sxs-lookup"><span data-stu-id="47650-202">The ID of the package to relist</span></span>
<span data-ttu-id="47650-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="47650-203">VERSION</span></span>        | <span data-ttu-id="47650-204">URL</span><span class="sxs-lookup"><span data-stu-id="47650-204">URL</span></span>    | <span data-ttu-id="47650-205">string</span><span class="sxs-lookup"><span data-stu-id="47650-205">string</span></span> | <span data-ttu-id="47650-206">是</span><span class="sxs-lookup"><span data-stu-id="47650-206">yes</span></span>      | <span data-ttu-id="47650-207">重新列出包的版本</span><span class="sxs-lookup"><span data-stu-id="47650-207">The version of the package to relist</span></span>
<span data-ttu-id="47650-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="47650-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="47650-209">Header</span><span class="sxs-lookup"><span data-stu-id="47650-209">Header</span></span> | <span data-ttu-id="47650-210">string</span><span class="sxs-lookup"><span data-stu-id="47650-210">string</span></span> | <span data-ttu-id="47650-211">是</span><span class="sxs-lookup"><span data-stu-id="47650-211">yes</span></span>      | <span data-ttu-id="47650-212">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="47650-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="47650-213">响应</span><span class="sxs-lookup"><span data-stu-id="47650-213">Response</span></span>

<span data-ttu-id="47650-214">状态代码</span><span class="sxs-lookup"><span data-stu-id="47650-214">Status Code</span></span> | <span data-ttu-id="47650-215">含义</span><span class="sxs-lookup"><span data-stu-id="47650-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="47650-216">200</span><span class="sxs-lookup"><span data-stu-id="47650-216">200</span></span>         | <span data-ttu-id="47650-217">现在，该包列</span><span class="sxs-lookup"><span data-stu-id="47650-217">The package is now listed</span></span>
<span data-ttu-id="47650-218">404</span><span class="sxs-lookup"><span data-stu-id="47650-218">404</span></span>         | <span data-ttu-id="47650-219">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="47650-219">No package with the provided `ID` and `VERSION` exists</span></span>
