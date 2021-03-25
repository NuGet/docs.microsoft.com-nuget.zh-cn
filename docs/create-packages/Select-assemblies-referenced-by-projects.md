---
title: 选择项目引用的程序集
description: 使包中的程序集子集可用于编译器，而所有程序集在运行时都可用。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859026"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="9984b-103">选择项目引用的程序集</span><span class="sxs-lookup"><span data-stu-id="9984b-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="9984b-104">显式程序集引用允许将程序集的子集用于 IntelliSense 和编译，而所有程序集在运行时都可用。</span><span class="sxs-lookup"><span data-stu-id="9984b-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="9984b-105">`PackageReference` 和 `packages.config` 的工作方式不同，因此包创建者需要注意创建与两种项目类型兼容的包。</span><span class="sxs-lookup"><span data-stu-id="9984b-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="9984b-106">显式程序集引用与 .NET 程序集相关。</span><span class="sxs-lookup"><span data-stu-id="9984b-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="9984b-107">它不是用于分发托管程序集调用的本机程序集的方法。</span><span class="sxs-lookup"><span data-stu-id="9984b-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="9984b-108">`PackageReference` 支持</span><span class="sxs-lookup"><span data-stu-id="9984b-108">`PackageReference` support</span></span>

<span data-ttu-id="9984b-109">当一个项目使用一个带有 `PackageReference` 的包，并且该包包含一个 `ref\<tfm>\` 目录时，NuGet 会将这些组件分类为编译时资产，而 `lib\<tfm>\` 程序集则归类为运行时资产。</span><span class="sxs-lookup"><span data-stu-id="9984b-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="9984b-110">`ref\<tfm>\` 中的程序集不在运行时使用。</span><span class="sxs-lookup"><span data-stu-id="9984b-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="9984b-111">这意味着 `ref\<tfm>\` 中的任何程序集都必须在 `lib\<tfm>\` 或相关的 `runtime\` 目录中具有匹配的程序集，否则可能会发生运行时错误。</span><span class="sxs-lookup"><span data-stu-id="9984b-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="9984b-112">由于 `ref\<tfm>\` 中的程序集未在运行时使用，因此可以使用[“仅元数据”专用程序集](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)来减小包的大小。</span><span class="sxs-lookup"><span data-stu-id="9984b-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="9984b-113">如果包中包含 nuspec `<references>` 元素（由 `packages.config` 使用，请参见下文）并且不包含 `ref\<tfm>\` 中的程序集，NuGet 会将 nuspec `<references>` 元素中列出的程序集作为编译和运行时资产进行播发。</span><span class="sxs-lookup"><span data-stu-id="9984b-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="9984b-114">这意味着当引用的程序集需要加载 `lib\<tfm>\` 目录中的任何其他程序集时，将存在运行时异常。</span><span class="sxs-lookup"><span data-stu-id="9984b-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="9984b-115">如果包包含 `runtime\` 目录，则 NuGet 可能不会使用 `lib\` 目录中的资产。</span><span class="sxs-lookup"><span data-stu-id="9984b-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="9984b-116">`packages.config` 支持</span><span class="sxs-lookup"><span data-stu-id="9984b-116">`packages.config` support</span></span>

<span data-ttu-id="9984b-117">使用 `packages.config` 管理 NuGet 包的项目通常会向 `lib\<tfm>\` 目录中的所有程序集添加引用。</span><span class="sxs-lookup"><span data-stu-id="9984b-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="9984b-118">添加 `ref\` 目录以支持 `PackageReference`，因此在使用 `packages.config` 时不予考虑。</span><span class="sxs-lookup"><span data-stu-id="9984b-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="9984b-119">要使用 `packages.config` 以显式方式设置项目引用的程序集，包必须使用 [nuspec 文件中的 `<references>` 元素](../reference/nuspec.md#explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="9984b-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="9984b-120">例如：</span><span class="sxs-lookup"><span data-stu-id="9984b-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="9984b-121">`packages.config` 项目使用名为 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) 的进程将程序集复制到 `bin\<configuration>\` 输出目录。</span><span class="sxs-lookup"><span data-stu-id="9984b-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="9984b-122">复制项目的程序集，然后构建系统查看引用程序集的程序集清单，然后复制这些程序集并递归重复所有程序集。</span><span class="sxs-lookup"><span data-stu-id="9984b-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="9984b-123">这意味着，如果 `lib\<tfm>\` 目录中的任何程序集不在任何其他程序集的清单中作为依赖项列出（如果在运行时使用 `Assembly.Load`、MEF 或其他依赖项注入框架加载程序集）那么即使在 `bin\<tfm>\` 中，也不能将其复制到项目的 `bin\<configuration>\` 输出目录中。</span><span class="sxs-lookup"><span data-stu-id="9984b-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="9984b-124">示例</span><span class="sxs-lookup"><span data-stu-id="9984b-124">Example</span></span>

<span data-ttu-id="9984b-125">我的包将包含三个程序集 `MyLib.dll``MyHelpers.dll` 和 `MyUtilities.dll`，它们以 .NET Framework 4.7.2 为目标。</span><span class="sxs-lookup"><span data-stu-id="9984b-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="9984b-126">`MyUtilities.dll` 包含仅供其他两个程序集使用的类，因此我不希望在 IntelliSense 中或在编译时将这些类用于使用我的包的项目。</span><span class="sxs-lookup"><span data-stu-id="9984b-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="9984b-127">我的 `nuspec` 文件需要包含以下 XML 元素：</span><span class="sxs-lookup"><span data-stu-id="9984b-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="9984b-128">并且包中的文件将为：</span><span class="sxs-lookup"><span data-stu-id="9984b-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
