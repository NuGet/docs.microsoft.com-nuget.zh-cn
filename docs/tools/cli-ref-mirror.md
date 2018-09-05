---
title: NuGet CLI 镜像命令
description: Nuget.exe 镜像命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550201"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="12354-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="12354-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="12354-104">**适用于：** 包发布&bullet;**支持的版本：** 3.2 + 中不推荐使用</span><span class="sxs-lookup"><span data-stu-id="12354-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="12354-105">镜像包并从指定的源存储库到目标存储库及其依赖项。</span><span class="sxs-lookup"><span data-stu-id="12354-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="12354-106">若要启用此命令的 NuGet 版本 3.2 之前，请转到[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)中，选择最新稳定版本，下载`NuGet.ServerExtensions.dll`并`Nuget-Signed.exe`到你的本地磁盘和重命名`Nuget-Signed.exe`到`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="12354-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="12354-107">用法</span><span class="sxs-lookup"><span data-stu-id="12354-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="12354-108">其中`<packageID>`是包以镜像，或`<configFilePath>`标识`packages.config`文件，其中列出要镜像的包。</span><span class="sxs-lookup"><span data-stu-id="12354-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="12354-109">`<listUrlTarget>`指定的源存储库和`<publishUrlTarget>`指定目标存储库。</span><span class="sxs-lookup"><span data-stu-id="12354-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="12354-110">如果目标存储库位于`https://machine/repo`运行[NuGet.Server](../hosting-packages/nuget-server.md)，将列表和推送 url`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分别。</span><span class="sxs-lookup"><span data-stu-id="12354-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="12354-111">选项</span><span class="sxs-lookup"><span data-stu-id="12354-111">Options</span></span>

| <span data-ttu-id="12354-112">选项</span><span class="sxs-lookup"><span data-stu-id="12354-112">Option</span></span> | <span data-ttu-id="12354-113">描述</span><span class="sxs-lookup"><span data-stu-id="12354-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12354-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="12354-114">ApiKey</span></span> | <span data-ttu-id="12354-115">目标存储库 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="12354-115">The API key for the target repository.</span></span> <span data-ttu-id="12354-116">如果不存在，请在配置文件中指定使用 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="12354-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="12354-117">帮助</span><span class="sxs-lookup"><span data-stu-id="12354-117">Help</span></span> | <span data-ttu-id="12354-118">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="12354-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="12354-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="12354-119">NoCache</span></span> | <span data-ttu-id="12354-120">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="12354-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="12354-121">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="12354-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="12354-122">Noop</span><span class="sxs-lookup"><span data-stu-id="12354-122">Noop</span></span> | <span data-ttu-id="12354-123">记录的内容就执行此操作，但不会执行操作;假定对于推送操作成功。</span><span class="sxs-lookup"><span data-stu-id="12354-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="12354-124">预发行版</span><span class="sxs-lookup"><span data-stu-id="12354-124">PreRelease</span></span> | <span data-ttu-id="12354-125">在镜像操作中包括预发行包。</span><span class="sxs-lookup"><span data-stu-id="12354-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="12354-126">源</span><span class="sxs-lookup"><span data-stu-id="12354-126">Source</span></span> | <span data-ttu-id="12354-127">包源进行镜像的列表。</span><span class="sxs-lookup"><span data-stu-id="12354-127">A list of package sources to mirror.</span></span> <span data-ttu-id="12354-128">如果指定了不到源，在中定义的配置文件 （请参阅上面的 ApiKey） 使用，如果未指定任何默认设置为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="12354-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="12354-129">超时</span><span class="sxs-lookup"><span data-stu-id="12354-129">Timeout</span></span> | <span data-ttu-id="12354-130">指定的超时，以秒为单位，以便将推送到服务器。</span><span class="sxs-lookup"><span data-stu-id="12354-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="12354-131">默认值为 300 秒 （5 分钟）。</span><span class="sxs-lookup"><span data-stu-id="12354-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="12354-132">版本</span><span class="sxs-lookup"><span data-stu-id="12354-132">Version</span></span> | <span data-ttu-id="12354-133">要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="12354-133">The version of the package to install.</span></span> <span data-ttu-id="12354-134">如果未指定，镜像最新版本。</span><span class="sxs-lookup"><span data-stu-id="12354-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="12354-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="12354-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="12354-136">示例</span><span class="sxs-lookup"><span data-stu-id="12354-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
