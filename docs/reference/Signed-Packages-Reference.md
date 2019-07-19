---
title: 已签名包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e02b2a241008b1b7096f20b351173fd3df7ed172
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317514"
---
# <a name="signed-packages"></a>已签名的包

*NuGet 4.6.0 + 和 Visual Studio 2017 版本15.6 及更高版本*

NuGet 包可以包含一个数字签名, 该签名提供针对篡改内容的保护。 此签名是通过 x.509 证书生成的, 该证书还将授权校样添加到包的实际来源。

签名包提供了最强大的端到端验证。 NuGet 签名有两种不同的类型:
- **作者签名**。 作者签名可保证自作者对包进行签名后包未修改, 无论包传送到哪个存储库或传输方法。 此外, 创作签名包还为 nuget.org 发布管道提供额外的身份验证机制, 因为必须提前注册签名证书。 有关详细信息, 请参阅[注册证书](#signature-requirements-on-nugetorg)。
- **存储库签名**。 存储库签名为存储库中的**所有**包提供完整性保证, 无论它们是否为作者签名, 即使这些包是从其签名的原始存储库以外的位置获取的。   

有关创建作者签名包的详细信息, 请参阅[签署包](../create-packages/Sign-a-package.md)和[nuget 签名命令](../reference/cli-reference/cli-ref-sign.md)。

> [!Important]
> 目前仅在 Windows 上使用 nuget.exe 时才支持包签名。 目前仅在使用 nuget.exe 或 Windows 上的 Visual Studio 时, 才支持验证已签名的包。

## <a name="certificate-requirements"></a>证书要求

包签名需要一个代码签名证书, 该证书是一种适用于`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] 的特殊类型证书。 此外, 证书的 RSA 公钥长度必须为2048位或更高。

## <a name="timestamp-requirements"></a>时间戳要求

签名包应包含 RFC 3161 时间戳, 以确保签名有效期超出包签名证书的有效期。 用于签署时间戳的证书必须有效, `id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外, 证书的 RSA 公钥长度必须为2048位或更高。

可以在[包签名技术规范](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub) 中找到其他技术详细信息。

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org 上的签名要求

nuget.org 对接受签名的包有其他要求:

- 主签名必须是作者签名。
- 主签名必须有一个有效的时间戳。
- 作者签名及其时间戳签名的 x.509 证书:
  - 必须具有 RSA 公钥2048或更高版本。
  - 在 nuget.org 上的包验证时, 必须在其每个当前 UTC 时间的有效期内。
  - 必须链接到 Windows 上默认受信任的受信任根证书颁发机构。 拒绝了用自行颁发的证书签名的包。
  - 的用途必须有效: 
    - 作者签名证书必须有效, 以便进行代码签名。
    - 对于时间戳, 时间戳证书必须有效。
  - 不能在签名时撤销。 (这可能不会在提交时 knowable, 因此 nuget.org 会定期复查列为吊销状态)。
  
  
## <a name="related-articles"></a>相关文章

- [对 NuGet 包进行签名](../create-packages/Sign-a-Package.md)
- [管理包信任边界](../consume-packages/installing-signed-packages.md)
