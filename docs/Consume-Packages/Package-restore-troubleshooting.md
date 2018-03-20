---
title: "对 Visual Studio 中的 NuGet 包还原进行故障排除 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。"
keywords: "NuGet 包还原, 还原包, 故障排除, 故障排除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="27d55-104">包还原错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="27d55-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="27d55-105">本文着重介绍还原包时遇到的常见错误以及相应的解决步骤。</span><span class="sxs-lookup"><span data-stu-id="27d55-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="27d55-106">有关还原包的完整详细信息，请参阅[包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="27d55-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="27d55-107">如果此处的说明对你没有帮助，[请在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们可以更仔细地检查你的情况。</span><span class="sxs-lookup"><span data-stu-id="27d55-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="27d55-108">请勿使用可能出现在该页面上的“此页面有帮助吗?”控件，</span><span class="sxs-lookup"><span data-stu-id="27d55-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="27d55-109">因为它无法让我们与你联系以获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="27d55-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="27d55-110">适用于 Visual Studio 用户的快速解决方案</span><span class="sxs-lookup"><span data-stu-id="27d55-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="27d55-111">如果使用 Visual Studio，请首先按如下方式启用包还原。</span><span class="sxs-lookup"><span data-stu-id="27d55-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="27d55-112">否则，请继续执行后面的部分。</span><span class="sxs-lookup"><span data-stu-id="27d55-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="27d55-113">选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令。</span><span class="sxs-lookup"><span data-stu-id="27d55-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="27d55-114">在“包还原”下设置这两个选项。</span><span class="sxs-lookup"><span data-stu-id="27d55-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="27d55-115">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="27d55-115">Select **OK**.</span></span>
1. <span data-ttu-id="27d55-116">再次生成项目。</span><span class="sxs-lookup"><span data-stu-id="27d55-116">Build your project again.</span></span>

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="27d55-118">也可以在 `NuGet.config` 文件中更改这些设置；请参阅[同意](#consent)部分。</span><span class="sxs-lookup"><span data-stu-id="27d55-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="27d55-119">此项目引用了此计算机上缺少的 NuGet 程序包</span><span class="sxs-lookup"><span data-stu-id="27d55-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="27d55-120">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="27d55-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="27d55-121">当你尝试生成包含对一个或多个 NuGet 包的引用的项目，但这些包当前未缓存在项目中时，发生了此错误。</span><span class="sxs-lookup"><span data-stu-id="27d55-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="27d55-122">（如果项目使用 `packages.config`，则将包缓存在解决方案根目录的 `packages` 文件夹中；或者如果项目使用 PackageReference 格式，则将其缓存到 `obj/project.assets.json` 文件中。）</span><span class="sxs-lookup"><span data-stu-id="27d55-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="27d55-123">当你从源代码管理或其他下载获得项目的源代码时，通常会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="27d55-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="27d55-124">包通常从源代码管理或下载中省略，因为它们可以从包源（例如 nuget.org）中还原（请参阅[包和源代码管理](Packages-and-Source-Control.md)）。</span><span class="sxs-lookup"><span data-stu-id="27d55-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="27d55-125">否则，包含它们会导致存储库膨胀或创建不必要的大型 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="27d55-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="27d55-126">使用下列方法之一还原包：</span><span class="sxs-lookup"><span data-stu-id="27d55-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="27d55-127">在 Visual Studio 中，通过以下方法启用包还原：选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令，在“包还原”下设置这两个选项，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="27d55-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="27d55-128">然后再次生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="27d55-128">Then build the solution again.</span></span>
- <span data-ttu-id="27d55-129">对于 .NET Core 项目，运行 `dotnet restore` 或 `dotnet build`（它会自动运行还原）。</span><span class="sxs-lookup"><span data-stu-id="27d55-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="27d55-130">在命令行上运行 `nuget restore`（使用 `dotnet` 创建的项目除外，这种情况下请使用 `dotnet restore`）。</span><span class="sxs-lookup"><span data-stu-id="27d55-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="27d55-131">在包含使用 PackageReference 格式的项目的命令行上，运行 `msbuild /t:restore`。</span><span class="sxs-lookup"><span data-stu-id="27d55-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="27d55-132">成功还原后，应会看到 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）。</span><span class="sxs-lookup"><span data-stu-id="27d55-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="27d55-133">该项目现在应能成功生成。</span><span class="sxs-lookup"><span data-stu-id="27d55-133">The project should now build successfully.</span></span> <span data-ttu-id="27d55-134">如果没有，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们跟进。</span><span class="sxs-lookup"><span data-stu-id="27d55-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="27d55-135">找不到资产文件 project.assets.json</span><span class="sxs-lookup"><span data-stu-id="27d55-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="27d55-136">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="27d55-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="27d55-137">此错误出现的原因与[上一部分](#missing)中所述的原因相同，并具有相同的补救措施。</span><span class="sxs-lookup"><span data-stu-id="27d55-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="27d55-138">例如，在从源代码管理获取的 .NET Core 项目上运行 `msbuild` 不会自动还原包。</span><span class="sxs-lookup"><span data-stu-id="27d55-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="27d55-139">在这种情况下，请运行 `msbuild /t:restore`，然后运行 `msbuild`，或使用 `dotnet build`（它会自动还原包）。</span><span class="sxs-lookup"><span data-stu-id="27d55-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="27d55-140">由于尚未获得同意，需要还原的一个或多个 NuGet 包无法进行还原</span><span class="sxs-lookup"><span data-stu-id="27d55-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="27d55-141">完整错误消息：</span><span class="sxs-lookup"><span data-stu-id="27d55-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="27d55-142">此错误表示你在 NuGet 配置中禁用了包还原。</span><span class="sxs-lookup"><span data-stu-id="27d55-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="27d55-143">可按照前文[适用于 Visual Studio 用户的快速解决方案](#quick-solution-for-visual-studio-users)中所述来更改 Visual Studio 中的适用设置。</span><span class="sxs-lookup"><span data-stu-id="27d55-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="27d55-144">也可以直接在适用的 `nuget.config` 文件中编辑这些设置（通常，Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="27d55-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="27d55-145">确保将 `packageRestore` 下的 `enabled` 和 `automatic` 键设置为 True：</span><span class="sxs-lookup"><span data-stu-id="27d55-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="27d55-146">请注意，如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值。</span><span class="sxs-lookup"><span data-stu-id="27d55-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="27d55-147">其他潜在条件</span><span class="sxs-lookup"><span data-stu-id="27d55-147">Other potential conditions</span></span>

- <span data-ttu-id="27d55-148">由于缺少文件，你可能会遇到生成错误，并看到提示使用 NuGet 还原来下载它们的消息。</span><span class="sxs-lookup"><span data-stu-id="27d55-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="27d55-149">但是，运行还原时可能会出现：“所有包都已安装，无可还原项。”</span><span class="sxs-lookup"><span data-stu-id="27d55-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="27d55-150">在这种情况下，请删除 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）并再次运行还原。</span><span class="sxs-lookup"><span data-stu-id="27d55-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="27d55-151">从源代码管理获取项目时，项目文件夹可能设置为只读。</span><span class="sxs-lookup"><span data-stu-id="27d55-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="27d55-152">更改文件夹权限并尝试重新还原包。</span><span class="sxs-lookup"><span data-stu-id="27d55-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="27d55-153">你可能使用了旧版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="27d55-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="27d55-154">请访问 [ nuget.org/downloads](https://www.nuget.org/downloads) 了解最新建议版本。</span><span class="sxs-lookup"><span data-stu-id="27d55-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="27d55-155">对于 Visual Studio 2015，建议使用 3.6.0。</span><span class="sxs-lookup"><span data-stu-id="27d55-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="27d55-156">如果遇到其他问题，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们获得更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="27d55-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>