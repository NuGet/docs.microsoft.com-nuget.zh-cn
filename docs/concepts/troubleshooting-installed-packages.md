---
title: 对安装包进行故障排除
description: 如何查找用于各个包的包源
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387528"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="73ab6-103">对安装包进行故障排除</span><span class="sxs-lookup"><span data-stu-id="73ab6-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="73ab6-104">有时，你可能想要验证从中安装特定包的源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="73ab6-105">下面是一些可以用来检验的方法。</span><span class="sxs-lookup"><span data-stu-id="73ab6-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="73ab6-106">某些包源支持称为上游源的概念。</span><span class="sxs-lookup"><span data-stu-id="73ab6-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="73ab6-107">例如，[Azure Artifacts 上游源](/azure/devops/artifacts/concepts/upstream-sources)。</span><span class="sxs-lookup"><span data-stu-id="73ab6-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="73ab6-108">NuGet 客户端不知道包是否来自上游源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="73ab6-109">因此，包源的任何日志记录将列出配置的源，而不是上游源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="73ab6-110">全局包文件夹中的 `.nupkg.metadata` 文件</span><span class="sxs-lookup"><span data-stu-id="73ab6-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="73ab6-111">将包提取到“global-packages”文件夹时，将写入一个 `.nupkg.metadata` 文件。</span><span class="sxs-lookup"><span data-stu-id="73ab6-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="73ab6-112">从 NuGet 5.9.0 开始，NuGet 将添加包源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="73ab6-113">请参阅下面的说明，将 NuGet 版本映射到 Visual Studio 或 .NET SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="73ab6-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="73ab6-114">例如：</span><span class="sxs-lookup"><span data-stu-id="73ab6-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="73ab6-115">如果在升级到具有 NuGet 5.9.0 的更新版本的工具之前，“global-packages”文件夹中的包已被提取，则 `.nupkg.metadata` 文件将为版本 1 并且不包含包源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="73ab6-116">你可以[清除“global-packages”文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)，以确保所有包都将包含包源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="73ab6-117">NuGet 仅将 `.nupkg.metadata` 文件写入到“global-packages”文件夹。</span><span class="sxs-lookup"><span data-stu-id="73ab6-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="73ab6-118">使用 `packages.config` 的项目使用“solution packages”文件夹，该文件夹不会创建 `.nupkg.metadata` 文件。</span><span class="sxs-lookup"><span data-stu-id="73ab6-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="73ab6-119">已安装包的日志消息</span><span class="sxs-lookup"><span data-stu-id="73ab6-119">Installed package log message</span></span>

<span data-ttu-id="73ab6-120">从 NuGet 5.9.0 开始，NuGet 将在还原消息中输出包源，通知已安装包。</span><span class="sxs-lookup"><span data-stu-id="73ab6-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="73ab6-121">例如：</span><span class="sxs-lookup"><span data-stu-id="73ab6-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="73ab6-122">此消息在正常/信息性详细程度下输出。</span><span class="sxs-lookup"><span data-stu-id="73ab6-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="73ab6-123">Visual Studio 和 `dotnet` CLI 默认为最小详细程度，因此在默认情况下，此消息不可见。</span><span class="sxs-lookup"><span data-stu-id="73ab6-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="73ab6-124">`msbuild` 和 `nuget` CLI 默认为正常详细程度，因此在默认情况下，此消息可见。</span><span class="sxs-lookup"><span data-stu-id="73ab6-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="73ab6-125">HTTP 日志消息</span><span class="sxs-lookup"><span data-stu-id="73ab6-125">HTTP log message</span></span>

<span data-ttu-id="73ab6-126">当包在本地不可用时，无论是在“global-packages”文件夹、回退文件夹还是本地文件源中，NuGet 都将通过 HTTP 从任何已配置的包源下载包。</span><span class="sxs-lookup"><span data-stu-id="73ab6-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="73ab6-127">HTTP 请求和响应在正常详细程度下记录，并且每个包版本只应显示单个请求和响应。</span><span class="sxs-lookup"><span data-stu-id="73ab6-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="73ab6-128">例如：</span><span class="sxs-lookup"><span data-stu-id="73ab6-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="73ab6-129">如果是在最近下载了这些文件，则可以从 NuGet 的“http-cache”中检索它们</span><span class="sxs-lookup"><span data-stu-id="73ab6-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="73ab6-130">不同 NuGet HTTP 服务器实现的 URL 格式可能不同，无论它是在实现 NuGet V2 还是 V3 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="73ab6-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="73ab6-131">如果 `nuget.config` 定义了多个 HTTP 源，则将看到对每个包的 `index.json` 文件的多个请求，一个请求对应一个源。</span><span class="sxs-lookup"><span data-stu-id="73ab6-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="73ab6-132">但对于包的每个版本，都只有一个 `nupkg` 下载。</span><span class="sxs-lookup"><span data-stu-id="73ab6-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="73ab6-133">包签名日志消息</span><span class="sxs-lookup"><span data-stu-id="73ab6-133">Package signature log message</span></span>

<span data-ttu-id="73ab6-134">如果要下载的包已签名，NuGet 将验证签名，并以详细的详细程度记录以下消息：</span><span class="sxs-lookup"><span data-stu-id="73ab6-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="73ab6-135">无论是从 HTTP 包源下载包，还是从本地包源复制包，都将报告此消息。</span><span class="sxs-lookup"><span data-stu-id="73ab6-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="73ab6-136">如果包已存在于“global-packages”文件夹或回退文件夹中，则不会输出此消息。</span><span class="sxs-lookup"><span data-stu-id="73ab6-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="73ab6-137">由于[删除了对 VeriSign CA 的信任](https://github.com/dotnet/announcements/issues/180)，因此 NuGet 已在某些平台上、某些版本的的 NuGet 和 .NET SDK 中禁用了签名包验证。</span><span class="sxs-lookup"><span data-stu-id="73ab6-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="73ab6-138">因此，相同的包可能包含 `PackageSignatureVerificationLog` 日志，或者可能缺少这些日志，具体取决于要还原的平台以及所使用的 .NET 或 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="73ab6-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="73ab6-139">NuGet 版本映射</span><span class="sxs-lookup"><span data-stu-id="73ab6-139">NuGet Version Map</span></span>

<span data-ttu-id="73ab6-140">以下版本的 NuGet 在包源日志记录方面有重要更改：</span><span class="sxs-lookup"><span data-stu-id="73ab6-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="73ab6-141">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="73ab6-141">NuGet Version</span></span>|<span data-ttu-id="73ab6-142">Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="73ab6-142">Visual Studio Version</span></span>|<span data-ttu-id="73ab6-143">.NET SDK 版本</span><span class="sxs-lookup"><span data-stu-id="73ab6-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="73ab6-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="73ab6-144">NuGet 5.9.0</span></span>|<span data-ttu-id="73ab6-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="73ab6-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="73ab6-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="73ab6-146">.NET 5 SDK 5.0.200</span></span>|
