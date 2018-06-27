---
title: NuGet PackageReference 格式（项目文件中的包引用）
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817666"
---
# <a name="package-references-packagereference-in-project-files"></a>项目文件中的包引用 (PackageReference)

使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。 使用所谓的 PackageReference 不会影响 NuGet 的其他方面；例如，仍按照[配置 NuGet 行为](configuring-nuget-behavior.md)中的说明应用 `NuGet.Config` 文件（包括包源）中的设置。

利用 PackageReference，还可以使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。 它还允许对依赖项和内容流实行精细控制。 （有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）

默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。 .NET 完整框架项目支持 PackageReference，但当前默认为 `packages.config`。 若要使用 PackageReference，请将 `packages.config` 中的依赖项迁移到项目文件中，然后删除 packages.config。

## <a name="adding-a-packagereference"></a>添加 PackageReference

在项目文件中使用以下语法添加依赖项：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>控制依赖项版本

用于指定包版本的约定与使用 `packages.config` 时的约定相同：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>对没有 PackageReferences 的项目使用 PackageReference
高级：如果项目中没有安装包（项目文件中没有 PackageReference，也没有 packages.config 文件），但想要项目还原为 PackageReference 样式，则可以在项目文件中将项目属性 RestoreProjectStyle 设置为 PackageReference。
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
如果引用 PackageReference 样式的项目（现有 csproj 或 SDK 样式的项目），这可能很有用。 这可让其他项目以“可传递”的方式引用这些项目引用的包。

## <a name="floating-versions"></a>可变版本

`PackageReference` 支持[可变版本](../consume-packages/dependency-resolution.md#floating-versions)：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>控制依赖项资产

你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。 在此情况下，可使用 `PrivateAssets` 元数据控制此行为。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

以下元数据标记控制依赖项资产：

| 标记 | 描述 | 默认值 |
| --- | --- | --- |
| IncludeAssets | 将使用这些资产 | 全部 |
| ExcludeAssets | 不会使用这些资产 | 无 |
| PrivateAssets | 将使用这些资产，但它们不会流入上级项目 | contentfiles;analyzers;build |

以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：

| “值” | 描述 |
| --- | ---
| 编译 | `lib` 文件夹的内容，控制项目能否对文件夹中的程序集进行编译 |
| Runtime — 运行时 | `lib` 和 `runtimes` 文件夹的内容，控制是否会复制这些程序集，以生成输出目录 |
| contentFiles | `contentfiles` 文件夹中的内容 |
| 生成 | `build` 文件夹中的属性和目标 |
| analyzers | .NET 分析器 |
| 本机 | `native` 文件夹中的内容 |
| 无 | 不使用以上任何内容。 |
| 全部 | 以上都是（除 `none` 之外） |

在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目。 例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。 AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。

## <a name="adding-a-packagereference-condition"></a>添加 PackageReference 条件

可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。 但目前仅支持 `TargetFramework` 变量。

例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。 在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。 要防止此情况，请在 `PackageReference` 上指定条件，如下所示：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

使用此项目生成的包会显示仅针对 `net452` 目标包括 Newtonsoft.json 作为依赖项：

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
