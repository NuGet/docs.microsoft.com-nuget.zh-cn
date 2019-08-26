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
ms.openlocfilehash: 992b3ddd04a1bb34e7aca25dfaa6f7df5485907b
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564544"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="8462a-104">创建符号包 (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="8462a-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="8462a-105">通过符号包可以提高 NuGet 包的调试体验。</span><span class="sxs-lookup"><span data-stu-id="8462a-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8462a-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="8462a-106">Prerequisites</span></span>

<span data-ttu-id="8462a-107">[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet.exe v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="8462a-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="8462a-108">创建符号包</span><span class="sxs-lookup"><span data-stu-id="8462a-108">Creating a symbol package</span></span>

<span data-ttu-id="8462a-109">可以使用 dotnet.exe、NuGet.exe 或 MSBuild 创建 snupkg 包。</span><span class="sxs-lookup"><span data-stu-id="8462a-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="8462a-110">如果使用 NuGet.exe，除 .nupkg 文件外，可以使用以下命令创建一个 .snupkg 文件：</span><span class="sxs-lookup"><span data-stu-id="8462a-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="8462a-111">如果使用 dotnet.exe 或 MSBuild，除 .nupkg 文件外，可以通过以下步骤创建一个 .snupkg 文件：</span><span class="sxs-lookup"><span data-stu-id="8462a-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="8462a-112">将以下属性添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="8462a-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="8462a-113">使用 `dotnet pack MyPackage.csproj` 或 `msbuild -t:pack MyPackage.csproj` 打包项目。</span><span class="sxs-lookup"><span data-stu-id="8462a-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="8462a-114">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性可以有下列两个值之一：`symbols.nupkg`（默认值）或 `snupkg`。</span><span class="sxs-lookup"><span data-stu-id="8462a-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="8462a-115">如果未指定 [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性，将会创建旧的符号包。</span><span class="sxs-lookup"><span data-stu-id="8462a-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="8462a-116">仍支持旧格式 `.symbols.nupkg`，但仅出于兼容性原因（请参阅[旧版符号包](Symbol-Packages.md)）。</span><span class="sxs-lookup"><span data-stu-id="8462a-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="8462a-117">NuGet.org 的符号服务器只接受新的符号包格式，即 `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="8462a-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="8462a-118">发布符号包</span><span class="sxs-lookup"><span data-stu-id="8462a-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="8462a-119">为方便起见，首先使用 NuGet 保存 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)）。</span><span class="sxs-lookup"><span data-stu-id="8462a-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="8462a-120">将主包发布到 nuget.org 后，按如下方式推送符号包。</span><span class="sxs-lookup"><span data-stu-id="8462a-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="8462a-121">还可以使用以下命令同时推送主包和符号包。</span><span class="sxs-lookup"><span data-stu-id="8462a-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="8462a-122">当前文件夹中必须同时有 .nupkg 和 .snupkg 文件。</span><span class="sxs-lookup"><span data-stu-id="8462a-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="8462a-123">NuGet 会将两个包发布到 nuget.org。`MyPackage.nupkg` 先发布，随后 `MyPackage.snupkg` 发布。</span><span class="sxs-lookup"><span data-stu-id="8462a-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="8462a-124">如果没有发布符号包，请检查是否已将 NuGet.org 源配置为 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="8462a-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8462a-125">只有 [NuGet V3 API](../api/overview.md#versioning) 才支持符号包发布。</span><span class="sxs-lookup"><span data-stu-id="8462a-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="8462a-126">NuGet.org 符号服务器</span><span class="sxs-lookup"><span data-stu-id="8462a-126">NuGet.org symbol server</span></span>

<span data-ttu-id="8462a-127">NuGet.org 支持自己的符号服务器存储库，只接受新的符号包格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="8462a-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="8462a-128">包使用者可将 `https://symbols.nuget.org/download/symbols` 添加到 Visual Studio 中的符号源，使用发布到 nuget.org 符号服务器的符号，这允许在 Visual Studio 调试程序中单步执行包代码。</span><span class="sxs-lookup"><span data-stu-id="8462a-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="8462a-129">有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)。</span><span class="sxs-lookup"><span data-stu-id="8462a-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="8462a-130">Nuget.org 符号包约束</span><span class="sxs-lookup"><span data-stu-id="8462a-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="8462a-131">nuget.org 上支持的符号包具有以下约束</span><span class="sxs-lookup"><span data-stu-id="8462a-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="8462a-132">只允许将以下文件扩展名添加到符号包中。</span><span class="sxs-lookup"><span data-stu-id="8462a-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="8462a-133">nuget 符号服务器目前仅支持托管的[可移植 pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。</span><span class="sxs-lookup"><span data-stu-id="8462a-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="8462a-134">需要使用 Visual Studio 15.9 或更高版本中的编译器构建 pdb 和关联的 nupkg dll（请参阅 [pdb 加密哈希](https://github.com/dotnet/roslyn/issues/24429)）</span><span class="sxs-lookup"><span data-stu-id="8462a-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="8462a-135">如果 .snupkg 中包含任何其他文件类型，则 nuget.org 上的符号包发布将失败。</span><span class="sxs-lookup"><span data-stu-id="8462a-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="8462a-136">符号包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="8462a-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="8462a-137">发布到 [NuGet.org](https://www.nuget.org/) 的符号包会进行多项验证，如病毒检查。</span><span class="sxs-lookup"><span data-stu-id="8462a-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="8462a-138">包通过所有验证检查后，符号可能需要一段时间才能编入索引和从 NuGet.org 符号服务器中使用。</span><span class="sxs-lookup"><span data-stu-id="8462a-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="8462a-139">如果包未通过验证检查，将更新 .nupkg 包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8462a-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="8462a-140">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="8462a-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="8462a-141">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="8462a-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="8462a-142">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包详细信息页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="8462a-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="8462a-143">符号包结构</span><span class="sxs-lookup"><span data-stu-id="8462a-143">Symbol package structure</span></span>

<span data-ttu-id="8462a-144">.nupkg 文件将和现在一模一样，但 .snupkg 文件具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="8462a-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="8462a-145">.snupkg 将具有与相应 .nupkg 相同的 ID 和版本。</span><span class="sxs-lookup"><span data-stu-id="8462a-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="8462a-146">.snupkg 将具有与任何 DLL 或 EXE 文件的 nupkg 完全相同的文件夹结构，区别在于其相应的 PDB 将包含在同一文件夹层次结构中，而不是 DLL/EXE 中。</span><span class="sxs-lookup"><span data-stu-id="8462a-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="8462a-147">扩展名不是 PDB 的文件和文件夹将被排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="8462a-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="8462a-148">.snupkg 中的 .nuspec 文件还将指定一个新的 PackageType，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8462a-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="8462a-149">这应该是唯一指定的 PackageType。</span><span class="sxs-lookup"><span data-stu-id="8462a-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="8462a-150">如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。</span><span class="sxs-lookup"><span data-stu-id="8462a-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="8462a-151">将从 snupkg 的 nuspec 中排除 ```authors``` 和 ```owners``` 字段。</span><span class="sxs-lookup"><span data-stu-id="8462a-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="8462a-152">不要使用 <license> 元素。</span><span class="sxs-lookup"><span data-stu-id="8462a-152">Do not use the <license> element.</span></span> <span data-ttu-id="8462a-153">.snupkg 与对应的 .nupk 位于同一个许可证中。</span><span class="sxs-lookup"><span data-stu-id="8462a-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="8462a-154">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8462a-154">See Also</span></span>

[<span data-ttu-id="8462a-155">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="8462a-155">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
