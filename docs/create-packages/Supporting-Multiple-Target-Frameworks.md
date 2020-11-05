---
title: NuGet 包的多目标
description: 介绍从一个 NuGet 包中以多个 .NET Framework 版本为目标的各种方法。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 7c0da38ab4059b89c9693ecbece2bc8ed1a775ec
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237940"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="c97ed-103">支持多个 .NET 版本</span><span class="sxs-lookup"><span data-stu-id="c97ed-103">Support multiple .NET versions</span></span>

<span data-ttu-id="c97ed-104">许多库以 .NET Framework 的特定版本为目标。</span><span class="sxs-lookup"><span data-stu-id="c97ed-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="c97ed-105">例如，你可能拥有特定于 UWP 的一个库版本，而拥有的另一版本利用 .NET Framework 4.6 中的功能。</span><span class="sxs-lookup"><span data-stu-id="c97ed-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="c97ed-106">为了适应这种情况，NuGet 支持将同一个库的多个版本放在单个包中。</span><span class="sxs-lookup"><span data-stu-id="c97ed-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="c97ed-107">本文介绍 NuGet 包的布局，但不考虑包或程序集的生成方式（也就是说，无论是使用多个非 SDK 样式的 .csproj  文件、自定义 .nuspec  文件，还是单个多目标 SDK 样式的 .csproj，布局都相同  ）。</span><span class="sxs-lookup"><span data-stu-id="c97ed-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj* ).</span></span> <span data-ttu-id="c97ed-108">对于 SDK 样式的项目，NuGet [pack 目标](../reference/msbuild-targets.md)知道如何设计包的布局，并自动将程序集放在正确的 lib 文件夹中，并为每个目标框架 (TFM) 创建依赖项组。</span><span class="sxs-lookup"><span data-stu-id="c97ed-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="c97ed-109">有关详细说明，请参阅[在项目文件中支持多个 .NET Framework 版本](multiple-target-frameworks-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="c97ed-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="c97ed-110">使用[创建包](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)中介绍的基于约定的工作目录方法时，必须按照本文所述手动设计包的布局。</span><span class="sxs-lookup"><span data-stu-id="c97ed-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="c97ed-111">对于 SDK 样式的项目，建议使用自动方法，但也可以选择按照本文所述手动设计包的布局。</span><span class="sxs-lookup"><span data-stu-id="c97ed-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="c97ed-112">框架版本的文件夹结构</span><span class="sxs-lookup"><span data-stu-id="c97ed-112">Framework version folder structure</span></span>

<span data-ttu-id="c97ed-113">生成仅包含一个库版本或面向多个框架的包时，始终根据以下约定使用区分大小写的不同框架名称在 `lib` 下创建子文件夹：</span><span class="sxs-lookup"><span data-stu-id="c97ed-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="c97ed-114">有关支持的名称的完整列表，请参阅[目标框架引用](../reference/target-frameworks.md#supported-frameworks)。</span><span class="sxs-lookup"><span data-stu-id="c97ed-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="c97ed-115">所具有的库版本必须特定于某框架，且不应直接放置在根 `lib` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c97ed-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="c97ed-116">（此功能仅受 `packages.config` 支持。）</span><span class="sxs-lookup"><span data-stu-id="c97ed-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="c97ed-117">此操作会导致库与任何目标框架兼容，并允许在任何位置上进行安装，很可能造成意外的运行时错误。</span><span class="sxs-lookup"><span data-stu-id="c97ed-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="c97ed-118">已弃用在根文件夹（如 `lib\abc.dll`）或子文件夹（如 `lib\abc\abc.dll`）中添加程序集的操作，且在使用 PackagesReference 格式时忽略了此操作。</span><span class="sxs-lookup"><span data-stu-id="c97ed-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="c97ed-119">例如，以下文件夹结构支持特定于框架的程序集的四种版本：</span><span class="sxs-lookup"><span data-stu-id="c97ed-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="c97ed-120">若要在生成包时轻松包括所有这些文件，请在 `.nuspec` 的 `<files>` 部分中使用递归 `**` 通配符：</span><span class="sxs-lookup"><span data-stu-id="c97ed-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="c97ed-121">特定于体系结构的文件夹</span><span class="sxs-lookup"><span data-stu-id="c97ed-121">Architecture-specific folders</span></span>

<span data-ttu-id="c97ed-122">如果具有特定于体系结构的程序集，即面向 ARM、x86 和 x64 的单独程序集，必须将它们放置在名为 `{platform}-{architecture}\lib\{framework}` 或 `{platform}-{architecture}\native` 的子文件夹内名为 `runtimes` 的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c97ed-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="c97ed-123">例如，以下文件夹结构可以容纳面向 Windows 10 的本机和托管 DLL 以及 `uap10.0` 框架：</span><span class="sxs-lookup"><span data-stu-id="c97ed-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="c97ed-124">这些程序集将仅在运行时可用，因此，如果你也想要提供相应的编译时程序集，则在 `/ref/{tfm}` 文件夹中设置 `AnyCPU` 程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="c97ed-125">请注意，NuGet 始终从一个文件夹选取这些编译或运行时资产，因此，如果在 `/ref` 中存在某些兼容资产，则将忽略 `/lib` 以添加编译时程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="c97ed-126">同样，如果在 `/runtimes` 中有某些兼容资产，则也将为运行时忽略 `/lib`。</span><span class="sxs-lookup"><span data-stu-id="c97ed-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="c97ed-127">有关在 `.nuspec` 清单中引用这些文件的示例，请参阅[创建 UWP 包](../guides/create-uwp-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="c97ed-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="c97ed-128">此外，请参阅[使用 NuGet 打包 Windows 存储应用组件](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="c97ed-128">Also, see [Packing a Windows store app component with NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="c97ed-129">将程序集版本与项目中的目标框架匹配</span><span class="sxs-lookup"><span data-stu-id="c97ed-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="c97ed-130">NuGet 在安装具有多个程序集版本的包时，会尝试将程序集的框架名称与项目的目标框架匹配。</span><span class="sxs-lookup"><span data-stu-id="c97ed-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="c97ed-131">如果未找到匹配项，NuGet 将复制小于或等于项目的目标框架的最高版本的程序集（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="c97ed-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="c97ed-132">如果未找到任何兼容的程序集，NuGet 将返回相应的错误消息。</span><span class="sxs-lookup"><span data-stu-id="c97ed-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="c97ed-133">例如，假设包中具有以下文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="c97ed-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="c97ed-134">当在面向 .NET Framework 4.6 的项目中安装此包时，NuGet 将在 `net45` 文件夹中安装程序集，因为它是小于或等于 4.6 的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="c97ed-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="c97ed-135">但是，如果项目面向 .NET Framework 4.6.1，NuGet 将在 `net461` 文件夹中安装程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="c97ed-136">如果项目面向 .NET Framework 4.0 和更早版本，NuGet 会发出相应的错误消息，因为找不到兼容的程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="c97ed-137">通过框架版本对程序集进行分组</span><span class="sxs-lookup"><span data-stu-id="c97ed-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="c97ed-138">NuGet 仅从包中的单个库文件夹中复制程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="c97ed-139">例如，假设包具有以下文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="c97ed-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="c97ed-140">当在面向 .NET Framework 4.5 的项目中安装包时，将仅安装 `MyAssembly.dll` (v2.0) 程序集。</span><span class="sxs-lookup"><span data-stu-id="c97ed-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="c97ed-141">不会安装 `MyAssembly.Core.dll` (v1.0)，因为它未在 `net45` 文件夹中列出。</span><span class="sxs-lookup"><span data-stu-id="c97ed-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="c97ed-142">NuGet 执行此操作的原因是 `MyAssembly.Core.dll` 可能已合并到 `MyAssembly.dll` 的 2.0 版本中。</span><span class="sxs-lookup"><span data-stu-id="c97ed-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="c97ed-143">如果要为 .NET Framework 4.5 安装 `MyAssembly.Core.dll`，请在 `net45` 文件夹中放置副本。</span><span class="sxs-lookup"><span data-stu-id="c97ed-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="c97ed-144">通过框架配置文件对程序集进行分组</span><span class="sxs-lookup"><span data-stu-id="c97ed-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="c97ed-145">NuGet 还通过向文件夹末尾追加短划线和配置文件名称，支持以特定的框架配置文件为目标。</span><span class="sxs-lookup"><span data-stu-id="c97ed-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="c97ed-146">以下是支持的配置文件：</span><span class="sxs-lookup"><span data-stu-id="c97ed-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="c97ed-147">`client`：客户端配置文件</span><span class="sxs-lookup"><span data-stu-id="c97ed-147">`client`: Client Profile</span></span>
- <span data-ttu-id="c97ed-148">`full`：完整配置文件</span><span class="sxs-lookup"><span data-stu-id="c97ed-148">`full`: Full Profile</span></span>
- <span data-ttu-id="c97ed-149">`wp`：Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c97ed-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="c97ed-150">`cf`：Compact Framework</span><span class="sxs-lookup"><span data-stu-id="c97ed-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="c97ed-151">声明依赖项（高级）</span><span class="sxs-lookup"><span data-stu-id="c97ed-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="c97ed-152">打程序包项目文件时，NuGet 尝试从项目自动生成依赖项。</span><span class="sxs-lookup"><span data-stu-id="c97ed-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="c97ed-153">此部分中的信息介绍了如何使用 .nuspec 文件声明依赖项，通常仅高级方案需要使用此信息。 </span><span class="sxs-lookup"><span data-stu-id="c97ed-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="c97ed-154">*（版本 2.0+）* 可以使用 `<dependencies>` 元素中的 `<group>` 元素在目标项目的目标框架对应的 .nuspec 中声明程序包依赖项。</span><span class="sxs-lookup"><span data-stu-id="c97ed-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="c97ed-155">有关详细信息，请参阅[依赖项元素](../reference/nuspec.md#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="c97ed-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="c97ed-156">每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<dependency>` 元素。</span><span class="sxs-lookup"><span data-stu-id="c97ed-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="c97ed-157">当目标框架与项目的框架配置文件兼容时，将会一起安装这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="c97ed-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="c97ed-158">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="c97ed-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="c97ed-159">建议每个目标框架名字对象 (TFM) 将一个组用于 lib/ 和 ref/ 文件夹中的文件。  </span><span class="sxs-lookup"><span data-stu-id="c97ed-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="c97ed-160">以下示例显示了 `<group>` 元素的不同变体：</span><span class="sxs-lookup"><span data-stu-id="c97ed-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="c97ed-161">确定要使用的 NuGet 目标</span><span class="sxs-lookup"><span data-stu-id="c97ed-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="c97ed-162">当打包面向可移植类库的库时，不容易确定应在文件夹名称和 `.nuspec` 文件中使用的 NuGet 目标，尤其当仅面向 PCL 的子集时。</span><span class="sxs-lookup"><span data-stu-id="c97ed-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="c97ed-163">以下外部资源有助于解决此问题：</span><span class="sxs-lookup"><span data-stu-id="c97ed-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="c97ed-164">[.NET 中的框架配置文件](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="c97ed-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="c97ed-165">[可移植类库的配置文件](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co)：枚举 PCL 配置文件及其等效 NuGet 目标的表</span><span class="sxs-lookup"><span data-stu-id="c97ed-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="c97ed-166">[可移植类库的配置文件工具](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com)：用于确定系统上可用的 PCL 配置文件的命令行工具</span><span class="sxs-lookup"><span data-stu-id="c97ed-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="c97ed-167">内容文件和 PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="c97ed-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="c97ed-168">仅可通过 `packages.config` 格式使用可变的内容文件和脚本执行；这些内容在使用所有其他格式时已弃用，且不应用于任何新的包。</span><span class="sxs-lookup"><span data-stu-id="c97ed-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="c97ed-169">对于 `packages.config`，可以使用 `content` 和 `tools` 文件夹中的相同文件夹约定，通过目标框架对内容文件和 PowerShell 脚本进行分组。</span><span class="sxs-lookup"><span data-stu-id="c97ed-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="c97ed-170">例如：</span><span class="sxs-lookup"><span data-stu-id="c97ed-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="c97ed-171">如果框架文件夹保留为空，NuGet 不会添加程序集引用或内容文件，也不会运行该框架的 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c97ed-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="c97ed-172">因为 `init.ps1` 在解决方案级别执行，且它不依赖于项目，所以必须将其直接放置在 `tools` 文件夹下。</span><span class="sxs-lookup"><span data-stu-id="c97ed-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="c97ed-173">如果将其放置在框架文件夹下，它会被忽略。</span><span class="sxs-lookup"><span data-stu-id="c97ed-173">It's ignored if placed under a framework folder.</span></span>