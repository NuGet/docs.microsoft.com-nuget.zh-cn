---
title: NuGet CLI 安装命令
description: nuget.exe install 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779267"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="4aab4-103"> (NuGet CLI 安装命令) </span><span class="sxs-lookup"><span data-stu-id="4aab4-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="4aab4-104">**适用于：** 包使用 &bullet; **受支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="4aab4-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4aab4-105">使用指定的包源，将包下载并安装到项目中，默认为当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="4aab4-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="4aab4-106">若要直接在项目上下文之外下载包，请访问 [nuget.org](https://www.nuget.org) 上的包页面，并选择 " **下载** " 链接。</span><span class="sxs-lookup"><span data-stu-id="4aab4-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="4aab4-107">如果未指定源，则 `%appdata%\NuGet\NuGet.Config` 使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 中列出的全局配置文件中列出的源。</span><span class="sxs-lookup"><span data-stu-id="4aab4-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="4aab4-108">有关更多详细信息，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md) 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="4aab4-109">如果未指定特定包，将 `install` 安装项目文件中列出的所有程序包 `packages.config` ，使其类似于 [`restore`](cli-ref-restore.md) 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="4aab4-110">`install`此命令不会修改项目文件，也不会修改项目文件， `packages.config` 这类似于 `restore` ，因为它仅将包添加到磁盘，但不会更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4aab4-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="4aab4-111">若要添加依赖项，请在 Visual Studio 中通过包管理器 UI 或控制台添加包，或修改 `packages.config` ，然后运行 `install` 或 `restore` 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="4aab4-112">使用情况</span><span class="sxs-lookup"><span data-stu-id="4aab4-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="4aab4-113">其中 `<packageID>` ，使用最新) 版本将包命名为要安装 (，或 `<configFilePath>` 标识 `packages.config` 列出要安装的包的文件。</span><span class="sxs-lookup"><span data-stu-id="4aab4-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="4aab4-114">可以使用选项指示特定版本 `-Version` 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="4aab4-115">选项</span><span class="sxs-lookup"><span data-stu-id="4aab4-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="4aab4-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4aab4-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4aab4-117">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="4aab4-118">*(4.4 +)* 要使用的依赖项包的版本，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="4aab4-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4aab4-119">*最低* (默认) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="4aab4-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4aab4-120">*HighestPatch*：最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="4aab4-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4aab4-121">*HighestMinor*：最小主要版本号最高的版本，最高修补程序</span><span class="sxs-lookup"><span data-stu-id="4aab4-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4aab4-122">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="4aab4-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="4aab4-123">*忽略*：将不使用任何依赖项包</span><span class="sxs-lookup"><span data-stu-id="4aab4-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="4aab4-124">直接下载，无需填充元数据或二进制文件的任何缓存。</span><span class="sxs-lookup"><span data-stu-id="4aab4-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="4aab4-125">禁止并行安装多个包。</span><span class="sxs-lookup"><span data-stu-id="4aab4-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="4aab4-126">将包安装到仅带有包名称而不是版本号的名为的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4aab4-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="4aab4-127">*(3.2 +)* 在主或默认源中找不到包时要用作回退的包的列表。</span><span class="sxs-lookup"><span data-stu-id="4aab4-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="4aab4-128">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4aab4-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="4aab4-129">*(4.4 +)* 用于选择依赖项的目标框架。</span><span class="sxs-lookup"><span data-stu-id="4aab4-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="4aab4-130">如果未指定，默认值为 "Any"。</span><span class="sxs-lookup"><span data-stu-id="4aab4-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="4aab4-131">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="4aab4-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="4aab4-132">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="4aab4-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="4aab4-133">请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="4aab4-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="4aab4-134">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="4aab4-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="4aab4-135">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4aab4-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4aab4-136">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="4aab4-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="4aab4-137">指定包安装后要保存的文件类型： `nuspec` 、 `nupkg` 或 `nuspec;nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="4aab4-138">允许安装预发行包。</span><span class="sxs-lookup"><span data-stu-id="4aab4-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="4aab4-139">当还原包时，不需要此标志 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="4aab4-140">验证在下载和安装包之前是否启用了还原包。</span><span class="sxs-lookup"><span data-stu-id="4aab4-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4aab4-141">有关详细信息，请参阅 [包还原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="4aab4-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="4aab4-142">指定要为其还原包的解决方案的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="4aab4-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="4aab4-143">指定要使用的 Url)  (包的列表。</span><span class="sxs-lookup"><span data-stu-id="4aab4-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="4aab4-144">如果省略，则该命令使用配置文件中提供的源，请参阅 [常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="4aab4-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="4aab4-145">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="4aab4-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="4aab4-146">指定要安装的程序包的版本。</span><span class="sxs-lookup"><span data-stu-id="4aab4-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="4aab4-147">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4aab4-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4aab4-148">示例</span><span class="sxs-lookup"><span data-stu-id="4aab4-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
