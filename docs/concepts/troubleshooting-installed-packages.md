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
# <a name="troubleshooting-installed-packages"></a>对安装包进行故障排除

有时，你可能想要验证从中安装特定包的源。 下面是一些可以用来检验的方法。

> [!Note]
> 某些包源支持称为上游源的概念。 例如，[Azure Artifacts 上游源](/azure/devops/artifacts/concepts/upstream-sources)。 NuGet 客户端不知道包是否来自上游源。 因此，包源的任何日志记录将列出配置的源，而不是上游源。

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>全局包文件夹中的 `.nupkg.metadata` 文件

将包提取到“global-packages”文件夹时，将写入一个 `.nupkg.metadata` 文件。 从 NuGet 5.9.0 开始，NuGet 将添加包源。 请参阅下面的说明，将 NuGet 版本映射到 Visual Studio 或 .NET SDK 版本。 例如：

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> 如果在升级到具有 NuGet 5.9.0 的更新版本的工具之前，“global-packages”文件夹中的包已被提取，则 `.nupkg.metadata` 文件将为版本 1 并且不包含包源。 你可以[清除“global-packages”文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)，以确保所有包都将包含包源。

> [!Tip]
> NuGet 仅将 `.nupkg.metadata` 文件写入到“global-packages”文件夹。 使用 `packages.config` 的项目使用“solution packages”文件夹，该文件夹不会创建 `.nupkg.metadata` 文件。

## <a name="installed-package-log-message"></a>已安装包的日志消息

从 NuGet 5.9.0 开始，NuGet 将在还原消息中输出包源，通知已安装包。 例如：

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> 此消息在正常/信息性详细程度下输出。 Visual Studio 和 `dotnet` CLI 默认为最小详细程度，因此在默认情况下，此消息不可见。 `msbuild` 和 `nuget` CLI 默认为正常详细程度，因此在默认情况下，此消息可见。

## <a name="http-log-message"></a>HTTP 日志消息

当包在本地不可用时，无论是在“global-packages”文件夹、回退文件夹还是本地文件源中，NuGet 都将通过 HTTP 从任何已配置的包源下载包。 HTTP 请求和响应在正常详细程度下记录，并且每个包版本只应显示单个请求和响应。 例如：

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

如果是在最近下载了这些文件，则可以从 NuGet 的“http-cache”中检索它们

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

不同 NuGet HTTP 服务器实现的 URL 格式可能不同，无论它是在实现 NuGet V2 还是 V3 HTTP 协议。

如果 `nuget.config` 定义了多个 HTTP 源，则将看到对每个包的 `index.json` 文件的多个请求，一个请求对应一个源。 但对于包的每个版本，都只有一个 `nupkg` 下载。

## <a name="package-signature-log-message"></a>包签名日志消息

如果要下载的包已签名，NuGet 将验证签名，并以详细的详细程度记录以下消息：

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

无论是从 HTTP 包源下载包，还是从本地包源复制包，都将报告此消息。 如果包已存在于“global-packages”文件夹或回退文件夹中，则不会输出此消息。

> [!Important]
> 由于[删除了对 VeriSign CA 的信任](https://github.com/dotnet/announcements/issues/180)，因此 NuGet 已在某些平台上、某些版本的的 NuGet 和 .NET SDK 中禁用了签名包验证。 因此，相同的包可能包含 `PackageSignatureVerificationLog` 日志，或者可能缺少这些日志，具体取决于要还原的平台以及所使用的 .NET 或 NuGet 版本。

## <a name="nuget-version-map"></a>NuGet 版本映射

以下版本的 NuGet 在包源日志记录方面有重要更改：

|NuGet 版本|Visual Studio 版本|.NET SDK 版本|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
