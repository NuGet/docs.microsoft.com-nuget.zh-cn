---
title: NuGet 程序包管理器 UI 参考
description: 使用 Visual Studio 中的 NuGet 包管理器用户界面，用于使用 NuGet 包的说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 307416908aff5db12fbf6f419e20acc6e0a9b241
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818836"
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="7e6d7-103">NuGet 包管理器 UI</span><span class="sxs-lookup"><span data-stu-id="7e6d7-103">NuGet Package Manager UI</span></span>

<span data-ttu-id="7e6d7-104">在 Windows 上的 Visual Studio 中的 NuGet 包管理器 UI，可轻松地安装、 卸载和更新为项目和解决方案的 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="7e6d7-105">Visual Studio 中适用于 Mac 的体验，请参阅[中你的项目包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="7e6d7-106">程序包管理器 UI 不包括 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="7e6d7-107">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-107">In this topic:</span></span>

- [<span data-ttu-id="7e6d7-108">查找和安装包 （浏览选项卡）</span><span class="sxs-lookup"><span data-stu-id="7e6d7-108">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="7e6d7-109">卸载程序包 （已安装选项卡）</span><span class="sxs-lookup"><span data-stu-id="7e6d7-109">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="7e6d7-110">[更新包 （已安装和更新选项卡）](#updating-a-package) (包括["隐式引用的 SDK"或"AutoReferenced"消息](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="7e6d7-110">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="7e6d7-111">[管理解决方案的包](#managing-packages-for-the-solution)（使用多个项目在同一时间）。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-111">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="7e6d7-112">包源</span><span class="sxs-lookup"><span data-stu-id="7e6d7-112">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="7e6d7-113">包管理器选项控件</span><span class="sxs-lookup"><span data-stu-id="7e6d7-113">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="7e6d7-114">如果您缺少 Visual Studio 2015 中的 NuGet 包管理器，请检查**工具 > 扩展和更新...** 并搜索*NuGet 包管理器*扩展。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-114">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="7e6d7-115">如果你无法使用 Visual Studio 中的扩展安装程序，下载直接从扩展[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-115">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="7e6d7-116">在 Visual Studio 2017，NuGet 和 NuGet 包管理器将自动安装与任意。提供与.NET 相关的工作负荷。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-116">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="7e6d7-117">通过选择单独安装它**各个组件 > 代码工具 > NuGet 包管理器**在 Visual Studio 2017 安装程序中的选项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-117">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="7e6d7-118">查找和安装的包</span><span class="sxs-lookup"><span data-stu-id="7e6d7-118">Finding and installing a package</span></span>

1. <span data-ttu-id="7e6d7-119">在**解决方案资源管理器**，右键单击**引用**或某个项目并选择**管理 NuGet 包...**.</span><span class="sxs-lookup"><span data-stu-id="7e6d7-119">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![管理 NuGet 包菜单选项](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="7e6d7-121">**浏览**选项卡显示由从当前所选的源的受欢迎程度包 (请参阅[包源](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-121">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="7e6d7-122">搜索特定包在左上方使用搜索框。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-122">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="7e6d7-123">从列表以显示其信息，还可以选择包**安装**以及版本选择的下拉列表的按钮。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-123">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![管理 NuGet 包对话框浏览选项卡](media/Search.png)

1. <span data-ttu-id="7e6d7-125">从下拉列表中选择所需的版本，然后选择**安装**。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-125">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="7e6d7-126">Visual Studio 在项目中安装包和其依赖项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-126">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="7e6d7-127">你可能会要求以接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-127">You may be asked to accept license terms.</span></span> <span data-ttu-id="7e6d7-128">安装完成后，添加的包会出现在**已安装**选项卡。包也会列在**引用**的解决方案资源管理器，指示，你可以参考它们具有项目中的节点`using`语句。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-128">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![在解决方案资源管理器的引用](media/References.png)

> [!Tip]
> <span data-ttu-id="7e6d7-130">若要在搜索中，包括预发布版本并使预发布版本在版本中可用下拉列表，选中**包括预发行版**选项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-130">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="7e6d7-131">卸载包</span><span class="sxs-lookup"><span data-stu-id="7e6d7-131">Uninstalling a package</span></span>

1. <span data-ttu-id="7e6d7-132">在**解决方案资源管理器**，右键单击**引用**或所需的项目，并选择**管理 NuGet 包...**.</span><span class="sxs-lookup"><span data-stu-id="7e6d7-132">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="7e6d7-133">选择**已安装**选项卡。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-133">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="7e6d7-134">选择要卸载 （使用搜索以筛选列表，如有必要） 的包，并选择**卸载**。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-134">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![卸载包](media/UninstallPackage.png)

1. <span data-ttu-id="7e6d7-136">请注意，**包括预发行版**和**包源**卸载包时，控件将产生任何影响。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-136">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="7e6d7-137">更新程序包</span><span class="sxs-lookup"><span data-stu-id="7e6d7-137">Updating a package</span></span>

1. <span data-ttu-id="7e6d7-138">在**解决方案资源管理器**，右键单击**引用**或所需的项目，并选择**管理 NuGet 包...**.(在网站项目中，右键单击**Bin**文件夹。)</span><span class="sxs-lookup"><span data-stu-id="7e6d7-138">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="7e6d7-139">选择**更新**选项卡可查看从选定的程序包源中具有可用的更新的包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-139">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="7e6d7-140">选择**包括预发行版**将预发行程序包包括在更新列表。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-140">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="7e6d7-141">选择要更新，从在右侧的下拉列表中选择所需的版本并选择的包**更新**。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-141">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![更新程序包](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="7e6d7-143">某些包的**更新**按钮处于禁用状态，并显示一条消息，指出，它"隐式引用由 SDK"（或"AutoReferenced"）。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-143">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="7e6d7-144">消息指示包，如 Microsoft.NETCore.App 或 Microsoft.NETStandard.Library，是更大的框架或 SDK 的一部分，并且不应单独更新。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-144">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="7e6d7-145">(此类包内部标记有`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)若要更新的包，更新其所属，推断从包名称包含的 SDK 的 SDK。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-145">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs, inferring the containing SDK from the package name.</span></span> <span data-ttu-id="7e6d7-146">例如，如 Microsoft.NETCore.App 包是.NET 核心 SDK 的一部分，因此你需要将.NET 核心 SDK 安装更新。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-146">For example, a package like Microsoft.NETCore.App is part of the .NET Core SDK, therefore you need to update your  .NET Core SDK installation.</span></span>

    ![示例包标记为作为隐式引用或 AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="7e6d7-148">若要为其最新版本更新多个包，它们在中选择该列表并选择**更新**列表上方的按钮。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="7e6d7-149">你还可以更新从单个包**已安装**选项卡。在这种情况下，包的详细信息包括版本选择器 (受制于**包括预发行版**选项) 和**更新**按钮。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="7e6d7-150">管理解决方案包</span><span class="sxs-lookup"><span data-stu-id="7e6d7-150">Managing packages for the solution</span></span>

<span data-ttu-id="7e6d7-151">管理包的解决方案是同时使用多个项目的便捷方式。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="7e6d7-152">选择**工具 > NuGet 包管理器 > 管理解决方案的 NuGet 包...** 菜单命令，或右键单击该解决方案并选择**管理 NuGet 包...**:</span><span class="sxs-lookup"><span data-stu-id="7e6d7-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![管理解决方案的 NuGet 包](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="7e6d7-154">在管理解决方案的包时，UI 将允许你选择的操作会影响的项目：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![管理解决方案的包时，项目选择器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="7e6d7-156">合并选项卡</span><span class="sxs-lookup"><span data-stu-id="7e6d7-156">Consolidate tab</span></span>

<span data-ttu-id="7e6d7-157">开发人员通常考虑它在同一解决方案中的不同项目使用不同版本的相同的 NuGet 包的做法不妥。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="7e6d7-158">当你选择管理包的解决方案时，提供包管理器 UI**合并**依据你可轻松看到其中由解决方案中的不同项目使用具有不同版本号的包的选项卡：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![包管理器 UI 合并选项卡](media/ConsolidateTab.png)

<span data-ttu-id="7e6d7-160">在此示例中，ClassLibrary1 项目使用 EntityFramework 6.2.0，而 ConsoleApp1 正在使用 EntityFramework 6.1.0。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="7e6d7-161">要合并包版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="7e6d7-162">选择项目列表中要更新的项目。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="7e6d7-163">选择要在中的所有这些项目中使用的版本**版本**的控制权，例如 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="7e6d7-164">选择**安装**按钮。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-164">Select the **Install** button.</span></span>

<span data-ttu-id="7e6d7-165">程序包管理器安装到所有选定的项目，此后包不会再出现在所选的包版本**合并**选项卡。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="7e6d7-166">包源</span><span class="sxs-lookup"><span data-stu-id="7e6d7-166">Package sources</span></span>

<span data-ttu-id="7e6d7-167">若要更改 Visual Studio 将从其获取包的源，选择一个从源选择器：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![包管理器 UI 中的包源选择器](media/PackageSourceDropDown.png)

<span data-ttu-id="7e6d7-169">若要管理的包源：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-169">To manage package sources:</span></span>

1. <span data-ttu-id="7e6d7-170">选择**设置**程序包管理器用户界面中的图标如下所述，或使用**工具 > 选项**命令并滚动到**NuGet 包管理器**:</span><span class="sxs-lookup"><span data-stu-id="7e6d7-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![包管理器 UI 设置图标](media/PackageSourceSettings.png)

1. <span data-ttu-id="7e6d7-172">选择**包源**节点：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-172">Select the **Package Sources** node:</span></span>

    ![包源选项](media/options.png)

1. <span data-ttu-id="7e6d7-174">若要添加的源，选择 **+** ，编辑的名称，输入的 URL 或路径中的 **源** 控件，并选择 **更新** 。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="7e6d7-175">源现在将显示在选择器下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="7e6d7-176">若要更改包源，选择它，请在编辑**名称**和**源**框中，然后选择**更新**。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="7e6d7-177">若要禁用的包源，请清除列表中的名称左边的框。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="7e6d7-178">若要删除的包源，选择它，然后选择**X**按钮。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="7e6d7-179">使用向上和向下箭头按钮更改包源的优先顺序。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="7e6d7-180">还原项目包时，visual Studio 中的优先级顺序搜索这些源。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="7e6d7-181">有关详细信息，请参阅[程序包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-181">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="7e6d7-182">如果包源中删除它后再次出现，它可能会列出在计算机级别或用户级别`NuGet.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="7e6d7-183">请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)对于这些文件的位置，然后删除源通过手动编辑文件，或使用[nuget 源命令](../tools/nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-183">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="7e6d7-184">包管理器选项控件</span><span class="sxs-lookup"><span data-stu-id="7e6d7-184">Package manager Options control</span></span>

<span data-ttu-id="7e6d7-185">选择包后，包管理器 UI 显示一个较小，可展开**选项**下面 （此处显示了折叠和扩展） 的版本选择器控件。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="7e6d7-186">请注意，对于某些项目类型，仅**显示预览窗口**提供选项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![包管理器选项](media/PackageManagerUIOptions.png)

<span data-ttu-id="7e6d7-188">以下各节说明这些选项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="7e6d7-189">显示预览窗口</span><span class="sxs-lookup"><span data-stu-id="7e6d7-189">Show preview window</span></span>

<span data-ttu-id="7e6d7-190">选定后，一个模式窗口显示其选包的依赖关系之前安装此包：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![示例预览对话框](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="7e6d7-192">安装和更新选项</span><span class="sxs-lookup"><span data-stu-id="7e6d7-192">Install and Update Options</span></span>

<span data-ttu-id="7e6d7-193">（不可用的所有项目类型。）</span><span class="sxs-lookup"><span data-stu-id="7e6d7-193">(Not available for all project types.)</span></span>

<span data-ttu-id="7e6d7-194">**依赖项行为**配置 NuGet 如何判断哪些版本的依赖的包要进行安装：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="7e6d7-195">*忽略依赖项*会跳过安装任何依赖关系，这通常违反要安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="7e6d7-196">*最低*[默认] 使用的最小的版本号，可满足要求的主选定包安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="7e6d7-197">*最高的修补程序*安装的版本具有相同主版本号和次版本号，但最高的修补程序数。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="7e6d7-198">例如，如果指定版本 1.2.2 则开头 1.2 最高的版本将安装</span><span class="sxs-lookup"><span data-stu-id="7e6d7-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="7e6d7-199">*最高的次要*与相同的主版本号，但最高次版本号和修补程序号一起安装的版本。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="7e6d7-200">如果指定版本 1.2.2，然后从 1 开始的最高版本安装</span><span class="sxs-lookup"><span data-stu-id="7e6d7-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="7e6d7-201">*最高*安装包的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="7e6d7-202">**文件冲突操作**指定 NuGet 应如何处理项目或本地计算机中已存在的包：</span><span class="sxs-lookup"><span data-stu-id="7e6d7-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="7e6d7-203">*提示*指示 NuGet 询问是要保留还是覆盖现有包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="7e6d7-204">*忽略所有*指示 NuGet 要跳过覆盖任何现有包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="7e6d7-205">*覆盖所有*指示 NuGet 覆盖任何现有包。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="7e6d7-206">卸载选项</span><span class="sxs-lookup"><span data-stu-id="7e6d7-206">Uninstall Options</span></span>

<span data-ttu-id="7e6d7-207">（不可用的所有项目类型。）</span><span class="sxs-lookup"><span data-stu-id="7e6d7-207">(Not available for all project types.)</span></span>

<span data-ttu-id="7e6d7-208">**删除依赖关系**： 当选中时，删除任何依赖的包，如果它们不在项目中的其他位置引用。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="7e6d7-209">**强制卸载，即使在其上有依赖关系**： 当选中时，卸载程序包，即使它仍然引用项目中。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="7e6d7-210">这通常与结合使用**删除依赖关系**若要删除包和任何依赖项安装它。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="7e6d7-211">使用此选项可能，但是，会导致损坏的引用，项目中。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-211">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="7e6d7-212">在这种情况下，你可能需要[重新安装这些其他包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="7e6d7-212">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
