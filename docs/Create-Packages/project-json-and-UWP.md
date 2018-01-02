---
title: "NuGet project.json 文件和 UWP 项目 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "介绍如何使用 project.json 文件来跟踪通用 Windows 平台 (UWP) 项目中的 NuGet 依赖项。"
keywords: "NuGet 依赖项, NuGet 和 UWP, UWP 和 project.json, NuGet project.json 文件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40507e541997cea368052c373a4124d9c4a00a51
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-and-uwp"></a>project.json 和 UWP

本文档介绍使用 NuGet 3+（Visual Studio 2015 及更高版本）中功能的包结构。 可以通过将 `.nuspec` 的 `minClientVersion` 设置为 3.1 来声明你需要此处介绍的功能。

## <a name="adding-uwp-support-to-an-existing-package"></a>向现有包添加 UWP 支持

如果有一个现有包，并且想添加对 UWP 应用程序的支持，则不需要采用此处介绍的打包格式。 如果需要此处介绍的功能并且只愿意使用已更新到 3+ 版 NuGet 的客户端，只需采用此格式即可。

## <a name="i-already-target-netcore45"></a>已面向 netcore45

如果已面向 `netcore45`，并且不需要利用此处介绍的功能，则无需执行任何操作。 UWP 应用程序可以使用 `netcore45` 包。

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>希望利用 Windows 10 特定的 API

在这种情况下，需要将 `uap10.0` 目标框架名字对象（TFM 或 TxM）添加到包。 在包中创建一个新文件夹，并将已编译为与 Windows 10 一起使用的程序集添加到该文件夹中。

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>不需要 Windows 10 特定的 API，但需要新的 .NET 功能或者尚没有 netcore45

在这种情况下，需要将 `dotnet` TxM 添加到包。 与其他 TxM 不同，`dotnet` 并不意味着外围应用或平台。 也就是说，包适用于依赖项适用的任何平台。 使用 `dotnet` TxM 生成包时，`.nuspec` 中可能存在许多 TxM 特定的依赖项，因为需要定义所依赖的 BCL 包，如 `System.Text`、`System.Xml` 等。这些依赖项适用的位置即是包的工作位置。

### <a name="how-do-i-find-out-my-dependencies"></a>如何查找依赖项

有两种方法可以查找要列出的依赖项：

1. 使用 [NuSpec 依赖项生成器](https://github.com/onovotny/ReferenceGenerator)第三方工具。 该工具自动执行该过程，并使用生成时依赖的包更新 `.nuspec` 文件。 该工具通过 NuGet 包 [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) 提供。
2. （复杂方法）使用 `ILDasm` 检查 `.dll`，查看运行时实际需要的程序集。 然后确定这些程序集分别来自哪个 NuGet 包。

请参阅 [`project.json`](../Schema/project-json.md) 主题，详细了解可帮助创建支持 `dotnet` TxM 的包的功能。

> [!Important]
> 如果打算将包用于 PCL 项目，强烈建议创建一个 `dotnet` 文件夹，以避免警告和潜在的兼容性问题。


## <a name="directory-structure"></a>目录结构

使用此格式的 NuGet 包具有以下已知文件夹和行为：

| 文件夹 | 行为 |
| --- | --- |
| 生成 | 此文件夹中包含 MSBuild 目标和属性文件将以不同的方式集成到项目中，但除此之外没有更改。 |
| 工具 | `install.ps1` 和 `uninstall.ps1` 不运行。 `init.ps1` 像往常一样工作。 |
| 内容 | 内容不会自动复制到用户的项目中。 后续发行版本计划支持将内容包含在项目中。 |
| Lib | 对于许多包而言，`lib` 的工作方式与 NuGet 2.x 相同，只不过其中使用的名称具有扩展选项，并且在使用包时具有更好的逻辑来选取正确的子文件夹。 但是，与 `ref` 一起使用时，`lib` 文件夹包含如下程序集：实现由 `ref` 文件夹中的程序集定义的外围应用。 |
| 引用 | `ref` 是一个可选文件夹，其中包含 .NET 程序集，用于定义应用程序编译的公共外围（公共类型和方法）。 此文件夹中的程序集可能没有实现，只是用于为编译器定义外围应用。 如果包没有 `ref` 文件夹，那么 `lib` 同时为引用程序集和实现程序集。 |
| 运行时 | `runtimes` 是一个可选文件夹，其中包含操作系统特定的代码，如 CPU 体系结构以及操作系统特定的或依赖于其他平台的二进制文件。 |


## <a name="msbuild-targets-and-props-files-in-packages"></a>包中的 MSBuild 目标和属性文件

NuGet 包可能包含 `.targets` 和 `.props` 文件，这些文件被导入到包安装到的任何 MSBuild 项目中。 在 NuGet 2.x 中，此操作是通过向 `.csproj` 文件注入 `<Import>` 语句而完成的；在 NuGet 3.0 中，没有特定的“安装到项目”操作。 而是包还原过程写入 `[projectname].nuget.props` 和 `[projectname].NuGet.targets` 两个文件。

MSBuild 知道查找这两个文件，并在项目生成过程开始和结束时自动导入它们。 此行为与 NuGet 2.x 非常相似，但有一个主要区别：在此情况下，无法保证目标/道属性文件的顺序。 但是，MSBuild 通过 `<Target>` 定义的 `BeforeTargets` 和 `AfterTargets` 特性（请参阅 [Target 元素 (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild)）提供了对目标进行排序的方法。


## <a name="lib-and-ref"></a>Lib 和引用

在 NuGet v3 中，`lib` 文件夹的行为没有重大变化。 但是，所有程序集都必须位于以 TxM 命名的子文件夹内，不再直接放置在 `lib` 文件夹下。 TxM 是包中给定资产适用的平台名称。 逻辑上，这些是目标框架名字对象 (TFM) 的扩展，例如，`net45`、`net46`、`netcore50` 和 `dnxcore50` 都是 TxM 的示例（请参阅[目标框架](../Schema/Target-Frameworks.md)）。 TxM 可以指框架 (TFM) 以及其他平台特定的外围应用。 例如，UWP TxM (`uap10.0`) 表示 .NET 外围应用以及适用于 UWP 应用程序的 Windows 外围应用。

Lib 结构示例：

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` 文件夹包含在运行时使用的程序集。 对于大多数包而言，每个目标 TxM 的 `lib` 下的文件夹全都是必需的。

## <a name="ref"></a>引用

有时在编译期间应使用不同的程序集（如 .NET 引用程序集）。 对于这些情况，请使用名为 `ref`（“引用程序集”的缩写）的顶层文件夹。

大多数包创建者都不需要 `ref` 文件夹。 这对以下包非常有用：需要为编译和 IntelliSense 提供一致的外围应用，但对不同的 TxM 具有不同的实现。 最大的用例是 `System.*` 包，这些包是在 NuGet 上提供 .NET Core 的过程中生成的。 这些包具有各种实现，这些实现由一组一致的引用程序集统一。

从表面上讲，`ref` 文件夹中包含的程序集是传递给编译器的引用程序集。 对于使用过 csc.exe 的用户来说，这些是我们传递给 [C# /reference 选项](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) 开关的程序集。

`ref` 文件夹的结构与 `lib` 的结构相同，例如：

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


在本例中，`ref` 目录中的程序集是相同的。


## <a name="runtimes"></a>运行时

运行时文件夹包含在特定“运行时”上运行所需的程序集和本机库，通常由操作系统和 CPU 体系结构定义。 这些运行时使用[运行时标识符 (RID)](https://docs.microsoft.com/dotnet/core/rid-catalog) 进行标识，如 `win`、`win-x86`、`win7-x86`、`win8-64` 等。

## <a name="native-light-up"></a>本机启动

以下示例显示这样的包：拥有适用于多个平台的纯托管实现，但可在 Windows 8 上使用本机帮助程序以调用 Windows 8 特定的本机 API。

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

提供上述包时，将发生以下情况：

- 当不在 Windows 8 上，将使用 `lib/net40/MyLibrary.dll` 程序集。

- 在 Windows 8 上时，将使用 `runtimes/win8-<architecture>/lib/MyLibrary.dll`，并且 `native/MyNativeHelper.dll` 将复制到生成的输出。

在上面的示例中，`lib/net40` 程序集是纯托管代码，而运行时文件夹中的程序集将平台调用到本机帮助程序程序集中，以调用特定于 Windows 8 的 API。

始终仅选取单个 `lib` 文件夹，因此如果有运行时特定的文件夹，将选择通过非运行时特定的 `lib`。 本机文件夹是累加式的，如果存在，将被复制到生成的输出。

## <a name="managed-wrapper"></a>托管包装器

使用运行时的另一种方式是将属于纯托管包装器的包提供到本机程序集上。 在此方案中，将创建如下所示的包：

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

在此情况下，没有顶层 `lib` 文件夹作为该文件夹，因为此包的实现不依赖于相应的本机程序集。 如果托管程序集 `MyLibrary.dll` 在这两种情况下完全相同，则可将它放在顶层 `lib` 文件夹中；但是，由于缺少本机程序集并不会导致将包安装到非 win-x86 或 win-x64 平台上时失败，因此将使用顶层 lib，但不会复制本机程序集。


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>创作适用于 NuGet 2 和 NuGet 3 的包

如果想创建一个可供使用 `packages.config` 的项目使用的包以及使用 `project.json` 的包，则以下内容适用：

- 引用和运行时只适用于 NuGet 3。 在 NuGet 2 中将被忽略。

- 不能依靠 `install.ps1` 或 `uninstall.ps1` 来运行。 这些文件在使用 `packages.config` 时执行，但使用 `project.json` 时会忽略。 因此包需要不运行它们时可用。 `init.ps1` 仍在 NuGet 3 上运行。

- 目标与属性安装不同，因此请确保包在两个客户端上按预期工作。

- 在 NuGet 3 中，lib 的子目录必须是一个 TxM。 不能将库放置在 `lib` 文件夹的根目录下。

- NuGet 3 将不会自动复制内容。 包的使用者可以自己复制文件，或使用任务运行程序之类的工具来自动复制文件。

- NuGet 3 不会运行源和配置文件转换。

如果支持 NuGet 2 和 3，`minClientVersion` 应该是包适用的最低版本的 NuGet 2 客户端。 如果存在现有包，则不需要更改。