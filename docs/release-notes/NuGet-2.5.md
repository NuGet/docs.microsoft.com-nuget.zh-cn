---
title: NuGet 2.5 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.5 发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044998"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="db26c-103">NuGet 2.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="db26c-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="db26c-104">[NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="db26c-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="db26c-105">NuGet 2.5 已于 2013 年 4 月 25 日发布。</span><span class="sxs-lookup"><span data-stu-id="db26c-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="db26c-106">此版本已大以至于，我们觉得必须跳过版本 2.3 和 2.4 ！</span><span class="sxs-lookup"><span data-stu-id="db26c-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="db26c-107">到目前为止，这是我们已在 nuget，最大版本通过[160 工作项](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)发行版中的。</span><span class="sxs-lookup"><span data-stu-id="db26c-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="db26c-108">致谢</span><span class="sxs-lookup"><span data-stu-id="db26c-108">Acknowledgements</span></span>

<span data-ttu-id="db26c-109">我们真诚地感谢以下外部参与者所做出的重要贡献到 NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="db26c-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="db26c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="db26c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="db26c-111">[# 2847年](https://nuget.codeplex.com/workitem/2847)-添加 MonoAndroid、 MonoTouch 和 MonoMac 到已知的目标框架标识符的列表。</span><span class="sxs-lookup"><span data-stu-id="db26c-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="db26c-112">[Andres G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="db26c-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="db26c-113">[# 2865年](https://nuget.codeplex.com/workitem/2865)-修复拼写`NuGet.targets`区分大小写的操作系统</span><span class="sxs-lookup"><span data-stu-id="db26c-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="db26c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="db26c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="db26c-115">请在 Mono 上生成的解决方案。</span><span class="sxs-lookup"><span data-stu-id="db26c-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="db26c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="db26c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="db26c-117">修复 Mono 上失败的单元测试。</span><span class="sxs-lookup"><span data-stu-id="db26c-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="db26c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="db26c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="db26c-119">[# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe 包命令不会传播到 MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="db26c-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="db26c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="db26c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="db26c-121">[# 1511年](https://nuget.codeplex.com/workitem/1511)-修改 XML 处理代码以保留格式化。</span><span class="sxs-lookup"><span data-stu-id="db26c-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="db26c-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="db26c-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="db26c-123">添加到自定义的字典，以允许 build.cmd 成功识别的字。</span><span class="sxs-lookup"><span data-stu-id="db26c-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="db26c-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="db26c-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="db26c-125">在本地化 VS 中运行时，请修复单元测试。</span><span class="sxs-lookup"><span data-stu-id="db26c-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="db26c-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="db26c-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="db26c-127">从 PackageService 提取的接口</span><span class="sxs-lookup"><span data-stu-id="db26c-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="db26c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="db26c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="db26c-129">[#936](https://nuget.codeplex.com/workitem/936) -时封装处理项目依赖项</span><span class="sxs-lookup"><span data-stu-id="db26c-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="db26c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="db26c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="db26c-131">[# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支持清除文本密码时在 nuget.cofig 文件中存储包源凭据</span><span class="sxs-lookup"><span data-stu-id="db26c-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="db26c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="db26c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="db26c-133">[#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修复 Get 包帮助说明</span><span class="sxs-lookup"><span data-stu-id="db26c-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="db26c-134">我们还非常感谢下列人员有关如何查找 bug 与 NuGet 2.5 Beta/RC 批准并在最终发布之前修复：</span><span class="sxs-lookup"><span data-stu-id="db26c-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="db26c-135">[Tony 墙](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="db26c-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="db26c-136">[#3200](https://nuget.codeplex.com/workitem/3200) -与最新 NuGet 2.4 和 2.5 生成中断的 MSTest</span><span class="sxs-lookup"><span data-stu-id="db26c-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="db26c-137">发行版中的值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="db26c-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="db26c-138">允许用户覆盖已存在的内容文件</span><span class="sxs-lookup"><span data-stu-id="db26c-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="db26c-139">所有时间的最常请求的功能之一已被覆盖已存在时 NuGet 程序包中包含的磁盘的内容文件的能力。</span><span class="sxs-lookup"><span data-stu-id="db26c-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="db26c-140">从 NuGet 2.5 开始，识别这些冲突，并提示您覆盖文件，而以前始终跳过这些文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![覆盖内容文件](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="db26c-142">nuget.exe 更新和 Install-package 现在都具有一个新选项-FileConflictAction 设置一些默认值为命令行的方案。</span><span class="sxs-lookup"><span data-stu-id="db26c-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="db26c-143">从包文件已存在目标项目中时，请设置的默认操作。</span><span class="sxs-lookup"><span data-stu-id="db26c-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="db26c-144">设置为覆盖以始终覆盖文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="db26c-145">设置为忽略可跳过的文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="db26c-146">如果未指定，则它将提示输入每个冲突的文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="db26c-147">MSBuild 目标与属性文件的自动导入</span><span class="sxs-lookup"><span data-stu-id="db26c-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="db26c-148">已为用户创建一个新的常规文件夹，在 NuGet 包的最高级别。</span><span class="sxs-lookup"><span data-stu-id="db26c-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="db26c-149">作为的对等方`\lib`， `\content`，和`\tools`，你现在可以包含`\build`包中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="db26c-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="db26c-150">在此文件夹下，可以将带有固定名称的两个文件`{packageid}.targets`或`{packageid}.props`。</span><span class="sxs-lookup"><span data-stu-id="db26c-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="db26c-151">这两个文件可以是直接在`build`或在其他文件夹一样的特定于框架的文件夹下。</span><span class="sxs-lookup"><span data-stu-id="db26c-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="db26c-152">选取最佳匹配的 framework 文件夹的规则正是与那些相同。</span><span class="sxs-lookup"><span data-stu-id="db26c-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="db26c-153">当 NuGet \build 文件安装包时，它会将添加 MSBuild`<Import>`指向项目文件中的元素`.targets`和`.props`文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="db26c-154">`.props`的顶部，添加文件，而`.targets`文件添加到底部。</span><span class="sxs-lookup"><span data-stu-id="db26c-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="db26c-155">指定每个平台使用的不同引用`<References/>`元素</span><span class="sxs-lookup"><span data-stu-id="db26c-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="db26c-156">2.5 中之前, 在`.nuspec`文件，用户可以仅指定要为所有 framework 添加的引用文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="db26c-157">现在在 2.5 此新功能，用户可以编写`<reference/>`元素为每个受支持的平台，例如：</span><span class="sxs-lookup"><span data-stu-id="db26c-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="db26c-158">下面是如何 NuGet 添加对基于项目的引用的流`.nuspec`文件：</span><span class="sxs-lookup"><span data-stu-id="db26c-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="db26c-159">查找`lib`适合于目标框架，并从该文件夹中获得的程序集列表的文件夹</span><span class="sxs-lookup"><span data-stu-id="db26c-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="db26c-160">单独查找适合于目标框架的引用组，并从该组中获得的程序集列表。</span><span class="sxs-lookup"><span data-stu-id="db26c-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="db26c-161">没有指定的目标框架的引用组是回退的组。</span><span class="sxs-lookup"><span data-stu-id="db26c-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="db26c-162">查找的交集的两个列表中，并使用它作为引用添加</span><span class="sxs-lookup"><span data-stu-id="db26c-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="db26c-163">此新功能将允许包作者引用功能用于将程序集的子集应用于不同的框架，否则将需要执行在多个重复的程序集时`lib`文件夹。</span><span class="sxs-lookup"><span data-stu-id="db26c-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="db26c-164">注意： 你必须目前用于 nuget.exe 包使用此功能;NuGet 包资源管理器尚不支持它。</span><span class="sxs-lookup"><span data-stu-id="db26c-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="db26c-165">更新所有按钮，以允许同时更新所有包</span><span class="sxs-lookup"><span data-stu-id="db26c-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="db26c-166">你们中的许多了解的有关"更新包"PowerShell cmdlet 以更新的所有包;现在是 UI 以及通过执行此操作的简单办法。</span><span class="sxs-lookup"><span data-stu-id="db26c-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="db26c-167">若要尝试此功能：</span><span class="sxs-lookup"><span data-stu-id="db26c-167">To try this feature out:</span></span>

1. <span data-ttu-id="db26c-168">创建新的 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="db26c-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="db26c-169">启动管理 NuGet 包对话框</span><span class="sxs-lookup"><span data-stu-id="db26c-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="db26c-170">选择更新</span><span class="sxs-lookup"><span data-stu-id="db26c-170">Select 'Updates'</span></span>
1. <span data-ttu-id="db26c-171">单击全部更新按钮</span><span class="sxs-lookup"><span data-stu-id="db26c-171">Click the 'Update All' button</span></span>

![更新对话框中的所有按钮](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="db26c-173">改进的项目引用支持 nuget.exe 包</span><span class="sxs-lookup"><span data-stu-id="db26c-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="db26c-174">现在 nuget.exe 包命令流程引用项目使用以下规则：</span><span class="sxs-lookup"><span data-stu-id="db26c-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="db26c-175">如果引用的项目都有相应`.nuspec`文件，例如，存在名为的文件`proj1.nuspec`在所在的文件夹`proj1.csproj`，则此项目将添加为依赖项到包中，使用 id 并从读取版本`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="db26c-176">否则，引用的项目的文件会捆绑到包中。</span><span class="sxs-lookup"><span data-stu-id="db26c-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="db26c-177">然后将使用 sames 规则以递归方式处理此项目引用的项目。</span><span class="sxs-lookup"><span data-stu-id="db26c-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="db26c-178">所有 DLL， `.pdb`，和`.exe`添加文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="db26c-179">添加所有其他内容的文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-179">All other content files are added.</span></span>
1. <span data-ttu-id="db26c-180">合并所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="db26c-180">All dependencies are merged.</span></span>

<span data-ttu-id="db26c-181">这样，被视为依赖项，如果没有一个引用的项目`.nuspec`文件，否则，它将成为包的一部分。</span><span class="sxs-lookup"><span data-stu-id="db26c-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="db26c-182">此处更多详细信息： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="db26c-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="db26c-183">将最小 NuGet 版本属性添加到包</span><span class="sxs-lookup"><span data-stu-id="db26c-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="db26c-184">现在，新的元数据属性调用 minClientVersion 可以指示使用包所需的最小 NuGet 客户端版本。</span><span class="sxs-lookup"><span data-stu-id="db26c-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="db26c-185">此功能可帮助包作者指定，包将仅在特定版本的 NuGet 后正常工作。</span><span class="sxs-lookup"><span data-stu-id="db26c-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="db26c-186">作为新`.nuspec`添加功能，在 NuGet 2.5 之后包将能够声明的最小的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="db26c-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="db26c-187">如果用户已安装的 NuGet 2.5 并且为需要 2.6 确定包，视觉提示将赋予指示包将不可安装的用户。</span><span class="sxs-lookup"><span data-stu-id="db26c-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="db26c-188">然后将指导用户更新其版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="db26c-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="db26c-189">这将改进了现有的包从其中开始安装，但无法，该值指示无法识别的架构版本已标识的经验。</span><span class="sxs-lookup"><span data-stu-id="db26c-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="db26c-190">依赖项是不再不必要地更新包安装</span><span class="sxs-lookup"><span data-stu-id="db26c-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="db26c-191">在 NuGet 2.5 之前安装包时，依赖于在项目中，已安装的包依赖项将会更新属于新安装，即使现有版本满足依赖项。</span><span class="sxs-lookup"><span data-stu-id="db26c-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="db26c-192">如果依赖项版本不满足为已从 NuGet 2.5，依赖项将不会更新在其他包安装过程。</span><span class="sxs-lookup"><span data-stu-id="db26c-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="db26c-193">**方案：**</span><span class="sxs-lookup"><span data-stu-id="db26c-193">**The scenario:**</span></span>

1. <span data-ttu-id="db26c-194">源存储库包含版本 1.0.0 和 1.0.2 包 B。</span><span class="sxs-lookup"><span data-stu-id="db26c-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="db26c-195">它还包含程序包 A B 具有依赖关系 (> = 1.0.0)。</span><span class="sxs-lookup"><span data-stu-id="db26c-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="db26c-196">假定当前项目已具有包 B 版本 1.0.0 安装。</span><span class="sxs-lookup"><span data-stu-id="db26c-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="db26c-197">现在你想要安装包 a。</span><span class="sxs-lookup"><span data-stu-id="db26c-197">Now you want to install package A.</span></span>

<span data-ttu-id="db26c-198">**在 NuGet 2.2 和更早：**</span><span class="sxs-lookup"><span data-stu-id="db26c-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="db26c-199">在安装时包 A，NuGet 将自动更新 B 到 1.0.2，即使现有版本 1.0.0 已满足的依赖项版本约束，这是 > = 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="db26c-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="db26c-200">**在 NuGet 2.5 和更高版本：**</span><span class="sxs-lookup"><span data-stu-id="db26c-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="db26c-201">NuGet 将不再更新 B，因为它检测到现有的版本 1.0.0 满足的依赖项版本约束。</span><span class="sxs-lookup"><span data-stu-id="db26c-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="db26c-202">有关此更改的更多背景，读取详细[工作项](http://nuget.codeplex.com/workitem/1681)以及相关[讨论线程](http://nuget.codeplex.com/discussions/436712)。</span><span class="sxs-lookup"><span data-stu-id="db26c-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="db26c-203">nuget.exe 包含详细的详细级别的输出结果 http 请求</span><span class="sxs-lookup"><span data-stu-id="db26c-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="db26c-204">如果进行故障排除 nuget.exe 或只想哪些 HTTP 请求都在操作期间，-详细的详细信息交换机现在将输出发出的所有 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="db26c-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![从 nuget.exe 的 HTTP 输出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="db26c-206">nuget.exe 推送现在支持 UNC 和文件夹的源</span><span class="sxs-lookup"><span data-stu-id="db26c-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="db26c-207">之前 NuGet 2.5 中，如果尝试运行 'nuget.exe push' 到包源基于的 UNC 路径或本地文件夹，将失败的推送。</span><span class="sxs-lookup"><span data-stu-id="db26c-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="db26c-208">通过使用最近添加的层次结构配置功能中，它已成为常见的 nuget.exe 需要一个 UNC/文件夹源或基于 HTTP 的 NuGet 库为目标。</span><span class="sxs-lookup"><span data-stu-id="db26c-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="db26c-209">从开始 NuGet 2.5 中，如果 nuget.exe 标识 UNC/文件夹源，它将执行文件复制到源。</span><span class="sxs-lookup"><span data-stu-id="db26c-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="db26c-210">以下命令将失败：</span><span class="sxs-lookup"><span data-stu-id="db26c-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="db26c-211">nuget.exe 支持显式指定配置文件</span><span class="sxs-lookup"><span data-stu-id="db26c-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="db26c-212">现在访问配置 （除规范和包全部） 的 nuget.exe 命令支持的新-ConfigFile 选项，这会强制要用于取代了 %appdata%\nuget\nuget.config 的默认配置文件的特定配置文件。</span><span class="sxs-lookup"><span data-stu-id="db26c-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="db26c-213">示例:</span><span class="sxs-lookup"><span data-stu-id="db26c-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="db26c-214">对本机项目的支持</span><span class="sxs-lookup"><span data-stu-id="db26c-214">Support for Native projects</span></span>

<span data-ttu-id="db26c-215">NuGet 2.5 与 NuGet 工具现已可供 Visual Studio 中的本机项目。</span><span class="sxs-lookup"><span data-stu-id="db26c-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="db26c-216">我们的预期最本机包将使用更高版本，MSBuild 导入功能使用由工具[CoApp 项目](http://coapp.org)。</span><span class="sxs-lookup"><span data-stu-id="db26c-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="db26c-217">详细信息，请阅读[有关该工具的详细信息](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 网站上。</span><span class="sxs-lookup"><span data-stu-id="db26c-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="db26c-218">"本机"的目标框架名称是用于时包安装到本机项目 \build、 \content 和 \tools 中包括的文件的包引入的。</span><span class="sxs-lookup"><span data-stu-id="db26c-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="db26c-219">\`Lib 文件夹不用于本机项目。</span><span class="sxs-lookup"><span data-stu-id="db26c-219">The \`lib` folder is not used for native projects.</span></span>
