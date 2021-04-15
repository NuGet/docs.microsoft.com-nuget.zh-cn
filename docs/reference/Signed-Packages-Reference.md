---
title: 已签名包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508795"
---
# <a name="signed-packages"></a><span data-ttu-id="647e3-103">已签名的包</span><span class="sxs-lookup"><span data-stu-id="647e3-103">Signed packages</span></span>

<span data-ttu-id="647e3-104">*NuGet 4.6.0 + 和 Visual Studio 2017 版本15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="647e3-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="647e3-105">NuGet 包可以包含一个数字签名，该签名提供针对篡改内容的保护。</span><span class="sxs-lookup"><span data-stu-id="647e3-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="647e3-106">此签名是通过 x.509 证书生成的，该证书还将授权校样添加到包的实际来源。</span><span class="sxs-lookup"><span data-stu-id="647e3-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="647e3-107">签名包提供了最强大的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="647e3-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="647e3-108">NuGet 签名有两种不同的类型：</span><span class="sxs-lookup"><span data-stu-id="647e3-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="647e3-109">**作者签名**。</span><span class="sxs-lookup"><span data-stu-id="647e3-109">**Author signature**.</span></span> <span data-ttu-id="647e3-110">作者签名可保证自作者对包进行签名后包未修改，无论包传送到哪个存储库或传输方法。</span><span class="sxs-lookup"><span data-stu-id="647e3-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="647e3-111">此外，创作签名包还为 nuget.org 发布管道提供额外的身份验证机制，因为必须提前注册签名证书。</span><span class="sxs-lookup"><span data-stu-id="647e3-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="647e3-112">有关详细信息，请参阅 [注册证书](#signature-requirements-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="647e3-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="647e3-113">**存储库签名**。</span><span class="sxs-lookup"><span data-stu-id="647e3-113">**Repository signature**.</span></span> <span data-ttu-id="647e3-114">存储库签名为存储库中的 **所有** 包提供完整性保证，无论它们是否为作者签名，即使这些包是从其签名的原始存储库以外的位置获取的。</span><span class="sxs-lookup"><span data-stu-id="647e3-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="647e3-115">有关创建作者签名包的详细信息，请参阅 [签署包](../create-packages/Sign-a-package.md) 和 [nuget 签名命令](../reference/cli-reference/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="647e3-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span> <span data-ttu-id="647e3-116">可以使用 [dotnet nuget 验证](/dotnet/core/tools/dotnet-nuget-verify) 或 [nuget 验证](../reference/cli-reference/cli-ref-verify.md) 命令验证包的签名。</span><span class="sxs-lookup"><span data-stu-id="647e3-116">You can verify packages' signatures using the [dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) or [nuget verify](../reference/cli-reference/cli-ref-verify.md) commands.</span></span>

> [!Important]
> <span data-ttu-id="647e3-117">目前仅支持 Windows 上的 nuget.exe 创作签名包。</span><span class="sxs-lookup"><span data-stu-id="647e3-117">Author signing packages is only supported by nuget.exe on Windows at this time.</span></span> <span data-ttu-id="647e3-118">但是，上传到 nuget.org 的所有包会自动存储存储库。</span><span class="sxs-lookup"><span data-stu-id="647e3-118">However, all packages uploaded to nuget.org are automatically repository signed.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="647e3-119">证书要求</span><span class="sxs-lookup"><span data-stu-id="647e3-119">Certificate requirements</span></span>

<span data-ttu-id="647e3-120">包签名需要一个代码签名证书，该证书是一种适用于 `id-kp-codeSigning` 目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] 的特殊类型证书。</span><span class="sxs-lookup"><span data-stu-id="647e3-120">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="647e3-121">此外，证书的 RSA 公钥长度必须为2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="647e3-121">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="647e3-122">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="647e3-122">Timestamp requirements</span></span>

<span data-ttu-id="647e3-123">签名包应包含 RFC 3161 时间戳，以确保签名有效期超出包签名证书的有效期。</span><span class="sxs-lookup"><span data-stu-id="647e3-123">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="647e3-124">用于签署时间戳的证书必须有效， `id-kp-timeStamping` 目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="647e3-124">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="647e3-125">此外，证书的 RSA 公钥长度必须为2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="647e3-125">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="647e3-126">其他技术详细信息可以在 " [包签名" 技术规范](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub) 中找到。</span><span class="sxs-lookup"><span data-stu-id="647e3-126">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="647e3-127">NuGet.org 上的签名要求</span><span class="sxs-lookup"><span data-stu-id="647e3-127">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="647e3-128">nuget.org 对接受签名的包有其他要求：</span><span class="sxs-lookup"><span data-stu-id="647e3-128">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="647e3-129">主签名必须是作者签名。</span><span class="sxs-lookup"><span data-stu-id="647e3-129">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="647e3-130">主签名必须有一个有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="647e3-130">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="647e3-131">作者签名及其时间戳签名的 x.509 证书：</span><span class="sxs-lookup"><span data-stu-id="647e3-131">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="647e3-132">必须具有 RSA 公钥2048或更高版本。</span><span class="sxs-lookup"><span data-stu-id="647e3-132">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="647e3-133">在 nuget.org 上的包验证时，必须在其每个当前 UTC 时间的有效期内。</span><span class="sxs-lookup"><span data-stu-id="647e3-133">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="647e3-134">必须链接到 Windows 上默认受信任的受信任根证书颁发机构。</span><span class="sxs-lookup"><span data-stu-id="647e3-134">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="647e3-135">拒绝了用自行颁发的证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="647e3-135">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="647e3-136">的用途必须有效：</span><span class="sxs-lookup"><span data-stu-id="647e3-136">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="647e3-137">作者签名证书必须有效，以便进行代码签名。</span><span class="sxs-lookup"><span data-stu-id="647e3-137">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="647e3-138">对于时间戳，时间戳证书必须有效。</span><span class="sxs-lookup"><span data-stu-id="647e3-138">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="647e3-139">不能在签名时撤销。</span><span class="sxs-lookup"><span data-stu-id="647e3-139">Must not be revoked at signing time.</span></span> <span data-ttu-id="647e3-140"> (这可能不会在提交时 knowable，因此 nuget.org 会定期复查列为吊销) 状态。</span><span class="sxs-lookup"><span data-stu-id="647e3-140">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="647e3-141">相关文章</span><span class="sxs-lookup"><span data-stu-id="647e3-141">Related articles</span></span>

- [<span data-ttu-id="647e3-142">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="647e3-142">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="647e3-143">使用 dotnet CLI 验证已签名的包</span><span class="sxs-lookup"><span data-stu-id="647e3-143">Verify signed packages using the dotnet CLI</span></span>](/dotnet/core/tools/dotnet-nuget-verify)
- [<span data-ttu-id="647e3-144">使用 nuget.exe验证已签名的包 </span><span class="sxs-lookup"><span data-stu-id="647e3-144">Verify signed packages using nuget.exe</span></span>](../reference/cli-reference/cli-ref-verify.md)
- [<span data-ttu-id="647e3-145">管理包信任边界</span><span class="sxs-lookup"><span data-stu-id="647e3-145">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
