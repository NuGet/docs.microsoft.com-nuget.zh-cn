---
title: "NuGet CLI 安装命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe 安装命令的引用"
keywords: "nuget 安装引用，安装包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="61935-104">安装命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="61935-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="61935-105">**适用于：**打包消耗&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="61935-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="61935-106">下载并安装到项目中，默认设置为当前文件夹中，使用指定的包源的包。</span><span class="sxs-lookup"><span data-stu-id="61935-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="61935-107">若要下载的项目上下文之外直接程序包，请访问包的页面上[nuget.org](https://www.nuget.org)和选择**下载**链接。</span><span class="sxs-lookup"><span data-stu-id="61935-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="61935-108">如果未不指定任何源，这些文件中列出全局配置， `%APPDATA%\NuGet\NuGet.Config`，使用。</span><span class="sxs-lookup"><span data-stu-id="61935-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="61935-109">请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)有关其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="61935-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="61935-110">如果未不指定任何特定的包，`install`安装在项目中列出的所有包`packages.config`文件，使它类似于[ `restore` ](#restore)。</span><span class="sxs-lookup"><span data-stu-id="61935-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="61935-111">(`install`命令不适用于`project.json`。)</span><span class="sxs-lookup"><span data-stu-id="61935-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="61935-112">`install`命令不会修改项目文件或`packages.config`; 在这种方式很类似于`restore`，因为它只将包添加到磁盘，但不会更改项目的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="61935-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="61935-113">若要添加依赖关系，请在 Visual Studio 中，添加通过程序包管理器 UI 或控制台项目，或者修改`packages.config`，然后运行或者`install`或`restore`。</span><span class="sxs-lookup"><span data-stu-id="61935-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="61935-114">对于项目使用`project.json`，你可以修改该文件，然后运行`restore`。</span><span class="sxs-lookup"><span data-stu-id="61935-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="61935-115">用法</span><span class="sxs-lookup"><span data-stu-id="61935-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="61935-116">其中`<packageID>`命名要安装 （使用最新版本） 的包或`<configFilePath>`标识`packages.config`列出要安装的包文件。</span><span class="sxs-lookup"><span data-stu-id="61935-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="61935-117">你可以指示特定版本与`-Version`选项。</span><span class="sxs-lookup"><span data-stu-id="61935-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="61935-118">选项</span><span class="sxs-lookup"><span data-stu-id="61935-118">Options</span></span>

| <span data-ttu-id="61935-119">选项</span><span class="sxs-lookup"><span data-stu-id="61935-119">Option</span></span> | <span data-ttu-id="61935-120">描述</span><span class="sxs-lookup"><span data-stu-id="61935-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61935-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="61935-121">ConfigFile</span></span> | <span data-ttu-id="61935-122">*（2.5 +)* NuGet 要应用的配置文件。</span><span class="sxs-lookup"><span data-stu-id="61935-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="61935-123">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="61935-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="61935-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="61935-124">DisableParallelProcessing</span></span> | <span data-ttu-id="61935-125">禁用并行安装多个包。</span><span class="sxs-lookup"><span data-stu-id="61935-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="61935-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="61935-126">ExcludeVersion</span></span> | <span data-ttu-id="61935-127">将包安装到名为仅的包名称和不的版本号的文件夹。</span><span class="sxs-lookup"><span data-stu-id="61935-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="61935-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="61935-128">FallbackSource</span></span> | <span data-ttu-id="61935-129">*（3.2 +)*要用作回退机制，以防主键中找不到包的包源的列表或默认源。</span><span class="sxs-lookup"><span data-stu-id="61935-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="61935-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="61935-130">ForceEnglishOutput</span></span> | <span data-ttu-id="61935-131">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="61935-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="61935-132">框架</span><span class="sxs-lookup"><span data-stu-id="61935-132">Framework</span></span> | <span data-ttu-id="61935-133">*（4.4 +)*用于选择依赖关系的目标框架。</span><span class="sxs-lookup"><span data-stu-id="61935-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="61935-134">默认值为任何如果未指定。</span><span class="sxs-lookup"><span data-stu-id="61935-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="61935-135">帮助</span><span class="sxs-lookup"><span data-stu-id="61935-135">Help</span></span> | <span data-ttu-id="61935-136">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="61935-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="61935-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="61935-137">NoCache</span></span> | <span data-ttu-id="61935-138">防止 NuGet 使用从本地计算机缓存的包。</span><span class="sxs-lookup"><span data-stu-id="61935-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="61935-139">非交互式</span><span class="sxs-lookup"><span data-stu-id="61935-139">NonInteractive</span></span> | <span data-ttu-id="61935-140">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="61935-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="61935-141">输出目录</span><span class="sxs-lookup"><span data-stu-id="61935-141">OutputDirectory</span></span> | <span data-ttu-id="61935-142">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="61935-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="61935-143">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="61935-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="61935-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="61935-144">PackageSaveMode</span></span> | <span data-ttu-id="61935-145">指定要保存包安装完成后的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="61935-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="61935-146">预发行版</span><span class="sxs-lookup"><span data-stu-id="61935-146">PreRelease</span></span> | <span data-ttu-id="61935-147">允许要安装预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="61935-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="61935-148">还原的包时，此标志不是必需`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="61935-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="61935-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="61935-149">RequireConsent</span></span> | <span data-ttu-id="61935-150">验证还原程序包启用了之前下载和安装包。</span><span class="sxs-lookup"><span data-stu-id="61935-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="61935-151">有关详细信息，请参阅[程序包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="61935-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="61935-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="61935-152">SolutionDirectory</span></span> | <span data-ttu-id="61935-153">指定为其还原包解决方案的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="61935-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="61935-154">源</span><span class="sxs-lookup"><span data-stu-id="61935-154">Source</span></span> | <span data-ttu-id="61935-155">指定包源的列表 （作为 Url) 使用。</span><span class="sxs-lookup"><span data-stu-id="61935-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="61935-156">如果省略，则该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../Consume-Packages/Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="61935-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="61935-157">详细级别</span><span class="sxs-lookup"><span data-stu-id="61935-157">Verbosity</span></span> | <span data-ttu-id="61935-158">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="61935-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="61935-159">版本</span><span class="sxs-lookup"><span data-stu-id="61935-159">Version</span></span> | <span data-ttu-id="61935-160">指定要安装的包的版本。</span><span class="sxs-lookup"><span data-stu-id="61935-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="61935-161">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="61935-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="61935-162">示例</span><span class="sxs-lookup"><span data-stu-id="61935-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
