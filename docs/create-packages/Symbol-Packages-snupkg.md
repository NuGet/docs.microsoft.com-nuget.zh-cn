---
title: 如何使用新的符号包格式“.snupkg”发布 NuGet 符号包 | Microsoft Docs
author: JonDouglas
ms.author: jodou
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
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387330"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="dc4f2-104">创建符号包 (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="dc4f2-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="dc4f2-105">良好的调试体验依赖于调试符号的存在，因为它们提供了一些关键信息，例如已编译的代码与源代码之间的关联、局部变量的名称、堆栈跟踪等。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="dc4f2-106">你可以使用符号包 (.snupkg) 来分发这些符号，并改善 NuGet 包的调试体验。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

> <span data-ttu-id="dc4f2-107">请注意，符号包并不是使调试符号可用于库使用者的唯一策略。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-107">Note that symbol package isn't the only strategy to make the debug symbols available to the consumers of your library.</span></span> <span data-ttu-id="dc4f2-108">还[可以通过以下项目属性在 `dll` 或 `exe` 中 `embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) 它们：`<DebugType>embedded</DebugType>`</span><span class="sxs-lookup"><span data-stu-id="dc4f2-108">It's also [possible to `embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) them in the `dll` or `exe` with the following project property: `<DebugType>embedded</DebugType>`</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc4f2-109">必备条件</span><span class="sxs-lookup"><span data-stu-id="dc4f2-109">Prerequisites</span></span>

<span data-ttu-id="dc4f2-110">[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet CLI v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-110">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="dc4f2-111">创建符号包</span><span class="sxs-lookup"><span data-stu-id="dc4f2-111">Creating a symbol package</span></span>

<span data-ttu-id="dc4f2-112">如果使用 dotnet CLI 或 MSBuild，则除 .nupkg 文件外，还需要设置 `IncludeSymbols` 和 `SymbolPackageFormat` 属性以创建 .snupkg 文件。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-112">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="dc4f2-113">要么将以下属性添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-113">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="dc4f2-114">要么在命令行上指定这些属性：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-114">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="dc4f2-115">或</span><span class="sxs-lookup"><span data-stu-id="dc4f2-115">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="dc4f2-116">如果使用 NuGet.exe，除 .nupkg 文件外，可以使用以下命令创建一个 .snupkg 文件：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-116">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="dc4f2-117">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性可以有下列两个值之一：`symbols.nupkg`（默认值）或 `snupkg`。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-117">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="dc4f2-118">如果未指定此属性，将会创建旧的符号包。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-118">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="dc4f2-119">旧格式 `.symbols.nupkg` 仍受支持，但只是出于兼容性的原因，例如本机包（请参阅[旧版符号包](Symbol-Packages.md)）。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-119">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="dc4f2-120">NuGet.org 的符号服务器只接受新的符号包格式，即 `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-120">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="dc4f2-121">发布符号包</span><span class="sxs-lookup"><span data-stu-id="dc4f2-121">Publishing a symbol package</span></span>

1. <span data-ttu-id="dc4f2-122">为方便起见，首先使用 NuGet 保存 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)）。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-122">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="dc4f2-123">将主包发布到 nuget.org 后，按如下方式推送符号包。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-123">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="dc4f2-124">还可以使用以下命令同时推送主包和符号包。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-124">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="dc4f2-125">当前文件夹中必须同时有 .nupkg 和 .snupkg 文件。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-125">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="dc4f2-126">NuGet 会将两个包发布到 nuget.org。`MyPackage.nupkg` 先发布，随后 `MyPackage.snupkg` 发布。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-126">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="dc4f2-127">如果没有发布符号包，请检查是否已将 NuGet.org 源配置为 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-127">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="dc4f2-128">只有 [NuGet V3 API](../api/overview.md#versioning) 才支持符号包发布。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-128">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="dc4f2-129">NuGet.org 符号服务器</span><span class="sxs-lookup"><span data-stu-id="dc4f2-129">NuGet.org symbol server</span></span>

<span data-ttu-id="dc4f2-130">NuGet.org 支持自己的符号服务器存储库，只接受新的符号包格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-130">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="dc4f2-131">包使用者可将 `https://symbols.nuget.org/download/symbols` 添加到 Visual Studio 中的符号源，使用发布到 nuget.org 符号服务器的符号，这允许在 Visual Studio 调试程序中单步执行包代码。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-131">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="dc4f2-132">有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-132">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="dc4f2-133">NuGet.org 符号包约束</span><span class="sxs-lookup"><span data-stu-id="dc4f2-133">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="dc4f2-134">NuGet.org 对符号包具有以下约束：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-134">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="dc4f2-135">符号包中仅允许使用以下文件扩展名：`.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`</span><span class="sxs-lookup"><span data-stu-id="dc4f2-135">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="dc4f2-136">NuGet.org 符号服务器目前仅支持托管的[可移植 PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-136">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="dc4f2-137">需要使用 Visual Studio 15.9 或更高版本中的编译器构建 PDB 及其关联的 nupkg DLL（请参阅 [PDB 加密哈希](https://github.com/dotnet/roslyn/issues/24429)）</span><span class="sxs-lookup"><span data-stu-id="dc4f2-137">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="dc4f2-138">如果未满足这些约束，则发布到 NuGet.org 的符号包将无法通过验证。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-138">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc4f2-139">本机项目（如 C++ 项目）生成 Windows PDB，而不是可移植的 PDB。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-139">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="dc4f2-140">NuGet.org 的符号服务器不支持这些 PDB。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-140">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="dc4f2-141">请改用[旧版符号包](Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-141">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="dc4f2-142">符号包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="dc4f2-142">Symbol package validation and indexing</span></span>

<span data-ttu-id="dc4f2-143">发布到 [NuGet.org](https://www.nuget.org/) 的符号包会接受多项验证，包括恶意软件扫描。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-143">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="dc4f2-144">如果包未通过验证检查，则其包详细信息页将显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-144">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="dc4f2-145">此外，包的所有者还将收到一封电子邮件，其中包含有关如何解决已识别问题的说明。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-145">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="dc4f2-146">当符号包通过所有验证后，NuGet.org 的符号服务器将为其中的符号编制索引，并且这些符号将可供使用。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-146">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="dc4f2-147">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-147">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="dc4f2-148">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 NuGet.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-148">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="dc4f2-149">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包详细信息页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-149">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="dc4f2-150">符号包结构</span><span class="sxs-lookup"><span data-stu-id="dc4f2-150">Symbol package structure</span></span>

<span data-ttu-id="dc4f2-151">符号包 (.snupkg) 具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-151">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="dc4f2-152">.snupkg 与相应的 NuGet 包 (.nupkg) 具有相同的 ID 和版本。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-152">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="dc4f2-153">.snupkg 具有与任何 DLL 或 EXE 文件的相应 .nupkg 相同的文件夹结构，区别在于其相应的 PDB 将包含在同一文件夹层次结构中，而不是 DLL/EXE 中。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-153">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="dc4f2-154">扩展名不是 PDB 的文件和文件夹将被排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-154">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="dc4f2-155">符号包的 .nuspec 文件具有 `SymbolsPackage` 包类型：</span><span class="sxs-lookup"><span data-stu-id="dc4f2-155">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="dc4f2-156">如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-156">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="dc4f2-157">将从 snupkg 的 nuspec 中排除以下字段：```authors```、```owners```、```requireLicenseAcceptance```、```license type```、```licenseUrl``` 和 ```icon```。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-157">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="dc4f2-158">不要使用 ```<license>``` 元素。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-158">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="dc4f2-159">.snupkg 与对应的 .nupk 位于同一个许可证中。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-159">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="dc4f2-160">另请参阅</span><span class="sxs-lookup"><span data-stu-id="dc4f2-160">See also</span></span>

<span data-ttu-id="dc4f2-161">考虑使用源链接来启用 .NET 程序集的源代码调试。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-161">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="dc4f2-162">有关详细信息，请参阅[源链接指南](/dotnet/standard/library-guidance/sourcelink)。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-162">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="dc4f2-163">有关符号包的更多信息，请参阅 [NuGet 包调试与符号改进](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)设计规范。</span><span class="sxs-lookup"><span data-stu-id="dc4f2-163">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>