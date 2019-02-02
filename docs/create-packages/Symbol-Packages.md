---
title: 如何创建 NuGet 符号包
description: 如何在 Visual Studio 中创建仅包含符号的 NuGet 包以支持调试其他 NuGet 包。
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 56125516345b2255998c1f734db60b58b9a92a06
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55046323"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="2b816-103">创建符号包（旧版）</span><span class="sxs-lookup"><span data-stu-id="2b816-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="2b816-104">符号包的新推荐格式为 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="2b816-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="2b816-105">请参阅[创建符号包 (.snupkg)](Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="2b816-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="2b816-106">.symbols.nupkg 仍受支持，但仅出于兼容性原因。</span><span class="sxs-lookup"><span data-stu-id="2b816-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="2b816-107">除了为 nuget.org 或其他源生成包之外，NuGet 还支持创建关联的符号包并将其发布到 SymbolSource 存储库。</span><span class="sxs-lookup"><span data-stu-id="2b816-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="2b816-108">然后，包使用者可将 `https://nuget.smbsrc.net` 添加到 Visual Studio 中的符号源，它允许在 Visual Studio 调试程序中单步执行包代码。</span><span class="sxs-lookup"><span data-stu-id="2b816-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="2b816-109">有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="2b816-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="2b816-110">创建符号包</span><span class="sxs-lookup"><span data-stu-id="2b816-110">Creating a symbol package</span></span>

<span data-ttu-id="2b816-111">若要创建符号包，请按照以下约定操作：</span><span class="sxs-lookup"><span data-stu-id="2b816-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="2b816-112">（使用代码）将主包命名为 `{identifier}.nupkg`，并包括除 `.pdb` 文件之外的所有文件。</span><span class="sxs-lookup"><span data-stu-id="2b816-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="2b816-113">将符号包命名为 `{identifier}.symbols.nupkg`，并包括程序集 DLL、`.pdb` 文件、XMLDOC 文件和源文件（请参阅以下各节）。</span><span class="sxs-lookup"><span data-stu-id="2b816-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="2b816-114">可使用 `-Symbols` 选项从 `.nuspec` 文件或项目文件中同时创建这两个包：</span><span class="sxs-lookup"><span data-stu-id="2b816-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="2b816-115">请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。</span><span class="sxs-lookup"><span data-stu-id="2b816-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="2b816-116">在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。</span><span class="sxs-lookup"><span data-stu-id="2b816-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="2b816-117">符号包结构</span><span class="sxs-lookup"><span data-stu-id="2b816-117">Symbol package structure</span></span>

<span data-ttu-id="2b816-118">符号包面向多个目标框架的方式可与库包的方式相同，因此 `lib` 文件夹的结构应与主包的结构完全相同，即仅包括 `.pdb` 和 DLL 文件。</span><span class="sxs-lookup"><span data-stu-id="2b816-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="2b816-119">例如，面向 .NET 4.0 和 Silverlight 4 的符号包具有以下布局：</span><span class="sxs-lookup"><span data-stu-id="2b816-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="2b816-120">然后，在名为 `src` 的单独的特殊文件夹中放入源文件，该文件夹必须遵循源存储库的相对结构。</span><span class="sxs-lookup"><span data-stu-id="2b816-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="2b816-121">这是因为 PDB 包含指向用于编译匹配 DLL 的源文件的绝对路径，在发布过程中需要找到这些路径。</span><span class="sxs-lookup"><span data-stu-id="2b816-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="2b816-122">可以去除基路径（通用路径前缀）。例如，假设从以下文件中生成一个库：</span><span class="sxs-lookup"><span data-stu-id="2b816-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="2b816-123">除了 `lib` 文件夹之外，符号包需要包含以下布局：</span><span class="sxs-lookup"><span data-stu-id="2b816-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="2b816-124">引用 nuspec 中的文件</span><span class="sxs-lookup"><span data-stu-id="2b816-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="2b816-125">可以通过约定从文件夹结构中生成符号包（如上一部分所述），也可以通过在清单的 `files` 部分中指定内容进行生成。</span><span class="sxs-lookup"><span data-stu-id="2b816-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="2b816-126">例如，若要生成上一部分中显示的包，请使用 `.nuspec` 文件中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="2b816-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="2b816-127">发布符号包</span><span class="sxs-lookup"><span data-stu-id="2b816-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="2b816-128">若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.9.1 或更高版本](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="2b816-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="2b816-129">为方便起见，请首先保存 NuGet 的 API 密钥（请参阅[发布包](../create-packages/publish-a-package.md)），它将应用于 nuget.org 和 symbolsource.org，因为 symbolsource.org 会与 nuget.org 进行核对以验证包所有者。</span><span class="sxs-lookup"><span data-stu-id="2b816-129">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="2b816-130">将主包发布到 nuget.org 后，按照以下方式推送符号包，由于文件名中的 `.symbols`，此步骤将 symbolsource.org 自动用作目标：</span><span class="sxs-lookup"><span data-stu-id="2b816-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="2b816-131">若要发布到另一符号存储库或推送不遵循命名约定的符号包，请使用 `-Source` 选项：</span><span class="sxs-lookup"><span data-stu-id="2b816-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="2b816-132">还可以使用以下项将主包和符号包同时推送到两个存储库：</span><span class="sxs-lookup"><span data-stu-id="2b816-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="2b816-133">在 nuget.exe 4.5.0 或更高版本中，符号包不会自动推送到 symbolsource.org。需要单独推送符号包，如下一步所述。</span><span class="sxs-lookup"><span data-stu-id="2b816-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="2b816-134">在此情况下，向 nuget.org 发布主包后，NuGet 将 `MyPackage.symbols.nupkg`（如果存在）发布到 https://nuget.smbsrc.net/（symbolsource.org 的推送 URL）。</span><span class="sxs-lookup"><span data-stu-id="2b816-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b816-135">请参阅</span><span class="sxs-lookup"><span data-stu-id="2b816-135">See Also</span></span>

<span data-ttu-id="2b816-136">[移动到新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="2b816-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
