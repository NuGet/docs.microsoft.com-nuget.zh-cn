---
title: 签名 NuGet 包引用
description: NuGet 包签名要求。
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a>已签名的软件包

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 及更高版本*

NuGet 包可以包含数字签名，它提供针对篡改的内容的保护。 此签名被生成一个 X.509 证书，还将真实性证明添加到包的实际来源。

已签名的软件包提供最高的端到端验证。 作者签名可保证由于作者签名包，无论从包不被修改的存储库或什么传输传递包的方法。

需要锁定环境使用者可以要求使用特定的作者证书签名的包。

此外，作者签名的包提供向 nuget.org 发布管道的额外的身份验证机制，因为签名的证书必须提前注册。

有关创建签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)和[nuget 登录命令](../tools/cli-ref-sign.md)。

> [!Important]
> nuget.org 目前不接受已签名的软件包。 可以对发布到自定义源的包进行签名。

> [!Important]
> 仅在 Windows 上使用 nuget.exe 时，当前支持包签名。 仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名的软件包的验证。

## <a name="certificate-requirements"></a>证书要求

包签名需要代码签名证书，这是一种特殊类型的证书有效`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

## <a name="get-a-code-signing-certificate"></a>获取代码签名证书

可能从等公共证书颁发机构那里获取有效证书：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全局登录](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

可以从获取由 Windows 受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>创建测试证书

出于测试目的，可以使用自行颁发的证书。 若要创建自行颁发的证书，请使用[的 New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 命令。

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

## <a name="timestamp-requirements"></a>时间戳要求

已签名的软件包应包括的 RFC 3161 时间戳，以确保签名有效性超出程序包签名证书的有效期。 用于签署时间戳证书必须是有效的`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。
