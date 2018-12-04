---
title: 如何使用新的符号包格式“.snupkg”发布 NuGet 符号包 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453450"
---
# <a name="creating-symbol-packages-snupkg"></a>创建符号包 (.snupkg)

## <a name="prerequisites"></a>系统必备

[nuget.exe v4.9.0 或更高版本](https://www.nuget.org/downloads)或 [dotnet.exe v2.2.0 或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，它们实现了所需的 [NuGet 协议](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>创建符号包

可从 .nuspec 文件或 .csproj 文件创建 snupkg 符号包。 同时支持 NuGet.exe 和 dotnet.exe。 当在 nuget.exe 包命令上使用选项 ```-Symbols -SymbolPackageFormat snupkg``` 时，将在除 .nupkg 文件以外另创建 .snupkg 文件。

用于创建 .snupkg 文件的示例命令
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

默认情况下不会生成 `.snupkgs`。 对于 nuget.exe，必须将 `SymbolPackageFormat` 属性与 `-Symbols` 一起传递；对于 dotnet.exe，必须传递 `--include-symbols`，对于 msbuild，必须传递 `-p:IncludeSymbols`。

SymbolPackageFormat 属性的可取值为下列两个之一：`symbols.nupkg`（默认值）或 `snupkg`。 如果未指定 SymbolPackageFormat，默认值为 `symbols.nupkg`，并将创建旧的符号包。

> [!Note]
> 仍支持旧格式 `.symbols.nupkg`，但仅出于兼容性原因（请参阅[旧版符号包](Symbol-Packages.md)）。 NuGet.org 符号服务器仅接受新的符号包格式 - `.snupkg`。

## <a name="publishing-a-symbol-package"></a>发布符号包

1. 为方便起见，首先使用 NuGet 保存 API 密钥（请参阅[发布包](../create-packages/publish-a-package.md)）。

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
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) 如果创建者决定使用自定义 nuspec 来构建其 nupkg 和 snupkg，则 snupkg 应该具有 2 中详细描述的同一文件夹层次结构和文件）。
5) 将从 snupkg 的 nuspec 中排除 ```authors``` 和 ```owners``` 字段。

## <a name="see-also"></a>请参阅

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
