---
title: NuGet CLI 验证命令
description: nuget.exe verify 命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622598"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="9b1ee-103"> (NuGet CLI 验证命令) </span><span class="sxs-lookup"><span data-stu-id="9b1ee-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="9b1ee-104">**适用于：** 包使用 &bullet; **受支持的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="9b1ee-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="9b1ee-105">验证包。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-105">Verifies a package.</span></span>

<span data-ttu-id="9b1ee-106">在 .NET Core、Mono 或非 Windows 平台上，尚不支持验证已签名的包。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="9b1ee-107">使用情况</span><span class="sxs-lookup"><span data-stu-id="9b1ee-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="9b1ee-108">其中 `<package(s)>` ，是一个或多个 `.nupkg` 文件。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="9b1ee-109">nuget 验证-全部</span><span class="sxs-lookup"><span data-stu-id="9b1ee-109">nuget verify -All</span></span>

<span data-ttu-id="9b1ee-110">指定应在)  (上执行所有验证。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="9b1ee-111">nuget 验证-签名</span><span class="sxs-lookup"><span data-stu-id="9b1ee-111">nuget verify -Signatures</span></span>

<span data-ttu-id="9b1ee-112">指定应执行的包签名验证。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="9b1ee-113">用于 "验证-签名" 的选项</span><span class="sxs-lookup"><span data-stu-id="9b1ee-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="9b1ee-114">指定一个或多256个证书证书指纹 (s，) 必须用来签署哪些签名包。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="9b1ee-115">证书 256 SHA-1 指纹是证书的 SHA-256 哈希。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="9b1ee-116">多个输入应以分号分隔。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="9b1ee-117">选项</span><span class="sxs-lookup"><span data-stu-id="9b1ee-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="9b1ee-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9b1ee-119">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="9b1ee-120">使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="9b1ee-121">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="9b1ee-122">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="9b1ee-123">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="9b1ee-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="9b1ee-124">示例</span><span class="sxs-lookup"><span data-stu-id="9b1ee-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```