---
title: NuGet CLI restore 命令
description: 针对 nuget.exe restore 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327634"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="4a434-103">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4a434-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="4a434-104">**适用于:** 包&bullet;使用**受支持的版本:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="4a434-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="4a434-105">下载并安装`packages`文件夹中缺少的任何程序包。</span><span class="sxs-lookup"><span data-stu-id="4a434-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="4a434-106">与 NuGet 4.0 + 和 PackageReference 格式一起使用时, 会`<project>.nuget.props` `obj`在需要时在文件夹中生成文件。</span><span class="sxs-lookup"><span data-stu-id="4a434-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="4a434-107">(可以从源代码管理中省略该文件。)</span><span class="sxs-lookup"><span data-stu-id="4a434-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="4a434-108">在 Mono 上带有 CLI 的 Mac OSX 和 Linux 上, PackageReference 不支持还原包。</span><span class="sxs-lookup"><span data-stu-id="4a434-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="4a434-109">用法</span><span class="sxs-lookup"><span data-stu-id="4a434-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="4a434-110">其中`<projectPath>`指定解决方案`packages.config`或文件的位置。</span><span class="sxs-lookup"><span data-stu-id="4a434-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="4a434-111">有关行为的详细信息, 请参阅下面的[备注](#remarks)。</span><span class="sxs-lookup"><span data-stu-id="4a434-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="4a434-112">选项</span><span class="sxs-lookup"><span data-stu-id="4a434-112">Options</span></span>

| <span data-ttu-id="4a434-113">选项</span><span class="sxs-lookup"><span data-stu-id="4a434-113">Option</span></span> | <span data-ttu-id="4a434-114">描述</span><span class="sxs-lookup"><span data-stu-id="4a434-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a434-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4a434-115">ConfigFile</span></span> | <span data-ttu-id="4a434-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4a434-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4a434-117">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="4a434-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4a434-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="4a434-118">DirectDownload</span></span> | <span data-ttu-id="4a434-119">*(4.0 +)* 直接下载包, 而不填充包含任何二进制文件或元数据的缓存。</span><span class="sxs-lookup"><span data-stu-id="4a434-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="4a434-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="4a434-120">DisableParallelProcessing</span></span> | <span data-ttu-id="4a434-121">禁用并行还原多个包。</span><span class="sxs-lookup"><span data-stu-id="4a434-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="4a434-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="4a434-122">FallbackSource</span></span> | <span data-ttu-id="4a434-123">*(3.2 +)* 在主或默认源中找不到包时要用作回退的包的列表。</span><span class="sxs-lookup"><span data-stu-id="4a434-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="4a434-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4a434-124">ForceEnglishOutput</span></span> | <span data-ttu-id="4a434-125">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4a434-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4a434-126">Help</span><span class="sxs-lookup"><span data-stu-id="4a434-126">Help</span></span> | <span data-ttu-id="4a434-127">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="4a434-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="4a434-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="4a434-128">MSBuildPath</span></span> | <span data-ttu-id="4a434-129">*(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径, 优先于`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="4a434-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="4a434-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="4a434-130">MSBuildVersion</span></span> | <span data-ttu-id="4a434-131">*(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="4a434-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="4a434-132">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="4a434-132">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="4a434-133">默认情况下, 将选取路径中的 MSBuild, 否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="4a434-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="4a434-134">NoCache</span><span class="sxs-lookup"><span data-stu-id="4a434-134">NoCache</span></span> | <span data-ttu-id="4a434-135">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="4a434-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="4a434-136">请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="4a434-136">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="4a434-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4a434-137">NonInteractive</span></span> | <span data-ttu-id="4a434-138">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="4a434-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4a434-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="4a434-139">OutputDirectory</span></span> | <span data-ttu-id="4a434-140">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4a434-141">如果未指定文件夹, 则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="4a434-142">使用`packages.config`文件进行还原时必需, `PackagesDirectory`除非`SolutionDirectory`使用或。</span><span class="sxs-lookup"><span data-stu-id="4a434-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="4a434-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="4a434-143">PackageSaveMode</span></span> | <span data-ttu-id="4a434-144">指定包安装后要保存的文件类型: `nuspec`、 `nupkg`或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="4a434-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="4a434-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="4a434-145">PackagesDirectory</span></span> | <span data-ttu-id="4a434-146">与 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="4a434-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="4a434-147">使用`packages.config`文件进行还原时必需, `OutputDirectory`除非`SolutionDirectory`使用或。</span><span class="sxs-lookup"><span data-stu-id="4a434-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="4a434-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="4a434-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="4a434-149">解析项目到项目引用的超时时间 (秒)。</span><span class="sxs-lookup"><span data-stu-id="4a434-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="4a434-150">recursive</span><span class="sxs-lookup"><span data-stu-id="4a434-150">Recursive</span></span> | <span data-ttu-id="4a434-151">*(4.0 +)* 还原 UWP 和 .NET Core 项目的所有引用项目。</span><span class="sxs-lookup"><span data-stu-id="4a434-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="4a434-152">不适用于使用`packages.config`的项目。</span><span class="sxs-lookup"><span data-stu-id="4a434-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="4a434-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="4a434-153">RequireConsent</span></span> | <span data-ttu-id="4a434-154">验证在下载和安装包之前是否启用了还原包。</span><span class="sxs-lookup"><span data-stu-id="4a434-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4a434-155">有关详细信息, 请参阅[包还原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="4a434-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="4a434-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="4a434-156">SolutionDirectory</span></span> | <span data-ttu-id="4a434-157">指定解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-157">Specifies the solution folder.</span></span> <span data-ttu-id="4a434-158">还原解决方案的包时无效。</span><span class="sxs-lookup"><span data-stu-id="4a434-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="4a434-159">使用`packages.config`文件进行还原时必需, `PackagesDirectory`除非`OutputDirectory`使用或。</span><span class="sxs-lookup"><span data-stu-id="4a434-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="4a434-160">Source</span><span class="sxs-lookup"><span data-stu-id="4a434-160">Source</span></span> | <span data-ttu-id="4a434-161">指定要用于还原的包源 (作为 Url) 的列表。</span><span class="sxs-lookup"><span data-stu-id="4a434-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="4a434-162">如果省略, 则该命令将使用配置文件中提供的源, 请参阅[配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="4a434-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="4a434-163">Verbosity</span><span class="sxs-lookup"><span data-stu-id="4a434-163">Verbosity</span></span> | <span data-ttu-id="4a434-164">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="4a434-164">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4a434-165">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4a434-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="4a434-166">备注</span><span class="sxs-lookup"><span data-stu-id="4a434-166">Remarks</span></span>

<span data-ttu-id="4a434-167">Restore 命令执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="4a434-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="4a434-168">确定 restore 命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="4a434-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="4a434-169">projectPath 文件类型</span><span class="sxs-lookup"><span data-stu-id="4a434-169">projectPath file type</span></span> | <span data-ttu-id="4a434-170">行为</span><span class="sxs-lookup"><span data-stu-id="4a434-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="4a434-171">解决方案 (文件夹)</span><span class="sxs-lookup"><span data-stu-id="4a434-171">Solution (folder)</span></span> | <span data-ttu-id="4a434-172">NuGet 查找`.sln`文件并使用该文件 (如果找到的话); 否则将会出现错误。</span><span class="sxs-lookup"><span data-stu-id="4a434-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="4a434-173">`(SolutionDir)\.nuget`用作起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="4a434-174">`.sln`文件</span><span class="sxs-lookup"><span data-stu-id="4a434-174">`.sln` file</span></span> | <span data-ttu-id="4a434-175">还原解决方案标识的包;如果`-SolutionDirectory`使用了, 则会出现错误。</span><span class="sxs-lookup"><span data-stu-id="4a434-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="4a434-176">`$(SolutionDir)\.nuget`用作起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="4a434-177">`packages.config`或项目文件</span><span class="sxs-lookup"><span data-stu-id="4a434-177">`packages.config` or project file</span></span> | <span data-ttu-id="4a434-178">还原文件中列出的包, 解析和安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="4a434-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="4a434-179">其他文件类型</span><span class="sxs-lookup"><span data-stu-id="4a434-179">Other file type</span></span> | <span data-ttu-id="4a434-180">文件被假定为如上所述的`.sln`文件; 如果该文件不是解决方案, NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="4a434-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="4a434-181">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="4a434-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="4a434-182">NuGet 在当前文件夹中查找解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="4a434-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="4a434-183">如果找到一个文件, 则使用该文件还原包;如果找到多个解决方案, NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="4a434-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="4a434-184">如果没有解决方案文件, NuGet 将查找`packages.config`并使用它来还原包。</span><span class="sxs-lookup"><span data-stu-id="4a434-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="4a434-185">如果未找到任何`packages.config`解决方案或文件, NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="4a434-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="4a434-186">使用以下优先级顺序确定包文件夹 (如果找不到这些文件夹, 则 NuGet 会出现错误):</span><span class="sxs-lookup"><span data-stu-id="4a434-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="4a434-187">用`-PackagesDirectory`指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a434-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="4a434-188">中`repositoryPath`的值`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="4a434-188">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="4a434-189">指定的文件夹`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="4a434-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="4a434-190">还原解决方案的包时, NuGet 会执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="4a434-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="4a434-191">加载解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="4a434-191">Loads the solution file.</span></span>
    - <span data-ttu-id="4a434-192">`$(SolutionDir)\.nuget\packages.config` 将`packages`中列出的解决方案级别包还原到文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4a434-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="4a434-193">`$(ProjectDir)\packages.config` 将`packages`中列出的包还原到文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4a434-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="4a434-194">对于指定的每个包, 请并行还原包`-DisableParallelProcessing` , 除非指定了。</span><span class="sxs-lookup"><span data-stu-id="4a434-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="4a434-195">示例</span><span class="sxs-lookup"><span data-stu-id="4a434-195">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
