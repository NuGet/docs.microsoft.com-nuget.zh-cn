---
title: 选择项目引用的程序集
description: 使包中的程序集子集可用于编译器，而所有程序集在运行时都可用。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859026"
---
# <a name="select-assemblies-referenced-by-projects"></a>选择项目引用的程序集

显式程序集引用允许将程序集的子集用于 IntelliSense 和编译，而所有程序集在运行时都可用。 `PackageReference` 和 `packages.config` 的工作方式不同，因此包创建者需要注意创建与两种项目类型兼容的包。

> [!Note]
> 显式程序集引用与 .NET 程序集相关。 它不是用于分发托管程序集调用的本机程序集的方法。

## <a name="packagereference-support"></a>`PackageReference` 支持

当一个项目使用一个带有 `PackageReference` 的包，并且该包包含一个 `ref\<tfm>\` 目录时，NuGet 会将这些组件分类为编译时资产，而 `lib\<tfm>\` 程序集则归类为运行时资产。 `ref\<tfm>\` 中的程序集不在运行时使用。 这意味着 `ref\<tfm>\` 中的任何程序集都必须在 `lib\<tfm>\` 或相关的 `runtime\` 目录中具有匹配的程序集，否则可能会发生运行时错误。 由于 `ref\<tfm>\` 中的程序集未在运行时使用，因此可以使用[“仅元数据”专用程序集](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)来减小包的大小。

> [!Important]
> 如果包中包含 nuspec `<references>` 元素（由 `packages.config` 使用，请参见下文）并且不包含 `ref\<tfm>\` 中的程序集，NuGet 会将 nuspec `<references>` 元素中列出的程序集作为编译和运行时资产进行播发。 这意味着当引用的程序集需要加载 `lib\<tfm>\` 目录中的任何其他程序集时，将存在运行时异常。

> [!Note]
> 如果包包含 `runtime\` 目录，则 NuGet 可能不会使用 `lib\` 目录中的资产。

## <a name="packagesconfig-support"></a>`packages.config` 支持

使用 `packages.config` 管理 NuGet 包的项目通常会向 `lib\<tfm>\` 目录中的所有程序集添加引用。 添加 `ref\` 目录以支持 `PackageReference`，因此在使用 `packages.config` 时不予考虑。 要使用 `packages.config` 以显式方式设置项目引用的程序集，包必须使用 [nuspec 文件中的 `<references>` 元素](../reference/nuspec.md#explicit-assembly-references)。 例如：

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` 项目使用名为 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) 的进程将程序集复制到 `bin\<configuration>\` 输出目录。 复制项目的程序集，然后构建系统查看引用程序集的程序集清单，然后复制这些程序集并递归重复所有程序集。 这意味着，如果 `lib\<tfm>\` 目录中的任何程序集不在任何其他程序集的清单中作为依赖项列出（如果在运行时使用 `Assembly.Load`、MEF 或其他依赖项注入框架加载程序集）那么即使在 `bin\<tfm>\` 中，也不能将其复制到项目的 `bin\<configuration>\` 输出目录中。

## <a name="example"></a>示例

我的包将包含三个程序集 `MyLib.dll``MyHelpers.dll` 和 `MyUtilities.dll`，它们以 .NET Framework 4.7.2 为目标。 `MyUtilities.dll` 包含仅供其他两个程序集使用的类，因此我不希望在 IntelliSense 中或在编译时将这些类用于使用我的包的项目。 我的 `nuspec` 文件需要包含以下 XML 元素：

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

并且包中的文件将为：

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
