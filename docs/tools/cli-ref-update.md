---
title: NuGet CLI update 命令
description: Nuget.exe 更新命令的引用
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145600"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="b4414-103">update 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b4414-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="b4414-104">**适用于：** 打包消耗&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="b4414-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b4414-105">更新项目中的所有包 (使用`packages.config`) 到其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="b4414-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="b4414-106">建议运行[还原](cli-ref-restore.md)运行之前`update`。</span><span class="sxs-lookup"><span data-stu-id="b4414-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="b4414-107">(若要更新的单个包，请使用[ `nuget install` ](cli-ref-install.md)而无需指定的版本号，在其中写 NuGet 安装最新版本。)</span><span class="sxs-lookup"><span data-stu-id="b4414-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="b4414-108">注意：`update`并不适用于 CLI 下运行 Mono （Mac OSX 或 Linux） 或使用 PackageReference 格式时。</span><span class="sxs-lookup"><span data-stu-id="b4414-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="b4414-109">`update`命令还会更新项目文件中的程序集引用、 提供这些引用已存在。</span><span class="sxs-lookup"><span data-stu-id="b4414-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="b4414-110">如果更新的包已添加的程序集，则新引用*不*添加。</span><span class="sxs-lookup"><span data-stu-id="b4414-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="b4414-111">新的包依赖项也没有添加其程序集引用。</span><span class="sxs-lookup"><span data-stu-id="b4414-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="b4414-112">若要更新的一部分中包括这些操作，更新 Visual Studio 中使用包管理器 UI 或程序包管理器控制台中的包。</span><span class="sxs-lookup"><span data-stu-id="b4414-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="b4414-113">此命令还可用于更新 nuget.exe 本身使用 *-自助*标志。</span><span class="sxs-lookup"><span data-stu-id="b4414-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="b4414-114">用法</span><span class="sxs-lookup"><span data-stu-id="b4414-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="b4414-115">其中`<configPath>`标识或者`packages.config`或解决方案文件，其中列出项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="b4414-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="b4414-116">选项</span><span class="sxs-lookup"><span data-stu-id="b4414-116">Options</span></span>

| <span data-ttu-id="b4414-117">选项</span><span class="sxs-lookup"><span data-stu-id="b4414-117">Option</span></span> | <span data-ttu-id="b4414-118">描述</span><span class="sxs-lookup"><span data-stu-id="b4414-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4414-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b4414-119">ConfigFile</span></span> | <span data-ttu-id="b4414-120">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="b4414-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b4414-121">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="b4414-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b4414-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="b4414-122">FileConflictAction</span></span> | <span data-ttu-id="b4414-123">指定当需要覆盖或忽略现有的项目所引用的文件时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="b4414-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b4414-124">值为*覆盖，忽略无*。</span><span class="sxs-lookup"><span data-stu-id="b4414-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="b4414-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b4414-125">ForceEnglishOutput</span></span> | <span data-ttu-id="b4414-126">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="b4414-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b4414-127">帮助</span><span class="sxs-lookup"><span data-stu-id="b4414-127">Help</span></span> | <span data-ttu-id="b4414-128">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="b4414-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="b4414-129">Id</span><span class="sxs-lookup"><span data-stu-id="b4414-129">Id</span></span> | <span data-ttu-id="b4414-130">指定包 Id，以更新的列表。</span><span class="sxs-lookup"><span data-stu-id="b4414-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="b4414-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="b4414-131">MSBuildPath</span></span> | <span data-ttu-id="b4414-132">*（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="b4414-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="b4414-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="b4414-133">MSBuildVersion</span></span> | <span data-ttu-id="b4414-134">*（3.2 +)* 指定要用于此命令的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="b4414-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b4414-135">支持的值为 4，12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7、 15.8，15.9。</span><span class="sxs-lookup"><span data-stu-id="b4414-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="b4414-136">默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="b4414-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="b4414-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b4414-137">NonInteractive</span></span> | <span data-ttu-id="b4414-138">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="b4414-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b4414-139">预发行版</span><span class="sxs-lookup"><span data-stu-id="b4414-139">PreRelease</span></span> | <span data-ttu-id="b4414-140">允许更新预发布版本。</span><span class="sxs-lookup"><span data-stu-id="b4414-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="b4414-141">更新已安装的预发行包时，则不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="b4414-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="b4414-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="b4414-142">RepositoryPath</span></span> | <span data-ttu-id="b4414-143">指定安装包的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="b4414-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="b4414-144">安全</span><span class="sxs-lookup"><span data-stu-id="b4414-144">Safe</span></span> | <span data-ttu-id="b4414-145">指定仅更新使用相同的主版本号和次版本中可用的最高版本将安装已安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="b4414-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="b4414-146">自助</span><span class="sxs-lookup"><span data-stu-id="b4414-146">Self</span></span> | <span data-ttu-id="b4414-147">Nuget.exe 更新到最新版本;将忽略所有其他参数。</span><span class="sxs-lookup"><span data-stu-id="b4414-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="b4414-148">源</span><span class="sxs-lookup"><span data-stu-id="b4414-148">Source</span></span> | <span data-ttu-id="b4414-149">指定包源的列表 （作为 Url) 若要使用的更新。</span><span class="sxs-lookup"><span data-stu-id="b4414-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="b4414-150">如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="b4414-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="b4414-151">详细级别</span><span class="sxs-lookup"><span data-stu-id="b4414-151">Verbosity</span></span> | <span data-ttu-id="b4414-152">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="b4414-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="b4414-153">版本</span><span class="sxs-lookup"><span data-stu-id="b4414-153">Version</span></span> | <span data-ttu-id="b4414-154">当用于一个包 ID，指定要更新的包的版本。</span><span class="sxs-lookup"><span data-stu-id="b4414-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="b4414-155">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b4414-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b4414-156">示例</span><span class="sxs-lookup"><span data-stu-id="b4414-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
