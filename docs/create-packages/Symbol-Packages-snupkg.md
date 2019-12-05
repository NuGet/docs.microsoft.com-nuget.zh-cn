---
title: 如何使用新的符号包格式“.snupkg”发布 NuGet 符号包 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 如何创建 NuGet 符号包 (snupkg)。
keywords: NuGet 符号包, NuGet 包调试, 支持 NuGet 调试, 包符号, 符号包约定
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 8528261f90e75e2dfac8cb746b396d227c3741f4
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825177"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="a6175-104">创建符号包 (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="a6175-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="a6175-105">通过符号包可以提高 NuGet 包的调试体验。</span><span class="sxs-lookup"><span data-stu-id="a6175-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6175-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="a6175-106">Prerequisites</span></span>

<span data-ttu-id="a6175-107">[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet.exe v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="a6175-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="a6175-108">创建符号包</span><span class="sxs-lookup"><span data-stu-id="a6175-108">Creating a symbol package</span></span>

<span data-ttu-id="a6175-109">如果使用 dotnet.exe 或 MSBuild，则除 .nupkg 文件外，还需要设置 `IncludeSymbols` 和 `SymbolPackageFormat` 属性创建 .snupkg 文件。</span><span class="sxs-lookup"><span data-stu-id="a6175-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="a6175-110">要么将以下属性添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="a6175-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="a6175-111">要么在命令行上指定这些属性：</span><span class="sxs-lookup"><span data-stu-id="a6175-111">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="a6175-112">or</span><span class="sxs-lookup"><span data-stu-id="a6175-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="a6175-113">如果使用 NuGet.exe，除 .nupkg 文件外，可以使用以下命令创建一个 .snupkg 文件：</span><span class="sxs-lookup"><span data-stu-id="a6175-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="a6175-114">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性可以有下列两个值之一：`symbols.nupkg`（默认值）或 `snupkg`。</span><span class="sxs-lookup"><span data-stu-id="a6175-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="a6175-115">如果未指定此属性，将会创建旧的符号包。</span><span class="sxs-lookup"><span data-stu-id="a6175-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="a6175-116">仍支持旧格式 `.symbols.nupkg`，但仅出于兼容性原因（请参阅[旧版符号包](Symbol-Packages.md)）。</span><span class="sxs-lookup"><span data-stu-id="a6175-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="a6175-117">NuGet.org 的符号服务器只接受新的符号包格式，即 `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="a6175-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="a6175-118">发布符号包</span><span class="sxs-lookup"><span data-stu-id="a6175-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="a6175-119">为方便起见，首先使用 NuGet 保存 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)）。</span><span class="sxs-lookup"><span data-stu-id="a6175-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="a6175-120">将主包发布到 nuget.org 后，按如下方式推送符号包。</span><span class="sxs-lookup"><span data-stu-id="a6175-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="a6175-121">还可以使用以下命令同时推送主包和符号包。</span><span class="sxs-lookup"><span data-stu-id="a6175-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="a6175-122">当前文件夹中必须同时有 .nupkg 和 .snupkg 文件。</span><span class="sxs-lookup"><span data-stu-id="a6175-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="a6175-123">NuGet 会将两个包发布到 nuget.org。`MyPackage.nupkg` 先发布，随后 `MyPackage.snupkg` 发布。</span><span class="sxs-lookup"><span data-stu-id="a6175-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="a6175-124">如果没有发布符号包，请检查是否已将 NuGet.org 源配置为 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="a6175-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="a6175-125">只有 [NuGet V3 API](../api/overview.md#versioning) 才支持符号包发布。</span><span class="sxs-lookup"><span data-stu-id="a6175-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="a6175-126">NuGet.org 符号服务器</span><span class="sxs-lookup"><span data-stu-id="a6175-126">NuGet.org symbol server</span></span>

<span data-ttu-id="a6175-127">NuGet.org 支持自己的符号服务器存储库，只接受新的符号包格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="a6175-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="a6175-128">包使用者可将 `https://symbols.nuget.org/download/symbols` 添加到 Visual Studio 中的符号源，使用发布到 nuget.org 符号服务器的符号，这允许在 Visual Studio 调试程序中单步执行包代码。</span><span class="sxs-lookup"><span data-stu-id="a6175-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="a6175-129">有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="a6175-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="a6175-130">NuGet.org 符号包约束</span><span class="sxs-lookup"><span data-stu-id="a6175-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="a6175-131">NuGet.org 对符号包具有以下约束：</span><span class="sxs-lookup"><span data-stu-id="a6175-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="a6175-132">符号包中仅允许使用以下文件扩展名：`.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`</span><span class="sxs-lookup"><span data-stu-id="a6175-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="a6175-133">NuGet.org 符号服务器目前仅支持托管的[可移植 PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。</span><span class="sxs-lookup"><span data-stu-id="a6175-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="a6175-134">需要使用 Visual Studio 15.9 或更高版本中的编译器构建 PDB 及其关联的 nupkg DLL（请参阅 [PDB 加密哈希](https://github.com/dotnet/roslyn/issues/24429)）</span><span class="sxs-lookup"><span data-stu-id="a6175-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="a6175-135">如果未满足这些约束，则发布到 NuGet.org 的符号包将无法通过验证。</span><span class="sxs-lookup"><span data-stu-id="a6175-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="a6175-136">符号包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="a6175-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="a6175-137">发布到 [NuGet.org](https://www.nuget.org/) 的符号包会接受多项验证，包括恶意软件扫描。</span><span class="sxs-lookup"><span data-stu-id="a6175-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="a6175-138">如果包未通过验证检查，则其包详细信息页将显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="a6175-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="a6175-139">此外，包的所有者还将收到一封电子邮件，其中包含有关如何解决已识别问题的说明。</span><span class="sxs-lookup"><span data-stu-id="a6175-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="a6175-140">当符号包通过所有验证后，NuGet.org 的符号服务器将为其中的符号编制索引。</span><span class="sxs-lookup"><span data-stu-id="a6175-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="a6175-141">编制索引后，NuGet.org 符号服务器即可使用这些符号。</span><span class="sxs-lookup"><span data-stu-id="a6175-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="a6175-142">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="a6175-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="a6175-143">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 NuGet.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="a6175-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="a6175-144">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包详细信息页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="a6175-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="a6175-145">符号包结构</span><span class="sxs-lookup"><span data-stu-id="a6175-145">Symbol package structure</span></span>

<span data-ttu-id="a6175-146">.nupkg 文件将和现在一模一样，但 .snupkg 文件具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="a6175-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="a6175-147">.snupkg 将具有与相应 .nupkg 相同的 ID 和版本。</span><span class="sxs-lookup"><span data-stu-id="a6175-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="a6175-148">.snupkg 将具有与任何 DLL 或 EXE 文件的 nupkg 完全相同的文件夹结构，区别在于其相应的 PDB 将包含在同一文件夹层次结构中，而不是 DLL/EXE 中。</span><span class="sxs-lookup"><span data-stu-id="a6175-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="a6175-149">扩展名不是 PDB 的文件和文件夹将被排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="a6175-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="a6175-150">.snupkg 中的 .nuspec 文件还将指定一个新的 PackageType，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6175-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="a6175-151">这应该是唯一指定的 PackageType。</span><span class="sxs-lookup"><span data-stu-id="a6175-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="a6175-152">如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。</span><span class="sxs-lookup"><span data-stu-id="a6175-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="a6175-153">将从 snupkg 的 nuspec 中排除 ```authors``` 和 ```owners``` 字段。</span><span class="sxs-lookup"><span data-stu-id="a6175-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="a6175-154">不要使用 ```<license>``` 元素。</span><span class="sxs-lookup"><span data-stu-id="a6175-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="a6175-155">.snupkg 与对应的 .nupk 位于同一个许可证中。</span><span class="sxs-lookup"><span data-stu-id="a6175-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="a6175-156">请参阅</span><span class="sxs-lookup"><span data-stu-id="a6175-156">See also</span></span>

<span data-ttu-id="a6175-157">考虑使用源链接来启用 .NET 程序集的源代码调试。</span><span class="sxs-lookup"><span data-stu-id="a6175-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="a6175-158">有关详细信息，请参阅[源链接指南](/dotnet/standard/library-guidance/sourcelink)。</span><span class="sxs-lookup"><span data-stu-id="a6175-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="a6175-159">有关符号包的更多信息，请参阅 [NuGet 包调试与符号改进](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)设计规范。</span><span class="sxs-lookup"><span data-stu-id="a6175-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
