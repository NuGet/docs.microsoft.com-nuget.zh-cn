---
title: NuGet CLI 还原命令
description: Nuget.exe restore 命令的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9964186dcbfedfbf2415a57102f8f019a1eef23a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931990"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="378cc-103">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="378cc-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="378cc-104">**适用于：** 打包消耗&bullet;**受支持的版本：** 2.7+</span><span class="sxs-lookup"><span data-stu-id="378cc-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="378cc-105">下载并安装缺少的任何包`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="378cc-106">如果用于 NuGet 4.0 + 和 PackageReference 格式，将生成`<project>.nuget.props`文件，如果需要在`obj`文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="378cc-107">（该文件可以省略从源代码管理。）</span><span class="sxs-lookup"><span data-stu-id="378cc-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="378cc-108">在 Mac OSX 和使用 Mono 上 CLI 在 Linux 上，还原包不支持使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="378cc-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="378cc-109">用法</span><span class="sxs-lookup"><span data-stu-id="378cc-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="378cc-110">其中`<projectPath>`指定解决方案的位置或`packages.config`文件。</span><span class="sxs-lookup"><span data-stu-id="378cc-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="378cc-111">请参阅[备注](#remarks)下面有关行为的详细信息。</span><span class="sxs-lookup"><span data-stu-id="378cc-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="378cc-112">选项</span><span class="sxs-lookup"><span data-stu-id="378cc-112">Options</span></span>

| <span data-ttu-id="378cc-113">Option</span><span class="sxs-lookup"><span data-stu-id="378cc-113">Option</span></span> | <span data-ttu-id="378cc-114">描述</span><span class="sxs-lookup"><span data-stu-id="378cc-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="378cc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="378cc-115">ConfigFile</span></span> | <span data-ttu-id="378cc-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="378cc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="378cc-117">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="378cc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="378cc-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="378cc-118">DirectDownload</span></span> | <span data-ttu-id="378cc-119">*（4.0 +)* 无填充任何二进制文件或元数据缓存，可直接下载包。</span><span class="sxs-lookup"><span data-stu-id="378cc-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="378cc-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="378cc-120">DisableParallelProcessing</span></span> | <span data-ttu-id="378cc-121">禁用还原并行的多个包。</span><span class="sxs-lookup"><span data-stu-id="378cc-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="378cc-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="378cc-122">FallbackSource</span></span> | <span data-ttu-id="378cc-123">*（3.2 +)* 要用作回退，如果主数据库中找不到包的包源的列表或默认源。</span><span class="sxs-lookup"><span data-stu-id="378cc-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="378cc-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="378cc-124">ForceEnglishOutput</span></span> | <span data-ttu-id="378cc-125">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="378cc-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="378cc-126">Help</span><span class="sxs-lookup"><span data-stu-id="378cc-126">Help</span></span> | <span data-ttu-id="378cc-127">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="378cc-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="378cc-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="378cc-128">MSBuildPath</span></span> | <span data-ttu-id="378cc-129">*（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="378cc-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="378cc-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="378cc-130">MSBuildVersion</span></span> | <span data-ttu-id="378cc-131">*（3.2 +)* 指定要用于此命令的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="378cc-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="378cc-132">支持的值为 4，12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7、 15.8，15.9。</span><span class="sxs-lookup"><span data-stu-id="378cc-132">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="378cc-133">默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="378cc-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="378cc-134">NoCache</span><span class="sxs-lookup"><span data-stu-id="378cc-134">NoCache</span></span> | <span data-ttu-id="378cc-135">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="378cc-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="378cc-136">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="378cc-136">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="378cc-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="378cc-137">NonInteractive</span></span> | <span data-ttu-id="378cc-138">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="378cc-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="378cc-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="378cc-139">OutputDirectory</span></span> | <span data-ttu-id="378cc-140">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="378cc-141">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="378cc-142">使用还原时所需`packages.config`文件，除非`PackagesDirectory`或`SolutionDirectory`使用。</span><span class="sxs-lookup"><span data-stu-id="378cc-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="378cc-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="378cc-143">PackageSaveMode</span></span> | <span data-ttu-id="378cc-144">指定要将包安装完成后保存的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="378cc-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="378cc-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="378cc-145">PackagesDirectory</span></span> | <span data-ttu-id="378cc-146">与 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="378cc-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="378cc-147">使用还原时所需`packages.config`文件，除非`OutputDirectory`或`SolutionDirectory`使用。</span><span class="sxs-lookup"><span data-stu-id="378cc-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="378cc-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="378cc-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="378cc-149">超时 （秒） 来解析项目到项目引用。</span><span class="sxs-lookup"><span data-stu-id="378cc-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="378cc-150">递归</span><span class="sxs-lookup"><span data-stu-id="378cc-150">Recursive</span></span> | <span data-ttu-id="378cc-151">*（4.0 +)* 还原所有引用项目类型提供的 UWP 和.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="378cc-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="378cc-152">不适用于使用项目`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="378cc-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="378cc-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="378cc-153">RequireConsent</span></span> | <span data-ttu-id="378cc-154">验证下载和安装包之前已启用还原包。</span><span class="sxs-lookup"><span data-stu-id="378cc-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="378cc-155">有关详细信息，请参阅[包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="378cc-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="378cc-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="378cc-156">SolutionDirectory</span></span> | <span data-ttu-id="378cc-157">指定的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-157">Specifies the solution folder.</span></span> <span data-ttu-id="378cc-158">未还原解决方案的包时才有效。</span><span class="sxs-lookup"><span data-stu-id="378cc-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="378cc-159">使用还原时所需`packages.config`文件，除非`PackagesDirectory`或`OutputDirectory`使用。</span><span class="sxs-lookup"><span data-stu-id="378cc-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="378cc-160">Source</span><span class="sxs-lookup"><span data-stu-id="378cc-160">Source</span></span> | <span data-ttu-id="378cc-161">指定包源的列表 （作为 Url) 要用于还原。</span><span class="sxs-lookup"><span data-stu-id="378cc-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="378cc-162">如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="378cc-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="378cc-163">Verbosity</span><span class="sxs-lookup"><span data-stu-id="378cc-163">Verbosity</span></span> |<span data-ttu-id="378cc-164">> 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="378cc-164">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="378cc-165">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="378cc-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="378cc-166">备注</span><span class="sxs-lookup"><span data-stu-id="378cc-166">Remarks</span></span>

<span data-ttu-id="378cc-167">Restore 命令将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="378cc-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="378cc-168">确定还原命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="378cc-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="378cc-169">projectPath 文件类型</span><span class="sxs-lookup"><span data-stu-id="378cc-169">projectPath file type</span></span> | <span data-ttu-id="378cc-170">行为</span><span class="sxs-lookup"><span data-stu-id="378cc-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="378cc-171">解决方案 （文件夹）</span><span class="sxs-lookup"><span data-stu-id="378cc-171">Solution (folder)</span></span> | <span data-ttu-id="378cc-172">NuGet 将查找`.sln`文件，并使用，如果找到; 否则为会出错。</span><span class="sxs-lookup"><span data-stu-id="378cc-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="378cc-173">`(SolutionDir)\.nuget` 使用作为起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="378cc-174">`.sln` 文件</span><span class="sxs-lookup"><span data-stu-id="378cc-174">`.sln` file</span></span> | <span data-ttu-id="378cc-175">还原由解决方案; 标识的包如果显示一条错误`-SolutionDirectory`使用。</span><span class="sxs-lookup"><span data-stu-id="378cc-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="378cc-176">`$(SolutionDir)\.nuget` 使用作为起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="378cc-177">`packages.config` 或项目文件</span><span class="sxs-lookup"><span data-stu-id="378cc-177">`packages.config` or project file</span></span> | <span data-ttu-id="378cc-178">还原文件，解决和安装依赖项中列出的包。</span><span class="sxs-lookup"><span data-stu-id="378cc-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="378cc-179">其他文件类型</span><span class="sxs-lookup"><span data-stu-id="378cc-179">Other file type</span></span> | <span data-ttu-id="378cc-180">文件被假定为`.sln`文件作为更高版本; 如果它不是一种解决方案，NuGet 提供的错误。</span><span class="sxs-lookup"><span data-stu-id="378cc-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="378cc-181">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="378cc-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="378cc-182">NuGet 将查找当前文件夹中的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="378cc-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="378cc-183">如果找到单个文件，一个用于还原的包;如果找到多个解决方案，NuGet 会出错。</span><span class="sxs-lookup"><span data-stu-id="378cc-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="378cc-184">如果没有任何解决方案文件，NuGet 将查找`packages.config`，并使用其还原包。</span><span class="sxs-lookup"><span data-stu-id="378cc-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="378cc-185">如果没有解决方案或`packages.config`找到文件，NuGet 会出错。</span><span class="sxs-lookup"><span data-stu-id="378cc-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="378cc-186">确定使用以下优先级顺序 （如果没有这些文件夹找到 NuGet 提供错误） 的包文件夹：</span><span class="sxs-lookup"><span data-stu-id="378cc-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="378cc-187">使用指定的文件夹`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="378cc-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="378cc-188">`repositoryPath`中的值 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="378cc-188">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="378cc-189">使用指定的文件夹 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="378cc-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="378cc-190">还原时解决方案的包，NuGet 将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="378cc-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="378cc-191">加载解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="378cc-191">Loads the solution file.</span></span>
    - <span data-ttu-id="378cc-192">还原中列出的解决方案级别包`$(SolutionDir)\.nuget\packages.config`到`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="378cc-193">还原中列出的包`$(ProjectDir)\packages.config`到`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="378cc-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="378cc-194">对于每个指定的包，还原并行中的包，除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="378cc-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="378cc-195">示例</span><span class="sxs-lookup"><span data-stu-id="378cc-195">Examples</span></span>

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
