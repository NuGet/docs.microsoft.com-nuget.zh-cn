---
title: "nuget.org 协议 |Microsoft 文档"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "不断发展与 NuGet 客户端交互 nuget.org 协议。"
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="00c36-103">nuget.org 协议</span><span class="sxs-lookup"><span data-stu-id="00c36-103">nuget.org Protocols</span></span>

<span data-ttu-id="00c36-104">若要与 nuget.org 进行交互，客户端需要遵循某些协议。</span><span class="sxs-lookup"><span data-stu-id="00c36-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="00c36-105">由于这些协议保留在发展，客户端必须标识调用特定 nuget.org Api 时，他们使用的协议版本。</span><span class="sxs-lookup"><span data-stu-id="00c36-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="00c36-106">这允许 nuget.org 的旧客户端的非换行方式引入的更改。</span><span class="sxs-lookup"><span data-stu-id="00c36-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="00c36-107">此页上介绍的 Api 是特定于 nuget.org 并且没有其他的 NuGet 服务器实现引入这些 Api 不期望。</span><span class="sxs-lookup"><span data-stu-id="00c36-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="00c36-108">有关 NuGet API 实现广泛整个 NuGet 生态系统的信息，请参阅[API 概述](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="00c36-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="00c36-109">本主题列出为各种协议和当到达存在。</span><span class="sxs-lookup"><span data-stu-id="00c36-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="00c36-110">所需的 NuGet 协议版本 4.1.0</span><span class="sxs-lookup"><span data-stu-id="00c36-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="00c36-111">4.1.0 协议指定的作用域验证密钥与除 nuget.org，若要验证针对 nuget.org 帐户之外的服务进行交互的用法。</span><span class="sxs-lookup"><span data-stu-id="00c36-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="00c36-112">请注意，`4.1.0`版本数是不透明的字符串，但不会支持此协议的官方 NuGet 客户端的第一个版本保持一致。</span><span class="sxs-lookup"><span data-stu-id="00c36-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="00c36-113">验证确保用户创建 API 密钥仅用于 nuget.org，并通过一次使用验证范围密钥处理该验证或从第三方服务的验证。</span><span class="sxs-lookup"><span data-stu-id="00c36-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="00c36-114">这些验证范围密钥可以用于验证包属于 nuget.org 上的特定用户 （帐户）。</span><span class="sxs-lookup"><span data-stu-id="00c36-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="00c36-115">客户端要求</span><span class="sxs-lookup"><span data-stu-id="00c36-115">Client requirement</span></span>

<span data-ttu-id="00c36-116">要求客户端传递以下标头，当他们开展 API 调用发布到**推送**nuget.org 的包：</span><span class="sxs-lookup"><span data-stu-id="00c36-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="00c36-117">请注意，预先存在`X-NuGet-Client-Version`标头具有相同的目的，但现已弃用和应不再使用。</span><span class="sxs-lookup"><span data-stu-id="00c36-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="00c36-118">**推送**协议本身中的文档所述[`PackagePublish`资源](package-publish-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="00c36-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="00c36-119">如果客户端与外部服务，需要验证是否属于特定用户 （帐户） 的包交互时，它应使用以下协议，并使用作用域的验证密钥和不从 nuget.org 的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="00c36-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="00c36-120">API 来请求作用域的验证密钥</span><span class="sxs-lookup"><span data-stu-id="00c36-120">API to request a verify-scope key</span></span>

<span data-ttu-id="00c36-121">此 API 用于获取 nuget.org 作者，以验证归他/她的包的作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="00c36-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="00c36-122">请求参数</span><span class="sxs-lookup"><span data-stu-id="00c36-122">Request parameters</span></span>

<span data-ttu-id="00c36-123">名称</span><span class="sxs-lookup"><span data-stu-id="00c36-123">Name</span></span>           | <span data-ttu-id="00c36-124">内</span><span class="sxs-lookup"><span data-stu-id="00c36-124">In</span></span>     | <span data-ttu-id="00c36-125">类型</span><span class="sxs-lookup"><span data-stu-id="00c36-125">Type</span></span>   | <span data-ttu-id="00c36-126">必需</span><span class="sxs-lookup"><span data-stu-id="00c36-126">Required</span></span> | <span data-ttu-id="00c36-127">说明</span><span class="sxs-lookup"><span data-stu-id="00c36-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="00c36-128">Id</span><span class="sxs-lookup"><span data-stu-id="00c36-128">ID</span></span>             | <span data-ttu-id="00c36-129">URL</span><span class="sxs-lookup"><span data-stu-id="00c36-129">URL</span></span>    | <span data-ttu-id="00c36-130">string</span><span class="sxs-lookup"><span data-stu-id="00c36-130">string</span></span> | <span data-ttu-id="00c36-131">是</span><span class="sxs-lookup"><span data-stu-id="00c36-131">yes</span></span>      | <span data-ttu-id="00c36-132">为其请求验证作用域键包 identidier</span><span class="sxs-lookup"><span data-stu-id="00c36-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="00c36-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="00c36-133">VERSION</span></span>        | <span data-ttu-id="00c36-134">URL</span><span class="sxs-lookup"><span data-stu-id="00c36-134">URL</span></span>    | <span data-ttu-id="00c36-135">string</span><span class="sxs-lookup"><span data-stu-id="00c36-135">string</span></span> | <span data-ttu-id="00c36-136">no</span><span class="sxs-lookup"><span data-stu-id="00c36-136">no</span></span>       | <span data-ttu-id="00c36-137">包版本</span><span class="sxs-lookup"><span data-stu-id="00c36-137">The package version</span></span>
<span data-ttu-id="00c36-138">X NuGet ApiKey</span><span class="sxs-lookup"><span data-stu-id="00c36-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="00c36-139">Header</span><span class="sxs-lookup"><span data-stu-id="00c36-139">Header</span></span> | <span data-ttu-id="00c36-140">string</span><span class="sxs-lookup"><span data-stu-id="00c36-140">string</span></span> | <span data-ttu-id="00c36-141">是</span><span class="sxs-lookup"><span data-stu-id="00c36-141">yes</span></span>      | <span data-ttu-id="00c36-142">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="00c36-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="00c36-143">响应</span><span class="sxs-lookup"><span data-stu-id="00c36-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="00c36-144">若要验证验证作用域键的 API</span><span class="sxs-lookup"><span data-stu-id="00c36-144">API to verify the verify scope key</span></span>

<span data-ttu-id="00c36-145">此 API 用于验证包归 nuget.org 作者作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="00c36-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="00c36-146">请求参数</span><span class="sxs-lookup"><span data-stu-id="00c36-146">Request parameters</span></span>

<span data-ttu-id="00c36-147">名称</span><span class="sxs-lookup"><span data-stu-id="00c36-147">Name</span></span>           | <span data-ttu-id="00c36-148">内</span><span class="sxs-lookup"><span data-stu-id="00c36-148">In</span></span>     | <span data-ttu-id="00c36-149">类型</span><span class="sxs-lookup"><span data-stu-id="00c36-149">Type</span></span>   | <span data-ttu-id="00c36-150">必需</span><span class="sxs-lookup"><span data-stu-id="00c36-150">Required</span></span> | <span data-ttu-id="00c36-151">说明</span><span class="sxs-lookup"><span data-stu-id="00c36-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="00c36-152">Id</span><span class="sxs-lookup"><span data-stu-id="00c36-152">ID</span></span>             | <span data-ttu-id="00c36-153">URL</span><span class="sxs-lookup"><span data-stu-id="00c36-153">URL</span></span>    | <span data-ttu-id="00c36-154">string</span><span class="sxs-lookup"><span data-stu-id="00c36-154">string</span></span> | <span data-ttu-id="00c36-155">是</span><span class="sxs-lookup"><span data-stu-id="00c36-155">yes</span></span>      | <span data-ttu-id="00c36-156">为其请求验证作用域键包标识符</span><span class="sxs-lookup"><span data-stu-id="00c36-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="00c36-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="00c36-157">VERSION</span></span>        | <span data-ttu-id="00c36-158">URL</span><span class="sxs-lookup"><span data-stu-id="00c36-158">URL</span></span>    | <span data-ttu-id="00c36-159">string</span><span class="sxs-lookup"><span data-stu-id="00c36-159">string</span></span> | <span data-ttu-id="00c36-160">no</span><span class="sxs-lookup"><span data-stu-id="00c36-160">no</span></span>       | <span data-ttu-id="00c36-161">包版本</span><span class="sxs-lookup"><span data-stu-id="00c36-161">The package version</span></span>
<span data-ttu-id="00c36-162">X NuGet ApiKey</span><span class="sxs-lookup"><span data-stu-id="00c36-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="00c36-163">Header</span><span class="sxs-lookup"><span data-stu-id="00c36-163">Header</span></span> | <span data-ttu-id="00c36-164">string</span><span class="sxs-lookup"><span data-stu-id="00c36-164">string</span></span> | <span data-ttu-id="00c36-165">是</span><span class="sxs-lookup"><span data-stu-id="00c36-165">yes</span></span>      | <span data-ttu-id="00c36-166">例如，`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="00c36-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="00c36-167">此验证作用域 API 密钥将在一天的时间之后过期或首次使用，无论哪个操作发生第一次。</span><span class="sxs-lookup"><span data-stu-id="00c36-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="00c36-168">响应</span><span class="sxs-lookup"><span data-stu-id="00c36-168">Response</span></span>

<span data-ttu-id="00c36-169">状态代码</span><span class="sxs-lookup"><span data-stu-id="00c36-169">Status Code</span></span> | <span data-ttu-id="00c36-170">含义</span><span class="sxs-lookup"><span data-stu-id="00c36-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="00c36-171">200</span><span class="sxs-lookup"><span data-stu-id="00c36-171">200</span></span>         | <span data-ttu-id="00c36-172">API 密钥是有效</span><span class="sxs-lookup"><span data-stu-id="00c36-172">The API key is valid</span></span>
<span data-ttu-id="00c36-173">403</span><span class="sxs-lookup"><span data-stu-id="00c36-173">403</span></span>         | <span data-ttu-id="00c36-174">API 密钥是无效或未授权推送对包</span><span class="sxs-lookup"><span data-stu-id="00c36-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="00c36-175">404</span><span class="sxs-lookup"><span data-stu-id="00c36-175">404</span></span>         | <span data-ttu-id="00c36-176">引用包`ID`和`VERSION`（可选） 不存在</span><span class="sxs-lookup"><span data-stu-id="00c36-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
