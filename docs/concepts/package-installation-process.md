---
title: 安装包时会发生什么情况？
description: 有关包安装过程的详细信息
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 69ef02e3c935287759b4012aadcfb1cb9811367c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488446"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a><span data-ttu-id="821b2-103">安装 NuGet 包时会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="821b2-103">What happens when a NuGet package is installed?</span></span>

<span data-ttu-id="821b2-104">简而言之，不同的 NuGet 工具通常会对项目文件或 `packages.config` 中的包创建引用，然后执行包还原，从而有效安装包。</span><span class="sxs-lookup"><span data-stu-id="821b2-104">Simply said, the different NuGet tools typically create a reference to a package in the project file or `packages.config`, then perform a package restore, which effectively installs the package.</span></span> <span data-ttu-id="821b2-105">`nuget install` 除外，它仅将包展开到 `packages` 文件夹，而不修改任何其他文件。</span><span class="sxs-lookup"><span data-stu-id="821b2-105">The exception is `nuget install`, which only expands the package into a `packages` folder and does not modify any other files.</span></span>

<span data-ttu-id="821b2-106">一般流程如下：</span><span class="sxs-lookup"><span data-stu-id="821b2-106">The general process is as follows:</span></span>

1. <span data-ttu-id="821b2-107">（除 `nuget.exe` 之外的所有工具）将包标识符和版本记录到项目文件或 `packages.config`中。</span><span class="sxs-lookup"><span data-stu-id="821b2-107">(All tools except `nuget.exe`) Record the package identifier and version into the project file or `packages.config`.</span></span>

   <span data-ttu-id="821b2-108">如果安装工具是 Visual Studio 或 dotnet CLI，则该工具首先尝试安装包。</span><span class="sxs-lookup"><span data-stu-id="821b2-108">If the installation tool is Visual Studio or the dotnet CLI, the tool first attempts to install the package.</span></span> <span data-ttu-id="821b2-109">如果不兼容，则不会将包添加到项目文件或 `packages.config` 中。</span><span class="sxs-lookup"><span data-stu-id="821b2-109">If it's incompatible, the package is not added to the project file or `packages.config`.</span></span>

2. <span data-ttu-id="821b2-110">获取包：</span><span class="sxs-lookup"><span data-stu-id="821b2-110">Acquire the package:</span></span>
   - <span data-ttu-id="821b2-111">检查包是否（通过标识符和版本号）已安装在 global-packages  文件夹中，如[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="821b2-111">Check if the package (by exact identifer and version number) is already installed in the *global-packages* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

   - <span data-ttu-id="821b2-112">如果包不在 global-packages  文件夹中，请尝试从[配置文件](../consume-packages/Configuring-NuGet-Behavior.md)中列出的源检索包。</span><span class="sxs-lookup"><span data-stu-id="821b2-112">If the package is not in the *global-packages* folder, attempt to retrieve it from the sources listed listed in the [configuration files](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> <span data-ttu-id="821b2-113">对于在线源，请首先尝试从 HTTP 缓存中检索包，除非通过 `nuget.exe` 命令指定 `-NoCache` 或通过 `dotnet restore` 指定 `--no-cache`。</span><span class="sxs-lookup"><span data-stu-id="821b2-113">For online sources, attempt first to retrieve the package from the HTTP cache unless `-NoCache` is specified with `nuget.exe` commands or `--no-cache` is specified with `dotnet restore`.</span></span> <span data-ttu-id="821b2-114">（Visual Studio 和 `dotnet add package` 始终使用缓存。）如果从缓存中使用包，“缓存”将出现在输出中。</span><span class="sxs-lookup"><span data-stu-id="821b2-114">(Visual Studio and `dotnet add package` always use the cache.) If a package is used from the cache, "CACHE" appears in the output.</span></span> <span data-ttu-id="821b2-115">缓存有 30 分钟的到期时间。</span><span class="sxs-lookup"><span data-stu-id="821b2-115">The cache has an expiration time of 30 minutes.</span></span>

   - <span data-ttu-id="821b2-116">如果包不在 HTTP 缓存中，请尝试从配置中列出的源下载包。</span><span class="sxs-lookup"><span data-stu-id="821b2-116">If the package is not in the HTTP cache, attempt to download it from the sources listed in the configuration.</span></span> <span data-ttu-id="821b2-117">如果下载包，则会在输出中出现“GET”和“OK”。</span><span class="sxs-lookup"><span data-stu-id="821b2-117">If a package is downloaded, "GET" and "OK" appear in the output.</span></span> <span data-ttu-id="821b2-118">NuGet 以常规详细级别记录 http 流量。</span><span class="sxs-lookup"><span data-stu-id="821b2-118">NuGet logs http traffic on normal verbosity.</span></span>

   - <span data-ttu-id="821b2-119">如果无法从任何源成功获取包，安装将失败，并显示诸如 [NU1103](../reference/errors-and-warnings/NU1103.md) 之类的错误。</span><span class="sxs-lookup"><span data-stu-id="821b2-119">If the package cannot be successfully acquired from any sources, installation fails at this point with an error such as [NU1103](../reference/errors-and-warnings/NU1103.md).</span></span> <span data-ttu-id="821b2-120">注意，来自 `nuget.exe` 命令的错误仅显示最后检查的源，但意味着无法从任何源获取包。</span><span class="sxs-lookup"><span data-stu-id="821b2-120">Note that errors from `nuget.exe` commands show only the last source checked, but implies that the package wasn't available from any source.</span></span>

   <span data-ttu-id="821b2-121">获取包时，NuGet 配置中的源顺序可能适用：</span><span class="sxs-lookup"><span data-stu-id="821b2-121">When acquiring the package, the order of sources in the NuGet configuration may apply:</span></span>

   - <span data-ttu-id="821b2-122">NuGet 将首先检查源本地文件夹和网络共享，然后再检查 HTTP 源。</span><span class="sxs-lookup"><span data-stu-id="821b2-122">NuGet checks sources local folder and network shares before checking HTTP sources.</span></span>

3. <span data-ttu-id="821b2-123">保存包副本和 http-cache  文件夹中的其他信息，如[管理全局包和缓存文件夹中所述](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="821b2-123">Save a copy of the package and other information in the *http-cache* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

4. <span data-ttu-id="821b2-124">如下载，请将包安装到每个用户的 global-packages  文件夹中。</span><span class="sxs-lookup"><span data-stu-id="821b2-124">If downloaded, install the package into the per-user *global-packages* folder.</span></span> <span data-ttu-id="821b2-125">NuGet 创建每个包标识符的子文件夹，然后创建每个已安装包版本的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="821b2-125">NuGet creates a subfolder for each package identifier, then creates subfolders for each installed version of the package.</span></span>

5. <span data-ttu-id="821b2-126">NuGet 安装所需的包依赖项。</span><span class="sxs-lookup"><span data-stu-id="821b2-126">NuGet installs package dependencies as required.</span></span> <span data-ttu-id="821b2-127">此过程可能会更新过程中的包版本，如[依赖项解析](../concepts/dependency-resolution.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="821b2-127">This process might update package versions in the process, as described in [Dependency Resolution](../concepts/dependency-resolution.md).</span></span>

6. <span data-ttu-id="821b2-128">更新其他项目文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="821b2-128">Update other project files and folders:</span></span>

    - <span data-ttu-id="821b2-129">对于使用 PackageReference 的项目，更新存储在 `obj/project.assets.json` 中的包依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="821b2-129">For projects using PackageReference, update the package dependency graph stored in `obj/project.assets.json`.</span></span> <span data-ttu-id="821b2-130">包内容本身不会复制到任何项目文件夹中。</span><span class="sxs-lookup"><span data-stu-id="821b2-130">Package contents themselves are not copied into any project folder.</span></span>
    - <span data-ttu-id="821b2-131">如果包使用[源和配置文件转换](../create-packages/source-and-config-file-transformations.md)，则更新 `app.config` 和/或 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="821b2-131">Update `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>

7. <span data-ttu-id="821b2-132">（仅适用于 Visual Studio）如果可用，请在 Visual Studio 窗口中显示包的自述文件。</span><span class="sxs-lookup"><span data-stu-id="821b2-132">(Visual Studio only) Display the package's readme file, if available, in a Visual Studio window.</span></span>

<span data-ttu-id="821b2-133">享受利用 NuGet 包高效处理代码的体验！</span><span class="sxs-lookup"><span data-stu-id="821b2-133">Enjoy your productive coding with NuGet packages!</span></span>
