---
title: NuGet CLI update 命令
description: 针对 nuget.exe update 命令的参考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327504"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="d116b-103">update 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d116b-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="d116b-104">**适用于:** 包&bullet;使用**受支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="d116b-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d116b-105">将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="d116b-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="d116b-106">建议在运行`update`之前运行["还原"](cli-ref-restore.md) 。</span><span class="sxs-lookup"><span data-stu-id="d116b-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="d116b-107">(若要更新单个包, 请[`nuget install`](cli-ref-install.md)使用而不指定版本号, 在这种情况下, NuGet 安装最新版本。)</span><span class="sxs-lookup"><span data-stu-id="d116b-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="d116b-108">注意: `update`不适用于在 Mono (Mac OSX 或 Linux) 下运行的 CLI 或使用 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="d116b-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="d116b-109">`update`命令还会更新项目文件中的程序集引用, 前提是这些引用已存在。</span><span class="sxs-lookup"><span data-stu-id="d116b-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="d116b-110">如果更新的包具有添加的程序集, 则*不*会添加新引用。</span><span class="sxs-lookup"><span data-stu-id="d116b-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="d116b-111">新的包依赖项也没有添加其程序集引用。</span><span class="sxs-lookup"><span data-stu-id="d116b-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="d116b-112">若要将这些操作包括为更新的一部分, 请使用包管理器 UI 或程序包管理器控制台在 Visual Studio 中更新包。</span><span class="sxs-lookup"><span data-stu-id="d116b-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="d116b-113">此命令还可用于使用 *-self*标志更新 nuget.exe 本身。</span><span class="sxs-lookup"><span data-stu-id="d116b-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="d116b-114">用法</span><span class="sxs-lookup"><span data-stu-id="d116b-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="d116b-115">其中`<configPath>` 标识`packages.config`列出项目依赖项的或解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="d116b-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="d116b-116">选项</span><span class="sxs-lookup"><span data-stu-id="d116b-116">Options</span></span>

| <span data-ttu-id="d116b-117">选项</span><span class="sxs-lookup"><span data-stu-id="d116b-117">Option</span></span> | <span data-ttu-id="d116b-118">描述</span><span class="sxs-lookup"><span data-stu-id="d116b-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d116b-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d116b-119">ConfigFile</span></span> | <span data-ttu-id="d116b-120">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="d116b-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d116b-121">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="d116b-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d116b-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d116b-122">FileConflictAction</span></span> | <span data-ttu-id="d116b-123">指定在要求覆盖或忽略项目引用的现有文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="d116b-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d116b-124">值为*overwrite、ignore、none*。</span><span class="sxs-lookup"><span data-stu-id="d116b-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="d116b-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d116b-125">ForceEnglishOutput</span></span> | <span data-ttu-id="d116b-126">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="d116b-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d116b-127">Help</span><span class="sxs-lookup"><span data-stu-id="d116b-127">Help</span></span> | <span data-ttu-id="d116b-128">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="d116b-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="d116b-129">Id</span><span class="sxs-lookup"><span data-stu-id="d116b-129">Id</span></span> | <span data-ttu-id="d116b-130">指定要更新的包 Id 列表。</span><span class="sxs-lookup"><span data-stu-id="d116b-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="d116b-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="d116b-131">MSBuildPath</span></span> | <span data-ttu-id="d116b-132">*(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径, 优先于`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="d116b-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="d116b-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="d116b-133">MSBuildVersion</span></span> | <span data-ttu-id="d116b-134">*(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="d116b-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="d116b-135">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="d116b-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="d116b-136">默认情况下, 将选取路径中的 MSBuild, 否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="d116b-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="d116b-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d116b-137">NonInteractive</span></span> | <span data-ttu-id="d116b-138">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="d116b-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d116b-139">早期</span><span class="sxs-lookup"><span data-stu-id="d116b-139">PreRelease</span></span> | <span data-ttu-id="d116b-140">允许更新到预发布版本。</span><span class="sxs-lookup"><span data-stu-id="d116b-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="d116b-141">更新已安装的预发布包时, 不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="d116b-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="d116b-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="d116b-142">RepositoryPath</span></span> | <span data-ttu-id="d116b-143">指定安装包的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="d116b-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="d116b-144">防</span><span class="sxs-lookup"><span data-stu-id="d116b-144">Safe</span></span> | <span data-ttu-id="d116b-145">指定仅安装具有与安装包相同的主要版本和次要版本中可用的最高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="d116b-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="d116b-146">解压</span><span class="sxs-lookup"><span data-stu-id="d116b-146">Self</span></span> | <span data-ttu-id="d116b-147">将 nuget.exe 更新到最新版本;忽略所有其他参数。</span><span class="sxs-lookup"><span data-stu-id="d116b-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="d116b-148">Source</span><span class="sxs-lookup"><span data-stu-id="d116b-148">Source</span></span> | <span data-ttu-id="d116b-149">指定要用于更新的包源 (作为 Url) 的列表。</span><span class="sxs-lookup"><span data-stu-id="d116b-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="d116b-150">如果省略, 则该命令使用配置文件中提供的源, 请参阅[常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="d116b-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="d116b-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d116b-151">Verbosity</span></span> | <span data-ttu-id="d116b-152">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="d116b-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="d116b-153">Version</span><span class="sxs-lookup"><span data-stu-id="d116b-153">Version</span></span> | <span data-ttu-id="d116b-154">与一个包 ID 一起使用时, 指定要更新的包的版本。</span><span class="sxs-lookup"><span data-stu-id="d116b-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="d116b-155">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d116b-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d116b-156">示例</span><span class="sxs-lookup"><span data-stu-id="d116b-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
