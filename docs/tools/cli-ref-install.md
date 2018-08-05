---
title: NuGet CLI 安装命令
description: Nuget.exe install 命令的引用
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508317"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="429a3-103">install 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="429a3-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="429a3-104">**适用于：** 打包消耗&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="429a3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="429a3-105">下载并安装到项目后，默认设置为当前文件夹中，使用指定的包源的包。</span><span class="sxs-lookup"><span data-stu-id="429a3-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="429a3-106">若要下载的包直接在项目的上下文以外，访问包的页面上[nuget.org](https://www.nuget.org) ，然后选择**下载**链接。</span><span class="sxs-lookup"><span data-stu-id="429a3-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="429a3-107">如果指定了不到源，那些在全局配置文件中，列出`%appdata%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="429a3-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="429a3-108">请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)有关其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="429a3-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="429a3-109">如果未不指定任何特定的包，`install`安装在项目中列出的所有包`packages.config`文件，使它类似于[ `restore` ](cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="429a3-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="429a3-110">`install`命令不会修改项目文件或`packages.config`; 在这种方式是类似于`restore`它仅将包添加到磁盘而不会更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="429a3-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="429a3-111">若要添加依赖项，请在 Visual Studio 中，添加一个包通过包管理器 UI 或控制台或修改`packages.config`，然后运行任一`install`或`restore`。</span><span class="sxs-lookup"><span data-stu-id="429a3-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="429a3-112">用法</span><span class="sxs-lookup"><span data-stu-id="429a3-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="429a3-113">其中`<packageID>`名称的包安装 （使用最新版本），或`<configFilePath>`标识`packages.config`文件，其中列出要安装的包。</span><span class="sxs-lookup"><span data-stu-id="429a3-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="429a3-114">您可以指示与特定版本`-Version`选项。</span><span class="sxs-lookup"><span data-stu-id="429a3-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="429a3-115">选项</span><span class="sxs-lookup"><span data-stu-id="429a3-115">Options</span></span>

| <span data-ttu-id="429a3-116">选项</span><span class="sxs-lookup"><span data-stu-id="429a3-116">Option</span></span> | <span data-ttu-id="429a3-117">描述</span><span class="sxs-lookup"><span data-stu-id="429a3-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="429a3-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="429a3-118">ConfigFile</span></span> | <span data-ttu-id="429a3-119">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="429a3-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="429a3-120">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="429a3-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="429a3-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="429a3-121">DependencyVersion</span></span> | <span data-ttu-id="429a3-122">*（4.4 +)* 版本的依赖项包使用，可以是以下值之一：</span><span class="sxs-lookup"><span data-stu-id="429a3-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="429a3-123">*最低*（默认值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="429a3-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="429a3-124">*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="429a3-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="429a3-125">*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</span><span class="sxs-lookup"><span data-stu-id="429a3-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="429a3-126">*最高*： 最高版本</span><span class="sxs-lookup"><span data-stu-id="429a3-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="429a3-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="429a3-127">DisableParallelProcessing</span></span> | <span data-ttu-id="429a3-128">禁用并行安装多个包。</span><span class="sxs-lookup"><span data-stu-id="429a3-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="429a3-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="429a3-129">ExcludeVersion</span></span> | <span data-ttu-id="429a3-130">将包安装到仅包名称而不是版本数字与名为的文件夹。</span><span class="sxs-lookup"><span data-stu-id="429a3-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="429a3-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="429a3-131">FallbackSource</span></span> | <span data-ttu-id="429a3-132">*（3.2 +)* 要用作回退，如果主数据库中找不到包的包源的列表或默认源。</span><span class="sxs-lookup"><span data-stu-id="429a3-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="429a3-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="429a3-133">ForceEnglishOutput</span></span> | <span data-ttu-id="429a3-134">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="429a3-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="429a3-135">框架</span><span class="sxs-lookup"><span data-stu-id="429a3-135">Framework</span></span> | <span data-ttu-id="429a3-136">*（4.4 +)* 用于选择依赖关系的目标框架。</span><span class="sxs-lookup"><span data-stu-id="429a3-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="429a3-137">默认值为 Any 如果未指定。</span><span class="sxs-lookup"><span data-stu-id="429a3-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="429a3-138">帮助</span><span class="sxs-lookup"><span data-stu-id="429a3-138">Help</span></span> | <span data-ttu-id="429a3-139">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="429a3-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="429a3-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="429a3-140">NoCache</span></span> | <span data-ttu-id="429a3-141">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="429a3-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="429a3-142">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="429a3-142">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="429a3-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="429a3-143">NonInteractive</span></span> | <span data-ttu-id="429a3-144">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="429a3-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="429a3-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="429a3-145">OutputDirectory</span></span> | <span data-ttu-id="429a3-146">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="429a3-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="429a3-147">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="429a3-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="429a3-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="429a3-148">PackageSaveMode</span></span> | <span data-ttu-id="429a3-149">指定要将包安装完成后保存的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="429a3-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="429a3-150">预发行版</span><span class="sxs-lookup"><span data-stu-id="429a3-150">PreRelease</span></span> | <span data-ttu-id="429a3-151">允许要安装的预发行包。</span><span class="sxs-lookup"><span data-stu-id="429a3-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="429a3-152">还原包时，此标志不是必需`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="429a3-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="429a3-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="429a3-153">RequireConsent</span></span> | <span data-ttu-id="429a3-154">验证下载和安装包之前已启用还原包。</span><span class="sxs-lookup"><span data-stu-id="429a3-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="429a3-155">有关详细信息，请参阅[包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="429a3-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="429a3-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="429a3-156">SolutionDirectory</span></span> | <span data-ttu-id="429a3-157">指定要为其还原包解决方案的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="429a3-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="429a3-158">源</span><span class="sxs-lookup"><span data-stu-id="429a3-158">Source</span></span> | <span data-ttu-id="429a3-159">指定包源的列表 （作为 Url) 来使用。</span><span class="sxs-lookup"><span data-stu-id="429a3-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="429a3-160">如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="429a3-160">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="429a3-161">详细级别</span><span class="sxs-lookup"><span data-stu-id="429a3-161">Verbosity</span></span> | <span data-ttu-id="429a3-162">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="429a3-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="429a3-163">版本</span><span class="sxs-lookup"><span data-stu-id="429a3-163">Version</span></span> | <span data-ttu-id="429a3-164">指定要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="429a3-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="429a3-165">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="429a3-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="429a3-166">示例</span><span class="sxs-lookup"><span data-stu-id="429a3-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
