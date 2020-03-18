---
title: NuGet 2.5 发行说明
description: NuGet 2.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428293"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="26ea1-103">NuGet 2.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="26ea1-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="26ea1-104">[Nuget 2.2.1 发行说明](../release-notes/nuget-2.2.1.md) | [Nuget 2.6 发行说明](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="26ea1-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="26ea1-105">NuGet 2.5 于2013年4月25日发布。</span><span class="sxs-lookup"><span data-stu-id="26ea1-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="26ea1-106">此版本非常大，我们认为我们会跳过版本2.3 和2.4！</span><span class="sxs-lookup"><span data-stu-id="26ea1-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="26ea1-107">迄今为止，这是我们为 NuGet 提供的最大版本，其中包含160多个[工作项](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)。</span><span class="sxs-lookup"><span data-stu-id="26ea1-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="26ea1-108">致谢</span><span class="sxs-lookup"><span data-stu-id="26ea1-108">Acknowledgements</span></span>

<span data-ttu-id="26ea1-109">我们想感谢以下外部参与者对 NuGet 2.5 的重大贡献：</span><span class="sxs-lookup"><span data-stu-id="26ea1-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="26ea1-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) （[@dsplaisted](https://twitter.com/dsplaisted)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="26ea1-111">[#2847](https://nuget.codeplex.com/workitem/2847) -将 MonoAndroid、Monotouch.dialog 和 MonoMac 添加到已知目标框架标识符的列表。</span><span class="sxs-lookup"><span data-stu-id="26ea1-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="26ea1-112">[Andres Aragoneses](https://www.codeplex.com/site/users/view/knocte) （[@knocte](https://twitter.com/knocte)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="26ea1-113">[#2865](https://nuget.codeplex.com/workitem/2865) -修复区分大小写的操作系统的 `NuGet.targets` 的拼写</span><span class="sxs-lookup"><span data-stu-id="26ea1-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="26ea1-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) （[@davidfowl](https://twitter.com/davidfowl)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="26ea1-115">使解决方案在 Mono 上构建。</span><span class="sxs-lookup"><span data-stu-id="26ea1-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="26ea1-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) （[@atheken](https://twitter.com/atheken)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="26ea1-117">修复 Mono 上失败的单元测试。</span><span class="sxs-lookup"><span data-stu-id="26ea1-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="26ea1-118">[Marc-olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) （[@OliIsCool](https://twitter.com/oliiscool)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="26ea1-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe 包命令未将属性传播到 MSBuild</span><span class="sxs-lookup"><span data-stu-id="26ea1-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="26ea1-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) （[@bajtos](https://twitter.com/bajtos)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="26ea1-121">用于保留格式的[#1511](https://nuget.codeplex.com/workitem/1511)修改的 XML 处理代码。</span><span class="sxs-lookup"><span data-stu-id="26ea1-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="26ea1-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) （[@adamralph](https://twitter.com/adamralph)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="26ea1-123">已将识别的字词添加到自定义字典，以允许成功生成 .cmd。</span><span class="sxs-lookup"><span data-stu-id="26ea1-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="26ea1-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="26ea1-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="26ea1-125">在本地化和中运行时修复单元测试</span><span class="sxs-lookup"><span data-stu-id="26ea1-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="26ea1-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="26ea1-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="26ea1-127">已从 PackageService 中提取接口</span><span class="sxs-lookup"><span data-stu-id="26ea1-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="26ea1-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) （[@brugidou](https://twitter.com/brugidou)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="26ea1-129">[#936](https://nuget.codeplex.com/workitem/936) -在打包时处理项目依赖项</span><span class="sxs-lookup"><span data-stu-id="26ea1-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="26ea1-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) （[@XavierDecoster](https://twitter.com/xavierdecoster)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="26ea1-131">[#2991](https://nuget.codeplex.com/workitem/2991)，在 cofig 文件中存储包源凭据时， [#3164](https://nuget.codeplex.com/workitem/3164)支持明文密码</span><span class="sxs-lookup"><span data-stu-id="26ea1-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="26ea1-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) （[@manningj](https://twitter.com/manningj)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="26ea1-133">[#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191)修复获取包帮助说明</span><span class="sxs-lookup"><span data-stu-id="26ea1-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="26ea1-134">此外，我们还会感谢以下人员查找在最终版本之前批准和修复的 NuGet 2.5 Beta/RC bug：</span><span class="sxs-lookup"><span data-stu-id="26ea1-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="26ea1-135">[Tony 墙](https://www.codeplex.com/site/users/view/CodeChief)（[@CodeChief](https://twitter.com/codechief)）</span><span class="sxs-lookup"><span data-stu-id="26ea1-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="26ea1-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 中断了最新 NuGet 2.4 和2.5 版本</span><span class="sxs-lookup"><span data-stu-id="26ea1-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="26ea1-137">版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="26ea1-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="26ea1-138">允许用户覆盖已存在的内容文件</span><span class="sxs-lookup"><span data-stu-id="26ea1-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="26ea1-139">所有时间最常请求的功能之一是能够覆盖包含在 NuGet 包中的已存在于磁盘上的内容文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="26ea1-140">从 NuGet 2.5 开始，会识别这些冲突，并提示您覆盖这些文件，而以前这些文件始终被跳过。</span><span class="sxs-lookup"><span data-stu-id="26ea1-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![覆盖内容文件](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="26ea1-142">"nuget.exe update" 和 "安装包" 现在都有一个新选项 "-FileConflictAction" 用于为命令行方案设置某些默认值。</span><span class="sxs-lookup"><span data-stu-id="26ea1-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="26ea1-143">当目标项目中已存在来自包的文件时，设置默认操作。</span><span class="sxs-lookup"><span data-stu-id="26ea1-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="26ea1-144">设置为 "覆盖" 以始终覆盖文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="26ea1-145">设置为 "Ignore" 可跳过文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="26ea1-146">如果未指定，则会提示输入每个冲突的文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="26ea1-147">MSBuild 目标和属性文件的自动导入</span><span class="sxs-lookup"><span data-stu-id="26ea1-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="26ea1-148">已在 NuGet 包的顶层创建了一个新的传统文件夹。</span><span class="sxs-lookup"><span data-stu-id="26ea1-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="26ea1-149">作为对等的 `\lib`、`\content`和 `\tools`，你现在可以在包中包含 `\build` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="26ea1-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="26ea1-150">在此文件夹下，可以将两个具有固定名称的文件、`{packageid}.targets` 或 `{packageid}.props`。</span><span class="sxs-lookup"><span data-stu-id="26ea1-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="26ea1-151">这两个文件可以直接位于 `build` 下，也可以在特定于框架的文件夹下直接进行，就像其他文件夹一样。</span><span class="sxs-lookup"><span data-stu-id="26ea1-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="26ea1-152">选择最佳匹配框架文件夹的规则与这些文件夹的规则完全相同。</span><span class="sxs-lookup"><span data-stu-id="26ea1-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="26ea1-153">当 NuGet 安装带有 \build 文件的包时，它会将项目文件中的 MSBuild `<Import>` 元素添加到 `.targets` 并 `.props` 文件中。</span><span class="sxs-lookup"><span data-stu-id="26ea1-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="26ea1-154">`.props` 文件会添加到顶部，而 `.targets` 文件会添加到底部。</span><span class="sxs-lookup"><span data-stu-id="26ea1-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="26ea1-155">使用 `<References/>` 元素为每个平台指定不同的引用</span><span class="sxs-lookup"><span data-stu-id="26ea1-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="26ea1-156">在2.5 之前，用户只能在 `.nuspec` 文件中指定要为所有框架添加的引用文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="26ea1-157">现在，在2.5 中提供了这项新功能，用户可以为每个受支持的平台创作 `<reference/>` 元素，例如：</span><span class="sxs-lookup"><span data-stu-id="26ea1-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="26ea1-158">下面是 NuGet 如何根据 `.nuspec` 文件添加对项目的引用的流程：</span><span class="sxs-lookup"><span data-stu-id="26ea1-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="26ea1-159">查找适用于目标框架的 `lib` 文件夹，并从该文件夹获取程序集列表</span><span class="sxs-lookup"><span data-stu-id="26ea1-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="26ea1-160">分别查找适用于目标框架的引用组，并从该组获取程序集列表。</span><span class="sxs-lookup"><span data-stu-id="26ea1-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="26ea1-161">未指定目标框架的引用组是回退组。</span><span class="sxs-lookup"><span data-stu-id="26ea1-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="26ea1-162">查找两个列表的交集，并将其用作要添加的引用</span><span class="sxs-lookup"><span data-stu-id="26ea1-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="26ea1-163">如果需要在多个 `lib` 文件夹中包含重复的程序集，则此新功能将允许包作者使用 "引用" 功能将程序集的子集应用于不同框架。</span><span class="sxs-lookup"><span data-stu-id="26ea1-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="26ea1-164">注意：你目前必须使用 nuget.exe 包才能使用此功能;NuGet 包资源管理器尚不支持。</span><span class="sxs-lookup"><span data-stu-id="26ea1-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="26ea1-165">"全部更新" 按钮允许同时更新所有包</span><span class="sxs-lookup"><span data-stu-id="26ea1-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="26ea1-166">许多人都知道，"更新包" PowerShell cmdlet 可用于更新所有包;现在，还可以通过 UI 轻松完成此操作。</span><span class="sxs-lookup"><span data-stu-id="26ea1-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="26ea1-167">要尝试此功能，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="26ea1-167">To try this feature out:</span></span>

1. <span data-ttu-id="26ea1-168">新建 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="26ea1-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="26ea1-169">启动 "管理 NuGet 包" 对话框</span><span class="sxs-lookup"><span data-stu-id="26ea1-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="26ea1-170">选择 "更新"</span><span class="sxs-lookup"><span data-stu-id="26ea1-170">Select 'Updates'</span></span>
1. <span data-ttu-id="26ea1-171">单击 "全部更新" 按钮</span><span class="sxs-lookup"><span data-stu-id="26ea1-171">Click the 'Update All' button</span></span>

![对话框中的 "全部更新" 按钮](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="26ea1-173">改进了对 nuget 包的项目引用支持</span><span class="sxs-lookup"><span data-stu-id="26ea1-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="26ea1-174">现在，nuget.exe 包命令处理具有以下规则的引用项目：</span><span class="sxs-lookup"><span data-stu-id="26ea1-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="26ea1-175">如果引用的项目具有相应的 `.nuspec` 文件（例如，在与 `proj1.csproj`相同的文件夹中有一个名为 `proj1.nuspec` 的文件，则会使用从 `.nuspec` 文件中读取的 id 和版本将此项目作为依赖项添加到包中。</span><span class="sxs-lookup"><span data-stu-id="26ea1-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="26ea1-176">否则，被引用项目的文件捆绑到包中。</span><span class="sxs-lookup"><span data-stu-id="26ea1-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="26ea1-177">然后，将以递归方式使用 sames 规则处理此项目引用的项目。</span><span class="sxs-lookup"><span data-stu-id="26ea1-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="26ea1-178">添加所有 DLL、`.pdb`和 `.exe` 文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="26ea1-179">添加了其他所有内容文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-179">All other content files are added.</span></span>
1. <span data-ttu-id="26ea1-180">所有依赖项都将合并。</span><span class="sxs-lookup"><span data-stu-id="26ea1-180">All dependencies are merged.</span></span>

<span data-ttu-id="26ea1-181">这允许将引用的项目视为依赖项（如果存在 `.nuspec` 文件），否则它将成为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="26ea1-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="26ea1-182">更多详细信息： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="26ea1-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="26ea1-183">向包中添加 "最小 NuGet 版本" 属性</span><span class="sxs-lookup"><span data-stu-id="26ea1-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="26ea1-184">名为 "minClientVersion" 的新元数据属性现在可以指示使用包所需的最小 NuGet 客户端版本。</span><span class="sxs-lookup"><span data-stu-id="26ea1-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="26ea1-185">此功能有助于包作者指定仅在特定版本的 NuGet 后使用包。</span><span class="sxs-lookup"><span data-stu-id="26ea1-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="26ea1-186">由于新的 `.nuspec` 功能将在 NuGet 2.5 后添加，因此包将能够声明最低版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="26ea1-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="26ea1-187">如果用户安装了 NuGet 2.5，并且包被标识为需要2.6，则将向用户提供视觉提示，指示将无法安装包。</span><span class="sxs-lookup"><span data-stu-id="26ea1-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="26ea1-188">然后，用户将指导更新其 NuGet 的版本。</span><span class="sxs-lookup"><span data-stu-id="26ea1-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="26ea1-189">这会改进现有的体验，其中包开始安装，但随后会失败，指示标识了无法识别的架构版本。</span><span class="sxs-lookup"><span data-stu-id="26ea1-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="26ea1-190">包安装过程中不再需要再更新依赖项</span><span class="sxs-lookup"><span data-stu-id="26ea1-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="26ea1-191">在 NuGet 2.5 之前，当安装了依赖于项目中已安装的包的包时，该依赖项将作为新安装的一部分进行更新，即使现有版本满足了依赖关系也是如此。</span><span class="sxs-lookup"><span data-stu-id="26ea1-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="26ea1-192">从 NuGet 2.5 开始，如果依赖项版本已满足，则不会在其他包安装期间更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="26ea1-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="26ea1-193">**方案：**</span><span class="sxs-lookup"><span data-stu-id="26ea1-193">**The scenario:**</span></span>

1. <span data-ttu-id="26ea1-194">源存储库包含版本1.0.0 和1.0.2 的包 B。</span><span class="sxs-lookup"><span data-stu-id="26ea1-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="26ea1-195">它还包含在 B （> = 1.0.0）上依赖的包 A。</span><span class="sxs-lookup"><span data-stu-id="26ea1-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="26ea1-196">假定当前项目已安装了包 B 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="26ea1-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="26ea1-197">现在，你想要安装包 A。</span><span class="sxs-lookup"><span data-stu-id="26ea1-197">Now you want to install package A.</span></span>

<span data-ttu-id="26ea1-198">**在 NuGet 2.2 和更早版本中：**</span><span class="sxs-lookup"><span data-stu-id="26ea1-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="26ea1-199">安装包 A 时，NuGet 将自动更新 B 到1.0.2，即使现有版本1.0.0 已经满足依赖项版本约束，该约束 > = 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="26ea1-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="26ea1-200">**在 NuGet 2.5 和更高版本中：**</span><span class="sxs-lookup"><span data-stu-id="26ea1-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="26ea1-201">NuGet 将不再更新 B，因为它检测到现有版本1.0.0 满足依赖项版本约束。</span><span class="sxs-lookup"><span data-stu-id="26ea1-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="26ea1-202">有关此更改的更多背景信息，请阅读详细的[工作项](http://nuget.codeplex.com/workitem/1681)和相关的[讨论线索](http://nuget.codeplex.com/discussions/436712)。</span><span class="sxs-lookup"><span data-stu-id="26ea1-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="26ea1-203">nuget.exe 输出 http 请求以及详细详细信息</span><span class="sxs-lookup"><span data-stu-id="26ea1-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="26ea1-204">如果你正在排查 nuget.exe 问题，或者只是想要在操作过程中发出 HTTP 请求，"-详细信息" 开关现在会输出发出的所有 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="26ea1-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe 的 HTTP 输出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="26ea1-206">nuget.exe 推送现在支持 UNC 和文件夹源</span><span class="sxs-lookup"><span data-stu-id="26ea1-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="26ea1-207">在 NuGet 2.5 之前，如果尝试根据 UNC 路径或本地文件夹将 "nuget.exe push" 运行到包源，则推送会失败。</span><span class="sxs-lookup"><span data-stu-id="26ea1-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="26ea1-208">使用最近添加的层次结构配置功能，nuget.exe 需要将 UNC/文件夹源或基于 HTTP 的 NuGet 库作为目标。</span><span class="sxs-lookup"><span data-stu-id="26ea1-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="26ea1-209">从 NuGet 2.5 开始，如果 nuget.exe 标识 UNC/文件夹源，将对源执行文件复制。</span><span class="sxs-lookup"><span data-stu-id="26ea1-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="26ea1-210">现在可以使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="26ea1-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="26ea1-211">nuget.exe 支持显式指定的配置文件</span><span class="sxs-lookup"><span data-stu-id="26ea1-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="26ea1-212">访问配置（除 "spec" 和 "pack" 之外的所有文件）的 nuget.exe 命令现在支持新的 "-Read-configfile" 选项，该选项强制使用特定的配置文件来替代%Appdata%\nuget\nuget.config 上的默认配置文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="26ea1-213">示例：</span><span class="sxs-lookup"><span data-stu-id="26ea1-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="26ea1-214">对本机项目的支持</span><span class="sxs-lookup"><span data-stu-id="26ea1-214">Support for Native projects</span></span>

<span data-ttu-id="26ea1-215">使用 NuGet 2.5，NuGet 工具现在可用于 Visual Studio 中的本机项目。</span><span class="sxs-lookup"><span data-stu-id="26ea1-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="26ea1-216">我们预计大多数本机包都将使用[CoApp 项目](http://coapp.org)创建的工具来利用上述 MSBuild 导入功能。</span><span class="sxs-lookup"><span data-stu-id="26ea1-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="26ea1-217">有关详细信息，请参阅 coapp.org 网站上[有关该工具的详细](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)信息。</span><span class="sxs-lookup"><span data-stu-id="26ea1-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="26ea1-218">当包安装到本机项目中时，将为包引入 "本机" 的目标框架名称，以包括 \build、\content 和 \tools 中的文件。</span><span class="sxs-lookup"><span data-stu-id="26ea1-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="26ea1-219">\`lib "文件夹不用于本机项目。</span><span class="sxs-lookup"><span data-stu-id="26ea1-219">The \`lib\` folder is not used for native projects.</span></span>
