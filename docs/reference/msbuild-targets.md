---
title: NuGet作为目标打包和还原 MSBuild
description: NuGet 打包和还原可以直接作为 MSBuild 使用 NuGet 4.0 + 的目标。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387369"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet作为目标打包和还原 MSBuild

*NuGet 4.0 +*

使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式时， NuGet 4.0 + 可以直接将所有清单元数据存储在项目文件中，而不是使用单独的 `.nuspec` 文件。

使用 MSBuild 15.1 + NuGet 也是具有和目标的第一类公民，如下 MSBuild `pack` `restore` 所述。 这些目标使你可以像处理 NuGet 任何其他 MSBuild 任务或目标一样使用。 有关 NuGet 使用创建包的说明 MSBuild ，请参阅[ NuGet 使用 MSBuild 创建包](../create-packages/creating-a-package-msbuild.md)。  (在 1.x NuGet 和更早版本中，你可以通过 CLI 改用 [包](../reference/cli-reference/cli-ref-pack.md) 和 [还原](../reference/cli-reference/cli-ref-restore.md) 命令 NuGet 。 ) 

## <a name="target-build-order"></a>目标生成顺序

由于 `pack` 和 `restore` 都是  MSBuild 目标，因此你可以访问它们以增强工作流。 例如，假设你想要将包打包到网络共享。 此操作可通过向项目文件中添加以下内容来完成：

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

同样，您可以编写 MSBuild 任务，编写自己的目标并使用 NuGet 任务中的属性 MSBuild 。

> [!NOTE]
> `$(OutputPath)` 是相对的，需要从项目根目录运行命令。

## <a name="pack-target"></a>包目标

对于使用格式的 .NET 项目 `PackageReference` ，使用 `msbuild -t:pack` 可以从项目文件中绘制输入，以在创建包时使用 NuGet 。

下表描述了 MSBuild 可添加到第一个节点中的项目文件的属性 `<PropertyGroup>` 。 在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。 为方便起见，表按[ `.nuspec` 文件](../reference/nuspec.md)中的等效属性进行组织。

> [!NOTE]
> `Owners``Summary`不支持中的和属性 `.nuspec` MSBuild 。

| 属性/ nuspec 值 | MSBuild 属性 | 默认 | 说明 |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` 来自 MSBuild |
| `Version` | `PackageVersion` | 版本 | 这是 semver 兼容的，例如 `1.0.0` 、 `1.0.0-beta` 或 `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | empty | 设置 `PackageVersion` 覆盖 `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | empty | `$(VersionSuffix)` from MSBuild 。 设置 `PackageVersion` 覆盖 `PackageVersionSuffix` |
| `Authors` | `Authors` | 当前用户的用户名 | 以分号分隔的包作者列表，与 nuget.org 上的配置文件名称匹配。它们显示在 nuget.org 的 NuGet 库中，并用于通过相同作者交叉引用包。 |
| `Owners` | 空值 | 不存在于 nuspec | |
| `Title` | `Title` | `PackageId` | 明了易用的包标题，通常用在 UI 显示中，如 nuget.org 上和 Visual Studio 中包管理器上的那样。 |
| `Description` | `Description` | “包描述” | 程序集的详细说明。 如果未指定 `PackageDescription`，则此属性还可用作包的说明。 |
| `Copyright` | `Copyright` | empty | 包的版权详细信息。 |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | 一个布尔值，指定客户端是否必须提示使用者接受包许可证后才可安装包。 |
| `license` | `PackageLicenseExpression` | empty | 对应到 `<license type="expression">`。 请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。 |
| `license` | `PackageLicenseFile` | empty | 如果使用的是未分配 SPDX 标识符的自定义许可证或许可证，则为包内的许可证文件的路径。 需要显式打包所引用的许可证文件。 对应到 `<license type="file">`。 请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。 |
| `LicenseUrl` | `PackageLicenseUrl` | empty | `PackageLicenseUrl` 已弃用。 请改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。 |
| `ProjectUrl` | `PackageProjectUrl` | empty | |
| `Icon` | `PackageIcon` | empty | 包中要用作包图标的图像的路径。 需要显式打包所引用的图标图像文件。 有关详细信息，请参阅[打包图标图像文件](#packing-an-icon-image-file)和[ `icon` 元数据](./nuspec.md#icon)。 |
| `IconUrl` | `PackageIconUrl` | empty | `PackageIconUrl` 对于，已弃用 `PackageIcon` 。 但是，为了获得最佳的下层体验，除了指定外，还应该指定 `PackageIconUrl` `PackageIcon` 。 |
| `Readme` | `PackageReadmeFile` | empty | 需要显式打包所引用的自述文件。|
| `Tags` | `PackageTags` | empty | 标记的分号分隔列表，这些标记用于指定包。 |
| `ReleaseNotes` | `PackageReleaseNotes` | empty | 包的发行说明。 |
| `Repository/Url` | `RepositoryUrl` | empty | 用于克隆或检索源代码的存储库 URL。 示例： *https://github.com/ NuGet / NuGet 。客户端*。 |
| `Repository/Type` | `RepositoryType` | empty | 存储库类型。 示例： `git` (默认) ， `tfs` 。 |
| `Repository/Branch` | `RepositoryBranch` | empty | 可选存储库分支信息。 还必须指定 `RepositoryUrl` 才能包含此属性。 示例： *master* (NuGet 4.7.0 +) 。 |
| `Repository/Commit` | `RepositoryCommit` | empty | 可选的存储库提交或更改集，指示针对其生成包的源。 还必须指定 `RepositoryUrl` 才能包含此属性。 示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。 |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | 不支持 | | |

### <a name="pack-target-inputs"></a>包目标输入

| 属性 | 说明 |
| - | - |
| `IsPackable` | 一个指定能否打包项目的布尔值。 默认值为 `true`。 |
| `SuppressDependenciesWhenPacking` | 设置为 `true` 以从生成的包中取消包依赖项 NuGet 。 |
| `PackageVersion` | 指定生成的包所具有的版本。 接受版本字符串的所有形式 NuGet 。 默认为值 `$(Version)`，即项目中 `Version` 属性的值。 |
| `PackageId` | 指定生成的包的名称。 如果未指定，`pack` 操作将默认使用 `AssemblyName` 或目录名称作为包的名称。 |
| `PackageDescription` | 用于 UI 显示的包的详细说明。 |
| `Authors` | 以分号分隔的包作者列表，与 nuget.org 上的配置文件名称匹配。它们显示在 nuget.org 的 NuGet 库中，并用于通过相同作者交叉引用包。 |
| `Description` | 程序集的详细说明。 如果未指定 `PackageDescription`，则此属性还可用作包的说明。 |
| `Copyright` | 包的版权详细信息。 |
| `PackageRequireLicenseAcceptance` | 一个布尔值，指定客户端是否必须提示使用者接受包许可证后才可安装包。 默认值为 `false`。 |
| `DevelopmentDependency` | 一个布尔值，用于指定包是否被标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中。 在 `PackageReference` (NuGet 4.8 +) 中，此标志还意味着编译时资产将从编译中排除。 有关详细信息，请参阅 [PackageReference 的 DevelopmentDependency 支持](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)。 |
| `PackageLicenseExpression` | [SPDX 许可证标识符](https://spdx.org/licenses/)或表达式，例如 `Apache-2.0` 。 有关详细信息，请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。 |
| `PackageLicenseFile` | 如果使用的是未分配 SPDX 标识符的自定义许可证或许可证，则为包内的许可证文件的路径。 |
| `PackageLicenseUrl` | `PackageLicenseUrl` 已弃用。 请改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。 |
| `PackageProjectUrl` | |
| `PackageIcon` | 指定相对于包根的包图标路径。 有关详细信息，请参阅对 [图标图像文件进行打包](#packing-an-icon-image-file)。 |
| `PackageReleaseNotes` | 包的发行说明。 |
| `PackageReadmeFile` | 包的自述文件。 |
| `PackageTags` | 标记的分号分隔列表，这些标记用于指定包。 |
| `PackageOutputPath` | 确定用于已打包的包的输出路径。 默认值为 `$(OutputPath)`。 |
| `IncludeSymbols` | 此布尔值指示在打包项目时，包是否应创建一个附加的符号包。 符号包的格式由 `SymbolPackageFormat` 属性控制。 有关详细信息，请参阅 [IncludeSymbols](#includesymbols)。 |
| `IncludeSource` | 此布尔值指示包进程是否应创建源包。 源包中包含库的源代码以及 PDB 文件。 源文件置于生成的包文件中的 `src/ProjectName` 目录下。 有关详细信息，请参阅 [IncludeSource](#includesource)。 |
| `PackageType` | |
| `IsTool` | 指定是否将所有输出文件复制到 *tools* 文件夹，而不是 *lib* 文件夹。 有关详细信息，请参阅 [IsTool](#istool)。 |
| `RepositoryUrl` | 用于克隆或检索源代码的存储库 URL。 示例： *https://github.com/ NuGet / NuGet 。客户端*。 |
| `RepositoryType` | 存储库类型。 示例： `git` (默认) ， `tfs` 。 |
| `RepositoryBranch` | 可选存储库分支信息。 还必须指定 `RepositoryUrl` 才能包含此属性。 示例： *master* (NuGet 4.7.0 +) 。 |
| `RepositoryCommit` | 可选的存储库提交或更改集，指示针对其生成包的源。 还必须指定 `RepositoryUrl` 才能包含此属性。 示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。 |
| `SymbolPackageFormat` | 指定符号包的格式。 如果是 "nupkg"，则会使用 *nupkg* 扩展（其中包含 Pdb、dll 和其他输出文件）创建旧的符号包。 如果是 "snupkg"，则会创建包含可移植 Pdb 的 snupkg 符号包。 默认值为 "nupkg"。 |
| `NoPackageAnalysis` | 指定 `pack` 不应在生成包后运行包分析。 |
| `MinClientVersion` | 指定 NuGet 可安装此包的客户端的最低版本，由 nuget.exe 和 Visual Studio 包管理器强制执行。 |
| `IncludeBuildOutput` | 此布尔值指定是否应将生成输出程序集打包到 .nupkg 文件中  。 |
| `IncludeContentInPack` | 此布尔值指定是否 `Content` 自动在生成的包中包含类型为的任何项。 默认为 `true`。 |
| `BuildOutputTargetFolder` | 指定放置输出程序集的文件夹。 输出程序集（和其他输出文件）会复制到各自的框架文件夹中。 有关详细信息，请参阅 [输出程序集](#output-assemblies)。 |
| `ContentTargetFolders` | 指定不为其指定所有内容文件的默认位置 `PackagePath` 。 默认值为“content;contentFiles”。 有关详细信息，请参阅[在包中包含内容](#including-content-in-a-package)。 |
| `NuspecFile` | 用于打包的文件的相对路径或绝对路径 *.nuspec* 。 如果已指定，则将 **专用** 于打包信息，并且不使用项目中的任何信息。 有关详细信息，请参阅[使用 .nuspec 打包](#packing-using-a-nuspec-file)。 |
| `NuspecBasePath` | 文件的基路径 *.nuspec* 。 有关详细信息，请参阅[使用 .nuspec 打包](#packing-using-a-nuspec-file)。 |
| `NuspecProperties` | 键=值对的分号分隔列表。 有关详细信息，请参阅[使用 .nuspec 打包](#packing-using-a-nuspec-file)。 |

## <a name="pack-scenarios"></a>包方案

### <a name="suppressing-dependencies"></a>抑制依赖项

若要从生成的包中取消包依赖项 NuGet ，请将设置 `SuppressDependenciesWhenPacking` 为， `true` 这样将允许跳过生成的 nupkg 文件中的所有依赖项。

### `PackageIconUrl`

`PackageIconUrl` 对属性的支持已弃用 [`PackageIcon`](#packageicon) 。 从 NuGet 5.3 和 Visual Studio 2019 版本16.3 开始， `pack` 如果包元数据仅指定了，则会引发 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。

### `PackageIcon`

> [!Tip]
> 若要保持与尚不支持的客户端和源的向后兼容性 `PackageIcon` ，请同时指定 `PackageIcon` 和 `PackageIconUrl` 。 Visual Studio 支持来自 `PackageIcon` 基于文件夹的源的包。

#### <a name="packing-an-icon-image-file"></a>打包图标图像文件

打包图标图像文件时，请使用 `PackageIcon` 属性来指定图标文件路径，该路径相对于包的根。 此外，请确保该文件已包含在包中。 图像文件大小限制为 1 MB。 支持的文件格式包括 JPEG 和 PNG。 建议使用128x128 的图像分辨率。

例如：

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[包图标示例](https://github.com/NuGet/Samples/tree/main/PackageIconExample)。

对于 nuspec 等效项，请查看[ nuspec 图标的参考](nuspec.md#icon)。

### <a name="packagereadmefile"></a>PackageReadmeFile

打包自述文件时，需要使用 `PackageReadmeFile` 属性来指定包路径，相对于包的根。 除此之外，还需要确保文件已包含在包中。 支持的文件格式仅包括 Markdown (*md*) 。

例如：

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

对于 nuspec 等效项，请查看[ nuspec 自述文件参考](nuspec.md#readme)。

### <a name="output-assemblies"></a>输出程序集

`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。 复制的输出文件取决于 MSBuild 从目标提供的内容 `BuiltOutputProjectGroup` 。

你 MSBuild  可以在项目文件或命令行中使用两个属性来控制输出程序集的位置：

- `IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。
- `BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。 输出程序集（和其他输出文件）会复制到各自的框架文件夹中。

### <a name="package-references"></a>包引用

请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)

### <a name="project-to-project-references"></a>项目到项目的引用

默认情况下，项目到项目引用被视为 NuGet 包引用。 例如：

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

也可将以下元数据添加到项目引用：

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>在包中添加内容

若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。 默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

如果只想将所有内容复制到 (s) 的特定根文件夹 (而不是 `content` 和 `contentFiles` 这两) ，则可以使用 MSBuild 属性 `ContentTargetFolders` ，默认值为 "content; contentFiles"，但可以设置为任何其他文件夹名称。 请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。

`PackagePath` 可以是一组以分号分隔的目标路径。 指定空的包路径会将文件添加到包的根目录。 例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

还有一个 MSBuild 属性 `$(IncludeContentInPack)` ，默认值为 `true` 。 如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。

您可以对上述任何项设置的其他包特定元数据包括 ```<PackageCopyToOutput>``` 和在 ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` 输出中的项上设置和值 ```contentFiles``` nuspec 。

> [!Note]
> 除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。
>
> 使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。

### <a name="includesymbols"></a>IncludeSymbols

使用 `MSBuild -t:pack -p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。 请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。

### <a name="includesource"></a>IncludeSource

这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。 类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。 对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。

如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。

### <a name="packing-a-license-expression-or-a-license-file"></a>打包许可证表达式或许可证文件

使用许可证表达式时，请使用 `PackageLicenseExpression` 属性。 有关示例，请参阅 [许可证表达式示例](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

若要了解有关 org 所接受的许可证表达式和许可证的详细信息 NuGet ，请参阅 [许可证元数据](nuspec.md#license)。

打包许可证文件时，请使用 `PackageLicenseFile` 属性来指定包路径，相对于包的根。 此外，请确保该文件已包含在包中。 例如：

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

有关示例，请参阅 [许可证文件示例](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)。

> [!NOTE]
> `PackageLicenseExpression`一次只能指定、和中的一个 `PackageLicenseFile` `PackageLicenseUrl` 。

### <a name="packing-a-file-without-an-extension"></a>打包不带扩展名的文件

在某些情况下（如打包许可证文件时），可能需要包含不带扩展名的文件。
出于历史原因，请 NuGet  &  MSBuild 将不带扩展名的路径视为目录。

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[不带扩展的文件示例](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)。

### <a name="istool"></a>IsTool

使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。 请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。

### <a name="packing-using-a-nuspec-file"></a>使用文件打包 `.nuspec`

尽管建议你改为在项目文件中包含通常在文件中的 [所有属性](../reference/msbuild-targets.md#pack-target) `.nuspec` ，但你可以选择使用 `.nuspec` 文件打包项目。 对于使用的非 SDK 样式项目 `PackageReference` ，必须导入， `NuGet.Build.Tasks.Pack.targets` 以便可以执行 pack 任务。 你仍需要还原项目，然后才能打包 nuspec 文件。 默认情况下，SDK 样式项目 (包含包目标。 ) 

项目文件的目标框架不相关，并且不会在打包时使用 nuspec 。 以下三个 MSBuild 属性与使用打包相关 `.nuspec` ：

1. `NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。
1. `NuspecProperties`：键=值对的分号分隔列表。 由于 MSBuild 命令行分析的工作方式，必须按如下所示指定多个属性： `-p:NuspecProperties="key1=value1;key2=value2"` 。  
1. `NuspecBasePath`：`.nuspec` 文件的基路径。

如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 打包项目，请使用类似于下面的命令：

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

请注意， nuspec 默认情况下，使用 dotnet.exe 或 msbuild 打包会导致生成项目。 可以通过将属性传递给 dotnet.exe 来避免这种情况，这与项目文件中的 ```--no-build``` 设置 ```<NoBuild>true</NoBuild> ``` 以及项目文件中的设置等效 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。

用于打包文件的 *.csproj* 文件的示例 nuspec 如下：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>用于创建自定义包的高级扩展点

`pack`目标提供两个扩展点，这些点在内部特定于目标框架的生成中运行。 扩展点支持包括特定于目标框架的内容和程序集到包中：

- `TargetsForTfmSpecificBuildOutput` 目标：用于文件夹内的文件 `lib` 或使用指定的文件夹 `BuildOutputTargetFolder` 。
- `TargetsForTfmSpecificContentInPackage` 目标：用于之外的文件 `BuildOutputTargetFolder` 。

#### `TargetsForTfmSpecificBuildOutput`

编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificBuildOutput)` 。 对于任何需要在 `BuildOutputTargetFolder` 默认情况下进入 (lib 的文件) ，目标应将这些文件写入 ItemGroup， `BuildOutputInPackage` 并设置以下两个元数据值：

- `FinalOutputPath`：文件的绝对路径;如果未提供，则标识用于计算源路径。
- `TargetPath`：当文件需要进入中的子文件夹时， (可选) 设置 `lib\<TargetFramework>` ，如位于其各自区域性文件夹下的附属程序集。 默认为文件的名称。

示例：

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### `TargetsForTfmSpecificContentInPackage`

编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificContentInPackage)` 。 对于要包含在包中的任何文件，目标应将这些文件写入 ItemGroup `TfmSpecificPackageFile` ，并设置以下可选的元数据：

- `PackagePath`：应在包中输出文件的路径。 NuGet 如果将多个文件添加到同一个包路径，则会发出警告。
- `BuildAction`：要分配给文件的生成操作，只有当包路径在文件夹中时才是必需的 `contentFiles` 。 默认值为 "None"。

示例：
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>还原目标

`MSBuild -t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：

1. 读取所有项目到项目的引用
1. 读取项目属性以查找中间文件夹和目标框架
1. MSBuild将数据传递到 NuGet.Build.Tasks.dll
1. 运行还原
1. 下载包
1. 编写资产文件、目标和属性

`restore`目标适用于使用 PackageReference 格式的项目。
`MSBuild 16.5+` 还具有对格式的 [选择支持](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` 。

> [!NOTE]
> `restore`目标[不应](#restoring-and-building-with-one-msbuild-command)与目标组合运行 `build` 。

### <a name="restore-properties"></a>还原属性

其他还原设置可能来自 MSBuild 项目文件中的属性。 还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。

| 属性 | 说明 |
|--------|--------|
| `RestoreSources` | 以分号分隔的包源列表。 |
| `RestorePackagesPath` | 用户包文件夹路径。 |
| `RestoreDisableParallel` | 将下载限制为一次一个。 |
| `RestoreConfigFile` | 要应用的 `Nuget.Config` 文件的路径。 |
| `RestoreNoCache` | 如果为 true，则避免使用缓存的包。 请参阅 [管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| `RestoreIgnoreFailedSources` | 如果为“true”，则忽略失败或丢失的包源。 |
| `RestoreFallbackFolders` | 后备文件夹，其使用方式与使用 "用户包" 文件夹的方式相同。 |
| `RestoreAdditionalProjectSources` | 要在还原期间使用的其他源。 |
| `RestoreAdditionalProjectFallbackFolders` | 要在还原期间使用的其他回退文件夹。 |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | 排除其中指定的回退文件夹 `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | `NuGet.Build.Tasks.dll` 的路径。 |
| `RestoreGraphProjectInput` | 要还原的以分号分隔的项目列表，其中应包含绝对路径。 |
| `RestoreUseSkipNonexistentTargets`  | 如果通过它收集项目，则会 MSBuild 确定是否使用优化进行收集 `SkipNonexistentTargets` 。 如果未设置，则默认为 `true` 。 如果无法导入项目的目标，则结果是一个故障快速的行为。 |
| `MSBuildProjectExtensionsPath` | Output 文件夹，默认为 `BaseIntermediateOutputPath` 和 `obj` 文件夹。 |
| `RestoreForce` | 在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。 指定此标志与删除 `project.assets.json` 文件类似。 这不会绕过 http 缓存。 |
| `RestorePackagesWithLockFile` | 选择使用锁定文件。 |
| `RestoreLockedMode` | 在锁定模式下运行还原。 这意味着，还原将不会重新评估依赖关系。 |
| `NuGetLockFilePath` | 锁定文件的自定义位置。 默认位置为项目旁边，名为 `packages.lock.json` 。 |
| `RestoreForceEvaluate` | 强制执行还原，重新计算依赖项并更新锁定文件，而不会出现任何警告。 |
| `RestorePackagesConfig` | 一种选择使用开关，用 packages.config 还原项目。仅支持 `MSBuild -t:restore` 。 |
| `RestoreUseStaticGraphEvaluation` | 选择使用静态图形 MSBuild 计算而不是标准计算。 静态图形评估是一项试验性功能，它对于大型存储库和解决方案的速度显著提高。 |

#### <a name="examples"></a>示例

命令行：

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

项目文件：

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>还原输出

还原会在生成 `obj` 文件夹中创建以下文件：

| 文件 | 说明 |
|--------|--------|
| `project.assets.json` | 包含所有包引用的依赖项关系图。 |
| `{projectName}.projectFileExtension.nuget.g.props` | 对 MSBuild 包中包含的属性的引用 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 对 MSBuild 包中包含的目标的引用 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>通过一个命令还原和生成 MSBuild

由于 NuGet 可以还原会导致目标和属性的包的事实 MSBuild ，还原和生成计算将以不同的全局属性运行。
这意味着，以下操作将具有不可预测且通常不正确的行为。

```cli
msbuild -t:restore,build
```

 相反，推荐的方法是：

```cli
msbuild -t:build -restore
```

相同的逻辑也适用于类似于的其他目标 `build` 。

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>还原 PackageReference 和 packages.config 项目 MSBuild

对于 MSBuild 16.5 +，还支持 packages.config `msbuild -t:restore` 。

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore 仅适用于 `MSBuild 16.5+` ，而不适用于 `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>恢复 MSBuild 静态图形计算

> [!NOTE]
> 使用 MSBuild 16.6 +， NuGet 已添加了一个试验性功能，可通过命令行使用静态图形计算，从而大幅缩短大型存储库的还原时间。

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

也可以通过设置属性中的属性来启用它。

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> 从 Visual Studio 2019. x 和1.x 版 NuGet ，此功能被视为实验性并选择加入。 有关默认情况下何时启用此功能的详细信息，请参阅[ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) 。

静态图形还原更改还原的 msbuild 部分、项目读取和评估，但不更改还原算法！ NuGet (NuGet .exe、 MSBuild .exe、dotnet.exe 和 Visual Studio) 的所有工具都是相同的。

在极少数情况下，静态图形还原的行为可能与当前还原不同，并且某些声明的 PackageReferences 或 Projectreference 可能已丢失。

若要轻松地在迁移到静态图形时进行一次检查，请考虑运行：

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet*不* 应报告任何更改。 如果看不到差异，请在[ NuGet /Home](https://github.com/nuget/home/issues/new)中进行操作。

### <a name="replacing-one-library-from-a-restore-graph"></a>从还原图中替换一个库

如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。 首先使用顶级 `PackageReference`，排除所有资产：

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

接下来，将自己的引用添加到适当的 DLL 本地副本：

```xml
<Reference Include="Newtonsoft.Json.dll" />
```