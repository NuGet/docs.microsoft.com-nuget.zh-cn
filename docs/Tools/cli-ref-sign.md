---
title: NuGet CLI 登录命令
description: Nuget.exe 登录命令参考
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="75bf6-103">登录命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75bf6-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="75bf6-104">**适用于：** ，创建包&bullet;**受支持的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="75bf6-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="75bf6-105">对匹配的第一个参数使用证书的所有包进行都签名。</span><span class="sxs-lookup"><span data-stu-id="75bf6-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="75bf6-106">从文件或从安装在证书存储区中，通过提供使用者名称或指纹的证书，则可以获取具有私钥的证书。</span><span class="sxs-lookup"><span data-stu-id="75bf6-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="75bf6-107">包签名尚不支持在.NET 核心，Mono、 下或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="75bf6-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="75bf6-108">用法</span><span class="sxs-lookup"><span data-stu-id="75bf6-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="75bf6-109">其中`<package(s)>`一个或多个`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="75bf6-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="75bf6-110">选项</span><span class="sxs-lookup"><span data-stu-id="75bf6-110">Options</span></span>

| <span data-ttu-id="75bf6-111">选项</span><span class="sxs-lookup"><span data-stu-id="75bf6-111">Option</span></span> | <span data-ttu-id="75bf6-112">描述</span><span class="sxs-lookup"><span data-stu-id="75bf6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75bf6-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="75bf6-113">CertificateFingerprint</span></span> | <span data-ttu-id="75bf6-114">指定用于搜索的证书的本地证书存储区的证书的 sha-1 指纹。</span><span class="sxs-lookup"><span data-stu-id="75bf6-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="75bf6-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="75bf6-115">CertificatePassword</span></span> | <span data-ttu-id="75bf6-116">如果需要请指定证书密码。</span><span class="sxs-lookup"><span data-stu-id="75bf6-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="75bf6-117">如果证书受密码保护，但提供没有密码，该命令将提示输入密码在运行时，除非-非交互式选项传递。</span><span class="sxs-lookup"><span data-stu-id="75bf6-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="75bf6-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="75bf6-118">CertificatePath</span></span> | <span data-ttu-id="75bf6-119">指定要用于对包进行签名的证书的文件路径。</span><span class="sxs-lookup"><span data-stu-id="75bf6-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="75bf6-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="75bf6-120">CertificateStoreLocation</span></span> | <span data-ttu-id="75bf6-121">指定与 X.509 证书存储用于搜索该证书的名称。</span><span class="sxs-lookup"><span data-stu-id="75bf6-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="75bf6-122">默认值为"CurrentUser"，使用当前用户的 X.509 证书存储区。</span><span class="sxs-lookup"><span data-stu-id="75bf6-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="75bf6-123">指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。</span><span class="sxs-lookup"><span data-stu-id="75bf6-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="75bf6-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="75bf6-124">CertificateStoreName</span></span> | <span data-ttu-id="75bf6-125">指定要用于搜索该证书的 X.509 证书存储区的名称。</span><span class="sxs-lookup"><span data-stu-id="75bf6-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="75bf6-126">默认值为"My"，个人证书的 X.509 证书存储。</span><span class="sxs-lookup"><span data-stu-id="75bf6-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="75bf6-127">指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。</span><span class="sxs-lookup"><span data-stu-id="75bf6-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="75bf6-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="75bf6-128">CertificateSubjectName</span></span> | <span data-ttu-id="75bf6-129">指定用于搜索的证书的本地证书存储区的证书的使用者名称。</span><span class="sxs-lookup"><span data-stu-id="75bf6-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="75bf6-130">搜索不使用所提供的值，将查找所有证书使用者名称为包含该字符串，而不考虑其他使用者值不区分大小写的字符串比较。</span><span class="sxs-lookup"><span data-stu-id="75bf6-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="75bf6-131">可以通过-CertificateStoreName 和-CertificateStoreLocation 选项指定的证书存储区。</span><span class="sxs-lookup"><span data-stu-id="75bf6-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="75bf6-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="75bf6-132">ConfigFile</span></span> | <span data-ttu-id="75bf6-133">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="75bf6-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="75bf6-134">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="75bf6-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="75bf6-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75bf6-135">ForceEnglishOutput</span></span> | <span data-ttu-id="75bf6-136">强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="75bf6-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75bf6-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="75bf6-137">HashAlgorithm</span></span> | <span data-ttu-id="75bf6-138">要用于对包进行签名的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="75bf6-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="75bf6-139">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="75bf6-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="75bf6-140">帮助</span><span class="sxs-lookup"><span data-stu-id="75bf6-140">Help</span></span> | <span data-ttu-id="75bf6-141">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="75bf6-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="75bf6-142">非交互式</span><span class="sxs-lookup"><span data-stu-id="75bf6-142">NonInteractive</span></span> | <span data-ttu-id="75bf6-143">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="75bf6-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="75bf6-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="75bf6-144">OutputDirectory</span></span> | <span data-ttu-id="75bf6-145">指定保存签名的包的目录。</span><span class="sxs-lookup"><span data-stu-id="75bf6-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="75bf6-146">默认情况下已签名的软件包的情况下会覆盖原始包。</span><span class="sxs-lookup"><span data-stu-id="75bf6-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="75bf6-147">Overwrite</span><span class="sxs-lookup"><span data-stu-id="75bf6-147">Overwrite</span></span> | <span data-ttu-id="75bf6-148">开关，这表示是否应覆盖当前的签名。</span><span class="sxs-lookup"><span data-stu-id="75bf6-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="75bf6-149">默认情况下如果包已签名，则该命令将失败。</span><span class="sxs-lookup"><span data-stu-id="75bf6-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="75bf6-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="75bf6-150">Timestamper</span></span> | <span data-ttu-id="75bf6-151">到 RFC 3161 时间戳服务器的 URL。</span><span class="sxs-lookup"><span data-stu-id="75bf6-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="75bf6-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="75bf6-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="75bf6-153">要由 RFC 3161 时间戳服务器的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="75bf6-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="75bf6-154">默认值为 SHA256。</span><span class="sxs-lookup"><span data-stu-id="75bf6-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="75bf6-155">详细级别</span><span class="sxs-lookup"><span data-stu-id="75bf6-155">Verbosity</span></span> | <span data-ttu-id="75bf6-156">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="75bf6-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="75bf6-157">示例</span><span class="sxs-lookup"><span data-stu-id="75bf6-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```