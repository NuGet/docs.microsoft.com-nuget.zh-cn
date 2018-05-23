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
---
# <a name="signed-packages"></a>已签名的软件包

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 及更高版本*

NuGet 包可以包含数字签名，它提供针对篡改的内容的保护。 此签名被生成一个 X.509 证书，还将真实性证明添加到包的实际来源。

已签名的软件包提供最高的端到端验证。 作者签名可保证由于作者签名包，无论从包不被修改的存储库或什么传输传递包的方法。

此外，作者签名的包提供向 nuget.org 发布管道的额外的身份验证机制，因为签名的证书必须提前注册。 有关详细信息，请参阅[将证书注册](#register-certificate-on-nugetorg)。

有关创建签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)和[nuget 登录命令](../tools/cli-ref-sign.md)。

> [!Important]
> 仅在 Windows 上使用 nuget.exe 时，当前支持包签名。 仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名的软件包的验证。

## <a name="certificate-requirements"></a>证书要求

包签名需要代码签名证书，这是一种特殊类型的证书有效`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

## <a name="get-a-code-signing-certificate"></a>获取代码签名证书

可能从类似的公共证书颁发机构那里获取有效证书：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全局登录](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

可以从获取由 Windows 受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>创建测试证书

出于测试目的，可以使用自行颁发的证书。 若要创建自行颁发的证书，请使用[的 New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。

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

此命令创建当前用户的个人证书存储中可用的测试证书。 你可以通过运行打开证书存储区`certmgr.msc`以查看新创建的证书。

> [!Warning]
> nuget.org 不接受包使用自行颁发的证书签名。

## <a name="timestamp-requirements"></a>时间戳要求

已签名的软件包应包括的 RFC 3161 时间戳，以确保签名有效性超出程序包签名证书的有效期。 用于签署时间戳证书必须是有效的`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 nuget.org 上的签名要求

nuget.org 具有用于接受签名的包的附加要求：

- 主签名必须是作者签名。
- 主签名必须具有一个有效的时间戳。
- 作者签名和其时间戳签名的 X.509 证书：
  - 必须具有 RSA 公钥 2048 位或更高版本。
  - 必须在每次当前 UTC 时间的 nuget.org 上的包验证其有效期内。
  - 必须链接到默认情况下，在 Windows 上受信任的受信任的根颁发机构。 使用自行颁发的证书签名的包将被拒绝。
  - 为其目的，必须是有效的： 
    - 签名证书的作者必须是有效的代码签名。
    - 时间戳证书必须是有效的时间戳。
  - 不必须吊销在签名时。 （这可能不为可知在提交时间，因此 nuget.org 定期重新检查吊销状态）。

## <a name="register-certificate-on-nugetorg"></a>注册在 nuget.org 上的证书

若要提交已签名的包，您必须首先向 nuget.org 注册证书。你需要作为证书`.cer`二进制 DER 格式文件中的。 使用证书导出向导，可以将现有证书导出到的二进制 DER 格式。

![证书导出向导](media/CertificateExportWizard.png)

高级的用户可以导出证书使用[导出证书 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。

若要向 nuget.org 注册证书，请转到`Certificates`节`Account settings`页 （或组织的设置页中），然后选择`Register new certificate`。

![注册的证书](media/registered-certs.png)

> [!Tip]
> 一个用户可以提交多个证书和相同的证书可由多个用户进行注册。

一旦用户拥有一个证书注册，所有将来的软件包提交**必须**用的某个证书进行签名。

用户还可以从帐户中删除已注册的证书。 一旦删除证书，使用该证书签名的包将在提交失败。 现有包不会受到影响。

## <a name="configure-package-signing-requirements"></a>配置包签名要求

如果你是包的唯一所有者，你将所需的签名者。 即你可以使用任何已注册的证书进行签名的包和将提交到 nuget.org。

如果包包含多个所有者，默认情况下，可以使用"任何"所有者的证书对包进行签名。 作为包共同所有者，您可以重写"任何"与自己或任何其他共同所有者为所需的签名者。 如果你将用户没有注册任何证书的所有者，则将允许未签名的包。 

同样，如果"任何"选项选择其中一个所有者所有已注册的证书包和另一个所有者的默认设置不具有注册任何证书，然后 nuget.org 接受签名的包具有由其所有者之一注册签名或未签名包 （因为某个所有者不具有注册任何证书）。

![配置包签名者](media/configure-package-signers.png)
