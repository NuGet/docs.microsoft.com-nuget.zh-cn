---
title: 对 NuGet 包进行签名
description: 介绍如何使用已签名包来启用内容完整性验证。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c598461831323ecfcc5da3877df71bd8d69557f6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551973"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="b0457-103">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="b0457-103">Signing NuGet Packages</span></span>

<span data-ttu-id="b0457-104">对包进行签名的过程可确保包自创建以来未被修改。</span><span class="sxs-lookup"><span data-stu-id="b0457-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0457-105">系统必备</span><span class="sxs-lookup"><span data-stu-id="b0457-105">Prerequisites</span></span>

1. <span data-ttu-id="b0457-106">待签名的包（一个 `.nupkg` 文件）。</span><span class="sxs-lookup"><span data-stu-id="b0457-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="b0457-107">请参阅[创建包](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="b0457-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="b0457-108">nuget.exe 4.6.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="b0457-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="b0457-109">请参阅如何[安装 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="b0457-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="b0457-110">[代码签名证书](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="b0457-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="b0457-111">对包进行签名</span><span class="sxs-lookup"><span data-stu-id="b0457-111">Sign a package</span></span>

<span data-ttu-id="b0457-112">若要对包进行签名，请使用 [nuget sign](../tools/cli-ref-sign.md)：</span><span class="sxs-lookup"><span data-stu-id="b0457-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="b0457-113">如命令参考中所述，可以使用证书存储中可用的证书或使用来自文件的证书。</span><span class="sxs-lookup"><span data-stu-id="b0457-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="b0457-114">对包签名时的常见问题</span><span class="sxs-lookup"><span data-stu-id="b0457-114">Common problems when signing a package</span></span>

- <span data-ttu-id="b0457-115">证书对代码签名无效。</span><span class="sxs-lookup"><span data-stu-id="b0457-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="b0457-116">必须确保指定的证书具有适当的扩展密钥用法 (EKU 1.3.6.1.5.5.7.3.3)。</span><span class="sxs-lookup"><span data-stu-id="b0457-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="b0457-117">证书不符合基本要求，例如 RSA SHA-256 签名算法或 2048 位或更高位公钥。</span><span class="sxs-lookup"><span data-stu-id="b0457-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="b0457-118">证书已过期或已吊销。</span><span class="sxs-lookup"><span data-stu-id="b0457-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="b0457-119">时间戳服务器不符合证书要求。</span><span class="sxs-lookup"><span data-stu-id="b0457-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="b0457-120">已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。</span><span class="sxs-lookup"><span data-stu-id="b0457-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="b0457-121">签名不含时间戳时，签名操作会发出[警告 NU3002](../reference/errors-and-warnings/NU3002.md)。</span><span class="sxs-lookup"><span data-stu-id="b0457-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="b0457-122">验证已签名的包</span><span class="sxs-lookup"><span data-stu-id="b0457-122">Verify a signed package</span></span>

<span data-ttu-id="b0457-123">使用 [nuget verify](../tools/cli-ref-verify.md) 查看给定包的签名详细信息：</span><span class="sxs-lookup"><span data-stu-id="b0457-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="b0457-124">安装已签名的包</span><span class="sxs-lookup"><span data-stu-id="b0457-124">Install a signed package</span></span>

<span data-ttu-id="b0457-125">安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并引发[错误 NU3008](../reference/errors-and-warnings/NU3008.md)。</span><span class="sxs-lookup"><span data-stu-id="b0457-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked and produces an [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="b0457-126">使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。</span><span class="sxs-lookup"><span data-stu-id="b0457-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="b0457-127">请参阅</span><span class="sxs-lookup"><span data-stu-id="b0457-127">See also</span></span>

[<span data-ttu-id="b0457-128">签名包引用</span><span class="sxs-lookup"><span data-stu-id="b0457-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
