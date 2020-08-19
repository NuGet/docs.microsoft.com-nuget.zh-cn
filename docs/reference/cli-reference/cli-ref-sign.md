---
title: NuGet CLI 签名命令
description: nuget.exe sign 命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622767"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="a3c6c-103"> (NuGet CLI 的 sign 命令) </span><span class="sxs-lookup"><span data-stu-id="a3c6c-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="a3c6c-104">**适用于：** 创建包的 &bullet; **支持版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a3c6c-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a3c6c-105">使用证书对匹配第一个参数的所有包进行签名。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="a3c6c-106">可以通过提供使用者名称或指纹，从文件或证书存储中安装的证书获取带有私钥的证书。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="a3c6c-107">.NET Core、Mono 或非 Windows 平台上尚不支持包签名。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a3c6c-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="a3c6c-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="a3c6c-109">其中 `<package(s)>` ，是一个或多个 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="a3c6c-110">选项</span><span class="sxs-lookup"><span data-stu-id="a3c6c-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a3c6c-111">指定用于搜索证书的本地证书存储区的证书的 SHA-1 指纹。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="a3c6c-112">如果需要，指定证书密码。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="a3c6c-113">如果证书受密码保护，但未提供密码，则该命令将在运行时提示输入密码，除非传递了 `-NonInteractive` 选项。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="a3c6c-114">指定用于对包进行签名的证书的文件路径。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="a3c6c-115">指定用于搜索证书的 x.509 证书存储区的名称。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="a3c6c-116">默认为 "CurrentUser"，当前用户使用的 x.509 证书存储。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="a3c6c-117">当通过或选项指定证书时，应使用此选项 `-CertificateSubjectName` `-CertificateFingerprint` 。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="a3c6c-118">指定用于搜索证书的 x.509 证书存储区的名称。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="a3c6c-119">默认值为 "My"，适用于个人证书的 x.509 证书存储。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="a3c6c-120">当通过或选项指定证书时，应使用此选项 `-CertificateSubjectName` `-CertificateFingerprint` 。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="a3c6c-121">指定用于在本地证书存储区中搜索证书的证书的使用者名称。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="a3c6c-122">搜索是使用提供的值进行区分大小写的字符串比较，它将查找使用者名称包含该字符串的所有证书，而与其他使用者值无关。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="a3c6c-123">证书存储区可以由 `-CertificateStoreName` 和选项指定 `-CertificateStoreLocation` 。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a3c6c-124">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3c6c-125">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a3c6c-126">使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="a3c6c-127">用于对包进行签名的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="a3c6c-128">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-128">Defaults to SHA256.</span></span> <span data-ttu-id="a3c6c-129">可能的值为 SHA256、SHA384 和 SHA512。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a3c6c-130">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a3c6c-131">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="a3c6c-132">指定应将已签名的包保存到的目录。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="a3c6c-133">默认情况下，已签名的包将覆盖原始包。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="a3c6c-134">切换以指示是否应覆盖当前签名。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="a3c6c-135">默认情况下，如果包已有签名，则该命令将失败。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="a3c6c-136">RFC 3161 时间戳服务器的 URL。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="a3c6c-137">RFC 3161 时间戳服务器使用的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="a3c6c-138">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a3c6c-139">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="a3c6c-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="a3c6c-140">示例</span><span class="sxs-lookup"><span data-stu-id="a3c6c-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
