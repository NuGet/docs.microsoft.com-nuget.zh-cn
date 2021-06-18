---
title: NuGet CLI 更新命令
description: nuget.exe update 命令的引用
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323643"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="ff67c-103">NuGet CLI (update) </span><span class="sxs-lookup"><span data-stu-id="ff67c-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="ff67c-104">**适用于：包** 消耗 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="ff67c-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ff67c-105">将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="ff67c-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ff67c-106">建议在运行 [之前运行"还原](cli-ref-restore.md) `update` "。</span><span class="sxs-lookup"><span data-stu-id="ff67c-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="ff67c-107"> (若要更新单个包，请使用 而不指定版本号，在这种情况下 [`nuget install`](cli-ref-install.md) ，NuGet 将安装最新版本.) </span><span class="sxs-lookup"><span data-stu-id="ff67c-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="ff67c-108">注意：在 Mono 下运行的 CLI (Mac OSX 或 Linux) `update` 使用 PackageReference 格式时。</span><span class="sxs-lookup"><span data-stu-id="ff67c-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="ff67c-109">该命令 `update` 还会更新项目文件中程序集引用，只要这些引用已存在。</span><span class="sxs-lookup"><span data-stu-id="ff67c-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="ff67c-110">如果更新的包具有已添加的程序集，则不添加 *新* 引用。</span><span class="sxs-lookup"><span data-stu-id="ff67c-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="ff67c-111">新包依赖项也尚未添加其程序集引用。</span><span class="sxs-lookup"><span data-stu-id="ff67c-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="ff67c-112">若要在更新中包括这些操作，请通过 Visual Studio UI 或 程序包管理器 控制台程序包管理器包。</span><span class="sxs-lookup"><span data-stu-id="ff67c-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="ff67c-113">此命令还可用于使用 -self nuget.exe自行 *更新。*</span><span class="sxs-lookup"><span data-stu-id="ff67c-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="ff67c-114">使用情况</span><span class="sxs-lookup"><span data-stu-id="ff67c-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="ff67c-115">其中 `<configPath>` 标识列出 `packages.config` 项目依赖项的 或 解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="ff67c-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="ff67c-116">选项</span><span class="sxs-lookup"><span data-stu-id="ff67c-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ff67c-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ff67c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ff67c-118">如果未指定，则 (Windows) 或 `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` (`~/.config/NuGet/NuGet.Config` Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="ff67c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="ff67c-119">指定要使用的依赖项包的版本，可以是以下项之一：</span><span class="sxs-lookup"><span data-stu-id="ff67c-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ff67c-120">*最低* (默认) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="ff67c-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ff67c-121">*HighestPatch：* 主要版本最低、次要版本最低、修补程序最高版本</span><span class="sxs-lookup"><span data-stu-id="ff67c-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ff67c-122">*HighestMinor：* 具有最低主要版本、最高次要版本、最高修补程序版本</span><span class="sxs-lookup"><span data-stu-id="ff67c-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ff67c-123">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="ff67c-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="ff67c-124">*忽略*：不会使用依赖项包</span><span class="sxs-lookup"><span data-stu-id="ff67c-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="ff67c-125">指定目标项目中已存在包中的文件时的默认操作。</span><span class="sxs-lookup"><span data-stu-id="ff67c-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="ff67c-126">将 设置为 `Overwrite` 以始终覆盖文件。</span><span class="sxs-lookup"><span data-stu-id="ff67c-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="ff67c-127">设置为 可 `Ignore` 跳过文件。</span><span class="sxs-lookup"><span data-stu-id="ff67c-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="ff67c-128">除非提供 或 ，否则操作（默认）将提示输入每个冲突文件，这将 `PromptUser` `OverwriteAll` `IgnoreAll` 应用于所有剩余文件。</span><span class="sxs-lookup"><span data-stu-id="ff67c-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ff67c-129">*(3.5+)* 强制nuget.exe使用固定、基于英语的区域性运行。</span><span class="sxs-lookup"><span data-stu-id="ff67c-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ff67c-130">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="ff67c-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="ff67c-131">指定要更新的包 ID 的列表。</span><span class="sxs-lookup"><span data-stu-id="ff67c-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="ff67c-132">*(4.0+)* 指定要与 命令一起使用的 MSBuild 路径，并优先于 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="ff67c-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="ff67c-133">*(3.2+)* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="ff67c-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ff67c-134">支持的值包括 4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="ff67c-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ff67c-135">默认情况下，选择路径中的 MSBuild，否则默认为最高安装的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="ff67c-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ff67c-136">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="ff67c-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="ff67c-137">允许更新到预发行版本。</span><span class="sxs-lookup"><span data-stu-id="ff67c-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="ff67c-138">更新已安装的预发行包时，不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="ff67c-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="ff67c-139">指定安装包的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="ff67c-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="ff67c-140">指定只会安装与已安装包相同的主版本和次要版本中可用的最高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="ff67c-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="ff67c-141">对 `nuget.exe` 最新版本的更新。</span><span class="sxs-lookup"><span data-stu-id="ff67c-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="ff67c-142">`-Source` 可以使用 ，但忽略所有其他参数。</span><span class="sxs-lookup"><span data-stu-id="ff67c-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="ff67c-143">如果未提供源，则 `nuget.org` 检查更新，而不考虑 `NuGet.Config` 设置。</span><span class="sxs-lookup"><span data-stu-id="ff67c-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="ff67c-144">指定要用作更新 (URL) 包源的列表。</span><span class="sxs-lookup"><span data-stu-id="ff67c-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="ff67c-145">如果省略，该命令将使用配置文件中提供的源，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="ff67c-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ff67c-146">指定输出中显示的详细信息量： (`normal` 默认 `quiet`) 、 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="ff67c-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="ff67c-147">与一个包 ID 一同使用时， 指定要更新的包的版本。</span><span class="sxs-lookup"><span data-stu-id="ff67c-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="ff67c-148">另 [请参阅环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ff67c-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ff67c-149">示例</span><span class="sxs-lookup"><span data-stu-id="ff67c-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
