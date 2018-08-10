---
title: 已签名的包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020504"
---
# <a name="signed-packages"></a><span data-ttu-id="f1f54-103">签名的包</span><span class="sxs-lookup"><span data-stu-id="f1f54-103">Signed packages</span></span>

<span data-ttu-id="f1f54-104">*NuGet 4.6.0+ 和 Visual Studio 2017 版本 15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="f1f54-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="f1f54-105">NuGet 包可以包含的数字签名来提供保护以防止被篡改的内容。</span><span class="sxs-lookup"><span data-stu-id="f1f54-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="f1f54-106">此签名被生成的 X.509 证书，还添加到包的实际来源真实性概念。</span><span class="sxs-lookup"><span data-stu-id="f1f54-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="f1f54-107">已签名的软件包提供最强的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="f1f54-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="f1f54-108">有两种不同类型的 NuGet 签名：</span><span class="sxs-lookup"><span data-stu-id="f1f54-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="f1f54-109">**创作签名**。</span><span class="sxs-lookup"><span data-stu-id="f1f54-109">**Author Signature**.</span></span> <span data-ttu-id="f1f54-110">作者签名可保证包作者签名包，而不管从后未被修改的存储库或内容传输，递送包裹的方法。</span><span class="sxs-lookup"><span data-stu-id="f1f54-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="f1f54-111">此外，作者签署的程序包提供额外的身份验证机制向 nuget.org 发布管道，因为必须提前注册签名证书。</span><span class="sxs-lookup"><span data-stu-id="f1f54-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="f1f54-112">有关详细信息，请参阅[注册的证书](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="f1f54-113">**存储库签名**。</span><span class="sxs-lookup"><span data-stu-id="f1f54-113">**Repository Signature**.</span></span> <span data-ttu-id="f1f54-114">存储库签名提供完整性保障**所有**包存储库中，无论它们是作者签名或不是，即使从不同的位置所在的原始存储库获取这些包签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="f1f54-115">创建作者签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)并[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="f1f54-116">仅当在 Windows 上使用 nuget.exe，目前支持包签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="f1f54-117">仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名包的验证。</span><span class="sxs-lookup"><span data-stu-id="f1f54-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="f1f54-118">证书要求</span><span class="sxs-lookup"><span data-stu-id="f1f54-118">Certificate requirements</span></span>

<span data-ttu-id="f1f54-119">包签名需要代码签名证书，这是一种特殊类型的有效的证书`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="f1f54-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="f1f54-120">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f1f54-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="f1f54-121">获取代码签名证书</span><span class="sxs-lookup"><span data-stu-id="f1f54-121">Get a code signing certificate</span></span>

<span data-ttu-id="f1f54-122">从公共证书颁发机构等都可以获得有效的证书：</span><span class="sxs-lookup"><span data-stu-id="f1f54-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="f1f54-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="f1f54-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="f1f54-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="f1f54-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="f1f54-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="f1f54-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="f1f54-126">全局符号</span><span class="sxs-lookup"><span data-stu-id="f1f54-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="f1f54-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="f1f54-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="f1f54-128">Certum</span><span class="sxs-lookup"><span data-stu-id="f1f54-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="f1f54-129">可以从 Windows 的受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="f1f54-130">创建测试证书</span><span class="sxs-lookup"><span data-stu-id="f1f54-130">Create a test certificate</span></span>

<span data-ttu-id="f1f54-131">出于测试目的，可以使用自行颁发的证书。</span><span class="sxs-lookup"><span data-stu-id="f1f54-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f1f54-132">若要创建自行颁发的证书，请使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="f1f54-133">此命令在当前用户的个人证书存储区中创建的测试证书可用。</span><span class="sxs-lookup"><span data-stu-id="f1f54-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="f1f54-134">可以通过运行打开证书存储区`certmgr.msc`若要查看新创建的证书。</span><span class="sxs-lookup"><span data-stu-id="f1f54-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="f1f54-135">nuget.org 不接受包使用自行颁发的证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="f1f54-136">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="f1f54-136">Timestamp requirements</span></span>

<span data-ttu-id="f1f54-137">已签名的包应包含一个 RFC 3161 时间戳，以确保包签名证书的有效期超出签名有效性。</span><span class="sxs-lookup"><span data-stu-id="f1f54-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="f1f54-138">用于登录时间戳的证书必须为有效`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="f1f54-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="f1f54-139">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f1f54-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="f1f54-140">其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="f1f54-141">在 nuget.org 上的签名要求</span><span class="sxs-lookup"><span data-stu-id="f1f54-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="f1f54-142">nuget.org 具有用于接受已签名的包的附加要求：</span><span class="sxs-lookup"><span data-stu-id="f1f54-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="f1f54-143">主签名必须是作者签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="f1f54-144">主签名必须具有一个有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="f1f54-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="f1f54-145">作者签名和其时间戳签名的 X.509 证书：</span><span class="sxs-lookup"><span data-stu-id="f1f54-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="f1f54-146">必须具有 RSA 公钥 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f1f54-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="f1f54-147">必须在每次当前 UTC 时间的 nuget.org 上的包验证其有效期内。</span><span class="sxs-lookup"><span data-stu-id="f1f54-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="f1f54-148">必须链接到默认情况下，在 Windows 上受信任的受信任的根颁发机构。</span><span class="sxs-lookup"><span data-stu-id="f1f54-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="f1f54-149">使用自行颁发的证书签名的包将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="f1f54-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="f1f54-150">必须是有效的它的用途：</span><span class="sxs-lookup"><span data-stu-id="f1f54-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="f1f54-151">签名证书的作者必须对代码签名有效。</span><span class="sxs-lookup"><span data-stu-id="f1f54-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="f1f54-152">时间戳证书必须是有效的时间戳。</span><span class="sxs-lookup"><span data-stu-id="f1f54-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="f1f54-153">必须不会撤消在签名时。</span><span class="sxs-lookup"><span data-stu-id="f1f54-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="f1f54-154">（这可能不是可知在提交时，因此 nuget.org 定期重新检查吊销状态）。</span><span class="sxs-lookup"><span data-stu-id="f1f54-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="f1f54-155">在 nuget.org 上注册证书</span><span class="sxs-lookup"><span data-stu-id="f1f54-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="f1f54-156">若要提交已签名的包，必须先使用 nuget.org 注册证书。你需要为证书`.cer`二进制 DER 格式文件中的。</span><span class="sxs-lookup"><span data-stu-id="f1f54-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="f1f54-157">使用证书导出向导，可以将现有的证书导出到二进制 DER 格式。</span><span class="sxs-lookup"><span data-stu-id="f1f54-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![证书导出向导](media/CertificateExportWizard.png)

<span data-ttu-id="f1f54-159">高级的用户可以导出证书使用[导出证书的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="f1f54-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="f1f54-160">若要向 nuget.org 注册证书，请转到`Certificates`部分`Account settings`页 （或组织的设置页），然后选择`Register new certificate`。</span><span class="sxs-lookup"><span data-stu-id="f1f54-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![已注册的证书](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="f1f54-162">一个用户可以提交多个用户可以注册多个证书和相同的证书。</span><span class="sxs-lookup"><span data-stu-id="f1f54-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="f1f54-163">一旦用户拥有一个证书注册，未来的程序包的所有提交**必须**使用其中一个证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="f1f54-164">用户还可以从帐户中删除已注册的证书。</span><span class="sxs-lookup"><span data-stu-id="f1f54-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="f1f54-165">删除证书后，使用该证书签名的包会在提交失败。</span><span class="sxs-lookup"><span data-stu-id="f1f54-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="f1f54-166">现有的包不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="f1f54-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="f1f54-167">配置包签名要求</span><span class="sxs-lookup"><span data-stu-id="f1f54-167">Configure package signing requirements</span></span>

<span data-ttu-id="f1f54-168">如果你是包的唯一所有者，则可以所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="f1f54-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="f1f54-169">也就是说，您可以使用任何已注册的证书签署应用程序包并将提交到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="f1f54-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="f1f54-170">如果包包含多个所有者，默认情况下，可以使用"任何"所有者的证书对程序包进行签名。</span><span class="sxs-lookup"><span data-stu-id="f1f54-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="f1f54-171">作为包的共同所有者，你可以重写"任何"与自己或任何其他共同所有者为所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="f1f54-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="f1f54-172">如果没有注册任何证书的所有者，则将允许未签名的包。</span><span class="sxs-lookup"><span data-stu-id="f1f54-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="f1f54-173">同样，如果"任何"选项选择其中一个所有者具有注册证书的包和另一个所有者的默认值不具有注册任何证书，然后 nuget.org 接受已签名的包具有签名由其所有者之一注册或未签名包 （因为某个所有者没有注册任何证书）。</span><span class="sxs-lookup"><span data-stu-id="f1f54-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![配置包签名者](media/configure-package-signers.png)
