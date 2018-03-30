---
title: 对 NuGet 包进行签名 | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 介绍如何使用已签名包来启用内容完整性验证。
keywords: NuGet 包签名, NuGet 安全性, 创建已签名包
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="91cdf-104">对 NuGet 包进行签名</span><span class="sxs-lookup"><span data-stu-id="91cdf-104">Signing NuGet Packages</span></span>

<span data-ttu-id="91cdf-105">对包进行签名的过程可确保包自创建以来未被修改。</span><span class="sxs-lookup"><span data-stu-id="91cdf-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91cdf-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="91cdf-106">Prerequisites</span></span>

1. <span data-ttu-id="91cdf-107">待签名的包（一个 `.nupkg` 文件）。</span><span class="sxs-lookup"><span data-stu-id="91cdf-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="91cdf-108">请参阅[创建包](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="91cdf-109">nuget.exe 4.6.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="91cdf-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="91cdf-110">请参阅如何[安装 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="91cdf-111">[代码签名证书](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="91cdf-112">nuget.org 目前不接受已签名的包。</span><span class="sxs-lookup"><span data-stu-id="91cdf-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="91cdf-113">可以对发布到自定义源的包进行签名。</span><span class="sxs-lookup"><span data-stu-id="91cdf-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="91cdf-114">对包进行签名</span><span class="sxs-lookup"><span data-stu-id="91cdf-114">Sign a package</span></span>

<span data-ttu-id="91cdf-115">若要对包进行签名，请使用 [nuget sign](../tools/cli-ref-sign.md)：</span><span class="sxs-lookup"><span data-stu-id="91cdf-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="91cdf-116">如命令参考中所述，可以使用证书存储中可用的证书或使用来自文件的证书。</span><span class="sxs-lookup"><span data-stu-id="91cdf-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="91cdf-117">对包签名时的常见问题</span><span class="sxs-lookup"><span data-stu-id="91cdf-117">Common problems when signing a package</span></span>

- <span data-ttu-id="91cdf-118">证书对代码签名无效。</span><span class="sxs-lookup"><span data-stu-id="91cdf-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="91cdf-119">必须确保指定的证书具有适当的扩展密钥用法 (EKU 1.3.6.1.5.5.7.3.3)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="91cdf-120">证书不符合基本要求，例如 RSA SHA-256 签名算法或 2048 位或更高位公钥。</span><span class="sxs-lookup"><span data-stu-id="91cdf-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="91cdf-121">证书已过期或已吊销。</span><span class="sxs-lookup"><span data-stu-id="91cdf-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="91cdf-122">时间戳服务器不符合证书要求。</span><span class="sxs-lookup"><span data-stu-id="91cdf-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="91cdf-123">已签名包应包含时间戳，用于确保签名证书过期时签名仍有效。</span><span class="sxs-lookup"><span data-stu-id="91cdf-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="91cdf-124">签名不含时间戳时，签名操作会发出[警告 NU3002](../reference/Errors-and-Warnings.md#nu3002)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="91cdf-125">验证已签名的包</span><span class="sxs-lookup"><span data-stu-id="91cdf-125">Verify a signed package</span></span>

<span data-ttu-id="91cdf-126">使用 [nuget verify](../tools/cli-ref-verify.md) 查看给定包的签名详细信息：</span><span class="sxs-lookup"><span data-stu-id="91cdf-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="91cdf-127">安装已签名的包</span><span class="sxs-lookup"><span data-stu-id="91cdf-127">Install a signed package</span></span>

<span data-ttu-id="91cdf-128">安装已签名的包不需要任何特定操作；但是，如果内容在签名后被修改，则安装会被阻止并发出[错误 NU3008](../reference/Errors-and-Warnings.md#nu3008)。</span><span class="sxs-lookup"><span data-stu-id="91cdf-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="91cdf-129">使用不受信任的证书签名的包被视为未签名，并且在安装时不会像其他任何未签名的包一样发出任何警告或错误。</span><span class="sxs-lookup"><span data-stu-id="91cdf-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="91cdf-130">请参阅</span><span class="sxs-lookup"><span data-stu-id="91cdf-130">See also</span></span>

[<span data-ttu-id="91cdf-131">签名包引用</span><span class="sxs-lookup"><span data-stu-id="91cdf-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
