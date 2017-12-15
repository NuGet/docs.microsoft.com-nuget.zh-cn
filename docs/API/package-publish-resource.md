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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "发布服务允许客户端发布新的包以及不列出或删除现有包。"
keywords: "NuGet API 推送包 NuGet API 删除包、 NuGet API 不列出包，NuGet API 上载包、 NuGet API 创建包"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="49390-104">推送和删除</span><span class="sxs-lookup"><span data-stu-id="49390-104">Push and Delete</span></span>

<span data-ttu-id="49390-105">可以推送和删除 （或不列出，具体取决于服务器实现） 包使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="49390-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="49390-106">这两种操作基于注销`PackagePublish`资源位于[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="49390-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="49390-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="49390-107">Versioning</span></span>

<span data-ttu-id="49390-108">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="49390-108">The following `@type` value is used:</span></span>

<span data-ttu-id="49390-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="49390-109">@type value</span></span>          | <span data-ttu-id="49390-110">说明</span><span class="sxs-lookup"><span data-stu-id="49390-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="49390-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="49390-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="49390-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="49390-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="49390-113">基 URL</span><span class="sxs-lookup"><span data-stu-id="49390-113">Base URL</span></span>

<span data-ttu-id="49390-114">以下 Api 的基 URL 是值`@id`属性`PackagePublish/2.0.0`包源中的资源[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="49390-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="49390-115">下面的文档中，使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="49390-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="49390-116">请考虑`https://www.nuget.org/api/v2/package`作为占位符`@id`服务索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="49390-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="49390-117">请注意此 URL 指向与旧的 V2 推送终结点相同的位置，因为协议是相同。</span><span class="sxs-lookup"><span data-stu-id="49390-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="49390-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="49390-118">HTTP methods</span></span>

<span data-ttu-id="49390-119">`PUT`和`DELETE`此资源支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="49390-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="49390-120">有关每个终结点支持的方法，请参阅下面。</span><span class="sxs-lookup"><span data-stu-id="49390-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="49390-121">推送包</span><span class="sxs-lookup"><span data-stu-id="49390-121">Push a package</span></span>

<span data-ttu-id="49390-122">nuget.org 支持使用以下 API 的推送新包。</span><span class="sxs-lookup"><span data-stu-id="49390-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="49390-123">如果已存在具有提供的 ID 和版本的包，nuget.org 将拒绝推送。</span><span class="sxs-lookup"><span data-stu-id="49390-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="49390-124">其他包源可能支持替换现有包。</span><span class="sxs-lookup"><span data-stu-id="49390-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="49390-125">请求参数</span><span class="sxs-lookup"><span data-stu-id="49390-125">Request parameters</span></span>

<span data-ttu-id="49390-126">名称</span><span class="sxs-lookup"><span data-stu-id="49390-126">Name</span></span>           | <span data-ttu-id="49390-127">内</span><span class="sxs-lookup"><span data-stu-id="49390-127">In</span></span>     | <span data-ttu-id="49390-128">类型</span><span class="sxs-lookup"><span data-stu-id="49390-128">Type</span></span>   | <span data-ttu-id="49390-129">必需</span><span class="sxs-lookup"><span data-stu-id="49390-129">Required</span></span> | <span data-ttu-id="49390-130">说明</span><span class="sxs-lookup"><span data-stu-id="49390-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="49390-131">X NuGet ApiKey</span><span class="sxs-lookup"><span data-stu-id="49390-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="49390-132">Header</span><span class="sxs-lookup"><span data-stu-id="49390-132">Header</span></span> | <span data-ttu-id="49390-133">string</span><span class="sxs-lookup"><span data-stu-id="49390-133">string</span></span> | <span data-ttu-id="49390-134">是</span><span class="sxs-lookup"><span data-stu-id="49390-134">yes</span></span>      | <span data-ttu-id="49390-135">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="49390-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="49390-136">API 密钥是由用户从包源收到以及配置到客户端不透明的字符串。</span><span class="sxs-lookup"><span data-stu-id="49390-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="49390-137">没有特定字符串格式都将托管，但 API 密钥的长度不应超过合理的大小为 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="49390-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="49390-138">请求正文</span><span class="sxs-lookup"><span data-stu-id="49390-138">Request body</span></span>

<span data-ttu-id="49390-139">请求正文必须采用以下形式：</span><span class="sxs-lookup"><span data-stu-id="49390-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="49390-140">多部分窗体数据</span><span class="sxs-lookup"><span data-stu-id="49390-140">Multipart form data</span></span>

<span data-ttu-id="49390-141">请求标头`Content-Type`是`multipart/form-data`和请求正文中的第一项是被按.nupkg 的原始字节。</span><span class="sxs-lookup"><span data-stu-id="49390-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="49390-142">多部分正文中的后续项将被忽略。</span><span class="sxs-lookup"><span data-stu-id="49390-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="49390-143">忽略的文件名称或任何其他标头的多部分项。</span><span class="sxs-lookup"><span data-stu-id="49390-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="49390-144">响应</span><span class="sxs-lookup"><span data-stu-id="49390-144">Response</span></span>

<span data-ttu-id="49390-145">状态代码</span><span class="sxs-lookup"><span data-stu-id="49390-145">Status Code</span></span> | <span data-ttu-id="49390-146">含义</span><span class="sxs-lookup"><span data-stu-id="49390-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="49390-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="49390-147">201, 202</span></span>    | <span data-ttu-id="49390-148">成功推送包</span><span class="sxs-lookup"><span data-stu-id="49390-148">The package was successfully pushed</span></span>
<span data-ttu-id="49390-149">400</span><span class="sxs-lookup"><span data-stu-id="49390-149">400</span></span>         | <span data-ttu-id="49390-150">提供的包无效</span><span class="sxs-lookup"><span data-stu-id="49390-150">The provided package is invalid</span></span>
<span data-ttu-id="49390-151">409</span><span class="sxs-lookup"><span data-stu-id="49390-151">409</span></span>         | <span data-ttu-id="49390-152">具有提供的 ID 和版本的包已存在</span><span class="sxs-lookup"><span data-stu-id="49390-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="49390-153">服务器实现上成功状态代码返回成功推送包时存在差异。</span><span class="sxs-lookup"><span data-stu-id="49390-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="49390-154">删除包</span><span class="sxs-lookup"><span data-stu-id="49390-154">Delete a package</span></span>

<span data-ttu-id="49390-155">nuget.org 解释为包删除请求的"不列出"。</span><span class="sxs-lookup"><span data-stu-id="49390-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="49390-156">这意味着包仍可用于现有的包的使用者，但包不会再出现在搜索结果中或在 web 界面。</span><span class="sxs-lookup"><span data-stu-id="49390-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="49390-157">有关这种做法的详细信息，请参阅[删除包](../policies/deleting-packages.md)策略。</span><span class="sxs-lookup"><span data-stu-id="49390-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="49390-158">其他服务器实现可以自由地解释为硬删除此信号、 软删除，或不列出。</span><span class="sxs-lookup"><span data-stu-id="49390-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="49390-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （仅支持较旧的 V2 API 的服务器实现） 支持为 unlist 或硬删除基于配置选项处理此请求。</span><span class="sxs-lookup"><span data-stu-id="49390-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="49390-160">请求参数</span><span class="sxs-lookup"><span data-stu-id="49390-160">Request parameters</span></span>

<span data-ttu-id="49390-161">名称</span><span class="sxs-lookup"><span data-stu-id="49390-161">Name</span></span>           | <span data-ttu-id="49390-162">内</span><span class="sxs-lookup"><span data-stu-id="49390-162">In</span></span>     | <span data-ttu-id="49390-163">类型</span><span class="sxs-lookup"><span data-stu-id="49390-163">Type</span></span>   | <span data-ttu-id="49390-164">必需</span><span class="sxs-lookup"><span data-stu-id="49390-164">Required</span></span> | <span data-ttu-id="49390-165">说明</span><span class="sxs-lookup"><span data-stu-id="49390-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="49390-166">Id</span><span class="sxs-lookup"><span data-stu-id="49390-166">ID</span></span>             | <span data-ttu-id="49390-167">URL</span><span class="sxs-lookup"><span data-stu-id="49390-167">URL</span></span>    | <span data-ttu-id="49390-168">string</span><span class="sxs-lookup"><span data-stu-id="49390-168">string</span></span> | <span data-ttu-id="49390-169">是</span><span class="sxs-lookup"><span data-stu-id="49390-169">yes</span></span>      | <span data-ttu-id="49390-170">要删除的包 ID</span><span class="sxs-lookup"><span data-stu-id="49390-170">The ID of the package to delete</span></span>
<span data-ttu-id="49390-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="49390-171">VERSION</span></span>        | <span data-ttu-id="49390-172">URL</span><span class="sxs-lookup"><span data-stu-id="49390-172">URL</span></span>    | <span data-ttu-id="49390-173">string</span><span class="sxs-lookup"><span data-stu-id="49390-173">string</span></span> | <span data-ttu-id="49390-174">是</span><span class="sxs-lookup"><span data-stu-id="49390-174">yes</span></span>      | <span data-ttu-id="49390-175">要删除的包的版本</span><span class="sxs-lookup"><span data-stu-id="49390-175">The version of the package to delete</span></span>
<span data-ttu-id="49390-176">X NuGet ApiKey</span><span class="sxs-lookup"><span data-stu-id="49390-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="49390-177">Header</span><span class="sxs-lookup"><span data-stu-id="49390-177">Header</span></span> | <span data-ttu-id="49390-178">string</span><span class="sxs-lookup"><span data-stu-id="49390-178">string</span></span> | <span data-ttu-id="49390-179">是</span><span class="sxs-lookup"><span data-stu-id="49390-179">yes</span></span>      | <span data-ttu-id="49390-180">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="49390-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="49390-181">响应</span><span class="sxs-lookup"><span data-stu-id="49390-181">Response</span></span>

<span data-ttu-id="49390-182">状态代码</span><span class="sxs-lookup"><span data-stu-id="49390-182">Status Code</span></span> | <span data-ttu-id="49390-183">含义</span><span class="sxs-lookup"><span data-stu-id="49390-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="49390-184">204</span><span class="sxs-lookup"><span data-stu-id="49390-184">204</span></span>         | <span data-ttu-id="49390-185">删除此包，</span><span class="sxs-lookup"><span data-stu-id="49390-185">The package was deleted</span></span>
<span data-ttu-id="49390-186">404</span><span class="sxs-lookup"><span data-stu-id="49390-186">404</span></span>         | <span data-ttu-id="49390-187">利用所提供的任何包`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="49390-187">No package with the provided `ID` and `VERSION` exists</span></span>
