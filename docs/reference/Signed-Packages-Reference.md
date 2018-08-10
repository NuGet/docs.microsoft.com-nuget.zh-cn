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
# <a name="signed-packages"></a>签名的包

*NuGet 4.6.0+ 和 Visual Studio 2017 版本 15.6 及更高版本*

NuGet 包可以包含的数字签名来提供保护以防止被篡改的内容。 此签名被生成的 X.509 证书，还添加到包的实际来源真实性概念。

已签名的软件包提供最强的端到端验证。 有两种不同类型的 NuGet 签名：
- **创作签名**。 作者签名可保证包作者签名包，而不管从后未被修改的存储库或内容传输，递送包裹的方法。 此外，作者签署的程序包提供额外的身份验证机制向 nuget.org 发布管道，因为必须提前注册签名证书。 有关详细信息，请参阅[注册的证书](#register-certificate-on-nugetorg)。
- **存储库签名**。 存储库签名提供完整性保障**所有**包存储库中，无论它们是作者签名或不是，即使从不同的位置所在的原始存储库获取这些包签名。   

创建作者签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)并[nuget 登录命令](../tools/cli-ref-sign.md)。

> [!Important]
> 仅当在 Windows 上使用 nuget.exe，目前支持包签名。 仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名包的验证。

## <a name="certificate-requirements"></a>证书要求

包签名需要代码签名证书，这是一种特殊类型的有效的证书`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

## <a name="get-a-code-signing-certificate"></a>获取代码签名证书

从公共证书颁发机构等都可以获得有效的证书：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全局符号](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

可以从 Windows 的受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>创建测试证书

出于测试目的，可以使用自行颁发的证书。 若要创建自行颁发的证书，请使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。

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

此命令在当前用户的个人证书存储区中创建的测试证书可用。 可以通过运行打开证书存储区`certmgr.msc`若要查看新创建的证书。

> [!Warning]
> nuget.org 不接受包使用自行颁发的证书进行签名。

## <a name="timestamp-requirements"></a>时间戳要求

已签名的包应包含一个 RFC 3161 时间戳，以确保包签名证书的有效期超出签名有效性。 用于登录时间戳的证书必须为有效`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 nuget.org 上的签名要求

nuget.org 具有用于接受已签名的包的附加要求：

- 主签名必须是作者签名。
- 主签名必须具有一个有效的时间戳。
- 作者签名和其时间戳签名的 X.509 证书：
  - 必须具有 RSA 公钥 2048 位或更高版本。
  - 必须在每次当前 UTC 时间的 nuget.org 上的包验证其有效期内。
  - 必须链接到默认情况下，在 Windows 上受信任的受信任的根颁发机构。 使用自行颁发的证书签名的包将被拒绝。
  - 必须是有效的它的用途： 
    - 签名证书的作者必须对代码签名有效。
    - 时间戳证书必须是有效的时间戳。
  - 必须不会撤消在签名时。 （这可能不是可知在提交时，因此 nuget.org 定期重新检查吊销状态）。

## <a name="register-certificate-on-nugetorg"></a>在 nuget.org 上注册证书

若要提交已签名的包，必须先使用 nuget.org 注册证书。你需要为证书`.cer`二进制 DER 格式文件中的。 使用证书导出向导，可以将现有的证书导出到二进制 DER 格式。

![证书导出向导](media/CertificateExportWizard.png)

高级的用户可以导出证书使用[导出证书的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。

若要向 nuget.org 注册证书，请转到`Certificates`部分`Account settings`页 （或组织的设置页），然后选择`Register new certificate`。

![已注册的证书](media/registered-certs.png)

> [!Tip]
> 一个用户可以提交多个用户可以注册多个证书和相同的证书。

一旦用户拥有一个证书注册，未来的程序包的所有提交**必须**使用其中一个证书进行签名。

用户还可以从帐户中删除已注册的证书。 删除证书后，使用该证书签名的包会在提交失败。 现有的包不会受到影响。

## <a name="configure-package-signing-requirements"></a>配置包签名要求

如果你是包的唯一所有者，则可以所需的签名者。 也就是说，您可以使用任何已注册的证书签署应用程序包并将提交到 nuget.org。

如果包包含多个所有者，默认情况下，可以使用"任何"所有者的证书对程序包进行签名。 作为包的共同所有者，你可以重写"任何"与自己或任何其他共同所有者为所需的签名者。 如果没有注册任何证书的所有者，则将允许未签名的包。 

同样，如果"任何"选项选择其中一个所有者具有注册证书的包和另一个所有者的默认值不具有注册任何证书，然后 nuget.org 接受已签名的包具有签名由其所有者之一注册或未签名包 （因为某个所有者没有注册任何证书）。

![配置包签名者](media/configure-package-signers.png)
