---
title: 存储库签名，NuGet API |Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 存储库签名资源允许客户端包源地宣布其签名功能的存储库。
keywords: NuGet API 存储库签名、 签名证书，nuget.org nuget.org 包签名
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020552"
---
# <a name="repository-signatures"></a><span data-ttu-id="ec155-104">存储库签名</span><span class="sxs-lookup"><span data-stu-id="ec155-104">Repository signatures</span></span>

<span data-ttu-id="ec155-105">如果包源支持添加存储库发布的包签名，就可以确定所用的包源的签名证书的客户端。</span><span class="sxs-lookup"><span data-stu-id="ec155-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="ec155-106">此资源允许客户端以检测包是否已签名的存储库已被篡改或包含意外的签名证书。</span><span class="sxs-lookup"><span data-stu-id="ec155-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="ec155-107">此存储库签名信息中提取的使用的资源是`RepositorySignatures`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="ec155-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="ec155-108">NuGet.org 将启动发布`RepositorySignatures`资源在不久的将来。</span><span class="sxs-lookup"><span data-stu-id="ec155-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="ec155-109">版本管理</span><span class="sxs-lookup"><span data-stu-id="ec155-109">Versioning</span></span>

<span data-ttu-id="ec155-110">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="ec155-110">The following `@type` value is used:</span></span>

<span data-ttu-id="ec155-111">@type 值</span><span class="sxs-lookup"><span data-stu-id="ec155-111">@type value</span></span>                | <span data-ttu-id="ec155-112">说明</span><span class="sxs-lookup"><span data-stu-id="ec155-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="ec155-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="ec155-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="ec155-114">初始版本</span><span class="sxs-lookup"><span data-stu-id="ec155-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="ec155-115">基 URL</span><span class="sxs-lookup"><span data-stu-id="ec155-115">Base URL</span></span>

<span data-ttu-id="ec155-116">以下 Api 的入口点 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="ec155-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="ec155-117">本主题使用占位符 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="ec155-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="ec155-118">请注意，与其他资源不同`{@id}`URL，才能通过 HTTPS 提供服务。</span><span class="sxs-lookup"><span data-stu-id="ec155-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ec155-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ec155-119">HTTP methods</span></span>

<span data-ttu-id="ec155-120">在存储库签名资源支持的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="ec155-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="ec155-121">存储库签名索引</span><span class="sxs-lookup"><span data-stu-id="ec155-121">Repository signatures index</span></span>

<span data-ttu-id="ec155-122">存储库签名索引包含两条信息：</span><span class="sxs-lookup"><span data-stu-id="ec155-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="ec155-123">所有包源上可以都找到的是受此包的来源签署的存储库。</span><span class="sxs-lookup"><span data-stu-id="ec155-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="ec155-124">包源来进行包所用证书的列表。</span><span class="sxs-lookup"><span data-stu-id="ec155-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="ec155-125">在大多数情况下，证书的列表将只会追加到。</span><span class="sxs-lookup"><span data-stu-id="ec155-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="ec155-126">以前的签名证书已过期，但包源需要开始使用新的签名证书时，会将新证书添加到列表。</span><span class="sxs-lookup"><span data-stu-id="ec155-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="ec155-127">如果从列表中删除证书，这意味着，使用已删除的签名证书创建的所有包签名应不再被都视为有效客户端。</span><span class="sxs-lookup"><span data-stu-id="ec155-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="ec155-128">在这种情况下，包的签名 （但不是一定是包） 是无效的。</span><span class="sxs-lookup"><span data-stu-id="ec155-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="ec155-129">客户端策略可能会允许安装未签名包。</span><span class="sxs-lookup"><span data-stu-id="ec155-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="ec155-130">在证书吊销 （例如密钥泄漏） 的情况下应将包的源文件重新签署所有受影响的证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="ec155-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="ec155-131">此外，包源应从签名的证书列表中删除受影响的证书。</span><span class="sxs-lookup"><span data-stu-id="ec155-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="ec155-132">以下请求获取存储库签名索引。</span><span class="sxs-lookup"><span data-stu-id="ec155-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="ec155-133">存储库签名索引是包含具有以下属性的对象的 JSON 文档：</span><span class="sxs-lookup"><span data-stu-id="ec155-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="ec155-134">name</span><span class="sxs-lookup"><span data-stu-id="ec155-134">Name</span></span>                | <span data-ttu-id="ec155-135">类型</span><span class="sxs-lookup"><span data-stu-id="ec155-135">Type</span></span>             | <span data-ttu-id="ec155-136">必需</span><span class="sxs-lookup"><span data-stu-id="ec155-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="ec155-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="ec155-137">allRepositorySigned</span></span> | <span data-ttu-id="ec155-138">boolean</span><span class="sxs-lookup"><span data-stu-id="ec155-138">boolean</span></span>          | <span data-ttu-id="ec155-139">是</span><span class="sxs-lookup"><span data-stu-id="ec155-139">yes</span></span>
<span data-ttu-id="ec155-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="ec155-140">signingCertificates</span></span> | <span data-ttu-id="ec155-141">对象的数组</span><span class="sxs-lookup"><span data-stu-id="ec155-141">array of objects</span></span> | <span data-ttu-id="ec155-142">是</span><span class="sxs-lookup"><span data-stu-id="ec155-142">yes</span></span>

<span data-ttu-id="ec155-143">`allRepositorySigned`布尔值设置为 false，如果包源具有一些具有任何存储库的签名的包。</span><span class="sxs-lookup"><span data-stu-id="ec155-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="ec155-144">如果布尔值设置为 true，可在上找到的所有包源必须由其中一个签名证书中所述的存储库签名`signingCertificates`。</span><span class="sxs-lookup"><span data-stu-id="ec155-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="ec155-145">应在一个或多个签名证书`signingCertificates`数组如果`allRepositorySigned`布尔值设置为 true。</span><span class="sxs-lookup"><span data-stu-id="ec155-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="ec155-146">如果数组为空并`allRepositorySigned`设置为 true，来自源的所有包应都视为无效，尽管客户端策略可能仍允许使用包。</span><span class="sxs-lookup"><span data-stu-id="ec155-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="ec155-147">此数组中的每个元素均具有以下属性的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="ec155-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="ec155-148">name</span><span class="sxs-lookup"><span data-stu-id="ec155-148">Name</span></span>         | <span data-ttu-id="ec155-149">类型</span><span class="sxs-lookup"><span data-stu-id="ec155-149">Type</span></span>   | <span data-ttu-id="ec155-150">必需</span><span class="sxs-lookup"><span data-stu-id="ec155-150">Required</span></span> | <span data-ttu-id="ec155-151">说明</span><span class="sxs-lookup"><span data-stu-id="ec155-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="ec155-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="ec155-152">contentUrl</span></span>   | <span data-ttu-id="ec155-153">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-153">string</span></span> | <span data-ttu-id="ec155-154">是</span><span class="sxs-lookup"><span data-stu-id="ec155-154">yes</span></span>      | <span data-ttu-id="ec155-155">绝对 URL 的 DER 编码的公用证书</span><span class="sxs-lookup"><span data-stu-id="ec155-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="ec155-156">指纹</span><span class="sxs-lookup"><span data-stu-id="ec155-156">fingerprints</span></span> | <span data-ttu-id="ec155-157">object</span><span class="sxs-lookup"><span data-stu-id="ec155-157">object</span></span> | <span data-ttu-id="ec155-158">是</span><span class="sxs-lookup"><span data-stu-id="ec155-158">yes</span></span>      |
<span data-ttu-id="ec155-159">主题</span><span class="sxs-lookup"><span data-stu-id="ec155-159">subject</span></span>      | <span data-ttu-id="ec155-160">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-160">string</span></span> | <span data-ttu-id="ec155-161">是</span><span class="sxs-lookup"><span data-stu-id="ec155-161">yes</span></span>      | <span data-ttu-id="ec155-162">从证书使用者可分辨的名称</span><span class="sxs-lookup"><span data-stu-id="ec155-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="ec155-163">issuer</span><span class="sxs-lookup"><span data-stu-id="ec155-163">issuer</span></span>       | <span data-ttu-id="ec155-164">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-164">string</span></span> | <span data-ttu-id="ec155-165">是</span><span class="sxs-lookup"><span data-stu-id="ec155-165">yes</span></span>      | <span data-ttu-id="ec155-166">证书的颁发者的可分辨的名称</span><span class="sxs-lookup"><span data-stu-id="ec155-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="ec155-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="ec155-167">notBefore</span></span>    | <span data-ttu-id="ec155-168">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-168">string</span></span> | <span data-ttu-id="ec155-169">是</span><span class="sxs-lookup"><span data-stu-id="ec155-169">yes</span></span>      | <span data-ttu-id="ec155-170">证书的有效期的起始时间戳</span><span class="sxs-lookup"><span data-stu-id="ec155-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="ec155-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="ec155-171">notAfter</span></span>     | <span data-ttu-id="ec155-172">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-172">string</span></span> | <span data-ttu-id="ec155-173">是</span><span class="sxs-lookup"><span data-stu-id="ec155-173">yes</span></span>      | <span data-ttu-id="ec155-174">证书的有效期的结束时间戳</span><span class="sxs-lookup"><span data-stu-id="ec155-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="ec155-175">请注意，`contentUrl`需要通过 HTTPS 提供服务。</span><span class="sxs-lookup"><span data-stu-id="ec155-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="ec155-176">此 URL 具有任何特定的 URL 模式，并且必须使用此存储库签名索引文档动态地发现。</span><span class="sxs-lookup"><span data-stu-id="ec155-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="ec155-177">此对象中的所有属性 (除了`contentUrl`) 必须是从证书，请参阅派生`contentUrl`。</span><span class="sxs-lookup"><span data-stu-id="ec155-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="ec155-178">为方便起见，尽量减少往返过程提供了这些派生的属性。</span><span class="sxs-lookup"><span data-stu-id="ec155-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="ec155-179">`fingerprints`对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="ec155-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="ec155-180">name</span><span class="sxs-lookup"><span data-stu-id="ec155-180">Name</span></span>                   | <span data-ttu-id="ec155-181">类型</span><span class="sxs-lookup"><span data-stu-id="ec155-181">Type</span></span>   | <span data-ttu-id="ec155-182">必需</span><span class="sxs-lookup"><span data-stu-id="ec155-182">Required</span></span> | <span data-ttu-id="ec155-183">说明</span><span class="sxs-lookup"><span data-stu-id="ec155-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="ec155-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="ec155-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="ec155-185">字符串</span><span class="sxs-lookup"><span data-stu-id="ec155-185">string</span></span> | <span data-ttu-id="ec155-186">是</span><span class="sxs-lookup"><span data-stu-id="ec155-186">yes</span></span>      | <span data-ttu-id="ec155-187">SHA-256 指纹</span><span class="sxs-lookup"><span data-stu-id="ec155-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="ec155-188">密钥名称`2.16.840.1.101.3.4.2.1`是 SHA-256 哈希算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="ec155-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="ec155-189">所有哈希值必须为小写字符、 十六进制编码的字符串表示形式的哈希摘要。</span><span class="sxs-lookup"><span data-stu-id="ec155-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ec155-190">示例请求</span><span class="sxs-lookup"><span data-stu-id="ec155-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="ec155-191">示例响应</span><span class="sxs-lookup"><span data-stu-id="ec155-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
