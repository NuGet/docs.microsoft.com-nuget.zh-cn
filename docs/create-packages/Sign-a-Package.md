---
title: 对 NuGet 包进行签名
description: 介绍如何使用已签名包来启用内容完整性验证。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428617"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="75eca-103">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="75eca-103">Signing NuGet Packages</span></span>

<span data-ttu-id="75eca-104">已签名的包允许进行内容完整性验证检查，可有效防止内容被篡改。</span><span class="sxs-lookup"><span data-stu-id="75eca-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="75eca-105">此外，包的签名还可作为包的实际来源的单一可信来源，增强了对包使用者的身份验证。</span><span class="sxs-lookup"><span data-stu-id="75eca-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="75eca-106">本指南假定你已[创建一个包](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="75eca-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="75eca-107">获取代码签名证书</span><span class="sxs-lookup"><span data-stu-id="75eca-107">Get a code signing certificate</span></span>

<span data-ttu-id="75eca-108">可从以下公共证书颁发机构获取有效的证书：[Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 等。可从 [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners) 获取 Windows 信任的证书颁发机构完整列表。</span><span class="sxs-lookup"><span data-stu-id="75eca-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="75eca-109">可使用自颁发证书进行测试。</span><span class="sxs-lookup"><span data-stu-id="75eca-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="75eca-110">但 NuGet.org 不接受使用自颁发证书签名的包。详细了解如何[创建测试证书](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="75eca-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="75eca-111">导出证书文件</span><span class="sxs-lookup"><span data-stu-id="75eca-111">Export the certificate file</span></span>

* <span data-ttu-id="75eca-112">使用证书导出向导，可将现有的证书导出为二进制 DER 格式。</span><span class="sxs-lookup"><span data-stu-id="75eca-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![证书导出向导](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="75eca-114">此外，还可使用 [Export-Certificate PowerShell 命令](/powershell/module/pkiclient/export-certificate)导出证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="75eca-115">对包进行签名</span><span class="sxs-lookup"><span data-stu-id="75eca-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="75eca-116">需要 nuget.exe 4.6.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="75eca-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="75eca-117">即将推出 dotnet.exe 支持 - [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="75eca-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="75eca-118">可使用 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 对包进行签名：</span><span class="sxs-lookup"><span data-stu-id="75eca-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="75eca-119">证书提供程序通常还提供时间戳服务器 URL，可用于如上所示的 `Timestamper` 可选参数。</span><span class="sxs-lookup"><span data-stu-id="75eca-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="75eca-120">请参考提供程序文档和/或该服务 URL 的支持。</span><span class="sxs-lookup"><span data-stu-id="75eca-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="75eca-121">可使用证书存储中可用的证书或使用来自文件的证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="75eca-122">请参阅 CLI 参考，了解 [nuget sign](../reference/cli-reference/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="75eca-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="75eca-123">已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。</span><span class="sxs-lookup"><span data-stu-id="75eca-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="75eca-124">否则签名操作将引发一个[警告](../reference/errors-and-warnings/NU3002.md)。</span><span class="sxs-lookup"><span data-stu-id="75eca-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="75eca-125">使用 [nuget verify](../reference/cli-reference/cli-ref-verify.md) 可查看给定包的签名详细信息。</span><span class="sxs-lookup"><span data-stu-id="75eca-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="75eca-126">使用 NuGet.org 注册证书</span><span class="sxs-lookup"><span data-stu-id="75eca-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="75eca-127">要发布已签名的包，必须先使用 NuGet.org 注册证书。需要将证书设置为二进制 DER 格式的 `.cer` 文件。</span><span class="sxs-lookup"><span data-stu-id="75eca-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="75eca-128">[登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="75eca-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="75eca-129">转到 `Account settings`（如果希望使用组织帐户注册证书，则转到 `Manage Organization` **>** `Edit Organziation`）。</span><span class="sxs-lookup"><span data-stu-id="75eca-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="75eca-130">展开 `Certificates` 部分，并选择 `Register new`。</span><span class="sxs-lookup"><span data-stu-id="75eca-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="75eca-131">浏览并选择前面导出的证书文件。</span><span class="sxs-lookup"><span data-stu-id="75eca-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="75eca-132">![已注册的证书](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="75eca-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="75eca-133">**注意**</span><span class="sxs-lookup"><span data-stu-id="75eca-133">**Note**</span></span>
* <span data-ttu-id="75eca-134">一个用户可以提交多个证书并且多个用户可以注册同一个证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="75eca-135">用户注册证书之后，所有未来的包提交都必须  使用其中一个证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="75eca-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="75eca-136">请参阅[管理 NuGet.org 上的包的签名要求](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="75eca-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="75eca-137">用户还可以从帐户中删除已注册的证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="75eca-138">删除证书后，使用该证书签名的新包将在提交时失败。</span><span class="sxs-lookup"><span data-stu-id="75eca-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="75eca-139">现有包不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="75eca-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="75eca-140">发布包</span><span class="sxs-lookup"><span data-stu-id="75eca-140">Publish the package</span></span>

<span data-ttu-id="75eca-141">现在即可将包发布到 NuGet.org。请参阅[发布包](../nuget-org/Publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="75eca-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="75eca-142">创建测试证书</span><span class="sxs-lookup"><span data-stu-id="75eca-142">Create a test certificate</span></span>

<span data-ttu-id="75eca-143">可使用自颁发证书进行测试。</span><span class="sxs-lookup"><span data-stu-id="75eca-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="75eca-144">要创建自颁发证书，请使用 [New-SelfSignedCertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="75eca-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="75eca-145">此命令将在当前用户的个人证书存储中创建可用的测试证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="75eca-146">可通过运行 `certmgr.msc` 打开证书存储，查看新创建的证书。</span><span class="sxs-lookup"><span data-stu-id="75eca-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="75eca-147">NuGet.org 不接受使用自颁发证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="75eca-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="75eca-148">管理 NuGet.org 上的包的签名要求</span><span class="sxs-lookup"><span data-stu-id="75eca-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="75eca-149">[登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="75eca-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="75eca-150">转到 `Manage Packages` 
   ![配置包签名程序](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="75eca-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="75eca-151">如果你是包的唯一所有者，那么你就是所要求的签名者，即你可使用任何已注册的证书对包进行签名，然后将其发布到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="75eca-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="75eca-152">如果包具有多个所有者，默认情况下，可以使用“任何”所有者的证书对包进行签名。</span><span class="sxs-lookup"><span data-stu-id="75eca-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="75eca-153">作为包的共同所有者，你可将“任何”重写为你自己或任何其他共同所有者，作为所需的签名者。</span><span class="sxs-lookup"><span data-stu-id="75eca-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="75eca-154">如果你让没有注册任何证书的人成为所有者，则将允许未签名的包。</span><span class="sxs-lookup"><span data-stu-id="75eca-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="75eca-155">同样，如果已选中某个包的默认“任何”选项，在该包中，有一个所有者已注册证书，而另一个所有者未注册任何证书，则 NuGet.org 接受已签名的包（由其中一个所有者注册签名）或接受未签名的包（因为其中一个所有者未注册任何证书）。</span><span class="sxs-lookup"><span data-stu-id="75eca-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="75eca-156">相关文章</span><span class="sxs-lookup"><span data-stu-id="75eca-156">Related articles</span></span>

- [<span data-ttu-id="75eca-157">管理包信任边界</span><span class="sxs-lookup"><span data-stu-id="75eca-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="75eca-158">签名包引用</span><span class="sxs-lookup"><span data-stu-id="75eca-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
