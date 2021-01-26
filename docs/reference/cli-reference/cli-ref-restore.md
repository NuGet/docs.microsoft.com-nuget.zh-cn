---
title: NuGet CLI restore 命令
description: nuget.exe restore 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780025"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="8937a-103"> (NuGet CLI 还原命令) </span><span class="sxs-lookup"><span data-stu-id="8937a-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="8937a-104">**适用于：** 包使用 &bullet; **受支持的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="8937a-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="8937a-105">下载并安装文件夹中缺少的任何程序包 `packages` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="8937a-106">与 NuGet 4.0 + 和 PackageReference 格式一起使用时，会 `<project>.nuget.props` 在需要时在文件夹中生成文件 `obj` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="8937a-107"> (可以从源代码管理中省略该文件。 ) </span><span class="sxs-lookup"><span data-stu-id="8937a-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="8937a-108">在 Mono 上带有 CLI 的 Mac OSX 和 Linux 上，PackageReference 不支持还原包。</span><span class="sxs-lookup"><span data-stu-id="8937a-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="8937a-109">使用情况</span><span class="sxs-lookup"><span data-stu-id="8937a-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="8937a-110">其中 `<projectPath>` 指定解决方案或文件的位置 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="8937a-111">有关行为的详细信息，请参阅下面的 [备注](#remarks) 。</span><span class="sxs-lookup"><span data-stu-id="8937a-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="8937a-112">选项</span><span class="sxs-lookup"><span data-stu-id="8937a-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8937a-113">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="8937a-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8937a-114">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="8937a-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="8937a-115">*(4.0 +)* 直接下载包，而不填充包含任何二进制文件或元数据的缓存。</span><span class="sxs-lookup"><span data-stu-id="8937a-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="8937a-116">禁用并行还原多个包。</span><span class="sxs-lookup"><span data-stu-id="8937a-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="8937a-117">*(3.2 +)* 在主或默认源中找不到包时要用作回退的包的列表。</span><span class="sxs-lookup"><span data-stu-id="8937a-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="8937a-118">使用分号分隔列表项。</span><span class="sxs-lookup"><span data-stu-id="8937a-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="8937a-119">在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。</span><span class="sxs-lookup"><span data-stu-id="8937a-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="8937a-120">指定此标志与删除 `project.assets.json` 文件类似。</span><span class="sxs-lookup"><span data-stu-id="8937a-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="8937a-121">这不会绕过 http 缓存。</span><span class="sxs-lookup"><span data-stu-id="8937a-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8937a-122">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="8937a-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="8937a-123">即使锁定文件已存在，也会强制还原以重新评估所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="8937a-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8937a-124">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="8937a-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="8937a-125">写入项目锁定文件的输出位置。</span><span class="sxs-lookup"><span data-stu-id="8937a-125">Output location where project lock file is written.</span></span> <span data-ttu-id="8937a-126">默认情况下，该属性为 `PROJECT_ROOT\packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="8937a-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="8937a-127">不允许更新项目锁定文件。</span><span class="sxs-lookup"><span data-stu-id="8937a-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="8937a-128">*(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="8937a-129">*(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="8937a-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="8937a-130">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="8937a-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="8937a-131">默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="8937a-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="8937a-132">阻止 NuGet 使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="8937a-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="8937a-133">请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="8937a-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8937a-134">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="8937a-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="8937a-135">指定在其中安装包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8937a-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="8937a-136">如果未指定文件夹，则使用当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="8937a-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="8937a-137">使用文件进行还原时必需， `packages.config` 除非 `PackagesDirectory` `SolutionDirectory` 使用或。</span><span class="sxs-lookup"><span data-stu-id="8937a-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="8937a-138">指定包安装后要保存的文件类型： `nuspec` 、 `nupkg` 或 `nuspec;nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="8937a-139">与 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="8937a-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="8937a-140">使用文件进行还原时必需， `packages.config` 除非 `OutputDirectory` `SolutionDirectory` 使用或。</span><span class="sxs-lookup"><span data-stu-id="8937a-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="8937a-141">解析项目到项目引用的超时时间（秒）。</span><span class="sxs-lookup"><span data-stu-id="8937a-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="8937a-142">*(4.0 +)* 还原 UWP 和 .NET Core 项目的所有引用项目。</span><span class="sxs-lookup"><span data-stu-id="8937a-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="8937a-143">不适用于使用 `packages.config` 的项目。</span><span class="sxs-lookup"><span data-stu-id="8937a-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="8937a-144">验证在下载和安装包之前是否启用了还原包。</span><span class="sxs-lookup"><span data-stu-id="8937a-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="8937a-145">有关详细信息，请参阅 [包还原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="8937a-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="8937a-146">指定解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="8937a-146">Specifies the solution folder.</span></span> <span data-ttu-id="8937a-147">还原解决方案的包时无效。</span><span class="sxs-lookup"><span data-stu-id="8937a-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="8937a-148">使用文件进行还原时必需， `packages.config` 除非 `PackagesDirectory` `OutputDirectory` 使用或。</span><span class="sxs-lookup"><span data-stu-id="8937a-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="8937a-149">将包源的列表指定为要用于还原的 Url)  (。</span><span class="sxs-lookup"><span data-stu-id="8937a-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="8937a-150">如果省略，则该命令将使用配置文件中提供的源，请参阅 [配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="8937a-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8937a-151">使用分号分隔列表项。</span><span class="sxs-lookup"><span data-stu-id="8937a-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="8937a-152">允许生成项目锁定文件并与还原一起使用。</span><span class="sxs-lookup"><span data-stu-id="8937a-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8937a-153">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="8937a-154">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8937a-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="8937a-155">备注</span><span class="sxs-lookup"><span data-stu-id="8937a-155">Remarks</span></span>

<span data-ttu-id="8937a-156">Restore 命令执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8937a-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="8937a-157">确定 restore 命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="8937a-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="8937a-158">projectPath 文件类型</span><span class="sxs-lookup"><span data-stu-id="8937a-158">projectPath file type</span></span> | <span data-ttu-id="8937a-159">行为</span><span class="sxs-lookup"><span data-stu-id="8937a-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="8937a-160">解决方案 (文件夹) </span><span class="sxs-lookup"><span data-stu-id="8937a-160">Solution (folder)</span></span> | <span data-ttu-id="8937a-161">NuGet 查找 `.sln` 文件并使用该文件（如果找到的话）; 否则将会出现错误。</span><span class="sxs-lookup"><span data-stu-id="8937a-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="8937a-162">`(SolutionDir)\.nuget` 用作起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="8937a-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="8937a-163">`.sln` 文件</span><span class="sxs-lookup"><span data-stu-id="8937a-163">`.sln` file</span></span> | <span data-ttu-id="8937a-164">还原解决方案标识的包;如果 `-SolutionDirectory` 使用了，则会出现错误。</span><span class="sxs-lookup"><span data-stu-id="8937a-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="8937a-165">`$(SolutionDir)\.nuget` 用作起始文件夹。</span><span class="sxs-lookup"><span data-stu-id="8937a-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="8937a-166">`packages.config` 或项目文件</span><span class="sxs-lookup"><span data-stu-id="8937a-166">`packages.config` or project file</span></span> | <span data-ttu-id="8937a-167">还原文件中列出的包，解析和安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="8937a-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="8937a-168">其他文件类型</span><span class="sxs-lookup"><span data-stu-id="8937a-168">Other file type</span></span> | <span data-ttu-id="8937a-169">文件被假定为如上所述的 `.sln` 文件; 如果该文件不是解决方案，NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="8937a-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="8937a-170">未指定 (projectPath) </span><span class="sxs-lookup"><span data-stu-id="8937a-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="8937a-171">NuGet 在当前文件夹中查找解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="8937a-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="8937a-172">如果找到一个文件，则使用该文件还原包;如果找到多个解决方案，NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="8937a-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="8937a-173">如果没有解决方案文件，NuGet 将查找 `packages.config` 并使用它来还原包。</span><span class="sxs-lookup"><span data-stu-id="8937a-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="8937a-174">如果未找到任何解决方案或 `packages.config` 文件，NuGet 将提供错误。</span><span class="sxs-lookup"><span data-stu-id="8937a-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="8937a-175">使用以下优先级顺序确定包文件夹 (NuGet 会在找不到任何这些文件夹时出现错误) ：</span><span class="sxs-lookup"><span data-stu-id="8937a-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="8937a-176">用指定的文件夹 `-PackagesDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="8937a-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="8937a-177">`repositoryPath`中的值`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="8937a-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="8937a-178">指定的文件夹 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="8937a-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="8937a-179">还原解决方案的包时，NuGet 会执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8937a-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="8937a-180">加载解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="8937a-180">Loads the solution file.</span></span>
    - <span data-ttu-id="8937a-181">将中列出的解决方案级别包还原 `$(SolutionDir)\.nuget\packages.config` 到 `packages` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8937a-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="8937a-182">将中列出的包还原 `$(ProjectDir)\packages.config` 到 `packages` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8937a-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="8937a-183">对于指定的每个包，请并行还原包，除非 `-DisableParallelProcessing` 指定了。</span><span class="sxs-lookup"><span data-stu-id="8937a-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="8937a-184">示例</span><span class="sxs-lookup"><span data-stu-id="8937a-184">Examples</span></span>

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
