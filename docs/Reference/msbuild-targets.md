---
title: 作为 MSBuild 目标的 NuGet 包和还原 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
keywords: NuGet 和 MSBuild, NuGet 包目标, NuGet 还原目标
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>作为 MSBuild 目标的 NuGet 包和还原

NuGet 4.0+

使用 PackageReference 格式，NuGet 4.0+ 可以将所有清单元数据直接存储在项目文件中，而不是使用单独的 `.nuspec` 文件。

如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。 借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。 （对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令。）

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

## <a name="pack-target"></a>包目标

对于标准.NET 项目使用 PackageReference 格式，并使用`msbuild /t:pack`绘制从项目文件以在创建 NuGet 包时使用的输入。

下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。 在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。 为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。

请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。

| 属性/NuSpec 值 | MSBuild 属性 | 默认 | 说明 |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | MSBuild 的 $(AssemblyName) |
| 版本 | PackageVersion | 版本 | 这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | 空 | 设置 PackageVersion 会覆盖 PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | 空 | MSBuild 的 $(VersionSuffix)。 设置 PackageVersion 会覆盖 PackageVersionSuffix |
| 作者 | 作者 | 当前用户的用户名 | |
| Owners | 不可用 | NuSpec 中不存在 | |
| 标题 | 标题 | PackageId| |
| 描述 | PackageDescription | “包描述” | |
| Copyright | Copyright | 空 | |
| requireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | 空 | |
| ProjectUrl | PackageProjectUrl | 空 | |
| IconUrl | PackageIconUrl | 空 | |
| Tags | PackageTags | 空 | 使用分号分隔标记。 |
| ReleaseNotes | PackageReleaseNotes | 空 | |
| 存储库/Url | RepositoryUrl | 空 | 用于克隆或检索源代码存储库 URL。 示例： *https://github.com/NuGet/NuGet.Client.git* |
| 存储库/类型 | RepositoryType | 空 | 存储库类型。 示例： *git*， *tfs*。 |
| 存储库/分支 | RepositoryBranch | 空 | 可选存储库分支信息。 *RepositoryUrl*还必须指定要包含此属性。 示例： *master* (NuGet 4.7.0+) |
| 存储库/提交 | RepositoryCommit | 空 | 针对构建的可选的存储库提交或变更集以指示哪些源包。 *RepositoryUrl*还必须指定要包含此属性。 示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| 总结 | 不支持 | | |

### <a name="pack-target-inputs"></a>包目标输入

- IsPackable
- PackageVersion
- PackageId
- 作者
- 描述
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
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

### <a name="packageiconurl"></a>PackageIconUrl

更改的一部分[NuGet 问题 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最终将更改为`PackageIconUri`和可以是到图标文件，它将包括在得到的包的根目录的相对路径。

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

使用 `MSBuild /t:pack /p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。 请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。

### <a name="includesource"></a>IncludeSource

这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。 类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。 对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。

如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。

### <a name="istool"></a>IsTool

使用 `MSBuild /t:pack /p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。 请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。

### <a name="packing-using-a-nuspec"></a>使用 .nuspec 打包

你可以使用`.nuspec`文件打包你的项目，前提是具有一个 SDK 项目文件导入`NuGet.Build.Tasks.Pack.targets`，以便可以执行包任务。 你仍需要将项目还原之前可以包 nuspec 文件。 项目文件的目标框架是不相关和封装 nuspec 时不使用。 以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：

1. `NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。
1. `NuspecProperties`：键=值对的分号分隔列表。 由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。  
1. `NuspecBasePath`：`.nuspec` 文件的基路径。

如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 打包项目，请使用类似于下面的命令：

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

请注意，封装 nuspec 使用 dotnet.exe 或 msbuild 也会导致到默认情况下生成项目。 这可以避免通过传递```--no-build```dotnet.exe，等同于设置属性```<NoBuild>true</NoBuild> ```在项目文件中，以及设置```<IncludeBuildOutput>false</IncludeBuildOutput> ```项目文件中

是要包 nuspec 文件的 csproj 文件的示例：

```
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

### <a name="advanced-extension-points-to-create-customized-package"></a>高级扩展点，以创建自定义的程序包

`pack`目标提供了两个扩展点，在内部，目标 framework 特定生成中运行。 包括目标框架特定内容和程序集放在一个程序包支持的扩展点：

- `TargetsForTfmSpecificBuildOutput` 目标： 用于中的文件`lib`文件夹或使用指定的文件夹`BuildOutputTargetFolder`。
- `TargetsForTfmSpecificContentInPackage` 目标： 用于外部文件`BuildOutputTargetFolder`。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

编写自定义的目标和指定的值为`$(TargetsForTfmSpecificBuildOutput)`属性。 需要转到任何文件`BuildOutputTargetFolder`(默认情况下的为 lib)，目标应将这些文件写入到 ItemGroup`BuildOutputInPackage`并设置以下两个元数据值：

- `FinalOutputPath`: 该文件; 绝对路径如果未提供，标识用于评估源路径。
- `TargetPath`: （可选) 时该文件必须转到子文件夹内设置`lib\<TargetFramework>`，像在其各自的区域性文件夹下，该转到附属程序集一样。 默认值为文件的名称。

示例:

```
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

编写自定义的目标和指定的值为`$(TargetsForTfmSpecificContentInPackage)`属性。 对于要在包中包含任何文件，目标应写入这些文件 ItemGroup`TfmSpecificPackageFile`并设置以下可选元数据：

- `PackagePath`： 该文件应在包中的输出路径。 如果多个文件添加到相同的包路径，NuGet 将发出警告。
- `BuildAction`: 生成操作以分配给文件，仅当时才需要的包路径中`contentFiles`文件夹。 默认值为"None"。

示例：
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a>还原目标

`MSBuild /t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：

1. 读取所有项目到项目的引用
1. 读取项目属性以查找中间文件夹和目标框架
1. 将 msbuild 数据传递到 NuGet.Build.Tasks.dll
1. 运行还原
1. 下载包
1. 编写资产文件、目标和属性

`restore`目标工作原理**仅**对于使用 PackageReference 格式的项目。 与其**不**工作的项目使用`packages.config`进行格式设置; 使用[nuget 还原](../tools/cli-ref-restore.md)相反。

### <a name="restore-properties"></a>还原属性

其他的还原设置可能来自项目文件中的 MSBuild 属性。 还可以从命令行使用 `/p:` 开关设置值（请参阅以下示例）。

| 属性 | 描述 |
|--------|--------|
| RestoreSources | 以分号分隔的包源列表。 |
| RestorePackagesPath | 用户包文件夹路径。 |
| RestoreDisableParallel | 将下载限制为一次一个。 |
| RestoreConfigFile | 要应用的 `Nuget.Config` 文件的路径。 |
| RestoreNoCache | 如果为 true，则避免使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| RestoreIgnoreFailedSources | 如果为“true”，则忽略失败或丢失的包源。 |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` 的路径。 |
| RestoreGraphProjectInput | 要还原的以分号分隔的项目列表，其中应包含绝对路径。 |
| RestoreOutputPath | 输出文件夹，默认为 `obj` 文件夹。 |

#### <a name="examples"></a>示例

命令行：

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

项目文件：

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>还原输出

还原会在生成 `obj` 文件夹中创建以下文件：

| 文件 | 描述 |
|--------|--------|
| `project.assets.json` | 包含的所有包引用的依赖项关系图。 |
| `{projectName}.projectFileExtension.nuget.g.props` | 包中包含的对 MSBuild 属性的引用 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 包中包含的对 MSBuild 目标的引用 |

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
