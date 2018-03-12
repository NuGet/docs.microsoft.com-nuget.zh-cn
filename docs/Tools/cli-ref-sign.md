---
title: "NuGet CLI 登录命令 |Microsoft 文档"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 登录命令参考"
keywords: "nuget 符号引用，登录命令"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 109b0f6aca0ebaae2ea56fbb45226bc1b14f2ea1
ms.sourcegitcommit: df7158169e84900d135416cd5e52f937df0beb52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="54b39-104">登录命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="54b39-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="54b39-105">**适用于：** ，创建包&bullet;**受支持的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="54b39-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="54b39-106">对匹配的第一个参数使用证书的所有包进行都签名。</span><span class="sxs-lookup"><span data-stu-id="54b39-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="54b39-107">从文件或从安装在证书存储区中，通过提供使用者名称或指纹的证书，则可以获取具有私钥的证书。</span><span class="sxs-lookup"><span data-stu-id="54b39-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="54b39-108">包签名尚不支持在 Mono 下或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="54b39-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="54b39-109">用法</span><span class="sxs-lookup"><span data-stu-id="54b39-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="54b39-110">其中`<package(s)>`一个或多个`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="54b39-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="54b39-111">选项</span><span class="sxs-lookup"><span data-stu-id="54b39-111">Options</span></span>

| <span data-ttu-id="54b39-112">选项</span><span class="sxs-lookup"><span data-stu-id="54b39-112">Option</span></span> | <span data-ttu-id="54b39-113">描述</span><span class="sxs-lookup"><span data-stu-id="54b39-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54b39-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="54b39-114">CertificateFingerprint</span></span> | <span data-ttu-id="54b39-115">指定用于搜索的证书的本地证书存储区的证书的 sha-1 指纹。</span><span class="sxs-lookup"><span data-stu-id="54b39-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="54b39-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="54b39-116">CertificatePassword</span></span> | <span data-ttu-id="54b39-117">如果需要请指定证书密码。</span><span class="sxs-lookup"><span data-stu-id="54b39-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="54b39-118">如果证书受密码保护，但提供没有密码，该命令将提示输入密码在运行时，除非-非交互式选项传递。</span><span class="sxs-lookup"><span data-stu-id="54b39-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="54b39-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="54b39-119">CertificatePath</span></span> | <span data-ttu-id="54b39-120">指定要用于对包进行签名的证书的文件路径。</span><span class="sxs-lookup"><span data-stu-id="54b39-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="54b39-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="54b39-121">CertificateStoreLocation</span></span> | <span data-ttu-id="54b39-122">指定与 X.509 证书存储用于搜索该证书的名称。</span><span class="sxs-lookup"><span data-stu-id="54b39-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="54b39-123">默认值为"CurrentUser"，使用当前用户的 X.509 证书存储区。</span><span class="sxs-lookup"><span data-stu-id="54b39-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="54b39-124">指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。</span><span class="sxs-lookup"><span data-stu-id="54b39-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="54b39-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="54b39-125">CertificateStoreName</span></span> | <span data-ttu-id="54b39-126">指定要用于搜索该证书的 X.509 证书存储区的名称。</span><span class="sxs-lookup"><span data-stu-id="54b39-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="54b39-127">默认值为"My"，个人证书的 X.509 证书存储。</span><span class="sxs-lookup"><span data-stu-id="54b39-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="54b39-128">指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。</span><span class="sxs-lookup"><span data-stu-id="54b39-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="54b39-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="54b39-129">CertificateSubjectName</span></span> | <span data-ttu-id="54b39-130">指定用于搜索的证书的本地证书存储区的证书的使用者名称。</span><span class="sxs-lookup"><span data-stu-id="54b39-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="54b39-131">搜索不使用所提供的值，将查找所有证书使用者名称为包含该字符串，而不考虑其他使用者值不区分大小写的字符串比较。</span><span class="sxs-lookup"><span data-stu-id="54b39-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="54b39-132">可以通过-CertificateStoreName 和-CertificateStoreLocation 选项指定的证书存储区。</span><span class="sxs-lookup"><span data-stu-id="54b39-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="54b39-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="54b39-133">ConfigFile</span></span> | <span data-ttu-id="54b39-134">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="54b39-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="54b39-135">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="54b39-135">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="54b39-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="54b39-136">ForceEnglishOutput</span></span> | <span data-ttu-id="54b39-137">强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="54b39-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="54b39-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="54b39-138">HashAlgorithm</span></span> | <span data-ttu-id="54b39-139">要用于对包进行签名的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="54b39-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="54b39-140">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="54b39-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="54b39-141">帮助</span><span class="sxs-lookup"><span data-stu-id="54b39-141">Help</span></span> | <span data-ttu-id="54b39-142">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="54b39-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="54b39-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="54b39-143">NonInteractive</span></span> | <span data-ttu-id="54b39-144">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="54b39-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="54b39-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="54b39-145">OutputDirectory</span></span> | <span data-ttu-id="54b39-146">指定保存签名的包的目录。</span><span class="sxs-lookup"><span data-stu-id="54b39-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="54b39-147">默认情况下已签名的软件包的情况下会覆盖原始包。</span><span class="sxs-lookup"><span data-stu-id="54b39-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="54b39-148">Overwrite</span><span class="sxs-lookup"><span data-stu-id="54b39-148">Overwrite</span></span> | <span data-ttu-id="54b39-149">开关，这表示是否应覆盖当前的签名。</span><span class="sxs-lookup"><span data-stu-id="54b39-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="54b39-150">默认情况下如果包已签名，则该命令将失败。</span><span class="sxs-lookup"><span data-stu-id="54b39-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="54b39-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="54b39-151">Timestamper</span></span> | <span data-ttu-id="54b39-152">到 RFC 3161 时间戳服务器的 URL。</span><span class="sxs-lookup"><span data-stu-id="54b39-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="54b39-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="54b39-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="54b39-154">要由 RFC 3161 时间戳服务器的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="54b39-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="54b39-155">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="54b39-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="54b39-156">详细级别</span><span class="sxs-lookup"><span data-stu-id="54b39-156">Verbosity</span></span> | <span data-ttu-id="54b39-157">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="54b39-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="54b39-158">示例</span><span class="sxs-lookup"><span data-stu-id="54b39-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```