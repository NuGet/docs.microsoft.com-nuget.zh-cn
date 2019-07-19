---
title: NuGet CLI 安装命令
description: 针对 nuget.exe install 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327784"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="b36c0-103">install 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b36c0-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="b36c0-104">**适用于:** 包&bullet;使用**受支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="b36c0-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b36c0-105">使用指定的包源, 将包下载并安装到项目中, 默认为当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="b36c0-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="b36c0-106">若要直接在项目上下文之外下载包, 请访问[nuget.org](https://www.nuget.org)上的包页面, 并选择 "**下载**" 链接。</span><span class="sxs-lookup"><span data-stu-id="b36c0-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="b36c0-107">如果未指定任何源, 将使用全局配置文件`%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 中列出的任何源。</span><span class="sxs-lookup"><span data-stu-id="b36c0-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="b36c0-108">有关更多详细信息, 请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="b36c0-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="b36c0-109">如果未指定特定包, `install`将安装`packages.config`项目文件中列出的所有程序包[`restore`](cli-ref-restore.md), 使其类似于。</span><span class="sxs-lookup"><span data-stu-id="b36c0-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="b36c0-110">此命令不会修改项目文件, 也`packages.config`不会修改项目文件, 这类似`restore`于, 因为它仅将包添加到磁盘, 但不会更改项目的依赖项。 `install`</span><span class="sxs-lookup"><span data-stu-id="b36c0-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="b36c0-111">若要添加依赖项, 请在 Visual Studio 中通过包管理器 UI 或控制台添加包, 或`packages.config`修改, 然后`install`运行或`restore`。</span><span class="sxs-lookup"><span data-stu-id="b36c0-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="b36c0-112">用法</span><span class="sxs-lookup"><span data-stu-id="b36c0-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="b36c0-113">其中`<packageID>` , 要安装的包的名称 (使用最新版本) `<configFilePath>`或标识`packages.config`列出列出要安装的包的文件。</span><span class="sxs-lookup"><span data-stu-id="b36c0-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="b36c0-114">可以使用`-Version`选项指示特定版本。</span><span class="sxs-lookup"><span data-stu-id="b36c0-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="b36c0-115">选项</span><span class="sxs-lookup"><span data-stu-id="b36c0-115">Options</span></span>

| <span data-ttu-id="b36c0-116">选项</span><span class="sxs-lookup"><span data-stu-id="b36c0-116">Option</span></span> | <span data-ttu-id="b36c0-117">描述</span><span class="sxs-lookup"><span data-stu-id="b36c0-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b36c0-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b36c0-118">ConfigFile</span></span> | <span data-ttu-id="b36c0-119">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="b36c0-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b36c0-120">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="b36c0-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b36c0-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="b36c0-121">DependencyVersion</span></span> | <span data-ttu-id="b36c0-122">*(4.4 +)* 要使用的依赖项包的版本, 可以是下列项之一:</span><span class="sxs-lookup"><span data-stu-id="b36c0-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b36c0-123">*最低*(默认值): 最低版本</span><span class="sxs-lookup"><span data-stu-id="b36c0-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b36c0-124">*HighestPatch*: 最小主要、次要和最高修补程序的版本</span><span class="sxs-lookup"><span data-stu-id="b36c0-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b36c0-125">*HighestMinor*: 最小主要版本号最高的版本, 最高修补程序</span><span class="sxs-lookup"><span data-stu-id="b36c0-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b36c0-126">*最高*: 最高版本</span><span class="sxs-lookup"><span data-stu-id="b36c0-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="b36c0-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="b36c0-127">DisableParallelProcessing</span></span> | <span data-ttu-id="b36c0-128">禁止并行安装多个包。</span><span class="sxs-lookup"><span data-stu-id="b36c0-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="b36c0-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="b36c0-129">ExcludeVersion</span></span> | <span data-ttu-id="b36c0-130">将包安装到仅带有包名称而不是版本号的名为的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="b36c0-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="b36c0-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="b36c0-131">FallbackSource</span></span> | <span data-ttu-id="b36c0-132">*(3.2 +)* 在主或默认源中找不到包时要用作回退的包的列表。</span><span class="sxs-lookup"><span data-stu-id="b36c0-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="b36c0-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b36c0-133">ForceEnglishOutput</span></span> | <span data-ttu-id="b36c0-134">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="b36c0-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b36c0-135">框架</span><span class="sxs-lookup"><span data-stu-id="b36c0-135">Framework</span></span> | <span data-ttu-id="b36c0-136">*(4.4 +)* 用于选择依赖项的目标框架。</span><span class="sxs-lookup"><span data-stu-id="b36c0-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="b36c0-137">如果未指定, 默认值为 "Any"。</span><span class="sxs-lookup"><span data-stu-id="b36c0-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="b36c0-138">Help</span><span class="sxs-lookup"><span data-stu-id="b36c0-138">Help</span></span> | <span data-ttu-id="b36c0-139">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="b36c0-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="b36c0-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="b36c0-140">NoCache</span></span> | <span data-ttu-id="b36c0-141">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="b36c0-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b36c0-142">请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="b36c0-142">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b36c0-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b36c0-143">NonInteractive</span></span> | <span data-ttu-id="b36c0-144">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="b36c0-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b36c0-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="b36c0-145">OutputDirectory</span></span> | <span data-ttu-id="b36c0-146">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b36c0-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="b36c0-147">如果未指定文件夹, 则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="b36c0-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="b36c0-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="b36c0-148">PackageSaveMode</span></span> | <span data-ttu-id="b36c0-149">指定包安装后要保存的文件类型: `nuspec`、 `nupkg`或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="b36c0-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="b36c0-150">早期</span><span class="sxs-lookup"><span data-stu-id="b36c0-150">PreRelease</span></span> | <span data-ttu-id="b36c0-151">允许安装预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="b36c0-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="b36c0-152">当还原包`packages.config`时, 不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="b36c0-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="b36c0-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="b36c0-153">RequireConsent</span></span> | <span data-ttu-id="b36c0-154">验证在下载和安装包之前是否启用了还原包。</span><span class="sxs-lookup"><span data-stu-id="b36c0-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="b36c0-155">有关详细信息, 请参阅[包还原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="b36c0-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="b36c0-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="b36c0-156">SolutionDirectory</span></span> | <span data-ttu-id="b36c0-157">指定要为其还原包的解决方案的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="b36c0-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="b36c0-158">Source</span><span class="sxs-lookup"><span data-stu-id="b36c0-158">Source</span></span> | <span data-ttu-id="b36c0-159">指定要使用的包源 (作为 Url) 的列表。</span><span class="sxs-lookup"><span data-stu-id="b36c0-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="b36c0-160">如果省略, 则该命令使用配置文件中提供的源, 请参阅[常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="b36c0-160">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="b36c0-161">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b36c0-161">Verbosity</span></span> | <span data-ttu-id="b36c0-162">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="b36c0-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="b36c0-163">Version</span><span class="sxs-lookup"><span data-stu-id="b36c0-163">Version</span></span> | <span data-ttu-id="b36c0-164">指定要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="b36c0-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="b36c0-165">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b36c0-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b36c0-166">示例</span><span class="sxs-lookup"><span data-stu-id="b36c0-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
