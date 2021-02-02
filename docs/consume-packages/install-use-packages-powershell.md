---
title: 在 Visual Studio 中使用控制台安装和管理 NuGet 包
description: 有关在 Visual Studio 中使用 NuGet 包管理器控制台以处理包的说明。
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 119bf32426e5cbc179c3713e60688c691e133c5d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774903"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="e41cf-103">在 Visual Studio 中使用包管理器控制台安装和管理包 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e41cf-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="e41cf-104">借助 NuGet 包管理器控制台，可以使用 [NuGet PowerShell 命令](../reference/powershell-reference.md)查找、安装、卸载和更新 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e41cf-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="e41cf-105">如果包管理器 UI 未提供执行操作的方法，则必须使用控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="e41cf-106">若要在控制台中使用 `nuget.exe` CLI 命令，请参阅[在控制台中使用 nuget.exe CLI](#use-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="e41cf-107">Windows 版 Visual Studio 中内置了该控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="e41cf-108">Visual Studio for Mac 或 Visual Studio Code 中未提供该控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="e41cf-109">此处列出的命令特定于 Visual Studio 中的包管理器控制台，它不同于常规 PowerShell 环境中提供的[包管理模块命令](/powershell/module/packagemanagement/)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="e41cf-110">具体而言，每个环境都有一些命令，这些命令在其他环境中不可用，而具有相同名称的命令在其特定参数中也可能不同。</span><span class="sxs-lookup"><span data-stu-id="e41cf-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="e41cf-111">使用 Visual Studio 中的包管理控制台时，本主题中所述的命令和参数适用。</span><span class="sxs-lookup"><span data-stu-id="e41cf-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="e41cf-112">查找和安装包</span><span class="sxs-lookup"><span data-stu-id="e41cf-112">Find and install a package</span></span>

<span data-ttu-id="e41cf-113">例如，通过三个简单的步骤查找和安装包：</span><span class="sxs-lookup"><span data-stu-id="e41cf-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="e41cf-114">在 Visual Studio 中打开项目/解决方案，然后使用“工具”>“NuGet 包管理器”>“包管理器控制台”命令打开控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="e41cf-115">找到要安装的包。</span><span class="sxs-lookup"><span data-stu-id="e41cf-115">Find the package you want to install.</span></span> <span data-ttu-id="e41cf-116">如果你已经知道此操作步骤，请跳至步骤 3。</span><span class="sxs-lookup"><span data-stu-id="e41cf-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="e41cf-117">运行安装命令：</span><span class="sxs-lookup"><span data-stu-id="e41cf-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="e41cf-118">控制台中可用的全部操作也可以通过 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 完成。</span><span class="sxs-lookup"><span data-stu-id="e41cf-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e41cf-119">但是，控制台命令在 Visual Studio 和已保存的项目/解决方案的上下文中运行，并且通常比其等效的 CLI 命令完成更多操作。</span><span class="sxs-lookup"><span data-stu-id="e41cf-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="e41cf-120">例如，通过控制台安装包会添加对项目的引用，而 CLI 命令则不会执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e41cf-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="e41cf-121">因此，在 Visual Studio 中工作的开发人员通常更愿意使用控制台而不是 CLI。</span><span class="sxs-lookup"><span data-stu-id="e41cf-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="e41cf-122">许多控制台操作依赖于在 Visual Studio 中通过已知路径名打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="e41cf-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="e41cf-123">如果你有未保存的解决方案或没有解决方案，可以看到错误：“解决方案未打开或未保存。</span><span class="sxs-lookup"><span data-stu-id="e41cf-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="e41cf-124">请确保你有一个已打开且已保存的解决方案。”</span><span class="sxs-lookup"><span data-stu-id="e41cf-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="e41cf-125">这表示控制台无法确定解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="e41cf-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="e41cf-126">保存未保存的解决方案，或者如果没有打开解决方案，则创建并保存解决方案，这些操作应该可以纠正错误。</span><span class="sxs-lookup"><span data-stu-id="e41cf-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="e41cf-127">打开控制台和控制台控件</span><span class="sxs-lookup"><span data-stu-id="e41cf-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="e41cf-128">在 Visual Studio 中使用“工具”>“NuGet 包管理器”>“包管理器控制台”命令打开控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="e41cf-129">控制台是一个 Visual Studio 窗口，可以根据需要进行排列和放置（请参阅[在 Visual Studio 中自定义窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio)）。</span><span class="sxs-lookup"><span data-stu-id="e41cf-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="e41cf-130">默认情况下，控制台命令针对窗口顶部控件中设置的特定包源和项目执行操作：</span><span class="sxs-lookup"><span data-stu-id="e41cf-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![包源和项目的“包管理器控制台”控件](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="e41cf-132">选择不同的包源和/或项目会更改后续命令的默认值。</span><span class="sxs-lookup"><span data-stu-id="e41cf-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="e41cf-133">要在不更改默认值的情况下覆盖这些设置，大多数命令都支持 `-Source` 和 `-ProjectName` 选项。</span><span class="sxs-lookup"><span data-stu-id="e41cf-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="e41cf-134">若要管理包源，请选择齿轮图标。</span><span class="sxs-lookup"><span data-stu-id="e41cf-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="e41cf-135">这是“工具”>“选项”>“NuGet 包管理器”>“包源”对话框的快捷方式，如[包管理器 UI](install-use-packages-visual-studio.md#package-sources) 页中所述。</span><span class="sxs-lookup"><span data-stu-id="e41cf-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="e41cf-136">此外，项目选择器右侧的控件可清除控制台的内容：</span><span class="sxs-lookup"><span data-stu-id="e41cf-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![包管理器控制台设置和清除控件](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="e41cf-138">最右边的按钮会中断长时间运行的命令。</span><span class="sxs-lookup"><span data-stu-id="e41cf-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="e41cf-139">例如，运行 `Get-Package -ListAvailable -PageSize 500` 会列出默认源（例如 nuget.org）上的前 500 个包，这可能需要几分钟才能运行完毕。</span><span class="sxs-lookup"><span data-stu-id="e41cf-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![包管理器控制台停止控件](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="e41cf-141">安装包</span><span class="sxs-lookup"><span data-stu-id="e41cf-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="e41cf-142">请参阅 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="e41cf-143">在控制台中安装包执行的步骤与[安装包时会发生什么情况](../concepts/package-installation-process.md)相同，只不过它添加了以下内容：</span><span class="sxs-lookup"><span data-stu-id="e41cf-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="e41cf-144">控制台在其窗口中显示适用的许可条款，并附带隐含协议。</span><span class="sxs-lookup"><span data-stu-id="e41cf-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="e41cf-145">如果你不同意这些条款，应立即卸载包。</span><span class="sxs-lookup"><span data-stu-id="e41cf-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="e41cf-146">此外，对包的引用也会添加到项目文件中，并显示在“引用”节点下的“解决方案资源管理器”中，需要保存项目才能直接查看项目文件中的更改。</span><span class="sxs-lookup"><span data-stu-id="e41cf-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="e41cf-147">卸载包</span><span class="sxs-lookup"><span data-stu-id="e41cf-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="e41cf-148">请参阅 [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="e41cf-149">如果需要查找标识符，请使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 查看当前安装在默认项目中的所有包。</span><span class="sxs-lookup"><span data-stu-id="e41cf-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="e41cf-150">卸载包将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e41cf-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="e41cf-151">从项目中删除对包的引用（以及正在使用的任何管理格式）。</span><span class="sxs-lookup"><span data-stu-id="e41cf-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="e41cf-152">引用不再出现在“解决方案资源管理器”中。</span><span class="sxs-lookup"><span data-stu-id="e41cf-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="e41cf-153">（可能需要重建项目才能看到它已从 Bin 文件夹中删除。）</span><span class="sxs-lookup"><span data-stu-id="e41cf-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="e41cf-154">安装包后，撤销对 `app.config` 或 `web.config` 的任何更改。</span><span class="sxs-lookup"><span data-stu-id="e41cf-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="e41cf-155">如果没有其余包使用这些依赖项，则删除以前安装的依赖项。</span><span class="sxs-lookup"><span data-stu-id="e41cf-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="e41cf-156">更新包</span><span class="sxs-lookup"><span data-stu-id="e41cf-156">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="e41cf-157">请参阅 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 和 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="e41cf-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="e41cf-158">查找包</span><span class="sxs-lookup"><span data-stu-id="e41cf-158">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="e41cf-159">请参阅 [Find-Package](../reference/ps-reference/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="e41cf-160">在 Visual Studio 2013 及更早版本中，请改用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="e41cf-161">控制台的可用性</span><span class="sxs-lookup"><span data-stu-id="e41cf-161">Availability of the console</span></span>

<span data-ttu-id="e41cf-162">从 Visual Studio 2017 开始，当你选择任何与 .NET 相关的工作负载时，会自动安装 NuGet 和 NuGet 包管理器；不过，也可以通过在 Visual Studio 安装程序中选中“单个组件”>“代码工具”>“NuGet 包管理器”选项来单独安装它。</span><span class="sxs-lookup"><span data-stu-id="e41cf-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="e41cf-163">另外，如果你在 Visual Studio 2015 及更早版本中缺少 NuGet 包管理器，请选中“工具”>“扩展和更新...”并搜索“NuGet 包管理器”扩展。</span><span class="sxs-lookup"><span data-stu-id="e41cf-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="e41cf-164">如果无法在 Visual Studio 中使用扩展安装程序，可以直接从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载扩展。</span><span class="sxs-lookup"><span data-stu-id="e41cf-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="e41cf-165">Visual Studio for Mac 目前不提供包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="e41cf-166">但是，可以通过 [NuGet CLI](../reference/nuget-exe-CLI-reference.md) 获取等效命令。</span><span class="sxs-lookup"><span data-stu-id="e41cf-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="e41cf-167">Visual Studio for Mac 确实有一个用于管理 NuGet 包的 UI。</span><span class="sxs-lookup"><span data-stu-id="e41cf-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="e41cf-168">请参阅[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="e41cf-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="e41cf-169">Visual Studio Code 中不包含包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="e41cf-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="e41cf-170">扩展包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="e41cf-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="e41cf-171">某些包为控制台安装新命令。</span><span class="sxs-lookup"><span data-stu-id="e41cf-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="e41cf-172">例如，`MvcScaffolding` 创建如下所示的 `Scaffold` 命令，用于生成 ASP.NET MVC 控制器和视图：</span><span class="sxs-lookup"><span data-stu-id="e41cf-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安装和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="e41cf-174">设置 NuGet PowerShell 配置文件</span><span class="sxs-lookup"><span data-stu-id="e41cf-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="e41cf-175">通过 PowerShell 配置文件，可以在每次使用 PowerShell 时使用常用命令。</span><span class="sxs-lookup"><span data-stu-id="e41cf-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="e41cf-176">NuGet 支持通常位于以下位置的 NuGet 特定配置文件：</span><span class="sxs-lookup"><span data-stu-id="e41cf-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

<span data-ttu-id="e41cf-177">%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1</span><span class="sxs-lookup"><span data-stu-id="e41cf-177">*%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1*</span></span>

<span data-ttu-id="e41cf-178">要查找配置文件，请在控制台中键入 `$profile`：</span><span class="sxs-lookup"><span data-stu-id="e41cf-178">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="e41cf-179">有关更多详细信息，请参阅 [Windows PowerShell 配置文件](/previous-versions//bb613488(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="e41cf-179">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="e41cf-180">在控制台中使用 nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="e41cf-180">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="e41cf-181">若要在包管理器控制台中使用 [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md)，请从控制台安装 [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) 包：</span><span class="sxs-lookup"><span data-stu-id="e41cf-181">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
