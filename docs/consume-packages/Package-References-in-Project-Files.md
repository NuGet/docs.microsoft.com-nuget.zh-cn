---
title: NuGet PackageReference 格式（项目文件中的包引用）
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 71ab5bb464d1513df89ab53e119d9768e880e4e5
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981023"
---
# <a name="package-references-packagereference-in-project-files"></a>项目文件中的包引用 (PackageReference)

使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。 使用 PackageReference 时（正如其名称所述），不会影响 NuGet 的其他方面；例如，“NuGet.fig”文件中的设置





（包括包源）仍将如[配置 NuGet 行为](configuring-nuget-behavior.md)中所述应用。

利用 PackageReference，还可以使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。 它还允许对依赖项和内容流实行精细控制。 （有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）

默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。 .NET 框架项目支持 PackageReference，但当前默认为 `packages.config`。 若要使用 PackageReference，请将 `packages.config` 中的依赖项迁移到项目文件中，然后删除 packages.config。

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
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

使用此项目生成的包会显示，仅对于 `net452` 目标，Newtonsoft.json 包含为依赖项：

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>锁定依赖项
NuGet 4.9 或更高版本以及 Visual Studio 2017 15.9 预览版 5 或更高版本中提供此功能。

NuGet 还原的输入是一组项目文件中的包引用（顶级或直接依赖项），而输出是所有包依赖项的完整闭包，其中包括可传递依赖项。 如果输入 PackageReference 列表尚未更改，则 NuGet 尝试始终生成相同的完整闭包。 但是，在某些情况下，它无法执行此操作。 例如:

* 在使用 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 等浮动版本时。 尽管在此处这样做的目的是浮动到每个包还原的最新版本，但是在某些情况下，用户需要在一个显式动作后，将图形锁定到某个最新版本并浮动到更高版本（如果有可用的更高版本）。
* 匹配 PackageReference 版本要求的较新版本已发布。 例如， 

  * 第 1 天：如果指定了 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但在 NuGet 存储库上可用的版本为 4.1.0、4.2.0 和 4.3.0。 在这种情况下，NuGet 将解析为 4.1.0（最接近的最低版本）

  * 第 2 天：版本 4.0.0 发布。 NuGet 现在将查找完全匹配并开始解析到 4.0.0

* 给定包版本将从存储库中删除。 尽管 nuget.org 不允许包删除，但并非所有包存储库都具有此约束。 这导致 NuGet 在无法解析到已删除的版本时查找最佳匹配项。

### <a name="enabling-lock-file"></a>启用锁定文件
为了保留包依赖项的完整闭包，可以选择锁定文件功能，方法是通过设置项目的 MSBuild 属性 `RestorePackagesWithLockFile`：

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

如果设置此属性，NuGet 还原将生成一个锁定文件 - 项目根目录中列出所有包依赖项的 `packages.lock.json` 文件。 

> [!Note]
> 一旦项目在其根目录中具有 `packages.lock.json` 文件，则即使在未设置属性 `RestorePackagesWithLockFile` 时，锁定文件仍将始终与还原配合使用。 因此，选择加入此功能的另一个方法是在项目的根目录中创建一个虚拟空白 `packages.lock.json` 文件。

### <a name="restore-behavior-with-lock-file"></a>锁定文件的 `restore` 行为
如果项目存在锁定文件，则 NuGet 使用此锁定文件来运行 `restore`。 NuGet 将执行一次快速检查，以确定在包依赖项中是否存在项目文件（或相关项目的文件）中所提及的任何更改，如果没有任何更改，则它将仅还原锁定文件中提及的包。 不会对包依赖项进行重新评估。

如果 NuGet 检测到在定义的依赖项中存在项目文件中提及的更改，则它将重新评估包关系图并更新锁定文件，以反映项目的新闭包。

对于 CI/CD 和其他应用场景（你不想匆忙更改包依赖项），可以通过将 `lockedmode` 设置为 `true` 来执行此操作：

对于 dotnet.exe，请运行：
```
> dotnet.exe restore --locked-mode
```

对于 msbuild.exe，请运行：
```
> msbuild.exe /t:restore /p:RestoreLockedMode=true
```

此外，还可以在项目文件中设置此条件 MSBuild 属性：
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

如果锁定模式为 `true`，则还原将还原锁定文件中列出的完全匹配的包，或者，如果在锁定文件创建后为项目更新了定义的包依赖项，则还原将失败。

### <a name="make-lock-file-part-of-your-source-repository"></a>使锁定文件作为源存储库的一部分
如果生成应用程序，存在问题的可执行文件和项目在依赖关系链结尾处，则将锁定文件签入到源代码存储库，以便 NuGet 能够在还原期间使用它。

但是，如果你的项目是不交付的库项目或其他项目依赖的常用代码项目，则不应将锁定文件作为源代码的一部分签入。 保留锁定文件没有任何坏处，但在依赖于此常用代码项目的项目还原/生成期间，锁定文件中列出的常用代码项目的锁定的包依赖项可能无法使用。

例如，
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
如果 `ProjectA` 在 `PackageX` 版本 `2.0.0` 上具有依赖项并引用依赖于 `PackageX` 版本 `1.0.0` 的 `ProjectB`，则 `ProjectB` 的锁定文件将列出 `PackageX` 版本 `1.0.0` 的依赖项。 但是，当生成 `ProjectA` 时，其锁定文件将包含 `ProjectB` 锁定文件中列出的 `PackageX` 版本 `2.0.0`（而不是 `1.0.0`）上的依赖项。 因此，常用代码项目的锁定文件对依赖于它的项目进行解析的包几乎没有控制。

### <a name="lock-file-extensibility"></a>锁定文件可扩展性
可以使用以下所述的锁定文件控制各种还原行为：

| 选项 | MSBuild 等效选项 | 
|:---  |:--- |
| `--use-lock-file` | 为项目启动锁定文件的使用。 或者，可以在项目文件中设置 `RestorePackagesWithLockFile` 属性 | 
| `--locked-mode` | 为还原启用锁定模式。 这对于想要获取重复版本的 CI/CD 应用场景非常有用。 通过将 `RestoreLockedMode` MSBuild 属性设置为 `true` 也可以实现此目的 |  
| `--force-evaluate` | 对于在项目中定义了浮动版本的包，此选项也非常有用。 默认情况下，NuGet 还原不会在每次还原时自动更新包版本，除非使用 `--force-evaluate` 选项运行还原。 |
| `--lock-file-path` | 为项目定义自定义锁定文件位置。 这也可以通过设置 MSBuild 属性 `NuGetLockFilePath` 来实现。 默认情况下，NuGet 支持根目录中的 `packages.lock.json`。 如果在同一目录中具有多个项目，则 NuGet 支持特定于项目的锁定文件 `packages.<project_name>.lock.json` |
