---
title: NuGet CLI 受信任-签署者命令
description: 有关 nuget.exe 受信任的签名者的参考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610331"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="cc7d1-103">受信任的签名者命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="cc7d1-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="cc7d1-104">**适用于：** &bullet; 支持的**版本**的包使用： 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="cc7d1-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="cc7d1-105">获取或设置 NuGet 配置的受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="cc7d1-106">有关其他用法，请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cc7d1-107">有关 nuget.exe 架构的外观的详细信息，请参阅[nuget 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cc7d1-108">用法</span><span class="sxs-lookup"><span data-stu-id="cc7d1-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="cc7d1-109">如果未指定 `list|add|remove|sync`，则该命令将默认为 `list`。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="cc7d1-110">nuget 可信-签署者列表</span><span class="sxs-lookup"><span data-stu-id="cc7d1-110">nuget trusted-signers list</span></span>

<span data-ttu-id="cc7d1-111">列出配置中的所有受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="cc7d1-112">此选项将包含每个签名者的所有证书（具有指纹和指纹算法）。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="cc7d1-113">如果证书具有前面的 `[U]`，则表示证书条目的 `allowUntrustedRoot` 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="cc7d1-114">下面是此命令的示例输出：</span><span class="sxs-lookup"><span data-stu-id="cc7d1-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="cc7d1-115">nuget 可信-签署者添加 [选项]</span><span class="sxs-lookup"><span data-stu-id="cc7d1-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="cc7d1-116">向配置添加具有给定名称的受信任的签名者。此选项具有不同的手势来添加受信任的作者或存储库。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="cc7d1-117">基于包的 "添加" 选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="cc7d1-118">其中 `<package(s)>` 是一个或多个 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="cc7d1-119">选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-119">Option</span></span> | <span data-ttu-id="cc7d1-120">描述</span><span class="sxs-lookup"><span data-stu-id="cc7d1-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7d1-121">作者</span><span class="sxs-lookup"><span data-stu-id="cc7d1-121">Author</span></span> | <span data-ttu-id="cc7d1-122">指定应信任包的作者签名。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="cc7d1-123">存储库</span><span class="sxs-lookup"><span data-stu-id="cc7d1-123">Repository</span></span> | <span data-ttu-id="cc7d1-124">指定应信任包的存储库签名或副署。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="cc7d1-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cc7d1-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="cc7d1-126">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="cc7d1-127">Owners</span><span class="sxs-lookup"><span data-stu-id="cc7d1-127">Owners</span></span> | <span data-ttu-id="cc7d1-128">以分号分隔的受信任所有者列表，进一步限制了存储库的信任。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="cc7d1-129">仅在使用 `-Repository` 选项时有效。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="cc7d1-130">不支持同时提供 `-Author` 和 `-Repository`。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="cc7d1-131">基于服务索引添加的选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cc7d1-132">_注意_：此选项将只添加受信任的存储库。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="cc7d1-133">选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-133">Option</span></span> | <span data-ttu-id="cc7d1-134">描述</span><span class="sxs-lookup"><span data-stu-id="cc7d1-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7d1-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="cc7d1-135">ServiceIndex</span></span> | <span data-ttu-id="cc7d1-136">指定要信任的存储库的 V3 服务索引。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="cc7d1-137">此存储库必须支持存储库签名资源。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="cc7d1-138">如果未提供，则该命令将查找具有相同 `-Name` 的包源，并从中获取服务索引。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="cc7d1-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cc7d1-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="cc7d1-140">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="cc7d1-141">Owners</span><span class="sxs-lookup"><span data-stu-id="cc7d1-141">Owners</span></span> | <span data-ttu-id="cc7d1-142">以分号分隔的受信任所有者列表，进一步限制了存储库的信任。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="cc7d1-143">基于证书信息添加的选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cc7d1-144">_注意_：如果已存在具有给定名称的受信任的签名者，则会将证书项目添加到该签名者。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="cc7d1-145">否则，将创建一个受信任的作者，其中包含来自给定证书信息的证书项目。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="cc7d1-146">选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-146">Option</span></span> | <span data-ttu-id="cc7d1-147">描述</span><span class="sxs-lookup"><span data-stu-id="cc7d1-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7d1-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="cc7d1-148">CertificateFingerprint</span></span> | <span data-ttu-id="cc7d1-149">指定证书的证书指纹，必须使用该证书对签名的包进行签名。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="cc7d1-150">证书指纹是证书的哈希。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="cc7d1-151">用于计算此哈希的哈希算法应在 `FingerprintAlgorithm` 选项中指定。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="cc7d1-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="cc7d1-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="cc7d1-153">指定用于计算证书指纹的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="cc7d1-154">默认为 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="cc7d1-155">支持的值为 `SHA256`、`SHA384` 和 `SHA512`</span><span class="sxs-lookup"><span data-stu-id="cc7d1-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="cc7d1-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cc7d1-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="cc7d1-157">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="cc7d1-158">nuget 可信-签名者删除名称 \<名称\></span><span class="sxs-lookup"><span data-stu-id="cc7d1-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="cc7d1-159">删除任何与给定名称匹配的受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="cc7d1-160">nuget 可信-签署者同步-名称 \<名称\></span><span class="sxs-lookup"><span data-stu-id="cc7d1-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="cc7d1-161">请求当前受信任的存储库中使用的最新证书列表，以更新受信任的签名者中的现有证书列表。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="cc7d1-162">_注意_：此笔势将删除当前的证书列表，并将其替换为存储库中的最新列表。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="cc7d1-163">选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-163">Options</span></span>

| <span data-ttu-id="cc7d1-164">选项</span><span class="sxs-lookup"><span data-stu-id="cc7d1-164">Option</span></span> | <span data-ttu-id="cc7d1-165">描述</span><span class="sxs-lookup"><span data-stu-id="cc7d1-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc7d1-166">Read-configfile</span><span class="sxs-lookup"><span data-stu-id="cc7d1-166">ConfigFile</span></span> | <span data-ttu-id="cc7d1-167">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc7d1-168">如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cc7d1-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cc7d1-169">ForceEnglishOutput</span></span> | <span data-ttu-id="cc7d1-170">使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cc7d1-171">帮助</span><span class="sxs-lookup"><span data-stu-id="cc7d1-171">Help</span></span> | <span data-ttu-id="cc7d1-172">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc7d1-173">详细级别</span><span class="sxs-lookup"><span data-stu-id="cc7d1-173">Verbosity</span></span> | <span data-ttu-id="cc7d1-174">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="cc7d1-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="cc7d1-175">示例</span><span class="sxs-lookup"><span data-stu-id="cc7d1-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
