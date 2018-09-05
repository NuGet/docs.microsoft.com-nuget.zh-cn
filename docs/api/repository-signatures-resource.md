---
title: 存储库签名，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存储库签名资源允许客户端包源地宣布其签名功能的存储库。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547976"
---
# <a name="repository-signatures"></a><span data-ttu-id="a2bbe-103">存储库签名</span><span class="sxs-lookup"><span data-stu-id="a2bbe-103">Repository signatures</span></span>

<span data-ttu-id="a2bbe-104">如果包源支持添加存储库发布的包签名，就可以确定所用的包源的签名证书的客户端。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="a2bbe-105">此资源允许客户端以检测包是否已签名的存储库已被篡改或包含意外的签名证书。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="a2bbe-106">此存储库签名信息中提取的使用的资源是`RepositorySignatures`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="a2bbe-107">NuGet.org 将启动发布`RepositorySignatures`资源在不久的将来。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="a2bbe-108">版本管理</span><span class="sxs-lookup"><span data-stu-id="a2bbe-108">Versioning</span></span>

<span data-ttu-id="a2bbe-109">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="a2bbe-109">The following `@type` value is used:</span></span>

<span data-ttu-id="a2bbe-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="a2bbe-110">@type value</span></span>                | <span data-ttu-id="a2bbe-111">说明</span><span class="sxs-lookup"><span data-stu-id="a2bbe-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="a2bbe-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="a2bbe-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="a2bbe-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="a2bbe-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="a2bbe-114">基 URL</span><span class="sxs-lookup"><span data-stu-id="a2bbe-114">Base URL</span></span>

<span data-ttu-id="a2bbe-115">以下 Api 的入口点 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a2bbe-116">本主题使用占位符 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="a2bbe-117">请注意，与其他资源不同`{@id}`URL，才能通过 HTTPS 提供服务。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a2bbe-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="a2bbe-118">HTTP methods</span></span>

<span data-ttu-id="a2bbe-119">在存储库签名资源支持的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="a2bbe-120">存储库签名索引</span><span class="sxs-lookup"><span data-stu-id="a2bbe-120">Repository signatures index</span></span>

<span data-ttu-id="a2bbe-121">存储库签名索引包含两条信息：</span><span class="sxs-lookup"><span data-stu-id="a2bbe-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="a2bbe-122">所有包源上可以都找到的是受此包的来源签署的存储库。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="a2bbe-123">包源来进行包所用证书的列表。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="a2bbe-124">在大多数情况下，证书的列表将只会追加到。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="a2bbe-125">以前的签名证书已过期，但包源需要开始使用新的签名证书时，会将新证书添加到列表。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="a2bbe-126">如果从列表中删除证书，这意味着，使用已删除的签名证书创建的所有包签名应不再被都视为有效客户端。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="a2bbe-127">在这种情况下，包的签名 （但不是一定是包） 是无效的。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="a2bbe-128">客户端策略可能会允许安装未签名包。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="a2bbe-129">在证书吊销 （例如密钥泄漏） 的情况下应将包的源文件重新签名由受影响的证书签名的所有包。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="a2bbe-130">此外，包源应从签名的证书列表中删除受影响的证书。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="a2bbe-131">以下请求获取存储库签名索引。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="a2bbe-132">存储库签名索引是包含具有以下属性的对象的 JSON 文档：</span><span class="sxs-lookup"><span data-stu-id="a2bbe-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="a2bbe-133">name</span><span class="sxs-lookup"><span data-stu-id="a2bbe-133">Name</span></span>                | <span data-ttu-id="a2bbe-134">类型</span><span class="sxs-lookup"><span data-stu-id="a2bbe-134">Type</span></span>             | <span data-ttu-id="a2bbe-135">必需</span><span class="sxs-lookup"><span data-stu-id="a2bbe-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="a2bbe-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="a2bbe-136">allRepositorySigned</span></span> | <span data-ttu-id="a2bbe-137">boolean</span><span class="sxs-lookup"><span data-stu-id="a2bbe-137">boolean</span></span>          | <span data-ttu-id="a2bbe-138">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-138">yes</span></span>
<span data-ttu-id="a2bbe-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="a2bbe-139">signingCertificates</span></span> | <span data-ttu-id="a2bbe-140">对象的数组</span><span class="sxs-lookup"><span data-stu-id="a2bbe-140">array of objects</span></span> | <span data-ttu-id="a2bbe-141">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-141">yes</span></span>

<span data-ttu-id="a2bbe-142">`allRepositorySigned`布尔值设置为 false，如果包源具有一些具有任何存储库的签名的包。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="a2bbe-143">如果布尔值设置为 true，可在上找到的所有包源必须由其中一个签名证书中所述的存储库签名`signingCertificates`。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="a2bbe-144">应在一个或多个签名证书`signingCertificates`数组如果`allRepositorySigned`布尔值设置为 true。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="a2bbe-145">如果数组为空并`allRepositorySigned`设置为 true，来自源的所有包应都视为无效，尽管客户端策略可能仍允许使用包。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="a2bbe-146">此数组中的每个元素均具有以下属性的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="a2bbe-147">name</span><span class="sxs-lookup"><span data-stu-id="a2bbe-147">Name</span></span>         | <span data-ttu-id="a2bbe-148">类型</span><span class="sxs-lookup"><span data-stu-id="a2bbe-148">Type</span></span>   | <span data-ttu-id="a2bbe-149">必需</span><span class="sxs-lookup"><span data-stu-id="a2bbe-149">Required</span></span> | <span data-ttu-id="a2bbe-150">说明</span><span class="sxs-lookup"><span data-stu-id="a2bbe-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="a2bbe-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="a2bbe-151">contentUrl</span></span>   | <span data-ttu-id="a2bbe-152">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-152">string</span></span> | <span data-ttu-id="a2bbe-153">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-153">yes</span></span>      | <span data-ttu-id="a2bbe-154">绝对 URL 的 DER 编码的公用证书</span><span class="sxs-lookup"><span data-stu-id="a2bbe-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="a2bbe-155">指纹</span><span class="sxs-lookup"><span data-stu-id="a2bbe-155">fingerprints</span></span> | <span data-ttu-id="a2bbe-156">object</span><span class="sxs-lookup"><span data-stu-id="a2bbe-156">object</span></span> | <span data-ttu-id="a2bbe-157">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-157">yes</span></span>      |
<span data-ttu-id="a2bbe-158">主题</span><span class="sxs-lookup"><span data-stu-id="a2bbe-158">subject</span></span>      | <span data-ttu-id="a2bbe-159">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-159">string</span></span> | <span data-ttu-id="a2bbe-160">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-160">yes</span></span>      | <span data-ttu-id="a2bbe-161">从证书使用者可分辨的名称</span><span class="sxs-lookup"><span data-stu-id="a2bbe-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="a2bbe-162">issuer</span><span class="sxs-lookup"><span data-stu-id="a2bbe-162">issuer</span></span>       | <span data-ttu-id="a2bbe-163">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-163">string</span></span> | <span data-ttu-id="a2bbe-164">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-164">yes</span></span>      | <span data-ttu-id="a2bbe-165">证书的颁发者的可分辨的名称</span><span class="sxs-lookup"><span data-stu-id="a2bbe-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="a2bbe-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="a2bbe-166">notBefore</span></span>    | <span data-ttu-id="a2bbe-167">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-167">string</span></span> | <span data-ttu-id="a2bbe-168">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-168">yes</span></span>      | <span data-ttu-id="a2bbe-169">证书的有效期的起始时间戳</span><span class="sxs-lookup"><span data-stu-id="a2bbe-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="a2bbe-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="a2bbe-170">notAfter</span></span>     | <span data-ttu-id="a2bbe-171">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-171">string</span></span> | <span data-ttu-id="a2bbe-172">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-172">yes</span></span>      | <span data-ttu-id="a2bbe-173">证书的有效期的结束时间戳</span><span class="sxs-lookup"><span data-stu-id="a2bbe-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="a2bbe-174">请注意，`contentUrl`需要通过 HTTPS 提供服务。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="a2bbe-175">此 URL 具有任何特定的 URL 模式，并且必须使用此存储库签名索引文档动态地发现。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="a2bbe-176">此对象中的所有属性 (除了`contentUrl`) 必须是从证书，请参阅派生`contentUrl`。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="a2bbe-177">为方便起见，尽量减少往返过程提供了这些派生的属性。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="a2bbe-178">`fingerprints`对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="a2bbe-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="a2bbe-179">name</span><span class="sxs-lookup"><span data-stu-id="a2bbe-179">Name</span></span>                   | <span data-ttu-id="a2bbe-180">类型</span><span class="sxs-lookup"><span data-stu-id="a2bbe-180">Type</span></span>   | <span data-ttu-id="a2bbe-181">必需</span><span class="sxs-lookup"><span data-stu-id="a2bbe-181">Required</span></span> | <span data-ttu-id="a2bbe-182">说明</span><span class="sxs-lookup"><span data-stu-id="a2bbe-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="a2bbe-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="a2bbe-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="a2bbe-184">字符串</span><span class="sxs-lookup"><span data-stu-id="a2bbe-184">string</span></span> | <span data-ttu-id="a2bbe-185">是</span><span class="sxs-lookup"><span data-stu-id="a2bbe-185">yes</span></span>      | <span data-ttu-id="a2bbe-186">SHA-256 指纹</span><span class="sxs-lookup"><span data-stu-id="a2bbe-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="a2bbe-187">密钥名称`2.16.840.1.101.3.4.2.1`是 SHA-256 哈希算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="a2bbe-188">所有哈希值必须为小写字符、 十六进制编码的字符串表示形式的哈希摘要。</span><span class="sxs-lookup"><span data-stu-id="a2bbe-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a2bbe-189">示例请求</span><span class="sxs-lookup"><span data-stu-id="a2bbe-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="a2bbe-190">示例响应</span><span class="sxs-lookup"><span data-stu-id="a2bbe-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
