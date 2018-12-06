---
title: 已签名的包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977506"
---
# <a name="signed-packages"></a><span data-ttu-id="773e7-103">签名的包</span><span class="sxs-lookup"><span data-stu-id="773e7-103">Signed packages</span></span>

<span data-ttu-id="773e7-104">*NuGet 4.6.0+ 和 Visual Studio 2017 版本 15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="773e7-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="773e7-105">NuGet 包可以包含的数字签名来提供保护以防止被篡改的内容。</span><span class="sxs-lookup"><span data-stu-id="773e7-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="773e7-106">此签名被生成的 X.509 证书，还添加到包的实际来源真实性概念。</span><span class="sxs-lookup"><span data-stu-id="773e7-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="773e7-107">已签名的软件包提供最强的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="773e7-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="773e7-108">有两种不同类型的 NuGet 签名：</span><span class="sxs-lookup"><span data-stu-id="773e7-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="773e7-109">**创作签名**。</span><span class="sxs-lookup"><span data-stu-id="773e7-109">**Author Signature**.</span></span> <span data-ttu-id="773e7-110">作者签名可保证包作者签名包，而不管从后未被修改的存储库或内容传输，递送包裹的方法。</span><span class="sxs-lookup"><span data-stu-id="773e7-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="773e7-111">此外，作者签署的程序包提供额外的身份验证机制向 nuget.org 发布管道，因为必须提前注册签名证书。</span><span class="sxs-lookup"><span data-stu-id="773e7-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="773e7-112">有关详细信息，请参阅[注册的证书](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="773e7-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="773e7-113">**存储库签名**。</span><span class="sxs-lookup"><span data-stu-id="773e7-113">**Repository Signature**.</span></span> <span data-ttu-id="773e7-114">存储库签名提供完整性保障**所有**包存储库中，无论它们是作者签名或不是，即使从不同的位置所在的原始存储库获取这些包签名。</span><span class="sxs-lookup"><span data-stu-id="773e7-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="773e7-115">创建作者签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)并[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="773e7-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="773e7-116">仅当在 Windows 上使用 nuget.exe，目前支持包签名。</span><span class="sxs-lookup"><span data-stu-id="773e7-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="773e7-117">仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名包的验证。</span><span class="sxs-lookup"><span data-stu-id="773e7-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="773e7-118">证书要求</span><span class="sxs-lookup"><span data-stu-id="773e7-118">Certificate requirements</span></span>

<span data-ttu-id="773e7-119">包签名需要代码签名证书，这是一种特殊类型的有效的证书`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="773e7-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="773e7-120">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="773e7-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="773e7-121">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="773e7-121">Timestamp requirements</span></span>

<span data-ttu-id="773e7-122">已签名的包应包含一个 RFC 3161 时间戳，以确保包签名证书的有效期超出签名有效性。</span><span class="sxs-lookup"><span data-stu-id="773e7-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="773e7-123">用于登录时间戳的证书必须为有效`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="773e7-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="773e7-124">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="773e7-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="773e7-125">其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="773e7-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="773e7-126">在 NuGet.org 上的签名要求</span><span class="sxs-lookup"><span data-stu-id="773e7-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="773e7-127">nuget.org 具有用于接受已签名的包的附加要求：</span><span class="sxs-lookup"><span data-stu-id="773e7-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="773e7-128">主签名必须是作者签名。</span><span class="sxs-lookup"><span data-stu-id="773e7-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="773e7-129">主签名必须具有一个有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="773e7-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="773e7-130">作者签名和其时间戳签名的 X.509 证书：</span><span class="sxs-lookup"><span data-stu-id="773e7-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="773e7-131">必须具有 RSA 公钥 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="773e7-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="773e7-132">必须在每次当前 UTC 时间的 nuget.org 上的包验证其有效期内。</span><span class="sxs-lookup"><span data-stu-id="773e7-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="773e7-133">必须链接到默认情况下，在 Windows 上受信任的受信任的根颁发机构。</span><span class="sxs-lookup"><span data-stu-id="773e7-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="773e7-134">使用自行颁发的证书签名的包将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="773e7-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="773e7-135">必须是有效的它的用途：</span><span class="sxs-lookup"><span data-stu-id="773e7-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="773e7-136">签名证书的作者必须对代码签名有效。</span><span class="sxs-lookup"><span data-stu-id="773e7-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="773e7-137">时间戳证书必须是有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="773e7-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="773e7-138">必须不会撤消在签名时。</span><span class="sxs-lookup"><span data-stu-id="773e7-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="773e7-139">（这可能不是可知在提交时，因此 nuget.org 定期重新检查吊销状态）。</span><span class="sxs-lookup"><span data-stu-id="773e7-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="773e7-140">相关文章</span><span class="sxs-lookup"><span data-stu-id="773e7-140">Related articles</span></span>

- [<span data-ttu-id="773e7-141">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="773e7-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="773e7-142">安装已签名的包</span><span class="sxs-lookup"><span data-stu-id="773e7-142">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
