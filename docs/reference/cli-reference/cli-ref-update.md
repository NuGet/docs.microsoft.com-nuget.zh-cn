---
title: NuGet CLI update 命令
description: nuget.exe update 命令的参考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622572"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5162f-103"> (NuGet CLI) 更新命令</span><span class="sxs-lookup"><span data-stu-id="5162f-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="5162f-104">**适用于：** 包使用 &bullet; **受支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="5162f-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5162f-105">将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="5162f-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5162f-106">建议在运行之前运行 ["还原"](cli-ref-restore.md) `update` 。</span><span class="sxs-lookup"><span data-stu-id="5162f-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="5162f-107"> (更新单个包，请使用 [`nuget install`](cli-ref-install.md) 而不指定版本号，在这种情况下，NuGet 安装最新版本。 ) </span><span class="sxs-lookup"><span data-stu-id="5162f-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5162f-108">注意：不适 `update` 用于在 Mono (MAC OSX 或 Linux) 下运行的 CLI 或使用 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="5162f-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="5162f-109">`update`命令还会更新项目文件中的程序集引用，前提是这些引用已存在。</span><span class="sxs-lookup"><span data-stu-id="5162f-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5162f-110">如果更新的包具有添加的程序集，则 *不* 会添加新引用。</span><span class="sxs-lookup"><span data-stu-id="5162f-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5162f-111">新的包依赖项也没有添加其程序集引用。</span><span class="sxs-lookup"><span data-stu-id="5162f-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5162f-112">若要将这些操作包括为更新的一部分，请使用包管理器 UI 或程序包管理器控制台在 Visual Studio 中更新包。</span><span class="sxs-lookup"><span data-stu-id="5162f-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5162f-113">此命令还可用于使用 *-self* 标志更新 nuget.exe 本身。</span><span class="sxs-lookup"><span data-stu-id="5162f-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5162f-114">使用情况</span><span class="sxs-lookup"><span data-stu-id="5162f-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="5162f-115">其中 `<configPath>` 标识 `packages.config` 列出项目依赖项的或解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="5162f-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5162f-116">选项</span><span class="sxs-lookup"><span data-stu-id="5162f-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5162f-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="5162f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5162f-118">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="5162f-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="5162f-119">指定当目标项目中已存在包的文件时的默认操作。</span><span class="sxs-lookup"><span data-stu-id="5162f-119">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="5162f-120">设置为 `Overwrite` 始终覆盖文件。</span><span class="sxs-lookup"><span data-stu-id="5162f-120">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="5162f-121">设置为 `Ignore` 以跳过文件。</span><span class="sxs-lookup"><span data-stu-id="5162f-121">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="5162f-122">`PromptUser`默认情况下，除非提供了或，否则该操作将提示输入每个冲突的文件 `OverwriteAll` `IgnoreAll` ，这将应用于所有剩余文件。</span><span class="sxs-lookup"><span data-stu-id="5162f-122">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5162f-123">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="5162f-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5162f-124">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="5162f-124">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="5162f-125">指定要更新的包 Id 列表。</span><span class="sxs-lookup"><span data-stu-id="5162f-125">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="5162f-126">\* (4.0 +) \* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="5162f-126">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="5162f-127">\* (3.2 +) \* 指定要与此命令一起使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="5162f-127">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5162f-128">支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="5162f-128">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="5162f-129">默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="5162f-129">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5162f-130">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="5162f-130">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="5162f-131">允许更新到预发布版本。</span><span class="sxs-lookup"><span data-stu-id="5162f-131">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5162f-132">更新已安装的预发布包时，不需要此标志。</span><span class="sxs-lookup"><span data-stu-id="5162f-132">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="5162f-133">指定安装包的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="5162f-133">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="5162f-134">指定仅安装具有与安装包相同的主要版本和次要版本中可用的最高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="5162f-134">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="5162f-135">将 nuget.exe 更新到最新版本;忽略所有其他参数。</span><span class="sxs-lookup"><span data-stu-id="5162f-135">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="5162f-136">指定包源的列表 (作为要用于更新) 的 Url。</span><span class="sxs-lookup"><span data-stu-id="5162f-136">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5162f-137">如果省略，则该命令使用配置文件中提供的源，请参阅 [常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="5162f-137">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5162f-138">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="5162f-138">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="5162f-139">与一个包 ID 一起使用时，指定要更新的包的版本。</span><span class="sxs-lookup"><span data-stu-id="5162f-139">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="5162f-140">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5162f-140">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5162f-141">示例</span><span class="sxs-lookup"><span data-stu-id="5162f-141">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
