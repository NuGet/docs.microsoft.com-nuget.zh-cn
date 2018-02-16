---
title: "NuGet CLI 镜像命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 镜像命令参考"
keywords: "nuget 镜像引用，镜像命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c0d49-104">镜像命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c0d49-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c0d49-105">**适用于：**包发布&bullet;**受支持的版本：** 3.2 + 中不推荐使用</span><span class="sxs-lookup"><span data-stu-id="c0d49-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c0d49-106">镜像包和到目标存储库及其依赖项从指定的源存储库。</span><span class="sxs-lookup"><span data-stu-id="c0d49-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d49-107">若要在 3.2 之前启用 NuGet 版本为此命令，请转到[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)，选择最新稳定版本，下载`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`到你的本地磁盘和重命名`Nuget-Signed.exe`到`nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c0d49-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c0d49-108">用法</span><span class="sxs-lookup"><span data-stu-id="c0d49-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c0d49-109">其中`<packageID>`是包镜像，或`<configFilePath>`标识`packages.config`列出要镜像的包文件。</span><span class="sxs-lookup"><span data-stu-id="c0d49-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c0d49-110">`<listUrlTarget>`指定源存储库，和`<publishUrlTarget>`指定目标存储库。</span><span class="sxs-lookup"><span data-stu-id="c0d49-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c0d49-111">如果你的目标存储库位于`https://machine/repo`运行[NuGet.Server](../hosting-packages/nuget-server.md)，将列表和推送 url`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分别。</span><span class="sxs-lookup"><span data-stu-id="c0d49-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c0d49-112">选项</span><span class="sxs-lookup"><span data-stu-id="c0d49-112">Options</span></span>

| <span data-ttu-id="c0d49-113">选项</span><span class="sxs-lookup"><span data-stu-id="c0d49-113">Option</span></span> | <span data-ttu-id="c0d49-114">描述</span><span class="sxs-lookup"><span data-stu-id="c0d49-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0d49-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c0d49-115">ApiKey</span></span> | <span data-ttu-id="c0d49-116">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="c0d49-116">The API key for the target repository.</span></span> <span data-ttu-id="c0d49-117">如果不存在，请在指定某一*%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="c0d49-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c0d49-118">帮助</span><span class="sxs-lookup"><span data-stu-id="c0d49-118">Help</span></span> | <span data-ttu-id="c0d49-119">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c0d49-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="c0d49-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="c0d49-120">NoCache</span></span> | <span data-ttu-id="c0d49-121">防止 NuGet 使用从本地计算机缓存的包。</span><span class="sxs-lookup"><span data-stu-id="c0d49-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="c0d49-122">Noop</span><span class="sxs-lookup"><span data-stu-id="c0d49-122">Noop</span></span> | <span data-ttu-id="c0d49-123">记录操作即告完成的内容，但不会执行操作;假定推送操作的成功。</span><span class="sxs-lookup"><span data-stu-id="c0d49-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c0d49-124">预发行版</span><span class="sxs-lookup"><span data-stu-id="c0d49-124">PreRelease</span></span> | <span data-ttu-id="c0d49-125">在镜像的操作中包含预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="c0d49-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c0d49-126">源</span><span class="sxs-lookup"><span data-stu-id="c0d49-126">Source</span></span> | <span data-ttu-id="c0d49-127">要镜像的包源的列表。</span><span class="sxs-lookup"><span data-stu-id="c0d49-127">A list of package sources to mirror.</span></span> <span data-ttu-id="c0d49-128">如果不指定任何源，则在定义*%AppData%\NuGet\NuGet.Config*使用，如果未指定任何默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c0d49-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c0d49-129">超时</span><span class="sxs-lookup"><span data-stu-id="c0d49-129">Timeout</span></span> | <span data-ttu-id="c0d49-130">指定超时，以秒为单位，以便将推送到服务器。</span><span class="sxs-lookup"><span data-stu-id="c0d49-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c0d49-131">默认值为 300 秒 （5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="c0d49-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c0d49-132">版本</span><span class="sxs-lookup"><span data-stu-id="c0d49-132">Version</span></span> | <span data-ttu-id="c0d49-133">要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="c0d49-133">The version of the package to install.</span></span> <span data-ttu-id="c0d49-134">如果未指定，正在镜像的最新版本。</span><span class="sxs-lookup"><span data-stu-id="c0d49-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c0d49-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c0d49-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c0d49-136">示例</span><span class="sxs-lookup"><span data-stu-id="c0d49-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
