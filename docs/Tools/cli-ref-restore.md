---
title: "NuGet CLI 还原命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "有关 nuget.exe 的还原命令的引用"
keywords: "nuget 还原引用，请还原包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ad5156a065e20dfced99da6b2e2860dbd748ad5
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="ea820-104">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ea820-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="ea820-105">**适用于：**打包消耗&bullet;**受支持的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="ea820-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="ea820-106">下载并安装任何缺少的程序包`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="ea820-107">如果用于 NuGet 4.0 + 和 PackageReference 格式，生成`<project>.nuget.props`文件，如果需要在`obj`文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="ea820-108">（该文件可以省略从源代码管理。）</span><span class="sxs-lookup"><span data-stu-id="ea820-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="ea820-109">在 Mac OSX 和 Linux 上 Mono cli 上，还原程序包不支持 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="ea820-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="ea820-110">用法</span><span class="sxs-lookup"><span data-stu-id="ea820-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="ea820-111">其中`<projectPath>`指定解决方案的位置或`packages.config`文件。</span><span class="sxs-lookup"><span data-stu-id="ea820-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="ea820-112">请参阅[备注](#remarks)下面有关行为的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ea820-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="ea820-113">选项</span><span class="sxs-lookup"><span data-stu-id="ea820-113">Options</span></span>

| <span data-ttu-id="ea820-114">选项</span><span class="sxs-lookup"><span data-stu-id="ea820-114">Option</span></span> | <span data-ttu-id="ea820-115">描述</span><span class="sxs-lookup"><span data-stu-id="ea820-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea820-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ea820-116">ConfigFile</span></span> | <span data-ttu-id="ea820-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ea820-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ea820-118">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="ea820-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ea820-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="ea820-119">DirectDownload</span></span> | <span data-ttu-id="ea820-120">*（4.0 +)*直接而不填充缓存与任何二进制文件或元数据将下载包。</span><span class="sxs-lookup"><span data-stu-id="ea820-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="ea820-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="ea820-121">DisableParallelProcessing</span></span> | <span data-ttu-id="ea820-122">禁用还原并行的多个包。</span><span class="sxs-lookup"><span data-stu-id="ea820-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="ea820-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="ea820-123">FallbackSource</span></span> | <span data-ttu-id="ea820-124">*（3.2 +)*要用作回退机制，以防主键中找不到包的包源的列表或默认源。</span><span class="sxs-lookup"><span data-stu-id="ea820-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="ea820-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ea820-125">ForceEnglishOutput</span></span> | <span data-ttu-id="ea820-126">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="ea820-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ea820-127">帮助</span><span class="sxs-lookup"><span data-stu-id="ea820-127">Help</span></span> | <span data-ttu-id="ea820-128">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="ea820-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="ea820-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ea820-129">MSBuildPath</span></span> | <span data-ttu-id="ea820-130">*（4.0 +)*指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="ea820-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ea820-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ea820-131">MSBuildVersion</span></span> | <span data-ttu-id="ea820-132">*（3.2 +)*指定要用于此命令的 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="ea820-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ea820-133">支持的值为 4、 12、 14、 15。</span><span class="sxs-lookup"><span data-stu-id="ea820-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="ea820-134">默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="ea820-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ea820-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="ea820-135">NoCache</span></span> | <span data-ttu-id="ea820-136">防止 NuGet 使用从本地计算机缓存的包。</span><span class="sxs-lookup"><span data-stu-id="ea820-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ea820-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ea820-137">NonInteractive</span></span> | <span data-ttu-id="ea820-138">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="ea820-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ea820-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="ea820-139">OutputDirectory</span></span> | <span data-ttu-id="ea820-140">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ea820-141">如果未不指定任何文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ea820-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="ea820-142">PackageSaveMode</span></span> | <span data-ttu-id="ea820-143">指定要保存包安装完成后的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="ea820-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="ea820-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="ea820-144">PackagesDirectory</span></span> | <span data-ttu-id="ea820-145">与 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="ea820-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="ea820-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="ea820-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="ea820-147">超时 （秒） 来解析项目到项目引用。</span><span class="sxs-lookup"><span data-stu-id="ea820-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="ea820-148">递归</span><span class="sxs-lookup"><span data-stu-id="ea820-148">Recursive</span></span> | <span data-ttu-id="ea820-149">*（4.0 +)*还原 UWP 和.NET 核心项目的所有引用项目。</span><span class="sxs-lookup"><span data-stu-id="ea820-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="ea820-150">不适用于使用项目`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="ea820-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="ea820-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="ea820-151">RequireConsent</span></span> | <span data-ttu-id="ea820-152">验证还原程序包启用了之前下载和安装包。</span><span class="sxs-lookup"><span data-stu-id="ea820-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ea820-153">有关详细信息，请参阅[程序包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ea820-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="ea820-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="ea820-154">SolutionDirectory</span></span> | <span data-ttu-id="ea820-155">指定的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-155">Specifies the solution folder.</span></span> <span data-ttu-id="ea820-156">不还原解决方案的包时才有效。</span><span class="sxs-lookup"><span data-stu-id="ea820-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="ea820-157">源</span><span class="sxs-lookup"><span data-stu-id="ea820-157">Source</span></span> | <span data-ttu-id="ea820-158">指定包源的列表 （作为 Url) 要用于还原。</span><span class="sxs-lookup"><span data-stu-id="ea820-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="ea820-159">如果省略，则该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="ea820-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="ea820-160">详细级别</span><span class="sxs-lookup"><span data-stu-id="ea820-160">Verbosity</span></span> |<span data-ttu-id="ea820-161">> 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="ea820-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ea820-162">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ea820-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="ea820-163">备注</span><span class="sxs-lookup"><span data-stu-id="ea820-163">Remarks</span></span>

<span data-ttu-id="ea820-164">还原命令执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ea820-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="ea820-165">确定还原命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="ea820-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="ea820-166">projectPath 文件类型</span><span class="sxs-lookup"><span data-stu-id="ea820-166">projectPath file type</span></span> | <span data-ttu-id="ea820-167">行为</span><span class="sxs-lookup"><span data-stu-id="ea820-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="ea820-168">解决方案 （文件夹）</span><span class="sxs-lookup"><span data-stu-id="ea820-168">Solution (folder)</span></span> | <span data-ttu-id="ea820-169">NuGet 中寻找`.sln`文件，然后使用，如果找到; 否则为会出错。</span><span class="sxs-lookup"><span data-stu-id="ea820-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="ea820-170">`(SolutionDir)\.nuget` 使用作为起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ea820-171">`.sln` 文件</span><span class="sxs-lookup"><span data-stu-id="ea820-171">`.sln` file</span></span> | <span data-ttu-id="ea820-172">还原由解决方案; 标识的包如果将会出错`-SolutionDirectory`使用。</span><span class="sxs-lookup"><span data-stu-id="ea820-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="ea820-173">`$(SolutionDir)\.nuget` 使用作为起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ea820-174">`packages.config` 或项目文件</span><span class="sxs-lookup"><span data-stu-id="ea820-174">`packages.config` or project file</span></span> | <span data-ttu-id="ea820-175">还原文件，解决和安装依赖关系中列出的包。</span><span class="sxs-lookup"><span data-stu-id="ea820-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="ea820-176">其他文件类型</span><span class="sxs-lookup"><span data-stu-id="ea820-176">Other file type</span></span> | <span data-ttu-id="ea820-177">文件被假定为`.sln`文件作为上述; 如果它不是一种解决方案，NuGet 提供的错误。</span><span class="sxs-lookup"><span data-stu-id="ea820-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="ea820-178">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="ea820-178">(projectPath not specified)</span></span> | <span data-ttu-id="ea820-179">-NuGet 查找当前文件夹中的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="ea820-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="ea820-180">如果找到单个文件，一个用于还原包;如果找到多个解决方案，NuGet 将会出错。</span><span class="sxs-lookup"><span data-stu-id="ea820-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="ea820-181">-如果没有任何解决方案文件，查找 NuGet`packages.config`并使用该值来还原程序包。</span><span class="sxs-lookup"><span data-stu-id="ea820-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="ea820-182">-如果没有解决方案或`packages.config`文件找不到，NuGet 将会出错。</span><span class="sxs-lookup"><span data-stu-id="ea820-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="ea820-183">确定使用以下优先级顺序 （如果没有这些文件夹发现，NuGet 都显示一条错误） 的包文件夹：</span><span class="sxs-lookup"><span data-stu-id="ea820-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="ea820-184">使用指定的文件夹`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="ea820-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="ea820-185">`repositoryPath`中的值改 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="ea820-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="ea820-186">使用指定的文件夹 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="ea820-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="ea820-187">在还原时解决方案的包，NuGet 将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ea820-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="ea820-188">加载的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="ea820-188">Loads the solution file.</span></span>
    - <span data-ttu-id="ea820-189">还原中列出的解决方案级别包`$(SolutionDir)\.nuget\packages.config`到`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="ea820-190">还原中列出的包`$(ProjectDir)\packages.config`到`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea820-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="ea820-191">对于每个指定的包，还原并行中的包，除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="ea820-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="ea820-192">示例</span><span class="sxs-lookup"><span data-stu-id="ea820-192">Examples</span></span>

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
