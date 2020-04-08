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
# <a name="signing-nuget-packages"></a>对 NuGet 包进行签名

已签名的包允许进行内容完整性验证检查，可有效防止内容被篡改。 此外，包的签名还可作为包的实际来源的单一可信来源，增强了对包使用者的身份验证。 本指南假定你已[创建一个包](creating-a-package.md)。

## <a name="get-a-code-signing-certificate"></a>获取代码签名证书

可从以下公共证书颁发机构获取有效的证书：[Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 等。可从 [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners) 获取 Windows 信任的证书颁发机构完整列表。

可使用自颁发证书进行测试。 但 NuGet.org 不接受使用自颁发证书签名的包。详细了解如何[创建测试证书](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>导出证书文件

* 使用证书导出向导，可将现有的证书导出为二进制 DER 格式。

  ![证书导出向导](../reference/media/CertificateExportWizard.png)

* 此外，还可使用 [Export-Certificate PowerShell 命令](/powershell/module/pkiclient/export-certificate)导出证书。

## <a name="sign-the-package"></a>对包进行签名

> [!note]
> 需要 nuget.exe 4.6.0 或更高版本。 即将推出 dotnet.exe 支持 - [#7939](https://github.com/NuGet/Home/issues/7939)

可使用 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 对包进行签名：

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> 证书提供程序通常还提供时间戳服务器 URL，可用于如上所示的 `Timestamper` 可选参数。 请参考提供程序文档和/或该服务 URL 的支持。

* 可使用证书存储中可用的证书或使用来自文件的证书。 请参阅 CLI 参考，了解 [nuget sign](../reference/cli-reference/cli-ref-sign.md)。
* 已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。 否则签名操作将引发一个[警告](../reference/errors-and-warnings/NU3002.md)。
* 使用 [nuget verify](../reference/cli-reference/cli-ref-verify.md) 可查看给定包的签名详细信息。

## <a name="register-the-certificate-on-nugetorg"></a>使用 NuGet.org 注册证书

要发布已签名的包，必须先使用 NuGet.org 注册证书。需要将证书设置为二进制 DER 格式的 `.cer` 文件。

1. [登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。
1. 转到 `Account settings`（如果希望使用组织帐户注册证书，则转到 `Manage Organization` **>** `Edit Organziation`）。
1. 展开 `Certificates` 部分，并选择 `Register new`。
1. 浏览并选择前面导出的证书文件。
  ![已注册的证书](../reference/media/registered-certs.png)

**注意**
* 一个用户可以提交多个证书并且多个用户可以注册同一个证书。
* 用户注册证书之后，所有未来的包提交都必须  使用其中一个证书进行签名。 请参阅[管理 NuGet.org 上的包的签名要求](#manage-signing-requirements-for-your-package-on-nugetorg)
* 用户还可以从帐户中删除已注册的证书。 删除证书后，使用该证书签名的新包将在提交时失败。 现有包不会受到影响。

## <a name="publish-the-package"></a>发布包

现在即可将包发布到 NuGet.org。请参阅[发布包](../nuget-org/Publish-a-package.md)。

## <a name="create-a-test-certificate"></a>创建测试证书

可使用自颁发证书进行测试。 要创建自颁发证书，请使用 [New-SelfSignedCertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate)。

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

此命令将在当前用户的个人证书存储中创建可用的测试证书。 可通过运行 `certmgr.msc` 打开证书存储，查看新创建的证书。

> [!Warning]
> NuGet.org 不接受使用自颁发证书签名的包。

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>管理 NuGet.org 上的包的签名要求
1. [登录](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)到 NuGet.org。

1. 转到 `Manage Packages` 
   ![配置包签名程序](../reference/media/configure-package-signers.png)

* 如果你是包的唯一所有者，那么你就是所要求的签名者，即你可使用任何已注册的证书对包进行签名，然后将其发布到 NuGet.org。

* 如果包具有多个所有者，默认情况下，可以使用“任何”所有者的证书对包进行签名。 作为包的共同所有者，你可将“任何”重写为你自己或任何其他共同所有者，作为所需的签名者。 如果你让没有注册任何证书的人成为所有者，则将允许未签名的包。 

* 同样，如果已选中某个包的默认“任何”选项，在该包中，有一个所有者已注册证书，而另一个所有者未注册任何证书，则 NuGet.org 接受已签名的包（由其中一个所有者注册签名）或接受未签名的包（因为其中一个所有者未注册任何证书）。

## <a name="related-articles"></a>相关文章

- [管理包信任边界](../consume-packages/installing-signed-packages.md)
- [签名包引用](../reference/Signed-Packages-Reference.md)
