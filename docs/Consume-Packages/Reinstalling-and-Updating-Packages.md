---
title: 重新安装和更新 NuGet 包 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 有关何时需要重新安装和更新包的详细信息，与 Visual Studio 中损坏的包引用一样。
keywords: NuGet 包安装, NuGet 包重新安装, NuGet 包还原, 更新包, 还原包, 修复损坏的引用
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9da385f51abf5877589c29ebdeffefc9a1a20a2e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-reinstall-and-update-packages"></a><span data-ttu-id="7e50b-104">如何重新安装和更新包</span><span class="sxs-lookup"><span data-stu-id="7e50b-104">How to reinstall and update packages</span></span>

<span data-ttu-id="7e50b-105">[何时重新安装包](#when-to-reinstall-a-package)中描述了大量有关对包的引用可能在 Visual Studio 项目中损坏的情况。</span><span class="sxs-lookup"><span data-stu-id="7e50b-105">There are a number of situations, described below under [When to Reinstall a Package](#when-to-reinstall-a-package), where references to a package might get broken within a Visual Studio project.</span></span> <span data-ttu-id="7e50b-106">在这些情况下，卸载并重新安装同一版本的包会将这些应用还原为正常工作状态。</span><span class="sxs-lookup"><span data-stu-id="7e50b-106">In these cases, uninstalling and then reinstalling the same version of the package will restore those references to working order.</span></span> <span data-ttu-id="7e50b-107">更新包仅意味着安装更新版本，这常常将包还原为正常工作状态。</span><span class="sxs-lookup"><span data-stu-id="7e50b-107">Updating a package simply means installing an updated version, which often restores a package to working order.</span></span>

<span data-ttu-id="7e50b-108">更新和重新安装包按以下方式实现：</span><span class="sxs-lookup"><span data-stu-id="7e50b-108">Updating and reinstalling packages is accomplished as follows:</span></span>

| <span data-ttu-id="7e50b-109">方法</span><span class="sxs-lookup"><span data-stu-id="7e50b-109">Method</span></span> | <span data-ttu-id="7e50b-110">更新</span><span class="sxs-lookup"><span data-stu-id="7e50b-110">Update</span></span> | <span data-ttu-id="7e50b-111">重新安装</span><span class="sxs-lookup"><span data-stu-id="7e50b-111">Reinstall</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e50b-112">包管理器控制台（[使用 Update-Package](#using-update-package) 中所述）</span><span class="sxs-lookup"><span data-stu-id="7e50b-112">Package Manager console (described in [Using Update-Package](#using-update-package))</span></span> | <span data-ttu-id="7e50b-113">`Update-Package` 命令</span><span class="sxs-lookup"><span data-stu-id="7e50b-113">`Update-Package` command</span></span> | <span data-ttu-id="7e50b-114">`Update-Package -reinstall` 命令</span><span class="sxs-lookup"><span data-stu-id="7e50b-114">`Update-Package -reinstall` command</span></span> |
| <span data-ttu-id="7e50b-115">包管理器 UI</span><span class="sxs-lookup"><span data-stu-id="7e50b-115">Package Manager UI</span></span> | <span data-ttu-id="7e50b-116">在“更新”选项卡上，选择一个或多个包并选择“更新”</span><span class="sxs-lookup"><span data-stu-id="7e50b-116">On the **Updates** tab, select one or more packages and select **Update**</span></span> | <span data-ttu-id="7e50b-117">在“已安装”选项卡上，选择一个包，记录其名称，然后选择“卸载”。</span><span class="sxs-lookup"><span data-stu-id="7e50b-117">On the **Installed** tab, select a package, record its name, then select **Uninstall**.</span></span> <span data-ttu-id="7e50b-118">切换到“浏览”选项卡，搜索包名称并选中，然后选择“安装”。</span><span class="sxs-lookup"><span data-stu-id="7e50b-118">Switch to the **Browse** tab, search for the package name, select it, then select **Install**).</span></span> |
| <span data-ttu-id="7e50b-119">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="7e50b-119">nuget.exe CLI</span></span> | <span data-ttu-id="7e50b-120">`nuget update` 命令</span><span class="sxs-lookup"><span data-stu-id="7e50b-120">`nuget update` command</span></span> | <span data-ttu-id="7e50b-121">对于所有包，删除包文件夹，然后运行 `nuget install`。</span><span class="sxs-lookup"><span data-stu-id="7e50b-121">For all packages, delete the package folder, then run `nuget install`.</span></span> <span data-ttu-id="7e50b-122">对于单个包，删除包文件夹并使用 `nuget install <id>` 再安装一个。</span><span class="sxs-lookup"><span data-stu-id="7e50b-122">For a single package, delete the package folder and use `nuget install <id>` to reinstall the same one.</span></span> |

<span data-ttu-id="7e50b-123">本文内容：</span><span class="sxs-lookup"><span data-stu-id="7e50b-123">In this article:</span></span>

- [<span data-ttu-id="7e50b-124">何时重新安装包</span><span class="sxs-lookup"><span data-stu-id="7e50b-124">When to Reinstall a Package</span></span>](#when-to-reinstall-a-package)
- [<span data-ttu-id="7e50b-125">约束升级版本</span><span class="sxs-lookup"><span data-stu-id="7e50b-125">Constraining upgrade versions</span></span>](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a><span data-ttu-id="7e50b-126">何时重新安装包</span><span class="sxs-lookup"><span data-stu-id="7e50b-126">When to Reinstall a Package</span></span>

1. <span data-ttu-id="7e50b-127">**包还原后的损坏引用**：如果已打开项目并还原了 NuGet 包，但仍看见了损坏的引用，请尝试重新安装每个包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-127">**Broken references after package restore**: If you've opened a project and restored NuGet packages, but still see broken references, try reinstalling each of those packages.</span></span>
1. <span data-ttu-id="7e50b-128">**项目因删除文件损坏**：NuGet 不会阻止删除从包添加的项，因此很容易在无意中修改从包安装的内容并损坏项目。</span><span class="sxs-lookup"><span data-stu-id="7e50b-128">**Project is broken due to deleted files**: NuGet does not prevent you from removing items added from packages, so it's easy to inadvertently modify contents installed from a package and break your project.</span></span> <span data-ttu-id="7e50b-129">要还原项目，请重新安装受影响的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-129">To restore the project, reinstall the affected packages.</span></span>
1. <span data-ttu-id="7e50b-130">**包更新损坏了项目**：如果包的更新损坏了项目，则故障通常由可能也已更新的依赖项包引起。</span><span class="sxs-lookup"><span data-stu-id="7e50b-130">**Package update broke the project**: If an update to a package breaks a project, the failure is generally caused by a dependency package which may have also been updated.</span></span> <span data-ttu-id="7e50b-131">要还原依赖项的状态，请重新安装该特定包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-131">To restore the state of the dependency, reinstall that specific package.</span></span>
1. <span data-ttu-id="7e50b-132">**项目重定向或升级**：这在项目已重定向或升级时并且如果包因为更改目标框架需要重新安装时有用。</span><span class="sxs-lookup"><span data-stu-id="7e50b-132">**Project retargeting or upgrade**: This can be useful when a project has been retargeted or upgraded and if the package requires reinstallation due to the change in target framework.</span></span> <span data-ttu-id="7e50b-133">NuGet 在项目重定向后立即显示该情况下的生成错误，后续生成警告会提醒你包可能需要重新安装。</span><span class="sxs-lookup"><span data-stu-id="7e50b-133">NuGet shows a build error in such cases immediately after project retargeting, and subsequent build warnings let you know that the package may need to be reinstalled.</span></span> <span data-ttu-id="7e50b-134">对于项目升级，NuGet 显示项目升级日志中的错误。</span><span class="sxs-lookup"><span data-stu-id="7e50b-134">For project upgrade, NuGet shows an error in the Project Upgrade Log.</span></span>
1. <span data-ttu-id="7e50b-135">**开发期间重新安装包**：包创作者常常需要重新安装与他们开发来测试行为的包版本相同的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-135">**Reinstalling a package during its development**: Package authors often need to reinstall the same version of package they're developing to test the behavior.</span></span> <span data-ttu-id="7e50b-136">`Install-Package` 命令不提供强制重新安装选项，所以换成使用 `Update-Package -reinstall`。</span><span class="sxs-lookup"><span data-stu-id="7e50b-136">The `Install-Package` command does not provide an option to force a reinstall, so use `Update-Package -reinstall` instead.</span></span>

## <a name="constraining-upgrade-versions"></a><span data-ttu-id="7e50b-137">约束升级版本</span><span class="sxs-lookup"><span data-stu-id="7e50b-137">Constraining upgrade versions</span></span>

<span data-ttu-id="7e50b-138">默认情况下，重新安装或更新包常常会安装包源中提供的最新版本。</span><span class="sxs-lookup"><span data-stu-id="7e50b-138">By default, reinstalling or updating a package *always* installs the latest version available from the package source.</span></span>

<span data-ttu-id="7e50b-139">但是，在使用 `packages.config` 管理格式的项目中，可以专门约束版本范围。</span><span class="sxs-lookup"><span data-stu-id="7e50b-139">In projects using the `packages.config` management format, however, you can specifically constrain the version range.</span></span> <span data-ttu-id="7e50b-140">例如，如果知道可能因为包 API 中存在重要更改，应用程序只能使用 1.x 版本的包，而不是 2.0 以及更高版本的包，则需要将升级约束为 1.x 版本。</span><span class="sxs-lookup"><span data-stu-id="7e50b-140">For example, if you know that your application works only with version 1.x of a package but not 2.0 and above, perhaps due to a major change in the package API, then you'd want to constrain upgrades to 1.x versions.</span></span> <span data-ttu-id="7e50b-141">这会阻止可能损坏应用程序的意外更新。</span><span class="sxs-lookup"><span data-stu-id="7e50b-141">This prevents accidental updates that would break the application.</span></span>

<span data-ttu-id="7e50b-142">要设置约束，在文本编辑器中打开 `packages.config`，找到有问题的依赖项，然后添加带版本范围的 `allowedVersions` 属性。</span><span class="sxs-lookup"><span data-stu-id="7e50b-142">To set a constraint, open `packages.config` in a text editor, locate the dependency in question, and add the `allowedVersions` attribute with a version range.</span></span> <span data-ttu-id="7e50b-143">例如，要将更新约束为版本 1.x，请将 `allowedVersions` 设为 `[1,2)`：</span><span class="sxs-lookup"><span data-stu-id="7e50b-143">For example, to constrain updates to version 1.x, set `allowedVersions` to `[1,2)`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

<span data-ttu-id="7e50b-144">在所有情况下，都使用[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="7e50b-144">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-update-package"></a><span data-ttu-id="7e50b-145">使用 Update-Package</span><span class="sxs-lookup"><span data-stu-id="7e50b-145">Using Update-Package</span></span>

<span data-ttu-id="7e50b-146">注意下述的[注意事项](#considerations)，可以使用 Visual Studio 包管理器控制台中的 [Update-Package 命令](../Tools/ps-ref-update-package.md)（“工具” > “NuGet 包管理器” > “包管理器控制台”）轻松重新安装任意包：</span><span class="sxs-lookup"><span data-stu-id="7e50b-146">Being mindful of the [Considerations](#considerations) described below, you can easily reinstall any package using the [Update-Package command](../Tools/ps-ref-update-package.md) in the Visual Studio Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

```ps
Update-Package -Id <package_name> –reinstall
```

<span data-ttu-id="7e50b-147">使用此命令比删除包然后尝试在 NuGet 库中找到同一版本的同一包更加简单。</span><span class="sxs-lookup"><span data-stu-id="7e50b-147">Using this command is much easier than removing a package and then trying to locate the same package in the NuGet gallery with the same version.</span></span> <span data-ttu-id="7e50b-148">请注意，`-Id` 开关是可选的。</span><span class="sxs-lookup"><span data-stu-id="7e50b-148">Note that the `-Id` switch is optional.</span></span>

<span data-ttu-id="7e50b-149">没有 `-reinstall` 更新的相同命令会将包更新为更新的版本（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="7e50b-149">The same command without `-reinstall` updates a package to a newer version, if applicable.</span></span> <span data-ttu-id="7e50b-150">如果有问题的包未安装在项目中，则命令会生成一个错误；即 `Update-Package` 未直接安装包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-150">The command gives an error if the package in question is not already installed in a project; that is, `Update-Package` does not install packages directly.</span></span>

```ps
Update-Package <package_name>
```

<span data-ttu-id="7e50b-151">默认情况下，`Update-Package` 影响解决方案中的所有包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-151">By default, `Update-Package` affects all packages in a solution.</span></span> <span data-ttu-id="7e50b-152">要将操作限制于特定项目，请使用 `-ProjectName` 开关，使用出现在解决方案资源管理器中的项目的名称：</span><span class="sxs-lookup"><span data-stu-id="7e50b-152">To limit the action to a specific project, use the `-ProjectName` switch, using the name of the project as it appears in Solution Explorer:</span></span>

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

<span data-ttu-id="7e50b-153">要更新一个项目中的所有包（或者使用 `-reinstall` 重新安装），请使用 `-ProjectName` 而无需指定任意特定的包：</span><span class="sxs-lookup"><span data-stu-id="7e50b-153">To *update* all packages in a project (or reinstall using `-reinstall`), use `-ProjectName` without specifying any particular package:</span></span>

```ps
Update-Package -ProjectName MyProject
```

<span data-ttu-id="7e50b-154">要更新一个解决方案中的所有包，只需使用 `Update-Package`，无需其他参数或开关。</span><span class="sxs-lookup"><span data-stu-id="7e50b-154">To update all packages in a solution, just use `Update-Package` by itself with no other arguments or switches.</span></span> <span data-ttu-id="7e50b-155">请谨慎使用此窗格，因为它可能需要大量时间来执行所有的更新：</span><span class="sxs-lookup"><span data-stu-id="7e50b-155">Use this form carefully, because it can take considerable time to perform all the updates:</span></span>

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

<span data-ttu-id="7e50b-156">使用 [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) 更新项目或解决方案中的包始终会更新为最新版本的包（不包括预发布包）。</span><span class="sxs-lookup"><span data-stu-id="7e50b-156">Updating packages in a project or solution using [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) always updates to the latest version of the package (excluding pre-release packages).</span></span> <span data-ttu-id="7e50b-157">如果需要，使用 `packages.config` 的项目可以限制更新版本，如下方[约束更新版本](#constraining-upgrade-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="7e50b-157">Projects that use `packages.config` can, if desired, limit update versions as described below in [Constraining upgrade versions](#constraining-upgrade-versions).</span></span>

<span data-ttu-id="7e50b-158">有关命令的完整详细信息，请参阅 [Update-Package](../Tools/ps-ref-update-package.md) 引用。</span><span class="sxs-lookup"><span data-stu-id="7e50b-158">For full details on the command, see the [Update-Package](../Tools/ps-ref-update-package.md) reference.</span></span>

### <a name="considerations"></a><span data-ttu-id="7e50b-159">注意事项</span><span class="sxs-lookup"><span data-stu-id="7e50b-159">Considerations</span></span>

<span data-ttu-id="7e50b-160">重新安装包可能影响以下内容：</span><span class="sxs-lookup"><span data-stu-id="7e50b-160">The following may be affected when reinstalling a package:</span></span>

1. <span data-ttu-id="7e50b-161">**根据项目目标框架重定向重新安装包**</span><span class="sxs-lookup"><span data-stu-id="7e50b-161">**Reinstalling packages according to project target framework retargeting**</span></span>
    - <span data-ttu-id="7e50b-162">在简单的情况下，可以仅使用 `Update-Package –reinstall <package_name>` 重新安装包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-162">In a simple case, just reinstalling a package using `Update-Package –reinstall <package_name>` works.</span></span> <span data-ttu-id="7e50b-163">会卸载根据旧的目标框架安装的包，同时会根据项目的当前目标框架安装相同的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-163">A package that is installed against an old target framework gets uninstalled and the same package gets installed against the current target framework of the project.</span></span>
    - <span data-ttu-id="7e50b-164">在某些情况下，可能会有不支持新目标框架的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-164">In some cases, there may be a package that does not support the new target framework.</span></span>
        - <span data-ttu-id="7e50b-165">如果包支持可移植类库 (PCL) 并且项目重定向到包不再支持的平台组合，则将在重新安装后会失去对包的引用。</span><span class="sxs-lookup"><span data-stu-id="7e50b-165">If a package supports portable class libraries (PCLs) and the project is retargeted to a combination of platforms no longer supported by the package, references to the package will be missing after reinstalling.</span></span>
        - <span data-ttu-id="7e50b-166">这可能会呈现直接使用的包或者作为依赖项安装的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-166">This can surface for packages you're using directly or for packages installed as dependencies.</span></span> <span data-ttu-id="7e50b-167">直接使用的包可能支持新的目标框架，而其依赖项不支持。</span><span class="sxs-lookup"><span data-stu-id="7e50b-167">It's possible for the package you're using directly to support the new target framework while its dependency does not.</span></span>
        - <span data-ttu-id="7e50b-168">如果重定向应用程序后重新安装包导致生成或运行时错误，则可能需要还原目标框架，或者搜索正确支持新目标框架的替换包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-168">If reinstalling packages after retargeting your application results in build or runtime errors, you may need to revert your target framework or search for alternative packages that properly support your new target framework.</span></span>

1. <span data-ttu-id="7e50b-169">**项目重定向或升级后添加到 packages.config 中的 requireReinstallation 属性**</span><span class="sxs-lookup"><span data-stu-id="7e50b-169">**requireReinstallation attribute added in packages.config after project retargeting or upgrade**</span></span>
    - <span data-ttu-id="7e50b-170">如果 NuGet 检测到包受到重定向或升级项目的影响，它会将 `packages.config` 中的 `requireReinstallation="true"` 属性添加到所有受影响的包引用。</span><span class="sxs-lookup"><span data-stu-id="7e50b-170">If NuGet detects that packages were affected by retargeting or upgrading a project, it adds a `requireReinstallation="true"` attribute in  `packages.config` to all affected package references.</span></span> <span data-ttu-id="7e50b-171">因此，Visual Studio 中的每个后续生成会引发这些包的生成警告，提醒你重新安装它们。</span><span class="sxs-lookup"><span data-stu-id="7e50b-171">Because of this, each subsequent build in Visual Studio raises build warnings for those packages so you can remember to reinstall them.</span></span>

1. <span data-ttu-id="7e50b-172">**使用依赖项重新安装包**</span><span class="sxs-lookup"><span data-stu-id="7e50b-172">**Reinstalling packages with dependencies**</span></span>
    - <span data-ttu-id="7e50b-173">`Update-Package –reinstall` 重新安装与初始包相同的版本，但是，如果没有提供特定的版本约束，则安装依赖项的最新版本。</span><span class="sxs-lookup"><span data-stu-id="7e50b-173">`Update-Package –reinstall` reinstalls the same version of the original package, but installs the latest version of dependencies unless specific version constraints are provided.</span></span> <span data-ttu-id="7e50b-174">这样可以按需仅更新依赖项以解决问题。</span><span class="sxs-lookup"><span data-stu-id="7e50b-174">This allows you to update only the dependencies as required to fix an issue.</span></span> <span data-ttu-id="7e50b-175">但是，如果这将依赖项滚动回早期版本，则可以使用 `Update-Package <dependency_name>` 重新安装该依赖项，而不会影响依赖的包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-175">However, if this rolls a dependency back to an earlier version, you can use `Update-Package <dependency_name>` to reinstall that one dependency without affecting the dependent package.</span></span>
    - <span data-ttu-id="7e50b-176">`Update-Package –reinstall <packageName> -ignoreDependencies` 重新安装同一版本的初始包，但不重新安装依赖项。</span><span class="sxs-lookup"><span data-stu-id="7e50b-176">`Update-Package –reinstall <packageName> -ignoreDependencies` reinstalls the same version of the original package but does not reinstall dependencies.</span></span> <span data-ttu-id="7e50b-177">在更新包依赖项时使用可能会导致损坏状态</span><span class="sxs-lookup"><span data-stu-id="7e50b-177">Use this when updating package dependencies might result in a broken state</span></span>

1. <span data-ttu-id="7e50b-178">**涉及依赖版本时重新安装包**</span><span class="sxs-lookup"><span data-stu-id="7e50b-178">**Reinstalling packages when dependent versions are involved**</span></span>
    - <span data-ttu-id="7e50b-179">如上所述，重新安装包不更改依赖它的其他任何已安装包的版本。</span><span class="sxs-lookup"><span data-stu-id="7e50b-179">As explained above, reinstalling a package does not change versions of any other installed packages that depend on it.</span></span> <span data-ttu-id="7e50b-180">然后，重新安装依赖项可能会损坏依赖包。</span><span class="sxs-lookup"><span data-stu-id="7e50b-180">It's possible, then, that reinstalling a dependency could break the dependent package.</span></span>
