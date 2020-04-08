---
title: NuGet 程序包还原
description: 概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428437"
---
# <a name="restore-packages-using-package-restore"></a><span data-ttu-id="8c687-103">使用“程序包还原”还原程序包</span><span class="sxs-lookup"><span data-stu-id="8c687-103">Restore packages using Package Restore</span></span>

<span data-ttu-id="8c687-104">为了促成更干净的开发环境并减少存储库大小，NuGet“程序包还原”安装了项目文件或 `packages.config` 中列出的所有项目依赖项  。</span><span class="sxs-lookup"><span data-stu-id="8c687-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="8c687-105">.NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令执行自动程序包还原。</span><span class="sxs-lookup"><span data-stu-id="8c687-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="8c687-106">Visual Studio 可以在构建项目时自动还原包，并且你可以随时通过 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 的 xbuild 来还原包。</span><span class="sxs-lookup"><span data-stu-id="8c687-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="8c687-107">程序包还原确保所有项目的依赖项都可用，无需将其存储在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="8c687-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="8c687-108">要配置源代码管理存储库以排除包二进制文件，请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="8c687-109">程序包还原概述</span><span class="sxs-lookup"><span data-stu-id="8c687-109">Package Restore overview</span></span>

<span data-ttu-id="8c687-110">程序包还原首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="8c687-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="8c687-111">如果尚未安装包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-global-packages-and-cache-folders.md)中检索它。</span><span class="sxs-lookup"><span data-stu-id="8c687-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="8c687-112">如果包不在缓存中，NuGet 将尝试从 Visual Studio 的“工具” > “选项” > “NuGet 包管理器” > “包源”下的列表中的所有已启用的源下载包     。</span><span class="sxs-lookup"><span data-stu-id="8c687-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="8c687-113">在还原期间，NuGet 会忽略包源的顺序，使用来自最先响应请求的源的包。</span><span class="sxs-lookup"><span data-stu-id="8c687-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="8c687-114">有关 NuGet 的行为方式的详细信息，请参阅[常见的 NuGet 配置](Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="8c687-115">在检查完所有源之前，NuGet 不会指示包还原失败。</span><span class="sxs-lookup"><span data-stu-id="8c687-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="8c687-116">届时，NuGet 仅会报告列表中最后一个源的失败。</span><span class="sxs-lookup"><span data-stu-id="8c687-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="8c687-117">该错误说明包已不在其他任意源上，尽管没有单独显示这些源的错误。 </span><span class="sxs-lookup"><span data-stu-id="8c687-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="8c687-118">还原包</span><span class="sxs-lookup"><span data-stu-id="8c687-118">Restore packages</span></span>

<span data-ttu-id="8c687-119">程序包还原试图将所有程序包依赖项安装到与项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用相匹配的正确状态。</span><span class="sxs-lookup"><span data-stu-id="8c687-119">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="8c687-120">（在 Visual Studio 中，这些引用位于解决方案资源管理器的“依赖项 \ NuGet”或“引用”节点中。）  </span><span class="sxs-lookup"><span data-stu-id="8c687-120">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.)</span></span>

1. <span data-ttu-id="8c687-121">若项目文件中的程序包引用正确，则使用你的首选工具还原程序包。</span><span class="sxs-lookup"><span data-stu-id="8c687-121">If the package references in your project file are correct, use your preferred tool to restore packages.</span></span>

   - <span data-ttu-id="8c687-122">[Visual Studio](#restore-using-visual-studio)（[自动还原](#restore-packages-automatically-using-visual-studio)或[手动还原](#restore-packages-manually-using-visual-studio)）</span><span class="sxs-lookup"><span data-stu-id="8c687-122">[Visual Studio](#restore-using-visual-studio) ([automatic restore](#restore-packages-automatically-using-visual-studio) or [manual restore](#restore-packages-manually-using-visual-studio))</span></span>
   - [<span data-ttu-id="8c687-123">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="8c687-123">dotnet CLI</span></span>](#restore-using-the-dotnet-cli)
   - [<span data-ttu-id="8c687-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="8c687-124">nuget.exe CLI</span></span>](#restore-using-the-nugetexe-cli)
   - [<span data-ttu-id="8c687-125">MSBuild</span><span class="sxs-lookup"><span data-stu-id="8c687-125">MSBuild</span></span>](#restore-using-msbuild)
   - [<span data-ttu-id="8c687-126">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="8c687-126">Azure Pipelines</span></span>](#restore-using-azure-pipelines)
   - [<span data-ttu-id="8c687-127">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="8c687-127">Azure DevOps Server</span></span>](#restore-using-azure-devops-server)

   <span data-ttu-id="8c687-128">若项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用不正确（它们与使用程序包还原时所需的状态不匹配），则需要安装或更新程序包。</span><span class="sxs-lookup"><span data-stu-id="8c687-128">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead.</span></span>

   <span data-ttu-id="8c687-129">对于使用 PackageReference 的项目，在成功还原后，global-packages 文件夹应显示此包，并且会重新创建 `obj/project.assets.json` 文件。 </span><span class="sxs-lookup"><span data-stu-id="8c687-129">For projects using PackageReference, after a successful restore, the package should be present in the *global-packages* folder and the `obj/project.assets.json` file is recreated.</span></span> <span data-ttu-id="8c687-130">对于使用 `packages.config` 的项目，项目的 `packages` 文件夹应显示此程序包。</span><span class="sxs-lookup"><span data-stu-id="8c687-130">For projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="8c687-131">该项目现在应能成功生成。</span><span class="sxs-lookup"><span data-stu-id="8c687-131">The project should now build successfully.</span></span> 

2. <span data-ttu-id="8c687-132">运行程序包还原后，若仍出现程序包缺失的情况或与程序包相关的错误（如 Visual Studio 的解决方案资源管理器中出现错误图标），可能需要按照[程序包还原错误疑难解答](package-restore-troubleshooting.md)中的步骤操作，或[重新安装和更新程序包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-132">After running Package Restore, if you still experience missing packages or package-related errors (such as error icons in Solution Explorer in Visual Studio), you may need to follow instructions described in [Troubleshooting Package Restore errors](package-restore-troubleshooting.md) or, alternatively, [reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

   <span data-ttu-id="8c687-133">Visual Studio 中的程序包管理器控制台提供了多个灵活的选项，用于重新安装程序包。</span><span class="sxs-lookup"><span data-stu-id="8c687-133">In Visual Studio, the Package Manager Console provides several flexible options for reinstalling packages.</span></span> <span data-ttu-id="8c687-134">请参阅[使用 Package-Update](reinstalling-and-updating-packages.md#using-update-package)。</span><span class="sxs-lookup"><span data-stu-id="8c687-134">See [Using Package-Update](reinstalling-and-updating-packages.md#using-update-package).</span></span>

## <a name="restore-using-visual-studio"></a><span data-ttu-id="8c687-135">使用 Visual Studio 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-135">Restore using Visual Studio</span></span>

<span data-ttu-id="8c687-136">在 Windows 上的 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="8c687-136">In Visual Studio on Windows, either:</span></span>

- <span data-ttu-id="8c687-137">自动还原程序包，或</span><span class="sxs-lookup"><span data-stu-id="8c687-137">Restore packages automatically, or</span></span>

- <span data-ttu-id="8c687-138">手动还原程序包</span><span class="sxs-lookup"><span data-stu-id="8c687-138">Restore packages manually</span></span>

### <a name="restore-packages-automatically-using-visual-studio"></a><span data-ttu-id="8c687-139">使用 Visual Studio 自动还原程序包</span><span class="sxs-lookup"><span data-stu-id="8c687-139">Restore packages automatically using Visual Studio</span></span>

<span data-ttu-id="8c687-140">从模板创建项目或生成项目时，是否自动执行程序包还原取决于[启用和禁用程序包还原](#enable-and-disable-package-restore-in-visual-studio)中的选项。</span><span class="sxs-lookup"><span data-stu-id="8c687-140">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="8c687-141">此外，在 NuGet 4.0+ 中，对 SDK 样式的项目（通常是 .NET Core 或 .NET Standard 项目）进行更改时还会自动进行还原。</span><span class="sxs-lookup"><span data-stu-id="8c687-141">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

1. <span data-ttu-id="8c687-142">按照以下方式启用自动程序包还原：选择“工具” > “选项” > “NuGet 程序包管理器”，然后在“程序包还原”下选择“在 Visual Studio 中生成期间自动检查缺少的程序包”。     </span><span class="sxs-lookup"><span data-stu-id="8c687-142">Enable automatic package restore by choosing **Tools** > **Options** > **NuGet Package Manager**, and then selecting **Automatically check for missing packages during build in Visual Studio** under **Package Restore**.</span></span>

   <span data-ttu-id="8c687-143">对于非 SDK 样式项目，首先需要选择“允许 NuGet 下载缺少的程序包”，以启动自动还原选项。 </span><span class="sxs-lookup"><span data-stu-id="8c687-143">For non-SDK-style projects, you first need to select **Allow NuGet to download missing packages** to enable the automatic restore option.</span></span>

1. <span data-ttu-id="8c687-144">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8c687-144">Build the project.</span></span>

   <span data-ttu-id="8c687-145">如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。</span><span class="sxs-lookup"><span data-stu-id="8c687-145">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="8c687-146">右键单击并选择“管理 NuGet 包”，然后使用“包管理器”卸载并重新安装受影响的包   。</span><span class="sxs-lookup"><span data-stu-id="8c687-146">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="8c687-147">有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-147">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="8c687-148">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="8c687-148">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="8c687-149">对于旧项目，亦请参阅[迁移到自动程序包还原](#migrate-to-automatic-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="8c687-149">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="8c687-150">另请参阅[程序包还原疑难解答](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-150">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="restore-packages-manually-using-visual-studio"></a><span data-ttu-id="8c687-151">使用 Visual Studio 手动还原程序包</span><span class="sxs-lookup"><span data-stu-id="8c687-151">Restore packages manually using Visual Studio</span></span>

1. <span data-ttu-id="8c687-152">选择“工具” > “选项” > “NuGet 程序包管理器”，以启用程序包还原。   </span><span class="sxs-lookup"><span data-stu-id="8c687-152">Enable package restore by choosing **Tools** > **Options** > **NuGet Package Manager**.</span></span> <span data-ttu-id="8c687-153">在“程序包还原”选项下，选择“允许 NuGet 下载缺少的程序包”。  </span><span class="sxs-lookup"><span data-stu-id="8c687-153">Under **Package Restore** options, select **Allow NuGet to download missing packages**.</span></span>

1. <span data-ttu-id="8c687-154">在“解决方案资源管理器”中，右键单击解决方案并选择“还原 NuGet 程序包”   。</span><span class="sxs-lookup"><span data-stu-id="8c687-154">In **Solution Explorer**, right click the solution and select **Restore NuGet Packages**.</span></span>

   <span data-ttu-id="8c687-155">如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。</span><span class="sxs-lookup"><span data-stu-id="8c687-155">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="8c687-156">右键单击并选择“管理 NuGet 程序包”，然后使用“程序包管理器”卸载并重新安装受影响的程序包   。</span><span class="sxs-lookup"><span data-stu-id="8c687-156">Right-click and select **Manage NuGet Packages**, and then use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="8c687-157">有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-157">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="8c687-158">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="8c687-158">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="8c687-159">对于旧项目，亦请参阅[迁移到自动程序包还原](#migrate-to-automatic-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="8c687-159">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="8c687-160">另请参阅[程序包还原疑难解答](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-160">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="enable-and-disable-package-restore-in-visual-studio"></a><span data-ttu-id="8c687-161">在 Visual Studio 中启用和禁用程序包还原</span><span class="sxs-lookup"><span data-stu-id="8c687-161">Enable and disable package restore in Visual Studio</span></span>

<span data-ttu-id="8c687-162">在 Visual Studio 中，主要通过“工具” > “选项” > “NuGet 包管理器”控制程序包还原    ：</span><span class="sxs-lookup"><span data-stu-id="8c687-162">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![通过 NuGet 包管理器选项控制程序包还原](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="8c687-164">“允许 NuGet 下载缺失的包”通过更改 `NuGet.Config` 文件中的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 设置，控制程序包还原的所有窗体（该文件在 Windows 上位于 `%AppData%\NuGet\`，在 Mac/Linux 上位于 `~/.nuget/NuGet/`）  。</span><span class="sxs-lookup"><span data-stu-id="8c687-164">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="8c687-165">在 Visual Studio 中，此设置还可启用解决方案上下文菜单中的 Restore NuGet Packages 命令  。</span><span class="sxs-lookup"><span data-stu-id="8c687-165">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > <span data-ttu-id="8c687-166">要全局重写 `packageRestore/enabled` 设置，请在启动 Visual Studio 或启动生成之前，将 EnableNuGetPackageRestore 环境变量设为 TRUE 或 FALSE 值  。</span><span class="sxs-lookup"><span data-stu-id="8c687-166">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="8c687-167">“生成期间在 Visual Studio 中自动检查缺失的包”通过更改 `NuGet.Config` 文件的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 设置控制自动还原  。</span><span class="sxs-lookup"><span data-stu-id="8c687-167">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="8c687-168">将该选项设置为 True 后，从 Visual Studio 运行生成会自动还原任何缺失的包。</span><span class="sxs-lookup"><span data-stu-id="8c687-168">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="8c687-169">此设置不会影响从 MSBuild 命令行运行的生成。</span><span class="sxs-lookup"><span data-stu-id="8c687-169">This setting doesn't affect builds run from the MSBuild command line.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="8c687-170">要为计算机上的所有用户启用或禁用程序包还原，开发人员或公司可以将配置设置添加到全局 `nuget.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="8c687-170">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="8c687-171">全局 `nuget.config` 在 Windows 中位于 `%ProgramData%\NuGet\Config` 下，有时在特定的 `\{IDE}\{Version}\{SKU}\`Visual Studio 文件夹下，或者在 Mac/Linux 中位于 `~/.local/share` 下。</span><span class="sxs-lookup"><span data-stu-id="8c687-171">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="8c687-172">然后，各个用户可以按照项目级别的要求有选择地启用还原。</span><span class="sxs-lookup"><span data-stu-id="8c687-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="8c687-173">有关 NuGet 如何设置多个配置文件优先级的详细信息，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="8c687-173">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="8c687-174">如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值  。</span><span class="sxs-lookup"><span data-stu-id="8c687-174">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

### <a name="choose-default-package-management-format"></a><span data-ttu-id="8c687-175">选择默认包管理格式</span><span class="sxs-lookup"><span data-stu-id="8c687-175">Choose default package management format</span></span>

![通过 NuGet 包管理器选项控制默认包管理格式](media/Restore-02-PackageFormatOptions.png)

<span data-ttu-id="8c687-177">NuGet 提供项目可使用包的两种格式：[`PackageReference`](package-references-in-project-files.md) 和 [`packages.config`](../reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-177">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="8c687-178">默认格式可从“包管理”标题下的下拉菜单中选择  。</span><span class="sxs-lookup"><span data-stu-id="8c687-178">The default format can be selected from the drop-down under the **Package Management** heading.</span></span> <span data-ttu-id="8c687-179">在项目中安装首个包时还会出现一个提示选项。</span><span class="sxs-lookup"><span data-stu-id="8c687-179">An option to be prompted when the first package is installed in a project is also available.</span></span>

> [!Note]
> <span data-ttu-id="8c687-180">如果这两种包管理格式均不受项目支持，则会使用与项目兼容的包管理格式，因此所用格式可能并非选项中的默认设置。</span><span class="sxs-lookup"><span data-stu-id="8c687-180">If a project does not support both package management formats, the package management format used will be the one that's compatible with the project, and therefore may not be the default set in the options.</span></span> <span data-ttu-id="8c687-181">此外，NuGet 不会在安装首个包时显示选择提示，即使选项窗口中已选中此选项时亦是如此。</span><span class="sxs-lookup"><span data-stu-id="8c687-181">Additionally, NuGet will not prompt for selection on first package installation, even if the option is selected in the options window.</span></span>
>
> <span data-ttu-id="8c687-182">如果使用包管理器控制台在项目中安装首个包，则即使选项窗口中已选中该选项，NuGet 也不会提示选择格式。</span><span class="sxs-lookup"><span data-stu-id="8c687-182">If Package Manager Console is used to install the first package in a project, NuGet will not prompt for format selection, even if the option is selected in the options window.</span></span>

## <a name="restore-using-the-dotnet-cli"></a><span data-ttu-id="8c687-183">使用 dotnet CLI 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-183">Restore using the dotnet CLI</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="8c687-184">若要将缺少的程序包引用添加到项目文件，请使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)，它也会运行 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="8c687-184">To add a missing package reference to the project file, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), which also runs the `restore` command.</span></span>

## <a name="restore-using-the-nugetexe-cli"></a><span data-ttu-id="8c687-185">使用 nuget.exe CLI 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-185">Restore using the nuget.exe CLI</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="8c687-186">`restore` 命令不会修改项目文件或 packages.config。  要添加依赖项，请通过 Visual Studio 中的包管理器 UI 或控制台添加包，或修改 packages.config  ，然后运行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="8c687-186">The `restore`command does not modify a project file or *packages.config*. To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

## <a name="restore-using-msbuild"></a><span data-ttu-id="8c687-187">使用 MSBuild 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-187">Restore using MSBuild</span></span>

<span data-ttu-id="8c687-188">使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令还原项目文件中通过 PackageReference 列出的程序包。</span><span class="sxs-lookup"><span data-stu-id="8c687-188">To restore packages listed in the project file with PackageReference, use the the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command.</span></span> <span data-ttu-id="8c687-189">此命令仅适用于 Visual Studio 2017 及更高版本附带的 NuGet 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="8c687-189">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="8c687-190">`nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。</span><span class="sxs-lookup"><span data-stu-id="8c687-190">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

1. <span data-ttu-id="8c687-191">打开开发人员命令提示符（在“搜索”框中，键入“开发人员命令提示符”）   。</span><span class="sxs-lookup"><span data-stu-id="8c687-191">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="8c687-192">用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置  。</span><span class="sxs-lookup"><span data-stu-id="8c687-192">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

2. <span data-ttu-id="8c687-193">切换到包含项目文件的文件夹，然后键入以下命令。</span><span class="sxs-lookup"><span data-stu-id="8c687-193">Switch to the folder containing the project file and type the following command.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. <span data-ttu-id="8c687-194">键入以下命令以重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="8c687-194">Type the following command to rebuild the project.</span></span>

   ```cmd
   msbuild
   ```

   <span data-ttu-id="8c687-195">确保 MSBuild 输出指示生成已成功完成。</span><span class="sxs-lookup"><span data-stu-id="8c687-195">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="restore-using-azure-pipelines"></a><span data-ttu-id="8c687-196">使用 Azure Pipelines 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-196">Restore using Azure Pipelines</span></span>

<span data-ttu-id="8c687-197">在 Azure Pipelines 上创建生成定义时，请在任意生成任务前将 NuGet [还原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 或 .NET Core [还原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 任务包括在定义中。</span><span class="sxs-lookup"><span data-stu-id="8c687-197">When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="8c687-198">默认情况下，某些生成模板包括还原任务。</span><span class="sxs-lookup"><span data-stu-id="8c687-198">Some build templates include the restore task by default.</span></span>

## <a name="restore-using-azure-devops-server"></a><span data-ttu-id="8c687-199">使用 Azure DevOps Server 进行还原</span><span class="sxs-lookup"><span data-stu-id="8c687-199">Restore using Azure DevOps Server</span></span>

<span data-ttu-id="8c687-200">如果你使用的是 TFS 2013 或更高版本的 Team Build 模板，Azure DevOps Server 和 TFS 2013 及更高版本会在生成期间自动还原包。</span><span class="sxs-lookup"><span data-stu-id="8c687-200">Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="8c687-201">对于较早的 TFS 版本，可以包含一个生成步骤来运行命令行还原选项，或者选择将生成模板迁移到更高版本。</span><span class="sxs-lookup"><span data-stu-id="8c687-201">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="8c687-202">有关详细信息，请参阅[使用 Team Foundation Build 设置程序包还原](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-202">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="8c687-203">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="8c687-203">Constrain package versions with restore</span></span>

<span data-ttu-id="8c687-204">NuGet 通过任意方法还原包时，将遵守你在 `packages.config` 或项目文件中指定的任何约束：</span><span class="sxs-lookup"><span data-stu-id="8c687-204">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="8c687-205">在 `packages.config` 中，可在依赖项的 `allowedVersion` 属性中指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="8c687-205">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="8c687-206">有关详细信息，请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="8c687-206">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="8c687-207">例如：</span><span class="sxs-lookup"><span data-stu-id="8c687-207">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="8c687-208">在项目文件中，可以使用 PackageReference 直接指定依赖项的范围。</span><span class="sxs-lookup"><span data-stu-id="8c687-208">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="8c687-209">例如：</span><span class="sxs-lookup"><span data-stu-id="8c687-209">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="8c687-210">在所有情况下，都使用[包版本控制](../concepts/package-versioning.md)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="8c687-210">In all cases, use the notation described in [Package versioning](../concepts/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="8c687-211">强制从包源还原</span><span class="sxs-lookup"><span data-stu-id="8c687-211">Force restore from package sources</span></span>

<span data-ttu-id="8c687-212">默认情况下，NuGet 还原操作使用 global-packages 和 http-cache 文件夹中的包，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述   。</span><span class="sxs-lookup"><span data-stu-id="8c687-212">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="8c687-213">若要避免使用 global-packages  文件夹，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="8c687-213">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="8c687-214">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c687-214">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="8c687-215">在进行还原操作之前，使用下列方法之一暂时更改 global-packages 的位置  ：</span><span class="sxs-lookup"><span data-stu-id="8c687-215">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="8c687-216">将 NUGET_PACKAGES 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c687-216">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="8c687-217">创建 `NuGet.Config` 文件，将 `globalPackagesFolder`（如果使用 PackageReference）或 `repositoryPath`（如果使用 `packages.config`）设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c687-217">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="8c687-218">有关详细信息，请参阅[配置设置](../reference/nuget-config-file.md#config-section)。</span><span class="sxs-lookup"><span data-stu-id="8c687-218">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="8c687-219">仅限 MSBuild：指定具有 `RestorePackagesPath` 属性的其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c687-219">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="8c687-220">若要避免将缓存用于 HTTP 源，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="8c687-220">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="8c687-221">将 `-NoCache` 选项与 `nuget restore` 结合使用，或者将 `--no-cache` 选项与 `dotnet restore` 结合使用。</span><span class="sxs-lookup"><span data-stu-id="8c687-221">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="8c687-222">这些选项不会影响通过 Visual Studio 包管理器或控制台执行的还原操作。</span><span class="sxs-lookup"><span data-stu-id="8c687-222">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="8c687-223">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear` 清除缓存。</span><span class="sxs-lookup"><span data-stu-id="8c687-223">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="8c687-224">暂时将 NUGET_HTTP_CACHE_PATH 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c687-224">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="8c687-225">迁移到自动程序包还原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8c687-225">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="8c687-226">对于 NuGet 2.6 及更早版本，以前支持集成 MSBuild 的包恢复，但现在不再支持。</span><span class="sxs-lookup"><span data-stu-id="8c687-226">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="8c687-227">（通常通过右键单击 Visual Studio 中的解决方案并选择“启用 NuGet 程序包还原”  来启用）。</span><span class="sxs-lookup"><span data-stu-id="8c687-227">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="8c687-228">如果项目使用已弃用的集成 MSBuild 的程序包还原，请迁移到自动程序包还原。</span><span class="sxs-lookup"><span data-stu-id="8c687-228">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="8c687-229">使用集成 MSBuild 的程序包还原的项目通常包含带有三个文件的 .nuget  文件夹：NuGet.config  、nuget.exe  和 NuGet.targets  。</span><span class="sxs-lookup"><span data-stu-id="8c687-229">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="8c687-230">NuGet.targets 文件的存在与否决定了 NuGet 是否继续使用集成 MSBuild 的方法，因此在迁移期间必须删除此文件。 </span><span class="sxs-lookup"><span data-stu-id="8c687-230">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="8c687-231">要迁移到自动程序包还原，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8c687-231">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="8c687-232">关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8c687-232">Close Visual Studio.</span></span>
2. <span data-ttu-id="8c687-233">删除 .nuget/nuget.exe  和 .nuget/NuGet.targets  。</span><span class="sxs-lookup"><span data-stu-id="8c687-233">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="8c687-234">对于每个项目文件，删除 `<RestorePackages>` 元素并删除对 NuGet.targets  的任何引用。</span><span class="sxs-lookup"><span data-stu-id="8c687-234">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="8c687-235">要测试自动程序包还原，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8c687-235">To test the automatic package restore:</span></span>

1. <span data-ttu-id="8c687-236">删除解决方案中的“packages”文件夹  。</span><span class="sxs-lookup"><span data-stu-id="8c687-236">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="8c687-237">在 Visual Studio 中打开解决方案并开始生成。</span><span class="sxs-lookup"><span data-stu-id="8c687-237">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="8c687-238">自动程序包还原应下载并安装每个依赖包，而不将它们添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="8c687-238">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8c687-239">疑难解答</span><span class="sxs-lookup"><span data-stu-id="8c687-239">Troubleshooting</span></span>

<span data-ttu-id="8c687-240">请参阅[程序包还原疑难解答](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="8c687-240">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
