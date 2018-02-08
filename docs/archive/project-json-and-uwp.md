---
title: "NuGet project.json 文件和 UWP 项目 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "介绍如何使用 project.json 文件来跟踪通用 Windows 平台 (UWP) 项目中的 NuGet 依赖项。"
keywords: "NuGet 依赖项, NuGet 和 UWP, UWP 和 project.json, NuGet project.json 文件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f1ec086d6404c441ca5ad53028af2265a2344905
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="935d7-104">project.json 和 UWP</span><span class="sxs-lookup"><span data-stu-id="935d7-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="935d7-105">此内容已弃用。</span><span class="sxs-lookup"><span data-stu-id="935d7-105">This content is deprecated.</span></span> <span data-ttu-id="935d7-106">项目应使用 `packages.config` 或 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="935d7-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="935d7-107">本文档介绍使用 NuGet 3+（Visual Studio 2015 及更高版本）中功能的包结构。</span><span class="sxs-lookup"><span data-stu-id="935d7-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="935d7-108">可以通过将 `.nuspec` 的 `minClientVersion` 设置为 3.1 来声明你需要此处介绍的功能。</span><span class="sxs-lookup"><span data-stu-id="935d7-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="935d7-109">向现有包添加 UWP 支持</span><span class="sxs-lookup"><span data-stu-id="935d7-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="935d7-110">如果有一个现有包，并且想添加对 UWP 应用程序的支持，则不需要采用此处介绍的打包格式。</span><span class="sxs-lookup"><span data-stu-id="935d7-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="935d7-111">如果需要此处介绍的功能并且只愿意使用已更新到 3+ 版 NuGet 的客户端，只需采用此格式即可。</span><span class="sxs-lookup"><span data-stu-id="935d7-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="935d7-112">已面向 netcore45</span><span class="sxs-lookup"><span data-stu-id="935d7-112">I already target netcore45</span></span>

<span data-ttu-id="935d7-113">如果已面向 `netcore45`，并且不需要利用此处介绍的功能，则无需执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="935d7-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="935d7-114">UWP 应用程序可以使用 `netcore45` 包。</span><span class="sxs-lookup"><span data-stu-id="935d7-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="935d7-115">希望利用 Windows 10 特定的 API</span><span class="sxs-lookup"><span data-stu-id="935d7-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="935d7-116">在这种情况下，需要将 `uap10.0` 目标框架名字对象（TFM 或 TxM）添加到包。</span><span class="sxs-lookup"><span data-stu-id="935d7-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="935d7-117">在包中创建一个新文件夹，并将已编译为与 Windows 10 一起使用的程序集添加到该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="935d7-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="935d7-118">不需要 Windows 10 特定的 API，但需要新的 .NET 功能或者尚没有 netcore45</span><span class="sxs-lookup"><span data-stu-id="935d7-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="935d7-119">在这种情况下，需要将 `dotnet` TxM 添加到包。</span><span class="sxs-lookup"><span data-stu-id="935d7-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="935d7-120">与其他 TxM 不同，`dotnet` 并不意味着外围应用或平台。</span><span class="sxs-lookup"><span data-stu-id="935d7-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="935d7-121">也就是说，包适用于依赖项适用的任何平台。</span><span class="sxs-lookup"><span data-stu-id="935d7-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="935d7-122">使用 `dotnet` TxM 生成包时，`.nuspec` 中可能存在许多 TxM 特定的依赖项，因为需要定义所依赖的 BCL 包，如 `System.Text`、`System.Xml` 等。这些依赖项适用的位置即是包的工作位置。</span><span class="sxs-lookup"><span data-stu-id="935d7-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="935d7-123">如何查找依赖项</span><span class="sxs-lookup"><span data-stu-id="935d7-123">How do I find out my dependencies</span></span>

<span data-ttu-id="935d7-124">有两种方法可以查找要列出的依赖项：</span><span class="sxs-lookup"><span data-stu-id="935d7-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="935d7-125">使用 [NuSpec 依赖项生成器](https://github.com/onovotny/ReferenceGenerator)第三方工具。</span><span class="sxs-lookup"><span data-stu-id="935d7-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="935d7-126">该工具自动执行该过程，并使用生成时依赖的包更新 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="935d7-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="935d7-127">该工具通过 NuGet 包 [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) 提供。</span><span class="sxs-lookup"><span data-stu-id="935d7-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="935d7-128">（复杂方法）使用 `ILDasm` 检查 `.dll`，查看运行时实际需要的程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="935d7-129">然后确定这些程序集分别来自哪个 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="935d7-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="935d7-130">请参阅 [`project.json`](project-json.md) 主题，详细了解可帮助创建支持 `dotnet` TxM 的包的功能。</span><span class="sxs-lookup"><span data-stu-id="935d7-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="935d7-131">如果打算将包用于 PCL 项目，强烈建议创建一个 `dotnet` 文件夹，以避免警告和潜在的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="935d7-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="935d7-132">目录结构</span><span class="sxs-lookup"><span data-stu-id="935d7-132">Directory structure</span></span>

<span data-ttu-id="935d7-133">使用此格式的 NuGet 包具有以下已知文件夹和行为：</span><span class="sxs-lookup"><span data-stu-id="935d7-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="935d7-134">文件夹</span><span class="sxs-lookup"><span data-stu-id="935d7-134">Folder</span></span> | <span data-ttu-id="935d7-135">行为</span><span class="sxs-lookup"><span data-stu-id="935d7-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="935d7-136">生成</span><span class="sxs-lookup"><span data-stu-id="935d7-136">Build</span></span> | <span data-ttu-id="935d7-137">此文件夹中包含 MSBuild 目标和属性文件将以不同的方式集成到项目中，但除此之外没有更改。</span><span class="sxs-lookup"><span data-stu-id="935d7-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="935d7-138">工具</span><span class="sxs-lookup"><span data-stu-id="935d7-138">Tools</span></span> | <span data-ttu-id="935d7-139">`install.ps1` 和 `uninstall.ps1` 不运行。</span><span class="sxs-lookup"><span data-stu-id="935d7-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="935d7-140">`init.ps1` 像往常一样工作。</span><span class="sxs-lookup"><span data-stu-id="935d7-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="935d7-141">内容</span><span class="sxs-lookup"><span data-stu-id="935d7-141">Content</span></span> | <span data-ttu-id="935d7-142">内容不会自动复制到用户的项目中。</span><span class="sxs-lookup"><span data-stu-id="935d7-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="935d7-143">后续发行版本计划支持将内容包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="935d7-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="935d7-144">Lib</span><span class="sxs-lookup"><span data-stu-id="935d7-144">Lib</span></span> | <span data-ttu-id="935d7-145">对于许多包而言，`lib` 的工作方式与 NuGet 2.x 相同，只不过其中使用的名称具有扩展选项，并且在使用包时具有更好的逻辑来选取正确的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="935d7-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="935d7-146">但是，与 `ref` 一起使用时，`lib` 文件夹包含如下程序集：实现由 `ref` 文件夹中的程序集定义的外围应用。</span><span class="sxs-lookup"><span data-stu-id="935d7-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="935d7-147">引用</span><span class="sxs-lookup"><span data-stu-id="935d7-147">Ref</span></span> | <span data-ttu-id="935d7-148">`ref` 是一个可选文件夹，其中包含 .NET 程序集，用于定义应用程序编译的公共外围（公共类型和方法）。</span><span class="sxs-lookup"><span data-stu-id="935d7-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="935d7-149">此文件夹中的程序集可能没有实现，只是用于为编译器定义外围应用。</span><span class="sxs-lookup"><span data-stu-id="935d7-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="935d7-150">如果包没有 `ref` 文件夹，那么 `lib` 同时为引用程序集和实现程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="935d7-151">运行时</span><span class="sxs-lookup"><span data-stu-id="935d7-151">Runtimes</span></span> | <span data-ttu-id="935d7-152">`runtimes` 是一个可选文件夹，其中包含操作系统特定的代码，如 CPU 体系结构以及操作系统特定的或依赖于其他平台的二进制文件。</span><span class="sxs-lookup"><span data-stu-id="935d7-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="935d7-153">包中的 MSBuild 目标和属性文件</span><span class="sxs-lookup"><span data-stu-id="935d7-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="935d7-154">NuGet 包可能包含 `.targets` 和 `.props` 文件，这些文件被导入到包安装到的任何 MSBuild 项目中。</span><span class="sxs-lookup"><span data-stu-id="935d7-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="935d7-155">在 NuGet 2.x 中，此操作是通过向 `.csproj` 文件注入 `<Import>` 语句而完成的；在 NuGet 3.0 中，没有特定的“安装到项目”操作。</span><span class="sxs-lookup"><span data-stu-id="935d7-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="935d7-156">而是包还原过程写入 `[projectname].nuget.props` 和 `[projectname].NuGet.targets` 两个文件。</span><span class="sxs-lookup"><span data-stu-id="935d7-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="935d7-157">MSBuild 知道查找这两个文件，并在项目生成过程开始和结束时自动导入它们。</span><span class="sxs-lookup"><span data-stu-id="935d7-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="935d7-158">此行为与 NuGet 2.x 非常相似，但有一个主要区别：在此情况下，无法保证目标/道属性文件的顺序。</span><span class="sxs-lookup"><span data-stu-id="935d7-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="935d7-159">但是，MSBuild 通过 `<Target>` 定义的 `BeforeTargets` 和 `AfterTargets` 特性（请参阅 [Target 元素 (MSBuild)](/visualstudio/msbuild/target-element-msbuild)）提供了对目标进行排序的方法。</span><span class="sxs-lookup"><span data-stu-id="935d7-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="935d7-160">Lib 和引用</span><span class="sxs-lookup"><span data-stu-id="935d7-160">Lib and Ref</span></span>

<span data-ttu-id="935d7-161">在 NuGet v3 中，`lib` 文件夹的行为没有重大变化。</span><span class="sxs-lookup"><span data-stu-id="935d7-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="935d7-162">但是，所有程序集都必须位于以 TxM 命名的子文件夹内，不再直接放置在 `lib` 文件夹下。</span><span class="sxs-lookup"><span data-stu-id="935d7-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="935d7-163">TxM 是包中给定资产适用的平台名称。</span><span class="sxs-lookup"><span data-stu-id="935d7-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="935d7-164">逻辑上，这些是目标框架名字对象 (TFM) 的扩展，例如，`net45`、`net46`、`netcore50` 和 `dnxcore50` 都是 TxM 的示例（请参阅[目标框架](../reference/target-frameworks.md)）。</span><span class="sxs-lookup"><span data-stu-id="935d7-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="935d7-165">TxM 可以指框架 (TFM) 以及其他平台特定的外围应用。</span><span class="sxs-lookup"><span data-stu-id="935d7-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="935d7-166">例如，UWP TxM (`uap10.0`) 表示 .NET 外围应用以及适用于 UWP 应用程序的 Windows 外围应用。</span><span class="sxs-lookup"><span data-stu-id="935d7-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="935d7-167">Lib 结构示例：</span><span class="sxs-lookup"><span data-stu-id="935d7-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="935d7-168">`lib` 文件夹包含在运行时使用的程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="935d7-169">对于大多数包而言，每个目标 TxM 的 `lib` 下的文件夹全都是必需的。</span><span class="sxs-lookup"><span data-stu-id="935d7-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="935d7-170">引用</span><span class="sxs-lookup"><span data-stu-id="935d7-170">Ref</span></span>

<span data-ttu-id="935d7-171">有时在编译期间应使用不同的程序集（如 .NET 引用程序集）。</span><span class="sxs-lookup"><span data-stu-id="935d7-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="935d7-172">对于这些情况，请使用名为 `ref`（“引用程序集”的缩写）的顶层文件夹。</span><span class="sxs-lookup"><span data-stu-id="935d7-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="935d7-173">大多数包创建者都不需要 `ref` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="935d7-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="935d7-174">这对以下包非常有用：需要为编译和 IntelliSense 提供一致的外围应用，但对不同的 TxM 具有不同的实现。</span><span class="sxs-lookup"><span data-stu-id="935d7-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="935d7-175">最大的用例是 `System.*` 包，这些包是在 NuGet 上提供 .NET Core 的过程中生成的。</span><span class="sxs-lookup"><span data-stu-id="935d7-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="935d7-176">这些包具有各种实现，这些实现由一组一致的引用程序集统一。</span><span class="sxs-lookup"><span data-stu-id="935d7-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="935d7-177">从表面上讲，`ref` 文件夹中包含的程序集是传递给编译器的引用程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="935d7-178">对于使用过 csc.exe 的用户来说，这些是我们传递给 [C# /reference 选项](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) 开关的程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="935d7-179">`ref` 文件夹的结构与 `lib` 的结构相同，例如：</span><span class="sxs-lookup"><span data-stu-id="935d7-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="935d7-180">在本例中，`ref` 目录中的程序集是相同的。</span><span class="sxs-lookup"><span data-stu-id="935d7-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="935d7-181">运行时</span><span class="sxs-lookup"><span data-stu-id="935d7-181">Runtimes</span></span>

<span data-ttu-id="935d7-182">运行时文件夹包含在特定“运行时”上运行所需的程序集和本机库，通常由操作系统和 CPU 体系结构定义。</span><span class="sxs-lookup"><span data-stu-id="935d7-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="935d7-183">这些运行时使用[运行时标识符 (RID)](/dotnet/core/rid-catalog) 进行标识，如 `win`、`win-x86`、`win7-x86`、`win8-64` 等。</span><span class="sxs-lookup"><span data-stu-id="935d7-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="935d7-184">本机启动</span><span class="sxs-lookup"><span data-stu-id="935d7-184">Native light-up</span></span>

<span data-ttu-id="935d7-185">以下示例显示这样的包：拥有适用于多个平台的纯托管实现，但可在 Windows 8 上使用本机帮助程序以调用 Windows 8 特定的本机 API。</span><span class="sxs-lookup"><span data-stu-id="935d7-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="935d7-186">提供上述包时，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="935d7-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="935d7-187">当不在 Windows 8 上，将使用 `lib/net40/MyLibrary.dll` 程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="935d7-188">在 Windows 8 上时，将使用 `runtimes/win8-<architecture>/lib/MyLibrary.dll`，并且 `native/MyNativeHelper.dll` 将复制到生成的输出。</span><span class="sxs-lookup"><span data-stu-id="935d7-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="935d7-189">在上面的示例中，`lib/net40` 程序集是纯托管代码，而运行时文件夹中的程序集将平台调用到本机帮助程序程序集中，以调用特定于 Windows 8 的 API。</span><span class="sxs-lookup"><span data-stu-id="935d7-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="935d7-190">始终仅选取单个 `lib` 文件夹，因此如果有运行时特定的文件夹，将选择通过非运行时特定的 `lib`。</span><span class="sxs-lookup"><span data-stu-id="935d7-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="935d7-191">本机文件夹是累加式的，如果存在，将被复制到生成的输出。</span><span class="sxs-lookup"><span data-stu-id="935d7-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="935d7-192">托管包装器</span><span class="sxs-lookup"><span data-stu-id="935d7-192">Managed wrapper</span></span>

<span data-ttu-id="935d7-193">使用运行时的另一种方式是将属于纯托管包装器的包提供到本机程序集上。</span><span class="sxs-lookup"><span data-stu-id="935d7-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="935d7-194">在此方案中，将创建如下所示的包：</span><span class="sxs-lookup"><span data-stu-id="935d7-194">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="935d7-195">在此情况下，没有顶层 `lib` 文件夹作为该文件夹，因为此包的实现不依赖于相应的本机程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="935d7-196">如果托管程序集 `MyLibrary.dll` 在这两种情况下完全相同，则可将它放在顶层 `lib` 文件夹中；但是，由于缺少本机程序集并不会导致将包安装到非 win-x86 或 win-x64 平台上时失败，因此将使用顶层 lib，但不会复制本机程序集。</span><span class="sxs-lookup"><span data-stu-id="935d7-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="935d7-197">创作适用于 NuGet 2 和 NuGet 3 的包</span><span class="sxs-lookup"><span data-stu-id="935d7-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="935d7-198">如果想创建一个可供使用 `packages.config` 的项目使用的包以及使用 `project.json` 的包，则以下内容适用：</span><span class="sxs-lookup"><span data-stu-id="935d7-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="935d7-199">引用和运行时只适用于 NuGet 3。</span><span class="sxs-lookup"><span data-stu-id="935d7-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="935d7-200">在 NuGet 2 中将被忽略。</span><span class="sxs-lookup"><span data-stu-id="935d7-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="935d7-201">不能依靠 `install.ps1` 或 `uninstall.ps1` 来运行。</span><span class="sxs-lookup"><span data-stu-id="935d7-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="935d7-202">这些文件在使用 `packages.config` 时执行，但使用 `project.json` 时会忽略。</span><span class="sxs-lookup"><span data-stu-id="935d7-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="935d7-203">因此包需要不运行它们时可用。</span><span class="sxs-lookup"><span data-stu-id="935d7-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="935d7-204">`init.ps1` 仍在 NuGet 3 上运行。</span><span class="sxs-lookup"><span data-stu-id="935d7-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="935d7-205">目标与属性安装不同，因此请确保包在两个客户端上按预期工作。</span><span class="sxs-lookup"><span data-stu-id="935d7-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="935d7-206">在 NuGet 3 中，lib 的子目录必须是一个 TxM。</span><span class="sxs-lookup"><span data-stu-id="935d7-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="935d7-207">不能将库放置在 `lib` 文件夹的根目录下。</span><span class="sxs-lookup"><span data-stu-id="935d7-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="935d7-208">NuGet 3 将不会自动复制内容。</span><span class="sxs-lookup"><span data-stu-id="935d7-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="935d7-209">包的使用者可以自己复制文件，或使用任务运行程序之类的工具来自动复制文件。</span><span class="sxs-lookup"><span data-stu-id="935d7-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="935d7-210">NuGet 3 不会运行源和配置文件转换。</span><span class="sxs-lookup"><span data-stu-id="935d7-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="935d7-211">如果支持 NuGet 2 和 3，`minClientVersion` 应该是包适用的最低版本的 NuGet 2 客户端。</span><span class="sxs-lookup"><span data-stu-id="935d7-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="935d7-212">如果存在现有包，则不需要更改。</span><span class="sxs-lookup"><span data-stu-id="935d7-212">In the case of an existing package it shouldn't need to change.</span></span>