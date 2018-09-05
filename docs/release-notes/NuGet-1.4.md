---
title: NuGet 1.4 的发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.4 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550626"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="40696-103">NuGet 1.4 的发行说明</span><span class="sxs-lookup"><span data-stu-id="40696-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="40696-104">[NuGet 1.3 发行说明](../release-notes/nuget-1.3.md) | [NuGet 1.5 发行说明](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="40696-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="40696-105">NuGet 1.4 已于 2011 年 6 月 17 日发布。</span><span class="sxs-lookup"><span data-stu-id="40696-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="40696-106">功能</span><span class="sxs-lookup"><span data-stu-id="40696-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="40696-107">更新包改进</span><span class="sxs-lookup"><span data-stu-id="40696-107">Update-Package improvements</span></span>
<span data-ttu-id="40696-108">NuGet 1.4 引入了大量改进，使其更容易地跨多个项目在解决方案中相同的版本将包的更新 Package 命令。</span><span class="sxs-lookup"><span data-stu-id="40696-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="40696-109">例如，当升级到最新版本的包，是很常见，要想要安装更新到相同 verision 该程序包的所有项目。</span><span class="sxs-lookup"><span data-stu-id="40696-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="40696-110">`Update-Package`命令现在可以更容易：</span><span class="sxs-lookup"><span data-stu-id="40696-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="40696-111">更新单个项目中的所有包</span><span class="sxs-lookup"><span data-stu-id="40696-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="40696-112">更新所有项目中的包</span><span class="sxs-lookup"><span data-stu-id="40696-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="40696-113">更新所有项目中的所有包</span><span class="sxs-lookup"><span data-stu-id="40696-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="40696-114">对所有包执行的"安全"更新</span><span class="sxs-lookup"><span data-stu-id="40696-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="40696-115">`-Safe`标志限制升级到与相同的主要和次要版本组件的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="40696-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="40696-116">例如，如果已安装的包的版本 1.0.0，并且在源中有版本 1.0.1、 1.0.2 和 1.1`-Safe`标志将程序包更新到 1.0.2。</span><span class="sxs-lookup"><span data-stu-id="40696-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="40696-117">升级而`-Safe`标志将包升级到最新版本 1.1。</span><span class="sxs-lookup"><span data-stu-id="40696-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="40696-118">在解决方案级别的管理包</span><span class="sxs-lookup"><span data-stu-id="40696-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="40696-119">在 NuGet 1.4 之前包安装到多个项目是件非常麻烦的使用对话框。</span><span class="sxs-lookup"><span data-stu-id="40696-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="40696-120">它需要启动一次每个项目对话框。</span><span class="sxs-lookup"><span data-stu-id="40696-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="40696-121">NuGet 1.4 同时添加多个项目中的安装/卸载/更新包的支持。</span><span class="sxs-lookup"><span data-stu-id="40696-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="40696-122">只需启动通过右键单击解决方案并选择**管理 NuGet 包**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="40696-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![解决方案级别管理 NuGet 包对话框](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="40696-124">请注意，在对话框的标题栏中，显示解决方案的名称，不是项目的名称。</span><span class="sxs-lookup"><span data-stu-id="40696-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="40696-125">包操作现在提供的操作应该应用到的项目列表的复选框的列表。</span><span class="sxs-lookup"><span data-stu-id="40696-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 包项目选择](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="40696-127">更多详细信息，请参阅主题上[解决方案的管理包](../tools/package-manager-ui.md#managing-packages-for-the-solution)。</span><span class="sxs-lookup"><span data-stu-id="40696-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="40696-128">约束升级到允许的版本</span><span class="sxs-lookup"><span data-stu-id="40696-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="40696-129">默认情况下，运行时`Update-Package`命令包 （或更新包使用对话框），它将更新为在源中的最新版本。</span><span class="sxs-lookup"><span data-stu-id="40696-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="40696-130">用于更新所有包的新支持，可能想要锁定到特定的版本范围的包的情况。</span><span class="sxs-lookup"><span data-stu-id="40696-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="40696-131">例如，您可能事先知道您的应用程序将仅用于版本 2.\* 的包，但不是 3.0 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="40696-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="40696-132">为了防止意外更新为 3 的包，NuGet 1.4 添加了用于约束的包可以通过手动编辑升级到的版本范围的支持`packages.config`文件中使用新`allowedVersions`属性。</span><span class="sxs-lookup"><span data-stu-id="40696-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="40696-133">例如，下面的示例演示如何锁定`SomePackage`包版本 2.0-3.0 （独占） 的范围。</span><span class="sxs-lookup"><span data-stu-id="40696-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="40696-134">`allowedVersions`属性接受的值使用[版本范围格式](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="40696-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="40696-135">请注意，在 1.4，锁定到特定的版本范围的包必须手动编辑。</span><span class="sxs-lookup"><span data-stu-id="40696-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="40696-136">我们打算在 NuGet 1.5 中添加对将通过此范围的支持`Install-Package`命令。</span><span class="sxs-lookup"><span data-stu-id="40696-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="40696-137">包可视化工具</span><span class="sxs-lookup"><span data-stu-id="40696-137">Package Visualizer</span></span>
<span data-ttu-id="40696-138">新的包可视化工具，通过启动**工具** -> **库程序包管理器** -> **包可视化工具**菜单选项可轻松地直观显示所有项目和解决方案及其包依赖关系。</span><span class="sxs-lookup"><span data-stu-id="40696-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="40696-139">_**重要说明：** 此功能在 Visual Studio 中充分利用 DGML 支持。仅支持 Visual Studio Ultimate 中创建可视化效果。查看 DGML 关系图仅支持在 Visual Studio 高级专业版或更高。_</span><span class="sxs-lookup"><span data-stu-id="40696-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![包可视化工具](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="40696-141">NuGet 对话框的自动更新检查</span><span class="sxs-lookup"><span data-stu-id="40696-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="40696-142">某些版本的 NuGet 中引入新功能通过表示`.nuspec`不理解的较旧版本的 NuGet 对话框的文件。</span><span class="sxs-lookup"><span data-stu-id="40696-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="40696-143">例如，对于 NuGet 1.4 中的引入[指定 framework 程序集](../release-notes/nuget-1.2.md#framework-assembly-refs)。</span><span class="sxs-lookup"><span data-stu-id="40696-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="40696-144">因此，务必使用 NuGet 的最新版本以确保你可以使用利用最新功能的包。</span><span class="sxs-lookup"><span data-stu-id="40696-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="40696-145">要使到 NuGet 更新更可见，NuGet 对话框包含逻辑，以便突出显示的较新版本时可用。</span><span class="sxs-lookup"><span data-stu-id="40696-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="40696-146">_**请注意**： 如果在仅进行检查**Online**当前会话中所选选项卡。_</span><span class="sxs-lookup"><span data-stu-id="40696-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![管理 NuGet 包对话框，使用新版本可用](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="40696-148">若要关闭自动检查更新，请转到 NuGet 设置对话框，并取消选中**自动检查更新**。</span><span class="sxs-lookup"><span data-stu-id="40696-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 设置](./media/nuget-settings.png)

<span data-ttu-id="40696-150">此功能实际上已添加在 NuGet 1.3 中，但会显示，当然，直到对 1.3，例如 NuGet 1.4 的更新，提供。</span><span class="sxs-lookup"><span data-stu-id="40696-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="40696-151">包管理器对话框改进</span><span class="sxs-lookup"><span data-stu-id="40696-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="40696-152">**改进的菜单名称**： 为了清楚起见已重命名的菜单选项来启动的对话框。</span><span class="sxs-lookup"><span data-stu-id="40696-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="40696-153">菜单选项现**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="40696-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="40696-154">**详细信息窗格中显示了最新的更新日期**: NuGet 对话框在包的详细信息窗格中显示的最新的更新日期时**Online**或**更新**选择选项卡。</span><span class="sxs-lookup"><span data-stu-id="40696-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="40696-155">**显示标记列表**: Nuget 对话框显示标记。</span><span class="sxs-lookup"><span data-stu-id="40696-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="40696-156">Powershell 改进</span><span class="sxs-lookup"><span data-stu-id="40696-156">Powershell Improvements</span></span>
* <span data-ttu-id="40696-157">**签名的 PowerShell 脚本**: NuGet 包含签名的 Powershell 脚本启用限制性更强的环境中的使用情况。</span><span class="sxs-lookup"><span data-stu-id="40696-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="40696-158">**提示支持**： 的程序包管理器控制台中现在支持通过提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。</span><span class="sxs-lookup"><span data-stu-id="40696-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="40696-159">**包源名称**： 指定包源使用时提供的包源名称支持`-Source`标志。</span><span class="sxs-lookup"><span data-stu-id="40696-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="40696-160">nuget.exe 命令行的改进</span><span class="sxs-lookup"><span data-stu-id="40696-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="40696-161">**NuGet 自定义命令**: nuget.exe 是可扩展的通过使用 MEF 的自定义命令。</span><span class="sxs-lookup"><span data-stu-id="40696-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="40696-162">**更简单的工作流创建符号包**:`-Symbols`标志可以应用于正常约定基于文件夹结构创建符号包仅包括源和`.pdb`文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="40696-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="40696-163">**指定多个源**:`NuGet install`命令支持指定多个源使用分号作为分隔符或通过指定`-Source`多次。</span><span class="sxs-lookup"><span data-stu-id="40696-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="40696-164">**代理身份验证支持**: NuGet 1.4 增加了对要求身份验证的代理后面使用 NuGet 时，会提示输入用户凭据支持。</span><span class="sxs-lookup"><span data-stu-id="40696-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="40696-165">**nuget.exe 更新重大更改**:`-Self`标志是现在所需的 nuget.exe 自行更新。</span><span class="sxs-lookup"><span data-stu-id="40696-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="40696-166">`nuget.exe Update` 现在只需在路径中`packages.config`文件，并将尝试更新包。</span><span class="sxs-lookup"><span data-stu-id="40696-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="40696-167">请注意此更新的局限性在于它不会: * * 更新，请添加、 删除项目文件中的内容。</span><span class="sxs-lookup"><span data-stu-id="40696-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="40696-168">* * 运行的包中的 Powershell 脚本。</span><span class="sxs-lookup"><span data-stu-id="40696-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="40696-169">使用 nuget.exe 推送包的 NuGet 服务器支持</span><span class="sxs-lookup"><span data-stu-id="40696-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="40696-170">NuGet 包括主机的简单方法[轻型 web 基于 NuGet 存储库](../hosting-packages/nuget-server.md)通过`NuGet.Server`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="40696-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="40696-171">与 NuGet 1.4 轻型服务器支持将推送和删除包使用 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="40696-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="40696-172">最新版`NuGet.Server`添加一个新`appSetting`名为`apiKey`。</span><span class="sxs-lookup"><span data-stu-id="40696-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="40696-173">当省略密钥或将其留空时，将包推送到源被禁用。</span><span class="sxs-lookup"><span data-stu-id="40696-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="40696-174">设置 apiKey 的值 （理想情况下为强密码），使用 nuget.exe 推送包。</span><span class="sxs-lookup"><span data-stu-id="40696-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="40696-175">对 Windows Phone 工具 Mango Edition 的支持</span><span class="sxs-lookup"><span data-stu-id="40696-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="40696-176">NuGet 现在支持在 Windows Phone Mango 的工具的候选发布版本。</span><span class="sxs-lookup"><span data-stu-id="40696-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="40696-177">目前，Windows Phone 工具不具有对 Visual Studio 扩展管理器，因此，若要安装 Windows Phone 工具的 NuGet 支持，可能需要下载并手动运行 VSIX。</span><span class="sxs-lookup"><span data-stu-id="40696-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="40696-178">若要卸载 Windows Phone 工具的 NuGet，请运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="40696-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="40696-179">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="40696-179">Bug Fixes</span></span>
<span data-ttu-id="40696-180">NuGet 1.4 有工作项固定为 88 总计。</span><span class="sxs-lookup"><span data-stu-id="40696-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="40696-181">71 的那些已标记为 bug。</span><span class="sxs-lookup"><span data-stu-id="40696-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="40696-182">有关工作的完整列表项中已修复 NuGet 1.4，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="40696-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="40696-183">值得注意的 bug 修复：</span><span class="sxs-lookup"><span data-stu-id="40696-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="40696-184">[问题 603](http://nuget.codeplex.com/workitem/603)： 跨不同的存储库的包依赖项是否正确解析时指定特定的包源。</span><span class="sxs-lookup"><span data-stu-id="40696-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="40696-185">[问题 1036年](http://nuget.codeplex.com/workitem/1036)： 添加`NuGet Pack SomeProject.csproj`后不再生成事件将导致无限循环。</span><span class="sxs-lookup"><span data-stu-id="40696-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="40696-186">[问题 961](http://nuget.codeplex.com/workitem/961):`-Source`标志支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="40696-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="40696-187">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="40696-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="40696-188">NuGet 1.4 发布，我们发现了几个重要修复的问题。</span><span class="sxs-lookup"><span data-stu-id="40696-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="40696-189">1.4 的此次更新的特定版本号是 1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="40696-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="40696-190">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="40696-190">Bug Fixes</span></span>
* <span data-ttu-id="40696-191">[问题 1220年](http://nuget.codeplex.com/workitem/1220)： 更新包不会执行`install.ps1` / `uninstall.ps1`在多个项目时的所有项目中</span><span class="sxs-lookup"><span data-stu-id="40696-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="40696-192">[问题 1156年](http://nuget.codeplex.com/workitem/1156)： 程序包管理器控制台停滞 W2K3/XP 上 （如果未安装 Powershell 2）</span><span class="sxs-lookup"><span data-stu-id="40696-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
