---
title: 使用 nuget.exe CLI 管理 NuGet 包
description: 有关使用 nuget.exe CLI 处理 NuGet 包的说明。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317737"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="2fabd-103">使用 nuget.exe CLI 管理包</span><span class="sxs-lookup"><span data-stu-id="2fabd-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="2fabd-104">通过 CLI 工具可轻松更新和还原项目和解决方案中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="2fabd-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="2fabd-105">该工具提供 Windows 上的所有 NuGet 功能以及 Mac 和 Linux 上在 Mono 下运行时的大多数功能。</span><span class="sxs-lookup"><span data-stu-id="2fabd-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="2fabd-106">`nuget.exe` CLI 适用于 .NET Framework 项目和非 SDK 样式项目（例如，面向 .NET Standard 库的非 SDK 样式项目）。</span><span class="sxs-lookup"><span data-stu-id="2fabd-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="2fabd-107">如果你使用的是已迁移到 `PackageReference` 的非 SDK 样式项目，请改用 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="2fabd-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="2fabd-108">`nuget.exe` CLI 需要 [packages.config](../reference/packages-config.md) 文件来进行包引用。</span><span class="sxs-lookup"><span data-stu-id="2fabd-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="2fabd-109">在大多数情况下，建议[将使用 `packages.config` 的非 SDK 样式项目迁移至 PackageReference](../reference/migrate-packages-config-to-package-reference.md)，然后可以使用 `dotnet` CLI 而不是 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="2fabd-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="2fabd-110">目前，C++ 和 ASP.NET 项目无法进行迁移。</span><span class="sxs-lookup"><span data-stu-id="2fabd-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="2fabd-111">本文介绍了一些最常见的 `nuget.exe` CLI 命令的基本用法。</span><span class="sxs-lookup"><span data-stu-id="2fabd-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="2fabd-112">对于大多数这些命令，CLI 工具在当前目录中查找项目文件，除非在命令中指定了项目文件。</span><span class="sxs-lookup"><span data-stu-id="2fabd-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="2fabd-113">有关命令和可能使用的参数的完整列表，请参阅 [nuget.exe CLI 参考](../reference/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2fabd-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fabd-114">系统必备</span><span class="sxs-lookup"><span data-stu-id="2fabd-114">Prerequisites</span></span>

- <span data-ttu-id="2fabd-115">要安装 `nuget.exe` CLI，从 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下载它，将 `.exe` 文件保存到合适的文件夹，然后将该文件夹添加到 PATH 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="2fabd-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="2fabd-116">安装包</span><span class="sxs-lookup"><span data-stu-id="2fabd-116">Install a package</span></span>

<span data-ttu-id="2fabd-117">[install](../reference/cli-reference/cli-ref-install.md) 命令使用指定的包源将包下载并安装到项目中，默认为当前文件夹。</span><span class="sxs-lookup"><span data-stu-id="2fabd-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="2fabd-118">将新包安装到项目根目录的“包”文件夹中  。</span><span class="sxs-lookup"><span data-stu-id="2fabd-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fabd-119">`install` 命令不会修改项目文件或 packages.config  ；在这种方式下，它类似于 `restore`，因为它只向磁盘添加包，而不更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="2fabd-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="2fabd-120">要添加依赖项，请通过 Visual Studio 中的包管理器 UI 或控制台添加包，或修改 packages.config  ，然后运行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="2fabd-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="2fabd-121">打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="2fabd-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="2fabd-122">使用以下命令将 NuGet 包安装到“包”文件夹  。</span><span class="sxs-lookup"><span data-stu-id="2fabd-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="2fabd-123">要将 `Newtonsoft.json` 包安装到“包”文件夹，请使用以下命令  ：</span><span class="sxs-lookup"><span data-stu-id="2fabd-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="2fabd-124">或者可以使用以下命令将现有 `packages.config` 文件的 NuGet 包安装到“包”  文件夹。</span><span class="sxs-lookup"><span data-stu-id="2fabd-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="2fabd-125">该操作不会将包添加到项目依赖项中，而是在本地安装它。</span><span class="sxs-lookup"><span data-stu-id="2fabd-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="2fabd-126">安装特定版本的包</span><span class="sxs-lookup"><span data-stu-id="2fabd-126">Install a specific version of a package</span></span>

<span data-ttu-id="2fabd-127">如果在使用 [install](../reference/cli-reference/cli-ref-install.md) 命令时未指定版本，NuGet 将安装最新版本的包。</span><span class="sxs-lookup"><span data-stu-id="2fabd-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="2fabd-128">还可以安装特定版本的 Nuget 包：</span><span class="sxs-lookup"><span data-stu-id="2fabd-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="2fabd-129">例如，要添加 `Newtonsoft.json` 包的 12.0.1 版，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="2fabd-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="2fabd-130">有关 `install` 的限制和行为的详细信息，请参阅[安装包](#install-a-package)。</span><span class="sxs-lookup"><span data-stu-id="2fabd-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="2fabd-131">删除包</span><span class="sxs-lookup"><span data-stu-id="2fabd-131">Remove a package</span></span>

<span data-ttu-id="2fabd-132">要删除一个或多个包，请从“包”文件夹中删除要删除的包  。</span><span class="sxs-lookup"><span data-stu-id="2fabd-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="2fabd-133">如果要重新安装包，请使用 `restore` 或 `install` 命令。</span><span class="sxs-lookup"><span data-stu-id="2fabd-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="2fabd-134">列出包</span><span class="sxs-lookup"><span data-stu-id="2fabd-134">List packages</span></span>

<span data-ttu-id="2fabd-135">可以使用 [list](../reference/cli-reference/cli-ref-list.md) 命令显示给定源的包列表。</span><span class="sxs-lookup"><span data-stu-id="2fabd-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="2fabd-136">使用 `-Source` 选项限制搜索。</span><span class="sxs-lookup"><span data-stu-id="2fabd-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="2fabd-137">例如，列出“包”文件夹中的包  。</span><span class="sxs-lookup"><span data-stu-id="2fabd-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="2fabd-138">如果使用搜索词，则搜索包括包名称、标记和包描述。</span><span class="sxs-lookup"><span data-stu-id="2fabd-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="2fabd-139">更新单个包</span><span class="sxs-lookup"><span data-stu-id="2fabd-139">Update an individual package</span></span>

<span data-ttu-id="2fabd-140">除非指定包版本，否则 NuGet 会在使用 `install` 命令时安装最新版本的包。</span><span class="sxs-lookup"><span data-stu-id="2fabd-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="2fabd-141">更新所有包</span><span class="sxs-lookup"><span data-stu-id="2fabd-141">Update all packages</span></span>

<span data-ttu-id="2fabd-142">使用 [update](../reference/cli-reference/cli-ref-update.md) 命令更新所有包。</span><span class="sxs-lookup"><span data-stu-id="2fabd-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="2fabd-143">将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="2fabd-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="2fabd-144">建议在运行 `update` 之前运行 `restore`。</span><span class="sxs-lookup"><span data-stu-id="2fabd-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="2fabd-145">还原包</span><span class="sxs-lookup"><span data-stu-id="2fabd-145">Restore packages</span></span>

<span data-ttu-id="2fabd-146">使用 [restore](../reference/cli-reference/cli-ref-restore.md) 命令，该命令可下载并安装“包”文件夹中缺少的所有包  。</span><span class="sxs-lookup"><span data-stu-id="2fabd-146">Use the [restore](../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="2fabd-147">`restore` 仅将包添加到磁盘，但不会更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="2fabd-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="2fabd-148">要还原项目依赖项，请修改 `packages.config`，然后使用 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="2fabd-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="2fabd-149">与其他 `nuget.exe` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="2fabd-149">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="2fabd-150">使用 `restore` 还原包：</span><span class="sxs-lookup"><span data-stu-id="2fabd-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```