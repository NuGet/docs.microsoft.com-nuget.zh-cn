---
title: "安装 NuGet 包的方式 | Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "介绍将 NuGet 包安装到项目中的过程，包括磁盘上和适用的项目文件会发生的情况。"
keywords: "安装 NuGet, NuGet 包使用, 安装 NuGet 包, NuGet 包引用"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a><span data-ttu-id="443f7-104">安装 NuGet 包的不同方式</span><span class="sxs-lookup"><span data-stu-id="443f7-104">Different ways to install a NuGet Package</span></span>

<span data-ttu-id="443f7-105">使用以下任一方法下载和安装 NuGet 包（如果尚未安装，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)）：</span><span class="sxs-lookup"><span data-stu-id="443f7-105">NuGet packages are downloaded and installed using any of the following methods (see [Install NuGet client tools](../install-nuget-client-tools.md) if you don't have these installed already):</span></span>

| <span data-ttu-id="443f7-106">方法</span><span class="sxs-lookup"><span data-stu-id="443f7-106">Method</span></span> | <span data-ttu-id="443f7-107">描述</span><span class="sxs-lookup"><span data-stu-id="443f7-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="443f7-108">dotnet.exe CLI</span><span class="sxs-lookup"><span data-stu-id="443f7-108">dotnet.exe CLI</span></span><br/>`dotnet install <package_name>` | <span data-ttu-id="443f7-109">（所有平台）下载用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中，然后添加对项目文件的引用。</span><span class="sxs-lookup"><span data-stu-id="443f7-109">(All platforms) Downloads the package identified by \<package_name\>, expands its contents into a folder in the current directory, and adds a reference to the project file.</span></span> <span data-ttu-id="443f7-110">同时还要下载和安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="443f7-110">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="443f7-111">安装并使用包 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="443f7-111">Install and use a package (dotnet CLI)</span></span>](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[<span data-ttu-id="443f7-112">dotnet 命令</span><span class="sxs-lookup"><span data-stu-id="443f7-112">dotnet commands</span></span>](../tools/dotnet-commands.md)</li></ul> |
| <span data-ttu-id="443f7-113">包管理器 UI (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="443f7-113">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="443f7-114">（Windows 和 Mac）提供 UI，你可以通过此 UI 浏览、选择包，并将包及其依赖项安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="443f7-114">(Windows and Mac) Provides a UI through which you can browse, select, and install packages and their dependencies into a project.</span></span> <span data-ttu-id="443f7-115">将对已安装的程序包引用添加到项目文件。</span><span class="sxs-lookup"><span data-stu-id="443f7-115">Adds references to installed packages to the project file.</span></span><ul><li>[<span data-ttu-id="443f7-116">安装并使用包 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="443f7-116">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="443f7-117">程序包管理器 UI 引用 (Windows)</span><span class="sxs-lookup"><span data-stu-id="443f7-117">Package Manager UI reference (Windows)</span></span>](../tools/package-manager-ui.md)</li><li>[<span data-ttu-id="443f7-118">在项目中包括 NuGet 包 (Mac)</span><span class="sxs-lookup"><span data-stu-id="443f7-118">Including a NuGet package in your project (Mac)</span></span>](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| <span data-ttu-id="443f7-119">程序包管理器控制台 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="443f7-119">Package Manager Console (Visual Studio)</span></span><br/>`Install-Package <package_name>` | <span data-ttu-id="443f7-120">（仅限 Windows）下载并将用 \<package_name\> 识别的包安装到解决方案的指定项目中，然后添加对项目文件的引用。</span><span class="sxs-lookup"><span data-stu-id="443f7-120">(Windows only) Downloads and installs the package identified by \<package_name\> into a specified project in the solution, then adds a reference to the project file.</span></span> <span data-ttu-id="443f7-121">同时还要下载和安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="443f7-121">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="443f7-122">安装并使用包 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="443f7-122">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="443f7-123">程序包管理器控制台指南</span><span class="sxs-lookup"><span data-stu-id="443f7-123">Package Manager Console guide</span></span>](../tools/package-manager-console.md)</li></ul> |
| <span data-ttu-id="443f7-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="443f7-124">nuget.exe CLI</span></span><br/>`nuget install <package_name>` | <span data-ttu-id="443f7-125">（所有平台）下载用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中；还可以下载 `packages.config` 文件中列出的所有包。</span><span class="sxs-lookup"><span data-stu-id="443f7-125">(All platforms) Downloads the package identified by \<package_name\> and expands its contents into a folder in the current directory; can also download all packages listed in a `packages.config` file.</span></span> <span data-ttu-id="443f7-126">同时还要下载和安装依赖项，但对项目文件未进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="443f7-126">Also downloads and installs dependencies, but makes no changes to project files.</span></span><ul><li>[<span data-ttu-id="443f7-127">安装命令</span><span class="sxs-lookup"><span data-stu-id="443f7-127">install command</span></span>](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a><span data-ttu-id="443f7-128">常规安装过程</span><span class="sxs-lookup"><span data-stu-id="443f7-128">General install process</span></span>

<span data-ttu-id="443f7-129">一般情况下，NuGet 会执行以下操作，然后要求安装一个包：</span><span class="sxs-lookup"><span data-stu-id="443f7-129">In general, NuGet does the following then asked to install a package:</span></span>

1. <span data-ttu-id="443f7-130">获取包：</span><span class="sxs-lookup"><span data-stu-id="443f7-130">Acquire the package:</span></span>
    - <span data-ttu-id="443f7-131">检查请求的包是否已存在于缓存中（请参阅[管理 NuGet 缓存](managing-the-nuget-cache.md)）。</span><span class="sxs-lookup"><span data-stu-id="443f7-131">Check if the requested package already exists in a cache (see [Managing the NuGet cache](managing-the-nuget-cache.md)).</span></span>
    - <span data-ttu-id="443f7-132">如果包不在缓存中，请尝试从[配置文件](Configuring-NuGet-Behavior.md)中列出的源下载包。</span><span class="sxs-lookup"><span data-stu-id="443f7-132">If the package is not in the cache, attempt to download the package from the sources listed in the [configuration files](Configuring-NuGet-Behavior.md).</span></span>
      - <span data-ttu-id="443f7-133">对于使用 `packages.config` 引用格式的项目，NuGet 会使用配置中的源顺序。</span><span class="sxs-lookup"><span data-stu-id="443f7-133">For projects using the `packages.config` reference format, NuGet uses the order of the sources in the configuration.</span></span>
      - <span data-ttu-id="443f7-134">对于使用 PackageReference 格式的项目，NuGet 会先检查本地文件夹的源，再检查网络共享中的源，最后检查 HTTP (Internet) 源。</span><span class="sxs-lookup"><span data-stu-id="443f7-134">For projects using the PackageReference format, NuGet checks sources that are local folders first, then checks sources on network shares, then checks HTTP (Internet) sources.</span></span>
      - <span data-ttu-id="443f7-135">一般情况下，NuGet 检查源的顺序不具有特别意义，因为具有特定标识符和版本号的任意给定包在找到的源方面完全相同。</span><span class="sxs-lookup"><span data-stu-id="443f7-135">In general, the order in which NuGet checks sources isn't particularly meaningful, because any given package with a specific identifier and version number is exactly the same on whatever source it's found.</span></span>
    - <span data-ttu-id="443f7-136">如果该包是从其中一个源成功获取的，NuGet 会将其添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="443f7-136">If the package is successfully acquired from one of the sources, NuGet adds it to the cache.</span></span> <span data-ttu-id="443f7-137">否则，安装将失败。</span><span class="sxs-lookup"><span data-stu-id="443f7-137">Otherwise, installation fails.</span></span>

1. <span data-ttu-id="443f7-138">将该包扩展到项目中。</span><span class="sxs-lookup"><span data-stu-id="443f7-138">Expand the package into the project.</span></span>
    - <span data-ttu-id="443f7-139">展开意味着将包的内容解压缩到适当的子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="443f7-139">Expanding means unzipping the package's contents into an appropriate subfolder.</span></span> <span data-ttu-id="443f7-140">子文件夹中还放置了 `.nupkg` 本身的副本。</span><span class="sxs-lookup"><span data-stu-id="443f7-140">A copy of the `.nupkg` itself is also placed in the subfolder.</span></span>
    - <span data-ttu-id="443f7-141">如果将包安装到 Visual Studio 或 .NET Core 项目中，则只展开与项目目标框架相关的文件。</span><span class="sxs-lookup"><span data-stu-id="443f7-141">If the package is being installed into a Visual Studio or .NET Core project, only the files relevant to the project's target framework are expanded.</span></span> <span data-ttu-id="443f7-142">使用 nuget.exe 命令行进行安装时，所有程序集都将展开。</span><span class="sxs-lookup"><span data-stu-id="443f7-142">When installed using the nuget.exe command line, all assemblies are expanded.</span></span>

1. <span data-ttu-id="443f7-143">如果将包安装在 Visual Studio 或 dotnet CLI 中，则将引用添加到相应的项目文件（或者对于 Visual Studio 中的某些项目类型为 `packages.config`）。</span><span class="sxs-lookup"><span data-stu-id="443f7-143">If the package is installed within Visual Studio or the dotnet CLI, a reference is added to the appropriate project file (or `packages.config` for some project types in Visual Studio).</span></span>

## <a name="related-topics"></a><span data-ttu-id="443f7-144">相关主题</span><span class="sxs-lookup"><span data-stu-id="443f7-144">Related topics</span></span>

- [<span data-ttu-id="443f7-145">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="443f7-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="443f7-146">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="443f7-146">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="443f7-147">配置 NuGet 行为</span><span class="sxs-lookup"><span data-stu-id="443f7-147">Configuring NuGet behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
- [<span data-ttu-id="443f7-148">管理 NuGet 缓存</span><span class="sxs-lookup"><span data-stu-id="443f7-148">Managing the NuGet cache</span></span>](managing-the-nuget-cache.md)
