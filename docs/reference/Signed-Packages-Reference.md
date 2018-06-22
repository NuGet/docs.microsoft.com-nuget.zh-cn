---
title: 已签名的包
description: NuGet 包签名要求。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449586"
---
# <a name="signed-packages"></a><span data-ttu-id="18335-103">已签名的软件包</span><span class="sxs-lookup"><span data-stu-id="18335-103">Signed packages</span></span>

<span data-ttu-id="18335-104">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="18335-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="18335-105">NuGet 包可以包含数字签名，它提供针对篡改的内容的保护。</span><span class="sxs-lookup"><span data-stu-id="18335-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="18335-106">此签名被生成一个 X.509 证书，还将真实性证明添加到包的实际来源。</span><span class="sxs-lookup"><span data-stu-id="18335-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="18335-107">已签名的软件包提供最高的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="18335-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="18335-108">作者签名可保证由于作者签名包，无论从包不被修改的存储库或什么传输传递包的方法。</span><span class="sxs-lookup"><span data-stu-id="18335-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="18335-109">此外，作者签名的包提供向 nuget.org 发布管道的额外的身份验证机制，因为签名的证书必须提前注册。</span><span class="sxs-lookup"><span data-stu-id="18335-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="18335-110">有关详细信息，请参阅[将证书注册](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="18335-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="18335-111">有关创建签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)和[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="18335-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="18335-112">仅在 Windows 上使用 nuget.exe 时，当前支持包签名。</span><span class="sxs-lookup"><span data-stu-id="18335-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="18335-113">仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名的软件包的验证。</span><span class="sxs-lookup"><span data-stu-id="18335-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="18335-114">证书要求</span><span class="sxs-lookup"><span data-stu-id="18335-114">Certificate requirements</span></span>

<span data-ttu-id="18335-115">包签名需要代码签名证书，这是一种特殊类型的证书有效`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="18335-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="18335-116">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="18335-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="18335-117">获取代码签名证书</span><span class="sxs-lookup"><span data-stu-id="18335-117">Get a code signing certificate</span></span>

<span data-ttu-id="18335-118">可能从类似的公共证书颁发机构那里获取有效证书：</span><span class="sxs-lookup"><span data-stu-id="18335-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="18335-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="18335-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="18335-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="18335-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="18335-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="18335-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="18335-122">全局登录</span><span class="sxs-lookup"><span data-stu-id="18335-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="18335-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="18335-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="18335-124">Certum</span><span class="sxs-lookup"><span data-stu-id="18335-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="18335-125">可以从获取由 Windows 受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="18335-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="18335-126">创建测试证书</span><span class="sxs-lookup"><span data-stu-id="18335-126">Create a test certificate</span></span>

<span data-ttu-id="18335-127">出于测试目的，可以使用自行颁发的证书。</span><span class="sxs-lookup"><span data-stu-id="18335-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="18335-128">若要创建自行颁发的证书，请使用[的 New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。</span><span class="sxs-lookup"><span data-stu-id="18335-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="18335-129">此命令创建当前用户的个人证书存储中可用的测试证书。</span><span class="sxs-lookup"><span data-stu-id="18335-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="18335-130">你可以通过运行打开证书存储区`certmgr.msc`以查看新创建的证书。</span><span class="sxs-lookup"><span data-stu-id="18335-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="18335-131">nuget.org 不接受包使用自行颁发的证书签名。</span><span class="sxs-lookup"><span data-stu-id="18335-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="18335-132">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="18335-132">Timestamp requirements</span></span>

<span data-ttu-id="18335-133">已签名的软件包应包括的 RFC 3161 时间戳，以确保签名有效性超出程序包签名证书的有效期。</span><span class="sxs-lookup"><span data-stu-id="18335-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="18335-134">用于签署时间戳证书必须是有效的`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="18335-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="18335-135">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="18335-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="18335-136">其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="18335-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="18335-137">在 nuget.org 上的签名要求</span><span class="sxs-lookup"><span data-stu-id="18335-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="18335-138">nuget.org 具有用于接受签名的包的附加要求：</span><span class="sxs-lookup"><span data-stu-id="18335-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="18335-139">主签名必须是作者签名。</span><span class="sxs-lookup"><span data-stu-id="18335-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="18335-140">主签名必须具有一个有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="18335-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="18335-141">作者签名和其时间戳签名的 X.509 证书：</span><span class="sxs-lookup"><span data-stu-id="18335-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="18335-142">必须具有 RSA 公钥 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="18335-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="18335-143">必须在每次当前 UTC 时间的 nuget.org 上的包验证其有效期内。</span><span class="sxs-lookup"><span data-stu-id="18335-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="18335-144">必须链接到默认情况下，在 Windows 上受信任的受信任的根颁发机构。</span><span class="sxs-lookup"><span data-stu-id="18335-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="18335-145">使用自行颁发的证书签名的包将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="18335-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="18335-146">为其目的，必须是有效的：</span><span class="sxs-lookup"><span data-stu-id="18335-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="18335-147">签名证书的作者必须是有效的代码签名。</span><span class="sxs-lookup"><span data-stu-id="18335-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="18335-148">时间戳证书必须是有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="18335-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="18335-149">不必须吊销在签名时。</span><span class="sxs-lookup"><span data-stu-id="18335-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="18335-150">（这可能不为可知在提交时间，因此 nuget.org 定期重新检查吊销状态）。</span><span class="sxs-lookup"><span data-stu-id="18335-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="18335-151">注册在 nuget.org 上的证书</span><span class="sxs-lookup"><span data-stu-id="18335-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="18335-152">若要提交已签名的包，您必须首先向 nuget.org 注册证书。你需要作为证书`.cer`二进制 DER 格式文件中的。</span><span class="sxs-lookup"><span data-stu-id="18335-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="18335-153">使用证书导出向导，可以将现有证书导出到的二进制 DER 格式。</span><span class="sxs-lookup"><span data-stu-id="18335-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![证书导出向导](media/CertificateExportWizard.png)

<span data-ttu-id="18335-155">高级的用户可以导出证书使用[导出证书 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="18335-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="18335-156">若要向 nuget.org 注册证书，请转到`Certificates`节`Account settings`页 （或组织的设置页中），然后选择`Register new certificate`。</span><span class="sxs-lookup"><span data-stu-id="18335-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![注册的证书](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="18335-158">一个用户可以提交多个证书和相同的证书可由多个用户进行注册。</span><span class="sxs-lookup"><span data-stu-id="18335-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="18335-159">一旦用户拥有一个证书注册，所有将来的软件包提交**必须**用的某个证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="18335-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="18335-160">用户还可以从帐户中删除已注册的证书。</span><span class="sxs-lookup"><span data-stu-id="18335-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="18335-161">一旦删除证书，使用该证书签名的包将在提交失败。</span><span class="sxs-lookup"><span data-stu-id="18335-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="18335-162">现有包不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="18335-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="18335-163">配置包签名要求</span><span class="sxs-lookup"><span data-stu-id="18335-163">Configure package signing requirements</span></span>

<span data-ttu-id="18335-164">如果你是包的唯一所有者，你将所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="18335-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="18335-165">即你可以使用任何已注册的证书进行签名的包和将提交到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="18335-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="18335-166">如果包包含多个所有者，默认情况下，可以使用"任何"所有者的证书对包进行签名。</span><span class="sxs-lookup"><span data-stu-id="18335-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="18335-167">作为包共同所有者，您可以重写"任何"与自己或任何其他共同所有者为所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="18335-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="18335-168">如果你将用户没有注册任何证书的所有者，则将允许未签名的包。</span><span class="sxs-lookup"><span data-stu-id="18335-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="18335-169">同样，如果"任何"选项选择其中一个所有者所有已注册的证书包和另一个所有者的默认设置不具有注册任何证书，然后 nuget.org 接受签名的包具有由其所有者之一注册签名或未签名包 （因为某个所有者不具有注册任何证书）。</span><span class="sxs-lookup"><span data-stu-id="18335-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![配置包签名者](media/configure-package-signers.png)
