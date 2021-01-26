---
title: NuGet 1.4 发行说明
description: NuGet 1.4 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777143"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="376df-103">NuGet 1.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="376df-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="376df-104">[NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)  | [NuGet 1.5 发行说明](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="376df-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="376df-105">NuGet 1.4 于2011年6月17日发布。</span><span class="sxs-lookup"><span data-stu-id="376df-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="376df-106">功能</span><span class="sxs-lookup"><span data-stu-id="376df-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="376df-107">Update-Package 改进</span><span class="sxs-lookup"><span data-stu-id="376df-107">Update-Package improvements</span></span>
<span data-ttu-id="376df-108">NuGet 1.4 对 Update-Package 命令进行了大量改进，使解决方案中多个项目的包保持相同的版本。</span><span class="sxs-lookup"><span data-stu-id="376df-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="376df-109">例如，将包升级到最新版本时，需要将安装该程序包的所有项目更新为相同的 verision，这种情况很常见。</span><span class="sxs-lookup"><span data-stu-id="376df-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="376df-110">`Update-Package`命令现在可以更轻松地执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="376df-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="376df-111">更新单个项目中的所有包</span><span class="sxs-lookup"><span data-stu-id="376df-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="376df-112">更新所有项目中的包</span><span class="sxs-lookup"><span data-stu-id="376df-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="376df-113">更新所有项目中的所有包</span><span class="sxs-lookup"><span data-stu-id="376df-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="376df-114">在所有包上执行 "安全" 更新</span><span class="sxs-lookup"><span data-stu-id="376df-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="376df-115">`-Safe`标志仅将升级限制为具有相同的主要版本和次要版本组件的版本。</span><span class="sxs-lookup"><span data-stu-id="376df-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="376df-116">例如，如果安装了包的1.0.0 版，并且源中提供了版本1.0.1、1.0.2 和1.1，则该标志会将 `-Safe` 包更新到1.0.2。</span><span class="sxs-lookup"><span data-stu-id="376df-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="376df-117">如果升级时没有 `-Safe` 标志，会将包升级到最新版本1.1。</span><span class="sxs-lookup"><span data-stu-id="376df-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="376df-118">在解决方案级别管理包</span><span class="sxs-lookup"><span data-stu-id="376df-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="376df-119">在 NuGet 1.4 之前，使用对话框将包安装到多个项目中会很繁琐。</span><span class="sxs-lookup"><span data-stu-id="376df-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="376df-120">每个项目都需要启动一次此对话。</span><span class="sxs-lookup"><span data-stu-id="376df-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="376df-121">NuGet 1.4 添加了对在多个项目中同时安装/卸载/更新包的支持。</span><span class="sxs-lookup"><span data-stu-id="376df-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="376df-122">只需通过右键单击解决方案并选择 " **管理 NuGet 包** " 菜单选项即可启动。</span><span class="sxs-lookup"><span data-stu-id="376df-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![解决方案级别 "管理 NuGet 包" 对话框](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="376df-124">请注意，在对话框的标题栏中显示解决方案的名称，而不是项目的名称。</span><span class="sxs-lookup"><span data-stu-id="376df-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="376df-125">包操作现在提供了一个复选框列表，其中包含操作应应用到的项目的列表。</span><span class="sxs-lookup"><span data-stu-id="376df-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 包项目选择](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="376df-127">有关更多详细信息，请参阅有关 [管理解决方案的包](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)的主题。</span><span class="sxs-lookup"><span data-stu-id="376df-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="376df-128">限制升级到允许的版本</span><span class="sxs-lookup"><span data-stu-id="376df-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="376df-129">默认情况下，在 `Update-Package` 包上运行命令时 (或使用对话框) 更新包时，会将其更新为源中的最新版本。</span><span class="sxs-lookup"><span data-stu-id="376df-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="376df-130">使用更新所有包的新支持，可能需要将包锁定到特定的版本范围。</span><span class="sxs-lookup"><span data-stu-id="376df-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="376df-131">例如，你可能事先知道，你的应用程序将仅适用于包的版本 2. \*，而不是3.0 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="376df-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="376df-132">为了防止意外将包更新到3，NuGet 1.4 添加了对使用新属性手动编辑文件，从而限制包可以升级到的版本范围的支持 `packages.config` `allowedVersions` 。</span><span class="sxs-lookup"><span data-stu-id="376df-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="376df-133">例如，下面的示例演示如何将 `SomePackage` 版本范围 2.0-3.0 (独占) 锁定。</span><span class="sxs-lookup"><span data-stu-id="376df-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="376df-134">`allowedVersions`属性接受使用[版本范围格式](../concepts/package-versioning.md#version-ranges)的值。</span><span class="sxs-lookup"><span data-stu-id="376df-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="376df-135">请注意，在1.4 中，必须手动编辑将包锁定到特定的版本范围。</span><span class="sxs-lookup"><span data-stu-id="376df-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="376df-136">在 NuGet 1.5 中，我们计划添加对通过命令放置此范围的支持 `Install-Package` 。</span><span class="sxs-lookup"><span data-stu-id="376df-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="376df-137">包可视化工具</span><span class="sxs-lookup"><span data-stu-id="376df-137">Package Visualizer</span></span>
<span data-ttu-id="376df-138">通过 **Tools**  ->  **Library 包管理器**  ->  **包可视化工具** 菜单选项启动的新包可视化工具可让你轻松地可视化解决方案中的所有项目及其包依赖关系。</span><span class="sxs-lookup"><span data-stu-id="376df-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="376df-139">_**重要说明：** 此功能利用 Visual Studio 中的 DGML 支持。仅 Visual Studio Ultimate 支持创建可视化效果。仅 Visual Studio Premium 或更高版本中支持查看 DGML 关系图。_</span><span class="sxs-lookup"><span data-stu-id="376df-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![包可视化工具](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="376df-141">NuGet 对话框的自动更新检查</span><span class="sxs-lookup"><span data-stu-id="376df-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="376df-142">某些版本的 NuGet 引入了通过文件表示的新功能，这些新功能 `.nuspec` 不能被 NuGet 对话框的较旧版本所理解。</span><span class="sxs-lookup"><span data-stu-id="376df-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="376df-143">其中一个示例是 NuGet 1.4 中用于 [指定框架程序集](../release-notes/nuget-1.2.md#framework-assembly-refs)的简介。</span><span class="sxs-lookup"><span data-stu-id="376df-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="376df-144">因此，请务必使用最新版本的 NuGet，以确保可以使用包利用最新功能。</span><span class="sxs-lookup"><span data-stu-id="376df-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="376df-145">为了更直观地更新 NuGet，NuGet 对话框包含了在更新版本可用时要突出显示的逻辑。</span><span class="sxs-lookup"><span data-stu-id="376df-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="376df-146">_**注意**：仅当在当前会话中选择了 " **联机** " 选项卡时，才进行此检查。_</span><span class="sxs-lookup"><span data-stu-id="376df-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![新版本可用的 "管理 NuGet 包" 对话框](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="376df-148">若要禁用自动检查更新，请转到 NuGet 设置对话框，并取消选中 " **自动检查更新**"。</span><span class="sxs-lookup"><span data-stu-id="376df-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 设置](./media/nuget-settings.png)

<span data-ttu-id="376df-150">此功能实际上已添加到 NuGet 1.3 中，但在更新到1.3 （如 NuGet 1.4）之前，将不会显示此功能。</span><span class="sxs-lookup"><span data-stu-id="376df-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="376df-151">程序包管理器对话框改进</span><span class="sxs-lookup"><span data-stu-id="376df-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="376df-152">**菜单名称改进**：为了清楚起见，已重命名用于启动对话框的菜单选项。</span><span class="sxs-lookup"><span data-stu-id="376df-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="376df-153">菜单选项现在为 " **管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="376df-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="376df-154">**详细信息窗格显示最新更新日期**：在选择 " **联机** " 或 " **更新** " 选项卡时，NuGet 对话框显示包的详细信息窗格中的最新更新的日期。</span><span class="sxs-lookup"><span data-stu-id="376df-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="376df-155">**显示的标记列表**： Nuget 对话框显示标记。</span><span class="sxs-lookup"><span data-stu-id="376df-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="376df-156">Powershell 改进</span><span class="sxs-lookup"><span data-stu-id="376df-156">Powershell Improvements</span></span>
* <span data-ttu-id="376df-157">**已签名的 powershell 脚本**： NuGet 包括已签名的 powershell 脚本，以实现更严格的环境中的使用。</span><span class="sxs-lookup"><span data-stu-id="376df-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="376df-158">**提示支持**：程序包管理器控制台现在支持通过 `$host.ui.Prompt` 和命令发出提示 `$host.ui.PromptForChoice` 。</span><span class="sxs-lookup"><span data-stu-id="376df-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="376df-159">**包源名称**：在使用标志指定包源时支持提供包源的名称 `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="376df-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="376df-160">nuget.exe 命令行改进</span><span class="sxs-lookup"><span data-stu-id="376df-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="376df-161">**NuGet 自定义命令**：通过使用 MEF 的自定义命令可扩展 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="376df-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="376df-162">**更简单地创建符号包的工作流**： `-Symbols` 标志可应用于基于标准的基于约定的文件夹结构，该结构仅在文件夹中包含源文件和文件即可创建符号包 `.pdb` 。</span><span class="sxs-lookup"><span data-stu-id="376df-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="376df-163">**指定多个源**： `NuGet install` 命令支持使用分号作为分隔符或指定多次来指定多个源 `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="376df-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="376df-164">**代理身份验证支持**：在需要身份验证的代理后面使用 nuget 时，nuget 1.4 添加了对提示用户凭据的支持。</span><span class="sxs-lookup"><span data-stu-id="376df-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="376df-165">**nuget.exe 更新重大更改**： `-Self` 现在需要标记，nuget.exe 才能更新自身。</span><span class="sxs-lookup"><span data-stu-id="376df-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="376df-166">`nuget.exe Update` 现在采用文件的路径 `packages.config` ，并将尝试更新包。</span><span class="sxs-lookup"><span data-stu-id="376df-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="376df-167">请注意，此更新有限，因为它不会： \* \* 更新、添加、删除项目文件中的内容。</span><span class="sxs-lookup"><span data-stu-id="376df-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="376df-168">\* \* 在包中运行 Powershell 脚本。</span><span class="sxs-lookup"><span data-stu-id="376df-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="376df-169">NuGet 服务器支持使用 nuget.exe 推送包</span><span class="sxs-lookup"><span data-stu-id="376df-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="376df-170">NuGet 包含一种简单的方法，可通过 nuget 包托管 [基于轻型 web 的 nuget 存储库](../hosting-packages/nuget-server.md) `NuGet.Server` 。</span><span class="sxs-lookup"><span data-stu-id="376df-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="376df-171">使用 NuGet 1.4，轻型服务器支持使用 nuget.exe 推送和删除包。</span><span class="sxs-lookup"><span data-stu-id="376df-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="376df-172">最新版本的 `NuGet.Server` 添加了 `appSetting` 名为的新 `apiKey` 。</span><span class="sxs-lookup"><span data-stu-id="376df-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="376df-173">如果省略该密钥或将其保留为空，则会禁用向该源推送包。</span><span class="sxs-lookup"><span data-stu-id="376df-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="376df-174">将 apiKey 设置为值 (理想情况下，强密码) 使用 nuget.exe 启用推送包。</span><span class="sxs-lookup"><span data-stu-id="376df-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="376df-175">支持 Windows Phone Tools Mango Edition</span><span class="sxs-lookup"><span data-stu-id="376df-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="376df-176">Mango 的 Windows Phone 工具的候选发布版本中现在支持 NuGet。</span><span class="sxs-lookup"><span data-stu-id="376df-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="376df-177">目前，Windows Phone 工具不支持 Visual Studio 扩展管理器，因此若要为 Windows Phone 工具安装 NuGet，你可能需要手动下载并运行该 VSIX。</span><span class="sxs-lookup"><span data-stu-id="376df-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="376df-178">若要卸载 Windows Phone 工具的 NuGet，请运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="376df-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="376df-179">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="376df-179">Bug Fixes</span></span>
<span data-ttu-id="376df-180">NuGet 1.4 总共修复了88个工作项。</span><span class="sxs-lookup"><span data-stu-id="376df-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="376df-181">71标记为 bug。</span><span class="sxs-lookup"><span data-stu-id="376df-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="376df-182">有关 NuGet 1.4 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="376df-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="376df-183">需要注意的 Bug 修复：</span><span class="sxs-lookup"><span data-stu-id="376df-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="376df-184">[问题 603](http://nuget.codeplex.com/workitem/603)：指定特定包源时，跨不同存储库的包依赖项解析正确。</span><span class="sxs-lookup"><span data-stu-id="376df-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="376df-185">[问题 1036](http://nuget.codeplex.com/workitem/1036)：添加 `NuGet Pack SomeProject.csproj` 到生成后事件不再导致无限循环。</span><span class="sxs-lookup"><span data-stu-id="376df-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="376df-186">[问题 961](http://nuget.codeplex.com/workitem/961)： `-Source` 标志支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="376df-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="376df-187">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="376df-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="376df-188">在 NuGet 1.4 发布之后不久，我们发现了一些很重要的问题需要解决。</span><span class="sxs-lookup"><span data-stu-id="376df-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="376df-189">此更新到1.4 的特定版本号为1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="376df-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="376df-190">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="376df-190">Bug Fixes</span></span>
* <span data-ttu-id="376df-191">[问题 1220](http://nuget.codeplex.com/workitem/1220)： `install.ps1` / `uninstall.ps1` 当有多个项目时，不会在所有项目中执行 Update-Package</span><span class="sxs-lookup"><span data-stu-id="376df-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="376df-192">[问题 1156](http://nuget.codeplex.com/workitem/1156)： Powershell 2 未安装时，包管理器控制台在 W2K3/XP (上停滞) </span><span class="sxs-lookup"><span data-stu-id="376df-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
