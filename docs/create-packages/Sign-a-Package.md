---
title: 对 NuGet 包进行签名
description: 介绍如何使用已签名包来启用内容完整性验证。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792962"
---
# <a name="signing-nuget-packages"></a>对 NuGet 包进行签名

对包进行签名的过程可确保包自创建以来未被修改。

## <a name="prerequisites"></a>系统必备

1. 待签名的包（一个 `.nupkg` 文件）。 请参阅[创建包](creating-a-package.md)。

1. nuget.exe 4.6.0 或更高版本。 请参阅如何[安装 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。

1. [代码签名证书](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。

## <a name="sign-a-package"></a>对包进行签名

若要对包进行签名，请使用 [nuget sign](../tools/cli-ref-sign.md)：

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

如命令参考中所述，可以使用证书存储中可用的证书或使用来自文件的证书。

### <a name="common-problems-when-signing-a-package"></a>对包签名时的常见问题

- 证书对代码签名无效。 必须确保指定的证书具有适当的扩展密钥用法 (EKU 1.3.6.1.5.5.7.3.3)。
- 证书不符合基本要求，例如 RSA SHA-256 签名算法或 2048 位或更高位公钥。
- 证书已过期或已吊销。
- 时间戳服务器不符合证书要求。

> [!Note]
> 已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。 签名不含时间戳时，签名操作会发出[警告 NU3002](../reference/errors-and-warnings/NU3002.md)。

## <a name="verify-a-signed-package"></a>验证已签名的包

使用 [nuget verify](../tools/cli-ref-verify.md) 查看给定包的签名详细信息：

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>安装已签名的包

安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并引发[错误 NU3008](../reference/errors-and-warnings/NU3008.md)。

> [!Warning]
> 使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。

## <a name="see-also"></a>请参阅

[签名包引用](../reference/Signed-Packages-Reference.md)
