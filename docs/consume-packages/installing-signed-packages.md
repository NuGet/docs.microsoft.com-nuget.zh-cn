---
title: 管理包信任边界
description: 介绍安装已签名 NuGet 包并配置包签名信任设置的过程。
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428599"
---
# <a name="manage-package-trust-boundaries"></a>管理包信任边界

安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并引发[错误 NU3008](../reference/errors-and-warnings/NU3008.md)。

> [!Warning]
> 使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。

## <a name="configure-package-signature-requirements"></a>配置包签名要求

> [!Note]
> 在 Windows 上需要 NuGet 4.9.0+ 和 Visual Studio 版本 15.9 及更高版本

可使用 `signatureValidationMode``require`[ 命令，通过在 ](../reference/nuget-config-file.md)nuget.config[ 文件中将 `nuget config` 设置为 ](../reference/cli-reference/cli-ref-config.md)，配置 NuGet 客户端包签名的验证方式。

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

此模式将验证所有包通过 `nuget.config` 文件中信任的任何证书进行签名。 此文件允许基于证书的指纹指定信任哪些作者和/或存储库。

### <a name="trust-package-author"></a>信任包作者

要基于作者签名信任包，请使用 [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) 命令设置 nuget.config 中的 `author` 属性。

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>使用 `nuget.exe` [验证命令](../reference/cli-reference/cli-ref-verify.md)获取证书的指纹值 `SHA256`。


### <a name="trust-all-packages-from-a-repository"></a>信任存储库中的所有包

要基于存储库签名信任包，请使用 `repository` 元素：

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>信任包所有者

存储库签名包括用于确定提交时包的所有者的其他元数据。 可以基于所有者列表限制存储库中的包：

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

如果某个包具有多个所有者，并且受信任列表中包含这些所有者中的任何一个，包安装将成功。

### <a name="untrusted-root-certificates"></a>不受信任的根证书

在某些情况下，你可能希望使用证书来启用验证，而证书并未链接到本地计算机的受信任根。 可使用 `allowUntrustedRoot` 属性来自定义此行为。

### <a name="sync-repository-certificates"></a>同步存储库证书

包存储库应发布其在[服务索引](../api/service-index.md)中使用的证书。 存储库最终将更新这些证书，例如证书过期时。 出现这种情况时，使用特定策略的客户端将需要更新配置，以包括新添加的证书。 可以使用 `nuget.exe` [受信任签名程序同步命令](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)，轻松升级与存储库关联的受信任签名程序。

### <a name="schema-reference"></a>架构参考

有关客户端策略的完整架构参考，请参阅 [nuget.config 参考](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>相关文章

- [对 NuGet 包进行签名](../create-packages/Sign-a-Package.md)
- [签名包引用](../reference/Signed-Packages-Reference.md)
