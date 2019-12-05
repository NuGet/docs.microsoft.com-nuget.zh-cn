---
title: 如何管理 NuGet 中的全局包、缓存、临时文件夹
description: 如何管理计算机上存在的全局包安装文件夹、包缓存和临时文件夹，这些在安装、还原和更新包时将用到。
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825205"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="295ee-103">管理全局包、缓存和临时文件夹</span><span class="sxs-lookup"><span data-stu-id="295ee-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="295ee-104">每当安装、更新或还原包时，NuGet 将管理项目结构多个文件夹之外的包和包信息：</span><span class="sxs-lookup"><span data-stu-id="295ee-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="295ee-105">name</span><span class="sxs-lookup"><span data-stu-id="295ee-105">Name</span></span> | <span data-ttu-id="295ee-106">说明和位置（每个用户）</span><span class="sxs-lookup"><span data-stu-id="295ee-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="295ee-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="295ee-107">global&#8209;packages</span></span> | <span data-ttu-id="295ee-108">global-packages  文件夹是 NuGet 安装任何下载包的位置。</span><span class="sxs-lookup"><span data-stu-id="295ee-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="295ee-109">每个包完全展开到匹配包标识符和版本号的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="295ee-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="295ee-110">使用 [PackageReference](package-references-in-project-files.md) 格式的项目始终直接从该文件夹中使用包。</span><span class="sxs-lookup"><span data-stu-id="295ee-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="295ee-111">使用 [packages.config](../reference/packages-config.md) 时，包将安装到 global-packages  文件夹，然后复制到项目的 `packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="295ee-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="295ee-112">Windows：`%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="295ee-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="295ee-113">Mac/Linux：`~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="295ee-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="295ee-114">使用 NUGET_PACKAGES 重写环境变量 `globalPackagesFolder` 或 `repositoryPath` [配置设置](../reference/nuget-config-file.md#config-section)（分别在使用 PackageReference 和 `packages.config` 时）或 `RestorePackagesPath` MSBuild 属性（仅限 MSBuild）。</span><span class="sxs-lookup"><span data-stu-id="295ee-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="295ee-115">环境变量优先于配置设置。</span><span class="sxs-lookup"><span data-stu-id="295ee-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="295ee-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="295ee-116">http&#8209;cache</span></span> | <span data-ttu-id="295ee-117">Visual Studio 包管理器 (NuGet 3.x+) 和 `dotnet` 工具存储此缓存中下载包的副本（另存为 `.dat` 文件），这些副本被组织到每个包源的子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="295ee-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="295ee-118">未展开包，且缓存中有 30 分钟的到期时间。</span><span class="sxs-lookup"><span data-stu-id="295ee-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="295ee-119">Windows：`%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="295ee-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="295ee-120">Mac/Linux：`~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="295ee-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="295ee-121">使用 NUGET_HTTP_CACHE_PATH 环境变量替代。</span><span class="sxs-lookup"><span data-stu-id="295ee-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="295ee-122">temp</span><span class="sxs-lookup"><span data-stu-id="295ee-122">temp</span></span> | <span data-ttu-id="295ee-123">NuGet 在各操作期间在其中存储临时文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="295ee-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="295ee-124">Windows：`%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="295ee-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="295ee-125">Mac/Linux：`/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="295ee-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="295ee-126">plugins-cache **4.8 +**</span><span class="sxs-lookup"><span data-stu-id="295ee-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="295ee-127">NuGet 存储来自操作声明请求的结果的文件夹。</span><span class="sxs-lookup"><span data-stu-id="295ee-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="295ee-128">Windows：`%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="295ee-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="295ee-129">Mac/Linux：`~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="295ee-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="295ee-130">使用 NUGET_PLUGINS_CACHE_PATH 环境变量替代。</span><span class="sxs-lookup"><span data-stu-id="295ee-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="295ee-131">NuGet 3.5 和早期版本使用 `%localappdata%\NuGet\Cache` 中的 packages-cache  而不是 http-cache  。</span><span class="sxs-lookup"><span data-stu-id="295ee-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="295ee-132">通过使用缓存和 global-packages  文件夹，NuGet 通常会避免下载计算机上已存在的包，以提高安装、更新和还原操作的性能。</span><span class="sxs-lookup"><span data-stu-id="295ee-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="295ee-133">在使用 PackageReference 时，global-packages  文件夹还会避免在项目文件夹中保存下载的包，其中它们可能会在无意间被添加到源代码管理，并减少 NuGet 对计算机存储的总体影响。</span><span class="sxs-lookup"><span data-stu-id="295ee-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="295ee-134">当要求检索包时，NuGet 会首先查看 global-packages  文件夹。</span><span class="sxs-lookup"><span data-stu-id="295ee-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="295ee-135">如果不存在包的确切版本，NuGet 将检查所有非 HTTP 包源。</span><span class="sxs-lookup"><span data-stu-id="295ee-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="295ee-136">如果仍未找到包，NuGet 将查找 http-cache  中的包，除非使用 `dotnet.exe` 命令指定 `--no-cache`，或使用 `nuget.exe` 命令指定 `-NoCache`。</span><span class="sxs-lookup"><span data-stu-id="295ee-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="295ee-137">如果包不在缓存中，或未使用缓存，那么 NuGet 将通过 HTTP 检索包。</span><span class="sxs-lookup"><span data-stu-id="295ee-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="295ee-138">有关详细信息，请参阅[安装包时会发生什么情况？](../concepts/package-installation-process.md)。</span><span class="sxs-lookup"><span data-stu-id="295ee-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="295ee-139">查看文件夹位置</span><span class="sxs-lookup"><span data-stu-id="295ee-139">Viewing folder locations</span></span>

<span data-ttu-id="295ee-140">可以使用 [nuget locals 命令](../reference/cli-reference/cli-ref-locals.md)查看位置：</span><span class="sxs-lookup"><span data-stu-id="295ee-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="295ee-141">典型输出（Windows；“user1”为当前用户名）：</span><span class="sxs-lookup"><span data-stu-id="295ee-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="295ee-142">（`package-cache` 在 NuGet 2.x 中使用，并在 NuGet 3.5 及更早版本中显示。）</span><span class="sxs-lookup"><span data-stu-id="295ee-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="295ee-143">还可以使用 [dotnet nuget locals 命令](/dotnet/core/tools/dotnet-nuget-locals)查看文件夹位置：</span><span class="sxs-lookup"><span data-stu-id="295ee-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="295ee-144">典型输出（Mac/Linux；“user1”为当前用户名）：</span><span class="sxs-lookup"><span data-stu-id="295ee-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="295ee-145">若要显示单个文件夹的位置，请使用 `http-cache`、`global-packages`、`temp` 或 `plugins-cache`，而不是 `all`。</span><span class="sxs-lookup"><span data-stu-id="295ee-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="295ee-146">清除本地文件夹</span><span class="sxs-lookup"><span data-stu-id="295ee-146">Clearing local folders</span></span>

<span data-ttu-id="295ee-147">如果安装包时遇到问题或想要确保从远程库安装包，请使用 `locals --clear` 选项 (dotnet.exe) 或 `locals -clear` (nuget.exe)，指定要清除的文件夹，或使用 `all` 清除所有文件夹：</span><span class="sxs-lookup"><span data-stu-id="295ee-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="295ee-148">目前在 Visual Studio 中打开的项目所使用的任何包都不会从 global-packages  文件夹中清除。</span><span class="sxs-lookup"><span data-stu-id="295ee-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="295ee-149">从 Visual Studio 2017 开始，使用“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令，然后选择“清除所有 NuGet 缓存”   。</span><span class="sxs-lookup"><span data-stu-id="295ee-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="295ee-150">管理缓存目前不支持通过包管理器控制台提供。</span><span class="sxs-lookup"><span data-stu-id="295ee-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="295ee-151">在 Visual Studio 2015 中，则改用 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="295ee-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![用于清除缓存的 NuGet 选项命令](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="295ee-153">错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="295ee-153">Troubleshooting errors</span></span>

<span data-ttu-id="295ee-154">使用 `nuget locals` 或 `dotnet nuget locals` 时可能出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="295ee-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="295ee-155">*错误：进程无法访问文件 <package>，因为另一个进程正在使用该文件* *或清除本地资源失败：无法删除一个或多个文件*</span><span class="sxs-lookup"><span data-stu-id="295ee-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="295ee-156">另一个进程正在使用文件夹中的一个或多个文件；例如，Visual Studio 项目处于打开状态，它指的是 global-packages  文件夹中的包。</span><span class="sxs-lookup"><span data-stu-id="295ee-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="295ee-157">关闭这些进程，然后重试。</span><span class="sxs-lookup"><span data-stu-id="295ee-157">Close those processes and try again.</span></span>

- <span data-ttu-id="295ee-158">*错误：访问路径 <path> 被拒绝或目录不为空* </span><span class="sxs-lookup"><span data-stu-id="295ee-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="295ee-159">你没有删除缓存文件的权限。</span><span class="sxs-lookup"><span data-stu-id="295ee-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="295ee-160">如果可能，请更改文件夹权限，然后重试。</span><span class="sxs-lookup"><span data-stu-id="295ee-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="295ee-161">否则，请与系统管理员联系。</span><span class="sxs-lookup"><span data-stu-id="295ee-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="295ee-162">*错误：指定的路径和/或文件名太长。完全限定文件名必须少于 260 个字符，而目录名必须少于 248 个字符。*</span><span class="sxs-lookup"><span data-stu-id="295ee-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="295ee-163">缩短文件夹名称，然后重试。</span><span class="sxs-lookup"><span data-stu-id="295ee-163">Shorten the folder names and try again.</span></span>
