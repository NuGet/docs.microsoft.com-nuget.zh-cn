---
title: 在 Visual Studio 中安装和管理 NuGet 包
description: 有关在 Visual Studio 中使用 NuGet 包管理器 UI 以处理 NuGet 包的说明。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428419"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="f27f6-103">使用 NuGet 包管理器在 Visual Studio 中安装和管理包</span><span class="sxs-lookup"><span data-stu-id="f27f6-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="f27f6-104">通过 Windows 版 Visual Studio 中的 NuGet 包管理器 UI，可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f27f6-105">若要了解 Visual Studio for Mac 的使用体验，请参阅[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="f27f6-106">Visual Studio Code 中不包含包管理器 UI。</span><span class="sxs-lookup"><span data-stu-id="f27f6-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="f27f6-107">如果 Visual Studio 2015 中缺少 NuGet 包管理器，请选中“工具”>“扩展和更新...”  并搜索“NuGet 包管理器”  扩展。</span><span class="sxs-lookup"><span data-stu-id="f27f6-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="f27f6-108">如果无法在 Visual Studio 中使用扩展安装程序，请直接从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载扩展。</span><span class="sxs-lookup"><span data-stu-id="f27f6-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="f27f6-109">从 Visual Studio 2017 开始，NuGet 和 NuGet 包管理器会与任何 .NET 相关的工作负载一起自动安装。</span><span class="sxs-lookup"><span data-stu-id="f27f6-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="f27f6-110">通过在 Visual Studio 安装程序中选择“单个组件”>“代码工具”>“NuGet 包管理器”  选项，可以单独安装它。</span><span class="sxs-lookup"><span data-stu-id="f27f6-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="f27f6-111">查找和安装包</span><span class="sxs-lookup"><span data-stu-id="f27f6-111">Find and install a package</span></span>

1. <span data-ttu-id="f27f6-112">在“解决方案资源管理器”中，右键单击“引用”或某个项目，然后选择“管理 NuGet 包...”    。</span><span class="sxs-lookup"><span data-stu-id="f27f6-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![“管理 NuGet 包”菜单选项](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="f27f6-114">“浏览”  选项卡按当前所选来源的受欢迎程度显示包（请参阅[包源](#package-sources)）。</span><span class="sxs-lookup"><span data-stu-id="f27f6-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="f27f6-115">使用左上角的搜索框搜索特定包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="f27f6-116">从列表中选择一个包以显示其信息，此操作还会启用“安装”  按钮以及版本选择下拉列表。</span><span class="sxs-lookup"><span data-stu-id="f27f6-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![“管理 NuGet 包”对话框“浏览”选项卡](media/Search.png)

1. <span data-ttu-id="f27f6-118">从下拉列表中选择所需的版本，然后选择“安装”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="f27f6-119">Visual Studio 随即将包及其依赖项安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="f27f6-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="f27f6-120">系统可能会要求你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="f27f6-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="f27f6-121">安装完成后，添加的包将显示在“已安装”  选项卡上。包同时还列在解决方案资源管理器的“引用”  节点中，表明可以使用 `using` 语句在项目中引用它们。</span><span class="sxs-lookup"><span data-stu-id="f27f6-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![解决方案资源管理器中的“引用”](media/References.png)

> [!Tip]
> <span data-ttu-id="f27f6-123">若要在搜索中包含预发布版本，并在版本下拉列表中提供预发布版本，请选中“包含预发布版本”  选项。</span><span class="sxs-lookup"><span data-stu-id="f27f6-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="f27f6-124">NuGet 提供项目可使用包的两种格式：[`PackageReference`](package-references-in-project-files.md) 和 [`packages.config`](../reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="f27f6-125">[默认项可以在 Visual Studio 的选项窗口中设置](Package-Restore.md#choose-default-package-management-format)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="f27f6-126">卸载包</span><span class="sxs-lookup"><span data-stu-id="f27f6-126">Uninstall a package</span></span>

1. <span data-ttu-id="f27f6-127">在“解决方案资源管理器”  中，右键单击“引用”  或所需项目，然后选择“管理 NuGet 包...”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f27f6-128">选择“已安装”  选项卡。</span><span class="sxs-lookup"><span data-stu-id="f27f6-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="f27f6-129">选择要卸载的包（如有必要，使用搜索来筛选列表）并选择“卸载”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![卸载包](media/UninstallPackage.png)

1. <span data-ttu-id="f27f6-131">请注意，在卸载包时，“包含预发布版本”  和“包源”  控件无效。</span><span class="sxs-lookup"><span data-stu-id="f27f6-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="f27f6-132">更新包</span><span class="sxs-lookup"><span data-stu-id="f27f6-132">Update a package</span></span>

1. <span data-ttu-id="f27f6-133">在“解决方案资源管理器”  中，右键单击“引用”  或所需项目，然后选择“管理 NuGet 包...”  。（在网站项目中，右键单击“Bin”  文件夹。）</span><span class="sxs-lookup"><span data-stu-id="f27f6-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="f27f6-134">选择“更新”  选项卡，查看所选包源中包含可用更新的包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="f27f6-135">选中“包含预发布版本”  ，以便在更新列表中包含预发布版本的包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="f27f6-136">选择要更新的包，从右侧的下拉列表中选择所需的版本，然后选择“更新”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![更新包](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="f27f6-138">对于某些包，“更新”  按钮处于禁用状态，并显示一条消息，指示它是“由 SDK 隐式引用”（或“AutoReferenced”）。</span><span class="sxs-lookup"><span data-stu-id="f27f6-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="f27f6-139">此消息表明该包是较大框架或 SDK 的一部分，不能单独更新。</span><span class="sxs-lookup"><span data-stu-id="f27f6-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="f27f6-140">（此类包在内部标有 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`。）例如，`Microsoft.NETCore.App` 是 .NET Core SDK 的一部分，并且包版本与应用程序使用的运行时框架的版本不同。</span><span class="sxs-lookup"><span data-stu-id="f27f6-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="f27f6-141">需要[更新 .NET Core 安装](https://aka.ms/dotnet-download)以获取新版本的 ASP.NET Core 和 .NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="f27f6-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="f27f6-142">[请参阅本文档，详细了解 .NET Core 元包和版本控制](/dotnet/core/packages)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="f27f6-143">这适用于以下常用包：</span><span class="sxs-lookup"><span data-stu-id="f27f6-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="f27f6-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="f27f6-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="f27f6-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="f27f6-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="f27f6-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="f27f6-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="f27f6-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="f27f6-147">NETStandard.Library</span></span>

    ![标记为“隐式引用”或“AutoReferenced”的示例包](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="f27f6-149">若要将多个包更新到其最新版本，请在列表中选中它们，然后选择列表上方的“更新”  按钮。</span><span class="sxs-lookup"><span data-stu-id="f27f6-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="f27f6-150">还可以从“已安装”  选项卡更新单个包。在这种情况下，包的详细信息包括版本选择器（受“包含预发布版本”  选项的约束）和“更新”  按钮。</span><span class="sxs-lookup"><span data-stu-id="f27f6-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="f27f6-151">管理解决方案的包</span><span class="sxs-lookup"><span data-stu-id="f27f6-151">Manage packages for the solution</span></span>

<span data-ttu-id="f27f6-152">管理解决方案的包是同时处理多个项目的便捷方式。</span><span class="sxs-lookup"><span data-stu-id="f27f6-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="f27f6-153">选择“工具”>“NuGet 包管理器”>“管理解决方案的 NuGet 包...”菜单命令，或右键单击解决方案，然后选择“管理 NuGet 包...”   ：</span><span class="sxs-lookup"><span data-stu-id="f27f6-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![管理解决方案的 NuGet 包](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="f27f6-155">管理解决方案的包时，UI 让你可以选择受操作影响的项目：</span><span class="sxs-lookup"><span data-stu-id="f27f6-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![管理解决方案的包时的项目选择器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="f27f6-157">“合并”选项卡</span><span class="sxs-lookup"><span data-stu-id="f27f6-157">Consolidate tab</span></span>

<span data-ttu-id="f27f6-158">开发人员通常认为，在同一解决方案的不同项目中使用相同 NuGet 包的不同版本的做法不好。</span><span class="sxs-lookup"><span data-stu-id="f27f6-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="f27f6-159">当你选择管理解决方案的包时，包管理器 UI 提供了一个“合并”  选项卡，让你可以轻松查看解决方案中不同项目使用的具有不同版本号的包：</span><span class="sxs-lookup"><span data-stu-id="f27f6-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![包管理器 UI“合并”选项卡](media/ConsolidateTab.png)

<span data-ttu-id="f27f6-161">在本例中，ClassLibrary1 项目使用的是 EntityFramework 6.2.0，而 ConsoleApp1 使用的是 EntityFramework 6.1.0。</span><span class="sxs-lookup"><span data-stu-id="f27f6-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="f27f6-162">若要合并包版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f27f6-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="f27f6-163">在项目列表中选择要更新的项目。</span><span class="sxs-lookup"><span data-stu-id="f27f6-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="f27f6-164">选择要在“版本”  控件中的所有项目中使用的版本，例如 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="f27f6-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="f27f6-165">选择“安装”按钮  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-165">Select the **Install** button.</span></span>

<span data-ttu-id="f27f6-166">包管理器将选定的包版本安装到所有选定的项目中，之后包不再显示在“合并”选项卡上  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="f27f6-167">包源</span><span class="sxs-lookup"><span data-stu-id="f27f6-167">Package sources</span></span>

<span data-ttu-id="f27f6-168">若要更改 Visual Studio 从中获取包的源，请从源选择器中选择一个源：</span><span class="sxs-lookup"><span data-stu-id="f27f6-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![包管理器 UI 中的包源选择器](media/PackageSourceDropDown.png)

<span data-ttu-id="f27f6-170">管理包源：</span><span class="sxs-lookup"><span data-stu-id="f27f6-170">To manage package sources:</span></span>

1. <span data-ttu-id="f27f6-171">在下面的包管理器 UI 中选择“设置”  图标，或使用“工具”>“选项”  命令并滚动到“NuGet 包管理器”  ：</span><span class="sxs-lookup"><span data-stu-id="f27f6-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![包管理器 UI“设置”图标](media/PackageSourceSettings.png)

1. <span data-ttu-id="f27f6-173">选择“包源”节点  ：</span><span class="sxs-lookup"><span data-stu-id="f27f6-173">Select the **Package Sources** node:</span></span>

    ![“包源”选项](media/options.png)

1. <span data-ttu-id="f27f6-175">要添加源，请选择“+”  ，编辑名称，在“源”  控件中输入 URL 或路径，然后选择“更新”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="f27f6-176">选择器下拉列表中现在显示源。</span><span class="sxs-lookup"><span data-stu-id="f27f6-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="f27f6-177">若要更改包源，请选中它，在“名称”  和“源”  框中进行编辑，然后选择“更新”  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="f27f6-178">若要禁用包源，请清除列表中名称左侧的框。</span><span class="sxs-lookup"><span data-stu-id="f27f6-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="f27f6-179">若要删除包源，请选中它，然后选择“X”  按钮。</span><span class="sxs-lookup"><span data-stu-id="f27f6-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="f27f6-180">使用向上和向下箭头按钮不会更改包源的优先级顺序。</span><span class="sxs-lookup"><span data-stu-id="f27f6-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="f27f6-181">Visual Studio 会忽略包源的顺序，使用来自任何首先响应请求的源的包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="f27f6-182">有关详细信息，请参阅[包源](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="f27f6-183">如果在删除某个包源后，该包源重新出现，则它可能会列在计算机级或用户级 `NuGet.Config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="f27f6-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="f27f6-184">有关这些文件的位置，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)，然后通过手动编辑文件或使用 [nuget 源命令](../reference/nuget-exe-CLI-reference.md)删除源。</span><span class="sxs-lookup"><span data-stu-id="f27f6-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="f27f6-185">包管理器“选项”控件</span><span class="sxs-lookup"><span data-stu-id="f27f6-185">Package manager Options control</span></span>

<span data-ttu-id="f27f6-186">选择包后，包管理器 UI 会在版本选择器下方显示一个可扩展的“选项”小控件（此处显示为折叠和展开）  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="f27f6-187">请注意，对于某些项目类型，仅提供“显示预览窗口”选项  。</span><span class="sxs-lookup"><span data-stu-id="f27f6-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![包管理器选项](media/PackageManagerUIOptions.png)

<span data-ttu-id="f27f6-189">以下各节介绍了这些选项。</span><span class="sxs-lookup"><span data-stu-id="f27f6-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="f27f6-190">显示预览窗口</span><span class="sxs-lookup"><span data-stu-id="f27f6-190">Show preview window</span></span>

<span data-ttu-id="f27f6-191">选中此选项后，模式窗口将显示安装包之前所选包的依赖项：</span><span class="sxs-lookup"><span data-stu-id="f27f6-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![示例“预览”对话框](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="f27f6-193">安装与更新选项</span><span class="sxs-lookup"><span data-stu-id="f27f6-193">Install and Update Options</span></span>

<span data-ttu-id="f27f6-194">（并非适用于所有项目类型。）</span><span class="sxs-lookup"><span data-stu-id="f27f6-194">(Not available for all project types.)</span></span>

<span data-ttu-id="f27f6-195">“依赖项行为”  用于配置 NuGet 如何决定要安装哪些版本的依赖包：</span><span class="sxs-lookup"><span data-stu-id="f27f6-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="f27f6-196">“忽略依赖项”  会跳过安装任何依赖项，这通常会破坏正在安装的软件包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="f27f6-197">如果选择“最低”  [默认选项]，则安装具有可满足主要选定包要求的最小版本号的依赖项。</span><span class="sxs-lookup"><span data-stu-id="f27f6-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="f27f6-198">如果选择“最高版本的修补程序”  ，则安装的版本的主要版本号和次要版本号相同，但修补程序版本号最高。</span><span class="sxs-lookup"><span data-stu-id="f27f6-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="f27f6-199">例如，如果指定版本 1.2.2，则会安装以 1.2 开头的最高版本</span><span class="sxs-lookup"><span data-stu-id="f27f6-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="f27f6-200">如果选择“最高次要版本”  ，则安装的版本的主要版本号相同，但次要版本号和修补程序版本号最高。</span><span class="sxs-lookup"><span data-stu-id="f27f6-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="f27f6-201">如果指定版本 1.2.2，则会安装以 1 开头的最高版本</span><span class="sxs-lookup"><span data-stu-id="f27f6-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="f27f6-202">选择“最高”  可安装包的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="f27f6-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="f27f6-203">“文件冲突操作”  指定 NuGet 应如何处理项目或本地计算机中已存在的包：</span><span class="sxs-lookup"><span data-stu-id="f27f6-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="f27f6-204">“提示”  指示 NuGet 询问是保留还是覆盖现有包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="f27f6-205">“全部忽略”  指示 NuGet 跳过覆盖任何现有包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="f27f6-206">“全部覆盖”  指示 NuGet 覆盖任何现有包。</span><span class="sxs-lookup"><span data-stu-id="f27f6-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="f27f6-207">卸载选项</span><span class="sxs-lookup"><span data-stu-id="f27f6-207">Uninstall Options</span></span>

<span data-ttu-id="f27f6-208">（并非适用于所有项目类型。）</span><span class="sxs-lookup"><span data-stu-id="f27f6-208">(Not available for all project types.)</span></span>

<span data-ttu-id="f27f6-209">“删除依赖项”  ：如果选中，则删除任何依赖包（如果它们未在项目中的其他位置引用）。</span><span class="sxs-lookup"><span data-stu-id="f27f6-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="f27f6-210">“在存在依赖项时仍强制卸载”  ：选中后，即使在项目中仍然引用了该包，也会卸载它。</span><span class="sxs-lookup"><span data-stu-id="f27f6-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="f27f6-211">此选项通常与“删除依赖项”  一起选中，用于删除包及其安装的任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="f27f6-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="f27f6-212">不过，使用此选项可能会导致项目中的引用中断。</span><span class="sxs-lookup"><span data-stu-id="f27f6-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="f27f6-213">在这种情况下，可能需要[重新安装其他包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="f27f6-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
