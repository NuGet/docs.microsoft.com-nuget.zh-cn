---
title: 作为 MSBuild 目标的 NuGet 包和还原
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510790"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>作为 MSBuild 目标的 NuGet 包和还原

NuGet 4.0+

使用[PackageReference](../consume-packages/package-references-in-project-files.md)格式，NuGet 4.0 + 可以直接将所有清单元数据存储在项目文件中，而不是使用单独的 @no__t 1 文件。

如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。 借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。 有关使用 MSBuild 创建 NuGet 包的说明，请参阅[使用 Msbuild 创建 nuget 包](../create-packages/creating-a-package-msbuild.md)。 （对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令。）

## <a name="target-build-order"></a>目标生成顺序

由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。 例如，假设希望在打包后将包复制到网络共享。 此操作可通过向项目文件中添加以下内容来完成：

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。

> [!NOTE]
> @no__t 是相对的，需要从项目根目录运行命令。

## <a name="pack-target"></a>包目标

对于使用 PackageReference 格式的 .NET Standard 项目，使用 @no__t 从项目文件中绘制输入，以用于创建 NuGet 包。

下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。 在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。 为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。

请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。

| 属性/NuSpec 值 | MSBuild 属性 | Default | 注意 |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | MSBuild 的 $(AssemblyName) |
| Version | PackageVersion | Version | 这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | 空 | 设置 PackageVersion 会覆盖 PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | 空 | MSBuild 的 $(VersionSuffix)。 设置 PackageVersion 会覆盖 PackageVersionSuffix |
| Authors | Authors | 当前用户的用户名 | |
| Owners | 不可用 | NuSpec 中不存在 | |
| Title | Title | PackageId| |
| 描述 | 描述 | “包描述” | |
| Copyright | Copyright | 空 | |
| requireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| 照 | PackageLicenseExpression | 空 | 对应于 `<license type="expression">` |
| 照 | PackageLicenseFile | 空 | 对应到 `<license type="file">`。 可能需要显式打包所引用的许可证文件。 |
| LicenseUrl | PackageLicenseUrl | 空 | `PackageLicenseUrl` 已弃用，请使用 PackageLicenseExpression 或 PackageLicenseFile 属性 |
| ProjectUrl | PackageProjectUrl | 空 | |
| 图标 | PackageIcon | 空 | 可能需要显式打包所引用的图标图像文件。|
| IconUrl | PackageIconUrl | 空 | `PackageIconUrl` 已弃用，请使用 PackageIcon 属性 |
| Tags | PackageTags | 空 | 使用分号分隔标记。 |
| ReleaseNotes | PackageReleaseNotes | 空 | |
| 存储库/Url | RepositoryUrl | 空 | 用于克隆或检索源代码的存储库 URL。 示例： *https://github.com/NuGet/NuGet.Client.git* |
| 存储库/类型 | RepositoryType | 空 | 存储库类型。 示例： *git*、 *tfs*。 |
| 存储库/分支 | RepositoryBranch | 空 | 可选存储库分支信息。 还必须为此属性指定要包含的*RepositoryUrl* 。 示例： *master* （NuGet 4.7.0 +） |
| 存储库/提交 | RepositoryCommit | 空 | 可选存储库提交或变更集，以指示生成包时所依据的源。 还必须为此属性指定要包含的*RepositoryUrl* 。 示例： *0e4d1b598f350b3dc675018d539114d1328189ef* （NuGet 4.7.0 +） |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| 总结 | 不支持 | | |

### <a name="pack-target-inputs"></a>包目标输入

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Authors
- 描述
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>包方案

### <a name="suppress-dependencies"></a>禁止依赖项

若要取消生成的 NuGet 包中的包依赖项，请将 `SuppressDependenciesWhenPacking` 设置为 `true`，这将允许跳过生成的 nupkg 文件中的所有依赖项。

### <a name="packageiconurl"></a>PackageIconUrl

> [!Important]
> & Visual Studio 2019 版本 16.3 + 不推荐使用 PackageIconUrl。 改用[PackageIcon](#packing-an-icon-image-file) 。

### <a name="packing-an-icon-image-file"></a>打包图标图像文件

打包图标图像文件时，需要使用 PackageIcon 属性来指定相对于包根的包路径。 此外，还需要确保文件已包含在包中。 图像文件大小限制为 1 MB。 支持的文件格式包括 JPEG 和 PNG。 建议使用64x64 的图像分辨率。

例如:

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

[包图标示例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。

对于 nuspec 等效项，请查看[图标的 nuspec 参考](nuspec.md#icon)。

### <a name="output-assemblies"></a>输出程序集

`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。 复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。

在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：

- `IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。
- `BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。 输出程序集（和其他输出文件）会复制到各自的框架文件夹中。

### <a name="package-references"></a>包引用

请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)

### <a name="project-to-project-references"></a>项目到项目的引用

默认情况下，项目到项目的引用被视为 nuget 包引用，例如：

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

如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。 请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。

`PackagePath` 可以是一组以分号分隔的目标路径。 指定空的包路径会将文件添加到包的根目录。 例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。 如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。

其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。

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

使用许可证表达式时，应使用 PackageLicenseExpression 属性。 
[许可证表达式示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[了解有关 NuGet.org 所接受的许可证表达式和许可证的详细信息](nuspec.md#license)。

打包许可证文件时，需要使用 PackageLicenseFile 属性来指定相对于包根的包路径。 此外，还需要确保文件已包含在包中。 例如:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[许可证文件示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。

### <a name="istool"></a>IsTool

使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。 请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。

### <a name="packing-using-a-nuspec"></a>使用 .nuspec 打包

尽管建议你在项目文件中包含通常位于 @no__t 1 文件中的[所有属性](../reference/msbuild-targets.md#pack-target)，但你可以选择使用 @no__t 2 文件来打包你的项目。 对于使用 `PackageReference` 的非 SDK 样式项目，必须导入 `NuGet.Build.Tasks.Pack.targets`，以便可以执行包任务。 你仍需要还原项目，然后才能打包 nuspec 文件。 （默认情况下，SDK 样式项目包括包目标。）

项目文件的目标框架不相关，并且不会在对 nuspec 进行打包时使用。 以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：

1. `NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。
1. `NuspecProperties`：键=值对的分号分隔列表。 由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。  
1. `NuspecBasePath`：`.nuspec` 文件的基路径。

如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 打包项目，请使用类似于下面的命令：

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

请注意，使用 dotnet 或 msbuild 打包 nuspec 在默认情况下也会导致生成项目。 可以通过将 ```--no-build``` 属性传递给 dotnet 来避免这种情况，这相当于在项目文件中设置 ```<NoBuild>true</NoBuild> ```，以及在项目文件中设置 @no__t。

用于打包 nuspec 文件的 *.csproj*文件的示例如下：

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

@No__t 的目标提供两个扩展点，它们在内部特定于目标框架的生成中运行。 扩展点支持包括特定于目标框架的内容和程序集到包中：

- `TargetsForTfmSpecificBuildOutput` target：用于 @no__t 1 文件夹内的文件或使用 `BuildOutputTargetFolder` 指定的文件夹。
- `TargetsForTfmSpecificContentInPackage` target：用于 @no__t 以外的文件。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

编写一个自定义目标并将其指定为 `$(TargetsForTfmSpecificBuildOutput)` 属性的值。 对于需要进入 `BuildOutputTargetFolder` （默认情况下为 lib）的任何文件，目标应将这些文件写到 ItemGroup `BuildOutputInPackage` 中，并设置以下两个元数据值：

- `FinalOutputPath`：文件的绝对路径;如果未提供，则标识用于计算源路径。
- `TargetPath`：（可选）当文件需要进入 `lib\<TargetFramework>` 内的子文件夹时设置，如在其各自的区域性文件夹下的附属程序集。 默认为文件的名称。

示例:

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

编写一个自定义目标并将其指定为 `$(TargetsForTfmSpecificContentInPackage)` 属性的值。 对于要包含在包中的任何文件，目标应将这些文件写入 ItemGroup `TfmSpecificPackageFile` 并设置以下可选的元数据：

- `PackagePath`：应在包中输出文件的路径。 如果将多个文件添加到同一个包路径，NuGet 将发出警告。
- `BuildAction`：要分配给文件的生成操作，只有当包路径在 @no__t 1 文件夹中时才是必需的。 默认值为 "None"。

例如：
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
1. 将 MSBuild 数据传递到 NuGet。生成 .dll
1. 运行还原
1. 下载包
1. 编写资产文件、目标和属性

@No__t-0 目标**仅**适用于使用 PackageReference 格式的项目。 它不适**用于**使用 `packages.config` 格式的项目;请改用[nuget 还原](../reference/cli-reference/cli-ref-restore.md)。

### <a name="restore-properties"></a>还原属性

其他的还原设置可能来自项目文件中的 MSBuild 属性。 还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。

| Property | 描述 |
|--------|--------|
| RestoreSources | 以分号分隔的包源列表。 |
| RestorePackagesPath | 用户包文件夹路径。 |
| RestoreDisableParallel | 将下载限制为一次一个。 |
| RestoreConfigFile | 要应用的 `Nuget.Config` 文件的路径。 |
| RestoreNoCache | 如果为 true，则避免使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| RestoreIgnoreFailedSources | 如果为“true”，则忽略失败或丢失的包源。 |
| RestoreFallbackFolders | 后备文件夹，其使用方式与使用 "用户包" 文件夹的方式相同。 |
| RestoreAdditionalProjectSources | 要在还原期间使用的其他源。 |
| RestoreAdditionalProjectFallbackFolders | 要在还原期间使用的其他回退文件夹。 |
| RestoreAdditionalProjectFallbackFoldersExcludes | 排除 @no__t 中指定的回退文件夹 |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` 的路径。 |
| RestoreGraphProjectInput | 要还原的以分号分隔的项目列表，其中应包含绝对路径。 |
| RestoreUseSkipNonexistentTargets  | 通过 MSBuild 收集项目后，它将确定是否使用 `SkipNonexistentTargets` 优化来收集这些项目。 如果未设置，则默认为 `true`。 如果无法导入项目的目标，则结果是一个故障快速的行为。 |
| MSBuildProjectExtensionsPath | Output 文件夹，默认为 `BaseIntermediateOutputPath` 和 @no__t 1 文件夹。 |
| RestoreForce | 在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。 指定此标志与删除 `project.assets.json` 文件类似。 这不会绕过 http 缓存。 |
| RestorePackagesWithLockFile | 使用锁定文件。 |
| RestoreLockedMode | 在锁定模式下运行还原。 这意味着，还原将不会重新评估依赖关系。 |
| NuGetLockFilePath | 锁定文件的自定义位置。 默认位置为项目旁边，名为 `packages.lock.json`。 |
| RestoreForceEvaluate | 强制执行还原，重新计算依赖项并更新锁定文件，而不会出现任何警告。 | 

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

| 文件 | 描述 |
|--------|--------|
| `project.assets.json` | 包含所有包引用的依赖项关系图。 |
| `{projectName}.projectFileExtension.nuget.g.props` | 包中包含的对 MSBuild 属性的引用 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 包中包含的对 MSBuild 目标的引用 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>通过一个 MSBuild 命令进行还原和生成

由于 NuGet 可以还原引入 MSBuild 目标和属性的包，因此，还原和生成评估将以不同的全局属性运行。
这意味着，以下操作将具有不可预测且通常不正确的行为。

```cli
msbuild -t:restore,build
```

 相反，推荐的方法是：

```cli
msbuild -t:build -restore
```

相同的逻辑也适用于与 `build` 类似的其他目标。

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。 旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。 也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。

例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。 如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

若要声明项目中所有目标的回退，请停止 `Condition` 属性。 还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

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
