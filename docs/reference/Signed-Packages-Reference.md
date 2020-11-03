---
title: 已签名包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238174"
---
# <a name="signed-packages"></a><span data-ttu-id="30bec-103">已签名的包</span><span class="sxs-lookup"><span data-stu-id="30bec-103">Signed packages</span></span>

<span data-ttu-id="30bec-104">*NuGet 4.6.0 + 和 Visual Studio 2017 版本15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="30bec-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="30bec-105">NuGet 包可以包含一个数字签名，该签名提供针对篡改内容的保护。</span><span class="sxs-lookup"><span data-stu-id="30bec-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="30bec-106">此签名是通过 x.509 证书生成的，该证书还将授权校样添加到包的实际来源。</span><span class="sxs-lookup"><span data-stu-id="30bec-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="30bec-107">签名包提供了最强大的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="30bec-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="30bec-108">NuGet 签名有两种不同的类型：</span><span class="sxs-lookup"><span data-stu-id="30bec-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="30bec-109">**作者签名** 。</span><span class="sxs-lookup"><span data-stu-id="30bec-109">**Author Signature** .</span></span> <span data-ttu-id="30bec-110">作者签名可保证自作者对包进行签名后包未修改，无论包传送到哪个存储库或传输方法。</span><span class="sxs-lookup"><span data-stu-id="30bec-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="30bec-111">此外，创作签名包还为 nuget.org 发布管道提供额外的身份验证机制，因为必须提前注册签名证书。</span><span class="sxs-lookup"><span data-stu-id="30bec-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="30bec-112">有关详细信息，请参阅 [注册证书](#signature-requirements-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="30bec-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="30bec-113">**存储库签名** 。</span><span class="sxs-lookup"><span data-stu-id="30bec-113">**Repository Signature** .</span></span> <span data-ttu-id="30bec-114">存储库签名为存储库中的 **所有** 包提供完整性保证，无论它们是否为作者签名，即使这些包是从其签名的原始存储库以外的位置获取的。</span><span class="sxs-lookup"><span data-stu-id="30bec-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="30bec-115">有关创建作者签名包的详细信息，请参阅 [签署包](../create-packages/Sign-a-package.md) 和 [nuget 签名命令](../reference/cli-reference/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="30bec-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="30bec-116">当前仅在使用 Windows 上的 nuget.exe 时才支持包签名。</span><span class="sxs-lookup"><span data-stu-id="30bec-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="30bec-117">[目前仅在使用 nuget.exe或 Windows 上的 Visual Studio 时，才支持验证已签名的包 ](../reference/cli-reference/cli-ref-verify.md) 。</span><span class="sxs-lookup"><span data-stu-id="30bec-117">[Verification of signed packages is currently supported only when using nuget.exe](../reference/cli-reference/cli-ref-verify.md) or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="30bec-118">证书要求</span><span class="sxs-lookup"><span data-stu-id="30bec-118">Certificate requirements</span></span>

<span data-ttu-id="30bec-119">包签名需要一个代码签名证书，该证书是一种适用于 `id-kp-codeSigning` 目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] 的特殊类型证书。</span><span class="sxs-lookup"><span data-stu-id="30bec-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="30bec-120">此外，证书的 RSA 公钥长度必须为2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="30bec-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="30bec-121">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="30bec-121">Timestamp requirements</span></span>

<span data-ttu-id="30bec-122">签名包应包含 RFC 3161 时间戳，以确保签名有效期超出包签名证书的有效期。</span><span class="sxs-lookup"><span data-stu-id="30bec-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="30bec-123">用于签署时间戳的证书必须有效， `id-kp-timeStamping` 目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="30bec-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="30bec-124">此外，证书的 RSA 公钥长度必须为2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="30bec-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="30bec-125">其他技术详细信息可以在 " [包签名" 技术规范](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub) 中找到。</span><span class="sxs-lookup"><span data-stu-id="30bec-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="30bec-126">NuGet.org 上的签名要求</span><span class="sxs-lookup"><span data-stu-id="30bec-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="30bec-127">nuget.org 对接受签名的包有其他要求：</span><span class="sxs-lookup"><span data-stu-id="30bec-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="30bec-128">主签名必须是作者签名。</span><span class="sxs-lookup"><span data-stu-id="30bec-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="30bec-129">主签名必须有一个有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="30bec-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="30bec-130">作者签名及其时间戳签名的 x.509 证书：</span><span class="sxs-lookup"><span data-stu-id="30bec-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="30bec-131">必须具有 RSA 公钥2048或更高版本。</span><span class="sxs-lookup"><span data-stu-id="30bec-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="30bec-132">在 nuget.org 上的包验证时，必须在其每个当前 UTC 时间的有效期内。</span><span class="sxs-lookup"><span data-stu-id="30bec-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="30bec-133">必须链接到 Windows 上默认受信任的受信任根证书颁发机构。</span><span class="sxs-lookup"><span data-stu-id="30bec-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="30bec-134">拒绝了用自行颁发的证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="30bec-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="30bec-135">的用途必须有效：</span><span class="sxs-lookup"><span data-stu-id="30bec-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="30bec-136">作者签名证书必须有效，以便进行代码签名。</span><span class="sxs-lookup"><span data-stu-id="30bec-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="30bec-137">对于时间戳，时间戳证书必须有效。</span><span class="sxs-lookup"><span data-stu-id="30bec-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="30bec-138">不能在签名时撤销。</span><span class="sxs-lookup"><span data-stu-id="30bec-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="30bec-139"> (这可能不会在提交时 knowable，因此 nuget.org 会定期复查列为吊销) 状态。</span><span class="sxs-lookup"><span data-stu-id="30bec-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="30bec-140">相关文章</span><span class="sxs-lookup"><span data-stu-id="30bec-140">Related articles</span></span>

- [<span data-ttu-id="30bec-141">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="30bec-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="30bec-142">管理包信任边界</span><span class="sxs-lookup"><span data-stu-id="30bec-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
