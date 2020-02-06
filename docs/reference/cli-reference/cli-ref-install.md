---
title: NuGet CLI 安装命令
description: 针对 nuget.exe install 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036937"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="fc248-103">install 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fc248-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="fc248-104">**适用于：** &bullet; 支持的**版本**的包使用：全部</span><span class="sxs-lookup"><span data-stu-id="fc248-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fc248-105">使用指定的包源，将包下载并安装到项目中，默认为当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="fc248-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="fc248-106">若要直接在项目上下文之外下载包，请访问[nuget.org](https://www.nuget.org)上的包页面，并选择 "**下载**" 链接。</span><span class="sxs-lookup"><span data-stu-id="fc248-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="fc248-107">如果未指定任何源，将使用全局配置文件中列出的 `%appdata%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="fc248-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="fc248-108">有关更多详细信息，请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="fc248-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="fc248-109">如果未指定特定的包，`install` 将安装项目 `packages.config` 文件中列出的所有包，使其类似于[`restore`](cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="fc248-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="fc248-110">`install` 命令不会修改项目文件或 `packages.config`;通过这种方式，它与 `restore` 类似，只是将包添加到磁盘，但不会更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="fc248-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="fc248-111">若要添加依赖项，请在 Visual Studio 中通过包管理器 UI 或控制台添加包，或修改 `packages.config` 然后运行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="fc248-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="fc248-112">用法</span><span class="sxs-lookup"><span data-stu-id="fc248-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="fc248-113">其中 `<packageID>` 命名要安装的包（使用最新版本），或 `<configFilePath>` 标识列出要安装的包的 `packages.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="fc248-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="fc248-114">您可以使用 `-Version` 选项指示特定版本。</span><span class="sxs-lookup"><span data-stu-id="fc248-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="fc248-115">Options</span><span class="sxs-lookup"><span data-stu-id="fc248-115">Options</span></span>

| <span data-ttu-id="fc248-116">选项</span><span class="sxs-lookup"><span data-stu-id="fc248-116">Option</span></span> | <span data-ttu-id="fc248-117">说明</span><span class="sxs-lookup"><span data-stu-id="fc248-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc248-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fc248-118">ConfigFile</span></span> | <span data-ttu-id="fc248-119">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="fc248-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fc248-120">如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="fc248-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fc248-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="fc248-121">DependencyVersion</span></span> | <span data-ttu-id="fc248-122">*（4.4 +）* 要使用的依赖项包的版本，可以是下列项之一：</span><span class="sxs-lookup"><span data-stu-id="fc248-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="fc248-123">*最低*（默认值）：最低版本</span><span class="sxs-lookup"><span data-stu-id="fc248-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="fc248-124">*HighestPatch*：最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="fc248-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="fc248-125">*HighestMinor*：最小主要版本号最高的版本，最高修补程序</span><span class="sxs-lookup"><span data-stu-id="fc248-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="fc248-126">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="fc248-126">*Highest*: the highest version</span></span></li><li><span data-ttu-id="fc248-127">*忽略*：将不使用任何依赖项包</span><span class="sxs-lookup"><span data-stu-id="fc248-127">*Ignore*: No dependency packages will be used</span></span></li></ul> |
| <span data-ttu-id="fc248-128">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="fc248-128">DisableParallelProcessing</span></span> | <span data-ttu-id="fc248-129">禁止并行安装多个包。</span><span class="sxs-lookup"><span data-stu-id="fc248-129">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="fc248-130">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="fc248-130">ExcludeVersion</span></span> | <span data-ttu-id="fc248-131">将包安装到仅带有包名称而不是版本号的名为的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="fc248-131">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="fc248-132">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="fc248-132">FallbackSource</span></span> | <span data-ttu-id="fc248-133">*（3.2 +）* 在主或默认源中找不到包时要用作回退的包的列表。</span><span class="sxs-lookup"><span data-stu-id="fc248-133">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="fc248-134">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fc248-134">ForceEnglishOutput</span></span> | <span data-ttu-id="fc248-135">*（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="fc248-135">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fc248-136">框架</span><span class="sxs-lookup"><span data-stu-id="fc248-136">Framework</span></span> | <span data-ttu-id="fc248-137">*（4.4 +）* 用于选择依赖项的目标框架。</span><span class="sxs-lookup"><span data-stu-id="fc248-137">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="fc248-138">如果未指定，默认值为 "Any"。</span><span class="sxs-lookup"><span data-stu-id="fc248-138">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="fc248-139">帮助</span><span class="sxs-lookup"><span data-stu-id="fc248-139">Help</span></span> | <span data-ttu-id="fc248-140">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="fc248-140">Displays help information for the command.</span></span> |
| <span data-ttu-id="fc248-141">NoCache</span><span class="sxs-lookup"><span data-stu-id="fc248-141">NoCache</span></span> | <span data-ttu-id="fc248-142">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="fc248-142">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="fc248-143">请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="fc248-143">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fc248-144">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fc248-144">NonInteractive</span></span> | <span data-ttu-id="fc248-145">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="fc248-145">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fc248-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="fc248-146">OutputDirectory</span></span> | <span data-ttu-id="fc248-147">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="fc248-147">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="fc248-148">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="fc248-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="fc248-149">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="fc248-149">PackageSaveMode</span></span> | <span data-ttu-id="fc248-150">指定包安装后要保存的文件的类型： `nuspec`、`nupkg`或 `nuspec;nupkg`之一。</span><span class="sxs-lookup"><span data-stu-id="fc248-150">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="fc248-151">PreRelease</span><span class="sxs-lookup"><span data-stu-id="fc248-151">PreRelease</span></span> | <span data-ttu-id="fc248-152">允许安装预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="fc248-152">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="fc248-153">在 `packages.config`还原包时，不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="fc248-153">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="fc248-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="fc248-154">RequireConsent</span></span> | <span data-ttu-id="fc248-155">验证在下载和安装包之前是否启用了还原包。</span><span class="sxs-lookup"><span data-stu-id="fc248-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="fc248-156">有关详细信息，请参阅[包还原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="fc248-156">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="fc248-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="fc248-157">SolutionDirectory</span></span> | <span data-ttu-id="fc248-158">指定要为其还原包的解决方案的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="fc248-158">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="fc248-159">源</span><span class="sxs-lookup"><span data-stu-id="fc248-159">Source</span></span> | <span data-ttu-id="fc248-160">指定要使用的包源（作为 Url）的列表。</span><span class="sxs-lookup"><span data-stu-id="fc248-160">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="fc248-161">如果省略，则该命令使用配置文件中提供的源，请参阅[常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="fc248-161">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="fc248-162">详细程度</span><span class="sxs-lookup"><span data-stu-id="fc248-162">Verbosity</span></span> | <span data-ttu-id="fc248-163">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="fc248-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="fc248-164">版本</span><span class="sxs-lookup"><span data-stu-id="fc248-164">Version</span></span> | <span data-ttu-id="fc248-165">指定要安装的程序包的版本。</span><span class="sxs-lookup"><span data-stu-id="fc248-165">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="fc248-166">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fc248-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fc248-167">示例</span><span class="sxs-lookup"><span data-stu-id="fc248-167">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
