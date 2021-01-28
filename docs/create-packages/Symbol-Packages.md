---
title: 创建旧式符号包 (.symbols.nupkg)
description: 如何在 Visual Studio 中创建仅包含符号的 NuGet 包以支持调试其他 NuGet 包。
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774543"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="c8242-103">创建旧式符号包 (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="c8242-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="c8242-104">符号包的新推荐格式为 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="c8242-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="c8242-105">请参阅[创建符号包 (.snupkg)](Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="c8242-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="c8242-106">.symbols.nupkg 仍受支持，但仅出于兼容性原因。</span><span class="sxs-lookup"><span data-stu-id="c8242-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="c8242-107">除了为 nuget.org 或其他源生成包之外，NuGet 还支持创建可发布到符号服务器的关联符号包。</span><span class="sxs-lookup"><span data-stu-id="c8242-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="c8242-108">旧式符号包格式 .symbols.nupkg 可以推送到 SymbolSource 存储库。</span><span class="sxs-lookup"><span data-stu-id="c8242-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="c8242-109">然后，包使用者可将 `https://nuget.smbsrc.net` 添加到 Visual Studio 中的符号源，它允许在 Visual Studio 调试程序中单步执行包代码。</span><span class="sxs-lookup"><span data-stu-id="c8242-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="c8242-110">有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="c8242-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="c8242-111">创建旧式符号包</span><span class="sxs-lookup"><span data-stu-id="c8242-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="c8242-112">若要创建旧式符号包，请按照以下约定操作：</span><span class="sxs-lookup"><span data-stu-id="c8242-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="c8242-113">（使用代码）将主包命名为 `{identifier}.nupkg`，并包括除 `.pdb` 文件之外的所有文件。</span><span class="sxs-lookup"><span data-stu-id="c8242-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="c8242-114">将旧式符号包命名为 `{identifier}.symbols.nupkg`，并包括程序集 DLL、`.pdb` 文件、XMLDOC 文件和源文件（请参阅以下各节）。</span><span class="sxs-lookup"><span data-stu-id="c8242-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="c8242-115">可使用 `-Symbols` 选项从 `.nuspec` 文件或项目文件中同时创建这两个包：</span><span class="sxs-lookup"><span data-stu-id="c8242-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="c8242-116">请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。</span><span class="sxs-lookup"><span data-stu-id="c8242-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="c8242-117">在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。</span><span class="sxs-lookup"><span data-stu-id="c8242-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="c8242-118">旧式符号包结构</span><span class="sxs-lookup"><span data-stu-id="c8242-118">Legacy symbol package structure</span></span>

<span data-ttu-id="c8242-119">旧式符号包面向多个目标框架的方式可与库包的方式相同，因此 `lib` 文件夹的结构应与主包的结构完全相同，即仅包括 `.pdb` 和 DLL 文件。</span><span class="sxs-lookup"><span data-stu-id="c8242-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="c8242-120">例如，面向 .NET 4.0 和 Silverlight 4 的旧式符号包具有以下布局：</span><span class="sxs-lookup"><span data-stu-id="c8242-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

<span data-ttu-id="c8242-121">然后，在名为 `src` 的单独的特殊文件夹中放入源文件，该文件夹必须遵循源存储库的相对结构。</span><span class="sxs-lookup"><span data-stu-id="c8242-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="c8242-122">这是因为 PDB 包含指向用于编译匹配 DLL 的源文件的绝对路径，在发布过程中需要找到这些路径。</span><span class="sxs-lookup"><span data-stu-id="c8242-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="c8242-123">可以去除基路径（通用路径前缀）。例如，假设从以下文件中生成一个库：</span><span class="sxs-lookup"><span data-stu-id="c8242-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

```
C:\Projects
    \MyProject
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
            \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs
            \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)
```

<span data-ttu-id="c8242-124">除了 `lib` 文件夹之外，旧式符号包需要包含以下布局：</span><span class="sxs-lookup"><span data-stu-id="c8242-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

```
\src
    \Common
        \MyClass.cs
    \Full
        \Properties
            \AssemblyInfo.cs
    \Silverlight
        \Properties
            \AssemblyInfo.cs
        \MySilverlightExtensions.cs
```

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="c8242-125">引用 nuspec 中的文件</span><span class="sxs-lookup"><span data-stu-id="c8242-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="c8242-126">可以通过约定从文件夹结构中生成旧式符号包（如上一部分所述），也可以通过在清单的 `files` 部分中指定内容进行生成。</span><span class="sxs-lookup"><span data-stu-id="c8242-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="c8242-127">例如，若要生成上一部分中显示的包，请使用 `.nuspec` 文件中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="c8242-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="c8242-128">发布旧式符号包</span><span class="sxs-lookup"><span data-stu-id="c8242-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="c8242-129">若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.9.1 或更高版本](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="c8242-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="c8242-130">为方便起见，请首先保存 NuGet 的 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)），它将应用于 nuget.org 和 symbolsource.org，因为 symbolsource.org 会与 nuget.org 进行核对以验证包所有者。</span><span class="sxs-lookup"><span data-stu-id="c8242-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="c8242-131">将主包发布到 nuget.org 后，按照以下方式推送旧式符号包，由于文件名中的 `.symbols`，此步骤将 symbolsource.org 自动用作目标：</span><span class="sxs-lookup"><span data-stu-id="c8242-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="c8242-132">若要发布到另一符号存储库或推送不遵循命名约定的旧式符号包，请使用 `-Source` 选项：</span><span class="sxs-lookup"><span data-stu-id="c8242-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="c8242-133">还可以使用以下项将主包和符号包同时推送到两个存储库：</span><span class="sxs-lookup"><span data-stu-id="c8242-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="c8242-134">在 nuget.exe 4.5.0 或更高版本中，符号包不会自动推送到 symbolsource.org。需要单独推送符号包，如前面步骤所述。</span><span class="sxs-lookup"><span data-stu-id="c8242-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="c8242-135">在此情况下，向 nuget.org 发布主包后，NuGet 将 `MyPackage.symbols.nupkg`（如果存在）发布到 https://nuget.smbsrc.net/ （symbolsource.org 的推送 URL）。</span><span class="sxs-lookup"><span data-stu-id="c8242-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="c8242-136">请参阅</span><span class="sxs-lookup"><span data-stu-id="c8242-136">See also</span></span>

* <span data-ttu-id="c8242-137">[创建符号包 (.snupkg)](Symbol-Packages-snupkg.md) - 符号包的新推荐格式</span><span class="sxs-lookup"><span data-stu-id="c8242-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="c8242-138">[移动到新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="c8242-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
