---
title: NuGet CLI 镜像命令
description: Nuget.exe 镜像命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959712"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="eee2b-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="eee2b-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="eee2b-104">**适用于:** 包发布&bullet; **支持的版本:** 3.2 + 中弃用</span><span class="sxs-lookup"><span data-stu-id="eee2b-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="eee2b-105">将包及其依赖项从指定的源存储库镜像到目标存储库。</span><span class="sxs-lookup"><span data-stu-id="eee2b-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="eee2b-106">ServerExtensions 和 NuGet-Signed 以前在 NuGet 2.x 中支持此命令 (通过将 NuGet-Signed 重命名为 nuget.exe) 已不再可供下载。</span><span class="sxs-lookup"><span data-stu-id="eee2b-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="eee2b-107">若要使用与此类似的命令, 请尝试[NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。</span><span class="sxs-lookup"><span data-stu-id="eee2b-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="eee2b-108">用法</span><span class="sxs-lookup"><span data-stu-id="eee2b-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="eee2b-109">其中`<packageID>` , 是要镜像的包, `<configFilePath>`或标识`packages.config`列出要镜像的包的文件。</span><span class="sxs-lookup"><span data-stu-id="eee2b-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="eee2b-110">指定源存储库, 并`<publishUrlTarget>`指定目标存储库。 `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="eee2b-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="eee2b-111">如果目标存储库在运行`https://machine/repo` [NuGet. 服务器](../../hosting-packages/nuget-server.md)的上, 则列表和推送 url 将分别为`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`。</span><span class="sxs-lookup"><span data-stu-id="eee2b-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="eee2b-112">选项</span><span class="sxs-lookup"><span data-stu-id="eee2b-112">Options</span></span>

| <span data-ttu-id="eee2b-113">选项</span><span class="sxs-lookup"><span data-stu-id="eee2b-113">Option</span></span> | <span data-ttu-id="eee2b-114">描述</span><span class="sxs-lookup"><span data-stu-id="eee2b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eee2b-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="eee2b-115">ApiKey</span></span> | <span data-ttu-id="eee2b-116">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="eee2b-116">The API key for the target repository.</span></span> <span data-ttu-id="eee2b-117">如果不存在, 则使用配置文件中指定的一个 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="eee2b-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="eee2b-118">Help</span><span class="sxs-lookup"><span data-stu-id="eee2b-118">Help</span></span> | <span data-ttu-id="eee2b-119">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="eee2b-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="eee2b-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="eee2b-120">NoCache</span></span> | <span data-ttu-id="eee2b-121">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="eee2b-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="eee2b-122">请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="eee2b-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="eee2b-123">Noop</span><span class="sxs-lookup"><span data-stu-id="eee2b-123">Noop</span></span> | <span data-ttu-id="eee2b-124">记录将执行的操作, 但不执行操作;假定推送操作成功。</span><span class="sxs-lookup"><span data-stu-id="eee2b-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="eee2b-125">早期</span><span class="sxs-lookup"><span data-stu-id="eee2b-125">PreRelease</span></span> | <span data-ttu-id="eee2b-126">在镜像操作中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="eee2b-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="eee2b-127">Source</span><span class="sxs-lookup"><span data-stu-id="eee2b-127">Source</span></span> | <span data-ttu-id="eee2b-128">要镜像的包源的列表。</span><span class="sxs-lookup"><span data-stu-id="eee2b-128">A list of package sources to mirror.</span></span> <span data-ttu-id="eee2b-129">如果未指定任何源, 将使用配置文件中定义的源 (请参阅上面的 ApiKey), 如果未指定, 则默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="eee2b-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="eee2b-130">超时</span><span class="sxs-lookup"><span data-stu-id="eee2b-130">Timeout</span></span> | <span data-ttu-id="eee2b-131">指定推送到服务器的超时值 (以秒为单位)。</span><span class="sxs-lookup"><span data-stu-id="eee2b-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="eee2b-132">默认值为300秒 (5 分钟)。</span><span class="sxs-lookup"><span data-stu-id="eee2b-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="eee2b-133">Version</span><span class="sxs-lookup"><span data-stu-id="eee2b-133">Version</span></span> | <span data-ttu-id="eee2b-134">要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="eee2b-134">The version of the package to install.</span></span> <span data-ttu-id="eee2b-135">如果未指定, 则将镜像最新版本。</span><span class="sxs-lookup"><span data-stu-id="eee2b-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="eee2b-136">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eee2b-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eee2b-137">示例</span><span class="sxs-lookup"><span data-stu-id="eee2b-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
