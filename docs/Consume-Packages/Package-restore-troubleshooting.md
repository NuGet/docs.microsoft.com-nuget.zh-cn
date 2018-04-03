---
title: 对 Visual Studio 中的 NuGet 包还原进行故障排除 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。
keywords: NuGet 包还原, 还原包, 故障排除, 故障排除
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="8ebc8-104">包还原错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="8ebc8-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="8ebc8-105">本文着重介绍还原包时遇到的常见错误以及相应的解决步骤。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="8ebc8-106">有关还原包的完整详细信息，请参阅[包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="8ebc8-107">如果此处的说明对你没有帮助，[请在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们可以更仔细地检查你的情况。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="8ebc8-108">请勿使用可能出现在该页面上的“此页面有帮助吗?”控件，</span><span class="sxs-lookup"><span data-stu-id="8ebc8-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="8ebc8-109">因为它无法让我们与你联系以获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="8ebc8-110">适用于 Visual Studio 用户的快速解决方案</span><span class="sxs-lookup"><span data-stu-id="8ebc8-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="8ebc8-111">如果使用 Visual Studio，请首先按如下方式启用包还原。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="8ebc8-112">否则，请继续执行后面的部分。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="8ebc8-113">选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="8ebc8-114">在“包还原”下设置这两个选项。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="8ebc8-115">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-115">Select **OK**.</span></span>
1. <span data-ttu-id="8ebc8-116">再次生成项目。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-116">Build your project again.</span></span>

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="8ebc8-118">也可以在 `NuGet.config` 文件中更改这些设置；请参阅[同意](#consent)部分。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="8ebc8-119">此项目引用了此计算机上缺少的 NuGet 程序包</span><span class="sxs-lookup"><span data-stu-id="8ebc8-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="8ebc8-120">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="8ebc8-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="8ebc8-121">当你尝试生成包含对一个或多个 NuGet 包的引用的项目，但这些包当前未安装在计算机上或项目中时，发生了此错误。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="8ebc8-122">使用 PackageReference 管理格式时，此错误意味着包未安装在 global-packages 文件夹中，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="8ebc8-123">当使用 `packages.config` 时，此错误意味着包未安装在解决方案根目录中的 `packages` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="8ebc8-124">当你从源代码管理或其他下载获得项目的源代码时，通常会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="8ebc8-125">包通常从源代码管理或下载中省略，因为它们可以从包源（例如 nuget.org）中还原（请参阅[包和源代码管理](Packages-and-Source-Control.md)）。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="8ebc8-126">否则，包含它们会导致存储库膨胀或创建不必要的大型 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="8ebc8-127">使用下列方法之一还原包：</span><span class="sxs-lookup"><span data-stu-id="8ebc8-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="8ebc8-128">在 Visual Studio 中，通过以下方法启用包还原：选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令，在“包还原”下设置这两个选项，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-128">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="8ebc8-129">然后再次生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-129">Then build the solution again.</span></span>
- <span data-ttu-id="8ebc8-130">对于 .NET Core 项目，运行 `dotnet restore` 或 `dotnet build`（它会自动运行还原）。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-130">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="8ebc8-131">在命令行上运行 `nuget restore`（使用 `dotnet` 创建的项目除外，这种情况下请使用 `dotnet restore`）。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-131">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="8ebc8-132">在包含使用 PackageReference 格式的项目的命令行上，运行 `msbuild /t:restore`。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-132">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="8ebc8-133">成功还原后，包应显示在 global-packages 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-133">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="8ebc8-134">对于使用 PackageReference 的项目，还原应重新创建 `obj/project.assets.json` 文件；对于使用 `packages.config` 的项目，包应显示在项目的 `packages` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-134">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="8ebc8-135">该项目现在应能成功生成。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-135">The project should now build successfully.</span></span> <span data-ttu-id="8ebc8-136">如果没有，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们跟进。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-136">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="8ebc8-137">找不到资产文件 project.assets.json</span><span class="sxs-lookup"><span data-stu-id="8ebc8-137">Assets file project.assets.json not found</span></span>

<span data-ttu-id="8ebc8-138">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="8ebc8-138">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="8ebc8-139">`project.assets.json` 文件在使用 PackageReference 管理格式时维护项目的依赖项关系图，用于确保在计算机上安装了所有必需的包。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-139">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="8ebc8-140">由于此文件是通过包还原动态生成的，它通常不添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-140">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="8ebc8-141">因此，该错误在使用工具生成项目时出现，例如，不自动还原包的 `msbuild`。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-141">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="8ebc8-142">在这种情况下，请运行 `msbuild /t:restore`，然后运行 `msbuild`，或使用 `dotnet build`（它会自动还原包）。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-142">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="8ebc8-143">也可以使用[上一节](#missing)中的任一包还原方法。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-143">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="8ebc8-144">由于尚未获得同意，需要还原的一个或多个 NuGet 包无法进行还原</span><span class="sxs-lookup"><span data-stu-id="8ebc8-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="8ebc8-145">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="8ebc8-145">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="8ebc8-146">此错误表示你在 NuGet 配置中禁用了包还原。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-146">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="8ebc8-147">可按照前文[适用于 Visual Studio 用户的快速解决方案](#quick-solution-for-visual-studio-users)中所述来更改 Visual Studio 中的适用设置。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-147">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="8ebc8-148">也可以直接在适用的 `nuget.config` 文件中编辑这些设置（通常，Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-148">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="8ebc8-149">确保将 `packageRestore` 下的 `enabled` 和 `automatic` 键设置为 True：</span><span class="sxs-lookup"><span data-stu-id="8ebc8-149">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="8ebc8-150">如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-150">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="8ebc8-151">其他潜在条件</span><span class="sxs-lookup"><span data-stu-id="8ebc8-151">Other potential conditions</span></span>

- <span data-ttu-id="8ebc8-152">由于缺少文件，你可能会遇到生成错误，并看到提示使用 NuGet 还原来下载它们的消息。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-152">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="8ebc8-153">但是，运行还原时可能会出现：“所有包都已安装，无可还原项。”</span><span class="sxs-lookup"><span data-stu-id="8ebc8-153">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="8ebc8-154">在这种情况下，请删除 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）并再次运行还原。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-154">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="8ebc8-155">如果错误仍然存在，请使用命令行中的 `nuget locals all -clear` 或 `dotnet locals all --clear` 以清除 global-packages 文件夹和缓存文件夹，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-155">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="8ebc8-156">从源代码管理获取项目时，项目文件夹可能设置为只读。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-156">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="8ebc8-157">更改文件夹权限并尝试重新还原包。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-157">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="8ebc8-158">你可能使用了旧版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-158">You may be using an old version of NuGet.</span></span> <span data-ttu-id="8ebc8-159">请访问 [ nuget.org/downloads](https://www.nuget.org/downloads) 了解最新建议版本。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-159">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="8ebc8-160">对于 Visual Studio 2015，建议使用 3.6.0。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-160">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="8ebc8-161">如果遇到其他问题，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们获得更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="8ebc8-161">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>