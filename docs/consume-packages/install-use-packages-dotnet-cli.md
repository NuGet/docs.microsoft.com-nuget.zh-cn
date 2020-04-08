---
title: 使用 dotnet CLI 安装和管理 NuGet 包
description: 有关使用 dotnet CLI 处理 NuGet 包的说明。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825151"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="277c4-103">使用 dotnet CLI 安装和管理包</span><span class="sxs-lookup"><span data-stu-id="277c4-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="277c4-104">通过 CLI 工具可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="277c4-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="277c4-105">它可在 Windows、Mac OS X 和 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="277c4-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="277c4-106">dotnet CLI 适用于 .NET Core 和 .NET Standard 项目（SDK 样式的项目类型），以及任何其他 SDK 样式项目（例如，面向 .NET Framework 的 SDK 样式项目）。</span><span class="sxs-lookup"><span data-stu-id="277c4-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="277c4-107">有关更多信息，请参阅 [SDK 属性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="277c4-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="277c4-108">本文介绍了一些最常见的 dotnet CLI 命令的基本用法。</span><span class="sxs-lookup"><span data-stu-id="277c4-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="277c4-109">对于这些中的大多数命令，CLI 工具在当前目录中查找项目文件，除非在命令中指定了项目文件（项目文件是一个可选开关）。</span><span class="sxs-lookup"><span data-stu-id="277c4-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="277c4-110">如需获取命令的完整列表和可能使用的参数，请参阅 [.NET Core 命令行界面 (CLI) 工具](../reference/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="277c4-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="277c4-111">必备条件</span><span class="sxs-lookup"><span data-stu-id="277c4-111">Prerequisites</span></span>

- <span data-ttu-id="277c4-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="277c4-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="277c4-113">从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="277c4-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="277c4-114">安装包</span><span class="sxs-lookup"><span data-stu-id="277c4-114">Install a package</span></span>

<span data-ttu-id="277c4-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 添加对项目文件的包引用，然后运行 `dotnet restore` 以安装包。</span><span class="sxs-lookup"><span data-stu-id="277c4-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="277c4-116">打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="277c4-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="277c4-117">运行以下命令安装 Nuget 包：</span><span class="sxs-lookup"><span data-stu-id="277c4-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="277c4-118">例如，若要安装 `Newtonsoft.Json` 包，请使用以下命令</span><span class="sxs-lookup"><span data-stu-id="277c4-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="277c4-119">命令完成后，查看项目文件以确保已安装该包。</span><span class="sxs-lookup"><span data-stu-id="277c4-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="277c4-120">可以打开 `.csproj` 文件以查看添加的引用：</span><span class="sxs-lookup"><span data-stu-id="277c4-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="277c4-121">安装特定版本的包</span><span class="sxs-lookup"><span data-stu-id="277c4-121">Install a specific version of a package</span></span>

<span data-ttu-id="277c4-122">如果未指定版本，NuGet 将安装最新版本的包。</span><span class="sxs-lookup"><span data-stu-id="277c4-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="277c4-123">还可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令安装特定版本的 Nuget 包：</span><span class="sxs-lookup"><span data-stu-id="277c4-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="277c4-124">例如，要添加 `Newtonsoft.Json` 包的 12.0.1 版，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="277c4-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="277c4-125">NuGet 包引用</span><span class="sxs-lookup"><span data-stu-id="277c4-125">List package references</span></span>

<span data-ttu-id="277c4-126">可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出项目的包引用。</span><span class="sxs-lookup"><span data-stu-id="277c4-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="277c4-127">删除包</span><span class="sxs-lookup"><span data-stu-id="277c4-127">Remove a package</span></span>

<span data-ttu-id="277c4-128">使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令从项目文件中移除包引用。</span><span class="sxs-lookup"><span data-stu-id="277c4-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="277c4-129">例如，要移除 `Newtonsoft.Json` 包，请使用以下命令</span><span class="sxs-lookup"><span data-stu-id="277c4-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="277c4-130">更新包</span><span class="sxs-lookup"><span data-stu-id="277c4-130">Update a package</span></span>

<span data-ttu-id="277c4-131">除非指定包版本，否则 NuGet 会在使用 `dotnet add package` 命令时安装最新版本的包（`-v` 开关）。</span><span class="sxs-lookup"><span data-stu-id="277c4-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="277c4-132">还原包</span><span class="sxs-lookup"><span data-stu-id="277c4-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
