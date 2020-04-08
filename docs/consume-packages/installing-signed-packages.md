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
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="10308-103">管理包信任边界</span><span class="sxs-lookup"><span data-stu-id="10308-103">Manage package trust boundaries</span></span>

<span data-ttu-id="10308-104">安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并引发[错误 NU3008](../reference/errors-and-warnings/NU3008.md)。</span><span class="sxs-lookup"><span data-stu-id="10308-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="10308-105">使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。</span><span class="sxs-lookup"><span data-stu-id="10308-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="10308-106">配置包签名要求</span><span class="sxs-lookup"><span data-stu-id="10308-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="10308-107">在 Windows 上需要 NuGet 4.9.0+ 和 Visual Studio 版本 15.9 及更高版本</span><span class="sxs-lookup"><span data-stu-id="10308-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="10308-108">可使用 `signatureValidationMode``require`[ 命令，通过在 ](../reference/nuget-config-file.md)nuget.config[ 文件中将 `nuget config` 设置为 ](../reference/cli-reference/cli-ref-config.md)，配置 NuGet 客户端包签名的验证方式。</span><span class="sxs-lookup"><span data-stu-id="10308-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="10308-109">此模式将验证所有包通过 `nuget.config` 文件中信任的任何证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="10308-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="10308-110">此文件允许基于证书的指纹指定信任哪些作者和/或存储库。</span><span class="sxs-lookup"><span data-stu-id="10308-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="10308-111">信任包作者</span><span class="sxs-lookup"><span data-stu-id="10308-111">Trust package author</span></span>

<span data-ttu-id="10308-112">要基于作者签名信任包，请使用 [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) 命令设置 nuget.config 中的 `author` 属性。</span><span class="sxs-lookup"><span data-stu-id="10308-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="10308-113">使用 `nuget.exe` [验证命令](../reference/cli-reference/cli-ref-verify.md)获取证书的指纹值 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="10308-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="10308-114">信任存储库中的所有包</span><span class="sxs-lookup"><span data-stu-id="10308-114">Trust all packages from a repository</span></span>

<span data-ttu-id="10308-115">要基于存储库签名信任包，请使用 `repository` 元素：</span><span class="sxs-lookup"><span data-stu-id="10308-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="10308-116">信任包所有者</span><span class="sxs-lookup"><span data-stu-id="10308-116">Trust Package Owners</span></span>

<span data-ttu-id="10308-117">存储库签名包括用于确定提交时包的所有者的其他元数据。</span><span class="sxs-lookup"><span data-stu-id="10308-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="10308-118">可以基于所有者列表限制存储库中的包：</span><span class="sxs-lookup"><span data-stu-id="10308-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="10308-119">如果某个包具有多个所有者，并且受信任列表中包含这些所有者中的任何一个，包安装将成功。</span><span class="sxs-lookup"><span data-stu-id="10308-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="10308-120">不受信任的根证书</span><span class="sxs-lookup"><span data-stu-id="10308-120">Untrusted Root certificates</span></span>

<span data-ttu-id="10308-121">在某些情况下，你可能希望使用证书来启用验证，而证书并未链接到本地计算机的受信任根。</span><span class="sxs-lookup"><span data-stu-id="10308-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="10308-122">可使用 `allowUntrustedRoot` 属性来自定义此行为。</span><span class="sxs-lookup"><span data-stu-id="10308-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="10308-123">同步存储库证书</span><span class="sxs-lookup"><span data-stu-id="10308-123">Sync repository certificates</span></span>

<span data-ttu-id="10308-124">包存储库应发布其在[服务索引](../api/service-index.md)中使用的证书。</span><span class="sxs-lookup"><span data-stu-id="10308-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="10308-125">存储库最终将更新这些证书，例如证书过期时。</span><span class="sxs-lookup"><span data-stu-id="10308-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="10308-126">出现这种情况时，使用特定策略的客户端将需要更新配置，以包括新添加的证书。</span><span class="sxs-lookup"><span data-stu-id="10308-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="10308-127">可以使用 `nuget.exe` [受信任签名程序同步命令](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)，轻松升级与存储库关联的受信任签名程序。</span><span class="sxs-lookup"><span data-stu-id="10308-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="10308-128">架构参考</span><span class="sxs-lookup"><span data-stu-id="10308-128">Schema reference</span></span>

<span data-ttu-id="10308-129">有关客户端策略的完整架构参考，请参阅 [nuget.config 参考](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="10308-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="10308-130">相关文章</span><span class="sxs-lookup"><span data-stu-id="10308-130">Related articles</span></span>

- [<span data-ttu-id="10308-131">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="10308-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="10308-132">签名包引用</span><span class="sxs-lookup"><span data-stu-id="10308-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
