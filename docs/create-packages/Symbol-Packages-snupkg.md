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
ms.openlocfilehash: e62d1872497e0e5e703bf7c49a87249ce9a996c7
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959681"
---
# <a name="creating-symbol-packages-snupkg"></a>创建符号包 (.snupkg)

通过符号包可以提高 NuGet 包的调试体验。

## <a name="prerequisites"></a>系统必备

[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet.exe v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>创建符号包

可以使用 dotnet.exe、NuGet.exe 或 MSBuild 创建 snupkg 包。 如果使用 NuGet.exe，除 .nupkg 文件外，可以使用以下命令创建一个 .snupkg 文件：

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

如果使用 dotnet.exe 或 MSBuild，除 .nupkg 文件外，可以通过以下步骤创建一个 .snupkg 文件：

1. 将以下属性添加到 .csproj 文件：

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. 使用 `dotnet pack MyPackage.csproj` 或 `msbuild -t:pack MyPackage.csproj` 打包项目。

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性可以有下列两个值之一：`symbols.nupkg`（默认值）或 `snupkg`。 如果未指定 [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 属性，将会创建旧的符号包。

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

NuGet.org 支持自己的符号服务器存储库，只接受新的符号包格式 - `.snupkg`。 包使用者可将 `https://symbols.nuget.org/download/symbols` 添加到 Visual Studio 中的符号源，使用发布到 nuget.org 符号服务器的符号，这允许在 Visual Studio 调试程序中单步执行包代码。 有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)。

### <a name="nugetorg-symbol-package-constraints"></a>Nuget.org 符号包约束

nuget.org 上支持的符号包具有以下约束

- 只允许将以下文件扩展名添加到符号包中。 ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- nuget 符号服务器目前仅支持托管的[可移植 pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。
- 需要使用 Visual Studio 15.9 或更高版本中的编译器构建 pdb 和关联的 nupkg dll（请参阅 [pdb 加密哈希](https://github.com/dotnet/roslyn/issues/24429)）

如果 .snupkg 中包含任何其他文件类型，则 nuget.org 上的符号包发布将失败。

### <a name="symbol-package-validation-and-indexing"></a>符号包验证和编制索引

发布到 [NuGet.org](https://www.nuget.org/) 的符号包会进行多项验证，如病毒检查。

包通过所有验证检查后，符号可能需要一段时间才能编入索引和从 NuGet.org 符号服务器中使用。 如果包未通过验证检查，将更新 .nupkg 包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。

包验证和编制索引所需的时间通常不超过 15 分钟。 如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。 如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包详细信息页面上的“联系支持人员”链接与我们联系。

## <a name="symbol-package-structure"></a>符号包结构

.nupkg 文件将和现在一模一样，但 .snupkg 文件具有以下特征：

1) .snupkg 将具有与相应 .nupkg 相同的 ID 和版本。
2) .snupkg 将具有与任何 DLL 或 EXE 文件的 nupkg 完全相同的文件夹结构，区别在于其相应的 PDB 将包含在同一文件夹层次结构中，而不是 DLL/EXE 中。 扩展名不是 PDB 的文件和文件夹将被排除在 snupkg 之外。
3) .snupkg 中的 .nuspec 文件还将指定一个新的 PackageType，如下所示。 这应该是唯一指定的 PackageType。

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。
5) 将从 snupkg 的 nuspec 中排除 ```authors``` 和 ```owners``` 字段。
6) 不要使用 <license> 元素。 .snupkg 与对应的 .nupk 位于同一个许可证中。

## <a name="see-also"></a>另请参阅

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
