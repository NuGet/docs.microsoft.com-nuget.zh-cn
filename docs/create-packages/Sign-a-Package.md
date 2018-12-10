---
title: 对 NuGet 包进行签名
description: 介绍如何使用已签名包来启用内容完整性验证。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977558"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="aeab0-103">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="aeab0-103">Signing NuGet Packages</span></span>

<span data-ttu-id="aeab0-104">已签名的包允许进行内容完整性验证检查，可有效防止内容被篡改。</span><span class="sxs-lookup"><span data-stu-id="aeab0-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="aeab0-105">此外，包的签名还可作为包的实际来源的单一可信来源，增强了对包使用者的身份验证。</span><span class="sxs-lookup"><span data-stu-id="aeab0-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="aeab0-106">本指南假定你已[创建一个包](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="aeab0-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="aeab0-107">获取代码签名证书</span><span class="sxs-lookup"><span data-stu-id="aeab0-107">Get a code signing certificate</span></span>

<span data-ttu-id="aeab0-108">可从以下公共证书颁发机构获取有效的证书：[Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 等。可从 [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners) 获取 Windows 信任的证书颁发机构完整列表。</span><span class="sxs-lookup"><span data-stu-id="aeab0-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="aeab0-109">可使用自颁发证书进行测试。</span><span class="sxs-lookup"><span data-stu-id="aeab0-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="aeab0-110">但 NuGet.org 不接受使用自颁发证书签名的包。详细了解如何[创建测试证书](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="aeab0-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="aeab0-111">导出证书文件</span><span class="sxs-lookup"><span data-stu-id="aeab0-111">Export the certificate file</span></span>

* <span data-ttu-id="aeab0-112">使用证书导出向导，可将现有的证书导出为二进制 DER 格式。</span><span class="sxs-lookup"><span data-stu-id="aeab0-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![证书导出向导](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="aeab0-114">此外，还可使用 [Export-Certificate PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)导出证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="aeab0-115">对包进行签名</span><span class="sxs-lookup"><span data-stu-id="aeab0-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="aeab0-116">需要 nuget.exe 4.6.0 或更高版本</span><span class="sxs-lookup"><span data-stu-id="aeab0-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="aeab0-117">可使用 [nuget sign](../tools/cli-ref-sign.md) 对包进行签名：</span><span class="sxs-lookup"><span data-stu-id="aeab0-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="aeab0-118">可使用证书存储中可用的证书或使用来自文件的证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="aeab0-119">请参阅 CLI 参考，了解 [nuget sign](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="aeab0-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="aeab0-120">已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。</span><span class="sxs-lookup"><span data-stu-id="aeab0-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="aeab0-121">否则签名操作将引发一个[警告](../reference/errors-and-warnings/NU3002.md)。</span><span class="sxs-lookup"><span data-stu-id="aeab0-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="aeab0-122">使用 [nuget verify](../tools/cli-ref-verify.md) 可查看给定包的签名详细信息。</span><span class="sxs-lookup"><span data-stu-id="aeab0-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="aeab0-123">使用 NuGet.org 注册证书</span><span class="sxs-lookup"><span data-stu-id="aeab0-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="aeab0-124">要发布已签名的包，必须先使用 NuGet.org 注册证书。需要将证书设置为二进制 DER 格式的 `.cer` 文件。</span><span class="sxs-lookup"><span data-stu-id="aeab0-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="aeab0-125">[登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="aeab0-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="aeab0-126">转到 `Account settings`（如果希望使用组织帐户注册证书，则转到 `Manage Organization` >  `Edit Organziation`）。</span><span class="sxs-lookup"><span data-stu-id="aeab0-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="aeab0-127">展开 `Certificates` 部分，并选择 `Register new`。</span><span class="sxs-lookup"><span data-stu-id="aeab0-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="aeab0-128">浏览并选择前面导出的证书文件。</span><span class="sxs-lookup"><span data-stu-id="aeab0-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="aeab0-129">![已注册的证书](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="aeab0-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="aeab0-130">**注意**</span><span class="sxs-lookup"><span data-stu-id="aeab0-130">**Note**</span></span>
* <span data-ttu-id="aeab0-131">一个用户可以提交多个证书并且多个用户可以注册同一个证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="aeab0-132">用户注册证书之后，所有未来的包提交都必须使用其中一个证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="aeab0-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="aeab0-133">请参阅[管理 NuGet.org 上的包的签名要求](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="aeab0-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="aeab0-134">用户还可以从帐户中删除已注册的证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="aeab0-135">删除证书后，使用该证书签名的新包将在提交时失败。</span><span class="sxs-lookup"><span data-stu-id="aeab0-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="aeab0-136">现有包不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="aeab0-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="aeab0-137">发布包</span><span class="sxs-lookup"><span data-stu-id="aeab0-137">Publish the package</span></span>

<span data-ttu-id="aeab0-138">现在即可将包发布到 NuGet.org。请参阅[发布包](Publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="aeab0-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="aeab0-139">创建测试证书</span><span class="sxs-lookup"><span data-stu-id="aeab0-139">Create a test certificate</span></span>

<span data-ttu-id="aeab0-140">可使用自颁发证书进行测试。</span><span class="sxs-lookup"><span data-stu-id="aeab0-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="aeab0-141">要创建自颁发证书，请使用 [New-SelfSignedCertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。</span><span class="sxs-lookup"><span data-stu-id="aeab0-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="aeab0-142">此命令将在当前用户的个人证书存储中创建可用的测试证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="aeab0-143">可通过运行 `certmgr.msc` 打开证书存储，查看新创建的证书。</span><span class="sxs-lookup"><span data-stu-id="aeab0-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="aeab0-144">NuGet.org 不接受使用自颁发证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="aeab0-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="aeab0-145">管理 NuGet.org 上的包的签名要求</span><span class="sxs-lookup"><span data-stu-id="aeab0-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="aeab0-146">[登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="aeab0-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="aeab0-147">转到 `Manage Packages`  
   ![配置包签名程序](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="aeab0-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="aeab0-148">如果你是包的唯一所有者，那么你就是所要求的签名者，即你可使用任何已注册的证书对包进行签名，然后将其发布到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="aeab0-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="aeab0-149">如果包具有多个所有者，默认情况下，可以使用“任何”所有者的证书对包进行签名。</span><span class="sxs-lookup"><span data-stu-id="aeab0-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="aeab0-150">作为包的共同所有者，你可将“任何”重写为你自己或任何其他共同所有者，作为所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="aeab0-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="aeab0-151">如果你让没有注册任何证书的人成为所有者，则将允许未签名的包。</span><span class="sxs-lookup"><span data-stu-id="aeab0-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="aeab0-152">同样，如果已选中某个包的默认“任何”选项，在该包中，有一个所有者已注册证书，而另一个所有者未注册任何证书，则 NuGet.org 接受已签名的包（由其中一个所有者注册签名）或接受未签名的包（因为其中一个所有者未注册任何证书）。</span><span class="sxs-lookup"><span data-stu-id="aeab0-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="aeab0-153">相关文章</span><span class="sxs-lookup"><span data-stu-id="aeab0-153">Related articles</span></span>

- [<span data-ttu-id="aeab0-154">安装已签名的包</span><span class="sxs-lookup"><span data-stu-id="aeab0-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="aeab0-155">签名包引用</span><span class="sxs-lookup"><span data-stu-id="aeab0-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
