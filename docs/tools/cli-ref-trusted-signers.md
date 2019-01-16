---
title: 受信任的签名者的 NuGet CLI 命令
description: Nuget.exe 受信任的签名者命令参考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324703"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="03566-103">受信任的签名者命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="03566-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="03566-104">**适用于：** 打包消耗&bullet;**受支持的版本：** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="03566-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="03566-105">获取或设置 NuGet 配置受信任的签名者。</span><span class="sxs-lookup"><span data-stu-id="03566-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="03566-106">有关其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="03566-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="03566-107">有关详细信息如何 nuget.config 架构看起来，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="03566-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="03566-108">用法</span><span class="sxs-lookup"><span data-stu-id="03566-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="03566-109">如果没有`list|add|remove|sync`指定，则该命令将默认为`list`。</span><span class="sxs-lookup"><span data-stu-id="03566-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="03566-110">nuget 受信任的签名者列表</span><span class="sxs-lookup"><span data-stu-id="03566-110">nuget trusted-signers list</span></span>

<span data-ttu-id="03566-111">列出了在配置中所有受信任的签名者。</span><span class="sxs-lookup"><span data-stu-id="03566-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="03566-112">此选项将包括所有证书 （具有指纹和指纹算法） 具有每个签名者。</span><span class="sxs-lookup"><span data-stu-id="03566-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="03566-113">如果证书具有前面`[U]`，则意味着证书条目已`allowUntrustedRoot`设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="03566-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="03566-114">下面是此命令的示例输出：</span><span class="sxs-lookup"><span data-stu-id="03566-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="03566-115">nuget 受信任的签名添加 [选项]</span><span class="sxs-lookup"><span data-stu-id="03566-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="03566-116">将具有给定名称信任的签名添加到配置。此选项具有不同的手势，若要添加受信任的作者或存储库。</span><span class="sxs-lookup"><span data-stu-id="03566-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="03566-117">添加基于包的选项</span><span class="sxs-lookup"><span data-stu-id="03566-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="03566-118">其中`<package(s)>`是一个或多个`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="03566-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="03566-119">选项</span><span class="sxs-lookup"><span data-stu-id="03566-119">Option</span></span> | <span data-ttu-id="03566-120">描述</span><span class="sxs-lookup"><span data-stu-id="03566-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03566-121">作者</span><span class="sxs-lookup"><span data-stu-id="03566-121">Author</span></span> | <span data-ttu-id="03566-122">指定应受信任的程序包作者签名。</span><span class="sxs-lookup"><span data-stu-id="03566-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="03566-123">存储库</span><span class="sxs-lookup"><span data-stu-id="03566-123">Repository</span></span> | <span data-ttu-id="03566-124">指定的存储库签名或副署的包应为受信任。</span><span class="sxs-lookup"><span data-stu-id="03566-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="03566-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="03566-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="03566-126">指定是否应链接到不受信任的根允许受信任的签名者的证书。</span><span class="sxs-lookup"><span data-stu-id="03566-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="03566-127">Owners</span><span class="sxs-lookup"><span data-stu-id="03566-127">Owners</span></span> | <span data-ttu-id="03566-128">受信任的所有者来进一步限制的信任存储库的以分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="03566-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="03566-129">仅在使用时有效`-Repository`选项。</span><span class="sxs-lookup"><span data-stu-id="03566-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="03566-130">同时提供`-Author`和`-Repository`不支持在同一时间。</span><span class="sxs-lookup"><span data-stu-id="03566-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="03566-131">添加基于服务索引的选项</span><span class="sxs-lookup"><span data-stu-id="03566-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="03566-132">_说明_：此选项将仅添加受信任的存储库。</span><span class="sxs-lookup"><span data-stu-id="03566-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="03566-133">选项</span><span class="sxs-lookup"><span data-stu-id="03566-133">Option</span></span> | <span data-ttu-id="03566-134">描述</span><span class="sxs-lookup"><span data-stu-id="03566-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03566-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="03566-135">ServiceIndex</span></span> | <span data-ttu-id="03566-136">指定要为受信任的存储库的 V3 服务索引。</span><span class="sxs-lookup"><span data-stu-id="03566-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="03566-137">此存储库必须支持存储库签名资源。</span><span class="sxs-lookup"><span data-stu-id="03566-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="03566-138">如果未提供，该命令将查找具有相同的包源`-Name`并从中获取服务索引。</span><span class="sxs-lookup"><span data-stu-id="03566-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="03566-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="03566-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="03566-140">指定是否应链接到不受信任的根允许受信任的签名者的证书。</span><span class="sxs-lookup"><span data-stu-id="03566-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="03566-141">Owners</span><span class="sxs-lookup"><span data-stu-id="03566-141">Owners</span></span> | <span data-ttu-id="03566-142">受信任的所有者来进一步限制的信任存储库的以分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="03566-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="03566-143">添加根据证书信息的选项</span><span class="sxs-lookup"><span data-stu-id="03566-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="03566-144">_说明_：如果已存在具有给定名称信任的签名，则证书项将添加到该签名者。</span><span class="sxs-lookup"><span data-stu-id="03566-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="03566-145">否则将使用证书项目中创建受信任的作者从给定的证书信息。</span><span class="sxs-lookup"><span data-stu-id="03566-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="03566-146">选项</span><span class="sxs-lookup"><span data-stu-id="03566-146">Option</span></span> | <span data-ttu-id="03566-147">描述</span><span class="sxs-lookup"><span data-stu-id="03566-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03566-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="03566-148">CertificateFingerprint</span></span> | <span data-ttu-id="03566-149">指定必须使用签名的已签名的包的证书指纹的证书。</span><span class="sxs-lookup"><span data-stu-id="03566-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="03566-150">证书指纹是证书的哈希。</span><span class="sxs-lookup"><span data-stu-id="03566-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="03566-151">在指定的哈希算法用于计算此哈希值应为`FingerprintAlgorithm`选项。</span><span class="sxs-lookup"><span data-stu-id="03566-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="03566-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="03566-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="03566-153">指定用于计算证书指纹的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="03566-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="03566-154">默认为 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="03566-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="03566-155">支持的值为`SHA256`，`SHA384`和 `SHA512`</span><span class="sxs-lookup"><span data-stu-id="03566-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="03566-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="03566-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="03566-157">指定是否应链接到不受信任的根允许受信任的签名者的证书。</span><span class="sxs-lookup"><span data-stu-id="03566-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="03566-158">nuget 受信任的签名 remove-名称 <name></span><span class="sxs-lookup"><span data-stu-id="03566-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="03566-159">删除任何受信任的签名者与给定名称匹配。</span><span class="sxs-lookup"><span data-stu-id="03566-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="03566-160">nuget 受信任的签名同步-名称 <name></span><span class="sxs-lookup"><span data-stu-id="03566-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="03566-161">请求的证书在当前受信任的存储库中用于更新的最新列表中受信任的签名者的现有证书列表。</span><span class="sxs-lookup"><span data-stu-id="03566-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="03566-162">_说明_：此笔势将删除当前证书的列表，并替换存储库中的最新列表。</span><span class="sxs-lookup"><span data-stu-id="03566-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="03566-163">选项</span><span class="sxs-lookup"><span data-stu-id="03566-163">Options</span></span>

| <span data-ttu-id="03566-164">选项</span><span class="sxs-lookup"><span data-stu-id="03566-164">Option</span></span> | <span data-ttu-id="03566-165">描述</span><span class="sxs-lookup"><span data-stu-id="03566-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03566-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="03566-166">ConfigFile</span></span> | <span data-ttu-id="03566-167">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="03566-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="03566-168">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="03566-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="03566-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="03566-169">ForceEnglishOutput</span></span> | <span data-ttu-id="03566-170">强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="03566-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="03566-171">帮助</span><span class="sxs-lookup"><span data-stu-id="03566-171">Help</span></span> | <span data-ttu-id="03566-172">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="03566-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="03566-173">详细级别</span><span class="sxs-lookup"><span data-stu-id="03566-173">Verbosity</span></span> | <span data-ttu-id="03566-174">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="03566-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="03566-175">示例</span><span class="sxs-lookup"><span data-stu-id="03566-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
