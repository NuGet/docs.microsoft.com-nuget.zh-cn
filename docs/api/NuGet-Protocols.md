---
title: nuget.org 协议
description: 要与 NuGet 客户端交互的不断发展 nuget.org 协议。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547268"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="ea7f9-103">nuget.org 协议</span><span class="sxs-lookup"><span data-stu-id="ea7f9-103">nuget.org protocols</span></span>

<span data-ttu-id="ea7f9-104">若要与 nuget.org 进行交互，客户端需要遵守某些协议。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="ea7f9-105">由于这些协议，让不断演变，客户端必须标识调用特定 nuget.org Api 时，它们使用的协议版本。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="ea7f9-106">这样，nuget.org 的旧客户端不间断的方式引入的更改。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="ea7f9-107">此页上所述的 Api 是特定于 nuget.org 并且没有任何其他 NuGet 服务器上实现来引入这些 Api 的假定条件。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="ea7f9-108">有关在 NuGet 生态系统中实施广泛 NuGet API 的信息，请参阅[API 概述](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="ea7f9-109">本主题列出了作为各种协议和时它们可以直接对存在。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="ea7f9-110">NuGet 协议版本 4.1.0</span><span class="sxs-lookup"><span data-stu-id="ea7f9-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="ea7f9-111">4.1.0 协议指定验证范围密钥与 nuget.org 中，若要验证包对 nuget.org 帐户以外的服务进行交互的用法。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="ea7f9-112">请注意，`4.1.0`数目是不透明的字符串，但恰好官方 NuGet 客户端支持此协议的第一个版本的版本。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="ea7f9-113">验证可确保用户创建 API 密钥仅用于 nuget.org 中，并通过使用一次验证作用域键处理该验证或通过第三方服务的验证。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="ea7f9-114">这些验证范围密钥可以用于验证包属于 nuget.org 上的特定用户 （帐户）。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="ea7f9-115">客户端要求</span><span class="sxs-lookup"><span data-stu-id="ea7f9-115">Client requirement</span></span>

<span data-ttu-id="ea7f9-116">要求客户端时它们向发出 API 调用传递以下标头**推送**到 nuget.org 的包：</span><span class="sxs-lookup"><span data-stu-id="ea7f9-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="ea7f9-117">请注意，`X-NuGet-Client-Version`标头具有类似语义，但将其保留仅供官方 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="ea7f9-118">第三方客户端应使用`X-NuGet-Protocol-Version`标头和值。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="ea7f9-119">**推送**协议本身中的文档所述[`PackagePublish`资源](package-publish-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="ea7f9-120">如果客户端与外部服务，需要验证是否属于特定用户 （帐户） 的包进行交互，它应使用以下协议，并使用作用域的验证密钥和不从 nuget.org 的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="ea7f9-121">API 请求作用域的验证密钥</span><span class="sxs-lookup"><span data-stu-id="ea7f9-121">API to request a verify-scope key</span></span>

<span data-ttu-id="ea7f9-122">此 API 用于获取 nuget.org 作者可以验证拥有的他/她的包的作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="ea7f9-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="ea7f9-123">Request parameters</span></span>

<span data-ttu-id="ea7f9-124">name</span><span class="sxs-lookup"><span data-stu-id="ea7f9-124">Name</span></span>           | <span data-ttu-id="ea7f9-125">内</span><span class="sxs-lookup"><span data-stu-id="ea7f9-125">In</span></span>     | <span data-ttu-id="ea7f9-126">类型</span><span class="sxs-lookup"><span data-stu-id="ea7f9-126">Type</span></span>   | <span data-ttu-id="ea7f9-127">必需</span><span class="sxs-lookup"><span data-stu-id="ea7f9-127">Required</span></span> | <span data-ttu-id="ea7f9-128">说明</span><span class="sxs-lookup"><span data-stu-id="ea7f9-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ea7f9-129">Id</span><span class="sxs-lookup"><span data-stu-id="ea7f9-129">ID</span></span>             | <span data-ttu-id="ea7f9-130">URL</span><span class="sxs-lookup"><span data-stu-id="ea7f9-130">URL</span></span>    | <span data-ttu-id="ea7f9-131">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-131">string</span></span> | <span data-ttu-id="ea7f9-132">是</span><span class="sxs-lookup"><span data-stu-id="ea7f9-132">yes</span></span>      | <span data-ttu-id="ea7f9-133">为其请求验证作用域键包 identidier</span><span class="sxs-lookup"><span data-stu-id="ea7f9-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="ea7f9-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="ea7f9-134">VERSION</span></span>        | <span data-ttu-id="ea7f9-135">URL</span><span class="sxs-lookup"><span data-stu-id="ea7f9-135">URL</span></span>    | <span data-ttu-id="ea7f9-136">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-136">string</span></span> | <span data-ttu-id="ea7f9-137">否</span><span class="sxs-lookup"><span data-stu-id="ea7f9-137">no</span></span>       | <span data-ttu-id="ea7f9-138">包版本</span><span class="sxs-lookup"><span data-stu-id="ea7f9-138">The package version</span></span>
<span data-ttu-id="ea7f9-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ea7f9-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ea7f9-140">Header</span><span class="sxs-lookup"><span data-stu-id="ea7f9-140">Header</span></span> | <span data-ttu-id="ea7f9-141">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-141">string</span></span> | <span data-ttu-id="ea7f9-142">是</span><span class="sxs-lookup"><span data-stu-id="ea7f9-142">yes</span></span>      | <span data-ttu-id="ea7f9-143">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="ea7f9-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="ea7f9-144">响应</span><span class="sxs-lookup"><span data-stu-id="ea7f9-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="ea7f9-145">若要验证验证作用域键的 API</span><span class="sxs-lookup"><span data-stu-id="ea7f9-145">API to verify the verify scope key</span></span>

<span data-ttu-id="ea7f9-146">此 API 用于验证归 nuget.org 作者的包的作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="ea7f9-147">请求参数</span><span class="sxs-lookup"><span data-stu-id="ea7f9-147">Request parameters</span></span>

<span data-ttu-id="ea7f9-148">name</span><span class="sxs-lookup"><span data-stu-id="ea7f9-148">Name</span></span>           | <span data-ttu-id="ea7f9-149">内</span><span class="sxs-lookup"><span data-stu-id="ea7f9-149">In</span></span>     | <span data-ttu-id="ea7f9-150">类型</span><span class="sxs-lookup"><span data-stu-id="ea7f9-150">Type</span></span>   | <span data-ttu-id="ea7f9-151">必需</span><span class="sxs-lookup"><span data-stu-id="ea7f9-151">Required</span></span> | <span data-ttu-id="ea7f9-152">说明</span><span class="sxs-lookup"><span data-stu-id="ea7f9-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="ea7f9-153">Id</span><span class="sxs-lookup"><span data-stu-id="ea7f9-153">ID</span></span>             | <span data-ttu-id="ea7f9-154">URL</span><span class="sxs-lookup"><span data-stu-id="ea7f9-154">URL</span></span>    | <span data-ttu-id="ea7f9-155">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-155">string</span></span> | <span data-ttu-id="ea7f9-156">是</span><span class="sxs-lookup"><span data-stu-id="ea7f9-156">yes</span></span>      | <span data-ttu-id="ea7f9-157">为其请求验证作用域键包标识符</span><span class="sxs-lookup"><span data-stu-id="ea7f9-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="ea7f9-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="ea7f9-158">VERSION</span></span>        | <span data-ttu-id="ea7f9-159">URL</span><span class="sxs-lookup"><span data-stu-id="ea7f9-159">URL</span></span>    | <span data-ttu-id="ea7f9-160">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-160">string</span></span> | <span data-ttu-id="ea7f9-161">否</span><span class="sxs-lookup"><span data-stu-id="ea7f9-161">no</span></span>       | <span data-ttu-id="ea7f9-162">包版本</span><span class="sxs-lookup"><span data-stu-id="ea7f9-162">The package version</span></span>
<span data-ttu-id="ea7f9-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ea7f9-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ea7f9-164">Header</span><span class="sxs-lookup"><span data-stu-id="ea7f9-164">Header</span></span> | <span data-ttu-id="ea7f9-165">字符串</span><span class="sxs-lookup"><span data-stu-id="ea7f9-165">string</span></span> | <span data-ttu-id="ea7f9-166">是</span><span class="sxs-lookup"><span data-stu-id="ea7f9-166">yes</span></span>      | <span data-ttu-id="ea7f9-167">例如，`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="ea7f9-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="ea7f9-168">此验证作用域 API 密钥将在某一天的时间后过期，或在首次使用准。</span><span class="sxs-lookup"><span data-stu-id="ea7f9-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="ea7f9-169">响应</span><span class="sxs-lookup"><span data-stu-id="ea7f9-169">Response</span></span>

<span data-ttu-id="ea7f9-170">状态代码</span><span class="sxs-lookup"><span data-stu-id="ea7f9-170">Status Code</span></span> | <span data-ttu-id="ea7f9-171">含义</span><span class="sxs-lookup"><span data-stu-id="ea7f9-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="ea7f9-172">200</span><span class="sxs-lookup"><span data-stu-id="ea7f9-172">200</span></span>         | <span data-ttu-id="ea7f9-173">API 密钥无效</span><span class="sxs-lookup"><span data-stu-id="ea7f9-173">The API key is valid</span></span>
<span data-ttu-id="ea7f9-174">403</span><span class="sxs-lookup"><span data-stu-id="ea7f9-174">403</span></span>         | <span data-ttu-id="ea7f9-175">API 密钥是无效或未授权，以对包推送</span><span class="sxs-lookup"><span data-stu-id="ea7f9-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="ea7f9-176">404</span><span class="sxs-lookup"><span data-stu-id="ea7f9-176">404</span></span>         | <span data-ttu-id="ea7f9-177">由包引用`ID`和`VERSION`（可选） 不存在</span><span class="sxs-lookup"><span data-stu-id="ea7f9-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
