---
title: NuGet CLI 验证命令
description: 参考 nuget.exe 验证命令
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="c607b-103">verify 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c607b-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="c607b-104">**适用于：** 打包消耗&bullet;**受支持的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="c607b-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="c607b-105">验证包。</span><span class="sxs-lookup"><span data-stu-id="c607b-105">Verifies a package.</span></span>

<span data-ttu-id="c607b-106">在.NET 核心，Mono、 下或在非 Windows 平台上尚不支持验证的已签名的软件包。</span><span class="sxs-lookup"><span data-stu-id="c607b-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="c607b-107">用法</span><span class="sxs-lookup"><span data-stu-id="c607b-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="c607b-108">其中`<package(s)>`一个或多个`.nupkg`文件。</span><span class="sxs-lookup"><span data-stu-id="c607b-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="c607b-109">nuget 验证-所有</span><span class="sxs-lookup"><span data-stu-id="c607b-109">nuget verify -All</span></span>

<span data-ttu-id="c607b-110">指定所有验证可能，应都执行的程序包。</span><span class="sxs-lookup"><span data-stu-id="c607b-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="c607b-111">nuget 验证的签名</span><span class="sxs-lookup"><span data-stu-id="c607b-111">nuget verify -Signatures</span></span>

<span data-ttu-id="c607b-112">指定应执行包签名验证。</span><span class="sxs-lookup"><span data-stu-id="c607b-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="c607b-113">"验证的签名"的选项</span><span class="sxs-lookup"><span data-stu-id="c607b-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="c607b-114">选项</span><span class="sxs-lookup"><span data-stu-id="c607b-114">Option</span></span> | <span data-ttu-id="c607b-115">描述</span><span class="sxs-lookup"><span data-stu-id="c607b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c607b-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="c607b-116">CertificateFingerprint</span></span> | <span data-ttu-id="c607b-117">指定一个或多个 sha-256 证书指纹的证书 (s) 必须使用签名的已签名的软件包。</span><span class="sxs-lookup"><span data-stu-id="c607b-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="c607b-118">Sha-256 证书指纹是该证书的 sha-256 哈希。</span><span class="sxs-lookup"><span data-stu-id="c607b-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="c607b-119">多个输入应为以分号分隔。</span><span class="sxs-lookup"><span data-stu-id="c607b-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="c607b-120">选项</span><span class="sxs-lookup"><span data-stu-id="c607b-120">Options</span></span>

| <span data-ttu-id="c607b-121">选项</span><span class="sxs-lookup"><span data-stu-id="c607b-121">Option</span></span> | <span data-ttu-id="c607b-122">描述</span><span class="sxs-lookup"><span data-stu-id="c607b-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c607b-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c607b-123">ConfigFile</span></span> | <span data-ttu-id="c607b-124">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c607b-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c607b-125">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="c607b-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c607b-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c607b-126">ForceEnglishOutput</span></span> | <span data-ttu-id="c607b-127">强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="c607b-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c607b-128">帮助</span><span class="sxs-lookup"><span data-stu-id="c607b-128">Help</span></span> | <span data-ttu-id="c607b-129">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c607b-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="c607b-130">详细级别</span><span class="sxs-lookup"><span data-stu-id="c607b-130">Verbosity</span></span> | <span data-ttu-id="c607b-131">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="c607b-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="c607b-132">示例</span><span class="sxs-lookup"><span data-stu-id="c607b-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```