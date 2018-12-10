---
title: 安装已签名的 NuGet 包
description: 介绍安装已签名 NuGet 包并配置包签名信任设置的过程。
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977831"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="b5b4f-103">安装已签名的包</span><span class="sxs-lookup"><span data-stu-id="b5b4f-103">Install a signed package</span></span>

<span data-ttu-id="b5b4f-104">安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并引发[错误 NU3008](../reference/errors-and-warnings/NU3008.md)。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="b5b4f-105">使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="b5b4f-106">配置包签名要求</span><span class="sxs-lookup"><span data-stu-id="b5b4f-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="b5b4f-107">在 Windows 上需要 NuGet 4.9.0+ 和 Visual Studio 版本 15.9 及更高版本</span><span class="sxs-lookup"><span data-stu-id="b5b4f-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="b5b4f-108">可使用 [`nuget config`](../tools/cli-ref-config) 命令，通过在 [nuget.config](../reference/nuget-config-file) 文件中将 `signatureValidationMode` 设置为 `require`，配置 NuGet 客户端包签名的验证方式。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="b5b4f-109">此模式将验证所有包通过 `nuget.config` 文件中信任的任何证书进行签名。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="b5b4f-110">此文件允许基于证书的指纹指定信任哪些作者和/或存储库。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="b5b4f-111">信任包作者</span><span class="sxs-lookup"><span data-stu-id="b5b4f-111">Trust package author</span></span>

<span data-ttu-id="b5b4f-112">要基于作者签名信任包，请使用 [`trusted-signers`](..tools/cli-ref-trusted-signers) 命令设置 nuget.config 中的 `author` 属性。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="b5b4f-113">使用`nuget.exe`[验证命令](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify)获取证书的指纹值 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="b5b4f-114">信任存储库中的所有包</span><span class="sxs-lookup"><span data-stu-id="b5b4f-114">Trust all packages from a repository</span></span>

<span data-ttu-id="b5b4f-115">要基于存储库签名信任包，请使用 `repository` 元素：</span><span class="sxs-lookup"><span data-stu-id="b5b4f-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="b5b4f-116">信任包所有者</span><span class="sxs-lookup"><span data-stu-id="b5b4f-116">Trust Package Owners</span></span>

<span data-ttu-id="b5b4f-117">存储库签名包括用于确定提交时包的所有者的其他元数据。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="b5b4f-118">可以基于所有者列表限制存储库中的包：</span><span class="sxs-lookup"><span data-stu-id="b5b4f-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="b5b4f-119">如果某个包具有多个所有者，并且受信任列表中包含这些所有者中的任何一个，包安装将成功。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="b5b4f-120">不受信任的根证书</span><span class="sxs-lookup"><span data-stu-id="b5b4f-120">Untrusted Root certificates</span></span>

<span data-ttu-id="b5b4f-121">在某些情况下，你可能希望使用证书来启用验证，而证书并未链接到本地计算机的受信任根。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="b5b4f-122">可使用 `allowUntrustedRoot` 属性来自定义此行为。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="b5b4f-123">同步存储库证书</span><span class="sxs-lookup"><span data-stu-id="b5b4f-123">Sync repository certificates</span></span>

<span data-ttu-id="b5b4f-124">包存储库应发布其在[服务索引](https://docs.microsoft.com/en-us/nuget/api/service-index)中使用的证书。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="b5b4f-125">存储库最终将更新这些证书，例如证书过期时。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="b5b4f-126">出现这种情况时，使用特定策略的客户端将需要更新配置，以包括新添加的证书。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="b5b4f-127">可通过使用 `nuget.exe` [受信任的签名程序同步命令](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-)，轻松升级与某个存储库关联的受信任签名程序。</span><span class="sxs-lookup"><span data-stu-id="b5b4f-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="b5b4f-128">架构参考</span><span class="sxs-lookup"><span data-stu-id="b5b4f-128">Schema reference</span></span>

<span data-ttu-id="b5b4f-129">有关客户端策略的完整架构参考，请参阅 [nuget.config 参考](/nuget/reference/nuget-config-file#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="b5b4f-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="b5b4f-130">相关文章</span><span class="sxs-lookup"><span data-stu-id="b5b4f-130">Related articles</span></span>

- [<span data-ttu-id="b5b4f-131">安装 NuGet 包的不同方式</span><span class="sxs-lookup"><span data-stu-id="b5b4f-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="b5b4f-132">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="b5b4f-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="b5b4f-133">签名包引用</span><span class="sxs-lookup"><span data-stu-id="b5b4f-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
