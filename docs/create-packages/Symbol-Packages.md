---
title: 如何创建 NuGet 符号包
description: 如何在 Visual Studio 中创建仅包含符号的 NuGet 包以支持调试其他 NuGet 包。
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f7503dd413a976997580aa03da26df0c462ff0e1
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564548"
---
# <a name="creating-symbol-packages-legacy"></a>创建符号包（旧版）

> [!Important]
> 符号包的新推荐格式为 .snupkg。 请参阅[创建符号包 (.snupkg)](Symbol-Packages-snupkg.md)。 </br>
> .symbols.nupkg 仍受支持，但仅出于兼容性原因。

除了为 nuget.org 或其他源生成包之外，NuGet 还支持创建关联的符号包并将其发布到 SymbolSource 存储库。

然后，包使用者可将 `https://nuget.smbsrc.net` 添加到 Visual Studio 中的符号源，它允许在 Visual Studio 调试程序中单步执行包代码。 有关该过程的详细信息，请参阅[在 Visual Studio 调试程序中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。

## <a name="creating-a-symbol-package"></a>创建符号包

若要创建符号包，请按照以下约定操作：

- （使用代码）将主包命名为 `{identifier}.nupkg`，并包括除 `.pdb` 文件之外的所有文件。
- 将符号包命名为 `{identifier}.symbols.nupkg`，并包括程序集 DLL、`.pdb` 文件、XMLDOC 文件和源文件（请参阅以下各节）。

可使用 `-Symbols` 选项从 `.nuspec` 文件或项目文件中同时创建这两个包：

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

请注意，`pack` 要求在 Mac OS X 上使用 Mono 4.4.2，但不能在 Linux 系统上使用。 在 Mac 上，还必须将 `.nuspec` 文件中的 Windows 路径名转换为 Unix 样式的路径。

## <a name="symbol-package-structure"></a>符号包结构

符号包面向多个目标框架的方式可与库包的方式相同，因此 `lib` 文件夹的结构应与主包的结构完全相同，即仅包括 `.pdb` 和 DLL 文件。

例如，面向 .NET 4.0 和 Silverlight 4 的符号包具有以下布局：

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

然后，在名为 `src` 的单独的特殊文件夹中放入源文件，该文件夹必须遵循源存储库的相对结构。 这是因为 PDB 包含指向用于编译匹配 DLL 的源文件的绝对路径，在发布过程中需要找到这些路径。 可以去除基路径（通用路径前缀）。例如，假设从以下文件中生成一个库：

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

除了 `lib` 文件夹之外，符号包需要包含以下布局：

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

## <a name="referring-to-files-in-the-nuspec"></a>引用 nuspec 中的文件

可以通过约定从文件夹结构中生成符号包（如上一部分所述），也可以通过在清单的 `files` 部分中指定内容进行生成。 例如，若要生成上一部分中显示的包，请使用 `.nuspec` 文件中的以下内容：

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>发布符号包

> [!Important]
> 若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.9.1 或更高版本](https://www.nuget.org/downloads)。

1. 为方便起见，请首先保存 NuGet 的 API 密钥（请参阅[发布包](../nuget-org/publish-a-package.md)），它将应用于 nuget.org 和 symbolsource.org，因为 symbolsource.org 会与 nuget.org 进行核对以验证包所有者。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. 将主包发布到 nuget.org 后，按照以下方式推送符号包，由于文件名中的 `.symbols`，此步骤将 symbolsource.org 自动用作目标：

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. 若要发布到另一符号存储库或推送不遵循命名约定的符号包，请使用 `-Source` 选项：

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. 还可以使用以下项将主包和符号包同时推送到两个存储库：

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > 在 nuget.exe 4.5.0 或更高版本中，符号包不会自动推送到 symbolsource.org。需要单独推送符号包，如前面步骤所述。
   
在此情况下，向 nuget.org 发布主包后，NuGet 将 `MyPackage.symbols.nupkg`（如果存在）发布到 https://nuget.smbsrc.net/ （symbolsource.org 的推送 URL）。

## <a name="see-also"></a>另请参阅

[移动到新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
