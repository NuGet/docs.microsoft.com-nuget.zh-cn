---
title: NuGet CLI 镜像命令
description: nuget.exe 镜像命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622962"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c8a9d-103"> (NuGet CLI 的镜像命令) </span><span class="sxs-lookup"><span data-stu-id="c8a9d-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c8a9d-104">**适用于：** 包发布 &bullet; **支持的版本：** 3.2 + 中弃用</span><span class="sxs-lookup"><span data-stu-id="c8a9d-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c8a9d-105">将包及其依赖项从指定的源存储库镜像到目标存储库。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c8a9d-106">NuGet.ServerExtensions.dll 和 NuGet-Signed.exe 以前在 NuGet 2.x (中支持此命令，方法是将 NuGet-Signed.exe 重命名为 nuget.exe) 不再可供下载。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="c8a9d-107">若要使用与此类似的命令，请尝试 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="c8a9d-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="c8a9d-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c8a9d-109">其中 `<packageID>` ，是要镜像的包，或 `<configFilePath>` 标识 `packages.config` 列出要镜像的包的文件。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c8a9d-110">`<listUrlTarget>`指定源存储库，并 `<publishUrlTarget>` 指定目标存储库。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c8a9d-111">如果目标存储库在 `https://machine/repo` 运行 [NuGet. 服务器](../../hosting-packages/nuget-server.md)的上，则列表和推送 url 将分别为 `https://machine/repo/nuget` 和 `https://machine/repo/api/v2/package` 。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c8a9d-112">选项</span><span class="sxs-lookup"><span data-stu-id="c8a9d-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="c8a9d-113">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-113">The API key for the target repository.</span></span> <span data-ttu-id="c8a9d-114">如果不存在，则使用配置文件中指定的 (`%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) # A5。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="c8a9d-115">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="c8a9d-116">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c8a9d-117">请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="c8a9d-118">记录将执行的操作，但不执行操作;假定推送操作成功。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="c8a9d-119">在镜像操作中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="c8a9d-120">要镜像的包源的列表。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-120">A list of package sources to mirror.</span></span> <span data-ttu-id="c8a9d-121">如果未指定源，则配置文件中定义的 (参阅) 使用上述 ApiKey，如果未指定，则默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="c8a9d-122">指定推送到服务器的超时值（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c8a9d-123">默认值为 300 秒（5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="c8a9d-124">要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-124">The version of the package to install.</span></span> <span data-ttu-id="c8a9d-125">如果未指定，则将镜像最新版本。</span><span class="sxs-lookup"><span data-stu-id="c8a9d-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="c8a9d-126">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c8a9d-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c8a9d-127">示例</span><span class="sxs-lookup"><span data-stu-id="c8a9d-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
