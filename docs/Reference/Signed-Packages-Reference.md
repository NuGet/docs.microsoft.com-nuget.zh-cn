---
title: "签名包引用 |Microsoft 文档"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "签名包功能说明。"
keywords: "NuGet 包签名、 签名、 证书"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9bf9885aaf42bedb681a5d916202fa8b26749a0c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="signed-packages"></a><span data-ttu-id="48278-104">已签名的软件包</span><span class="sxs-lookup"><span data-stu-id="48278-104">Signed packages</span></span>

<span data-ttu-id="48278-105">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 及更高版本*</span><span class="sxs-lookup"><span data-stu-id="48278-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="48278-106">NuGet 包可以包含数字签名，它提供针对篡改的内容的保护。</span><span class="sxs-lookup"><span data-stu-id="48278-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="48278-107">此签名被生成一个 X.509 证书，还将真实性证明添加到包的实际来源。</span><span class="sxs-lookup"><span data-stu-id="48278-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="48278-108">已签名的软件包提供最高的端到端验证。</span><span class="sxs-lookup"><span data-stu-id="48278-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="48278-109">作者签名可保证由于作者签名包，无论从包不被修改的存储库或什么传输传递包的方法。</span><span class="sxs-lookup"><span data-stu-id="48278-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="48278-110">需要锁定环境使用者可以要求使用特定的作者证书签名的包。</span><span class="sxs-lookup"><span data-stu-id="48278-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="48278-111">此外，作者签名的包提供向 nuget.org 发布管道的额外的身份验证机制，因为签名的证书必须提前注册。</span><span class="sxs-lookup"><span data-stu-id="48278-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="48278-112">有关创建签名的包的详细信息，请参阅[签名包](../create-packages/Sign-a-package.md)和[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="48278-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="48278-113">nuget.org 目前不接受已签名的软件包。</span><span class="sxs-lookup"><span data-stu-id="48278-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="48278-114">可以用于发布到自定义源的程序包进行签名。</span><span class="sxs-lookup"><span data-stu-id="48278-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="48278-115">证书要求</span><span class="sxs-lookup"><span data-stu-id="48278-115">Certificate requirements</span></span>

<span data-ttu-id="48278-116">包签名需要代码签名证书，这是一种特殊类型的证书有效`id-kp-codeSigning`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="48278-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="48278-117">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="48278-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="48278-118">获取代码签名证书</span><span class="sxs-lookup"><span data-stu-id="48278-118">Get a code signing certificate</span></span>

<span data-ttu-id="48278-119">可能从等公共证书颁发机构那里获取有效证书：</span><span class="sxs-lookup"><span data-stu-id="48278-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="48278-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="48278-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="48278-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="48278-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="48278-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="48278-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="48278-123">全局登录</span><span class="sxs-lookup"><span data-stu-id="48278-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="48278-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="48278-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="48278-125">Certum</span><span class="sxs-lookup"><span data-stu-id="48278-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="48278-126">可以从获取由 Windows 受信任的证书颁发机构的完整列表[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="48278-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="48278-127">创建测试证书</span><span class="sxs-lookup"><span data-stu-id="48278-127">Create a test certificate</span></span>

<span data-ttu-id="48278-128">出于测试目的，可以使用自行颁发的证书。</span><span class="sxs-lookup"><span data-stu-id="48278-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="48278-129">若要创建自行颁发的证书，请使用[的 New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="48278-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="48278-130">此命令创建当前用户的个人证书存储中可用的测试证书。</span><span class="sxs-lookup"><span data-stu-id="48278-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="48278-131">你可以通过运行打开证书存储区`certmgr.msc`以查看新创建的证书。</span><span class="sxs-lookup"><span data-stu-id="48278-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="48278-132">时间戳要求</span><span class="sxs-lookup"><span data-stu-id="48278-132">Timestamp requirements</span></span>

<span data-ttu-id="48278-133">已签名的软件包应包括的 RFC 3161 时间戳，以确保签名有效性超出程序包签名证书的有效期。</span><span class="sxs-lookup"><span data-stu-id="48278-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="48278-134">用于签署时间戳证书必须是有效的`id-kp-timeStamping`目的 [[RFC 5280 部分 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="48278-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="48278-135">此外，证书必须具有 RSA 公钥长度为 2048 位或更高版本。</span><span class="sxs-lookup"><span data-stu-id="48278-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="48278-136">其他技术详细信息可在[包签名的技术规格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="48278-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
