---
title: 使用 dotnet CLI 安装和管理 NuGet 包
description: 有关使用 dotnet CLI 处理 NuGet 包的说明。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842362"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="28826-103">使用 dotnet CLI 安装和管理包</span><span class="sxs-lookup"><span data-stu-id="28826-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="28826-104">通过 CLI 工具可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="28826-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="28826-105">它可在 Windows、Mac OS X 和 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="28826-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="28826-106">dotnet CLI 适用于 .NET Core 和 .NET Standard 项目（SDK 样式的项目类型），以及任何其他 SDK 样式项目（例如，面向 .NET Framework 的 SDK 样式项目）。</span><span class="sxs-lookup"><span data-stu-id="28826-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="28826-107">有关更多信息，请参阅 [SDK 属性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="28826-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="28826-108">本文介绍了一些最常见的 dotnet CLI 命令的基本用法。</span><span class="sxs-lookup"><span data-stu-id="28826-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="28826-109">对于这些中的大多数命令，CLI 工具在当前目录中查找项目文件，除非在命令中指定了项目文件（项目文件是一个可选开关）。</span><span class="sxs-lookup"><span data-stu-id="28826-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="28826-110">如需获取命令的完整列表和可能使用的参数，请参阅 [.NET Core 命令行界面 (CLI) 工具](../tools/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="28826-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28826-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="28826-111">Prerequisites</span></span>

- <span data-ttu-id="28826-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="28826-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="28826-113">从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="28826-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="28826-114">安装包</span><span class="sxs-lookup"><span data-stu-id="28826-114">Install a package</span></span>

<span data-ttu-id="28826-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 添加对项目文件的包引用，然后运行 `dotnet restore` 以安装包。</span><span class="sxs-lookup"><span data-stu-id="28826-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="28826-116">打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="28826-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="28826-117">运行以下命令安装 Nuget 包：</span><span class="sxs-lookup"><span data-stu-id="28826-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="28826-118">例如，若要安装 `Newtonsoft.Json` 包，请使用以下命令</span><span class="sxs-lookup"><span data-stu-id="28826-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="28826-119">命令完成后，查看项目文件以确保已安装该包。</span><span class="sxs-lookup"><span data-stu-id="28826-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="28826-120">可以打开 `.csproj` 文件以查看添加的引用：</span><span class="sxs-lookup"><span data-stu-id="28826-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="28826-121">安装特定版本的包</span><span class="sxs-lookup"><span data-stu-id="28826-121">Install a specific version of a package</span></span>

<span data-ttu-id="28826-122">如果未指定版本，NuGet 将安装最新版本的包。</span><span class="sxs-lookup"><span data-stu-id="28826-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="28826-123">还可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令安装特定版本的 Nuget 包：</span><span class="sxs-lookup"><span data-stu-id="28826-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="28826-124">例如，要添加 12.0.1 版的 `Newtonsoft.Json` 包，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="28826-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="28826-125">NuGet 包引用</span><span class="sxs-lookup"><span data-stu-id="28826-125">List package references</span></span>

<span data-ttu-id="28826-126">可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出项目的包引用。</span><span class="sxs-lookup"><span data-stu-id="28826-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="28826-127">移除包</span><span class="sxs-lookup"><span data-stu-id="28826-127">Remove a package</span></span>

<span data-ttu-id="28826-128">使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令从项目文件中移除包引用。</span><span class="sxs-lookup"><span data-stu-id="28826-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="28826-129">例如，要移除 `Newtonsoft.Json` 包，请使用以下命令</span><span class="sxs-lookup"><span data-stu-id="28826-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="28826-130">更新包</span><span class="sxs-lookup"><span data-stu-id="28826-130">Update a package</span></span>

<span data-ttu-id="28826-131">除非指定包版本，否则 NuGet 会在使用 `dotnet add package` 命令时安装最新版本的包（`-v` 开关）。</span><span class="sxs-lookup"><span data-stu-id="28826-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="28826-132">还原包</span><span class="sxs-lookup"><span data-stu-id="28826-132">Restore packages</span></span>

<span data-ttu-id="28826-133">使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。</span><span class="sxs-lookup"><span data-stu-id="28826-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="28826-134">使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。</span><span class="sxs-lookup"><span data-stu-id="28826-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="28826-135">从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。</span><span class="sxs-lookup"><span data-stu-id="28826-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="28826-136">与其他 `dotnet` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="28826-136">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="28826-137">使用 `dotnet restore` 还原包：</span><span class="sxs-lookup"><span data-stu-id="28826-137">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
