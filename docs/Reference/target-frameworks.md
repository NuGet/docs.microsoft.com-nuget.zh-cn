---
title: NuGet 的目标框架引用 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet 目标框架引用标识并隔离包的框架依赖组件。
keywords: NuGet 包定向, .NET ramework 目标, .NET framework 版本
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0a9c45ef31e27c2242edce48e2cf272e5280dcff
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="target-frameworks"></a>目标框架

NuGet 在各个地方使用目标框架引用，以特别标识和隔离包的框架依赖组件：

- [.nuspec 清单](../reference/nuspec.md)：根据项目的目标框架，包可以指示要包含在项目中的不同包。
- [.nupkg 文件夹名称](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)：包的 `lib` 文件夹内的文件夹可根据目标框架进行命名，每个文件夹都包含适合该框架的 DLL 及其他内容。
- [packages.config](../reference/packages-config.md)：依赖项的 `targetframework` 特性指定要安装的包的变体。

> [!Note]
> 计算下方表格的 NuGet 客户端源代码位于以下位置：
> - 支持的框架名称：[FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Framework 优先级和映射：[DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>支持的框架

通常按简短的目标框架名字对象或 TFM 引用框架。 在 .NET Standard 中，这也泛化成 TxM，以便一次引用多个框架。

NuGet 客户端支持下表中的框架。 等效项显示在括号内 []。 请注意，某些工具（如 `dotnet`）可能会在某些文件中使用规范的 TFM 变体。 例如，`dotnet pack` 在 `.nuspec` 文件中使用 `.NETCoreApp2.0`，而非 `netcoreapp2.0` 文件。 各种 NuGet 客户端工具正确处理这些变体，但是在直接编辑文件时，应始终使用规范的 TFM。

| 名称           | 缩写 | TFM/TxM |
| -------------  | ------------ | --------- |
|.NET Framework  | net          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Microsoft Store（Windows 应用商店） | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | win [win8、netcore45] |
| | | win8 [netcore45、win] |
| | | win81 [netcore451] |
| | | win10（Windows 10 平台不支持） |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
通用 Windows 平台 | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET Core 应用 | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>弃用的框架
以下框架已弃用。 定位这些框架的包应迁移到指明的替代框架。

| 弃用的框架 | Replacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>优先级

许多框架相互关联且彼此兼容，但不一定是等效的：

| 框架 | 可以使用 |
| --- | --- |
| uap（通用 Windows 平台） | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>NET 平台标准

[.NET 平台标准](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md)简化了二进制兼容框架之间的引用，允许单个目标框架引用其他框架的组合。 （有关背景信息，请参阅 [.NET 入门](/dotnet/articles/standard/index)。）

[NuGet 获取最新框架工具](https://aka.ms/s2m3th)模拟用于从基于项目框架的包中的许多可用框架资产中选择一个框架的 NuGet 逻辑。

NuGet 3.3 及更早版本应该使用 `dotnet` 系列的名字对象；v3.4 及更高版本应该使用 `netstandard` 名字对象语法。

## <a name="portable-class-libraries"></a>可移植类库

> [!Warning]
> 建议不要使用 PCL。 尽管支持 PCL，但包创建者反而应支持 netstandard。 .NET 平台标准是演变而来的 Pcl 和跨平台使用不绑定到静态库类似的单个标记表示二进制可移植性*可移植-a + b + c*名字对象。

若要定义一个引用多个子目标框架的目标框架，请使用 `portable` 关键字作为所引用框架列表的前缀。 避免人为地包含非直接编译的额外框架，因为可能会导致这些框架中出现意外的负面效果。

由第三方定义的附加框架提供了与其他环境的兼容性，这些环境可通过此方式进行访问。 此外，还有速记配置文件编号，可用于以 `Profile#` 形式引用相关框架的组合，但不建议通过此方法引用这些编号，因为这会降低文件夹和 `.nuspec` 的可读性。

| 配置文件编号 | 框架 | 全称 | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

另外，面向 Xamarin 的 NuGet 包可以使用 Xamarin 定义的其他框架。 请参阅[创建适用于 Xamarin 的 NuGet 包](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/)。

| 名称 | 描述 | .NET Standard |
| --- | --- | ---
| monoandroid | Mono 支持 Android OS | netstandard1.4 |
| monotouch | Mono 支持 iOS | netstandard1.4 |
| monomac | Mono 支持 OSX | netstandard1.4 |
| xamarinios | 支持适用于 iOS 的 Xamarin | netstandard1.4 |
| xamarinmac | 支持适用于 Mac 的 Xamarin | netstandard1.4 |
| xamarinpsthree | 支持 Playstation 3 上的 Xamarin | netstandard1.4 |
| xamarinpsfour | 支持 Playstation 4 上的 Xamarin | netstandard1.4 |
| xamarinpsvita | 支持 PS Vita 上的 Xamarin | netstandard1.4 |
| xamarinwatchos | 适用于 Watch OS 的 Xamarin | netstandard1.4 |
| xamarintvos | 适用于 TV OS 的 Xamarin | netstandard1.4 |
| xamarinxboxthreesixty | 适用于 XBox 360 的 Xamarin | netstandard1.4 |
| xamarinxboxone | 适用于 XBox One 的 Xamarin | netstandard1.4 |

> [!Note]
> Stephen Cleary 创建了一种工具，用于列出支持的 PCL，该工具可在其文章 [Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)（.NET 中的框架配置文件）中找到。
