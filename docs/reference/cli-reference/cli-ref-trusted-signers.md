---
title: NuGet CLI 受信任-签署者命令
description: nuget.exe 受信任的签名者命令的参考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238148"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="511f1-103"> (NuGet CLI 的受信任的签名者命令) </span><span class="sxs-lookup"><span data-stu-id="511f1-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="511f1-104">**适用于：** 包使用 &bullet; **受支持的版本：** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="511f1-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="511f1-105">获取或设置 NuGet 配置的受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="511f1-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="511f1-106">有关其他用法，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="511f1-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="511f1-107">有关 nuget.config 架构的外观的详细信息，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="511f1-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="511f1-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="511f1-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="511f1-109">如果 `list|add|remove|sync` 未指定任何，则该命令将默认为 `list` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="511f1-110">nuget 可信-签署者列表</span><span class="sxs-lookup"><span data-stu-id="511f1-110">nuget trusted-signers list</span></span>

<span data-ttu-id="511f1-111">列出配置中的所有受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="511f1-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="511f1-112">此选项将包括每个签名者)  (具有指纹和指纹算法的所有证书。</span><span class="sxs-lookup"><span data-stu-id="511f1-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="511f1-113">如果证书前面有一个 `[U]` ，则表示证书项已 `allowUntrustedRoot` 设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="511f1-114">下面是此命令的示例输出：</span><span class="sxs-lookup"><span data-stu-id="511f1-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="511f1-115">nuget 可信-签署者添加 [选项]</span><span class="sxs-lookup"><span data-stu-id="511f1-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="511f1-116">向配置添加具有给定名称的受信任的签名者。此选项具有不同的手势来添加受信任的作者或存储库。</span><span class="sxs-lookup"><span data-stu-id="511f1-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="511f1-117">基于包的 "添加" 选项</span><span class="sxs-lookup"><span data-stu-id="511f1-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="511f1-118">其中 `<package(s)>` ，是一个或多个 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="511f1-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="511f1-119">指定应信任包 () 的作者签名。</span><span class="sxs-lookup"><span data-stu-id="511f1-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="511f1-120">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="511f1-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="511f1-121">以分号分隔的受信任所有者列表，进一步限制了存储库的信任。</span><span class="sxs-lookup"><span data-stu-id="511f1-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="511f1-122">仅在使用选项时有效 `-Repository` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="511f1-123">指定应信任包 (s) 的存储库签名或副署。</span><span class="sxs-lookup"><span data-stu-id="511f1-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="511f1-124">`-Author`不支持同时提供和 `-Repository` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="511f1-125">基于服务索引添加的选项</span><span class="sxs-lookup"><span data-stu-id="511f1-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="511f1-126">_注意_ ：此选项将只添加受信任的存储库。</span><span class="sxs-lookup"><span data-stu-id="511f1-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="511f1-127">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="511f1-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="511f1-128">以分号分隔的受信任所有者列表，进一步限制了存储库的信任。</span><span class="sxs-lookup"><span data-stu-id="511f1-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="511f1-129">指定要信任的存储库的 V3 服务索引。</span><span class="sxs-lookup"><span data-stu-id="511f1-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="511f1-130">此存储库必须支持存储库签名资源。</span><span class="sxs-lookup"><span data-stu-id="511f1-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="511f1-131">如果未提供，则该命令将查找具有相同的包源 `-Name` ，并从中获取服务索引。</span><span class="sxs-lookup"><span data-stu-id="511f1-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="511f1-132">基于证书信息添加的选项</span><span class="sxs-lookup"><span data-stu-id="511f1-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="511f1-133">_注意_ ：如果已存在具有给定名称的受信任的签名者，则会将证书项目添加到该签名者。</span><span class="sxs-lookup"><span data-stu-id="511f1-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="511f1-134">否则，将创建一个受信任的作者，其中包含来自给定证书信息的证书项目。</span><span class="sxs-lookup"><span data-stu-id="511f1-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="511f1-135">指定是否允许受信任的签名者的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="511f1-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="511f1-136">指定证书的证书指纹，必须使用该证书对签名的包进行签名。</span><span class="sxs-lookup"><span data-stu-id="511f1-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="511f1-137">证书指纹是证书的哈希。</span><span class="sxs-lookup"><span data-stu-id="511f1-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="511f1-138">用于计算此哈希的哈希算法应在选项中指定 `FingerprintAlgorithm` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="511f1-139">指定用于计算证书指纹的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="511f1-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="511f1-140">默认为 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="511f1-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="511f1-141">支持的值为 `SHA256` 、 `SHA384` 和 `SHA512` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="511f1-142">nuget 可信-签名者删除名称 \<name\></span><span class="sxs-lookup"><span data-stu-id="511f1-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="511f1-143">删除任何与给定名称匹配的受信任签署者。</span><span class="sxs-lookup"><span data-stu-id="511f1-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="511f1-144">nuget 可信-签署者同步名称 \<name\></span><span class="sxs-lookup"><span data-stu-id="511f1-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="511f1-145">请求当前受信任的存储库中使用的最新证书列表，以更新受信任的签名者中的现有证书列表。</span><span class="sxs-lookup"><span data-stu-id="511f1-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="511f1-146">_注意_ ：此笔势将删除当前的证书列表，并将其替换为存储库中的最新列表。</span><span class="sxs-lookup"><span data-stu-id="511f1-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="511f1-147">选项</span><span class="sxs-lookup"><span data-stu-id="511f1-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="511f1-148">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="511f1-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="511f1-149">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="511f1-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="511f1-150">使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="511f1-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="511f1-151">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="511f1-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="511f1-152">受信任的签名者的名称。</span><span class="sxs-lookup"><span data-stu-id="511f1-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="511f1-153">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="511f1-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="511f1-154">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="511f1-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="511f1-155">示例</span><span class="sxs-lookup"><span data-stu-id="511f1-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
