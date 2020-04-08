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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380413"
---
# <a name="creating-symbol-packages-snupkg"></a>创建符号包 (.snupkg)

良好的调试体验依赖于调试符号的存在，因为它们提供了一些关键信息，例如已编译的代码与源代码之间的关联、局部变量的名称、堆栈跟踪等。 你可以使用符号包 (.snupkg) 来分发这些符号，并改善 NuGet 包的调试体验。

## <a name="prerequisites"></a>必备条件

[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet CLI v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>创建符号包

如果使用 dotnet CLI 或 MSBuild，则除 .nupkg 文件外，还需要设置 `IncludeSymbols` 和 `SymbolPackageFormat` 属性以创建 .snupkg 文件。

* 要么将以下属性添加到 .csproj 文件：

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* 要么在命令行上指定这些属性：

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  或

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

如果使用 NuGet.exe，除 .nupkg 文件外，可以使用以下命令创建一个 .snupkg 文件：

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性可以有下列两个值之一：`symbols.nupkg`（默认值）或 `snupkg`。 如果未指定此属性，将会创建旧的符号包。

> [!Note]
> 仍支持旧格式 `.symbols.nupkg`，但仅出于兼容性原因（请参阅[旧版符号包](Symbol-Packages.md)）。 NuGet.org 的符号服务器只接受新的符号包格式，即 `.snupkg`。

## <a name="publishing-a-symbol-package"></a>发布符号包

1. 为方便起见，首先使用 NuGet 保存 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)）。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. 将主包发布到 nuget.org 后，按如下方式推送符号包。

    ```cli
    nuget push MyPackage.snupkg
    ```

1. 还可以使用以下命令同时推送主包和符号包。 当前文件夹中必须同时有 .nupkg 和 .snupkg 文件。

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet 会将两个包发布到 nuget.org。`MyPackage.nupkg` 先发布，随后 `MyPackage.snupkg` 发布。

> [!Note]
> 如果没有发布符号包，请检查是否已将 NuGet.org 源配置为 `https://api.nuget.org/v3/index.json`。 只有 [NuGet V3 API](../api/overview.md#versioning) 才支持符号包发布。

## <a name="nugetorg-symbol-server"></a>NuGet.org 符号服务器

NuGet.org 支持自己的符号服务器存储库，只接受新的符号包格式 - `.snupkg`。 包使用者可将 `https://symbols.nuget.org/download/symbols` 添加到 Visual Studio 中的符号源，使用发布到 nuget.org 符号服务器的符号，这允许在 Visual Studio 调试程序中单步执行包代码。 有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org 符号包约束

NuGet.org 对符号包具有以下约束：

- 符号包中仅允许使用以下文件扩展名：`.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`
- NuGet.org 符号服务器目前仅支持托管的[可移植 PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。
- 需要使用 Visual Studio 15.9 或更高版本中的编译器构建 PDB 及其关联的 nupkg DLL（请参阅 [PDB 加密哈希](https://github.com/dotnet/roslyn/issues/24429)）

如果未满足这些约束，则发布到 NuGet.org 的符号包将无法通过验证。 

### <a name="symbol-package-validation-and-indexing"></a>符号包验证和编制索引

发布到 [NuGet.org](https://www.nuget.org/) 的符号包会接受多项验证，包括恶意软件扫描。 如果包未通过验证检查，则其包详细信息页将显示错误消息。 此外，包的所有者还将收到一封电子邮件，其中包含有关如何解决已识别问题的说明。

当符号包通过所有验证后，NuGet.org 的符号服务器将为其中的符号编制索引，并且这些符号将可供使用。

包验证和编制索引所需的时间通常不超过 15 分钟。 如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 NuGet.org 是否遇到任何中断。 如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包详细信息页面上的“联系支持人员”链接与我们联系。

## <a name="symbol-package-structure"></a>符号包结构

符号包 (.snupkg) 具有以下特征：

1) .snupkg 与相应的 NuGet 包 (.nupkg) 具有相同的 ID 和版本。
2) .snupkg 具有与任何 DLL 或 EXE 文件的相应 .nupkg 相同的文件夹结构，区别在于其相应的 PDB 将包含在同一文件夹层次结构中，而不是 DLL/EXE 中。 扩展名不是 PDB 的文件和文件夹将被排除在 snupkg 之外。
3) 符号包的 .nuspec 文件具有 `SymbolsPackage` 包类型：

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。
5) 将从 snupkg 的 nuspec 中排除以下字段：```authors```、```owners```、```requireLicenseAcceptance```、```license type```、```licenseUrl``` 和 ```icon```。
6) 不要使用 ```<license>``` 元素。 .snupkg 与对应的 .nupk 位于同一个许可证中。

## <a name="see-also"></a>另请参阅

考虑使用源链接来启用 .NET 程序集的源代码调试。 有关详细信息，请参阅[源链接指南](/dotnet/standard/library-guidance/sourcelink)。

有关符号包的更多信息，请参阅 [NuGet 包调试与符号改进](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)设计规范。
