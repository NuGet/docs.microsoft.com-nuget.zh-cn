---
title: NuGet CLI 验证命令
description: Nuget.exe 验证命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327494"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="710e1-103">verify 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="710e1-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="710e1-104">**适用于:** 包&bullet;使用**受支持的版本:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="710e1-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="710e1-105">验证包。</span><span class="sxs-lookup"><span data-stu-id="710e1-105">Verifies a package.</span></span>

<span data-ttu-id="710e1-106">在 .NET Core、Mono 或非 Windows 平台上, 尚不支持验证已签名的包。</span><span class="sxs-lookup"><span data-stu-id="710e1-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="710e1-107">用法</span><span class="sxs-lookup"><span data-stu-id="710e1-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="710e1-108">其中`<package(s)>` , 是一个或`.nupkg`多个文件。</span><span class="sxs-lookup"><span data-stu-id="710e1-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="710e1-109">nuget 验证-全部</span><span class="sxs-lookup"><span data-stu-id="710e1-109">nuget verify -All</span></span>

<span data-ttu-id="710e1-110">指定应在包上执行所有验证。</span><span class="sxs-lookup"><span data-stu-id="710e1-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="710e1-111">nuget 验证-签名</span><span class="sxs-lookup"><span data-stu-id="710e1-111">nuget verify -Signatures</span></span>

<span data-ttu-id="710e1-112">指定应执行的包签名验证。</span><span class="sxs-lookup"><span data-stu-id="710e1-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="710e1-113">用于 "验证-签名" 的选项</span><span class="sxs-lookup"><span data-stu-id="710e1-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="710e1-114">选项</span><span class="sxs-lookup"><span data-stu-id="710e1-114">Option</span></span> | <span data-ttu-id="710e1-115">描述</span><span class="sxs-lookup"><span data-stu-id="710e1-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="710e1-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="710e1-116">CertificateFingerprint</span></span> | <span data-ttu-id="710e1-117">指定一个或多个证书的一个或多256个证书指纹, 证书必须用来签名包。</span><span class="sxs-lookup"><span data-stu-id="710e1-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="710e1-118">证书 256 SHA-1 指纹是证书的 SHA-256 哈希。</span><span class="sxs-lookup"><span data-stu-id="710e1-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="710e1-119">多个输入应以分号分隔。</span><span class="sxs-lookup"><span data-stu-id="710e1-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="710e1-120">选项</span><span class="sxs-lookup"><span data-stu-id="710e1-120">Options</span></span>

| <span data-ttu-id="710e1-121">选项</span><span class="sxs-lookup"><span data-stu-id="710e1-121">Option</span></span> | <span data-ttu-id="710e1-122">描述</span><span class="sxs-lookup"><span data-stu-id="710e1-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="710e1-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="710e1-123">ConfigFile</span></span> | <span data-ttu-id="710e1-124">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="710e1-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="710e1-125">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="710e1-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="710e1-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="710e1-126">ForceEnglishOutput</span></span> | <span data-ttu-id="710e1-127">使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="710e1-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="710e1-128">Help</span><span class="sxs-lookup"><span data-stu-id="710e1-128">Help</span></span> | <span data-ttu-id="710e1-129">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="710e1-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="710e1-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="710e1-130">Verbosity</span></span> | <span data-ttu-id="710e1-131">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="710e1-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="710e1-132">示例</span><span class="sxs-lookup"><span data-stu-id="710e1-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```