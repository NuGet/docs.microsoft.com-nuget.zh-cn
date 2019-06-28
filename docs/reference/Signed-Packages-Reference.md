---
title: 已签名的包
description: NuGet 包签名的要求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426174"
---
# <a name="signed-packages"></a>已签名的包

*NuGet 4.6.0+ 和 Visual Studio 2017 版本 15.6 及更高版本*

NuGet 包可以包含的数字签名来提供保护以防止被篡改的内容。 此签名被生成的 X.509 证书，还添加到包的实际来源真实性概念。

已签名的软件包提供最强的端到端验证。 有两种不同类型的 NuGet 签名：
- **创作签名**。 作者签名可保证包作者签名包，而不管从后未被修改的存储库或内容传输，递送包裹的方法。 此外，作者签署的程序包提供额外的身份验证机制向 nuget.org 发布管道，因为必须提前注册签名证书。 有关详细信息，请参阅[注册的证书](#signature-requirements-on-nugetorg)。
- **存储库签名**。 存储库签名提供完整性保障**所有**包存储库中，无论它们是作者签名或不是，即使从不同的位置所在的原始存储库获取这些包签名。   

创建作者签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)并[nuget 登录命令](../tools/cli-ref-sign.md)。

> [!Important]
> 仅当在 Windows 上使用 nuget.exe，目前支持包签名。 仅在 Windows 上使用 nuget.exe 或 Visual Studio 时，当前支持的已签名包的验证。

## <a name="certificate-requirements"></a>证书要求

包签名需要代码签名证书，这是一种特殊类型的有效的证书`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

## <a name="timestamp-requirements"></a>时间戳要求

已签名的包应包含一个 RFC 3161 时间戳，以确保包签名证书的有效期超出签名有效性。 用于登录时间戳的证书必须为有效`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。

其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 NuGet.org 上的签名要求

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
  
  
## <a name="related-articles"></a>相关文章

- [对 NuGet 包进行签名](../create-packages/Sign-a-Package.md)
- [管理包信任边界](../consume-packages/installing-signed-packages.md)
