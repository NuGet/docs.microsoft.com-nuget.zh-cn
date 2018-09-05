---
title: NuGet 2.8 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.8 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547454"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="5c055-103">NuGet 2.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="5c055-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="5c055-104">[NuGet 2.7.2 发行说明](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="5c055-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="5c055-105">NuGet 2.8 已于 2014 年 1 月 29 日发布。</span><span class="sxs-lookup"><span data-stu-id="5c055-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="5c055-106">致谢</span><span class="sxs-lookup"><span data-stu-id="5c055-106">Acknowledgements</span></span>

1. <span data-ttu-id="5c055-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="5c055-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="5c055-108">[#3466](https://nuget.codeplex.com/workitem/3466) -打包验证 Id 的依赖项包的包时。</span><span class="sxs-lookup"><span data-stu-id="5c055-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="5c055-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="5c055-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="5c055-110">[# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 源的凭据时删除 $metadata 后缀。</span><span class="sxs-lookup"><span data-stu-id="5c055-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="5c055-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="5c055-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="5c055-112">[#3538](http://nuget.codeplex.com/workitem/3538) -指定用于 nuget.exe 更新命令的项目文件的支持。</span><span class="sxs-lookup"><span data-stu-id="5c055-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="5c055-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="5c055-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="5c055-114">[#3536](http://nuget.codeplex.com/workitem/3536) -不使用-IncludeReferencedProjects 传递的替换令牌。</span><span class="sxs-lookup"><span data-stu-id="5c055-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="5c055-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="5c055-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="5c055-116">[#3677](http://nuget.codeplex.com/workitem/3677) -修复 nuget.push 推送大型包时引发 OutOfMemoryException。</span><span class="sxs-lookup"><span data-stu-id="5c055-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="5c055-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="5c055-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="5c055-118">[#3666](http://nuget.codeplex.com/workitem/3666) -项目引用另一个 CLI/c + + 项目时修复不正确的目标路径。</span><span class="sxs-lookup"><span data-stu-id="5c055-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="5c055-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="5c055-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="5c055-120">[#3639](https://nuget.codeplex.com/workitem/3639) -允许用于默认情况下为开发依赖项安装的包</span><span class="sxs-lookup"><span data-stu-id="5c055-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="5c055-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="5c055-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="5c055-122">[#3717](https://nuget.codeplex.com/workitem/3717) -删除隐式升级到最新的修补程序版本</span><span class="sxs-lookup"><span data-stu-id="5c055-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="5c055-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="5c055-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="5c055-124">了几个 bug 修复和改进 NuGet.Server、 nuget.exe 镜像命令和其他人。</span><span class="sxs-lookup"><span data-stu-id="5c055-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="5c055-125">这项工作在几个月，已完成，Gregory 使用正确的计时我们要将集成到为 2.8 母版。</span><span class="sxs-lookup"><span data-stu-id="5c055-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="5c055-126">修补程序解析依赖项</span><span class="sxs-lookup"><span data-stu-id="5c055-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="5c055-127">在解析包依赖项，NuGet 已从历史上看实现选择满足对包依赖项的最小主版本号和次包版本的策略。</span><span class="sxs-lookup"><span data-stu-id="5c055-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="5c055-128">与不同的主版本号和次版本，但是，修补程序版本是始终解析为的最高版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="5c055-129">该行为是善意的但缺乏安装具有依赖项包的确定性创建它。</span><span class="sxs-lookup"><span data-stu-id="5c055-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="5c055-130">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="5c055-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="5c055-131">在此示例中，即使 Developer1 和 Developer2 安装PackageA@1.0.0、 每个使用不同版本的 PackageB 向上结束。</span><span class="sxs-lookup"><span data-stu-id="5c055-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="5c055-132">这样，修补程序版本的依赖关系解析行为与主要和次要版本的行为保持一致，NuGet 2.8 会更改此默认行为。</span><span class="sxs-lookup"><span data-stu-id="5c055-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="5c055-133">在上面的示例中，然后PackageB@1.0.0由于安装将安装PackageA@1.0.0，而不考虑的较新的修补程序版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="5c055-134">-DependencyVersion 开关</span><span class="sxs-lookup"><span data-stu-id="5c055-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="5c055-135">尽管 NuGet 2.8 更改_默认_行为对于解析的依赖关系，它还将添加更加精确地控制通过-DependencyVersion 开关的依赖关系解析过程中包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="5c055-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="5c055-136">开关可以启用对可能的最低版本 （默认行为）、 可能的最高版本，或最高次要或修补程序版本的解析依赖项。</span><span class="sxs-lookup"><span data-stu-id="5c055-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="5c055-137">此开关仅适用于在 powershell 命令中的安装包。</span><span class="sxs-lookup"><span data-stu-id="5c055-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 开关](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="5c055-139">DependencyVersion 属性</span><span class="sxs-lookup"><span data-stu-id="5c055-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="5c055-140">除了上面详细说明的功能还允许 NuGet 在 Nuget.Config 文件中设置新属性-DependencyVersion 开关定义默认值什么，如果在调用中未指定-DependencyVersion 开关安装包。</span><span class="sxs-lookup"><span data-stu-id="5c055-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="5c055-141">NuGet 包管理器对话框中的任何安装包操作还会遵循此值。</span><span class="sxs-lookup"><span data-stu-id="5c055-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="5c055-142">若要设置此值，请将以下属性添加到在 Nuget.Config 文件：</span><span class="sxs-lookup"><span data-stu-id="5c055-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="5c055-143">使用-whatif 预览 NuGet 操作</span><span class="sxs-lookup"><span data-stu-id="5c055-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="5c055-144">一些 NuGet 包可以有深入的依赖项关系图，并且在这种情况下，它可以在安装过程中会有所帮助、 卸载或更新操作，以首先查看会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="5c055-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="5c055-145">NuGet 2.8 将标准 PowerShell-whatif 开关添加到安装包、 卸载包和更新包命令来启用可视化命令将应用于包的完整闭包。</span><span class="sxs-lookup"><span data-stu-id="5c055-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="5c055-146">例如，运行`install-package Microsoft.AspNet.WebApi -whatif`中一个空的 ASP.NET Web 应用程序会产生以下结果。</span><span class="sxs-lookup"><span data-stu-id="5c055-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a><span data-ttu-id="5c055-147">降级包</span><span class="sxs-lookup"><span data-stu-id="5c055-147">Downgrade Package</span></span>

<span data-ttu-id="5c055-148">不常见安装包的预发布版本，以便调查的新功能，然后决定要回滚到上次的稳定版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="5c055-149">之前 NuGet 2.8，这是一个多步骤过程，以及卸载预发行包和其依赖项，然后安装较早版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="5c055-150">使用 NuGet 2.8，但是，更新包将现在回滚整个包闭包 （例如包的依赖项树） 到以前的版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="5c055-151">开发依赖项</span><span class="sxs-lookup"><span data-stu-id="5c055-151">Development Dependencies</span></span>

<span data-ttu-id="5c055-152">作为 NuGet 包-包括用于优化开发过程的工具，可以提供许多不同类型的功能。</span><span class="sxs-lookup"><span data-stu-id="5c055-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="5c055-153">这些组件，它们可有助于开发新的包，而不应将新包的依赖项更高版本发布时。</span><span class="sxs-lookup"><span data-stu-id="5c055-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="5c055-154">NuGet 2.8 使包来标识自身中`.nuspec`为 developmentDependency 文件。</span><span class="sxs-lookup"><span data-stu-id="5c055-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="5c055-155">安装时，此元数据也将添加到`packages.config`已在其中安装了包的项目文件。</span><span class="sxs-lookup"><span data-stu-id="5c055-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="5c055-156">时，`packages.config`文件更高版本的 NuGet 依赖项期间分析`nuget.exe pack`，它将排除这些依赖项标记为开发依赖项。</span><span class="sxs-lookup"><span data-stu-id="5c055-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="5c055-157">针对不同平台的单独的 packages.config 文件</span><span class="sxs-lookup"><span data-stu-id="5c055-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="5c055-158">开发针对多个目标平台的应用程序，时，通常会为每个相应的生成环境中有不同的项目文件。</span><span class="sxs-lookup"><span data-stu-id="5c055-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="5c055-159">也很常见使用不同的 NuGet 包在不同的项目文件中，如包具有不同级别的不同平台的支持。</span><span class="sxs-lookup"><span data-stu-id="5c055-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="5c055-160">NuGet 2.8 提供改进的支持实现此方案创建不同`packages.config`不同的特定于平台的项目文件的文件。</span><span class="sxs-lookup"><span data-stu-id="5c055-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![多个 package.config 文件](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="5c055-162">回退到本地缓存</span><span class="sxs-lookup"><span data-stu-id="5c055-162">Fallback to Local Cache</span></span>

<span data-ttu-id="5c055-163">尽管 NuGet 包会通常占用从远程库等[NuGet 库](http://www.nuget.org/)使用的网络连接，有许多方案，客户端未连接。</span><span class="sxs-lookup"><span data-stu-id="5c055-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="5c055-164">无网络连接，NuGet 客户端无法成功安装包的即使这些包已在本地 NuGet 缓存中的客户端的计算机上。</span><span class="sxs-lookup"><span data-stu-id="5c055-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="5c055-165">NuGet 2.8 将自动缓存回退添加到包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="5c055-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="5c055-166">例如，当断开连接的网络适配器并安装 jQuery，在控制台显示如下信息：</span><span class="sxs-lookup"><span data-stu-id="5c055-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="5c055-167">缓存回退功能不需要任何特定的命令参数。</span><span class="sxs-lookup"><span data-stu-id="5c055-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="5c055-168">此外，只能在包管理器控制台中当前运行缓存回退-行为目前不能在包管理器对话框。</span><span class="sxs-lookup"><span data-stu-id="5c055-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="5c055-169">WebMatrix NuGet 客户端的更新</span><span class="sxs-lookup"><span data-stu-id="5c055-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="5c055-170">NuGet 2.8 以及适用于 WebMatrix 的 NuGet 扩展也已更新为包括的许多主要功能附带[NuGet 2.5](../release-notes/nuget-2.5.md)。</span><span class="sxs-lookup"><span data-stu-id="5c055-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="5c055-171">新功能包括如更新全部、 最小值 NuGet 版本和允许的内容文件的覆盖。</span><span class="sxs-lookup"><span data-stu-id="5c055-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="5c055-172">若要更新你在 WebMatrix 3 中的 NuGet 包管理器扩展：</span><span class="sxs-lookup"><span data-stu-id="5c055-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="5c055-173">打开 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="5c055-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="5c055-174">单击功能区中的扩展图标</span><span class="sxs-lookup"><span data-stu-id="5c055-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="5c055-175">选择更新选项卡</span><span class="sxs-lookup"><span data-stu-id="5c055-175">Select the Updates tab</span></span>
1. <span data-ttu-id="5c055-176">单击此项可为 2.5.0 更新 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="5c055-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="5c055-177">关闭并重新启动 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="5c055-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="5c055-178">这是 NuGet 团队的 NuGet 包管理器扩展的 WebMatrix 的第一个版本。</span><span class="sxs-lookup"><span data-stu-id="5c055-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="5c055-179">代码最近已由 Microsoft 的开源 NuGet 项目到提供。</span><span class="sxs-lookup"><span data-stu-id="5c055-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="5c055-180">以前，NuGet 集成已内置到 WebMatrix 中，并且带外从 WebMatrix 无法更新。</span><span class="sxs-lookup"><span data-stu-id="5c055-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="5c055-181">现在，我们能够进行进一步与 NuGet 的客户端工具的其余部分一起更新。</span><span class="sxs-lookup"><span data-stu-id="5c055-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5c055-182">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="5c055-182">Bug Fixes</span></span>

<span data-ttu-id="5c055-183">所做的主要 bug 修复之一就是更新包中的性能改进的重新安装命令。</span><span class="sxs-lookup"><span data-stu-id="5c055-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="5c055-184">除了这些功能和前面提到的性能修复程序，此版本的 NuGet 还包括许多其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="5c055-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="5c055-185">出现的版本中解决的 181 总问题。</span><span class="sxs-lookup"><span data-stu-id="5c055-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="5c055-186">有关完整列表的工作项中已修复 NuGet 2.8，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。</span><span class="sxs-lookup"><span data-stu-id="5c055-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
