---
title: "安装 NuGet 客户端工具 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "安装客户端工具、命令行界面 (CLI) 和适用于 Visual Studio 包管理器的指南。"
keywords: "nuget.exe CLI, NuGet 客户端工具, NuGet 包管理器, NuGet 包管理器控制台, 适用于 Visual Studio 的 NuGet, NuGet beta 通道"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="75bbb-104">安装 NuGet 客户端工具</span><span class="sxs-lookup"><span data-stu-id="75bbb-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="75bbb-105">**打算安装包？请参阅[快速入门 - 使用包](../Quickstart/Use-a-Package.md)。**</span><span class="sxs-lookup"><span data-stu-id="75bbb-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="75bbb-106">有两个主要工具可用于帮助生成、发布和使用 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="75bbb-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="75bbb-107">[NuGet CLI](#nuget-cli) 是适用于 Windows 的命令行实用工具，可提供所有 NuGet 功能；它也可以使用 Mono 或通过 .NET Core CLI (`dotnet`) 在 Mac OSX 和 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="75bbb-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="75bbb-108">[Visual Studio 中的 NuGet 包管理器](#nuget-package-manager-in-visual-studio)（仅限于 Windows）是用于管理包的 GUI 工具，它包括 PowerShell 控制台，通过该控制台可直接在 Visual Studio 中使用某些 NuGet 命令。</span><span class="sxs-lookup"><span data-stu-id="75bbb-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="75bbb-109">包管理器 UI 和控制台均包括在 Visual Studio（Windows 上）2012 及更高版本中，并且可为早期版本手动安装。</span><span class="sxs-lookup"><span data-stu-id="75bbb-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="75bbb-110">对于 Visual Studio for Mac，NuGet 功能是直接内置的。</span><span class="sxs-lookup"><span data-stu-id="75bbb-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="75bbb-111">请参阅[在项目中添加 NuGet 包](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)，获取有关演练。</span><span class="sxs-lookup"><span data-stu-id="75bbb-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="75bbb-112">Visual Studio Code 目前没有任何内置 NuGet 支持。</span><span class="sxs-lookup"><span data-stu-id="75bbb-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="75bbb-113">请使用 NuGet CLI 或 [dotnet CLI](../Tools/dotnet-Commands.md)。</span><span class="sxs-lookup"><span data-stu-id="75bbb-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="75bbb-114">NuGet CLI 和包管理器均支持以下操作：</span><span class="sxs-lookup"><span data-stu-id="75bbb-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="75bbb-115">搜索包</span><span class="sxs-lookup"><span data-stu-id="75bbb-115">Search packages</span></span>
- <span data-ttu-id="75bbb-116">安装包</span><span class="sxs-lookup"><span data-stu-id="75bbb-116">Install packages</span></span>
- <span data-ttu-id="75bbb-117">更新包</span><span class="sxs-lookup"><span data-stu-id="75bbb-117">Update packages</span></span>
- <span data-ttu-id="75bbb-118">卸载包</span><span class="sxs-lookup"><span data-stu-id="75bbb-118">Uninstall packages</span></span>
- <span data-ttu-id="75bbb-119">还原包（仅限于包管理器中的 UI）</span><span class="sxs-lookup"><span data-stu-id="75bbb-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="75bbb-120">管理 NuGet 源</span><span class="sxs-lookup"><span data-stu-id="75bbb-120">Manage NuGet sources</span></span>

<span data-ttu-id="75bbb-121">以下功能仅受 NuGet CLI 支持：</span><span class="sxs-lookup"><span data-stu-id="75bbb-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="75bbb-122">管理包（nuget.org 或专用源）</span><span class="sxs-lookup"><span data-stu-id="75bbb-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="75bbb-123">创建包</span><span class="sxs-lookup"><span data-stu-id="75bbb-123">Create packages</span></span> 
- <span data-ttu-id="75bbb-124">发布包</span><span class="sxs-lookup"><span data-stu-id="75bbb-124">Publish packages</span></span>
- <span data-ttu-id="75bbb-125">管理 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="75bbb-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="75bbb-126">管理 NuGet 缓存</span><span class="sxs-lookup"><span data-stu-id="75bbb-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="75bbb-127">复制包</span><span class="sxs-lookup"><span data-stu-id="75bbb-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="75bbb-128">另一个很好的工具是 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，它是可直观浏览、创建和编辑 NuGet 包的独立开源工具。</span><span class="sxs-lookup"><span data-stu-id="75bbb-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="75bbb-129">它非常有用，例如，无需每次重新生成包即可对包结构进行实验性更改。</span><span class="sxs-lookup"><span data-stu-id="75bbb-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="75bbb-130">用于开发 .NET Core 应用程序的跨平台 [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) 工具链支持多个 NuGet 命令，如删除、局部变量、推送、打包和还原。</span><span class="sxs-lookup"><span data-stu-id="75bbb-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="75bbb-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="75bbb-131">NuGet CLI</span></span>

<span data-ttu-id="75bbb-132">NuGet 命令行接口提供对所有 NuGet 功能的访问权限，并且可在 Windows、Mac OSX 和 Linux 上运行，如以下各节所述。</span><span class="sxs-lookup"><span data-stu-id="75bbb-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="75bbb-133">Windows</span><span class="sxs-lookup"><span data-stu-id="75bbb-133">Windows</span></span>

<span data-ttu-id="75bbb-134">**直接下载：**</span><span class="sxs-lookup"><span data-stu-id="75bbb-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="75bbb-135">对于 NuGet 1.4+，可以使用 `nuget update -self` 将现有 nuget.exe 更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="75bbb-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="75bbb-136">**其他方法：**</span><span class="sxs-lookup"><span data-stu-id="75bbb-136">**Other methods:**</span></span>

- <span data-ttu-id="75bbb-137">**Chocolatey**：使用 [Chocolatey](http://chocolatey.org) 客户端安装 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 包。</span><span class="sxs-lookup"><span data-stu-id="75bbb-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="75bbb-138">**Visual Studio**：从 Visual Studio 中的包管理器控制台安装 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 包。</span><span class="sxs-lookup"><span data-stu-id="75bbb-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="75bbb-139">**针对 NuGet 2.x 用户**：由于 NuGet 3.2 中引入了重大更改，因此 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) 指向最新稳定 NuGet 2.x 版本，防止持续集成系统可能出现的中断。</span><span class="sxs-lookup"><span data-stu-id="75bbb-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="75bbb-140">Mac OSX 和 Linux</span><span class="sxs-lookup"><span data-stu-id="75bbb-140">Mac OSX and Linux</span></span>

<span data-ttu-id="75bbb-141">在 Mac OSX 和 Linux 上，有两种方法可运行 NuGet CLI：</span><span class="sxs-lookup"><span data-stu-id="75bbb-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="75bbb-142">安装包括核心 NuGet 功能的 [.NET Core SDK](https://www.microsoft.com/net/download/core)。</span><span class="sxs-lookup"><span data-stu-id="75bbb-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="75bbb-143">下载还会在 [github.com/dotnet/cli](https://github.com/dotnet/cli) 上列出。</span><span class="sxs-lookup"><span data-stu-id="75bbb-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="75bbb-144">如果需要更完整的功能，则通过下面第二个选项，将 `nuget.exe` 与 Mono 结合使用。</span><span class="sxs-lookup"><span data-stu-id="75bbb-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="75bbb-145">安装 [Mono](http://www.mono-project.com/docs/getting-started/install/)，然后从 [nuget.org/downloads](https://nuget.org/downloads) 使用适用于 Windows（版本 3.2 及更高版本）的 `nuget.exe` 命令行可执行文件。</span><span class="sxs-lookup"><span data-stu-id="75bbb-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="75bbb-146">在 Mono 上运行 NuGet 受到以下限制：</span><span class="sxs-lookup"><span data-stu-id="75bbb-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="75bbb-147">经测试可运行的命令：</span><span class="sxs-lookup"><span data-stu-id="75bbb-147">Commands tested to work:</span></span>
        - <span data-ttu-id="75bbb-148">config</span><span class="sxs-lookup"><span data-stu-id="75bbb-148">config</span></span>
        - <span data-ttu-id="75bbb-149">删除</span><span class="sxs-lookup"><span data-stu-id="75bbb-149">delete</span></span>
        - <span data-ttu-id="75bbb-150">帮助</span><span class="sxs-lookup"><span data-stu-id="75bbb-150">help</span></span>
        - <span data-ttu-id="75bbb-151">install</span><span class="sxs-lookup"><span data-stu-id="75bbb-151">install</span></span>
        - <span data-ttu-id="75bbb-152">list</span><span class="sxs-lookup"><span data-stu-id="75bbb-152">list</span></span>
        - <span data-ttu-id="75bbb-153">push</span><span class="sxs-lookup"><span data-stu-id="75bbb-153">push</span></span>
        - <span data-ttu-id="75bbb-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="75bbb-154">setApiKey</span></span>
        - <span data-ttu-id="75bbb-155">sources</span><span class="sxs-lookup"><span data-stu-id="75bbb-155">sources</span></span>
        - <span data-ttu-id="75bbb-156">spec</span><span class="sxs-lookup"><span data-stu-id="75bbb-156">spec</span></span>

    - <span data-ttu-id="75bbb-157">部分运行的命令：</span><span class="sxs-lookup"><span data-stu-id="75bbb-157">Partially-working commands:</span></span>
        - <span data-ttu-id="75bbb-158">pack：适用于 `.nuspec` 文件，但不适用于项目文件。</span><span class="sxs-lookup"><span data-stu-id="75bbb-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="75bbb-159">restore：适用于 `packages.config` 和 `project.json` 文件，但不适用于解决方案 (`.sln`) 文件。</span><span class="sxs-lookup"><span data-stu-id="75bbb-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="75bbb-160">不起作用的命令：</span><span class="sxs-lookup"><span data-stu-id="75bbb-160">Commands that do not work:</span></span>
        - <span data-ttu-id="75bbb-161">更新</span><span class="sxs-lookup"><span data-stu-id="75bbb-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="75bbb-162">相关主题</span><span class="sxs-lookup"><span data-stu-id="75bbb-162">Related topics</span></span>

- [<span data-ttu-id="75bbb-163">NuGet CLI 引用</span><span class="sxs-lookup"><span data-stu-id="75bbb-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="75bbb-164">创建包</span><span class="sxs-lookup"><span data-stu-id="75bbb-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="75bbb-165">发布包</span><span class="sxs-lookup"><span data-stu-id="75bbb-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="75bbb-166">Visual Studio 中的 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="75bbb-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="75bbb-167">Windows（2012 及更高版本）上每个版本的 Visual Studio 中都包括 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="75bbb-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="75bbb-168">它包括包管理器 UI（[引用](../tools/package-manager-ui.md)，以及包管理器控制台，可通过其访问某些包附带的工具（[引用](../tools/package-manager-console.md)）。</span><span class="sxs-lookup"><span data-stu-id="75bbb-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="75bbb-169">Visual Studio 2017 安装程序包括具有任何采用 .NET 的工作负荷的 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="75bbb-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="75bbb-170">若要单独安装，或验证是否已安装包管理器，运行 Visual Studio 2017 安装程序，并检查“各个组件”>“代码工具”>“NuGet 包管理器”下的选项。</span><span class="sxs-lookup"><span data-stu-id="75bbb-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="75bbb-171">控制台需要 [PowerShell 2.0](http://support.microsoft.com/kb/968929)，Windows 7 或更高版本及 Windows Server 2008 R2 或更高版本中已安装 PowerShell 2.0。</span><span class="sxs-lookup"><span data-stu-id="75bbb-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="75bbb-172">包管理器控制台命令也仅可在 Windows 上的 Visual Studio 中运行。</span><span class="sxs-lookup"><span data-stu-id="75bbb-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="75bbb-173">在该环境外使用 NuGet CLI，包括使用 Visual Studio for Mac 和 Visual Studio Code 的情况。</span><span class="sxs-lookup"><span data-stu-id="75bbb-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="75bbb-174">适用于 Visual Studio 2010 及更早版本的包管理器安装</span><span class="sxs-lookup"><span data-stu-id="75bbb-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="75bbb-175">Visual Studio 2012 及更高版本不需要这些步骤，它们已包括包管理器。</span><span class="sxs-lookup"><span data-stu-id="75bbb-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="75bbb-176">在 Visual Studio 2010 及更早版本中，单击“工具”>“扩展和更新”。</span><span class="sxs-lookup"><span data-stu-id="75bbb-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="75bbb-177">导航到“联机”，然后搜索“适用于 Visual Studio 的 NuGet 包管理器”，然后单击“下载”。</span><span class="sxs-lookup"><span data-stu-id="75bbb-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="75bbb-178">在“安装程序”对话框中，单击“安装”。</span><span class="sxs-lookup"><span data-stu-id="75bbb-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="75bbb-179">安装完成后，重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="75bbb-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="75bbb-180">如果无法使用 Visual Studio 中的“扩展和更新”对话框（例如，已被代理阻止），则可以直接在 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载适用于 Visual Studio 2013 和 2015 的扩展。</span><span class="sxs-lookup"><span data-stu-id="75bbb-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="75bbb-181">更新包管理器</span><span class="sxs-lookup"><span data-stu-id="75bbb-181">Updating the Package Manager</span></span>

<span data-ttu-id="75bbb-182">对于 Visual Studio 2015 Update 2 及更高版本，包管理器自动更新为最新稳定版本。</span><span class="sxs-lookup"><span data-stu-id="75bbb-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="75bbb-183">对于 Visual Studio 2015 Update 1 及更早版本，请选择“工具 > 扩展和更新”命令，然后单击“更新”选项卡，查看是否有可用的包管理器新版本。</span><span class="sxs-lookup"><span data-stu-id="75bbb-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="75bbb-184">NuGet 预览版</span><span class="sxs-lookup"><span data-stu-id="75bbb-184">NuGet previews</span></span>

<span data-ttu-id="75bbb-185">如果希望预览即将推出的 NuGet 功能，请安装 [Visual Studio 2017 预览版](https://www.visualstudio.com/vs/preview/)，该版本与 Visual Studio 稳定版本并行工作。</span><span class="sxs-lookup"><span data-stu-id="75bbb-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="75bbb-186">请注意，不再使用以前的适用于 Visual Studio 2015 的 NuGet Beta 通道 (`https://dotnet.myget.org/F/nuget-beta/vsix/`)。</span><span class="sxs-lookup"><span data-stu-id="75bbb-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="75bbb-187">若要报告任何版本的 NuGet 的问题或分享观点，请在 [NuGet GitHub 存储库](https://github.com/Nuget/Home)上打开问题。</span><span class="sxs-lookup"><span data-stu-id="75bbb-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="75bbb-188">相关主题</span><span class="sxs-lookup"><span data-stu-id="75bbb-188">Related topics</span></span>

- [<span data-ttu-id="75bbb-189">包管理器 UI 引用</span><span class="sxs-lookup"><span data-stu-id="75bbb-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="75bbb-190">包管理器控制台引用</span><span class="sxs-lookup"><span data-stu-id="75bbb-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="75bbb-191">包管理器控制台 PowerShell 引用</span><span class="sxs-lookup"><span data-stu-id="75bbb-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)