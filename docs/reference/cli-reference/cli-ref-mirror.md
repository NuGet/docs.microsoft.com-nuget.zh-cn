---
title: NuGet CLI 镜像命令
description: Nuget.exe 镜像命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327664"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="7a7c5-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7a7c5-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="7a7c5-104">**适用于:** 包发布&bullet; **支持的版本:** 3.2 + 中弃用</span><span class="sxs-lookup"><span data-stu-id="7a7c5-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="7a7c5-105">将包及其依赖项从指定的源存储库镜像到目标存储库。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7a7c5-106">若要为3.2 之前的 NuGet 版本启用此命令, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)请跳到, 选择最新稳定`NuGet.ServerExtensions.dll` 版本`Nuget-Signed.exe` , 将和下载到本地`Nuget-Signed.exe` 磁盘`nuget.exe`, 并将重命名为。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="7a7c5-107">用法</span><span class="sxs-lookup"><span data-stu-id="7a7c5-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="7a7c5-108">其中`<packageID>` , 是要镜像的包, `<configFilePath>`或标识`packages.config`列出要镜像的包的文件。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="7a7c5-109">指定源存储库, 并`<publishUrlTarget>`指定目标存储库。 `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="7a7c5-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="7a7c5-110">如果目标存储库在运行`https://machine/repo` [NuGet. 服务器](../../hosting-packages/nuget-server.md)的上, 则列表和推送 url 将分别为`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="7a7c5-111">选项</span><span class="sxs-lookup"><span data-stu-id="7a7c5-111">Options</span></span>

| <span data-ttu-id="7a7c5-112">选项</span><span class="sxs-lookup"><span data-stu-id="7a7c5-112">Option</span></span> | <span data-ttu-id="7a7c5-113">描述</span><span class="sxs-lookup"><span data-stu-id="7a7c5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a7c5-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="7a7c5-114">ApiKey</span></span> | <span data-ttu-id="7a7c5-115">目标存储库的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-115">The API key for the target repository.</span></span> <span data-ttu-id="7a7c5-116">如果不存在, 则使用配置文件中指定的一个 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="7a7c5-117">Help</span><span class="sxs-lookup"><span data-stu-id="7a7c5-117">Help</span></span> | <span data-ttu-id="7a7c5-118">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="7a7c5-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="7a7c5-119">NoCache</span></span> | <span data-ttu-id="7a7c5-120">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="7a7c5-121">请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7a7c5-122">Noop</span><span class="sxs-lookup"><span data-stu-id="7a7c5-122">Noop</span></span> | <span data-ttu-id="7a7c5-123">记录将执行的操作, 但不执行操作;假定推送操作成功。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="7a7c5-124">早期</span><span class="sxs-lookup"><span data-stu-id="7a7c5-124">PreRelease</span></span> | <span data-ttu-id="7a7c5-125">在镜像操作中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="7a7c5-126">Source</span><span class="sxs-lookup"><span data-stu-id="7a7c5-126">Source</span></span> | <span data-ttu-id="7a7c5-127">要镜像的包源的列表。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-127">A list of package sources to mirror.</span></span> <span data-ttu-id="7a7c5-128">如果未指定任何源, 将使用配置文件中定义的源 (请参阅上面的 ApiKey), 如果未指定, 则默认为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="7a7c5-129">超时</span><span class="sxs-lookup"><span data-stu-id="7a7c5-129">Timeout</span></span> | <span data-ttu-id="7a7c5-130">指定推送到服务器的超时值 (以秒为单位)。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="7a7c5-131">默认值为300秒 (5 分钟)。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="7a7c5-132">Version</span><span class="sxs-lookup"><span data-stu-id="7a7c5-132">Version</span></span> | <span data-ttu-id="7a7c5-133">要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-133">The version of the package to install.</span></span> <span data-ttu-id="7a7c5-134">如果未指定, 则将镜像最新版本。</span><span class="sxs-lookup"><span data-stu-id="7a7c5-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="7a7c5-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7a7c5-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7a7c5-136">示例</span><span class="sxs-lookup"><span data-stu-id="7a7c5-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
