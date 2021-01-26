---
title: 存储库签名，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存储库签名资源允许客户端包源公布其存储库签名功能。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775328"
---
# <a name="repository-signatures"></a><span data-ttu-id="0e918-103">存储库签名</span><span class="sxs-lookup"><span data-stu-id="0e918-103">Repository signatures</span></span>

<span data-ttu-id="0e918-104">如果包源支持将存储库签名添加到已发布的包，客户端可能会确定包源使用的签名证书。</span><span class="sxs-lookup"><span data-stu-id="0e918-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="0e918-105">此资源可让客户端检测存储库签名包是否已被篡改或是否有意外的签名证书。</span><span class="sxs-lookup"><span data-stu-id="0e918-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="0e918-106">用于获取此存储库签名信息的资源是 `RepositorySignatures` 在 [服务索引](service-index.md)中找到的资源。</span><span class="sxs-lookup"><span data-stu-id="0e918-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0e918-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="0e918-107">Versioning</span></span>

<span data-ttu-id="0e918-108">使用以下 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="0e918-108">The following `@type` value is used:</span></span>

<span data-ttu-id="0e918-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="0e918-109">@type value</span></span>                | <span data-ttu-id="0e918-110">说明</span><span class="sxs-lookup"><span data-stu-id="0e918-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="0e918-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="0e918-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="0e918-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="0e918-112">The initial release</span></span>
<span data-ttu-id="0e918-113">RepositorySignatures/4.9。0</span><span class="sxs-lookup"><span data-stu-id="0e918-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="0e918-114">NuGet v 4.9 + 客户端支持</span><span class="sxs-lookup"><span data-stu-id="0e918-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="0e918-115">RepositorySignatures/5.0。0</span><span class="sxs-lookup"><span data-stu-id="0e918-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="0e918-116">允许启用 `allRepositorySigned` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="0e918-117">由 NuGet 版本 5.0 + 客户端支持</span><span class="sxs-lookup"><span data-stu-id="0e918-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="0e918-118">基 URL</span><span class="sxs-lookup"><span data-stu-id="0e918-118">Base URL</span></span>

<span data-ttu-id="0e918-119">以下 Api 的入口点 URL 是 `@id` 与上述资源值关联的属性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="0e918-120">本主题使用占位符 URL `{@id}` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="0e918-121">请注意，与其他资源不同， `{@id}` 需要通过 HTTPS 提供 URL。</span><span class="sxs-lookup"><span data-stu-id="0e918-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0e918-122">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0e918-122">HTTP methods</span></span>

<span data-ttu-id="0e918-123">存储库签名资源中的所有 Url 仅支持 HTTP 方法 `GET` 和 `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="0e918-124">存储库签名索引</span><span class="sxs-lookup"><span data-stu-id="0e918-124">Repository signatures index</span></span>

<span data-ttu-id="0e918-125">存储库签名索引包含两条信息：</span><span class="sxs-lookup"><span data-stu-id="0e918-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="0e918-126">源中找到的所有包是否均为此包源签名的存储库。</span><span class="sxs-lookup"><span data-stu-id="0e918-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="0e918-127">包源用于对包进行签名的证书列表。</span><span class="sxs-lookup"><span data-stu-id="0e918-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="0e918-128">在大多数情况下，证书列表仅会附加到。</span><span class="sxs-lookup"><span data-stu-id="0e918-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="0e918-129">当以前的签名证书已过期，并且包源需要使用新的签名证书开始时，将向列表中添加新证书。</span><span class="sxs-lookup"><span data-stu-id="0e918-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="0e918-130">如果从列表中删除了证书，则表示使用已删除签名证书创建的所有包签名都不应再被客户端视为有效。</span><span class="sxs-lookup"><span data-stu-id="0e918-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="0e918-131">在这种情况下，包签名 (，但不一定包) 无效。</span><span class="sxs-lookup"><span data-stu-id="0e918-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="0e918-132">客户端策略可能允许将包安装为无符号。</span><span class="sxs-lookup"><span data-stu-id="0e918-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="0e918-133">如果证书吊销 (例如密钥泄漏) ，则包源应对受影响证书签名的所有包进行重新签名。</span><span class="sxs-lookup"><span data-stu-id="0e918-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="0e918-134">此外，包源还应从签名证书列表中删除受影响的证书。</span><span class="sxs-lookup"><span data-stu-id="0e918-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="0e918-135">以下请求将获取存储库签名索引。</span><span class="sxs-lookup"><span data-stu-id="0e918-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="0e918-136">存储库签名索引是一个 JSON 文档，其中包含具有以下属性的对象：</span><span class="sxs-lookup"><span data-stu-id="0e918-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="0e918-137">名称</span><span class="sxs-lookup"><span data-stu-id="0e918-137">Name</span></span>                | <span data-ttu-id="0e918-138">类型</span><span class="sxs-lookup"><span data-stu-id="0e918-138">Type</span></span>             | <span data-ttu-id="0e918-139">必须</span><span class="sxs-lookup"><span data-stu-id="0e918-139">Required</span></span> | <span data-ttu-id="0e918-140">注释</span><span class="sxs-lookup"><span data-stu-id="0e918-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="0e918-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="0e918-141">allRepositorySigned</span></span> | <span data-ttu-id="0e918-142">boolean</span><span class="sxs-lookup"><span data-stu-id="0e918-142">boolean</span></span>          | <span data-ttu-id="0e918-143">是</span><span class="sxs-lookup"><span data-stu-id="0e918-143">yes</span></span>      | <span data-ttu-id="0e918-144">必须 `false` 在4.7.0 和4.9.0 资源上</span><span class="sxs-lookup"><span data-stu-id="0e918-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="0e918-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="0e918-145">signingCertificates</span></span> | <span data-ttu-id="0e918-146">对象数组</span><span class="sxs-lookup"><span data-stu-id="0e918-146">array of objects</span></span> | <span data-ttu-id="0e918-147">是</span><span class="sxs-lookup"><span data-stu-id="0e918-147">yes</span></span>      | 

<span data-ttu-id="0e918-148">`allRepositorySigned`如果包源包含某些没有存储库签名的包，则将该布尔值设置为 false。</span><span class="sxs-lookup"><span data-stu-id="0e918-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="0e918-149">如果布尔值设置为 true，则源上可用的所有包都必须具有存储库签名，该签名由中提到的一个签名证书生成 `signingCertificates` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="0e918-150">对于 `allRepositorySigned` 4.7.0 和4.9.0 资源，布尔值必须为 false。</span><span class="sxs-lookup"><span data-stu-id="0e918-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="0e918-151">NuGet 4.7 4.7、med-v 和 v 4.9 客户端无法从设置为 true 的源安装包 `allRepositorySigned` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="0e918-152">`signingCertificates`如果 `allRepositorySigned` 布尔值设置为 true，则在数组中应该有一个或多个签名证书。</span><span class="sxs-lookup"><span data-stu-id="0e918-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="0e918-153">如果数组为空且 `allRepositorySigned` 设置为 true，则源中的所有包都应视为无效，不过，客户端策略可能仍允许使用包。</span><span class="sxs-lookup"><span data-stu-id="0e918-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="0e918-154">此数组中的每个元素都是具有以下属性的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="0e918-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="0e918-155">名称</span><span class="sxs-lookup"><span data-stu-id="0e918-155">Name</span></span>         | <span data-ttu-id="0e918-156">类型</span><span class="sxs-lookup"><span data-stu-id="0e918-156">Type</span></span>   | <span data-ttu-id="0e918-157">必须</span><span class="sxs-lookup"><span data-stu-id="0e918-157">Required</span></span> | <span data-ttu-id="0e918-158">注释</span><span class="sxs-lookup"><span data-stu-id="0e918-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="0e918-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="0e918-159">contentUrl</span></span>   | <span data-ttu-id="0e918-160">string</span><span class="sxs-lookup"><span data-stu-id="0e918-160">string</span></span> | <span data-ttu-id="0e918-161">是</span><span class="sxs-lookup"><span data-stu-id="0e918-161">yes</span></span>      | <span data-ttu-id="0e918-162">DER 编码的公共证书的绝对 URL</span><span class="sxs-lookup"><span data-stu-id="0e918-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="0e918-163">指纹</span><span class="sxs-lookup"><span data-stu-id="0e918-163">fingerprints</span></span> | <span data-ttu-id="0e918-164">object</span><span class="sxs-lookup"><span data-stu-id="0e918-164">object</span></span> | <span data-ttu-id="0e918-165">是</span><span class="sxs-lookup"><span data-stu-id="0e918-165">yes</span></span>      |
<span data-ttu-id="0e918-166">subject</span><span class="sxs-lookup"><span data-stu-id="0e918-166">subject</span></span>      | <span data-ttu-id="0e918-167">string</span><span class="sxs-lookup"><span data-stu-id="0e918-167">string</span></span> | <span data-ttu-id="0e918-168">是</span><span class="sxs-lookup"><span data-stu-id="0e918-168">yes</span></span>      | <span data-ttu-id="0e918-169">证书中的使用者可分辨名称</span><span class="sxs-lookup"><span data-stu-id="0e918-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="0e918-170">颁发者</span><span class="sxs-lookup"><span data-stu-id="0e918-170">issuer</span></span>       | <span data-ttu-id="0e918-171">string</span><span class="sxs-lookup"><span data-stu-id="0e918-171">string</span></span> | <span data-ttu-id="0e918-172">是</span><span class="sxs-lookup"><span data-stu-id="0e918-172">yes</span></span>      | <span data-ttu-id="0e918-173">证书颁发者的可分辨名称</span><span class="sxs-lookup"><span data-stu-id="0e918-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="0e918-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="0e918-174">notBefore</span></span>    | <span data-ttu-id="0e918-175">string</span><span class="sxs-lookup"><span data-stu-id="0e918-175">string</span></span> | <span data-ttu-id="0e918-176">是</span><span class="sxs-lookup"><span data-stu-id="0e918-176">yes</span></span>      | <span data-ttu-id="0e918-177">证书有效期的开始时间戳</span><span class="sxs-lookup"><span data-stu-id="0e918-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="0e918-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="0e918-178">notAfter</span></span>     | <span data-ttu-id="0e918-179">string</span><span class="sxs-lookup"><span data-stu-id="0e918-179">string</span></span> | <span data-ttu-id="0e918-180">是</span><span class="sxs-lookup"><span data-stu-id="0e918-180">yes</span></span>      | <span data-ttu-id="0e918-181">证书有效期的结束时间戳</span><span class="sxs-lookup"><span data-stu-id="0e918-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="0e918-182">请注意， `contentUrl` 需要通过 HTTPS 进行服务。</span><span class="sxs-lookup"><span data-stu-id="0e918-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="0e918-183">此 URL 没有特定的 URL 模式，必须使用此存储库签名索引文档动态发现它。</span><span class="sxs-lookup"><span data-stu-id="0e918-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="0e918-184">此对象中 (除了) 之外的所有属性都 `contentUrl` 必须从找到的证书中名称可以 `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="0e918-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="0e918-185">提供这些名称可以属性是为了最大程度地减少往返行程。</span><span class="sxs-lookup"><span data-stu-id="0e918-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="0e918-186">`fingerprints` 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="0e918-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="0e918-187">名称</span><span class="sxs-lookup"><span data-stu-id="0e918-187">Name</span></span>                   | <span data-ttu-id="0e918-188">类型</span><span class="sxs-lookup"><span data-stu-id="0e918-188">Type</span></span>   | <span data-ttu-id="0e918-189">必须</span><span class="sxs-lookup"><span data-stu-id="0e918-189">Required</span></span> | <span data-ttu-id="0e918-190">注释</span><span class="sxs-lookup"><span data-stu-id="0e918-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="0e918-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="0e918-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="0e918-192">string</span><span class="sxs-lookup"><span data-stu-id="0e918-192">string</span></span> | <span data-ttu-id="0e918-193">是</span><span class="sxs-lookup"><span data-stu-id="0e918-193">yes</span></span>      | <span data-ttu-id="0e918-194">SHA-256 指纹</span><span class="sxs-lookup"><span data-stu-id="0e918-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="0e918-195">密钥名称 `2.16.840.1.101.3.4.2.1` 是 SHA-256 哈希算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="0e918-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="0e918-196">所有哈希值必须为哈希摘要的十六进制编码字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="0e918-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0e918-197">示例请求</span><span class="sxs-lookup"><span data-stu-id="0e918-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="0e918-198">示例响应</span><span class="sxs-lookup"><span data-stu-id="0e918-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
