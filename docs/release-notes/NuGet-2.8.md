---
title: NuGet 2.8 发行说明
description: NuGet 2.8 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237008"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="73ee2-103">NuGet 2.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="73ee2-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="73ee2-104">[NuGet 2.7.2 发行说明](../release-notes/nuget-2.7.2.md)  | [NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="73ee2-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="73ee2-105">NuGet 2.8 于2014年1月29日发布。</span><span class="sxs-lookup"><span data-stu-id="73ee2-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="73ee2-106">致谢</span><span class="sxs-lookup"><span data-stu-id="73ee2-106">Acknowledgements</span></span>

1. <span data-ttu-id="73ee2-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="73ee2-108">[#3466](https://nuget.codeplex.com/workitem/3466) -打包包时，验证依赖项包的 Id。</span><span class="sxs-lookup"><span data-stu-id="73ee2-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="73ee2-109">[圣马丁 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="73ee2-110">[#2379](https://nuget.codeplex.com/workitem/2379) -删除 persistening 源凭据时 $metadata 后缀。</span><span class="sxs-lookup"><span data-stu-id="73ee2-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="73ee2-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="73ee2-112">[#3538](http://nuget.codeplex.com/workitem/3538) -支持指定 nuget.exe update 命令的项目文件。</span><span class="sxs-lookup"><span data-stu-id="73ee2-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="73ee2-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="73ee2-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="73ee2-114">不通过-IncludeReferencedProjects 传递[#3536](http://nuget.codeplex.com/workitem/3536)替换标记。</span><span class="sxs-lookup"><span data-stu-id="73ee2-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="73ee2-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="73ee2-116">[#3677](http://nuget.codeplex.com/workitem/3677) 修复了推送大包时的 OutOfMemoryException 引发。</span><span class="sxs-lookup"><span data-stu-id="73ee2-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="73ee2-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="73ee2-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="73ee2-118">[#3666](http://nuget.codeplex.com/workitem/3666) -在项目引用另一个 CLI/c + + 项目时修复不正确的目标路径。</span><span class="sxs-lookup"><span data-stu-id="73ee2-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="73ee2-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="73ee2-120">[#3639](https://nuget.codeplex.com/workitem/3639) -默认情况下，允许将包安装为开发依赖项</span><span class="sxs-lookup"><span data-stu-id="73ee2-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="73ee2-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl)) </span><span class="sxs-lookup"><span data-stu-id="73ee2-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="73ee2-122">[#3717](https://nuget.codeplex.com/workitem/3717) -删除到最新修补程序版本的隐式升级</span><span class="sxs-lookup"><span data-stu-id="73ee2-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="73ee2-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="73ee2-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="73ee2-124">NuGet. Server、nuget.exe mirror 命令及其他程序的几个 bug 修复和改进。</span><span class="sxs-lookup"><span data-stu-id="73ee2-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="73ee2-125">这项工作是在数个月内完成的，Gregory 与我们一起使用，以将其集成到2.8 的主节点。</span><span class="sxs-lookup"><span data-stu-id="73ee2-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="73ee2-126">依赖项的修补程序解析</span><span class="sxs-lookup"><span data-stu-id="73ee2-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="73ee2-127">解析包依赖关系时，NuGet 一直实现了一个策略，该策略选择满足包的依赖项的最低主要和次要包版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="73ee2-128">但与主要和次要版本不同的是，修补程序版本总是解析为最高版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="73ee2-129">尽管此行为是善意的，但它却缺乏了安装具有依赖项的包的确定性。</span><span class="sxs-lookup"><span data-stu-id="73ee2-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="73ee2-130">请考虑以下示例：</span><span class="sxs-lookup"><span data-stu-id="73ee2-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="73ee2-131">在此示例中，即使安装了 Developer1 和 Developer2 PackageA@1.0.0 ，每个都最终使用不同版本的 PackageB。</span><span class="sxs-lookup"><span data-stu-id="73ee2-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="73ee2-132">NuGet 2.8 更改此默认行为，以便修补程序版本的依赖关系解析行为与主版本和次要版本的行为一致。</span><span class="sxs-lookup"><span data-stu-id="73ee2-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="73ee2-133">在上面的示例中，将在 PackageB@1.0.0 安装时安装 PackageA@1.0.0 ，而不考虑较新的修补程序版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="73ee2-134">-DependencyVersion 开关</span><span class="sxs-lookup"><span data-stu-id="73ee2-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="73ee2-135">尽管 NuGet 2.8 更改了用于解决依赖项的 _默认_ 行为，但它还在包管理器控制台中通过-DependencyVersion 开关更精确地控制依赖项解析过程。</span><span class="sxs-lookup"><span data-stu-id="73ee2-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="73ee2-136">开关允许将依赖项解析 (默认行为) 、可能的最高版本或最高的次要版本或修补程序版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="73ee2-137">此开关仅适用于 powershell 命令中的安装包。</span><span class="sxs-lookup"><span data-stu-id="73ee2-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 开关](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="73ee2-139">DependencyVersion 特性</span><span class="sxs-lookup"><span data-stu-id="73ee2-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="73ee2-140">除了上面详细说明的-DependencyVersion 开关以外，还允许 NuGet 在定义默认值的情况下设置新 Nuget.Config 属性的功能，如果未在的调用中指定-DependencyVersion 开关。</span><span class="sxs-lookup"><span data-stu-id="73ee2-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="73ee2-141">任何安装包操作的 "NuGet 包管理器" 对话框也会遵守此值。</span><span class="sxs-lookup"><span data-stu-id="73ee2-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="73ee2-142">若要设置此值，请将以下属性添加到 Nuget.Config 文件：</span><span class="sxs-lookup"><span data-stu-id="73ee2-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="73ee2-143">预览具有-whatif 的 NuGet 操作</span><span class="sxs-lookup"><span data-stu-id="73ee2-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="73ee2-144">某些 NuGet 包可能具有深层依赖项关系图，因此，在安装、卸载或更新操作过程中，它可帮助您首先了解将发生的情况。</span><span class="sxs-lookup"><span data-stu-id="73ee2-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="73ee2-145">NuGet 2.8 将标准 PowerShell whatif 交换机添加到安装包、卸载包和更新包命令中，以使将应用该命令的包的整个关闭可视化。</span><span class="sxs-lookup"><span data-stu-id="73ee2-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="73ee2-146">例如， `install-package Microsoft.AspNet.WebApi -whatif` 在空的 ASP.NET Web 应用程序中运行将生成以下项。</span><span class="sxs-lookup"><span data-stu-id="73ee2-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="73ee2-147">降级包</span><span class="sxs-lookup"><span data-stu-id="73ee2-147">Downgrade Package</span></span>

<span data-ttu-id="73ee2-148">安装包的预发行版本是为了调查新功能，然后决定回滚到最后一个稳定的版本，这种情况并不常见。</span><span class="sxs-lookup"><span data-stu-id="73ee2-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="73ee2-149">在 NuGet 2.8 之前，这是卸载预发行包及其依赖项，然后安装早期版本的多步骤过程。</span><span class="sxs-lookup"><span data-stu-id="73ee2-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="73ee2-150">不过，对于 NuGet 2.8，更新包现在将回滚整个包关闭 (例如，包的依赖关系树) 到以前的版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="73ee2-151">开发依赖项</span><span class="sxs-lookup"><span data-stu-id="73ee2-151">Development Dependencies</span></span>

<span data-ttu-id="73ee2-152">许多不同类型的功能可作为 NuGet 包提供-包括用于优化开发过程的工具。</span><span class="sxs-lookup"><span data-stu-id="73ee2-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="73ee2-153">这些组件虽然可以有助于开发新包，但在以后发布时，不应将其视为新包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="73ee2-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="73ee2-154">使用 NuGet 2.8，包可以将文件中的自身标识 `.nuspec` 为 developmentDependency。</span><span class="sxs-lookup"><span data-stu-id="73ee2-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="73ee2-155">安装后，还会将此元数据添加到 `packages.config` 安装包的项目的文件中。</span><span class="sxs-lookup"><span data-stu-id="73ee2-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="73ee2-156">稍后在 `packages.config` 中为 NuGet 依赖关系分析该文件时 `nuget.exe pack` ，它将排除标记为开发依赖项的这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="73ee2-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="73ee2-157">不同平台的单个 packages.config 文件</span><span class="sxs-lookup"><span data-stu-id="73ee2-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="73ee2-158">为多个目标平台开发应用程序时，通常会为各自的每个生成环境使用不同的项目文件。</span><span class="sxs-lookup"><span data-stu-id="73ee2-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="73ee2-159">在不同的项目文件中使用不同的 NuGet 包也很常见，因为包具有不同平台的不同级别的支持。</span><span class="sxs-lookup"><span data-stu-id="73ee2-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="73ee2-160">NuGet 2.8 通过 `packages.config` 为不同平台特定的项目文件创建不同的文件，为此方案提供了改进的支持。</span><span class="sxs-lookup"><span data-stu-id="73ee2-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![多个 package.config 文件](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="73ee2-162">回退到本地缓存</span><span class="sxs-lookup"><span data-stu-id="73ee2-162">Fallback to Local Cache</span></span>

<span data-ttu-id="73ee2-163">尽管 NuGet 包通常是从使用网络连接 [的](http://www.nuget.org/) 远程库使用，但在很多情况下客户端未连接。</span><span class="sxs-lookup"><span data-stu-id="73ee2-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="73ee2-164">如果没有网络连接，NuGet 客户端将无法成功安装包-即使这些包已在本地 NuGet 缓存中的客户端计算机上。</span><span class="sxs-lookup"><span data-stu-id="73ee2-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="73ee2-165">NuGet 2.8 将自动缓存回退添加到程序包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="73ee2-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="73ee2-166">例如，断开网络适配器和安装 jQuery 时，控制台将显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="73ee2-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="73ee2-167">缓存回退功能不需要任何特定的命令参数。</span><span class="sxs-lookup"><span data-stu-id="73ee2-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="73ee2-168">此外，缓存回退当前仅在包管理器控制台中运行-"包管理器" 对话框中当前未使用该行为。</span><span class="sxs-lookup"><span data-stu-id="73ee2-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="73ee2-169">WebMatrix NuGet 客户端更新</span><span class="sxs-lookup"><span data-stu-id="73ee2-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="73ee2-170">除了 NuGet 2.8，还更新了 WebMatrix 的 NuGet 扩展，以包含 [nuget 2.5](../release-notes/nuget-2.5.md)提供的很多主要功能。</span><span class="sxs-lookup"><span data-stu-id="73ee2-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="73ee2-171">新功能包括 "全部更新"、"最低 NuGet 版本" 等，并允许覆盖内容文件。</span><span class="sxs-lookup"><span data-stu-id="73ee2-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="73ee2-172">在 WebMatrix 3 中更新 NuGet 包管理器扩展：</span><span class="sxs-lookup"><span data-stu-id="73ee2-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="73ee2-173">打开 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="73ee2-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="73ee2-174">单击功能区中的扩展图标</span><span class="sxs-lookup"><span data-stu-id="73ee2-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="73ee2-175">选择 "更新" 选项卡</span><span class="sxs-lookup"><span data-stu-id="73ee2-175">Select the Updates tab</span></span>
1. <span data-ttu-id="73ee2-176">单击以将 NuGet 包管理器更新到2.5。0</span><span class="sxs-lookup"><span data-stu-id="73ee2-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="73ee2-177">关闭并重新启动 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="73ee2-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="73ee2-178">这是 NuGet 团队发布的 NuGet 包管理器扩展的第一个版本。</span><span class="sxs-lookup"><span data-stu-id="73ee2-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="73ee2-179">Microsoft 最近向开源 NuGet 项目提供了该代码。</span><span class="sxs-lookup"><span data-stu-id="73ee2-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="73ee2-180">以前，NuGet 集成内置于 WebMatrix 中，无法在 WebMatrix 中进行带外更新。</span><span class="sxs-lookup"><span data-stu-id="73ee2-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="73ee2-181">现在，我们可以将其与 NuGet 的客户端工具的其余部分进行进一步更新。</span><span class="sxs-lookup"><span data-stu-id="73ee2-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="73ee2-182">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="73ee2-182">Bug Fixes</span></span>

<span data-ttu-id="73ee2-183">在更新包-重新安装命令中，所做的一个主要 bug 修复是性能改进。</span><span class="sxs-lookup"><span data-stu-id="73ee2-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="73ee2-184">除了这些功能和前面提到的性能修复外，此版本的 NuGet 还包括许多其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="73ee2-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="73ee2-185">此版本中解决了181的总问题。</span><span class="sxs-lookup"><span data-stu-id="73ee2-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="73ee2-186">有关 NuGet 2.8 中已修复工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。</span><span class="sxs-lookup"><span data-stu-id="73ee2-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
