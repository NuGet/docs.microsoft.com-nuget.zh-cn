---
title: nuget.org 协议
description: 用于与 NuGet 客户端进行交互的演变 nuget.org 协议。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773975"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="77b64-103">nuget.org 协议</span><span class="sxs-lookup"><span data-stu-id="77b64-103">nuget.org protocols</span></span>

<span data-ttu-id="77b64-104">若要与 nuget.org 交互，客户端需要遵循某些协议。</span><span class="sxs-lookup"><span data-stu-id="77b64-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="77b64-105">由于这些协议不断发展，因此客户端必须在调用特定的 nuget.org Api 时标识它们使用的协议版本。</span><span class="sxs-lookup"><span data-stu-id="77b64-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="77b64-106">这允许 nuget.org 为旧客户端引入非重大的更改。</span><span class="sxs-lookup"><span data-stu-id="77b64-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="77b64-107">本页面上所述的 Api 特定于 nuget.org，并且不希望其他 NuGet 服务器实现引入这些 Api。</span><span class="sxs-lookup"><span data-stu-id="77b64-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="77b64-108">有关在 NuGet 生态系统中广泛实现的 NuGet API 的信息，请参阅 [API 概述](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="77b64-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="77b64-109">本主题列出了各种协议，无论它们何时存在都是如此。</span><span class="sxs-lookup"><span data-stu-id="77b64-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="77b64-110">NuGet 协议版本4.1。0</span><span class="sxs-lookup"><span data-stu-id="77b64-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="77b64-111">4.1.0 协议指定使用验证作用域密钥与 nuget.org 以外的服务进行交互，以针对 nuget.org 帐户验证包。</span><span class="sxs-lookup"><span data-stu-id="77b64-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="77b64-112">请注意， `4.1.0` 版本号是不透明的字符串，但会与支持此协议的第一个正式 NuGet 客户端版本一致。</span><span class="sxs-lookup"><span data-stu-id="77b64-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="77b64-113">验证可确保用户创建的 API 密钥仅与 nuget.org 一起使用，并且第三方服务的其他验证或验证是通过一次性使用验证-作用域密钥来处理的。</span><span class="sxs-lookup"><span data-stu-id="77b64-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="77b64-114">可以使用这些验证作用域密钥来验证包是否属于特定用户 (帐户) nuget.org 上。</span><span class="sxs-lookup"><span data-stu-id="77b64-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="77b64-115">客户端要求</span><span class="sxs-lookup"><span data-stu-id="77b64-115">Client requirement</span></span>

<span data-ttu-id="77b64-116">当客户端进行 API 调用以将包 **推送** 到 nuget.org 时，需要客户端传递以下标头：</span><span class="sxs-lookup"><span data-stu-id="77b64-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="77b64-117">请注意， `X-NuGet-Client-Version` 标头具有相似的语义，但保留为仅供官方 NuGet 客户端使用。</span><span class="sxs-lookup"><span data-stu-id="77b64-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="77b64-118">第三方客户端应使用 `X-NuGet-Protocol-Version` 标头和值。</span><span class="sxs-lookup"><span data-stu-id="77b64-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="77b64-119">[ `PackagePublish` 资源](package-publish-resource.md)的文档中描述了 **推送** 协议本身。</span><span class="sxs-lookup"><span data-stu-id="77b64-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="77b64-120">如果客户端与外部服务进行交互，并且需要验证包是否属于特定用户 (帐户) ，则它应使用以下协议，并使用 nuget.org 中的验证作用域密钥而不是 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="77b64-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="77b64-121">用于请求验证作用域密钥的 API</span><span class="sxs-lookup"><span data-stu-id="77b64-121">API to request a verify-scope key</span></span>

<span data-ttu-id="77b64-122">此 API 用于获取 nuget.org 作者验证范围的密钥，以便验证其拥有的包。</span><span class="sxs-lookup"><span data-stu-id="77b64-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="77b64-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="77b64-123">Request parameters</span></span>

<span data-ttu-id="77b64-124">名称</span><span class="sxs-lookup"><span data-stu-id="77b64-124">Name</span></span>           | <span data-ttu-id="77b64-125">In</span><span class="sxs-lookup"><span data-stu-id="77b64-125">In</span></span>     | <span data-ttu-id="77b64-126">类型</span><span class="sxs-lookup"><span data-stu-id="77b64-126">Type</span></span>   | <span data-ttu-id="77b64-127">必须</span><span class="sxs-lookup"><span data-stu-id="77b64-127">Required</span></span> | <span data-ttu-id="77b64-128">注释</span><span class="sxs-lookup"><span data-stu-id="77b64-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="77b64-129">ID</span><span class="sxs-lookup"><span data-stu-id="77b64-129">ID</span></span>             | <span data-ttu-id="77b64-130">URL</span><span class="sxs-lookup"><span data-stu-id="77b64-130">URL</span></span>    | <span data-ttu-id="77b64-131">string</span><span class="sxs-lookup"><span data-stu-id="77b64-131">string</span></span> | <span data-ttu-id="77b64-132">是</span><span class="sxs-lookup"><span data-stu-id="77b64-132">yes</span></span>      | <span data-ttu-id="77b64-133">为其请求验证作用域密钥的包 identidier</span><span class="sxs-lookup"><span data-stu-id="77b64-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="77b64-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="77b64-134">VERSION</span></span>        | <span data-ttu-id="77b64-135">URL</span><span class="sxs-lookup"><span data-stu-id="77b64-135">URL</span></span>    | <span data-ttu-id="77b64-136">string</span><span class="sxs-lookup"><span data-stu-id="77b64-136">string</span></span> | <span data-ttu-id="77b64-137">否</span><span class="sxs-lookup"><span data-stu-id="77b64-137">no</span></span>       | <span data-ttu-id="77b64-138">包版本</span><span class="sxs-lookup"><span data-stu-id="77b64-138">The package version</span></span>
<span data-ttu-id="77b64-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="77b64-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="77b64-140">标头</span><span class="sxs-lookup"><span data-stu-id="77b64-140">Header</span></span> | <span data-ttu-id="77b64-141">string</span><span class="sxs-lookup"><span data-stu-id="77b64-141">string</span></span> | <span data-ttu-id="77b64-142">是</span><span class="sxs-lookup"><span data-stu-id="77b64-142">yes</span></span>      | <span data-ttu-id="77b64-143">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="77b64-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="77b64-144">响应</span><span class="sxs-lookup"><span data-stu-id="77b64-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="77b64-145">用于验证验证作用域密钥的 API</span><span class="sxs-lookup"><span data-stu-id="77b64-145">API to verify the verify scope key</span></span>

<span data-ttu-id="77b64-146">此 API 用于验证 nuget.org 作者拥有的包的验证范围键。</span><span class="sxs-lookup"><span data-stu-id="77b64-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="77b64-147">请求参数</span><span class="sxs-lookup"><span data-stu-id="77b64-147">Request parameters</span></span>

<span data-ttu-id="77b64-148">名称</span><span class="sxs-lookup"><span data-stu-id="77b64-148">Name</span></span>           | <span data-ttu-id="77b64-149">In</span><span class="sxs-lookup"><span data-stu-id="77b64-149">In</span></span>     | <span data-ttu-id="77b64-150">类型</span><span class="sxs-lookup"><span data-stu-id="77b64-150">Type</span></span>   | <span data-ttu-id="77b64-151">必须</span><span class="sxs-lookup"><span data-stu-id="77b64-151">Required</span></span> | <span data-ttu-id="77b64-152">注释</span><span class="sxs-lookup"><span data-stu-id="77b64-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="77b64-153">ID</span><span class="sxs-lookup"><span data-stu-id="77b64-153">ID</span></span>             | <span data-ttu-id="77b64-154">URL</span><span class="sxs-lookup"><span data-stu-id="77b64-154">URL</span></span>    | <span data-ttu-id="77b64-155">string</span><span class="sxs-lookup"><span data-stu-id="77b64-155">string</span></span> | <span data-ttu-id="77b64-156">是</span><span class="sxs-lookup"><span data-stu-id="77b64-156">yes</span></span>      | <span data-ttu-id="77b64-157">为其请求验证作用域密钥的包标识符</span><span class="sxs-lookup"><span data-stu-id="77b64-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="77b64-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="77b64-158">VERSION</span></span>        | <span data-ttu-id="77b64-159">URL</span><span class="sxs-lookup"><span data-stu-id="77b64-159">URL</span></span>    | <span data-ttu-id="77b64-160">string</span><span class="sxs-lookup"><span data-stu-id="77b64-160">string</span></span> | <span data-ttu-id="77b64-161">否</span><span class="sxs-lookup"><span data-stu-id="77b64-161">no</span></span>       | <span data-ttu-id="77b64-162">包版本</span><span class="sxs-lookup"><span data-stu-id="77b64-162">The package version</span></span>
<span data-ttu-id="77b64-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="77b64-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="77b64-164">标头</span><span class="sxs-lookup"><span data-stu-id="77b64-164">Header</span></span> | <span data-ttu-id="77b64-165">string</span><span class="sxs-lookup"><span data-stu-id="77b64-165">string</span></span> | <span data-ttu-id="77b64-166">是</span><span class="sxs-lookup"><span data-stu-id="77b64-166">yes</span></span>      | <span data-ttu-id="77b64-167">例如： `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="77b64-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="77b64-168">此验证作用域 API 密钥会在一天的时间或第一次使用时过期，以先发生的情况为准。</span><span class="sxs-lookup"><span data-stu-id="77b64-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="77b64-169">响应</span><span class="sxs-lookup"><span data-stu-id="77b64-169">Response</span></span>

<span data-ttu-id="77b64-170">状态代码</span><span class="sxs-lookup"><span data-stu-id="77b64-170">Status Code</span></span> | <span data-ttu-id="77b64-171">含义</span><span class="sxs-lookup"><span data-stu-id="77b64-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="77b64-172">200</span><span class="sxs-lookup"><span data-stu-id="77b64-172">200</span></span>         | <span data-ttu-id="77b64-173">API 密钥有效</span><span class="sxs-lookup"><span data-stu-id="77b64-173">The API key is valid</span></span>
<span data-ttu-id="77b64-174">403</span><span class="sxs-lookup"><span data-stu-id="77b64-174">403</span></span>         | <span data-ttu-id="77b64-175">API 密钥无效或无权推送包</span><span class="sxs-lookup"><span data-stu-id="77b64-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="77b64-176">404</span><span class="sxs-lookup"><span data-stu-id="77b64-176">404</span></span>         | <span data-ttu-id="77b64-177">由引用的包 `ID` 和 `VERSION` (可选) 不存在</span><span class="sxs-lookup"><span data-stu-id="77b64-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
