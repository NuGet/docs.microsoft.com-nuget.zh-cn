---
title: NuGet 程序包管理器控制台指南 |Microsoft 文档
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
f1_keywords:
- vs.nuget.packagemanager.console
description: 使用 Visual Studio 中的 NuGet 程序包管理器控制台，用于处理包的说明。
keywords: NuGet 包管理器控制台，NuGet powershell，管理 NuGet 包
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: af22a524f6b4a41a4c24077fe396846da6fb1ff8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="ebe9d-104">程序包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="ebe9d-104">Package Manager Console</span></span>

<span data-ttu-id="ebe9d-105">NuGet Package Manager Console 内置于 Visual Studio 在 Windows 2012 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="ebe9d-106">（不包含在 Visual Studio 用于 Mac 或 Visual Studio Code。）</span><span class="sxs-lookup"><span data-stu-id="ebe9d-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="ebe9d-107">控制台，你可以使用[NuGet PowerShell 命令](../tools/powershell-reference.md)若要查找，安装、 卸载和更新 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="ebe9d-108">使用控制台是在包管理器 UI 不提供了如何执行操作的情况下必需的。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="ebe9d-109">若要使用`nuget.exe`命令在控制台中，请参阅[使用控制台中的 CLI nuget.exe](#using-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="ebe9d-110">例如，查找和安装的包，可使用三个简单步骤：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="ebe9d-111">在 Visual Studio 中，打开项目/解决方案并打开控制台使用**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="ebe9d-112">查找你想要安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-112">Find the package you want to install.</span></span> <span data-ttu-id="ebe9d-113">如果你已经知道此，请跳到步骤 3。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="ebe9d-114">运行安装命令：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="ebe9d-115">在控制台中可用的所有操作也都可以与[NuGet CLI](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="ebe9d-116">但是，控制台命令在 Visual Studio 和已保存的项目/解决方案的上下文中运行，并且通常完成多个其等效的 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="ebe9d-117">例如，安装通过控制台的包将引用添加到项目而 CLI 命令不运行。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="ebe9d-118">为此，通常在 Visual Studio 中工作的开发人员喜欢使用 CLI 到控制台。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="ebe9d-119">许多控制台操作取决于使用已知的路径名称在 Visual Studio 中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="ebe9d-120">如果你有未保存的解决方案或没有解决方案，您可以看到此错误，"是未打开或保存解决方案。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="ebe9d-121">请确保你已打开并保存解决方案。"</span><span class="sxs-lookup"><span data-stu-id="ebe9d-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="ebe9d-122">这表示控制台无法确定解决方案的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="ebe9d-123">保存未保存的解决方案，或创建和保存解决方案，如果你还没有打开，应纠正该错误。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="ebe9d-124">打开的控制台和控制台控件</span><span class="sxs-lookup"><span data-stu-id="ebe9d-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="ebe9d-125">打开 Visual Studio 中使用控制台**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="ebe9d-126">在控制台中，可以排列和定位你的喜好的 Visual Studio 窗口 (请参阅[自定义 Visual Studio 中的窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="ebe9d-127">默认情况下，控制台命令运行针对特定的包源和项目中控件的窗口的顶部设置：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![对包源和项目程序包管理器控制台控制](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="ebe9d-129">选择一个不同的包源和/或项目更改这些默认设置的后续命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="ebe9d-130">覆盖而无需更改默认设置，这些设置的大多数命令支持`-Source`和`-ProjectName`选项。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="ebe9d-131">若要管理的包源，选择齿轮图标。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="ebe9d-132">这是一个指向快捷方式**工具 > 选项 > NuGet 包管理器 > 程序包源**对话框上所述[包管理器 UI](package-manager-ui.md#package-sources)页。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="ebe9d-133">此外，右侧为项目选择器控件清除控制台的内容：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![程序包管理器控制台设置和清除控件](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="ebe9d-135">最右边的按钮中断长时间运行的命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="ebe9d-136">例如，运行`Get-Package -ListAvailable -PageSize 500`列出上默认源 （如 nuget.org)，可能需要几分钟时间运行的前 500 包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![程序包管理器控制台停止控件](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="ebe9d-138">安装的包</span><span class="sxs-lookup"><span data-stu-id="ebe9d-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="ebe9d-139">请参阅[安装包](../tools/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="ebe9d-140">在控制台中安装的包执行相同的步骤，如所述[安装包时，会发生什么情况](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)，添加了以下内容：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="ebe9d-141">控制台显示在其窗口并默示协议适用的许可条款。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="ebe9d-142">如果你不同意这些条款，你应立即卸载程序包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="ebe9d-143">此外对包的引用添加到项目文件，并出现在**解决方案资源管理器**下**引用**节点，您必须先保存该项目才能直接看到项目文件中的更改。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="ebe9d-144">卸载包</span><span class="sxs-lookup"><span data-stu-id="ebe9d-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="ebe9d-145">请参阅[卸载包](../tools/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="ebe9d-146">使用[Get 包](../tools/ps-ref-get-package.md)查看当前安装在默认项目中，如果你需要查找标识符的所有包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="ebe9d-147">卸载程序包执行下列操作：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="ebe9d-148">将对包从项目 （和正在使用的任何管理格式） 的引用。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="ebe9d-149">引用不再显示在**解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="ebe9d-150">(你可能需要重新生成该项目才能看到它从删除**Bin**文件夹。)</span><span class="sxs-lookup"><span data-stu-id="ebe9d-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="ebe9d-151">反转对所做任何更改`app.config`或`web.config`时已安装了包。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="ebe9d-152">如果没有剩余的包使用这些依赖关系，依赖以前安装中删除项。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="ebe9d-153">更新程序包</span><span class="sxs-lookup"><span data-stu-id="ebe9d-153">Updating a package</span></span>

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

<span data-ttu-id="ebe9d-154">请参阅[Get 包](../tools/ps-ref-get-package.md)和[更新包](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="ebe9d-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="ebe9d-155">查找包</span><span class="sxs-lookup"><span data-stu-id="ebe9d-155">Finding a package</span></span>

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

<span data-ttu-id="ebe9d-156">请参阅[查找包](../tools/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="ebe9d-157">在 Visual Studio 2013 和更早版本，使用[Get 包](../tools/ps-ref-get-package.md)相反。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="ebe9d-158">控制台可用性</span><span class="sxs-lookup"><span data-stu-id="ebe9d-158">Availability of the console</span></span>

<span data-ttu-id="ebe9d-159">在 Visual Studio 2017，NuGet 和 NuGet 包管理器将自动安装时选择任何。提供与.NET 相关的工作负荷;你就可以还单独安装它，通过检查**各个组件 > 代码工具 > NuGet 包管理器**在 Visual Studio 2017 安装程序中的选项。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-159">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="ebe9d-160">此外，如果你缺少 NuGet 包管理器在 Visual Studio 2015 及更早版本，请检查**工具 > 扩展和更新...**和搜索 NuGet 包管理器扩展。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="ebe9d-161">如果你无法使用 Visual Studio 中的扩展安装程序，你可以下载直接从扩展[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="ebe9d-162">程序包管理器控制台不是当前适用于 Visual Studio for mac。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="ebe9d-163">等效命令，但是，这些功能通过[NuGet CLI](nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="ebe9d-164">适用于 Mac 的 visual Studio 也用于管理 NuGet 包存在一些 UI。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="ebe9d-165">请参阅[中你的项目包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="ebe9d-166">程序包管理器控制台不包括 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="ebe9d-167">扩展包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="ebe9d-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="ebe9d-168">某些包安装新的控制台的命令。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="ebe9d-169">例如，`MvcScaffolding`创建等命令`Scaffold`下面所示，这将生成 ASP.NET MVC 控制器和视图：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安装和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="ebe9d-171">设置 NuGet PowerShell 配置文件</span><span class="sxs-lookup"><span data-stu-id="ebe9d-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="ebe9d-172">PowerShell 配置文件，可以提供常用的命令，只要你使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="ebe9d-173">NuGet 支持通常在以下位置找到 NuGet 特定配置文件：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="ebe9d-174">若要查找配置文件，请键入`$profile`在控制台中：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="ebe9d-175">有关更多详细信息，请参阅[Windows PowerShell 配置文件](https://technet.microsoft.com/library/bb613488.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ebe9d-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="ebe9d-176">使用 nuget.exe CLI 在控制台中</span><span class="sxs-lookup"><span data-stu-id="ebe9d-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="ebe9d-177">若要使[ `nuget.exe` CLI](nuget-exe-cli-reference.md)可用在程序包管理器控制台中，安装[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)从控制台的包：</span><span class="sxs-lookup"><span data-stu-id="ebe9d-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
