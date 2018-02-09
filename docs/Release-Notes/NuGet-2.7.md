---
title: "NuGet 2.7 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.7 的发行说明。"
keywords: "NuGet 2.7 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b0e12f7e2cffa6e721dd13c117b7b3727cfcb5d7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-27-release-notes"></a><span data-ttu-id="ba066-104">NuGet 2.7 发行说明</span><span class="sxs-lookup"><span data-stu-id="ba066-104">NuGet 2.7 Release Notes</span></span>

<span data-ttu-id="ba066-105">[NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)</span><span class="sxs-lookup"><span data-stu-id="ba066-105">[NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md)</span></span>

<span data-ttu-id="ba066-106">NuGet 2.7 已于 2013 年 8 月 22 日发布。</span><span class="sxs-lookup"><span data-stu-id="ba066-106">NuGet 2.7 was released on August 22, 2013.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="ba066-107">致谢</span><span class="sxs-lookup"><span data-stu-id="ba066-107">Acknowledgements</span></span>

<span data-ttu-id="ba066-108">我们真诚地感谢以下外部参与者的 NuGet 2.7 进行重大贡献：</span><span class="sxs-lookup"><span data-stu-id="ba066-108">We would like to thank the following external contributors for their significant contributions to NuGet 2.7:</span></span>

1. <span data-ttu-id="ba066-109">[Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))</span><span class="sxs-lookup"><span data-stu-id="ba066-109">[Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))</span></span>
    - <span data-ttu-id="ba066-110">显示许可证 url 时详细列出包和详细级别。</span><span class="sxs-lookup"><span data-stu-id="ba066-110">Show License url when listing packages and verbosity is detailed.</span></span>
1. <span data-ttu-id="ba066-111">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="ba066-111">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="ba066-112">[# 1956年](http://nuget.codeplex.com/workitem/1956)-developmentDependency 将特性添加到`packages.config`和命令中使用它包以仅包括运行时包</span><span class="sxs-lookup"><span data-stu-id="ba066-112">[#1956](http://nuget.codeplex.com/workitem/1956) - Add developmentDependency attribute to `packages.config` and use it in pack command to only include runtime packages</span></span>
1. <span data-ttu-id="ba066-113">[Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))</span><span class="sxs-lookup"><span data-stu-id="ba066-113">[Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))</span></span>
    - <span data-ttu-id="ba066-114">避免 nuget.exe 包命令中的重复属性键。</span><span class="sxs-lookup"><span data-stu-id="ba066-114">Avoid duplicate Properties key in nuget.exe pack command.</span></span>
1. <span data-ttu-id="ba066-115">[Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))</span><span class="sxs-lookup"><span data-stu-id="ba066-115">[Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))</span></span>
    - <span data-ttu-id="ba066-116">[# 2610年](http://nuget.codeplex.com/workitem/2610)-机缓存大小增加到 200。</span><span class="sxs-lookup"><span data-stu-id="ba066-116">[#2610](http://nuget.codeplex.com/workitem/2610) - Increase machine cache size to 200.</span></span>
1. <span data-ttu-id="ba066-117">[Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))</span><span class="sxs-lookup"><span data-stu-id="ba066-117">[Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))</span></span>
    - <span data-ttu-id="ba066-118">[#3217](http://nuget.codeplex.com/workitem/3217) -修复 NuGet 对话框的错误选项卡中显示更新</span><span class="sxs-lookup"><span data-stu-id="ba066-118">[#3217](http://nuget.codeplex.com/workitem/3217) - Fix NuGet dialog showing updates in the wrong tab</span></span>
    - <span data-ttu-id="ba066-119">修复 Project.TargetFramework 可以为 null ProjectManager 中</span><span class="sxs-lookup"><span data-stu-id="ba066-119">Fix Project.TargetFramework can be null in ProjectManager</span></span>
    - <span data-ttu-id="ba066-120">[#3248](http://nuget.codeplex.com/workitem/3248) -修复 SharedPackageRepository FindPackage/FindPackagesById 上不存在 packageId 将失败</span><span class="sxs-lookup"><span data-stu-id="ba066-120">[#3248](http://nuget.codeplex.com/workitem/3248) - Fix SharedPackageRepository FindPackage/FindPackagesById will fail on non-existent packageId</span></span>
1. <span data-ttu-id="ba066-121">[Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))</span><span class="sxs-lookup"><span data-stu-id="ba066-121">[Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))</span></span>
    - <span data-ttu-id="ba066-122">[#3234](http://nuget.codeplex.com/workitem/3234) -启用对 Nomad 项目的支持</span><span class="sxs-lookup"><span data-stu-id="ba066-122">[#3234](http://nuget.codeplex.com/workitem/3234) - Enable support for Nomad project</span></span>
1. <span data-ttu-id="ba066-123">[Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))</span><span class="sxs-lookup"><span data-stu-id="ba066-123">[Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))</span></span>
    - <span data-ttu-id="ba066-124">[#3252](http://nuget.codeplex.com/workitem/3252) -修复推送命令将会失败，退出代码 0，当文件不存在。</span><span class="sxs-lookup"><span data-stu-id="ba066-124">[#3252](http://nuget.codeplex.com/workitem/3252) - Fix push command fails with exit code 0 when file doesn't exist.</span></span>
1. [<span data-ttu-id="ba066-125">Martin Veselý</span><span class="sxs-lookup"><span data-stu-id="ba066-125">Martin Veselý</span></span>](http://www.codeplex.com/site/users/view/veselkamartin)
    - <span data-ttu-id="ba066-126">[#3226](http://nuget.codeplex.com/workitem/3226) -使用项目引用数据库项目时添加 BindingRedirect 命令修复 bug。</span><span class="sxs-lookup"><span data-stu-id="ba066-126">[#3226](http://nuget.codeplex.com/workitem/3226) - Fix bug with Add-BindingRedirect command when a project references a database project.</span></span>
1. <span data-ttu-id="ba066-127">[Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="ba066-127">[Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="ba066-128">[# 2891年](http://nuget.codeplex.com/workitem/2891)-修复 bug 的 nuget.pack 错误地解析排除属性中的通配符。</span><span class="sxs-lookup"><span data-stu-id="ba066-128">[#2891](http://nuget.codeplex.com/workitem/2891) - Fix bug of nuget.pack parsing wildcard in the 'exclude' attribute incorrectly.</span></span>
1. <span data-ttu-id="ba066-129">[Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))</span><span class="sxs-lookup"><span data-stu-id="ba066-129">[Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))</span></span>
    - <span data-ttu-id="ba066-130">[#3307](http://nuget.codeplex.com/workitem/3307) -修复 bug`NuGet.targets`未通过 $(Platform) 到 nuget.exe 还原包时。</span><span class="sxs-lookup"><span data-stu-id="ba066-130">[#3307](http://nuget.codeplex.com/workitem/3307) - Fix bug `NuGet.targets` does not pass $(Platform) to nuget.exe when restoring packages.</span></span>
1. [<span data-ttu-id="ba066-131">Brian Federici</span><span class="sxs-lookup"><span data-stu-id="ba066-131">Brian Federici</span></span>](http://www.codeplex.com/site/users/view/benerdin)
    - <span data-ttu-id="ba066-132">[#3294](http://nuget.codeplex.com/workitem/3294) -这将允许将具有相同名称但不同大小写，最终导致"项已存在"异常的文件添加 nuget.exe 包命令中的修复 bug。</span><span class="sxs-lookup"><span data-stu-id="ba066-132">[#3294](http://nuget.codeplex.com/workitem/3294) - Fix bug in nuget.exe package command which would allow adding files with the same name but different casing, eventually causing "Item already exists" exception.</span></span>
1. <span data-ttu-id="ba066-133">[Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))</span><span class="sxs-lookup"><span data-stu-id="ba066-133">[Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))</span></span>
    - <span data-ttu-id="ba066-134">[# 2990年](http://nuget.codeplex.com/workitem/2990)-NetPortableProfile 类添加版本属性。</span><span class="sxs-lookup"><span data-stu-id="ba066-134">[#2990](http://nuget.codeplex.com/workitem/2990) - Add Version property to NetPortableProfile class.</span></span>
1. [<span data-ttu-id="ba066-135">David Simner</span><span class="sxs-lookup"><span data-stu-id="ba066-135">David Simner</span></span>](https://www.codeplex.com/site/users/view/DavidSimner)
    - <span data-ttu-id="ba066-136">[#3460](https://nuget.codeplex.com/workitem/3460) -如果修复 bug NullReferenceException requireApiKey = true，但标头 X NUGET APIKEY 不存在</span><span class="sxs-lookup"><span data-stu-id="ba066-136">[#3460](https://nuget.codeplex.com/workitem/3460) - Fix bug NullReferenceException if requireApiKey = true, but the header X-NUGET-APIKEY isn't present</span></span>
1. <span data-ttu-id="ba066-137">[Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))</span><span class="sxs-lookup"><span data-stu-id="ba066-137">[Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))</span></span>
    - <span data-ttu-id="ba066-138">[#3278](https://nuget.codeplex.com/workitem/3278) -修复 NuGet.Build 目标文件到，以便它新平台上正常工作 MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="ba066-138">[#3278](https://nuget.codeplex.com/workitem/3278) - Fixes NuGet.Build targets file to so that it works correctly on MonoDevelop</span></span>
1. <span data-ttu-id="ba066-139">[Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))</span><span class="sxs-lookup"><span data-stu-id="ba066-139">[Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))</span></span>
    - <span data-ttu-id="ba066-140">通过增加并行化提高还原命令性能</span><span class="sxs-lookup"><span data-stu-id="ba066-140">Improve Restore command performance by increasing parallelization</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="ba066-141">发行版中的值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="ba066-141">Notable features in the release</span></span>

### <a name="package-restore-by-default-with-implicit-consent"></a><span data-ttu-id="ba066-142">默认情况下，（具有隐式同意） 的程序包还原</span><span class="sxs-lookup"><span data-stu-id="ba066-142">Package Restore by Default (with implicit consent)</span></span>

<span data-ttu-id="ba066-143">NuGet 2.7 引入了一种新方法来打包还原，并且还克服了主要障碍： 现在，包还原同意默认情况下处于启用 ！</span><span class="sxs-lookup"><span data-stu-id="ba066-143">NuGet 2.7 introduces a new approach to package restore, and also overcomes a major hurdle: Package restore consent is now on by default!</span></span> <span data-ttu-id="ba066-144">新的方法和隐式同意的组合将极大地简化包还原方案。</span><span class="sxs-lookup"><span data-stu-id="ba066-144">The combination of the new approach and the implicit consent will drastically simplify package restore scenarios.</span></span>

#### <a name="implicit-consent"></a><span data-ttu-id="ba066-145">隐式同意</span><span class="sxs-lookup"><span data-stu-id="ba066-145">Implicit Consent</span></span>

<span data-ttu-id="ba066-146">使用 NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6，用户需要显式允许 NuGet 下载缺少的程序包期间生成。</span><span class="sxs-lookup"><span data-stu-id="ba066-146">With NuGet versions 2.0, 2.1, 2.2, 2.5, and 2.6, users needed to explicitly allow NuGet to download missing packages during build.</span></span> <span data-ttu-id="ba066-147">如果此许可实际上并没有显式授予，则必须启用程序包还原的解决方案将无法生成，直至用户具有向授予许可。</span><span class="sxs-lookup"><span data-stu-id="ba066-147">If this consent had not been explicitly given, then solutions that had enabled package restore would fail to build until the user had granted consent.</span></span>

<span data-ttu-id="ba066-148">从 NuGet 2.7 开始，包还原同意的情况下为 ON 默认情况下同时显式允许用户*选择退出*的程序包还原，如果需要，使用 Visual Studio 中的 NuGet 的设置中的复选框。</span><span class="sxs-lookup"><span data-stu-id="ba066-148">Starting with NuGet 2.7, package restore consent is ON by default while allowing users to explicitly *opt out* of package restore if desired, using the checkbox in NuGet's settings in Visual Studio.</span></span> <span data-ttu-id="ba066-149">隐式同意此更改影响 NuGet 在以下环境：</span><span class="sxs-lookup"><span data-stu-id="ba066-149">This change for implicit consent affects NuGet in the following environments:</span></span>

* <span data-ttu-id="ba066-150">Visual Studio 2013 预览版</span><span class="sxs-lookup"><span data-stu-id="ba066-150">Visual Studio 2013 Preview</span></span>
* <span data-ttu-id="ba066-151">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ba066-151">Visual Studio 2012</span></span>
* <span data-ttu-id="ba066-152">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="ba066-152">Visual Studio 2010</span></span>
* <span data-ttu-id="ba066-153">nuget.exe 命令行实用工具</span><span class="sxs-lookup"><span data-stu-id="ba066-153">nuget.exe Command-Line Utility</span></span>

#### <a name="automatic-package-restore-in-visual-studio"></a><span data-ttu-id="ba066-154">Visual Studio 中的包自动还原</span><span class="sxs-lookup"><span data-stu-id="ba066-154">Automatic Package Restore in Visual Studio</span></span>

<span data-ttu-id="ba066-155">从 NuGet 2.7 开始，NuGet 将自动下载缺少的程序包在 Visual Studio 中，在生成期间即使程序包还原尚未显式启用解决方案。</span><span class="sxs-lookup"><span data-stu-id="ba066-155">Starting with NuGet 2.7, NuGet will automatically download missing packages during build in Visual Studio, even if package restore hasn't been explicitly enabled for the solution.</span></span> <span data-ttu-id="ba066-156">此自动包还原发生在 Visual Studio 中，在生成项目或解决方案，但之前调用 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="ba066-156">This Automatic Package Restore happens in Visual Studio when you build a project or the solution, but before MSBuild is invoked.</span></span> <span data-ttu-id="ba066-157">这将生成几个明显的好处：</span><span class="sxs-lookup"><span data-stu-id="ba066-157">This yields a few significant benefits:</span></span>

1. <span data-ttu-id="ba066-158">不再需要对解决方案中使用"启用 NuGet 包还原"笔势</span><span class="sxs-lookup"><span data-stu-id="ba066-158">No further need to use the "Enable NuGet Package Restore" gesture on your solution</span></span>
1. <span data-ttu-id="ba066-159">项目无需进行修改，NuGet 不会对你的项目以确保启用程序包还原进行更改</span><span class="sxs-lookup"><span data-stu-id="ba066-159">Projects don't need to be modified, and NuGet won't make changes to your project to ensure package restore is enabled</span></span>
1. <span data-ttu-id="ba066-160">将还原所有 NuGet 包，包括那些包含 MSBuild 属性中的目标文件的导入*之前*调用 MSBuild 时，确保这些属性/目标正确识别生成过程</span><span class="sxs-lookup"><span data-stu-id="ba066-160">All NuGet packages, including those that included MSBuild imports for props/targets files, will be restored *before* MSBuild is invoked, ensuring those props/targets are properly recognized during the build</span></span>

<span data-ttu-id="ba066-161">若要在 Visual Studio 中使用自动程序包还原，只需执行一个操作 （中）：</span><span class="sxs-lookup"><span data-stu-id="ba066-161">In order to use Automatic Package Restore in Visual Studio, you only need to take one (in)action:</span></span>

1. <span data-ttu-id="ba066-162">未签入你`packages`文件夹</span><span class="sxs-lookup"><span data-stu-id="ba066-162">Don't check in your `packages` folder</span></span>

<span data-ttu-id="ba066-163">有几种方法忽略你`packages`从源代码管理文件夹。</span><span class="sxs-lookup"><span data-stu-id="ba066-163">There are several ways to omit your `packages` folder from source control.</span></span> <span data-ttu-id="ba066-164">有关详细信息，请参阅[包和源控件](../consume-packages/packages-and-source-control.md)主题。</span><span class="sxs-lookup"><span data-stu-id="ba066-164">For more information, see the [Packages and Source Control](../consume-packages/packages-and-source-control.md) topic.</span></span>

<span data-ttu-id="ba066-165">当所有用户隐式选择了参加自动包还原同意的情况下，你可以轻松地选择退出计划通过 Visual Studio 中的包管理器设置。</span><span class="sxs-lookup"><span data-stu-id="ba066-165">While all users are implicitly opted into Automatic Package Restore consent, you can easily opt out through the Package Manager settings in Visual Studio.</span></span>

![程序包管理器设置](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a><span data-ttu-id="ba066-167">从命令行的简化的程序包还原</span><span class="sxs-lookup"><span data-stu-id="ba066-167">Simplified Package Restore from the Command-Line</span></span>

<span data-ttu-id="ba066-168">NuGet 2.7 引入 nuget.exe 的新功能：`nuget.exe restore`</span><span class="sxs-lookup"><span data-stu-id="ba066-168">NuGet 2.7 introduces a new feature for nuget.exe: `nuget.exe restore`</span></span>

<span data-ttu-id="ba066-169">此新的 Restore 命令允许你轻松地通过接受的解决方案文件或文件夹作为自变量来还原使用单个命令，解决方案的所有包。</span><span class="sxs-lookup"><span data-stu-id="ba066-169">This new Restore command allows you to easily restore all packages for a solution with a single command, by accepting a solution file or folder as an argument.</span></span> <span data-ttu-id="ba066-170">此外，在当前文件夹中没有单个解决方案时，会进行隐式该自变量。</span><span class="sxs-lookup"><span data-stu-id="ba066-170">Furthermore, that argument is implied when there's only a single solution in the current folder.</span></span> <span data-ttu-id="ba066-171">这意味着所有以下各项工作从包含单个解决方案文件 (MySolution.sln) 的文件夹：</span><span class="sxs-lookup"><span data-stu-id="ba066-171">That means the following all work from a folder that contains a single solution file (MySolution.sln):</span></span>

1. <span data-ttu-id="ba066-172">nuget.exe restore MySolution.sln</span><span class="sxs-lookup"><span data-stu-id="ba066-172">nuget.exe restore MySolution.sln</span></span>
1. <span data-ttu-id="ba066-173">nuget.exe 还原。</span><span class="sxs-lookup"><span data-stu-id="ba066-173">nuget.exe restore .</span></span>
1. <span data-ttu-id="ba066-174">nuget.exe 还原</span><span class="sxs-lookup"><span data-stu-id="ba066-174">nuget.exe restore</span></span>

<span data-ttu-id="ba066-175">Restore 命令将打开的解决方案文件并找到解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="ba066-175">The Restore command will open the solution file and find all projects within the solution.</span></span> <span data-ttu-id="ba066-176">在这里，它将查找`packages.config`为每个项目和还原的所有包找到的文件。</span><span class="sxs-lookup"><span data-stu-id="ba066-176">From there, it will find the `packages.config` files for each of the projects and restore all of the packages found.</span></span> <span data-ttu-id="ba066-177">它还将还原的解决方案级包中找到`.nuget\packages.config`文件。</span><span class="sxs-lookup"><span data-stu-id="ba066-177">It also restores solution-level packages found in the `.nuget\packages.config` file.</span></span> <span data-ttu-id="ba066-178">有关新的 Restore 命令的详细信息可在[命令行参考](../tools/cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ba066-178">More information about the new Restore command can be found in the [Command-Line Reference](../tools/cli-ref-restore.md).</span></span>

#### <a name="the-new-package-restore-workflow"></a><span data-ttu-id="ba066-179">新的包还原工作流</span><span class="sxs-lookup"><span data-stu-id="ba066-179">The New Package Restore Workflow</span></span>

<span data-ttu-id="ba066-180">很高兴有关这些更改对包还原，因为它引入了新的工作流。</span><span class="sxs-lookup"><span data-stu-id="ba066-180">We are excited about these changes to Package Restore, as it introduces a new workflow.</span></span> <span data-ttu-id="ba066-181">如果你想要忽略从源代码管理包你只需不要分配出`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="ba066-181">If you want to omit your packages from source control you simply don't commit the `packages` folder.</span></span> <span data-ttu-id="ba066-182">打开并生成解决方案的 visual Studio 用户会自动还原的包。</span><span class="sxs-lookup"><span data-stu-id="ba066-182">Visual Studio users who open and build the solution will see the packages automatically restored.</span></span> <span data-ttu-id="ba066-183">对于命令行生成，只需调用`nuget.exe restore`之前调用`msbuild`。</span><span class="sxs-lookup"><span data-stu-id="ba066-183">For command-line builds, simply invoke `nuget.exe restore` before invoking `msbuild`.</span></span> <span data-ttu-id="ba066-184">你将不再需要请记得对解决方案，使用"启用 NuGet 包还原"笔势，我们将不再需要修改你的项目以 alter 生成。</span><span class="sxs-lookup"><span data-stu-id="ba066-184">You'll no longer need to remember to use the "Enable NuGet Package Restore" gesture on your solution, and we'll no longer need to modify your projects to alter the build.</span></span> <span data-ttu-id="ba066-185">这还会生成包含 MSBuild 的导入，尤其是通过 NuGet 的最新功能添加导入的包提供大大提高的体验和[自动导入属性/目标文件](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ba066-185">And this also yields a much improved experience for packages that include MSBuild imports, especially for imports added through NuGet's recent feature for [automatically importing props/targets files](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) from the \build folder.</span></span>

<span data-ttu-id="ba066-186">除了我们已完成自己工作，我们还致力于与某些重要的合作伙伴，为了使这种新方法。我们不是具体的时间线为其中的任何未知的但每个伙伴是因为我们有关新的方法非常高兴。</span><span class="sxs-lookup"><span data-stu-id="ba066-186">In addition to the work we've done ourselves, we're also working with some important partners to round this new approach out. We don't have concrete timelines for any of these yet, but each partner is as excited as we are about the new approach.</span></span>

* <span data-ttu-id="ba066-187">Team Foundation Service-它们正在努力将集成到调用`nuget.exe restore`到默认值生成方案。</span><span class="sxs-lookup"><span data-stu-id="ba066-187">Team Foundation Service - They are working to integrate the call to `nuget.exe restore` into the default build scenarios.</span></span>
* <span data-ttu-id="ba066-188">Windows Azure 网站-它们正在努力，可以将你的项目推送到 Azure，并且具有`nuget.exe restore`调用之前生成您的网站。</span><span class="sxs-lookup"><span data-stu-id="ba066-188">Windows Azure Web Sites - They are working to allow you to push your project to Azure and have `nuget.exe restore` called before your web site is built.</span></span>
* <span data-ttu-id="ba066-189">TeamCity-它们正在更新以其 NuGet 安装程序插件获得 TeamCity 8.x</span><span class="sxs-lookup"><span data-stu-id="ba066-189">TeamCity - They are updating their NuGet Installer plugin for TeamCity 8.x</span></span>
* <span data-ttu-id="ba066-190">他们正在处理 AppHarbor-若要允许您将你的存储库推送到 AppHarbor 并使`nuget.exe restore`生成你的解决方案之前调用。</span><span class="sxs-lookup"><span data-stu-id="ba066-190">AppHarbor - They are working to allow you to push your repo to AppHarbor and have `nuget.exe restore` called before your solution is build.</span></span>

<span data-ttu-id="ba066-191">与每个上述伙伴，它们将使用其自己的 nuget.exe 的副本并不需要执行 nuget.exe 解决方案中。</span><span class="sxs-lookup"><span data-stu-id="ba066-191">With each of the partners above, they would use their own copy of nuget.exe and you would not need to carry nuget.exe in your solution.</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ba066-192">已知问题</span><span class="sxs-lookup"><span data-stu-id="ba066-192">Known Issues</span></span>

<span data-ttu-id="ba066-193">出现了两个已知的问题 nuget.exe 还原初始 2.7 版本中，但它们已固定到更新的 9/6/2013年上[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)。</span><span class="sxs-lookup"><span data-stu-id="ba066-193">There were two known issues with nuget.exe restore with the initial 2.7 release, but they were fixed on 9/6/2013 with an update to the [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/).</span></span>  <span data-ttu-id="ba066-194">此更新，还可以在[NuGet 2.7 下载页](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。</span><span class="sxs-lookup"><span data-stu-id="ba066-194">This update is also available on the [NuGet 2.7 download page](https://nuget.codeplex.com/releases/view/107605) on CodePlex.</span></span>  <span data-ttu-id="ba066-195">运行`nuget.exe update -self`将更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="ba066-195">Running `nuget.exe update -self` will update to the latest release.</span></span>

<span data-ttu-id="ba066-196">固定了：</span><span class="sxs-lookup"><span data-stu-id="ba066-196">The fixed were:</span></span>

1. [<span data-ttu-id="ba066-197">使用 SLN 文件时，新的程序包还原不能在 Mono</span><span class="sxs-lookup"><span data-stu-id="ba066-197">New package restore doesn't work on Mono when using SLN file</span></span>](https://nuget.codeplex.com/workitem/3596)
1. [<span data-ttu-id="ba066-198">新的程序包还原不能使用 Wix 项目</span><span class="sxs-lookup"><span data-stu-id="ba066-198">New package restore doesn't work with Wix projects</span></span>](https://nuget.codeplex.com/workitem/3598)

<span data-ttu-id="ba066-199">此外，还有新的包还原工作流的已知的问题，由此[自动包还原并不适用于解决方案文件夹下的项目](https://nuget.codeplex.com/workitem/3625)。</span><span class="sxs-lookup"><span data-stu-id="ba066-199">There is also a known issue with the new package restore workflow whereby [Automatic Package Restore does not work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625).</span></span> <span data-ttu-id="ba066-200">在 NuGet 2.7.1 中进行了修复此问题。</span><span class="sxs-lookup"><span data-stu-id="ba066-200">This issue was fixed in NuGet 2.7.1.</span></span>

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a><span data-ttu-id="ba066-201">项目重定目标和升级生成错误/警告</span><span class="sxs-lookup"><span data-stu-id="ba066-201">Project Retargeting and Upgrade Build Errors/Warnings</span></span>

<span data-ttu-id="ba066-202">多次重定目标或升级你的项目之后, 你找到一些 NuGet 程序包不正常。</span><span class="sxs-lookup"><span data-stu-id="ba066-202">Many times after retargeting or upgrading your project, you find that some NuGet packages aren't functioning properly.</span></span> <span data-ttu-id="ba066-203">遗憾的是，没有这不会指示，然后不提供的指导上没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="ba066-203">Unfortunately, there is no indication of this and then there's no guidance on how to address it.</span></span> <span data-ttu-id="ba066-204">使用 NuGet 2.7，我们现在使用某些 Visual Studio 事件识别已重定目标或升级而影响你已安装的 NuGet 包中的项目时。</span><span class="sxs-lookup"><span data-stu-id="ba066-204">With NuGet 2.7, we now use some Visual Studio events to recognize when you've retargeted or upgraded your project in a way that affects your installed NuGet packages.</span></span>

<span data-ttu-id="ba066-205">如果我们检测到的任何你的包已受重定目标或升级，我们将生成立即生成错误，告知你。</span><span class="sxs-lookup"><span data-stu-id="ba066-205">If we detect that any of your packages were affected by the retargeting or upgrade, we'll produce immediate build errors to let you know.</span></span> <span data-ttu-id="ba066-206">除了立即生成错误，我们还保留`requireReinstallation="true"`中标记出来。 你`packages.config`文件适用于 Visual Studio 中的所有程序包都是受影响的重定目标，并且每个后续都生成将会引发这些包的都生成警告。</span><span class="sxs-lookup"><span data-stu-id="ba066-206">In addition to the immediate build error, we also persist a `requireReinstallation="true"` flag in your `packages.config` file for all packages that were affected by the retargeting, and each subsequent build in Visual Studio will raise build warnings for those packages.</span></span>

<span data-ttu-id="ba066-207">尽管 NuGet 无法执行自动操作以重新安装受影响的包，我们希望这种指示和警告将指导帮助您发现何时需要重新安装包。</span><span class="sxs-lookup"><span data-stu-id="ba066-207">Although NuGet cannot take automatic action to reinstall affected packages, we hope this indication and warning will guide help you discover when you need to reinstall packages.</span></span> <span data-ttu-id="ba066-208">我们还致力于[包重新安装指南文档](../consume-packages/reinstalling-and-updating-packages.md)这些错误消息将定向到你。</span><span class="sxs-lookup"><span data-stu-id="ba066-208">We are also working on [package reinstallation guidance documentation](../consume-packages/reinstalling-and-updating-packages.md) that these error messages direct you to.</span></span>

### <a name="nuget-configuration-defaults"></a><span data-ttu-id="ba066-209">NuGet 配置默认值</span><span class="sxs-lookup"><span data-stu-id="ba066-209">NuGet Configuration Defaults</span></span>

<span data-ttu-id="ba066-210">许多公司内部，使用 NuGet，但有引导其开发人员可以使用内部包源，而不是 nuget.org 硬时间。NuGet 2.7 引入了一种允许计算机范围的默认值为指定的配置默认值功能：</span><span class="sxs-lookup"><span data-stu-id="ba066-210">Many companies are using NuGet internally, but have had a hard time guiding their developers to use internal package sources instead of nuget.org. NuGet 2.7 introduces a Configuration Defaults feature that allows machine-wide defaults to be specified for:</span></span>

1. <span data-ttu-id="ba066-211">已启用的程序包源</span><span class="sxs-lookup"><span data-stu-id="ba066-211">Enabled package sources</span></span>
1. <span data-ttu-id="ba066-212">已注册，但已禁用的包源</span><span class="sxs-lookup"><span data-stu-id="ba066-212">Registered, but disabled package sources</span></span>
1. <span data-ttu-id="ba066-213">默认 nuget.exe 推送源</span><span class="sxs-lookup"><span data-stu-id="ba066-213">The default nuget.exe push source</span></span>

<span data-ttu-id="ba066-214">其中每个现在可以配置在一个文件位于内`%ProgramData%\NuGet\NuGetDefaults.Config`。</span><span class="sxs-lookup"><span data-stu-id="ba066-214">Each of these can now be configured within a file located at `%ProgramData%\NuGet\NuGetDefaults.Config`.</span></span> <span data-ttu-id="ba066-215">如果此配置文件指定包源，则将不会自动注册的默认 nuget.org 包源中与的`NuGetDefaults.Config`将改为注册。</span><span class="sxs-lookup"><span data-stu-id="ba066-215">If this config file specifies package sources, then the default nuget.org package source will not be registered automatically, and the ones in `NuGetDefaults.Config` will be registered instead.</span></span>

<span data-ttu-id="ba066-216">虽然不需要使用此功能，我们预期公司部署`NuGetDefaults.Config`使用组策略文件。</span><span class="sxs-lookup"><span data-stu-id="ba066-216">While not required to use this feature, we expect companies to deploy `NuGetDefaults.Config` files using Group Policy.</span></span>

<span data-ttu-id="ba066-217">*请注意，此功能将永远不会导致包源以为从开发人员 NuGet 设置中删除。这意味着如果开发人员已使用 NuGet，并因此具有 nuget.org 包源注册，它也不会删除创建后`NuGetDefaults.Config`文件。*</span><span class="sxs-lookup"><span data-stu-id="ba066-217">*Note that this feature will never cause a package source to be removed from a developer's NuGet settings. That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.*</span></span>

<span data-ttu-id="ba066-218">请参阅[NuGet 配置的默认值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)有关此功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ba066-218">See [NuGet Configuration Defaults](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) for more information about this feature.</span></span>

### <a name="renaming-the-default-package-source"></a><span data-ttu-id="ba066-219">重命名默认的程序包源</span><span class="sxs-lookup"><span data-stu-id="ba066-219">Renaming the Default Package Source</span></span>

<span data-ttu-id="ba066-220">NuGet 始终注册了名为"NuGet 正式程序包源"，指向 nuget.org 一个默认包源。该名称详细，且它还未指定实际上指向。</span><span class="sxs-lookup"><span data-stu-id="ba066-220">NuGet has always registered a default package source called "NuGet official package source" that points to nuget.org. That name was verbose and it also didn't specify where it was actually pointing.</span></span> <span data-ttu-id="ba066-221">若要解决这些两个问题，我们已重命名只需"nuget.org"在 UI 中为此包源。</span><span class="sxs-lookup"><span data-stu-id="ba066-221">To address those two issues, we've renamed this package source to simply "nuget.org" in the UI.</span></span> <span data-ttu-id="ba066-222">包源的 URL 也进行了更改以包括"www"。</span><span class="sxs-lookup"><span data-stu-id="ba066-222">The URL for the package source was also changed to include the "www."</span></span> <span data-ttu-id="ba066-223">前缀。</span><span class="sxs-lookup"><span data-stu-id="ba066-223">prefix.</span></span> <span data-ttu-id="ba066-224">使用 NuGet 2.7 之后, 你现有的"NuGet 正式程序包源"将自动更新到"nuget.org"作为其名称和"https://www.nuget.org/api/v2/"作为其 URL。</span><span class="sxs-lookup"><span data-stu-id="ba066-224">After using NuGet 2.7, your existing "NuGet official package source" will automatically be updated to "nuget.org" as its name and "https://www.nuget.org/api/v2/" as its URL.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="ba066-225">性能改进</span><span class="sxs-lookup"><span data-stu-id="ba066-225">Performance Improvements</span></span>

<span data-ttu-id="ba066-226">我们在 2.7 其会生成较小的内存需求量、 更少的磁盘使用情况和更快的包安装进行了一些性能改进。</span><span class="sxs-lookup"><span data-stu-id="ba066-226">We made some performance improvement in 2.7 which will yield smaller memory footprint, less disk usage and faster package installation.</span></span> <span data-ttu-id="ba066-227">我们还对基于 OData 的源，这将减少总体负载进行了更智能的查询。</span><span class="sxs-lookup"><span data-stu-id="ba066-227">We also made smarter queries to OData-based feeds which will reduce the overall payload.</span></span>

### <a name="new-extensibility-apis"></a><span data-ttu-id="ba066-228">新扩展性 Api</span><span class="sxs-lookup"><span data-stu-id="ba066-228">New Extensibility APIs</span></span>

<span data-ttu-id="ba066-229">我们将一些新 Api 添加到我们的扩展性服务以填充的缺少的功能在早期版本的差距。</span><span class="sxs-lookup"><span data-stu-id="ba066-229">We added some new APIs to our extensibility services to fill the gap of missing functionalities in previous releases.</span></span>

#### <a name="ivspackageinstallerservices"></a><span data-ttu-id="ba066-230">IVsPackageInstallerServices</span><span class="sxs-lookup"><span data-stu-id="ba066-230">IVsPackageInstallerServices</span></span>

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a><span data-ttu-id="ba066-231">IVsPackageInstaller</span><span class="sxs-lookup"><span data-stu-id="ba066-231">IVsPackageInstaller</span></span>

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a><span data-ttu-id="ba066-232">仅限开发的依赖关系</span><span class="sxs-lookup"><span data-stu-id="ba066-232">Development-Only Dependencies</span></span>

<span data-ttu-id="ba066-233">此功能由提供[Adam Ralph](https://twitter.com/adamralph)并且它允许程序包作者以声明依赖项仅在开发使用时间，而不需要包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ba066-233">This feature was contributed by [Adam Ralph](https://twitter.com/adamralph) and it allows package authors to declare dependencies that were only used at development time and don't require package dependencies.</span></span> <span data-ttu-id="ba066-234">通过添加`developmentDependency="true"`到中的包属性`packages.config`，`nuget.exe pack`不再包括作为依赖项包。</span><span class="sxs-lookup"><span data-stu-id="ba066-234">By adding a `developmentDependency="true"` attribute to a package in `packages.config`, `nuget.exe pack` will no longer include that package as a dependency.</span></span>

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a><span data-ttu-id="ba066-235">删除 Visual Studio 2010 Express 适用于 Windows Phone 支持</span><span class="sxs-lookup"><span data-stu-id="ba066-235">Removed Support for Visual Studio 2010 Express for Windows Phone</span></span>

<span data-ttu-id="ba066-236">2.7 中的新包还原模型由新 VSPackage 不同于主要的 NuGet VSPackage 的实现。</span><span class="sxs-lookup"><span data-stu-id="ba066-236">The new package restore model in 2.7 is implemented by a new VSPackage which is different from the main NuGet VSPackage.</span></span> <span data-ttu-id="ba066-237">由于技术问题，此新 VSPackage 不正确在适用*Visual Studio 2010 Express 为 Windows Phone* SKU 为我们共享相同的基本代码与其他支持 Visual Studio Sku。</span><span class="sxs-lookup"><span data-stu-id="ba066-237">Due to a technical issue, this new VSPackage doesn't work correctly in the *Visual Studio 2010 Express for Windows Phone* SKU as we share the same code base with other supported Visual Studio SKUs.</span></span> <span data-ttu-id="ba066-238">因此，从 NuGet 2.7 开始，我们删除支持*Visual Studio 2010 Express 为 Windows Phone*来自已发布的扩展插件。</span><span class="sxs-lookup"><span data-stu-id="ba066-238">Therefore, starting with NuGet 2.7, we are dropping support for *Visual Studio 2010 Express for Windows Phone* from the published extension.</span></span> <span data-ttu-id="ba066-239">支持*Visual Studio 2010 Express for Web*仍包含在主扩展发布到 Visual Studio 扩展库中。</span><span class="sxs-lookup"><span data-stu-id="ba066-239">Support for *Visual Studio 2010 Express for Web* is still included in the primary extension published to the Visual Studio Extension Gallery.</span></span>

<span data-ttu-id="ba066-240">因为我们不确定如何许多开发人员仍在使用该版本/版本的 Visual Studio 中 NuGet，我们发布专门为这些用户单独的 Visual Studio 扩展和发布上 CodePlex （而不是 Visual Studio 扩展库）.</span><span class="sxs-lookup"><span data-stu-id="ba066-240">Since we are unsure how many developers are still using NuGet in that version/edition of Visual Studio, we are publishing a separate Visual Studio extension specifically for those users and publishing it on CodePlex (rather than the Visual Studio Extension Gallery).</span></span> <span data-ttu-id="ba066-241">我们不打算继续保持该扩展，但如果这会影响你通过在 CodePlex 上填写问题来请让我们知道。</span><span class="sxs-lookup"><span data-stu-id="ba066-241">We don't plan to continue to maintain that extension, but if this affects you please let us know by filing an issue on CodePlex.</span></span>

<span data-ttu-id="ba066-242">若要下载 NuGet 包管理器 （Visual Studio 2010 Express 为 Windows Phone)，请访问[NuGet 2.7 下载](https://nuget.codeplex.com/releases/view/107605)页。</span><span class="sxs-lookup"><span data-stu-id="ba066-242">To download the NuGet Package Manager (for Visual Studio 2010 Express for Windows Phone), visit the [NuGet 2.7 Downloads](https://nuget.codeplex.com/releases/view/107605) page.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="ba066-243">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="ba066-243">Bug Fixes</span></span>

<span data-ttu-id="ba066-244">除了这些功能，此版本的 NuGet 还包括许多其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="ba066-244">In addition to these features, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="ba066-245">出现了 97 总问题在版本中解决。</span><span class="sxs-lookup"><span data-stu-id="ba066-245">There were 97 total issues addressed in the release.</span></span> <span data-ttu-id="ba066-246">有关工作的完整列表项固定在 NuGet 2.7，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。</span><span class="sxs-lookup"><span data-stu-id="ba066-246">For a full list of work items fixed in NuGet 2.7, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).</span></span>